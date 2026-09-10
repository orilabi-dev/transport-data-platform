# ADR 0001: Branching Strategy

- **Status:** Accepted
- **Date:** 2026-09-10
- **Decision owners:** orilabi-dev

## Context

A branching strategy defines how changes are developed, reviewed and integrated into the repository. The strategy should support the project's development workflow while remaining proportionate to the size and complexity of the team.

TDP is currently in the early stages of development, with features being developed iteratively towards a working product. The project is maintained by a small team and is not currently operating multiple long-lived deployment environments.

The chosen strategy should therefore prioritize:

- Fast iteration and development
- Clear separation between stable and in-progress work
- Low operational and maintenance overhead
- The ability to review changes before they reach `main`
- A workflow that can evolve as the project grows

## Decision

TDP will use a **feature branching strategy**.

The `main` branch will represent the stable version of the project. New work will be developed on short-lived feature branches created from `main` and merged back through pull requests.

Branches should follow the naming convention:

```text
feature/<short-description>
```

For example:

```text
feature/transport-data-ingestion
feature/add-cdc-pipeline
feature/implement-data-quality-tests
```

Feature branches should remain focused on a single change or piece of functionality and should be merged into `main` once the work is complete and the relevant checks have passed.

The `main` branch will be protected against direct pushes. Changes should be integrated through pull requests with automated checks enforced before merging.

This approach provides a balance between development speed, code review and repository stability without introducing the additional complexity of multiple long-lived branches.

## Options Considered

### Trunk-Based Development

Trunk-based development centres around a single shared branch, typically `main`, with developers integrating small and frequent changes into the trunk. Short-lived branches may still be used for individual changes.

**Advantages**

- Simple repository structure
- Encourages small, frequent integrations
- Low branch maintenance overhead
- Reduces long-lived branch divergence

**Disadvantages**

- Requires strong automated testing and CI/CD practices
- Incomplete features may require additional techniques such as feature flags
- Less separation between independent pieces of work

**Decision:** Not selected at this stage. TDP is still establishing its automated testing and CI/CD capabilities, so feature branches provide a useful additional layer of isolation while the platform is being developed.

### Released Branching

Released branching maintains branches around specific releases or versions rather than individual features.

**Advantages**

- Provides clear separation between releases
- Makes maintaining previous releases easier
- Useful for projects that support multiple versions simultaneously

**Disadvantages**

- Adds branch management overhead
- Slower iteration cycles
- More appropriate for projects that maintain multiple released versions
- Unnecessary complexity for the current stage of TDP

**Decision:** Not selected. TDP is expected to iterate frequently and does not currently need to maintain multiple released versions.

### Fork Strategy

The fork workflow allows contributors to create their own copy of the repository, make changes and submit pull requests back to the upstream repository.

**Advantages**

- Well suited to open-source projects
- Provides strong separation between contributors and the upstream repository
- Maintainers retain control over the main repository

**Disadvantages**

- Adds unnecessary workflow overhead for a small internal team
- Primarily designed for external contributors
- Requires additional repository management

**Decision:** Not selected. TDP is currently developed within a small team and does not require the contributor isolation provided by a fork-based workflow.

### Git Flow

Git Flow uses multiple long-lived branches, typically including `main` and `develop`, alongside feature, release and hotfix branches.

**Advantages**

- Provides clear separation between development and released code
- Supports formal release cycles
- Useful for projects with scheduled releases and multiple supported versions

**Disadvantages**

- More complex branch management
- Longer-lived branches can diverge from one another
- Slower integration and iteration
- Introduces processes that are unnecessary for the current stage of TDP

**Decision:** Not selected. Protecting `main` does not require Git Flow. Branch protection, pull requests and automated CI checks provide sufficient protection while keeping the development workflow simpler.

### Environment Branching

Environment branching maintains separate branches for deployment environments, such as `development`, `testing` and `staging`.

**Advantages**

- Provides clear separation between deployment environments
- Can support environment-specific validation and release workflows
- Allows changes to progress through environments before reaching production

**Disadvantages**

- High branch and deployment management overhead
- Can cause branches to diverge
- Can make synchronising changes between environments more complicated
- Requires multiple persistent environments to provide meaningful value

**Decision:** Not selected. TDP is currently designed as a locally deployable platform and does not require multiple persistent deployment environments. Environment separation can be introduced later if the project's deployment requirements change.

## Consequences

This decision establishes feature branching as the default development workflow for TDP.

The strategy should be revisited if the project grows significantly, introduces multiple contributors or deployment environments, or requires a more formal release management process.

### Positive

- Faster iteration and development
- Clear separation between stable and in-progress work
- Changes can be reviewed before being merged into `main`
- Low branch management overhead
- Simple workflow appropriate for the current team size
- Can evolve towards a different strategy as project requirements change

### Negative / Trade-offs

- Provides less isolation than strategies using dedicated environment or development branches
- Relies on CI/CD and automated testing to maintain the stability of `main`
- Feature branches can still become problematic if they remain open for long periods
- Does not provide dedicated branches for managing multiple released versions

## References

- [Atlassian — Git branching strategies](https://www.atlassian.com/git/tutorials/comparing-workflows)
- [Trunk Based Development](https://trunkbaseddevelopment.com/)
