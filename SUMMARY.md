# Catalog Inventory

## Description

Catalog Inventory is the bounded context that owns scarce stock in Arcadia
Editions. It protects edition availability by deciding whether a customer can
claim a copy, holding that copy during checkout, and releasing it when the order
does not complete.

It also supports backoffice inventory operations by tracking how much stock is
available, reserved, sold, received, or adjusted for each SKU.

## Scope

- Reserve stock for an order during checkout
- Release reserved stock when payment or scheduling fails
- Track reservation lifecycle and release reasons
- Maintain inventory positions for available, reserved, and sold quantities
- Support stock intake and manual stock adjustments in backoffice flows

## Main domain elements

- `StockReservation`: aggregate for scarce inventory claims made during checkout
- `InventoryPosition`: aggregate for backoffice inventory balances per SKU
- `InventoryService`: reservation API and event-driven release handling
- `InventoryBackofficeService`: stock intake and adjustment operations
