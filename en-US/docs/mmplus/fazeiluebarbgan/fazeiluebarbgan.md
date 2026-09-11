---
title: Anwenderhandbuch m+m Production Order Overview with Routing Status Overview
---

# User Guide m+m Production Order Overview with Routing Status Overview

## Introduction

The m+m app "Production Order Overview with Routing Status Overview" connects two existing m+m modules: the **Prod. Order Line List** (overview of production order lines) and the **Routing Status View**. The app adds an additional area to the **Prod. Order Line List** that shows, for the currently selected production order line, the status of all operations both graphically and as a list.

As a result, the user works on **one** page: on the left, in the line overview, they select a production order and, immediately below, see the processing state of that production order's individual operations — without having to open the production order or the associated routing separately.

**Target audience:** The primary audience is **operational users in production control** — production controllers, work schedulers, and staff who monitor the progress of running production orders and trigger follow-up actions (change status, post in the journal, open the routing). Planners and order coordinators use the overview secondarily for rough-cut and schedule control.

**Brief process overview:** Production orders are created and scheduled in the BC standard or in the upstream m+m modules. In the **Prod. Order Line List**, the user monitors the resulting production order lines. The app extends this line overview with the **Routing Status View**, which makes the feedback state of each operation visible in real time. From there, the user branches, when needed, into the **routing**, into the production order, or into the further actions of the line overview.

**Setup:** Using this app requires **no separate setup**. There are no dedicated setup pages, number series, or master data. After installation, the **Routing Status View** is automatically available in the **Prod. Order Line List**. The only prerequisite is that the dependent modules (m+m Cloud Base, m+m Production Order Overview, m+m Routing Status Overview) are installed.

## Quick start for users

The fastest path from opening the overview to checking the status of an operation:

1. Use **Search** to open the **Prod. Order Line List** page. The page is discoverable as a list page and can be reached without a higher-level entry page.
2. In the line list, select the desired **production order line** (the columns **Status**, **Prod. Order No.**, and **Item No.** help with the selection).
3. In the lower **Routing Status View** area, read off the progress: each tile represents one operation; the color shows the processing state (see the *Color logic* section).
4. Click a **tile** to view the production order's **routing** (action **Prod. Order Routing**).
5. When needed, use the list form of the view to switch directly into the matching **production order** by clicking the **Prod. Order No.**
6. Trigger follow-up actions from the **Prod. Order Line List**: **Change Status**, **Production Journal**, **Components**, or **Prod. Order Routing** (see the *Actions* section).

No preparatory setup steps are necessary; the quick start begins directly with opening the list.

## The Prod. Order Line List

The **Prod. Order Line List** is the central list page of this interplay. It shows the lines of all production orders from status **Planned** upward and is sorted by **Status**, **Prod. Order No.**, and **Line No.** The page itself is not editable (with the exception of the **Routing No.**, see below); creating and deleting lines is blocked on this page. It can be opened directly via **Search**.

The app extends this page: directly above the **Assigned Prod. Order Component** area, the **Routing Status View** is displayed, which automatically updates to the selected production order line on every line change.

### Columns of the line list

The following table describes the columns of the **Prod. Order Line List**. All columns are read-only and serve for information; the only exception is the **Routing No.**

