# Hello, it's Aggie

## SmartHome App

### Documentiation

1. [Purpose](docs/purpose.md)
2. [Architecture Considerations](docs/architecture.md)
3. Validation - precommits, code review, best practices - To be considered and documented.

### File structure

    Infrastructure/
    ├── modules/             # reusable Terraform modules
    ├── envs/
    │   ├── dev/
    │   │   └── terragrunt.hcl
    │   └── prod/
    │       └── terragrunt.hcl
    ├── main.tf              # could be minimal, calls modules
    ├── variables.tf
    ├── outputs.tf
    ├── Makefile             # terraform/terragrunt commands
    ├── .pre-commit-config.yaml
    └── README.md

    Ingestion/
    ├── pipelines/           # JSON / ARM templates for ADF pipelines
    ├── datasets/
    ├── linked-services/
    ├── scripts/             # deployment scripts (Az CLI,PowerShell)
    ├── Makefile             # deploy, validate commands
    ├── .pre-commit-config.yaml
    └── README.md

    DatabricksResources/
    ├── notebooks/           # python notebooks
    ├── jobs/                # job configs
    ├── src/                 # supporting Python scripts
    ├── tests/               # unit tests for scripts
    ├── Makefile             # test, lint, deploy
    ├── requirements.txt
    ├── .pre-commit-config.yaml
    └── README.md

    DBT/
    ├── models/              # DBT models
    ├── macros/
    ├── seeds/
    ├── tests/
    ├── dbt_project.yml
    ├── profiles.yml.example # template for dev/production
    ├── Makefile             # run dbt commands
    ├── .pre-commit-config.yaml
    └── README.md

### Important links

1. [visual design - Miro](https://miro.com/app/board/uXjVJnn1rDU=/)
