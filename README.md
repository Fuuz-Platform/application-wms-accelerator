# application-wms-accelerator

> **Fuuz Industrial Operations Platform — Warehouse Management System**
> Package Version: `2.0.0` | Platform Version: `2025.12.1` | Spec: `2.0.0`

The **WMS** accelerator is a production-ready Warehouse Management System built on the [Fuuz Industrial Operations Platform](https://fuuz.com). It delivers end-to-end warehouse operations management — from inbound receiving and putaway through inventory control, order fulfillment, wave picking, and shipping — built on an ISA-95-compliant site hierarchy.

This package contains **33 modules** across **12 functional areas**, **46 data flows**, **72 data models**, **56 screens**, and **32 seed data records**.

---

## Table of Contents

1. [Overview](#overview)
2. [Module Structure](#module-structure)
3. [Functional Areas](#functional-areas)
4. [Data Flows](#data-flows)
5. [Data Models](#data-models)
6. [Screens](#screens)
7. [Access Control](#access-control)
8. [Package Contents](#package-contents)
9. [Dependencies](#dependencies)
10. [Installation](#installation)

---

## Overview

The WMS accelerator provides the foundational and operational infrastructure for warehouse management, including:

- **Receiving** — Purchase order-based receipt processing with status lifecycle (Pending Confirmation → Confirmed / Canceled), exception handling, and inventory creation on confirmation
- **Inventory Management** — Real-time inventory tracking by storage unit, lot, and serial number; inventory status management (Ok, Hold, Damaged, Lost, Retired); inventory transactions including moves, splits, and merges
- **Order Fulfillment** — Outbound order processing with full status lifecycle (New → Pending Fulfillment → Partial Fulfillment → Fulfilled / Cancelled), wave picking for grouped order execution, and packing/shipping workflows
- **Cycle Counting** — Scheduled and ad-hoc inventory counts with status workflow (New → Started → Completed / Cancelled) and variance management
- **Site Management** — ISA-95-compliant facility hierarchy (Site → Area → Line → Cell) for location-based inventory and operational organization
- **System Platform** — Access control, configuration, IoT integration, scheduling, orchestration, data modeling, business intelligence, and application lifecycle management

---

## Module Structure

| Module Group | Modules |
|---|---|
| **Applications** | Application Connector, Application Lifecycle Management, Application Trace |
| **Customer Relationship Management** | Sales |
| **Human Capital Management** | Employees |
| **Inventory Management** | Cycle Counting, Inventory Tracking |
| **Materials Management** | Inventory, Logistics, Storage Management |
| **Order Fulfillment** | Order Processing, Order Tracking, Wave Picking |
| **Product Data Management** | Engineering, Materials, Quality |
| **Production Management** | Advanced Production Scheduling, Customer Management, Kanban Production, Manufacturing, Planning, Product Data Management, Supplier Management, Work Order Management |
| **Receiving** | Order Receiving |
| **Site Management** | Site Management |
| **Supply Chain Management** | Procurement |
| **System** | Access Control, Application Setup, Configuration, Dashboard, Data Management, Data Modeling, Files, Integration, Internet of Things, Orchestration, Scheduling, Testing |

---

## Functional Areas

### Receiving

Inbound shipment processing with exception management:

- **Order Receiving** — PO-linked receipt creation and confirmation workflow; receipt status lifecycle: Pending Confirmation → Confirmed / Canceled; inventory record creation upon receipt confirmation; receipt line-level quantity tracking
- **Receipt Exception Handling** — Capture and classify inbound exceptions (damage, quantity discrepancy, wrong item); exception reason code management with configurable resolution workflows
- **Putaway** — Location assignment and directed putaway based on site hierarchy and storage rules

### Inventory Management

Real-time inventory visibility and control:

- **Inventory Tracking** — Real-time inventory balance visibility by storage unit, location, lot, and serial number; inventory status lifecycle management: Ok, Hold, Damaged, Lost, Retired
- **Inventory Transactions** — Full transaction audit trail for all inventory movements:
  - **Inventory Move** — Transfer inventory from one storage unit to another
  - **Inventory Split** — Split quantity from an existing inventory record into a new record
  - **Inventory Merge** — Consolidate quantity from one inventory record into an existing record
- **Cycle Counting** — Scheduled and ad-hoc cycle counts with count status lifecycle: New → Started → Completed / Cancelled; variance capture and approval workflow; location-based count task assignment

### Order Fulfillment

Outbound order management and execution:

- **Order Processing** — Outbound order management with full status lifecycle: New → Pending Fulfillment → Partial Fulfillment → Fulfilled / Cancelled; order line and release-level tracking; pick, pack, and ship execution
- **Order Tracking** — Real-time visibility into open orders, order lines, and releases for outbound shipments; order progress monitoring and exception management
- **Wave Picking** — Group multiple orders into pick waves for efficient warehouse floor execution; wave release and assignment to warehouse operators; pick confirmation and quantity verification

### Site Management

ISA-95-compliant facility hierarchy:

- **Site Management** — Define and manage the complete ISA-95 equipment hierarchy: Site → Area → Line → Cell; location-based inventory assignment and operational zone management; foundation for directed putaway rules and inventory location tracking

### Materials Management

Inventory and logistics operations shared with MES:

- **Inventory** — Inventory balance tracking by location and lot/serial with transaction history
- **Storage Management** — Location hierarchy, bin/rack/shelf assignment, and storage rule configuration
- **Logistics** — Material movement workflows including transfers and inter-facility logistics

### Product Data Management

Engineering and specification master data:

- **Engineering** — Engineering change management and revision-controlled engineering data
- **Materials** — Material master data with specifications and procurement parameters
- **Quality** — Quality specification management linked to inspection plans

### Supply Chain Management

Procurement operations:

- **Procurement** — Purchase order management, receiving integration, supplier performance tracking, and procurement approval workflows

### System Platform

Core platform infrastructure and administration:

- **Access Control** — Role-based access management, permission assignment, and user provisioning
- **Configuration** — System-wide settings including reason codes, unit-of-measure tables, and lookup tables
- **Scheduling** — Background job scheduling for automated flow execution and maintenance triggers
- **Orchestration** — Multi-step workflow orchestration for complex cross-module business processes
- **Internet of Things** — Device registry, tag mapping, and real-time data ingestion from sensors and SCADA systems
- **Integration** — Generic integration framework for external system connectivity
- **Data Modeling** — Platform-level data model management and schema configuration
- **Business Intelligence** — Configurable analytics and reporting with dashboard builder
- **Application Lifecycle Management** — Package versioning, deployment, and environment promotion workflows

---

## Data Flows

The package includes **46 data flow files** organized by functional area:

| Flow Type | Examples |
|---|---|
| **System (Scheduled)** | Inventory balance recalculation; cycle count task generation; order status transition automation |
| **System (Background)** | Receipt confirmation inventory creation; wave release processing; order fulfillment status updates |
| **Screen** | UI-driven flows for receipt entry, inventory moves, count recording, order processing, and wave picking |
| **Integration** | ERP purchase order sync; outbound shipment confirmation; inventory transaction export |

Flow types used across the package:
- **System** — Backend/scheduled business logic, data processing, and automated state management
- **Screen** — User-interface-triggered flows responding to operator actions and form submissions
- **Integration** — External system connectors for ERP, carrier, and trading partner integration

---

## Data Models

The package includes **72 data model files** spanning all functional areas:

**Receiving** — Receipt, ReceiptLine, ReceiptException, ReceiptStatus, ReceiptExceptionReason

**Inventory** — Inventory, InventoryTransaction, StorageUnit, StorageUnitStatus, InventoryStatus, TransactionType, Lot, Serial

**Order Fulfillment** — Order, OrderLine, OrderLineRelease, OrderStatus, OrderType, OrderLineReleaseStatus, OrderLineReleaseType, Wave, WaveLine, PickTask

**Cycle Counting** — CycleCount, CycleCountLine, CountStatus, CountVariance

**Site** — Site, Area, Line, Cell, Location

**System** — Configuration, Sequence, ApplicationSetting, AuditLog, FileAttachment, IoTDevice, IoTTag, IntegrationMapping

---

## Screens

The package includes **56 screen files** providing warehouse operational interfaces:

- Inbound receiving screens with receipt creation, line entry, and confirmation workflows
- Receipt exception capture and resolution screens
- Inventory management screens with status, location, and transaction visibility
- Inventory move, split, and merge transaction entry screens
- Order management and fulfillment tracking dashboards
- Wave creation, release, and pick task execution screens
- Cycle count initiation, count entry, and variance review screens
- Site hierarchy management and location configuration screens
- System configuration and administration panels

---

## Access Control

The package establishes core warehouse roles:

| Role | Description |
|---|---|
| WMS Administrator | Full system access including configuration and module management |
| Warehouse Manager | Full warehouse operations management and reporting |
| Warehouse Supervisor | Order release, wave management, and operator oversight |
| Warehouse Operator | Directed warehouse tasks: receive, pick, move, count |
| Inventory Analyst | Inventory management, cycle counts, adjustments, and reporting |
| Receiving Clerk | Inbound receipt processing and exception handling |
| System Administrator | User management, access control, and integration configuration |

---

## Package Contents

```
wms/
├── manifest.json          # Package metadata (version 2.0.0)
├── definition.json        # Package structure and selection definitions
├── package-data.json      # All seed data (modules, config, lookup tables)
├── data/                  # 32 seed data files
├── dataFlows/             # 46 data flow definitions
├── dataModels/            # 72 data model definitions
└── screens/               # 56 screen definitions
```

The **32 seed data records** establish the foundational warehouse configuration:
- Complete module group and module registry (12 groups, 33 modules)
- Order status lifecycle values: New, Pending Fulfillment, Partial Fulfillment, Fulfilled, Cancelled
- Receipt status lifecycle values: Pending Confirmation, Confirmed, Canceled
- Inventory status values: Ok, Hold, Damaged, Lost, Retired
- Inventory transaction types: Inventory Move, Inventory Split, Inventory Merge
- Cycle count status values: New, Started, Completed, Cancelled
- Order type definitions (Purchase) with extensibility for additional types
- Sequence number configuration for orders, receipts, and counts

---

## Dependencies

| Dependency | Version | Required |
|---|---|---|
| Fuuz Industrial Operations Platform | `>= 2025.12.1` | Required |
| `application-mes-core-accelerator` | any | Optional (shared modules) |

> **Note:** This is the standalone WMS package. It includes shared modules (Production Management, Materials Management, Supply Chain) that overlap with `application-mes-core-accelerator`. If deploying alongside the full MES suite, coordinate module registry seeding to avoid duplicate entries. For a complete production-and-warehouse deployment, see `application-mes-accelerator`.

---

## Installation

1. Ensure your Fuuz platform instance is running version `>= 2025.12.1`
2. Navigate to **Platform > Packages** in your Fuuz tenant
3. Import the `wms` package (`.fuuz` file or directory import)
4. Run the module registry seeding flows to populate module group and module tables
5. Configure the ISA-95 site hierarchy (Site → Area → Line → Cell) for your facility
6. Assign roles and users per the Access Control section above
7. Apply system configuration defaults appropriate for your facility
8. Configure order type and status lookup tables for your operational workflows
9. Set up ERP integration credentials if synchronizing purchase orders and inventory
10. Validate the deployment by processing a test receipt end-to-end

For detailed setup and configuration documentation, see the [Fuuz Platform Documentation](https://help.fuuz.com).

## Service levels

No service level agreement applies to anything published here. It becomes a supported
deliverable only once it has been implemented by a Fuuz services professional or an
approved Fuuz partner.
