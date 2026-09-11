---
title: Anwenderhandbuch m+m Production Order Overview
---

# User Guide m+m Production Order Overview

## Introduction

The **m+m Production Order Overview** app extends Microsoft Dynamics 365 Business Central with a central overview of all production order lines (prod. order lines). By default, Business Central spreads this information across several order types (Simulated, Planned, Firm Planned, Released, Finished) and across the respective production order header. The **Prod. Order Line List** brings together all prod. order lines of these status values on a **single** page and makes the **Prod. Order Components**, **operations** and **sales lines** belonging to a line immediately visible.

**Target audience:** The app is primarily aimed at **operational users in manufacturing** – production control, work scheduling and shop-floor workers who work daily with open and released production orders, check quantities, change statuses and jump from the overview into the production journal and the operations. Planners and schedulers who want a filtered overall view of the stock of production order lines benefit as a secondary audience.

**Brief process overview:** The user opens the **Prod. Order Line List**, selects a prod. order line in the upper table and automatically sees the assigned components and sales lines below it, as well as – in the info pane on the right – the operations of the line. From the same page, the user calls the most important functions of a production order without the detour via the document header: Show Document, Change Status, open Components, start Production Journal and open Prod. Order Routing. Using the filter icon, the user filters the view by their own criteria and saves these views as personal views.

This app brings **no setup pages of its own, no master data of its own and no posting routine of its own**. It is a pure evaluation and control interface built on the standard tables of Business Central. All functions that are called (status change, journal, operations, document display) are standard Business Central functions that are merely made accessible from the overview.

## Quick Start for Users

The fastest path to the most important results:

1. **Open the Prod. Order Line List.** Call the **Prod. Order Line List** page via the Business Central search (**Search**). The page can be found as a list page under the usage category *Lists* and requires no prior setup.
2. **Select a prod. order line.** In the upper table, select the desired production order line. By default the view shows all lines from status **Planned** upwards (**Planned**, **Firm Planned**, **Released**, **Finished**), sorted by status, **Prod. Order No.** and **Line No.**.
3. **Read the assigned data.** As soon as you select a prod. order line, the middle area **Prod. Order Components** and the lower area **Sales Lines** fill automatically with the data belonging to the line. On the right, the info pane **Operation for prod. order line** shows the operations of the selected line.
4. **Run a function.** If needed, use the ribbon actions to call one of the following standard functions: **Show Document**, **Change Status**, **Components**, **Production Journal** or **Prod. Order Routing**.
5. **Filter and save the view.** Using the filter icon, set a filter (for example **Status** = **Released**) and save the result as a personal view so you can call it up again later.

> The app does not enforce a fixed sequence of setup steps. Since it is built exclusively on standard tables, production orders and their lines are the only prerequisite; these arise in the standard Business Central process.

## Structure of the Prod. Order Line List

The **Prod. Order Line List** page (page type List, source table *Prod. Order Line*) is divided into three vertically stacked areas and supplemented by an info pane on the right. The upper area is the actual list of prod. order lines; the two lower areas and the info pane are subpages that update automatically when the selected prod. order line changes.

The record selection of the upper list is fixed via the source table view to prod. order lines from status **Planned** (`where(Status = filter(Planned ..))`); simulated lines therefore only appear if their status is set accordingly. Creating new records and deleting are blocked in the overview; editing is generally allowed but is mostly disabled at the field level (see the section **Editing Prod. Order Lines**).

### Upper area – Prod. Order Lines

The upper area lists the production order lines in tabular form. The following table describes the columns that are most important from a business perspective; the complete set of columns corresponds to the fields of the standard table *Prod. Order Line* and can be shown and hidden via personalization.

| Field | Explanation |
|------|-------------|
| **Status** | Shows the production order status of the line. The value controls which functions are allowed and whether the line can be posted in the **Production Journal**. Possible values: **Simulated:** non-binding simulation, no posting; **Planned:** generated from planning, not yet confirmed; **Firm Planned:** firmly scheduled, not yet released; **Released:** released for production – only in this status is the **Production Journal** possible; **Finished:** completed, no further postings. |
| **Prod. Order No.** | Number of the production order to which the line belongs. Serves as the jump target for **Show Document** and as the filter criterion for the assigned components and sales lines. |
| **Line No.** | Sequential number of the line within the production order. Together with **Prod. Order No.** and **Status**, it determines which components and operations are shown in the lower area and in the info pane. |
| **Item No.** | The item to be produced on the line. |
| **Variant Code** | Item variant of the line, provided the item is managed with variants. |
| **Description** / **Description 2** | Description of the item from the line. |
| **Location Code** | Location to which the production of the line is assigned. |
| **Quantity** | Target quantity of the production order line. |
| **Finished Quantity** | Quantity already reported back as output. Increases with each output posting; when it reaches the **Quantity**, the line is completed in terms of quantity. |
| **Remaining Quantity** | Quantity still open (target quantity less finished quantity). Decreases with each feedback; at zero there is nothing more to produce. |
| **Scrap %** | Scrap surcharge in percent that is taken into account in the quantity calculation. |
| **Due Date**, **Starting Date**/**Starting Time**, **Ending Date**/**Ending Time** | Scheduling fields of the line from detailed planning. |
| **Routing No.** | Assigned routing. This field is editable in the statuses **Simulated**, **Planned** and **Firm Planned**; see **Editing Prod. Order Lines**. |
| **Production BOM No.** | Assigned production BOM of the line. |
| **Unit Cost**, **Cost Amount**, **Expected Operation Cost Amount**, **Expected Component Cost Amount** | Value and cost fields of the line for cost control. |

