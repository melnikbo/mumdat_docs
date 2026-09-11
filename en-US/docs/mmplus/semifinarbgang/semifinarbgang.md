---
title: Anwenderhandbuch m+m Semifinished Items with Routing Status Overview
---

# User Guide m+m Semifinished Items with Routing Status Overview

## Introduction

The **m+m Semifinished Items with Routing Status Overview** app connects two existing m+m extensions in Microsoft Dynamics 365 Business Central: the **Routing Status View** (module *m+m Routing Status Overview*) and semi-finished item processing (module *m+m Semifinished Items*). The app itself does not add any pages, setup screens, or master data of its own. Its entire effect unfolds within an already existing view: the **Routing Status View** on the **Sales Order**.

Without this app, the Routing Status View shows only the operations of the **Production Order** that belongs directly to the Sales Order. However, if a production order contains **semi-finished items** — that is, production order lines that arise from upstream processing steps at a **Work Center** flagged as a semi-finished item — then their operations are missing from the standard view. This is exactly the gap the app closes: it adds the operations of the semi-finished item lines both in the graphical view **and** in the list view, so that the user can track the progress of the entire production process — the main item and all semi-finished stages — from a single place on the Sales Order.

### Target audience

The primary audience is **operational users** who work daily with sales orders and the associated production: internal sales, order processing, production control, and sales. They use the Routing Status View to give customers information about production progress and to coordinate their own scheduling. Secondarily, the app concerns **administrators**, who set up the prerequisites (installed dependencies, license, work centers flagged as semi-finished items) once.

### Brief process overview

1. The user creates a **Sales Order** and generates a **Production Order** from it.
2. If the production order contains operations at a semi-finished item work center, additional production order lines for the **semi-finished items** are created when the order is split (module *m+m Semifinished Items*).
3. On the Sales Order, the **Routing Status View** shows the status of all operations. Thanks to this app, the operations of the semi-finished item lines also appear there — indented as an additional **Level** in the list view and as further tiles in the graphical view.
4. The user reads off status, quantities, and dates and, when needed, jumps by click into the **Prod. Order Routing** or into the **Production Order**.

## Quick start for users

The app requires no setup of its own. Once the prerequisites are met (see **Prerequisites and permissions**), the fastest route to a result is:

1. Open the relevant **Sales Order**. To locate it, use the BC **Search** function or the order list of your Role Center.
2. On the Sales Order, select the **Sales Line** whose production progress you want to see. Below the sales lines, the **Routing Status View** area is displayed and automatically updated for the selected line.
3. In the **graphical view**, read off the progress by color (gray, green, red, blue — see **Color-coded status display**). The tiles of the semi-finished item operations are additionally shown by this app.
4. Use the **list view** below it for the detailed values per operation (**Level**, **Status**, **Production Order No.**, **Description**, **Quantity**, **Start Date/Start Time**, **End Date/End Time**, **Finished Quantity**).
5. Click a **tile** to open the **Prod. Order Routing** of the operation, or click the **Production Order No.** in the list to open the **Production Order**.

There is no posting, release, or finish step in this app. The statuses shown arise from the regular production feedback postings.

## Prerequisites and permissions

This app is a pure connector app and provides **no** setup pages, number series, or master data screens of its own. For the additional display to work, however, the following prerequisites from the base modules must be met. These prerequisites are set up once by the **administrator** before first use; they are then applied in day-to-day work on the **Sales Order**.

### Dependent modules

The app requires three installed m+m modules (from `app.json`):

| Prerequisite | Explanation |
|---------------|-------------|
| **m+m Cloud Base** | When installed, the shared base functions and the license check are available, without which the app cannot unlock its use at sign-in. |
| **m+m Routing Status Overview** | When installed, the **Routing Status View** area exists on the Sales Order in the first place; this app extends exactly this area with the semi-finished item operations. Without this module there is no display that could be supplemented. |
| **m+m Semifinished Items** | When installed, production order lines are flagged as **Semi-Finished Item** and linked to their originating line via a **Semi-Finished Item Source Line No.**; only this flagging provides the data that this app feeds into the display. |

### Semi-finished item work centers (maintained in the base module)

For semi-finished item lines to be created, at least one **Work Center** must be flagged as a **Semi-Finished Item** in the *m+m Semifinished Items* module. When the production order is created and split, the operations of this work center are transferred into separate production order lines with the **Semi-Finished Item** flag. This configuration is made **not** in this app but in the base module; it is mentioned here only as a functional prerequisite so that the user understands why additional lines and tiles appear.

