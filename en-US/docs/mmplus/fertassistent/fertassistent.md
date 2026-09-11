---
title: Anwenderhandbuch m+m Production Order Assistant
---

# m+m Production Order Assistant User Guide

The **m+m Production Order Assistant** (in the user interface: **Prod. Assistant**) connects sales with manufacturing in Microsoft Dynamics 365 Business Central. From a sales line in a **Sales Quote** or **Sales Order**, a matching **production order** is created in just a few steps – either manually via a guided dialog or automatically upon order release. In addition, the module keeps the link between the sales document and the production order transparent through an **order reference** and a **Check Status**.

This guide describes the setup, the daily work, and the typical processes. All field, action, and page names correspond to the German user interface (with the English UI captions given here).

## Introduction

### Purpose of the Module

The Prod. Assistant automates and simplifies the creation of production orders from sales. It ensures that a production order keeps the same reference as the triggering sales line (**Prod. Target Type**, **Prod. Target No.**, **Prod. Target Line No.**), that the responsible salesperson is informed about new production orders, and that converting a quote into an order is only possible once the linked production orders have been checked from a business perspective.

### Target Audience

The primary target audience is **operational users in Sales and Production Planning** who record, release, and trigger production orders from sales documents on a daily basis, and who maintain their **Check Status**. Secondarily, the **Setup** chapter is aimed at **administrators and key users** who define the company-wide defaults once.

### Short Process Overview

The typical path runs along the sales document up to the production order:

1. The user records an item line in the **Sales Quote** or **Sales Order**.
2. On the sales line, the **Create PO** field controls whether a production order should be created for this line.
3. Via the **Prod. Assistant** action on the sales line, the user opens a guided dialog and creates the production order with a **Routing** and **Components** – or the production order is created automatically upon **release** of the sales order.
4. The created production order carries a **Check Status** and an **order reference** to the sales line; the salesperson is notified if required.
5. When a quote is converted into an order, the production order moves along and receives the status intended for orders.

## Quick Start for Users

The following sequence follows the technical dependency: first the **setup**, then the daily work on the sales document.

**A. One-time setup (administrator).** Using **Search**, open the **Prod. Assistent Setup** page and define at least: **Prod. Order Status f. Sales Quote** and **Prod. Order Status f. Sales Order**, whether **Create Prod. Order on Sales Order Release** should be active, and how **Prefill Create Prod. Order in Sales Lines** takes effect.

**B. Manual creation in the sales document (user).**

1. Open the **Sales Order** (or the **Sales Quote**) and record an item line.
2. On the line, check the **Create PO** field (prefilled by default according to setup).
3. On the sales line, choose the **Prod. Assistant** action.
4. In the dialog, review and complete **Quantity**, **Routing No.**, **Due Date**, as well as the **Routing** and **Components** tabs.
5. Confirm the dialog with **OK**. The production order is created, receives the **Prod. Order Status** intended in setup as well as a **Check Status**, and the salesperson is notified – if activated.

**C. Automatic creation upon release (user).**

1. In setup, activate **Create Prod. Order on Sales Order Release**.
2. Release the **Sales Order**.
3. If **Confirm Create Prod. Order on Sales Order Release** is active, answer the prompt **"Create Production Order?"** with **Yes**.
4. For each item line with **Create PO** = activated, a production order is created in the **Prod. Order Status f. Sales Order**.

## Setup

Setup is done centrally on the **Prod. Assistent Setup** page. It is a company-wide single-record setup: Business Central creates the record automatically when the page is first opened.

**Access:** Open the **Prod. Assistent Setup** page via **Search**. This page is filed under **Administration** and has no parent master data page that calls it; access via **Search** is therefore the intended way.

All fields of the page are located on the **General** tab. Because this is a pure setup table of the module, all visible fields are documented below – there are no additional base fields on this screen.

### Basic Settings of the Prod. Assistent Setup

**Who sets up and when:** An administrator or key user defines these values once before first use. They control both the manual creation via the **Prod. Assistant** (see *Daily Work*) and the automatic creation upon release.