All fields of the upper area are **not editable** by default and serve for display. The only exception is the **Routing No.** in the plannable statuses (see below).

#### Editing Prod. Order Lines

In the statuses **Simulated**, **Planned** and **Firm Planned**, the overview allows editing the **Routing No.** directly in the line; in the statuses **Released** and **Finished** this field is locked. When you change the **Routing No.** in a plannable status, the prompt **"Do you want to update the production order?"** appears:

- If you confirm the prompt, the app applies the new **Routing No.** to the production order and recalculates the order backward (the routing is redetermined; components and due date remain unchanged). The view is then updated.
- If you decline the prompt, the change is not carried out.

### Middle area – Prod. Order Components

The middle area **Assigned Prod. Order Component** (subpage on the standard table *Prod. Order Component*) shows the material components of the prod. order line selected above. The area is intended for display only and filters automatically on **Status**, **Prod. Order No.** and **Line No.** of the selected line.

| Field | Explanation |
|------|-------------|
| **Item No.** | Component item that is required for the production of the line. |
| **Description** / **Description 2** | Description of the component. **Description 2** is loaded for display from the item or – if a variant is set – from the item variant. |
| **Variant Code** | Variant code of the component. |
| **Position**, **Position 2**, **Position 3** | Position information of the component from the production BOM. |
| **Unit of Measure Code** | Unit of measure of the component. |
| **Quantity** / **Quantity per** | Required quantity or quantity per unit of the end item. |
| **Expected Quantity** | Material requirement calculated from the target quantity and the BOM quantity. |
| **Remaining Quantity** | Quantity of the component not yet consumed. |
| **Act. Consumption (Qty)** | Quantity of the component already posted as consumption. |
| **Flushing Method** | Controls how consumption is posted: manual posting, forward flushing at production start, or backward flushing at output reporting. |
| **Location Code**, **Bin Code** | Warehouse assignment of the component. |
| **Due Date** / **Due Time** | Provisioning date of the component. |
| **Scrap %** | Scrap surcharge of the component. |
| **Qty. to Pick**, **Qty. Picked**, **Completely Picked** | Picking status of the component for material provisioning. |
| **Unit Cost**, **Cost Amount**, **Direct Cost Amount**, **Overhead Rate**, **Indirect Cost %** | Value and cost fields of the component. |

### Lower area – Sales Lines

The lower area **Sales Lines** (subpage on the standard table *Sales Line*) shows the sales lines that are related to the prod. order line selected above. The area is read-only.

The link is not established via a simple key, but via the reservation logic of Business Central: the app first determines the reserved sales lines via the **Reservation Entries** of the prod. order line. If it finds no reservation, it evaluates the **Item Ledger Entries** of the type Output of the production instead and determines the associated sales line from those. In this way the user sees which customer orders are tied to the selected production.

| Field | Explanation |
|------|-------------|
| **Document Type** | Type of the sales document (e.g. Order) of the line. |
| **Document No.** | Number of the sales document. |
| **Sell-to Customer No.** | Number of the customer to whom the sale is made. |
| **Sell-to Customer Name** | Name of the customer. The app adds this field as a derived field (see the section **Extension of the Sales Line**) and displays the customer name directly next to the customer number, so the user can identify the customer without opening the document. |
| **Type** | Line type of the sales line (e.g. Item). |
| **No.** | Item or general ledger number of the sales line. |
| **Description** | Description of the sales line. |
| **Location Code** | Location of the sales line. |
| **Reserve** | Reservation method of the sales line. |
| **Quantity** | Quantity sold. |
| **Reserved Quantity (Base)** | Quantity already reserved in base units. |
| **Unit of Measure Code** | Unit of measure of the sales line. |
| **Line Amount** | Amount of the sales line (zero values are hidden). |
| **Shipment Date** | Planned shipment date of the sales line. |
| **Remaining Quantity** | Quantity of the sales line not yet shipped. |