| Field | Explanation |
|------|-------------|
| **Status** | Shows the document status of the line's production order (e.g. Planned, Firm Planned, Released, Finished). When you select a line, this determines which production order is addressed when opening or when changing the status. |
| **Prod. Order No.** | Number of the production order. If you use this number for orientation, you can identify which order the line and the operations shown below belong to. |
| **Line No.** | Sequential number of the production order line. When an order has several lines, the Line No. distinguishes the individual positions to be produced. |
| **Item No.** | Item to be produced by the line. When you select the line, the Routing Status View refers to the production of exactly this item. |
| **Variant Code** | Variant of the item. When a variant is set, the production progress concerns this variant of the item. |
| **Description** | Name of the item or line for quick identification. |
| **Description 2** | Supplementary second name line, if maintained. |
| **Location Code** | Location for which the line is produced. When set, it assigns the production order to a location. |
| **Shortcut Dimension 1 Code** | Value of the line's first global dimension; serves for accounting assignment. |
| **Shortcut Dimension 2 Code** | Value of the line's second global dimension; serves for accounting assignment. |
| **Bin Code** | Bin within the location, provided the location is bin-managed. |
| **Quantity** | Planned production quantity of the line. It is the reference value for Finished Quantity and Remaining Quantity. |
| **Finished Quantity** | Good quantity of the line already reported/posted. When this value rises, the Remaining Quantity decreases accordingly; it shows the production progress achieved. |
| **Remaining Quantity** | Quantity still open (Quantity minus Finished Quantity). When the Remaining Quantity reaches 0, the planned quantity of the line has been fully produced. |
| **Scrap %** | Planned scrap share of the line as a percentage. When set, the production order calculates a quantity surcharge for expected scrap. |
| **Due Date** | Date by which the line should be finished. It serves for schedule and backlog control. |
| **Starting Date** | Planned start of the line's production. |
| **Starting Time** | Planned start time of the line's production. |
| **Ending Date** | Planned end of the line's production. |
| **Ending Time** | Planned end time of the line's production. |
| **Planning Level Code** | Identifies the planning level of the line in multi-level production. |
| **Priority** | Priority of the line; supports sequencing when orders compete. |
| **Production BOM No.** | Production BOM used by the line; determines which components are required. |
| **Routing No.** | Routing used by the line. This field is editable: when you change it and confirm the prompt, the system transfers the new Routing No. into the production order and recalculates the routing backward — the operations shown below change accordingly. |
| **Inventory Posting Group** | Controls G/L account determination for the line's inventory-related postings. |
| **Routing Reference No.** | Reference number by which the line is linked to the associated operations of the routing. |
| **Unit Cost** | Unit cost per unit of the line; basis for value determination. |
| **Cost Amount** | Calculated cost amount of the line. |
| **Reserved Quantity** | Quantity reserved for the line; shows how much demand is already covered by reservations. |
| **Unit of Measure Code** | Unit of measure of the line in which Quantity and Finished Quantity are kept. |
| **Quantity (Base)** | Quantity in the item's base unit of measure. |
| **Finished Quantity (Base)** | Finished Quantity in the base unit of measure. |
| **Remaining Quantity (Base)** | Remaining Quantity in the base unit of measure. |
| **Reserved Quantity (Base)** | Reserved Quantity in the base unit of measure. |
| **Expected Operation Cost Amount** | Expected cost amount from the line's operations. |
| **Exp. Oper. Output (Qty.)** | Expected total quantity resulting from the line's operations. |
| **Expected Component Cost Amount** | Expected cost amount from the line's components. |
| **Starting Date-Time** | Combined start point (date and time) of the line. |
| **Ending Date-Time** | Combined end point (date and time) of the line. |
| **Cost Amount (ACY)** | Cost amount in the additional reporting currency. |
| **Unit Cost (ACY)** | Unit cost in the additional reporting currency. |
| **Production BOM Version Code** | Version of the production BOM used. |
| **Routing Version Code** | Version of the routing used. |
| **Routing Type** | Type of the routing (e.g. serial or parallel); influences the scheduling of the operations. |
| **Qty. per Unit of Measure** | Conversion factor between the unit of measure and the base unit of measure. |
| **MPS Order** | Identifies whether the line originates from master production scheduling. |
| **Planning Flexibility** | Controls whether the line may be moved by planning; with "None" the date remains fixed. |
| **Indirect Cost %** | Surcharge for indirect costs per unit of the line. |
| **Overhead Rate** | Fixed overhead surcharge per unit of the line. |

> Note on the **Routing No.**: This change acts directly on the production order. Confirm the safety prompt only if the routing is genuinely to be swapped — the system then reschedules the operations.

### Further areas of the page

Besides the line list and the **Routing Status View**, the page displays accompanying additional areas that relate to the selected line:

- **Assigned Prod. Order Component** — subpage with the components of the selected production order line (read-only); shows which material the line consumes.
- **Sales Lines** — subpage with the sales lines that triggered the demand for the production order; establishes the link between production and customer order.
- Additionally, fact boxes for the **operations** and the **material components** of the selected line are displayed.

## Routing Status View

The **Routing Status View** is the area that this app adds to the **Prod. Order Line List**. It consists of two related parts: a **graphical view** (tiles) and a **list view** (table). Both always refer to the production order line currently selected in the line list and update automatically on every line change.

