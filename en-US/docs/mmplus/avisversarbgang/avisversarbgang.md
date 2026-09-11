---
title: Anwenderhandbuch m+m Logistic Management with Routing Status Overview
---

# User Guide m+m Logistic Management with Routing Status Overview

## Introduction

The app **m+m Logistic Management with Routing Status Overview** connects two existing m+m extensions with each other: the **Shipment Planning** (from *m+m Logistic Management*) and the **Routing Status View** (from *m+m Routing Status Overview*). It adds an additional area **Routing Status View** to the **Shipment Planning Assignment and Inventory Control** page. This lets users see, directly within shipment planning, the production state of the goods on a selected shipment line, without having to leave the page.

**Target audience.** The primary audience is **operational users in shipping and inventory control** who work daily with the **Shipment Planning Assignment and Inventory Control** page: they assign sales lines to shipment planning, create warehouse documents, and in doing so need to recognize whether the associated **production orders** are already finished. Secondary beneficiaries are **production control and planning**, who want to answer queries about the production progress of a shipment line quickly.

**Brief process overview.** The app itself brings **no** setup, master data, or document pages of its own. Its entire functional contribution consists of showing the **Routing Status View** in the lower part of the **Shipment Planning Assignment and Inventory Control** page. When the user selects a line in the **Lines** list, the **Routing Status View** refreshes and shows the routing and production status of the production order that lies behind the sales line of that shipment line. A separate documentation for the m+m **Routing Status** app describes the view itself in detail; this guide describes the **combination** of both functions within shipment planning.

## Quick Start for Users

The app requires **no** setup. After installation, the **Routing Status View** is immediately available on the **Shipment Planning Assignment and Inventory Control** page. The fastest way to a result:

1. Open the **Shipment Planning Assignment and Inventory Control** page via the search in Business Central. (The page is a company-wide work page and is opened via **Search**.)
2. If needed, narrow down the positions to be displayed using the filters in the **General** area — at least the **Location Filter** and **Date Filter** are useful — and select **Refresh Data**.
3. In the **Lines** list, select the desired **line** (a position line, not a grouping line).
4. Read off the production status in the lower **Routing Status View** area: the view shows, by color and in the list, whether the production order is **firm planned**, **released**, **in progress**, or **finished**.
5. Jump to the detail: in the **Routing Status View** list, click the **Prod. Order No.** to open the associated **production order**, or click a tile to view the **Prod. Order Routing**.

The other actions on the page (**Create/Register Warehouse Documents**, **Post Warehouse Documents**) belong to the base module *m+m Logistic Management* and are described here only as context — see the section **Daily Work**.

## Setup

This extension requires **no separate setup**. It contains no setup page, no number series, and no controlling flags. As soon as the app is installed, the **Routing Status View** appears automatically on the **Shipment Planning Assignment and Inventory Control** page.

However, for the view to show **content**, the functional prerequisites from the underlying modules must be met:

- The **Shipment Planning** from *m+m Logistic Management* must be set up so that the **Shipment Planning Assignment and Inventory Control** page can be populated with shipment lines. The setup of this page (filter templates, locations, delivery tours) is part of the base module.
- A **production order** must exist for the selected shipment line. Only then can the app determine the production order via the sales line and display the routing status. If no production order exists, the **Routing Status View** area remains empty.
- The **m+m Routing Status Overview** (Routing Status) app provides the actual view. Its behavior (graphic, colors, output messages) is described in the separate m+m documentation on **Routing Status**.

## Daily Work: Shipment Planning Assignment and Routing Status View

This extension acts exclusively on the **Shipment Planning Assignment and Inventory Control** page. The user works there with shipment planning as usual; in addition, they observe the production progress of the currently selected line in the embedded **Routing Status View** area.

The page is controlled by the central setups of the base module (filter templates, locations, delivery tours from *m+m Logistic Management*). The app **Logistic Management with Routing Status Overview** itself controls none of that; it merely adds the view. The following structure describes the **combined interface** that the user actually sees.

### Entry Point and Page Structure

**Entry point:** Open the **Shipment Planning Assignment and Inventory Control** page via the search in Business Central. It is a company-wide work page (not a document-related call from a higher-level list) and is therefore reached via **Search**.