| Setting | Explanation |
|---|---|
| **Prod. Order Status f. Sales Quote** | When set, a production order created from a **Sales Quote** receives exactly this status. Allowed values are **Simulated**, **Planned**, **Firm Planned**, and **Released**; **Finished** is not allowed and is rejected. The value must not be higher than **Prod. Order Status f. Sales Order**, otherwise an error message appears. This lets the administrator ensure that quotes trigger only a less binding production stage than confirmed orders. |
| **Prod. Order Status f. Sales Order** | When set, a production order created from a **Sales Order** receives this status – including automatic creation during release and when converting a quote into an order. Allowed values are **Simulated**, **Planned**, **Firm Planned**, **Released** (not **Finished**). The value must be at least as high as **Prod. Order Status f. Sales Quote**. |
| **Set Confirm Status for Prod. Order Check** | When activated, the newly created production order immediately receives the **Check Status "Confirmed"** after the dialog is confirmed; if the field is not set, the production order starts with **Check Status "Open"** and must be checked manually later. This decides whether a quote can be converted into an order without further checking (see *Check Status verification*). |
| **Reset Sales Quote Prod. Order Formula** | When a date formula is stored, it serves as a default for the period after which production orders from expired **Sales Quotes** should be reset or cleaned up; without a date formula, there is no such time-based default. |
| **Notify Salesperson by Status Change** | When activated, the responsible user receives the notification **"Show Production Order"** when a production order is created from the sales document, with the note that the Check Status still needs to be set; if the field is not set, this message is omitted and the user must track new production orders themselves. |
| **Create Prod. Order on Sales Order Release** | When activated, upon **release** of a sales order Business Central automatically creates a production order for each item line with **Create PO** = activated; if the field is not set, production orders are created only manually via the **Prod. Assistant** action. |
| **Confirm Create Prod. Order on Sales Order Release** | When activated, the prompt **"Create Production Order?"** appears first upon order release; the production orders are created only after confirmation with **Yes**. This lets the user skip the automatic creation in individual cases. This field requires that **Create Prod. Order on Sales Order Release** is activated. |
| **Prefill Create Prod. Order in Sales Lines** | Controls the prefilling of the line field **Create PO** on new item lines. With **All**, **Create PO** is automatically activated on new item lines; with **None**, it stays deactivated and the user activates it selectively per line. Non-inventory item types are always excluded. |
| **Create Prod. Order on Sales Order For Special Order** | When activated, sales lines flagged as **Special Order** may also trigger a production order; if the field is not set, the Prod. Assistant blocks such lines (check for **Special Order** = No), and during automatic creation Special Order lines are skipped. |
| **Delete assigned Prod. Order on Sales Order delete** | When activated, when a sales line is deleted the assigned production orders are handled as well: without existing item or capacity ledger entries, the production order is deleted; with existing entries, the prompt appears instead asking whether only the **link** should be removed. If the field is not set, production orders remain unchanged when the sales line is deleted. |

#### Value Range "Prod. Order Status" (Option)

The two status fields use the standard production order statuses, but without **Finished**:

- **Simulated:** The production order is created as a non-binding simulation – suitable for quotes and calculations, without firm scheduling.
- **Planned:** The production order is created as planned; it flows into demand planning but is not yet firm planned.
- **Firm Planned:** The production order is firm planned and reserves capacity; production is not yet released.
- **Released:** The production order is released for production; postings in production are possible.
- **Finished:** not allowed – the selection is rejected with an error message, because the assistant must not create an already completed order.

### Setting Up Automatic Prod. Order Creation Upon Order Release

**Process intro:** This capability allows all required production orders to be created upon release of a sales order without an additional click. It is set up by the administrator before first use and takes effect in daily work when releasing orders (see *Daily Work in the Sales Document*).

Set up the chain in dependency order:

1. **Check master data:** First, the affected items must be manufacturable (items with a **Routing No.** and a production BOM). If this master data is missing, no production order can be calculated.
2. **Set the global field:** Activate **Create Prod. Order on Sales Order Release**. When activated, Business Central checks the order lines upon every release.
3. **Optionally activate the prompt:** Activate **Confirm Create Prod. Order on Sales Order Release** if the user should confirm the automatic creation per release. When activated, **"Create Production Order?"** appears.
4. **Define the target status:** Set **Prod. Order Status f. Sales Order**. When set, all automatically created production orders are created in exactly this status.
5. **Special case Special Order:** Activate **Create Prod. Order on Sales Order For Special Order** if Special Order lines should also be considered; otherwise they are skipped upon release.
6. **Align prefilling:** Set **Prefill Create Prod. Order in Sales Lines** so that only the desired lines carry an active **Create PO** – only these trigger a production order upon release.

