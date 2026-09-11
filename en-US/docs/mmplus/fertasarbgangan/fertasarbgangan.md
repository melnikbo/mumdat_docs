---
title: Anwenderhandbuch m+m Production Order Assistant with Routing Status View
---

# User Guide m+m Production Order Assistant with Routing Status View

## Introduction

The **m+m Production Order Assistant with Routing Status View** app is an extension for **Microsoft Dynamics 365 Business Central**. It links two existing m+m functions with each other: the **Production Order Assistant**, which is used to create a production order directly from a sales line, and the graphical **Routing Status View**, which displays the progress of the associated production in the sales order.

Without this extension, the Routing Status View draws its data exclusively from **reservation entries** and **item ledger entries** that are linked to the sales line. In many order-related production scenarios, however, this reservation link does not exist (the production order was created directly from the sales line via the Production Order Assistant, but was not reserved against the sales line). In this case the view would remain empty.

This app closes exactly that gap: it ensures that the Routing Status View additionally takes into account **all production orders** that the Production Order Assistant created from the respective sales line. The assignment is not made through reservations, but through the source fields that the Production Order Assistant sets when creating the production order (Source Type **Sales Order**, source document number and source line number). As a result, the **routing status** of these production orders becomes directly visible in the sales order.

### Target Audience

The primary target audience are **operational users in sales and production** who trigger production orders from customer orders and track their progress on the sales order: order processors, production planners and sales support staff. Administrators are a secondary target audience; their task is limited to the one-time installation and the assignment of permissions (see **Prerequisites and Setup**), because the app intentionally has **no setup pages of its own**.

### Classification and Dependencies

The app is a pure connecting extension. It contains no pages, tables or setup fields of its own. Its entire effect is delivered through the following base modules, which must be installed:

- **m+m Production Order Assistant** — provides the **Production Order Assistant** action on the sales line and marks the created production orders with the source fields (Source Type, Source No., Source Line No.).
- **m+m Routing Status Overview** — provides the graphical **Routing Status View** in the sales order and supplies the base logic that determines which production order lines are displayed.
- **m+m Cloud Base** — technical base module.

This app merely extends the selection logic of the Routing Status View to include the production orders linked by the Production Order Assistant.

## Quick Start for Users

The fastest path from customer order to status tracking:

1. Open the **Sales Order** and enter the sales line with the item to be produced (Type **Item**, item number and quantity).
2. Select the sales line and choose the **Production Order Assistant** action from the **Line** line menu.
3. Confirm the **Production Order Assistant** view with **OK**. Business Central then creates the production order and links it to this sales line via the source fields.
4. Return to the **Sales Order**. The **Routing Status View** area below the sales lines updates automatically when you switch to the sales line and shows the routing progress of the linked production orders — graphically and as a line list.
5. Assess the progress based on the color (see the color legend under **Daily Work**) and, if needed, open the associated **Prod. Order Routing** or the production order with a click.

A separate setup step in day-to-day work is not required: as soon as the Production Order Assistant has created the production order, the link is set and the view is populated.

## Prerequisites and Setup

This extension has **no setup page, no setup table and no setup toggle of its own**. There are therefore no module-specific fields to maintain. Setup is limited to two administrative steps that must be carried out once before first use.

### Provide App Prerequisites

Who sets this up: Administrator. When: once before first use. Purpose: The display logic of this app only takes effect if the three base modules are present.

Ensure the following dependency chain in order:

1. **m+m Cloud Base** is installed (technical foundation).
2. **m+m Production Order Assistant** is installed. If this module is active, then the **Production Order Assistant** action is available on the sales line, and the production orders created carry the source fields through which this app links them.
3. **m+m Routing Status Overview** is installed. If this module is active, then the **Routing Status View** area appears in the sales order, which this app supplies with additional production order lines.
4. **m+m Production Order Assistant with Routing Status View** (this app) is installed. If this app is active, then the Routing Status View also displays the non-reserved production orders linked by the Production Order Assistant.

If one of the first three apps is missing, the additional logic has no effect; the base view then relies solely on reservation entries and item ledger entries.

### Assign Permission

Who sets this up: Administrator. When: during role assignment. Purpose: The permission set defines which actions users may perform with the function.