The page is structured from top to bottom into:

1. the **General** filter area,
2. the **Lines** list with the shipment positions,
3. the total lines **Selected Total Net Weight** / **Selected Total Gross Weight**,
4. the **Routing Status View** area added by this app.

### Filters (General Area)

Using the filters in the **General** area, you restrict which shipment positions appear in the **Lines** list. When a filter is set, the lines are narrowed down by the respective criterion; after each change, the list refreshes.

| Filter field | Explanation |
|------------|-------------|
| **Last Data Refresh** | Shows when the displayed lines were last recalculated; used to check whether the list is up to date. If the value seems outdated, select **Refresh Data**. |
| **User Filter Template Code** | When set, the stored filter values of the selected template are loaded and applied to the list; this lets you recall a recurring filter combination in one step, without setting all individual filters again. |
| **Group By** | When set, the lines are combined into groups (e.g. by date or delivery date); the list then shows grouping lines as a tree, under which the position lines are sorted. |
| **Date Filter** | When set, only lines within the specified period are shown; this lets you display, for example, only the positions relevant for today's shipment. |
| **Location Filter** | When set, only lines of the selected location are shown; this way you specifically process the shipment of one location. |
| **Customer Filter** | When set, only lines of the selected customers are shown; useful when you are preparing a specific customer delivery. |
| **Delivery Tour Filter** | When set, only lines of the selected delivery tour are shown; this way you assemble a tour. |
| **Post Code Filter** | When set, only lines with a matching post code are shown; helpful for regional tour planning. |
| **Country/Region Code Filter** | When set, only lines of the selected country or region are shown. |
| **Quantity Filter** | When set, only lines whose quantity matches the filter expression are shown; this way you separate, for example, partial from full quantities. |
| **Sales Order Filter** | When set, only lines of the selected sales orders are shown; this way you track a specific order. |
| **Item Category Filter** | When set, only lines of the selected item category are shown. |
| **Filter for Purchase Return Orders** | When set, only lines of the selected purchase complaints (return orders) are shown; this way you plan returns in the same view. |
| **Shipment Method Code Filter** | When set, only lines of the selected shipment method are shown. |

With the **Clear Filters for Assignment** action you reset all of the filters listed above; the list then again shows the unfiltered scope.

### Lines List

The **Lines** list is built as a tree (grouping and position lines). All columns are purely informational (not editable). The **Routing Status View** below always refers to the currently selected **position line** (lines of type Line); on a pure grouping line, the view remains empty.

| Field | Explanation |
|------|-------------|
| **Grouping Name** | Designation of the grouping line when **Group By** is active; names the collective line in the tree. |
| **Selected** | When marked, the line is earmarked for the further functions (e.g. create warehouse documents); you set or remove the mark via the **Select Lines** / **Deselect Lines** actions. |
| **Source No.** | Number of the source document (e.g. sales order) from which the shipment line originates; establishes the reference to the originating document. |
| **Item No.** | Item of the position; identifies the goods to be shipped. |
| **Variant Code** | Variant of the item, if maintained. |
| **Item Category Code** | Item category of the position; supports grouping and filtering. |
| **Location Code** | Location from which shipping takes place; determines which inventory is drawn upon. |
| **Description** | Item description. |
| **Description 2** | Additional item description. |
| **Quantity** | Position quantity of the shipment line. |
| **Remaining Quantity** | Still-open quantity of the position; shows how much is still to be shipped. |
| **Unit of Measure Code** | Unit of measure of the position. |
| **Reference No.** | Reference number (e.g. item reference/EAN), if stored. |
| **Gross Weight** | Gross weight of the position; feeds into the total lines. |
| **Net Weight** | Net weight of the position; feeds into the total lines. |
| **Shipment Date** | Date of the planned goods issue of the position. |
| **Planned Delivery Date** | Planned delivery date. |
| **Planned Shipment Date** | Planned shipment date. |
| **Requested Delivery Date** | Delivery date requested by the customer. |
| **Promised Delivery Date** | Delivery date promised to the customer. |
| **Delivery Tour Code** | Assigned delivery tour of the position. |
| **Ship-to Type** | Type of the ship-to address (e.g. default address or alternate address). |
| **Ship-to No.** | Number of the alternate ship-to address, if used. |
| **Ship-to Name** | Name of the ship-to address. |
| **Ship-to Name 2** | Name addendum of the ship-to address. |
| **Ship-to Address** | Street/address of the ship-to address. |
| **Ship-to Address 2** | Address addendum of the ship-to address. |
| **Ship-to City** | City of the ship-to address. |
| **Ship-to Post Code** | Post code of the ship-to address. |
| **Ship-to Country/Region Code** | Country/region of the ship-to address. |
| **Warehouse Process** | Indicates the intended warehouse process of the position (e.g. goods issue/picking); determines which follow-up documents are created. |
| **Warehouse Shipment Created** | When set, a warehouse shipment has already been created for the position; prevents duplicate document creation and shows the processing state. |
| **Warehouse Shipment No.** | Number of the created warehouse shipment; refers to the follow-up document. |
| **Warehouse Shipment Line No.** | Line number in the warehouse shipment. |
| **Pick Created** | When set, a pick has already been created; shows that the position is in progress in the warehouse. |
| **Pick No.** | Number of the created pick. |
| **Pick Line No.** | Line number in the pick. |
| **Production Order Created** | When set, a production order exists for the position; only then can the **Routing Status View** show a status. |
| **Prod. Order Status** | Production order status of the position (see status values below); shows how far production has progressed. |
| **Prod. Order No.** | Number of the associated production order. |
| **Finished Quantity** | Already-finished quantity of the production order; shows how much of the ordered quantity has already been produced. |
| **Quantity for Shipment Planning** | Quantity of the position available for shipment planning; basis of the assignment to the shipment. |
| **Shipment Method Code** | Shipment method of the position. |

