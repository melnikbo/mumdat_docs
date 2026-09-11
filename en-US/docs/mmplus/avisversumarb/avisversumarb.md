---
title: Anwenderhandbuch m+m Logistic Mgt. with Metal Tolling
---

# User Guide m+m Logistic Mgt. with Metal Tolling

## Introduction

The **m+m Logistic Mgt. with Metal Tolling** extension links two existing m+m modules together: the **Metal Orders** from *m+m Metal & Tolling* and the **Shipment Planning** from *m+m Logistic Management*. Without this extension, Metal Orders and Shipment Planning are managed separately. With it, released Metal Orders can be called up directly in **Shipment Planning**, assigned to shipment planning lines, and posted through the normal Warehouse Shipment.

The operational benefit: a Metal Order that triggers an inbound or outbound warehouse movement no longer has to be recorded as a separate document for tour planning. It appears in the same **Shipment Planning** in which Sales and Transfer Orders are also assembled, and it can be grouped together with them into a single delivery tour.

**Target audience.** This guide is primarily aimed at **operational users in logistics and shipping** who work with **Shipment Planning** every day: they select Metal Orders, assign them to a shipment planning record, and trigger the Warehouse Shipment. **Secondarily**, it addresses administrators who set the address source for Shipment Planning once in the **Metal & Tolling Setup**, as well as clerks who record the delivery tour on the **Metal Order**.

**Short process overview.** The typical path runs in this order:

1. One-time **setup**: In the **Metal & Tolling Setup**, on the **Logistic Management** tab, the administrator defines which address of the Metal Order is transferred into Shipment Planning.
2. **Master data on the document**: On the **Metal Order**, a **Shipment Tour Code** is recorded if required; the **Avail. for Shipment Planning** field controls whether the order is offered for assignment.
3. **Daily work**: In **Shipment Planning**, the user opens the **Metal Order for Assignment** area, selects orders, and transfers them with **Add Lines to Shipment Planning**.
4. **Completion**: Shipment Planning is released in the base module, the **Warehouse Shipment** is created and posted. When the delivery for the Metal Order is posted (**Shipped**), the system automatically sets the related shipment planning lines to **Finished**.

## Quick Start for Users

The quick start describes the shortest path from a released Metal Order to a posted Warehouse Shipment. The setup (step 0) is done only once; steps 1 through 6 are the daily routine.

0. **Setup (one-time, administrator).** Use **Search** to open the **Metal & Tolling Setup** and, on the **Logistic Management** tab, set the **Metal Order Addr. f. Ship. Planning** field to the desired value (**Standard**, **Ship-to**, or **Pickup**). Without this selection, the standard applies.
1. **Prepare the Metal Order.** Make sure the Metal Order has the **Status** **Released** (or **Certified**) and that **Avail. for Shipment Planning** = Yes is set. If required, record the **Shipment Tour Code** on the Metal Order.
2. **Open Shipment Planning.** Open **Shipment Planning** and select the shipment planning record to which the Metal Orders are to be assigned. The **Metal Order for Assignment** area is visible as long as the shipment tour is **not** flagged as **Internal Logistics**.
3. **Select Metal Orders.** In the **Metal Order for Assignment** area, mark the desired lines and choose **Select Lines** (Ctrl+1). Remove incorrectly marked lines with **Remove Lines** (Ctrl+2). Use **Show Selected Lines** (Ctrl+4) and **Show All Lines** (Ctrl+3) to switch the view.
4. **Transfer into Shipment Planning.** Choose **Add Lines to Shipment Planning** (Ctrl+I). A shipment planning line is created for each selected Metal Order; the order is subsequently no longer offered for assignment (**Avail. for Shipment Planning** = No).
5. **Release and post the Warehouse Shipment.** Complete the Shipment Planning in the base module, release it via **Release**, and create or post the **Warehouse Shipment**.
6. **Completion.** Post the delivery for the Metal Order. As soon as the Metal Order reaches the **Status** **Shipped**, the system automatically sets the related shipment planning lines to **Finished**; a manual close is not necessary.

## Setup

The setup of this extension is deliberately lean: it adds exactly **one** field to the existing **Metal & Tolling Setup**. All other fields on this card belong to the base module *m+m Metal & Tolling* and are maintained there. The following section describes fully what this extension adds to the setup and how this setting feeds into the daily Shipment Planning.