### Graphical view

The graphical view presents the production order's operations as tiles side by side:

- On the left edge is the **Starting Date-Time**, on the right edge the **Ending Date-Time** of the production order — so the time span of the production can be read off.
- Each **tile** represents one operation. On the tile are the **description** of the operation and, in parentheses, the **operation number**.
- A smaller tile below shows the **Finished Quantity** of the respective operation, so that the progress achieved per operation is visible.
- The operation currently in progress is highlighted separately. The basis is the production order's last capacity ledger entry: the operation to which the most recent feedback was posted is considered the active operation.
- A **click on a tile** opens the production order's **routing** (the **Prod. Order Routing** page) in a read-only view. Thus the user gets from the status overview into the detail view of the routing with one click.

#### Color logic of the tiles

The color of a tile combines the document status of the production order and the feedback state of the operation. The view derives the color from the status of the production order as well as from the routing status (field **Routing Status** of the routing line):

- **Gray — Firm Planned:** The production order is in status **Firm Planned**. When a tile is gray, the operation is scheduled, but production cannot yet take place.
- **Green — Released:** The production order has been set to **Released**. When the tile is green, the operation is released for production and can be processed.
- **Red — Started/in progress:** The operation has been started or is in progress. When the tile is red, feedback is being posted to this operation; the document status of the production order does not change as a result.
- **Blue — Finished:** The operation has been set to **Finished** by a corresponding report/posting. When the production order as a whole is set to **Finished**, all associated operations also appear blue.

> In practice, the operations are posted or reported one after another, so that the tiles of a production order show different colors at the same time — from this the user recognizes at a glance which operation is already completed, which is currently running, and which is still outstanding.

### List view

Below the graphical tiles, the list view shows the same production order lines as a table. It is read-only and indented as a tree structure (field **Level**), so that multi-level productions (production order with sub-orders) are recognizable hierarchically.

| Field | Explanation |
|------|-------------|
| **Level** | Indentation level of the line in multi-level productions. When the level is greater than 0, the line belongs to a subordinate production order; the tree structure makes the production hierarchy visible. |
| **Status** | Document status of the line's production order; assigns the line to the same status range as in the upper line list. |
| **Prod. Order No.** | Number of the production order. A click on the number opens the production order matching the status (Simulated, Planned, Firm Planned, Released, or Finished), in which the user can edit the order with all functions. |
| **Description** | Name of the production order line for quick identification. |
| **Quantity** | Planned production quantity of the line; reference value for the Finished Quantity. |
| **Starting Date** | Planned start of the line's production. |
| **Starting Time** | Planned start time of the line's production. |
| **Ending Date** | Planned end of the line's production. |
| **Ending Time** | Planned end time of the line's production. |
| **Finished Quantity** | Good quantity of the line already produced. When this value reaches the Quantity, the line is fully produced in terms of quantity. |

By clicking the **Prod. Order No.** in this list, the user gets directly into the production order; from there they can continue to process the order with the standard functions (including status change, line maintenance).

## Actions

The actions are available in the ribbon of the **Prod. Order Line List** and relate to the currently selected production order line. They are additionally available as promoted actions in the process area.

| Action | Explanation |
|--------|-------------|
| **Show Document** | Opens the production order of the selected line in the document matching the status (Simulated, Planned, Firm Planned, Released, or Finished). When you choose this action, you edit the complete production order instead of just the line. |
| **Change Status** | Starts the status change of the production order via the BC standard function. When you change the status (e.g. from Firm Planned to Released or from Released to Finished), the color of the tiles in the Routing Status View also changes afterward. |
| **Components** | Opens the production order components of the selected line. When you choose this action, you check and maintain the material demand of the line. (Shortcut Alt+K.) |
| **Production Journal** | Opens the production journal for the selected line. Prerequisite: the production order has status **Released** — otherwise the system rejects the action. When you report consumption and finished quantity here, the Finished Quantity rises and the colors/quantities in the Routing Status View update. (Shortcut Alt+P.) |
| **Prod. Order Routing** | Opens the routing (the operations) of the selected line's production order. When you choose this action, you view and edit the operations in detail — the same detail view that clicking a tile also opens. |