Via the line actions of the lower area (group **Line**), the following are available for the selected sales line:

- **Show Document** – opens the associated sales document.
- **Reservation Entries** – shows the reservation entries of the line.
- **Item Tracking Lines** – opens the item tracking (lot/serial numbers) of the line.

### Info pane – Operations and Components

On the right the page shows two info boxes:

- **Operation for prod. order line** (standard table *Prod. Order Routing Line*): shows the operations for the selected prod. order line with **Operation No.**, **No.** (work center/machine center), **Description**, **Setup Time** and **Run Time**. The box is read-only and filters on **Routing No.**, **Routing Reference No.**, **Prod. Order No.** and **Status** of the selected line.
- **Components** (standard table *Prod. Order Component*): compact material view with **Item No.** and **Variant Code**. This box is hidden by default and can be shown via personalization.

## Functions in the Ribbon

From the Prod. Order Line List, the user calls functions that in the standard would only be available via the production order header. All functions are accessible as promoted actions in the ribbon and refer to the prod. order line selected above or its production order.

| Action | Explanation |
|--------|-------------|
| **Show Document** | Opens the production order of the selected line in the appropriate document view. The app chooses the view based on the status: **Simulated Prod. Order**, **Planned Prod. Order**, **Firm Planned Prod. Order**, **Released Prod. Order** or **Finished Prod. Order**. There the user has – according to their permissions – all the usual functions of the document available. |
| **Change Status** | Starts the standard function for changing the status of the production order. This way the user can, for example, set the order from **Firm Planned** to **Released**; only after that is feedback via the **Production Journal** possible. |
| **Components** | Opens the standard view **Prod. Order Components** for the selected line. Link: **Status**, **Prod. Order No.** and **Line No.** of the line. Keyboard shortcut Alt+K. |
| **Production Journal** | Creates the posting data and opens the production journal, in which the user – with the appropriate permissions – posts consumption and output of the line. The action is only permitted in status **Released**; in other statuses the app rejects execution. Keyboard shortcut Alt+P. |
| **Prod. Order Routing** | Opens the standard view of the operations of the production order. Link: **Status**, **Prod. Order No.**, **Routing No.** and **Routing Reference No.** of the line. |

## Filters and Personal Views

The Prod. Order Line List gives the user the option to narrow down the view with the standard filter functions of Business Central and to save the result as a **personal view**.

This is how you proceed:

1. Click the **filter icon** at the top right. The filter pane opens on the left edge of the page.
2. Set a filter on one or more columns – for example **Status** = **Released**. The list then shows only the matching prod. order lines.
3. Save the filtered view via the three-dots menu with **Save As…** under a name of your own.
4. Repeat the procedure for further criteria, for example for **Firm Planned** production orders.

The next time you call the Prod. Order Line List, you select one of the saved views with a click and immediately continue working with the desired narrowing. The filtering uses the standard Business Central mechanism for views; the app brings no filter fields of its own.

## Extension of the Sales Line

The app extends the standard table *Sales Line* by a single, derived field that serves exclusively for display in the lower area of the overview:

| Field | Explanation |
|------|-------------|
| **Sell-to Customer Name** | Derived field (FlowField) that looks up the name of the customer from the customer table based on the **Sell-to Customer No.**. When this field is shown in the **Sales Lines** area, the user recognizes the customer directly in the line without having to open the sales document or the customer master. The field is read-only and does not change any data. |

The field is released as a read/write field for personalizations, but is used by the app itself for read access only.

## Permissions

The app supplies the permission set **All Permissions** (AL object `MuM PL Permission`). This set defines which actions the users may perform within the app: it includes the execute permission on the pages of the Prod. Order Line List (upper list, subpages for components and sales lines, both info boxes) as well as on the internal license check.

Since the app accesses standard tables, the **standard permissions** of Business Central on manufacturing, sales and warehouse additionally determine, for the actual data display and editing, which fields a user can see and change. Editing in the overview (for example the **Routing No.**) and posting via the **Production Journal** require the corresponding standard permissions.

## License Check

At sign-in the app checks, via the m+m base module, whether a valid license for the app exists. This check runs technically in the background and requires no user action. Without a valid license the functions of the app are not available; in that case contact your system administrator.

## Typical Use Cases

### Use Case 1: Report Back a Released Production

**Trigger:** A worker reports to production control that a production order is completed and is to be posted.

**Entry in BC:** Production control opens the **Prod. Order Line List** via the **Search**.