**Prod. Order Status — meaning of the values.** The **Prod. Order Status** field reflects the status of the associated production order. The same values determine the color of the **Routing Status View**:

- **Simulated:** The production order serves only for preview/calculation; nothing is produced.
- **Planned:** The production order is planned, but not yet firm planned; no release to production yet.
- **Firm Planned:** The production order is firm planned, but not yet released — production cannot start yet.
- **Released:** The production order is released for production; output/postings on the routing operations are possible.
- **Finished:** The production order is completed; the goods are considered finished and ready for shipment.

### Totals

Below the list, the page summarizes the weights of the **selected** lines:

| Field | Explanation |
|------|-------------|
| **Selected Total Net Weight** | Sum of the net weight of all marked lines; supports loading and tour planning. |
| **Selected Total Gross Weight** | Sum of the gross weight of all marked lines. |

### Routing Status View (Added by This App)

The **Routing Status View** area is the actual contribution of this extension. It appears below the lines and shows, for the currently selected **position line**, the production status of the underlying **production order**. The basis is the sales line of the shipment line: the app determines the sales line for the **Source No.** and line, and hands it over to the view.

The view consists of two related parts:

- **Graphical view:** Tiles represent the operations of the production order. Their color depends on the state:
  - **Gray** — production order **firm planned**: not yet producible.
  - **Green** — production order **released**: ready for production.
  - **Red** — operation **started / in progress**: the order status itself does not change as a result.
  - **Blue** — operation or production order **finished**: production completed.
- **List view:** A tabular summary of the production order, including **Level**, **Status**, **Prod. Order No.** and quantities. Via the **Level**, multi-level production orders are displayed as a tree.

**Navigation out of the view.** A click on the **Prod. Order No.** in the list opens the associated production order — depending on the status, the **Simulated Prod. Order**, **Planned Prod. Order**, **Firm Planned Prod. Order**, **Released Prod. Order** or **Finished Prod. Order** card. A click on a tile opens the **Prod. Order Routing** of the production order. This way you get directly from the shipment line into the production order, without a detour, in order to continue working there.

> Note: If several sales lines exist for a sales order, the **Routing Status View** switches accordingly as soon as you mark a different **line**. The complete description of the view (graphic, output messages, processing of the production order) can be found in the separate m+m documentation **Routing Status**.

### Context: Warehouse Documents and Other Actions (Base Module)

The following actions are located on the same page, but belong to the base module *m+m Logistic Management* and are mentioned here only as context, so that the interface is fully understandable. They are not provided by this extension:

- **Selection:** **Select Lines**, **Deselect Lines**, **Show All Lines**, **Show Selected Lines** — control which lines are marked or visible.
- **Functions:** **Refresh Data**, **Add Lines to Shipment Planning**, **Clear Filters for Assignment**, **Create/Register Warehouse Documents**.
- **Post Warehouse Documents** and **Post and Send Warehouse Documents** — post the created warehouse documents; before posting, a confirmation prompt appears.
- **Line:** **Show Documents**, **Bin Content Overview**.
- **Documents:** **Shipment Planning** (opens the list of shipment plans).

For working with the **Routing Status View**, these actions are not required; the view refreshes solely through the selection of a line.

## FAQ and Troubleshooting

### 1. Why do I see nothing in the Routing Status View?
The view only fills when a **production order** exists for the marked **position line**. Check the **Production Order Created** field or the **Prod. Order No.** in the line. If no production order exists, the area remains empty.

### 2. Why does the view stay empty although a line is marked?
The app only evaluates lines of type **position line**. On a **grouping line** (with **Group By** active), nothing is displayed. Expand the group and mark an individual position.

### 3. Do I have to set up the app before I can use it?
No. The extension requires no setup of its own. The only prerequisite is that the base module's shipment planning is used and that a production order exists for the line.

### 4. How do I know whether the goods are finished?
If the **Prod. Order Status** is **Finished** and the tiles of the routing status view appear **blue**, the production order is completed and the goods are finished. The **Finished Quantity** field additionally shows the produced quantity.

### 5. What do the colors Gray, Green, Red, and Blue mean?
**Gray** = production order firm planned (not yet producible), **Green** = released (producible), **Red** = operation started/in progress, **Blue** = operation or production order finished.

### 6. Does the color Red change the status of the production order?
No. Red only indicates that at least one operation has been started or is in progress. The overarching **Prod. Order Status** (e.g. **Released**) remains unaffected by this.

### 7. How do I open the production order for a shipment line?
In the **Routing Status View** list, click the **Prod. Order No.**. Depending on the status, the matching production order card opens (**Firm Planned Prod. Order**, **Released Prod. Order**, **Finished Prod. Order**, etc.).

### 8. How do I see the individual operations?
In the graphical view, click a tile. The **Prod. Order Routing** of the production order opens, with the operations.

### 9. I have several sales lines — which one is shown?
Always the one belonging to the currently marked **line**. If you mark a different line, the view switches accordingly.

### 10. Where do I find the complete description of the view itself?
In the separate m+m documentation for the **Routing Status** app (*m+m Routing Status Overview*). This guide describes the integration of the view into the **Shipment Planning Assignment and Inventory Control**.

## Typical Use Cases

### Use Case 1: Check Shipment Release Only After Completion

**Trigger.** The shipping clerk wants to make sure, before creating the warehouse documents, that the goods of a customer position are already produced.

**Entry point in BC.** He opens the **Shipment Planning Assignment and Inventory Control** page via the search and narrows down the positions using the **Location Filter** and **Date Filter**; afterwards he selects **Refresh Data**.

**Core process.** In the **Lines** list, he marks the relevant position line. In the **Routing Status View** area, he recognizes the state: if the tiles are **blue** and the **Prod. Order Status** is **Finished**, the goods are finished. As a check, he additionally reviews **Finished Quantity**.

**Conclusion.** If the position is finished, he marks the line via **Select Lines** and initiates the further shipment processing of the base module (**Create/Register Warehouse Documents**). If the view is still **red** (in progress) or **gray** (firm planned), he postpones the position and turns to the next one.

### Use Case 2: Query About the Production Progress of a Shipment Line

**Trigger.** Planning receives a phone question about how far the production order for a specific shipment position has progressed.

**Entry point in BC.** The employee opens the **Shipment Planning Assignment and Inventory Control** page and sets the **Sales Order Filter** to the named order.

**Core process.** She marks the relevant **line**. The **Routing Status View** shows the graphic and list of the production order. From the color of the tiles she reads off which operations have already been started (**red**) or finished (**blue**).

**Conclusion.** For details, she clicks the **Prod. Order No.** in the list and opens the **Released Prod. Order**; via a tile she calls up the **Prod. Order Routing** if needed and answers the query based on the concrete operation progress.