**Operational conclusion:** The user releases the sales order; for each line with **Create PO** = activated, a production order is created. Lines that are already linked are not served twice.

### Setting Up Manual Prod. Order Creation via the Prod. Assistant

**Process intro:** For the manual, guided creation in the sales document, the administrator defines in which status the production order is created and how the Check Status is prefilled. The user later triggers the creation via the **Prod. Assistant** action on the sales line (see *Daily Work in the Sales Document*).

1. **Define the target status per document type:** Set **Prod. Order Status f. Sales Quote** and **Prod. Order Status f. Sales Order**. When set, the production order created via the dialog receives the status matching the document type.
2. **Choose the check default:** Activate **Set Confirm Status for Prod. Order Check** if the production order should immediately count as **Confirmed**; otherwise it starts as **Open** and must be checked before the quote-to-order conversion.
3. **Activate the notification:** Activate **Notify Salesperson by Status Change** so that the user receives the **"Show Production Order"** message after creation.

**Operational conclusion:** The user chooses **Prod. Assistant** on the sales line, reviews **Quantity**, **Routing No.**, and **Due Date** in the dialog, and confirms with **OK**.

### Setting Up Cleanup of Production Orders

**Process intro:** These settings determine how production orders are handled whose triggering sales line is deleted or whose quote expires. They protect against orphaned production orders and against deleting orders that have already been posted.

1. **Activate the delete behavior:** Activate **Delete assigned Prod. Order on Sales Order delete**. When activated, assigned production orders are handled as well when the sales line is deleted.
2. **Observe ledger entry protection:** If item or capacity ledger entries already exist for the production order, it is not deleted; instead the prompt **"Ledger Entries already exist … Unassign the link …?"** appears. If the user confirms, the production order remains and only the **order reference** is removed; if they decline, the delete operation is canceled.
3. **Store the quote deadline:** Maintain **Reset Sales Quote Prod. Order Formula** to specify a deadline for cleaning up production orders from expired quotes.

**Operational conclusion:** The user deletes a sales line or the quote – the production orders are deleted, unlinked, or cleaned up accordingly.

## Daily Work in the Sales Document

The actual usage takes place in the **sales lines** of the **Sales Order** and **Sales Quote**. These areas are controlled by the central **Prod. Assistent Setup**: there the administrator defines the prefilling of **Create PO**, the target statuses, the Check Status default, the notification, and the automatic creation upon release (see *Setup*). In case of unexpected behavior, always check this setup first.

### Sales Line: Field and Action

On the sales lines (header via the standard sales document, lines via the subform), the module adds one field and one action.

| Field / Action | Explanation |
|---|---|
| **Create PO** (field) | When activated, this item line is considered for automatic production order creation upon order release; if deactivated, no production order is created for the line upon release. The field is prefilled on new lines according to **Prefill Create Prod. Order in Sales Lines** and is editable only on inventory item lines (deactivated automatically for other types). |
| **Prod. Assistant** (action) | Via the **Prod. Assistant** action, open the guided dialog for the current sales line. When executed, the module checks item type, item no., quantity, and drop shipment, creates a simulated production order, and shows it for review. Prerequisite: the line quantity is not yet fully assigned to other production orders – otherwise a note appears stating that the sales line quantity has already been completely assigned. |

### "Prod. Assistant" Dialog

The **Prod. Assistant** dialog is the guided form for reviewing and creating the production order. It is opened exclusively via the action of the same name on the sales line.

In the header area (**General** tab), you review and change the central values:

| Field | Explanation |
|---|---|
| **Item No.** | Shows the item to be produced (not editable); serves to verify that the correct item is being manufactured. |
| **Description** / **Description 2** | Show the item text of the production order (not editable). |
| **Quantity** | When you change the quantity, the production order is recalculated: the underlying production order takes over the quantity and the components are re-determined. This way the production quantity matches the required sales quantity. |
| **Routing No.** | When you change the routing, the production order is recalculated with the operations of the new routing; this lets you control the production path directly from the dialog. |
| **Routing Version Code** | When you choose a different routing version, the production order is recalculated based on this version. |
| **Due Date** | When you change the due date, the ending date is re-determined from the item's lead time and the production order is rescheduled; this way you align the production date with the delivery date. |

