---
title: Anwenderhandbuch m+m Item Status
---

# m+m Item Status User Guide

## Introduction

The m+m Item Status app (**Item Status**) extends Microsoft Dynamics 365 Business Central with a feature that lets you block an item selectively for individual business transactions. Using an **Item Status**, you define which documents, journal postings, and warehouse activities are still permitted for an item and which the system blocks.

Unlike the simple standard blocking in Business Central, which either blocks an item entirely or not at all, the item status works **fine-grained**: you can, for example, block the same item for purchasing while sales of the remaining stock stays possible. Within one rule (one item status), any combination of the blocking options is possible; however, each item is always assigned to only **one** item status.

In addition, the app provides a **requalification**: a time-controlled strategy that automatically moves items to a different item status after a defined period and thereby activates the blocks stored there on its own.

**Target audience:** The primary users are the operational roles that work with items every day — purchasing, sales, warehouse, manufacturing, and service. They mainly experience the item status in the form of checks and blocking messages when entering document lines and journal lines. The secondary audience is administrators and master data managers, who set up the item statuses and requalifications and assign them to items.

**Typical flow:** First, an administrator defines the blocking rules in the **Item Status List** and optionally configures a time-controlled transition in the **Item St. Requalifications**. Then a master data manager assigns the appropriate status to the affected items via the **Item Card** (action **Set Item Status**). From that point on, the blocks take effect immediately: if a user enters a blocked document line, the system prevents the entry with an error message. Every status change is logged in the **Item Status Entries**.

## Quick start for users

The fastest way from an empty installation to an effective block follows the dependency order in the code (first setup, then master data assignment, then day-to-day work):

1. **Create an item status.** In the search (**Tell me**), type `Item Status List` and open the **Item Status List**. Create a new rule with a meaningful **Code** and a **Description**.
2. **Set the blocking options.** Open the line by double-clicking; the item status opens (**Item Status Card**). On the tabs **Block Purchase**, **Block Sales**, **Block Warehouse**, **Block Item Journal**, **Block Manufacturing**, and **Block Service**, select the desired check boxes — individually or in bulk via the **All Activate** / **All Deactivate** actions per business area.
3. *(Optional)* **Set up requalification.** In the search, type `Item St. Requalifications`, create a rule with **Code**, **Date Formula** (a date formula), and **Item Status To Set**, and enter this **Requalificationcode** in the item status.
4. **Assign the item status.** Open the **Item Card** of the affected item and choose the action **Set Item Status**. Select the status and confirm the security prompt. The fields **Item Status Code** and **Item Status Set At** then show the active status.
5. **Effect in day-to-day work.** From now on, the system blocks the operations blocked in the status as soon as a user enters the corresponding document line, journal line, or warehouse line.

The setup (steps 1–3) is a prerequisite for the day-to-day work (steps 4–5) and is therefore performed first.

## Setup

Setting up the item status covers two areas: the **Item Status List** with the blocking rules themselves and — for time-controlled blocking — the **Item St. Requalifications**. Both pages are standalone list pages of this app and are opened via the search.

### Setting up the item status

**Entry point:** In the search (**Tell me**), type `Item Status List` and open the **Item Status List**. From the line you reach the associated **Item Status Card** by double-clicking.

**Process:** An administrator or master data manager sets up the item statuses **before** the first assignment to items. Each item status is a reusable rule: it bundles the desired blocks and is later assigned to one or more items on the **Item Card** (see chapter *Daily work on the Item Card*). The blocks only take effect once an item is linked to the status.

The **Item Status List** shows the existing rules at a glance:

| Field | Explanation |
|------|-------------|
| **Code** | Unique name of the rule (mandatory field). Once you assign a code, this item status can then be assigned to items and referenced in requalifications. |
| **Description** | Plain-text label of the rule. When maintained, this text appears in lookup lists and in the blocking message, so that in case of an error the user immediately recognizes which rule applies. |
| **Requalificationcode** | Link to an **Item Status Requalification**. When set, the daily background run checks whether items with this status are automatically moved to another status after the stored period has elapsed; without an entry, the status remains in place indefinitely. |