### Permissions

The app supplies the assignable permission set **MuM SFRO All** (`permissionset 5613851`). This permission set defines which actions a user may perform within the scope of this app: it grants execution permission for the connector codeunit **MuM SFRO Routing Status Mgt.** Assign this permission set to all users who should use the extended Routing Status View on the Sales Order. Without this permission set, the supplementary display logic cannot be executed for the user. In addition, the license check runs automatically at sign-in via the m+m Cloud Base module; if no valid license is present, the additional function remains inactive.

## Routing Status View on the Sales Order

The **Routing Status View** area is displayed on the **Sales Order** below the sales lines. It consists of two coordinated parts: a **graphical view** (tiles per operation) and a **list view** (tabular detail lines). Both parts are related and updated to the currently selected **Sales Line**; if the user switches the sales line, both views update accordingly.

The actual contribution of this app: in both parts, the operations of the **semi-finished item** production order lines additionally appear. In the list view, these lines are indented via the **Level** field (tree display), so that their affiliation to the parent production order line remains visible.

### Graphical view

The graphical view presents the operations of the production order as tiles. On the left, the **Start Date** is shown; on the right, the **End Date** of the production order. Each tile contains the **Operation No.** and the **Description** of the operation; for semi-finished item operations, the associated **Item No.** is added so that the user can clearly identify the semi-finished stage. In addition, the tile shows the **Finished Quantity** of the respective operation.

Clicking a tile opens the **Prod. Order Routing** of the relevant production order. In this way, the user goes directly from the overview into the detailed processing of the routing.

#### Color-coded status display

The color of a tile depends on the **Routing Status** field of the respective operation in the **Prod. Order Routing**. The routing status is a field with a fixed set of values; for each value, the display means the following:

| Routing Status | Color and meaning |
|-------------------|---------------------|
| **(blank)** | If the routing status is blank, the tile appears **gray**: the operation is created but not yet started; no feedback postings exist. |
| **Planned** | If the routing status is *Planned*, the tile appears **green**: the operation is scheduled and intended for processing. |
| **In Progress** | If the routing status is *In Progress*, the tile appears **red**: work is currently being done on the operation, or partial feedback has been posted. |
| **Finished** | If the routing status is *Finished*, the tile appears **blue**: the operation is completed. |

In this way, the user obtains a real-time color overview of progress — for the operations of the main item as well as for the semi-finished item operations added by this app. In practice, feedback is posted operation by operation, so the tiles of a production order take on different colors.

### List view

Below the graphical view, the list view lists the operations and production order lines as detail lines. The semi-finished item lines are inserted by this app with **Level = 1** and are thereby displayed indented under their originating line. All fields are read-only (display only).

| Field | Explanation |
|------|-------------|
| **Level** | If the level is greater than 0, the line is a **semi-finished item** line added by this app; it is displayed indented under the parent production order line. Level 0 identifies the main line. |
| **Status** | Shows the production order status of the line (e.g. Released, Finished). It controls which Production Order screen opens when called up. |
| **Production Order No.** | If the user clicks this number, the associated **Production Order** opens in the screen matching the status (e.g. **Released Prod. Order** or **Finished Prod. Order**). |
| **Description** | Name of the production order line or the operation; serves for unambiguous identification in the tree structure. |
| **Quantity** | Planned quantity of the production order line. It forms the reference value against which the finished quantity is read. |
| **Start Date** | Planned start of the production order line; supports the scheduling information given to the customer. |
| **Start Time** | Planned start time complementing the Start Date for fine scheduling. |
| **End Date** | Planned end of the production order line; basis for the delivery date estimate. |
| **End Time** | Planned end time complementing the End Date. |
| **Finished Quantity** | If feedback has been posted, this field shows the quantity of the operation already finished; the comparison with **Quantity** shows the user the remaining progress. The value is determined from the operation's capacity ledger entries. |

### Navigation from the display

From the Routing Status View, two jump-offs are available to the user:

- **Clicking a tile** opens the **Prod. Order Routing** of the production order. There, the user sees the operations in detail (opened read-only).
- **Clicking the Production Order No. in the list** opens the **Production Order** itself. Depending on the **Status** of the line, the matching screen opens, e.g. **Released Prod. Order** or **Finished Prod. Order**.