The dialog contains two subtabs and an infobox. They are each described in a separate section below.

#### "Routing" Tab

The **Routing** tab shows the operations of the production order (production order routing lines). The user can review and adjust dates and times per operation; changes update the display immediately.

| Field | Explanation |
|---|---|
| **Operation No.** | Number of the operation; determines the sequence in production. |
| **Type** / **No.** | Define the capacity of the operation (work center or machine center and its number); this determines where the operation is produced. |
| **Description** | Text of the operation. |
| **Starting Date/Time** / **Ending Date/Time** | When you change the starting or ending time, the scheduling of the operation is updated and the display is recalculated. |
| **Setup Time** / **Run Time** / **Wait Time** / **Move Time** | When you change one of these times, the capacity need and the scheduling of the operation are recalculated. |
| **Expected Capacity Need** | Shows the expected capacity need of the operation, converted to the work center's unit of measure – for controlling utilization. |
| *Additional fields hidden by default* | The routing additionally contains hidden detail fields (including Previous/Next Operation No., Routing Link Code, Fixed Scrap Quantity, Scrap Factor %, Send-Ahead Quantity, Concurrent Capacities, Unit Cost per, Lot Size, expected costs, operation status, location, and bins for production). They serve fine control and are shown when needed. |

Additional actions are available for the operations: **Comments**, **Tools**, **Personnel**, **Quality Measures**, **Allocated Capacity**, and **Order Tracking**. With **Allocated Capacity** you see the scheduled capacity needs of the operation; **Order Tracking** shows the triggering demands.

#### "Components" Tab

The **Components** tab shows the production order components. Here the user reviews and maintains the required material. Changes to quantity- or inventory-relevant fields automatically trigger a reservation for items configured accordingly.

| Field | Explanation |
|---|---|
| **Item No.** | Component item; on change – depending on the item – a reservation is made automatically. |
| **Due Date** | Demand date of the component. |
| **Description** | Text of the component. |
| **Quantity per** | When you change the quantity per, the material need is re-determined and, if applicable, re-reserved. |
| **Expected Quantity** | Shows the total expected component quantity for the production order. |
| **Remaining Quantity** | Shows the still open, unconsumed component quantity. |
| **Unit of Measure Code** | Unit of measure of the component; on change a re-reservation is made. |
| **Flushing Method** | Controls how the component is consumed/posted (e.g. manually or automatically upon posting). |
| **Bin Code** | Take-from bin of the component. |
| **Substitution Available** | Indicates whether a substitute item is stored for the component. |
| *Additional fields hidden by default* | Additionally present (hidden): Variant Code, Due Date/Time, Scrap %, Calculation Formula, Length/Width/Weight/Depth, Reserved Quantity, cost fields, position fields, Lead-Time Offset, picked quantity, dimension codes, Routing Link Code. They serve detailed calculation and are shown when needed. |

Actions on the **Components** tab:

- **Reserve** – reserves inventory for the component. With the statuses **Simulated** and **Planned**, reservation is not possible; a note appears stating that components with this status cannot be reserved.
- **Select Item Substitution** – selects a substitute item and then reserves automatically.
- **Item Tracking Lines** – records lot and serial numbers of the component.
- **Item Availability by** (Event, Period, Variant, Location, Lot, BOM Level) – checks the availability of the component item.
- **Bin Contents**, **Put-away/Pick Lines/Movement Lines** – show inventory stock and warehouse activities for the component.
- **Dimensions**, **Comments**, **Order Tracking**, **Print** (pick list).

#### "Components Lots & Serials" Infobox

The **Components Lots & Serials** infobox shows the reserved item tracking information for the selected component, consolidated per lot/serial number.

| Field | Explanation |
|---|---|
| **Lot No.** | Reserved lot number of the component. |
| **Serial No.** | Reserved serial number of the component. |
| **Quantity** | Total quantity reserved for this lot/serial number. |

## Production Orders Across All Statuses

The created production order is a **standard production order**; the module extends it with reference and status information. These extensions appear uniformly across all four status variants – **Simulated Production Order**, **Planned Production Order**, **Firm Planned Production Order**, and **Released Production Order** – each on the **card**, in the **list**, and in the **prod. order lines**.