Assign the permission set **MuM PARO Permission** to the affected users. If this permission set is assigned to a role, then the display logic of this app may be executed for those users; the additional production order lines appear in the Routing Status View. Without this permission, the enhancement provided by this app remains inactive, while the base view continues to work. The permission set covers exclusively the execution of this app's internal display logic and does not grant any further rights to production or sales data; those rights come from the permission sets of the base modules.

## Daily Work on the Sales Order

The central workplace for this function is the **Sales Order**. Below the sales lines, the **Routing Status View** area shows the production progress for the currently selected sales line. The view consists of two parts: a **graphical representation** (status chart) and a **line list** of the associated production order lines.

The prerequisite for data to appear here are the base modules named in the **Prerequisites and Setup** chapter, as well as a production order that was created from the sales line via the **Production Order Assistant**. The content of the view is re-determined automatically each time the sales line is changed; a manual refresh is not required.

### Create a Production Order from the Sales Line

Who works here: order processor or production planner. When: as soon as an item to be produced is on the customer order.

1. Open the **Sales Order** and select the sales line.
2. Choose **Line** and then **Production Order Assistant**. The **Production Order Assistant** view opens.
3. Confirm with **OK**. When you confirm, then Business Central creates the production order and sets the source fields on the production order line (Source Type **Sales Order**, source document number and source line number of the sales line). It is precisely through these source fields that this app later finds the production order again and displays it in the Routing Status View.

The status in which the production order is created (for example planned, firm planned or released) depends on the setup of the Production Order Assistant and is not part of this app.

### Reading the Routing Status View

The line list of the Routing Status View contains the following columns for each displayed production order line. All columns are read-only; they serve as information and as an entry point into the details.

| Field | Explanation |
|---|---|
| **Level** | Shows the structural indentation of the line in the tree view. When a multi-level production is displayed, then the level makes visible which line is a parent and which is a child. |
| **Status** | Indicates the order status of the production order from which the line originates. The permitted values are explained below by meaning. |
| **Production Order No.** | Number of the production order. If you click this number, then the associated production order (or the Prod. Order Routing) opens, so you can check the details without a detour. |
| **Description** | Description of the production order line (usually the item to be produced). Serves for quick identification of the line. |
| **Quantity** | Quantity to be produced of the production order line. If you compare the target and finished quantities, then you can recognize the open remainder. |
| **Starting Date** | Planned start of production. If the starting date is in the future, then processing has not yet started as scheduled. |
| **Starting Time** | Planned start time supplementing the starting date in the case of more finely scheduled production. |
| **Ending Date** | Planned end of production. If the ending date has been exceeded and the order has not yet been finished, then there is a schedule delay. |
| **Ending Time** | Planned end time supplementing the ending date. |
| **Finished Quantity** | Quantity of the line already reported as finished. When the finished quantity reaches the quantity, then production of this line is complete; as long as it is smaller, a remaining quantity is still outstanding. |

**Values of the Status column** (order status of the production order):

- **Simulated:** The production order is a simulation and not yet effective for production; it serves for pre-costing.
- **Planned:** The production order is planned but not yet firm planned; dates and quantities can still shift.
- **Firm Planned:** The production order is firm planned; it is intended for production but not yet released.
- **Released:** The production order is released for production; output and postings are possible, the finished quantity can grow.
- **Finished:** The production order is finished; production is complete and no further output is to be expected.

The base view generally takes into account released and finished production orders from reservation entries and item ledger entries. Through this app, the production orders linked by the Production Order Assistant are added in addition, independent of any reservation.

### Color-Coded Status Display

The graphical representation colors each operation according to its **routing status** in the Prod. Order Routing. This way you recognize the progress at a glance without reading the line list. The coloring itself is determined by the **m+m Routing Status Overview** base module; this app only decides **which** production orders feed into the chart.

| Routing Status | Color | Meaning for the User |
|---|---|---|
| **Empty** | gray | No routing status has been set for the operation yet; processing is not yet scheduled. |
| **Planned** | green | The operation is scheduled; processing is imminent. |
| **In Progress** | red | The operation is currently being processed; it has been started but not yet completed. |
| **Finished** | blue | The operation is completed. |

### Switching to the Details

From the Routing Status View you reach the underlying documents directly without searching:

- A click on an entry in the chart or on the **Production Order No.** opens the **Prod. Order Routing** of the relevant production order. There you see the individual operations and their status in detail.
- Via the production order line you reach the production order itself in the status it is in (for example the released or the finished production order).

These drill-downs open read-only so that the status view is not changed inadvertently.

## FAQ and Troubleshooting

### 1. Why does nothing appear in the Routing Status View even though a production order exists?

The view is determined per **sales line**. Check whether the production order was actually created from exactly this sales line via the **Production Order Assistant** and whether the source fields are set. If the production order was created manually and without a reservation reference, neither the base view nor this app knows the link.

### 2. What is the difference between this app and the plain Routing Status View?

The base view (module m+m Routing Status Overview) is populated from **reservation entries** and **item ledger entries**. This app supplements it with production orders that the **Production Order Assistant** has linked to the sales line via the source fields — even when no reservation exists.

### 3. Why do I see a production order here even though it is not reserved against the sales line?

That is precisely the purpose of this app. It evaluates the source fields of the Production Order Assistant (Source Type **Sales Order**, source document number, source line number) and displays the matching production order lines, independent of reservation entries.

### 4. Which sales documents are taken into account?

The additional logic of this app takes effect for the Source Type **Sales Order**. The Production Order Assistant can also mark production orders with the Source Type **Sales Quote** or without a source type (**empty**); the Routing Status View of this app, however, is geared toward the sales order.

### 5. Do I have to refresh the view manually?

No. The view refreshes automatically as soon as you switch the line in the sales order. There is no separate refresh action for this area.

### 6. What do the colors gray, green, red and blue mean?

They reflect the **routing status** of the respective operation: gray = **Empty** (not yet scheduled), green = **Planned**, red = **In Progress**, blue = **Finished**. The color rule comes from the base module.

### 7. How do I get from the status area to the operations in detail?

Click the entry in the chart or the **Production Order No.** in the line list. The **Prod. Order Routing** of the production order opens with all operations.

### 8. Why is the status area empty even though the colors were displayed before?

Check whether all three base modules and this app are active and whether the permission set **MuM PARO Permission** is assigned to the users. If a prerequisite is missing, the view is populated only via the base logic (reservation/item ledger entries) or remains empty.

### 9. Can I change values in the status area?

No. All columns and the chart are read-only. You make changes in the production order or in the Prod. Order Routing, which you reach with a click.

### 10. How do I recognize that a production order was created via the Production Order Assistant?

On the production order or on the production order line, the source fields are set (Source Type, source document number, source line number). These fields are filled by the Production Order Assistant when creating the order and are at the same time the key through which this app includes the line in the Routing Status View.

## Typical Use Cases

### Use Case 1: Trigger and track order-related production

**Trigger:** A customer orders an item by phone that has to be produced specifically.

**Entry in BC:** The order processor enters the **Sales Order** with the sales line (item and quantity). On the sales line he chooses **Line** and then **Production Order Assistant**.

**Core flow:** In the **Production Order Assistant** view he confirms with **OK**. Business Central creates the production order and sets the source fields to Source Type **Sales Order** as well as to the document number and line number of the sales line. Back in the sales order, the processor switches to the sales line; the **Routing Status View** area updates and shows the production order line with columns such as **Status**, **Quantity** and **Finished Quantity** as well as the colored status chart.

**Conclusion:** In the further course, the processor tracks the color of the operations (green → red → blue) and the growing **Finished Quantity**. As soon as the operations are blue (**Finished**) and the finished quantity reaches the quantity, production is complete. For details he opens the **Prod. Order Routing** by clicking the **Production Order No.**.

### Use Case 2: See the progress of a non-reserved production order

**Trigger:** Production planning has created a production order via the Production Order Assistant but has not reserved it against the sales line. Sales asks about the status.

**Entry in BC:** The user opens the relevant **Sales Order** and selects the sales line.

**Core flow:** Without this app the Routing Status View would remain empty here, because no reservation entry exists. With this app, Business Central recognizes the production order via the source fields of the Production Order Assistant and displays its production order lines together with the routing status. The user reads the progress from the color and columns.

**Conclusion:** For follow-up questions, the user jumps via the **Production Order No.** into the **Prod. Order Routing** and reports the current routing status back to sales. A posting or release step is not required in this area; the view serves for information only.