On the **Item Status Card**, the blocking options are structured into six functional tabs. Each option is a check box: **if activated, then** the system prevents the respective operation for all items that carry this status; if the flag is not set, the operation remains fully possible.

#### Tab "Block Purchase"

Controls the purchasing side. The check applies when validating the purchase line (field **No.**) and when converting a quote into an order.

| Field | Explanation |
|------|-------------|
| **Block Purch. Quote** | When activated, the item can no longer be added to a purchase quote (document type Quote); line entry aborts with a blocking message. |
| **Block Purch. Order** | When activated, the item is blocked in purchase orders — including when creating the order from a quote. This prevents reorders of a discontinued item. |
| **Block Purch. Blanket Order** | When activated, the item is no longer permitted in purchase blanket orders; existing releases must run through a different item. |
| **Block Purch. Invoice** | When activated, the item can no longer be entered in purchase invoices; invoice verification stops before posting. |
| **Block Purch. Cr. Memo** | When activated, the item is blocked in purchase credit memos; returns to the vendor via this item are not possible. |

#### Tab "Block Sales"

Controls the sales side. The check applies when validating the sales line (fields **No.** and **Quantity**) and when converting a quote into an order.

| Field | Explanation |
|------|-------------|
| **Block Sales Quote** | When activated, the item can no longer be added to sales quotes; the sales department can no longer offer the item to customers. |
| **Block Sales Order** | When activated, the item is blocked in sales orders — including when creating the order from a quote. New sales are thereby prevented. |
| **Block Sales Blanket Order** | When activated, the item is no longer permitted in sales blanket orders. |
| **Block Sales Invoice** | When activated, the item can no longer be entered in sales invoices; invoicing stops before posting. |
| **Block Sales Cr. Memo** | When activated, the item is blocked in sales credit memos; customer returns via this item are not possible. |
| **Allow Sales Till Available Stock** | Special case for discontinued items. When activated, the system checks availability when entering the sales line: if stock is still available, sales remain permitted; if no stock is available anymore, entry aborts with the note that the item is a discontinued part and only the still-available stock can be sold. This lets you sell off remaining stock without allowing oversells. |

> Note: The flag **Allow Sales Till Available Stock** acts independently of the other sales blocks as a standalone availability check. If it is set, the stock situation determines whether the sales line is permitted.

#### Tab "Block Warehouse"

Controls warehouse activities. The check applies when inserting warehouse receipt, warehouse shipment, and warehouse activity lines, as well as when validating item journal and transfer lines.

| Field | Explanation |
|------|-------------|
| **Block Warehouse Receipt** | When activated, the item cannot be added to a warehouse receipt; the warehouse receipt line is rejected on insert. |
| **Block Warehouse Shipment** | When activated, the item is blocked in the warehouse shipment; shipping via this item is not possible. |
| **Block Pick** | When activated, the item is blocked in pick lines (warehouse and inventory pick); the item cannot be picked for shipment. |
| **Block Put-Away** | When activated, the item is blocked in put-away lines (warehouse and inventory put-away); putting away into bins is prevented. |
| **Block Transfer Order** | When activated, the item cannot be entered in transfer order lines; transfers between locations via this item are blocked. |
| **Block Reclass. Journal** | When activated, the item is blocked in the reclassification journal as well as in item journal lines with a new location or new bin; internal transfers are thereby prevented. |

#### Tab "Block Item Journal"

Controls the direct journal postings. The check applies when inserting and when validating the item number in the item journal line and depends on the posting type (entry type) of the line.