### Additional Fields on Card and List

| Field | Explanation |
|---|---|
| **Check Status** | Shows the business check status of the production order. In particular, it controls whether a quote may be converted into an order (see *Check Status verification*). The values are explained below. |
| **Sell-to Customer No.** | Shows the customer number of the sales order linked via the **order reference** (derived field). This way the production user recognizes for which customer production is happening. |
| **Sell-to Customer Name** | Shows the associated customer name (derived). |

### Additional Fields in the Prod. Order Lines

In addition to **Check Status**, **Sell-to Customer No.**, and **Sell-to Customer Name**, the **prod. order lines** show the full order reference:

| Field | Explanation |
|---|---|
| **Prod. Target Type** | Shows whether the reference is to a **Sales Quote** or a **Sales Order** (or **(blank)** if no reference exists). From this the module derives the check and conversion logic. |
| **Prod. Target No.** | Shows the document number of the linked sales document (not editable). |
| **Prod. Target Line No.** | Shows the line number of the linked sales line (not editable). |
| **Sell-to Customer No.** / **Sell-to Customer Name** | Derived customer information for the linked sales line. |

#### Value Range "Check Status" (Option)

- **(blank):** No check status is set yet (initial state without a reference).
- **Open:** The production order is created but not yet checked from a business perspective; a quote-to-order conversion is not yet allowed.
- **In Progress:** The check is running; the conversion is still not allowed.
- **Confirmed:** The production order is checked and released; only with this status may the associated sales quotes be converted into orders.
- **Refused:** The production order was refused; a conversion is not allowed.

### "Delete Order Reference" Action (Prod. Order Lines)

In the **prod. order lines** of the **Simulated**, **Planned**, **Firm Planned**, and **Released** statuses, the **Delete Order Reference** action is available.

When you run **Delete Order Reference**, the reference of the prod. order line to the sales document is removed (**Prod. Target Type** is set to **(blank)**, number and line number are cleared) and existing reservations of the prod. order line are canceled. Afterwards a message appears stating that the order reference has been removed. If no reference exists, the system reports that no order reference exists. Use the action when a production order should remain but be decoupled from the sales document.

## Notification and Check Status Workflow

### "Show Production Order" Notification

If **Notify Salesperson by Status Change** is activated, the user receives a notification after a production order is created from the sales document, with the note that the production order has been created and the **Check Status** still needs to be set. Via the **Show Production Order** action in the notification, the user opens the production order directly on the page matching the status.

### Check Status Verification for Quote → Order

When converting a **Sales Quote** into a **Sales Order**, the module checks all item lines: if a line has a linked production order with **Check Status** **Open**, **In Progress**, or **Refused**, the conversion is canceled with the note that all lines must have a **"Confirmed"** Check Status. Only when all linked production orders are **Confirmed** does the conversion go through; the production orders are then reassigned to the **order** and raised to the **Prod. Order Status f. Sales Order**.

## Deleting and Unlinking

When a sales line is deleted – provided **Delete assigned Prod. Order on Sales Order delete** is activated – the automatic handling of the linked production orders takes effect:

- **Without** existing item or capacity ledger entries, the production order (or the prod. order line) is deleted; if the production order becomes empty as a result, it is removed completely.
- **With** existing ledger entries, the prompt appears asking whether the link between the production order and the sales order should be removed. On confirmation, the production order is retained and only the **order reference** is removed; on decline, the delete operation is canceled.

Regardless of this, you can remove the reference selectively at any time via the prod. order line action **Delete Order Reference**.

## Permissions

The module ships the permission set **All permissions** (permission object name: internal). It determines which actions users may perform in the Prod. Assistant and includes read/write rights on the setup table as well as execute rights on the module's pages and codeunits. Assign this permission set to the users who are to create and maintain production orders from sales.

## FAQ and Troubleshooting

### 1. Why can I not convert a Sales Quote into an order?

Because at least one linked production order does not yet have **Check Status** **Confirmed**. As long as a line has a production order with **Open**, **In Progress**, or **Refused**, the conversion is canceled. Set the **Check Status** of all linked production orders to **Confirmed**.

### 2. Why is no production order created upon order release?