### Setting up the address source for Shipment Planning

**Process.** This setting is made by the administrator or key user **once before first use**. It defines which of the addresses kept on the Metal Order (customer/vendor, delivery, or pickup) is used as the **shipping address** when assembling the Shipment Planning. The selection has an immediate effect on the **Metal Order for Assignment** area and on the generated shipment planning lines (cross-reference: sections *Metal Order for Assignment* and *Shipment Planning Integration*).

**Access:** Use **Search** to open the **Metal & Tolling Setup** and select the **Logistic Management** tab. This is a company-wide setup (one record per company); there is no parent list, so access via **Search** is the intended way.

| Setup | Explanation |
|-------|-------------|
| **Metal Order Addr. f. Ship. Planning** | Defines the address source that is transferred into Shipment Planning when the Metal Orders are retrieved. The selected value controls which address fields of the Metal Order are written into the shipment planning line (Ship-to data) and by which address the grouping by **Ship-to Address** is consolidated. **If** a value is set here, **then** the system uses exactly this address source uniformly for all Metal Orders on every transfer. |

**Values of the field Metal Order Addr. f. Ship. Planning** (option field — each value in detail):

- **Standard:** The delivery address of the Metal Order (Ship-to data) is transferred. **If** selected, **then** the system writes **Ship-to Code**, **Ship-to Name**, **Ship-to Address**, **Ship-to City**, etc. into the shipment planning line and groups by these.
- **Ship-to:** Behaves like **Standard** and likewise transfers the delivery address (Ship-to data) of the Metal Order. **If** selected, **then** the same Ship-to fields as with **Standard** are used.
- **Pickup:** The **pickup** address of the Metal Order is transferred. **If** selected, **then** the system writes **Pickup No.**, **Pickup Name**, **Pickup City**, etc. into the shipment planning line and groups by the pickup address — useful when the goods are planned at the vendor's or the pickup location rather than at the delivery address.

**Numbered activation (order from the code):**

1. **First**, in the **Metal & Tolling Setup**, set the **Metal Order Addr. f. Ship. Planning** field. **If** set, **then** the address logic is available for all subsequent transfers.
2. **Then**, on the **Metal Order**, the clerks make sure that **Avail. for Shipment Planning** = Yes and the **Status** is **Released** or **Certified** (see section *Master Data and Document Data on the Metal Order*).
3. **Finally**, the users transfer the orders in the daily routine via **Add Lines to Shipment Planning** in **Shipment Planning** (cross-reference: *Metal Order for Assignment*).

**Dependency.** The address selection takes effect automatically on every transfer; it does not have to be repeated per order. A change affects only **future** transfers — shipment planning lines that have already been created keep their transferred address.

## Master Data and Document Data on the Metal Order

The **Metal Order** is the leading document from which Shipment Planning is fed. This extension adds four fields to the Metal Order card: one controls the delivery tour, three indicate the relationship to Shipment Planning.

**Process.** These fields are maintained or observed by the clerks in day-to-day business on the Metal Order, **before** and **after** the order is transferred into Shipment Planning. The **Shipment Tour Code** is set actively; the three remaining fields are maintained by the system and serve for control. The values then appear in the **Metal Order for Assignment** list and control whether and how the order is offered there (cross-reference: *Metal Order for Assignment*, *Setting up the address source for Shipment Planning*).

**Access:** Open the **Metal Orders** list and select the desired **Metal Order** to open the card. The **Shipment Tour Code** is located on the tab with the delivery data (Ship-to Address); the three Shipment Planning fields are located in the area of the related documents.