| Field | Explanation |
|------|-------------|
| **Block Item Journal Purchase** | When activated, an item journal line of entry type Purchase is rejected for this item. |
| **Block Item Journal Sale** | When activated, a journal line of entry type Sale is blocked. |
| **Block Item Journal Consumption** | When activated, a journal line of entry type Consumption is blocked; a manual consumption outside a production order is not possible. |
| **Block Item Journal Output** | When activated, a journal line of entry type Output is blocked; a manual output posting of the item is prevented. |
| **Block Item Journal Assembly Consumption** | When activated, a journal line of entry type Assembly Consumption is blocked. |
| **Block Item Journal Assembly Output** | When activated, a journal line of entry type Assembly Output is blocked. |
| **Block Item Journal Positive Adjustment** | When activated, a journal line of entry type Positive Adjustment is blocked; manual stock increases are prevented. |
| **Block Item Journal Negative Adjustment** | When activated, a journal line of entry type Negative Adjustment is blocked; manual stock decreases are prevented. |

> Note: If the item journal line carries a new location or new bin (transfer posting), the **Block Reclass. Journal** flag from the "Block Warehouse" tab applies instead of the entry-type check.

#### Tab "Block Manufacturing"

Controls manufacturing. The check applies when validating the item number in production order lines, production BOM lines, and prod. order components, and for production orders depends on their status.

| Field | Explanation |
|------|-------------|
| **Block Simulated Prod. Order** | When activated, the item cannot be used in a production order line with status Simulated. |
| **Block Planned Prod. Order** | When activated, the item is blocked in production order lines with status Planned. |
| **Block Firm Planned Prod. O.** | When activated, the item is blocked in production order lines with status Firm Planned. |
| **Block Released Prod. Order** | When activated, the item is blocked in released production order lines; production of the item is prevented. For already finished orders, no check is performed. |
| **Block Production BOM** | When activated, the item cannot be entered as an item position in a production BOM line. |
| **Block Prod. Order Component** | When activated, the item is blocked as a component of a production order; it cannot be assigned to the production order as consumption material. |

#### Tab "Block Service"

Controls the service module. The check applies when validating the item number in service lines, service items, service item lines, and service contract lines, and depends on the respective document type or contract type.

| Field | Explanation |
|------|-------------|
| **Block Service Item** | When activated, the item cannot be assigned to a service item. |
| **Block Service Quote** | When activated, the item is blocked in service lines and service item lines of document type Quote. |
| **Block Service Order** | When activated, the item is blocked in service lines and service item lines of document type Order. |
| **Block Service Contract Qu.** | When activated, the item is blocked in service contract lines of contract type Quote. |
| **Block Service Contract** | When activated, the item is blocked in service contract lines of contract type Contract. |
| **Block Service Invoice** | When activated, the item is blocked in service lines of document type Invoice. |
| **Block Service Cr. Memo** | When activated, the item is blocked in service lines of document type Credit Memo. |

#### Bulk actions per tab

So that you do not have to set each check box individually, every tab offers two actions. They act exclusively on the fields of the respective business area:

| Action | Explanation |
|--------|-------------|
| **All Activate** | Sets all blocks of the respective tab (e.g. **Sales**) to active. On the **Sales** tab, **Allow Sales Till Available Stock** is also set along with them. |
| **All Deactivate** | Removes all blocks of the respective tab again. |

The bulk actions are available per area as a group: **Sales**, **Purchase**, **Warehouse**, **Item Journal**, **Manufacturing**, and **Service**.

### Setting up requalification

**Entry point:** In the search (**Tell me**), type `Item St. Requalifications` and open the **Item St. Requalifications** page. The link to the item status is then made via the **Requalificationcode** field on the **Item Status Card**.

**Process:** Requalification is an optional, time-controlled building block and is set up by an administrator **after** the item statuses have been created (the requalification refers to an Item Status To Set). "Requalification" means the automatic transition of an item to a different item status once a defined period has elapsed since the current status was set. The blocks stored there then take effect immediately. In day-to-day work, the building block does not act through a user action, but through a background run (see below).

Explanations of the fields on the **Item St. Requalifications** page:

| Field | Explanation |
|------|-------------|
| **Code** | Unique name of the requalification (mandatory field). Once assigned, the rule can be referenced in the **Requalificationcode** field of an item status. |
| **Description** | Plain-text label of the requalification for better findability in lookup lists. |
| **Date Formula** | Date formula used to calculate the period (mandatory field as soon as an Item Status To Set is stored). When set, the background run determines the expiration point from the item's **Item Status Set At** field plus this formula; once it is exceeded, the item is automatically moved to the Item Status To Set. All date formulas common in Business Central are permitted. |
| **Item Status To Set** | The item status to which the item is moved when the period elapses. When filled, the **Date Formula** field is mandatory; if a date formula is entered without this value, the system rejects the entry. |
| **Item Status Description** | Automatically shows the **Description** of the Item Status To Set (calculated field, not editable). Serves to verify that the correct follow-up rule was stored. |

**Process steps (setting up the time-controlled block):**

1. **First**, create in the **Item Status List** the target status that the item is to carry after the period elapses (with the desired blocks).
2. **Then**, in the **Item St. Requalifications**, enter a rule with **Code**, **Date Formula**, and **Item Status To Set**.
3. **Next**, store this **Requalificationcode** in the outgoing item status (**Item Status Card**).
4. **Finally**, assign the outgoing status to the items via the Item Card (see *Daily work on the Item Card*). From then on, the background run handles the transition.

**Cascading requalification:** If the Item Status To Set in turn refers to a requalification again, the block can be tightened step by step in a time sequence. Example: after six months, an item is blocked for manufacturing in the first stage; 30 days later, additionally for purchasing in the second stage; after one more day, fully in the third stage.

#### Automatic background run (job queue)

The requalification is not triggered manually, but monitored by a job queue entry. **When you create the first item status**, the system automatically creates a recurring job queue entry with the description **Act. Item Status** (codeunit *MuM IS Item Status Management*). By default, it starts daily (interval 1440 minutes, first run at 11:00 PM). Directly after creation, the system asks whether the associated job queue entry card should be opened, so that you can adjust the schedule if needed.

On each run, the background process checks all items with a set status: if the period calculated from **Item Status Set At** and the requalification's **Date Formula** has been exceeded, the item is moved to the **Item Status To Set** and the **Item Status Set At** field is updated to the current work date. Each automatic transition also creates an entry in the **Item Status Entries**.

## Master data: item with item status

The app extends the standard master data of the item (**Item Card** and the item list) with two fields that make the currently assigned item status visible. These fields are not typed directly, but filled by the **Set Item Status** action or by the requalification run.

**Process:** The master data manager maintains the assignment per item. Both fields are read-only and serve for display; their values then control, throughout day-to-day work, which operations the system permits for this item (see chapters *Daily work* and *Effect in day-to-day work*).

| Field | Explanation |
|------|-------------|
| **Item Status Code** | Shows the item's currently assigned item status (read-only). When filled, the blocks set in the associated item status apply for this item; if the field is empty, no item status blocks apply. The value is set via the **Set Item Status** action or by the requalification. |
| **Item Status Set At** | Shows the date since which the current status applies (read-only). When filled, this value serves as the starting point for the requalification's period calculation; it is updated to the work date when the status is set and on each automatic transition. |

Both fields appear both on the **Item Card** (in the FastTab for the item data) and as additional columns in the item list, so that you can recognize the status of an item already in the list without opening the card.

## Daily work on the Item Card

The **Item Card** is the central entry point for operational work with the item status. The app adds two actions there: **Set Item Status** and **Item Status History**.

**Entry point:** Open the item list or the **Item Card** of the item (standard navigation via the item master data). You find the two actions in the card's action menu.

### Set Item Status

Using the **Set Item Status** action, you assign a previously defined item status to the item. The assignment can be repeated and changed as often as you like.

Flow:

1. Open the **Item Card** of the item.
2. Choose the action **Set Item Status**. The selection of the existing item statuses opens.
3. Select the desired status and confirm with **OK**.
4. If the new status differs from the current one, a security prompt appears: *"The current Item Status Code is … Your selected Item Status is … Do you want to use the selected …?"* Confirm to apply the change, or cancel.
5. The item receives the new status; the fields **Item Status Code** and **Item Status Set At** are updated. The date is set to the current work date.

