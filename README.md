# catalog-inventory-api

Catalog Inventory is the bounded context that owns scarce stock in Arcadia Editions.
Following the center-of-gravity heuristic from the bounded contexts article, this
service exists because stock reservation changes independently, enforces its own
rules, and emits its own facts.

In the Place Order flow this context answers questions such as:

- Can this limited edition SKU still be reserved?
- Which order is currently holding that stock?
- When must reserved stock be released back to the pool?
- How does backoffice replenish or adjust inventory positions?

This repository contains the service-level specifications used to describe that
inventory boundary and generate the API and event contracts around it.

## Bounded context scope

- Reservation flow: reserve stock, release stock, and publish stock outcomes
- Inventory operations: create stock positions, receive stock, and adjust balances
- Ownership of reservation lifecycle and release reasons
- Ownership of inventory counts for available, reserved, and sold quantities

This service does not own product merchandising data such as title, artwork, or
price. Those belong to Product Catalog.

## Contents

- `domain-model.zdl`: source of truth for aggregates, commands, lifecycle, and events
- `asyncapi.yml`: AsyncAPI contract generated from the ZDL model
- `openapi.yml`: HTTP API contract generated from the ZDL model
- `avro/`: Avro event schemas referenced by the AsyncAPI document
- `.github/workflows/provision-kafka.yml`: workflow entrypoint for shared Kafka provisioning
- `scripts/run-kafka-pipeline-local.sh`: local Git Bash helper for the same generate and Terraform flow

## Main domain elements

- `StockReservation`: aggregate for scarce inventory claims made during checkout
- `InventoryPosition`: aggregate for backoffice inventory balances per SKU
- `InventoryService`: reservation API and event-driven release handling
- `InventoryBackofficeService`: stock intake and adjustment operations

## Local usage

From Git Bash, after exporting the required Terraform and Confluent environment variables:

```bash
./scripts/run-kafka-pipeline-local.sh develop
```

To apply the generated Terraform locally:

```bash
APPLY_MODE=true ./scripts/run-kafka-pipeline-local.sh develop
```