| Field | Explanation |
|------|-------------|
| **Shipment Tour Code** | Assigns the Metal Order to a shipment tour. **If** a Shipment Tour Code is set, **then** the system — provided a carrier is recorded on the shipment tour — transfers this carrier into the Metal Order; in addition, the order becomes filterable and groupable by this shipment tour in Shipment Planning. Without a Shipment Tour Code, the order remains without a tour reference and must be searched for in Shipment Planning without a tour filter. |
| **Shipment Planning Lines** | Shows the number of open shipment planning lines that reference this Metal Order (calculated field). **If** this value is greater than 0, **then** the order has already been assigned to at least one Shipment Planning and is not offered for assignment again. |
| **Reg. Shipment Planning Lines** | Shows the number of already **registered** shipment planning lines for this Metal Order (calculated field). **If** this value is greater than 0, **then** Shipment Planning for this order has already been registered (processed further) and the order remains blocked for assignment until no registered line exists anymore. |
| **Avail. for Shipment Planning** | Indicates whether the Metal Order is offered in the **Metal Order for Assignment** area (not manually editable, default value Yes). **If** = Yes, **then** the order appears for selection; as soon as it is added to a Shipment Planning, the system automatically sets the field to No. **If** the related shipment planning line is later deleted and no registered line exists anymore, **then** the system sets the field back to Yes, and the order is available again for assignment. |

**Status dependency.** Only Metal Orders with **Status** **Released** or **Certified** (and **Avail. for Shipment Planning** = Yes) are offered for assignment. The status values of the Metal Order mean:

- **Open:** Entries on the order are possible; the order does **not** appear for assignment.
- **Released:** The order is checked/released and is offered for Shipment Planning.
- **Certified:** Optional status; the order is likewise offered for Shipment Planning.
- **Shipped:** Set by the system as soon as the delivery for the Metal Order is posted; the related shipment planning lines are then automatically **finished** (see *Posting and Completion Behavior*).

## Metal Order for Assignment

The **Metal Order for Assignment** page is the central work area of this extension. It appears **embedded** in **Shipment Planning** (not as a standalone page) and lists the Metal Orders available for assignment. The user marks orders here and transfers them into Shipment Planning.

**Access:** Open **Shipment Planning**, select the shipment planning record and, optionally, the desired shipment tour; the **Metal Order for Assignment** area is displayed underneath. The list is not editable; all work is done exclusively via the actions.

**Visible columns.** The list shows the following columns for each Metal Order:

| Field | Explanation |
|------|-------------|
| **Selected** | Marker indicating whether the line is selected for the transfer. **If** marked, **then** the order is taken into account by **Add Lines to Shipment Planning**. |
| **No.** | Number of the Metal Order; uniquely identifies the document. |
| **Template** | Shows the template type of the Metal Order (e.g. an inbound or sales transaction) and helps to distinguish similar orders in the list. |
| **Cust./Vendor Type** | Indicates whether the order is assigned to a customer or a vendor; together with the **Delivery Direction**, it determines the later Ship-to Type of the shipment planning line. |
| **Cust./Vendor No.** | Number of the assigned customer or vendor. |
| **Cust./Vendor Name** | Name of the assigned customer or vendor for quick identification in the list. |
| **Cust./Vendor City** | City of the customer or vendor; supports orientation by region. |
| **Delivery Direction** | Indicates the direction of the movement (Own Location or Customer/Vendor). **If** Own Location, **then** the shipment planning line is treated as a warehouse delivery; **if** Customer/Vendor, **then** the Ship-to Type follows the **Cust./Vendor Type**. |
| **Delivery/Pickup Date** | Date of the delivery or pickup; serves as a date filter when assembling the tour and is transferred into planning as the warehouse shipment date. |
| **Shipment Tour Code** | Shows the shipment tour recorded on the Metal Order; allows grouping several orders into one tour. |
| **Pickup Name** | Name of the pickup address of the Metal Order for checking the pickup location before the transfer. |
| **Ship-to Name** | Name of the delivery address of the Metal Order for checking the delivery destination before the transfer. |
| **Ship-to City** | City of the delivery address for quick orientation by destination region. |
| **Pickup City** | City of the pickup address for quick orientation by pickup region. |

Additional address and detail columns (e.g. the full address, post code, country/region code, delivery-terms and carrier data, as well as the individual delivery and pickup detail fields) are **hidden** by default and can be shown as needed via personalization; they contain the complete address data from the Metal Order.

**Actions.** All work steps are carried out via two action groups:

Group **Selection**:

| Action | Explanation |
|--------|-------------|
| **Select Lines** (Ctrl+1) | Marks the currently selected lines for the transfer. **If** executed, **then** the affected orders are flagged in the **Selected** column. |
| **Remove Lines** (Ctrl+2) | Cancels the marking of the selected lines again. |
| **Show All Lines** (Ctrl+3) | Shows all available Metal Orders, regardless of the marking. |
| **Show Selected Lines** (Ctrl+4) | Filters the list down to the marked lines in order to check the selection before the transfer. |

