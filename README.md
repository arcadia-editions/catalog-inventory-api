# catalog-inventory-api

AsyncAPI-first service repository for the Arcadia Editions inventory contracts.

## Contents

- [SUMMARY.md](./SUMMARY.md): bounded context description, scope, and main domain elements
- [CHANGELOG.md](./CHANGELOG.md): documentation change history for this repository
- [domain-model.zdl](./domain-model.zdl): source of truth for aggregates, commands, lifecycle, and events
- [asyncapi.yml](./asyncapi.yml): AsyncAPI contract generated from the ZDL model
- [openapi.yml](./openapi.yml): HTTP API contract generated from the ZDL model
- [avro/](./avro/): Avro event schemas referenced by the AsyncAPI document
- [.github/workflows/provision-kafka.yml](./.github/workflows/provision-kafka.yml): workflow entrypoint for shared Kafka provisioning
- [scripts/run-kafka-pipeline-local.sh](./scripts/run-kafka-pipeline-local.sh): local Git Bash helper for the same generate and Terraform flow

## Local usage

From Git Bash, after exporting the required Terraform and Confluent environment variables:

```bash
./scripts/run-kafka-pipeline-local.sh develop
```

To apply the generated Terraform locally:

```bash
APPLY_MODE=true ./scripts/run-kafka-pipeline-local.sh develop
```