All blocks stored in the selected item status take effect **immediately** for this item. If a requalification is set up for the assigned status, **Item Status Set At** together with the **Date Formula** forms the basis for the later automatic transition.

### Item Status History

Using the **Item Status History** action, you open the **Item Status Entries** — the complete logging of all statuses ever set for the item. This lets you trace when which status was set and by whom. An entry arises on each change of the item status code, both for manual assignment and for automatic requalification; a transition to the same status creates no entry.

The **Item Status Entries** page is display-only (no creating, changing, or deleting possible):

| Field | Explanation |
|------|-------------|
| **Entry No.** | Sequential counter of the entry (assigned consecutively). |
| **Item No.** | The item number for which the status was changed. |
| **Old Item Status Code** | The status the item had before the change. On the first assignment, this field is empty. |
| **New Item Status Code** | The status the item received with the change. |
| **Set By** | User name of the user who triggered the change. For automatic requalification, this corresponds to the executing context of the background run. |
| **Set At** | Date and time of the status change. |

The same history is also reachable outside the Item Card via the search (**Tell me**, entering `Item Status Entries`).

## Effect in day-to-day work (blocking checks)

Operational users experience the actual blocking effect not on the setup pages, but when entering their documents and journals. The app checks the item status automatically at the following points; if the relevant block is set, the operation aborts with the message *"The Item … is blocked by the Item Status … ."*:

| Area | Triggering point |
|---------|-------------------|
| **Sales** | when changing **No.** or **Quantity** in the sales line and when creating the order from the quote |
| **Purchase** | when changing **No.** in the purchase line and when creating the order from the quote |
| **Warehouse** | when inserting warehouse receipt, warehouse shipment, and warehouse activity lines |
| **Item Journal** | when inserting the journal line and when changing the item number |
| **Transfer** | when changing the item number in the transfer line |
| **Manufacturing** | when changing the item number in production order line, prod. order component, and production BOM line |
| **Service** | when changing the item number in service line, service item, service item line, and service contract line |

The check is performed only if the item carries an **Item Status Code** at all and the block corresponding to the operation is active in the status. If the item carries no status or the matching block is not set, the operation continues unchanged.

Special case of discontinued items: if **Allow Sales Till Available Stock** is active in the status, an availability check replaces the hard block. If stock is still available, sales remain permitted; otherwise the note appears that the item is a discontinued part and only the available stock can be sold.

## Permissions

The app ships with the permission set **All permissions** (object name *MuM IS All*). It determines the permissions for all tables, pages, and codeunits of the item status (Read, Insert, Modify, Delete on the data tables) and defines which actions users can perform in the module. Assign this set to the users or user groups that are to set up and assign item statuses. The assignment is done via the standard permission management of Business Central.

## Typical use cases

The following scenarios show the item status in a real workflow. All steps and messages are backed by the program code of this app.

### Discontinued item – still sell remaining stock, but no longer procure

**Trigger:** Sales reports that an item will be replaced by a successor product in the future. The existing inventory stock should still be sold off, but nothing more should be reordered or produced.

**Entry point in BC:** The master data manager creates a rule "Discontinued" in the **Item Status List**. On the **Item Status Card**, on the **Block Purchase** tab he activates all options as well as the manufacturing blocks on the **Block Manufacturing** tab; on the **Block Sales** tab he sets only **Allow Sales Till Available Stock**.

**Core flow:**
1. Via the **Item Card** of the affected item, he chooses **Set Item Status** and assigns the status "Discontinued"; he confirms the security prompt.
2. From now on, when entering a purchase order or a production order with this item, the system reports that the item is blocked.
3. If sales enters a sales line, the system checks availability: as long as stock is available, sales remain possible; once the stock is used up, the note about the discontinued part appears.

