# Transport Data Platform

TDP is a production-style, locally deployable data platform ingesting static, streaming and CDC data, with automated transformation, orchestration, testing and deployment.

## Objective

TDP is a portfolio project designed to demonstrate the end-to-end design and implementation of a production-style data engineering platform.

The objective is to build a realistic, locally deployable data platform that demonstrates how modern data engineering practices can be applied to ingest, process, transform, test, orchestrate and deploy transport data across multiple data sources and processing patterns.

The project focuses on demonstrating practical engineering principles, including:

- Ingestion of static, streaming and change data capture (CDC) data.
- Data transformation and modelling.
- Workflow orchestration and dependency management.
- Automated data quality testing.
- Reproducible local development and deployment.
- Infrastructure and environment management.
- Monitoring, observability and operational reliability.
- CI/CD and software engineering best practices.

Rather than focusing on a single tool or technology, the project aims to demonstrate how these components can be designed and integrated into a cohesive, maintainable data platform.

## Status

Early-stage development. The initial repository structure and branching strategy have been established, with architectural and engineering decisions documented in `docs/decisions`.

## Usage

Start the local containers

```python
make containers-up
```