Group **Functions**:

| Action | Explanation |
|--------|-------------|
| **Add Lines to Shipment Planning** (Ctrl+I) | Transfers all marked Metal Orders as shipment planning lines. **If** executed, **then** the system creates one line per order with item, **Qty. to Assign** (from the **Total Net Weight**), weights, location, and the Ship-to Address selected according to the setup; afterwards, each transferred order is set to **Avail. for Shipment Planning** = No and the list is refreshed. |

Group **Line**:

| Action | Explanation |
|--------|-------------|
| **Show Document** (Shift+F7) | Opens the Metal Order belonging to the marked line in order to check the source document before the transfer. |

## Shipment Planning Integration

This extension adds the embedded **Metal Order for Assignment** area to the base module's **Shipment Planning**, as well as an action with which the assigned Metal Orders are called up. Metal Orders thus line up seamlessly alongside Sales and Transfer Orders in the same planning workflow.

**Process.** The user continues to work in the familiar **Shipment Planning**; the Metal Orders are carried along there. Whether the assignment area is visible depends on the shipment tour.

| Field/Action | Explanation |
|-------------|-------------|
| **Metal Order for Assignment** area (embedded) | Shows the Metal Orders available for assignment for the current shipment planning record. **If** the assigned shipment tour is **not** flagged as **Internal Logistics**, **then** the area is displayed; with internal logistics it remains hidden, since no external tour assembly takes place here. |
| **Metal Orders** action | Opens the list of Metal Orders that are already assigned to the current shipment planning record. **If** executed, **then** the system shows exactly the Metal Orders for which shipment planning lines of this record exist — useful for jumping back from the planning record to the source documents. |