Check three points: In setup, **Create Prod. Order on Sales Order Release** must be activated, the sales line must have **Create PO** = activated and type **Item**, and no production order may exist for the line yet. If **Confirm Create Prod. Order …** is active, you must also answer the prompt with **Yes**.

### 3. What happens if I click Cancel in the "Prod. Assistant" dialog?

The production order previously created as a simulation is deleted again. No half-finished production order remains.

### 4. Why does the system report that the sales line quantity has already been completely assigned?

Because production orders already exist for this sales line whose quantity reaches or exceeds the line quantity. No further production order can be created for the line until the assigned quantity falls below the line quantity.

### 5. Why can I not edit the "Create PO" field for a sales line?

Because the line does not contain an inventory item. For non-inventory item types and for non-item lines, **Create PO** is automatically deactivated and is not editable.

### 6. Why can I not create a production order for a Special Order line?

Because **Create Prod. Order on Sales Order For Special Order** is not activated in setup. Without this field, the assistant blocks Special Order lines and the automatic creation skips them.

### 7. Why can I not reserve components in the dialog?

Because the production order has the status **Simulated** or **Planned**. In these statuses no reservation is possible; the system points to the status with a note. Reservation is possible only from **Firm Planned** onwards.

### 8. Why can I not set the "Prod. Order Status f. Sales Quote" to "Finished"?

Because the assistant must not create an already completed production order. **Finished** is rejected. In addition, the quote status must never be higher than the **Prod. Order Status f. Sales Order**.

### 9. What happens when deleting a sales line with an already posted production order?

If item or capacity ledger entries exist for the production order, it is not deleted. You are asked whether the link should be removed: with **Yes**, the production order remains without an order reference; with **No**, the delete operation is canceled.

### 10. How do I recognize in the production order for which customer production is happening?

Via the fields **Sell-to Customer No.** and **Sell-to Customer Name** on the card, in the list, and in the prod. order lines, as well as via **Prod. Target Type/No./Line No.**, which show the linked sales document.

## Typical Use Cases

### Use Case 1: Customer Inquiry with Production Preview in the Quote

**Trigger:** A prospect inquires about a manufactured item by phone; Sales is to create a reliable quote with a realistic production date.

**Entry in BC:** The user creates a **Sales Quote**, records the item line, and chooses the **Prod. Assistant** action on the sales line.

**Core flow:** In the dialog, the user reviews **Quantity**, **Routing No.**, and **Due Date**; via the **Routing** and **Components** tabs they check operations and material. With **OK**, a production order is created in the **Prod. Order Status f. Sales Quote**. Depending on setup, the production order receives the **Check Status** **Confirmed** or **Open**, and the salesperson is notified via **Show Production Order**.

**Conclusion:** The quote goes to the customer with the stored production preview. The production order remains linked to the quote line via the **order reference**.

### Use Case 2: Confirmed Order with Automatic Production Order Creation

**Trigger:** A written order arrives; the order is to be recorded, released, and production is to be triggered without manual rework.

**Entry in BC:** The prerequisite is the activated setting **Create Prod. Order on Sales Order Release**. The user records the **Sales Order** with item lines; **Create PO** is set according to the prefilling.

**Core flow:** The user releases the order. If **Confirm Create Prod. Order on Sales Order Release** is active, they confirm the prompt **"Create Production Order?"** with **Yes**. For each item line with **Create PO** = activated, a production order is created in the **Prod. Order Status f. Sales Order**; Special Order lines are considered only if this has been set up.

**Conclusion:** The production orders are created and carry **Sell-to Customer No.**/**Name** as well as the order reference; production can continue working directly.

### Use Case 3: Converting a Quote into an Order with Check Safeguard

**Trigger:** The customer awards the order for an existing quote; the quote is to be transferred into an order.

**Entry in BC:** The user opens the **Sales Quote** and starts the standard function to convert it into a **Sales Order**.

**Core flow:** The module checks all item lines: only when all linked production orders have **Check Status** **Confirmed** does the conversion go through. Otherwise it is canceled with the note that all lines require a **"Confirmed"** Check Status. After a successful conversion, the production orders are automatically reassigned from the quote to the order and raised to the **Prod. Order Status f. Sales Order**.

**Conclusion:** The new order is linked to the same production orders as the quote before; the production reference is preserved without gaps.