**Conclusion:** Every status change is traceable in the item's **Item Status History**.

### Quality block with automatic tightening

**Trigger:** Quality assurance detects a defect in a purchased part. The item should be blocked for manufacturing immediately and – if the defect is not fixed within a period – subsequently blocked completely.

**Entry point in BC:** The administrator creates two item statuses: "QA-Prod-Block" (only manufacturing blocked) and "QA-Full-Block" (all areas blocked). In the **Item St. Requalifications** he enters a rule with **Date Formula** (e.g. `14D`) and **Item Status To Set** = "QA-Full-Block" and stores its **Code** as the **Requalificationcode** in the "QA-Prod-Block" status.

**Core flow:**
1. Via the **Item Card**, QA sets the status "QA-Prod-Block"; **Item Status Set At** is set to the work date.
2. From now on, the system blocks the item in production orders.
3. The automatically created job queue entry **Act. Item Status** checks the period daily. Once the date calculated from **Item Status Set At** plus **Date Formula** is exceeded, it automatically sets the item to "QA-Full-Block".

**Conclusion:** The automatic transition creates another **Item Status Entry**, so that the escalation is documented completely.

### Warehouse and transfer block for a blocked item

**Trigger:** An item may neither leave a certain warehouse nor be transferred internally until a clarification has taken place.

**Entry point in BC:** On the **Item Status Card**, on the **Block Warehouse** tab the administrator activates, among others, **Block Warehouse Shipment**, **Block Pick**, **Block Transfer Order**, and **Block Reclass. Journal**, and assigns the status to the item.

**Core flow:**
1. When entering a transfer order line with this item, the system aborts with the blocking message.
2. Likewise, warehouse shipment and pick lines are rejected on insert.

**Conclusion:** After clarification, the administrator removes the blocks via **All Deactivate** on the **Warehouse** tab, or resets the item to a releasing status via **Set Item Status**.

## FAQ and troubleshooting

### Why can I no longer add an item to an order?
The item carries an **Item Status Code** in which **Block Purch. Order** is active. Check the assigned status via the **Item Card** (field **Item Status Code**) and, on the associated **Item Status Card**, the **Block Purchase** tab.

### What does the message "The Item … is blocked by the Item Status … ." mean?
The operation you are currently entering (e.g. an order or journal line) is blocked in the item's assigned item status. The message names the item, description, and code of the status so that you can find the responsible rule.

### Why does the system allow the sale even though the item is supposed to be blocked?
In the status, **Allow Sales Till Available Stock** is probably active. In that case an availability check replaces the hard block: as long as stock is available, the sale remains possible.

### What happens when no stock is available anymore and "Allow Sales Till Available Stock" is set?
The sales line is rejected with the note that the item is a discontinued part and only the still-available stock can be sold.

### Why does an item's item status change on its own?
A **requalification** is stored for the status. The daily job queue entry **Act. Item Status** automatically moves the item to the **Item Status To Set** after the period defined in the **Date Formula** has elapsed.

### Why was a job queue created after the first item status?
Creating the first item status automatically creates the recurring job queue entry **Act. Item Status**, which monitors the requalifications. By default it runs daily at 11:00 PM; you can adjust the schedule on the job queue entry card.

### Why can I not delete an item status?
Items are still assigned to the item status. The system rejects the deletion with the note that the item status must first be removed from the affected items.

### Why can I not delete a requalification?
The requalification code is still stored in at least one item status. Remove the **Requalificationcode** from the relevant item status first, then the requalification can be deleted.

### Why does the requalification require a date formula as soon as I enter an Item Status To Set?
Without a **Date Formula**, the expiration date cannot be calculated. As soon as an **Item Status To Set** is stored, the **Date Formula** field is therefore mandatory; otherwise the system rejects saving.

### How do I see who changed the item status and when?
Open the **Item Status History** action via the **Item Card**, or call up the **Item Status Entries** via the search. There, **Old Item Status Code**, **New Item Status Code**, **Set By**, and **Set At** are logged for each change.