**Core sequence:**
1. Select the relevant prod. order line in the upper list; for quick narrowing, first activate the saved view **Status = Released** or use the **filter icon**.
2. In the middle area, check the **Prod. Order Components** and their **Remaining Quantity**; in the info pane **Operation for prod. order line**, check the operations.
3. Open the production journal via the **Production Journal** action. The prerequisite is status **Released**; the app creates the posting data and opens the journal.
4. Post consumption and output in the standard journal.

**Conclusion:** After posting, the **Finished Quantity** of the line increases and the **Remaining Quantity** decreases. Once production is complete, production control changes the order to **Finished** via **Change Status**.

### Use Case 2: Check the Customer Reference of a Production

**Trigger:** Sales calls to ask which customer order a particular production is running for and when it can be delivered.

**Entry in BC:** Production control opens the **Prod. Order Line List** and finds the prod. order line via a filter on **Prod. Order No.** or **Item No.**.

**Core sequence:**
1. Select the relevant prod. order line in the upper list.
2. In the lower area **Sales Lines**, read off the assigned customer orders: **Document No.**, **Sell-to Customer Name**, **Quantity**, **Remaining Quantity** and **Shipment Date**.
3. If needed, open the sales document via the line action **Show Document**, or trace the assignment in detail via **Item Tracking Lines** or **Reservation Entries**.

**Conclusion:** The user tells sales the customer, quantity and planned shipment date – without having to switch between production order, reservation and sales order.

### Use Case 3: Adjust the Routing of a Planned Line

**Trigger:** In work scheduling it turns out that a production order not yet released should be produced using a different routing.

**Entry in BC:** Work scheduling opens the **Prod. Order Line List** and filters on **Status = Firm Planned** (or **Planned**).

**Core sequence:**
1. Select the prod. order line to be changed.
2. In the **Routing No.** column, enter the new routing. Since the line is plannable, the field is editable.
3. Confirm the prompt **"Do you want to update the production order?"**. The app applies the new routing to the production order and recalculates it backward.

**Conclusion:** In the info pane **Operation for prod. order line**, the operations of the new routing appear. If needed, the **Prod. Order Routing** action opens the full standard view for checking.

## FAQ and Troubleshooting

### 1. Why do I not see any simulated production orders in the Prod. Order Line List?
The upper list is fixed via the source table view to lines from status **Planned** (`Status = filter(Planned ..)`). Lines of a purely simulated character only appear if their status lies within this range. Check the **Status** of the line.

### 2. Why can I not edit most fields in the upper list?
The overview is deliberately mostly read-only and serves for evaluation and control. The only editable field is the **Routing No.**, and even that only in the statuses **Simulated**, **Planned** and **Firm Planned**. You make field changes to quantities, dates and costs in the respective standard document, which you open via **Show Document**.

### 3. Why does the prompt "Do you want to update the production order?" appear when I change the Routing No.?
A changed **Routing No.** affects the operations and dates of the production order. Only when you confirm the prompt does the app apply the new routing to the order and recalculate it backward. If you decline, the previous routing remains in place.

### 4. Why is the Routing No. field locked for released and finished lines?
From status **Released** onward, the order is in production; a subsequent routing change via the overview is therefore prevented. In the plannable statuses **Simulated**, **Planned** and **Firm Planned**, the field is editable, however.

### 5. Why can the Production Journal not be started?
The **Production Journal** action is only permitted in status **Released**. For an order in another status, the app rejects execution. First set the order to **Released** via **Change Status**.

### 6. Why is no data shown in the middle and lower areas?
Both areas filter on the prod. order line selected above. Select a line in the upper list; only then do **Prod. Order Components** and **Sales Lines** fill. If a line shows no components, the order has none for that line; if it shows no sales lines, there is no reservation or output assignment to a sales document.

### 7. Why do I see sales lines for a prod. order line even though I did not expect a direct link?
The lower area determines the sales lines via the **Reservation Entries** of the prod. order line. If a reservation is missing, the app evaluates the **Item Ledger Entries** of the type Output of the production instead. This way, sales lines are also shown that are only connected to the production via the actual output.

### 8. Why is the customer name displayed next to the customer number?
The app extends the sales line with the derived field **Sell-to Customer Name**, which looks up the name based on the **Sell-to Customer No.**. This way you recognize the customer directly in the line without opening the document.

### 9. How do I quickly call up recurring evaluations?
Using the **filter icon**, set the desired criteria and save the result via **Save As…** as a personal view. The next time you open the Prod. Order Line List, activate this view with a click. The views are personal and are permanently available to you.

### 10. Do I have to set up the app before I can use it?
No. The app brings no setup pages of its own and no master data of its own. The only prerequisites are existing production orders from the standard process as well as the appropriate standard permissions for manufacturing, sales and warehouse. For the full range of functions, a valid license must also be present.