> To create and delete production order lines, the user uses the standard functions of the respective production order (reachable via **Show Document** or by clicking the Prod. Order No.). The technical prerequisites must be met (e.g. no already posted entries on the line).

## Typical use cases

The following scenarios show how the app is used in daily operations. All described pages, columns, and actions correspond to the actual behavior of the **Prod. Order Line List** with **Routing Status View**.

### Progress check following an inquiry from sales

**Trigger:** Sales calls and asks how far along the production of a customer order is.

**Entry in BC:** The production controller opens the **Prod. Order Line List** via **Search** and selects the line with the matching **Prod. Order No.** or **Item No.**

**Core flow:** In the **Routing Status View** they read off from the tile colors which operations are already **blue** (finished), which one is currently **red** (in progress), and which are still **green** (released, but not started). The small tiles show them the **Finished Quantity** per operation. Via the **Sales Lines** subpage they link the production to the triggering sales line.

**Conclusion:** They give sales the current status. For detailed questions, they click a tile and open the **Prod. Order Routing** to name the dates of individual operations.

### Releasing a firm planned production order

**Trigger:** A firm planned order is to go into production.

**Entry in BC:** The user opens the **Prod. Order Line List** and selects the relevant line — the tiles of the operations are initially **gray** (status **Firm Planned**).

**Core flow:** They choose the **Change Status** action and set the production order to **Released** via the BC standard function. After the update, the tiles in the **Routing Status View** appear **green** — the operations are now ready for production.

**Conclusion:** Afterward, at production start, the user can post the first feedback via **Production Journal**; the affected tiles then switch to **red**.

### Posting the feedback of an operation

**Trigger:** From production comes the report that an operation has been processed or is finished.

**Entry in BC:** The user selects the associated line in the **Prod. Order Line List** (the status must be **Released**).

**Core flow:** They open the production journal via **Production Journal** (Alt+P) and report the consumption and finished quantity of the operation. After posting, the **Routing Status View** updates: the **Finished Quantity** of the affected tile rises, and the tile color shows the new feedback state (red for running, blue for finished processing).

**Conclusion:** Once all operations are blue, the production of the line is complete; the user can set the order to **Finished** via **Change Status**.

## FAQ and troubleshooting

### 1. Do I have to set up the app before use?
No. The app requires no separate setup, no number series, and no master data. After installing the app and its dependent modules, the **Routing Status View** automatically appears in the **Prod. Order Line List**.

### 2. Where do I find the Prod. Order Line List?
You open the page via **Search**. The **Prod. Order Line List** is directly discoverable as a list page and requires no entry via a higher-level page.

### 3. Why do I not see any simulated production orders in the overview?
The **Prod. Order Line List** shows production order lines only from status **Planned** upward. Lines in status **Simulated** are deliberately not listed.

### 4. What do the colors of the tiles mean?
**Gray** = production order **Firm Planned** (not yet producible), **Green** = **Released** (ready for production), **Red** = operation **started/in progress**, **Blue** = operation **Finished**. An operation marked red does not change the document status of the production order.

### 5. Why are all tiles colored the same?
This occurs when all operations are in the same state. In normal operation, operations are posted/reported one after another, so that the tiles show different colors depending on progress.

### 6. How do I open the routing of a production order?
In the graphical view, click a **tile**, or in the **Prod. Order Line List** choose the **Prod. Order Routing** action. Both open the production order's routing in a read-only view.

### 7. How do I recognize the operation currently running?
The view evaluates the production order's last capacity ledger entry and highlights the operation to which feedback was most recently posted. This is considered the active operation.

### 8. Why can the production journal not be opened?
The **Production Journal** action requires status **Released**. If the production order is still **Firm Planned** or already **Finished**, the system rejects the action. First set the order to **Released** via **Change Status**.

### 9. What happens when I change the Routing No. in the line?
After a safety prompt, the system transfers the new **Routing No.** into the production order and reschedules the routing backward. Afterward, the **Routing Status View** shows the operations of the new routing. Confirm the prompt only for an intended routing swap.

### 10. Why does the view update after a posting?
The **Routing Status View** is bound to the selected line and is rebuilt on every line change as well as when the page is opened. After feedback in the production journal, the tile colors and the **Finished Quantity** immediately reflect the new production progress.