**Address origin.** Which address is written into the shipment planning line when adding is determined by the **Metal Order Addr. f. Ship. Planning** setup (cross-reference: *Setting up the address source for Shipment Planning*). With **Standard**/**Ship-to**, the delivery data is transferred; with **Pickup**, the pickup data.

## Posting and Completion Behavior

This extension does not post any document itself. The Warehouse Shipment is posted via **Shipment Planning** and the base module's Warehouse Shipment (Release → create Warehouse Shipment → post). The extension does, however, react automatically to two events and keeps the Metal Order and Shipment Planning consistent.

- **After posting the delivery for the Metal Order:** When the Metal Order reaches the **Status** **Shipped**, the system automatically sets all related shipment planning lines of this order to **Finished** and **Open** = No. The user does not have to close the lines manually.
- **When deleting a shipment planning line:** If a shipment planning line for a Metal Order is deleted and no registered shipment planning line for this order exists anymore, the system sets **Avail. for Shipment Planning** back to Yes. The order then appears again in the **Metal Order for Assignment** area.

**Partial quantities.** Each Metal Order is transferred as a whole via its **Total Net Weight** as a single shipment planning line; there is no block against incomplete quantities. An order can be removed at any time and — after availability has been released — assigned again.

## Permissions

For operating the extension, m+m ships the permission set **MuM ASMT ALL**. It is assignable and determines the permissions for the objects of this extension: the two processing codeunits as well as the **Metal Order for Assignment** page. Assign this permission set to all users who are to work with Metal Orders in Shipment Planning. The set determines which actions the users can carry out in this area; for the actual Shipment Planning and the Metal Orders, the permissions of the two base modules additionally apply.

## FAQ and Troubleshooting

### 1. Why does a Metal Order not appear in the Metal Order for Assignment area?
The order is only offered if its **Status** is **Released** or **Certified** **and** **Avail. for Shipment Planning** = Yes is set. An order with **Open** status or an already assigned order (Avail. = No) does not appear.

### 2. Why is the Metal Order for Assignment area not visible at all?
The area is hidden when the shipment tour of the shipment planning record is flagged as **Internal Logistics**. Select a shipment planning record or a shipment tour without internal logistics so that the area appears.

### 3. What happens when I choose Add Lines to Shipment Planning?
For each marked Metal Order, a shipment planning line is created with item, **Qty. to Assign** (from the Total Net Weight), weights, location, and the configured Ship-to Address. Afterwards, the order is set to **Avail. for Shipment Planning** = No and disappears from the selection list.

### 4. Why can I not assign the same Metal Order twice?
As soon as an order has been added, **Avail. for Shipment Planning** is set to No and the **Shipment Planning Lines** counter is greater than 0. This prevents a duplicate assignment. Only when the related line is deleted and no registered line exists anymore is the order released again.

### 5. How do I undo an incorrect assignment?
Delete the relevant shipment planning line. If no registered shipment planning line for this Metal Order exists afterwards, the system automatically sets **Avail. for Shipment Planning** back to Yes, and the order appears again for assignment.

### 6. Which address is transferred into the shipment planning line?
This is controlled by the **Metal Order Addr. f. Ship. Planning** setup in the **Metal & Tolling Setup**. With **Standard** and **Ship-to**, the delivery data is transferred; with **Pickup**, the pickup data of the Metal Order.

### 7. Why does my changed address setup not take effect for old lines?
The setting takes effect only for **new** transfers. Shipment planning lines that have already been created keep the address that was valid at the time of the transfer. Remove and repeat the transfer if an existing line is to use the new address source.

### 8. Why was the shipment planning line automatically set to Finished?
As soon as the delivery for the Metal Order was posted and the order reaches the **Status** **Shipped**, the system automatically sets all related shipment planning lines to **Finished** and **Open** = No. This is intended behavior and saves the manual close.

### 9. How do I get from Shipment Planning back to the assigned Metal Orders?
In **Shipment Planning**, use the **Metal Orders** action. It opens the list of exactly those Metal Orders for which shipment planning lines of the current record exist.

### 10. Why is a carrier entered in the Metal Order when the Shipment Tour Code is set?
If a carrier is recorded on the selected shipment tour, the system transfers it into the Metal Order when the **Shipment Tour Code** is set. This ensures the order is consistently assigned to a tour and its carrier; the entry can be overwritten on the order if required.

## Typical Use Cases

The following scenarios show the workflow from the perspective of the operational users. All steps and designations correspond to the pages and actions present in this extension.

### Use Case 1: Transfer a released Metal Order into daily planning

**Trigger.** Planning reports that a released Metal Order is to be delivered today.

**Entry in BC.** The user first checks on the **Metal Order** card that the **Status** is **Released**, **Avail. for Shipment Planning** = Yes is set, and a suitable **Shipment Tour Code** is recorded. The user then opens **Shipment Planning** and selects the shipment planning record of the tour.

**Core workflow.** In the displayed **Metal Order for Assignment** area, the user marks the order and chooses **Select Lines**. Using **Show Selected Lines**, the user checks the selection and transfers it via **Add Lines to Shipment Planning**. The system creates the shipment planning line and blocks the order against a repeated assignment.

**Completion.** The user releases the Shipment Planning in the base module via **Release**, creates and posts the **Warehouse Shipment**. After the delivery is posted, the Metal Order reaches the **Shipped** status, and the shipment planning line is automatically **finished**.

### Use Case 2: Correct an accidentally assigned order

**Trigger.** While assembling the tour, it is noticed that a Metal Order was assigned to the wrong Shipment Planning.

**Entry in BC.** The user opens the affected **Shipment Planning** and calls up the assigned orders via the **Metal Orders** action in order to identify the wrong document.

**Core workflow.** The user deletes the related shipment planning line. Since no registered shipment planning line for this Metal Order exists anymore, the system automatically sets **Avail. for Shipment Planning** back to Yes.

**Completion.** The order appears again in the **Metal Order for Assignment** area and can be assigned to the correct Shipment Planning.

### Use Case 3: Plan a pickup at the vendor

**Trigger.** Raw metal is to be picked up at the vendor and included in tour planning.

**Entry in BC.** The administrator has set the **Metal Order Addr. f. Ship. Planning** field in the **Metal & Tolling Setup** to **Pickup**, so that the pickup address is decisive. The user opens **Shipment Planning** and the appropriate shipment planning record.

**Core workflow.** In the **Metal Order for Assignment** area, the user marks the relevant Metal Order and transfers it with **Add Lines to Shipment Planning**. The **Pickup** data (Pickup Name, Pickup City, etc.) of the Metal Order is written into the shipment planning line.

**Completion.** The Shipment Planning is released and the **Warehouse Shipment** is posted; the pickup is thereby included in the tour.