Both jump-offs are display or edit jumps into standard screens; this app performs no posting and no status change in the process.

## FAQ and troubleshooting

### 1. Why do I suddenly see additional, indented lines in the Routing Status View on the Sales Order?

Because the production order contains **semi-finished item** lines. This app inserts their operations with **Level = 1** into the display, so that they appear indented under the respective main line. Without the app, only the operations of the main item would be visible.

### 2. What do the colors of the tiles mean?

The color follows the **Routing Status** field in the **Prod. Order Routing**: blank = gray, *Planned* = green, *In Progress* = red, *Finished* = blue. This makes the processing status of each operation recognizable at a glance.

### 3. Why does a tile stay gray even though the operation exists?

Because the **Routing Status** of this operation is still blank. As soon as the operation is scheduled or feedback is posted, the color changes to green, red, or blue. Gray means: created, but no feedback yet.

### 4. Why do no semi-finished item operations appear even though the production order should have some?

The lines are only added if the production order lines are actually flagged as **Semi-Finished Item** (flag **Semi-Finished Item = yes** and a set **Semi-Finished Item Source Line No.**). This flagging arises in the *m+m Semifinished Items* module when the production order is split. Check whether the relevant **Work Center** is flagged as a semi-finished item and whether the production order was split.

### 5. Where does the displayed finished quantity come from?

The **Finished Quantity** of an operation is summed from the capacity ledger entries of the production order (output quantity of the respective operation). It increases as soon as feedback on the operation is posted.

### 6. Which page opens when I click a tile?

The **Prod. Order Routing** of the associated production order. It opens read-only and shows the operations of the line in detail.

### 7. Which page opens when I click the Production Order No.?

The **Production Order** in the screen matching the **Status**, for example **Released Prod. Order** for released orders or **Finished Prod. Order** for finished orders.

### 8. Do I have to set anything up for this app?

No. The app requires no setup of its own. You only need to have the dependent modules installed, a valid license present, and the **MuM SFRO All** permission set assigned. The semi-finished item flagging of the work centers is done in the base module *m+m Semifinished Items*.

### 9. Why does the display change when I select a different sales line?

The Routing Status View always relates to the currently selected **Sales Line**. With multiple sales lines, the graphical and list views update according to the selected line.

### 10. Can I change quantities or status in the Routing Status View?

No. The display is read-only. You make changes to operations, quantities, or status in the **Prod. Order Routing** or in the **Production Order**; the display then reflects these values.

## Typical use cases

The following scenarios are based on the actual behavior of this app as traceable in the code (linking semi-finished item production lines to the Routing Status View on the Sales Order). They are deliberately kept brief.

### Use case 1: Customer call about the delivery status of a multi-stage order

- **Trigger:** A customer calls internal sales and asks about the production progress of an order whose item is manufactured via a semi-finished stage.
- **Entry in BC:** The user opens the **Sales Order** (via **Search** or the order list) and selects the relevant **Sales Line**. Below the sales lines, the **Routing Status View** appears.
- **Core flow:** In the **graphical view**, the user reads off the progress by color. Alongside the operations of the main item — thanks to this app — the tiles of the **semi-finished item** operations are visible (with **Operation No.**, **Description**, and **Item No.** of the semi-finished stage). Blue tiles show completed operations, red tiles show operations in progress, green tiles show planned ones, and gray tiles show operations not yet started. In the **list view**, the user checks **Finished Quantity** against **Quantity** and **End Date/End Time** if needed.
- **Conclusion:** Based on the colors and dates, the user gives the customer reliable information. For detailed questions, the user clicks a tile and opens the **Prod. Order Routing**.

### Use case 2: Internal progress check before fine scheduling

- **Trigger:** Production control wants to check, before the weekly planning, which semi-finished stages of a sales order are already finished.
- **Entry in BC:** Opening the **Sales Order** and selecting the relevant **Sales Line**; the **Routing Status View** is updated for this line.
- **Core flow:** In the **list view**, the user recognizes via the **Level** indentation which lines are semi-finished item operations. For each operation, the user compares **Finished Quantity** with **Quantity** and reads **Start Date/End Date**. Via the **Production Order No.**, the user jumps into the **Production Order** (**Released Prod. Order**) if needed to check capacities.
- **Conclusion:** Based on the visible progress, production control decides on the sequence of the next operations. This app performs no posting in the process; it provides only the consolidated status overview.
