---
title: m+m EDI mit Logistikmanagement
---

# User Guide m+m EDI with Logistic Management

## Introduction

The app **m+m EDI with Logistic Management** connects the EDI classification **Automotive** from the app
**m+m EDI Base** with the **Shipment Planning** from the app **m+m Logistic Management**. It ensures that
automotive-relevant sales orders are recognized in Shipment Planning, filtered in a targeted way, and assigned a
reserved shipment number upon release. In this way, an automotive-relevant warehouse shipment receives a fixed
number—drawn from the **Shipping No. Series** of the sales order—already before posting.

**Prerequisite** is that the following m+m apps are installed and set up:

- **m+m Logistic Management** (Shipment Planning, warehouse shipments, user filter template),
- **m+m EDI Base** (field **Automotive** on the customer and on the sales order),
- **m+m Cloud Base**.

**Target audience.** The primary users are **operational shipment planners and warehouse dispatchers** who assign,
release, and generate warehouse shipments for lines in the Shipment Planning worksheet on a daily basis. Secondary
users are **administrators and key users** who set up the automotive classification on the customer and the user
filter templates.

**Brief process overview.** The administrator classifies automotive-relevant customers; this causes the field
**Automotive** on the sales order to be set and validated. The planner opens **Shipment Planning**, restricts the
worksheet using the **Automotive** filter, and assigns the lines. With **Release**, the app reserves a
**Reserved Shipment No.** for each automotive-relevant sales order line. When the warehouse documents are created and
posted, this reserved number is used as the shipment no. of the posted sales shipment.

## Quick start for users

The fastest path from classification to the reserved warehouse shipment. The setup steps deliberately come before the
daily work, because they are a prerequisite.

1. **Setup (one-time, administrator):** On the **Customer**, on the **EDI** tab, set the field **Automotive** to
   **Yes**. As a result, when a sales order is created for this customer, the header field **Automotive** is set
   automatically and may no longer be removed.
2. **Setup (one-time, administrator):** Make sure a **Shipping No. Series** is defined on the sales order; the app
   draws the reserved number from this series.
3. **Setup (one-time, key user):** Create a **User Filter Template** of type **Shipment Planning** and, on the
   **Shipment Planning Filters** tab, set the field **Automotive** to **Yes** (automotive only) or **No** (without
   automotive).
4. **Daily work:** Open **Shipment Planning** and switch to the Shipment Planning worksheet.
5. **Daily work:** In the filter area, set the field **Automotive** to **Yes** to display only automotive-relevant
   sales lines, and assign the desired lines via **Qty. to Assign**.
6. **Daily work:** Choose **Release**. For each automotive-relevant line, a **Reserved Shipment No.** is now assigned
   from the Shipping No. Series of the sales order.
7. **Daily work:** Choose **Create Warehouse Documents** and then **Post Warehouse Documents**. The posted warehouse
   shipment receives the reserved shipment no. of the sales order.

## Setup

The setup of this app does not consist of a dedicated setup page, but rather of a **chain across several pages**: the
automotive classification on the customer and sales order (from **m+m EDI Base**), the Shipping No. Series on the sales
order, and the **User Filter Template** (from **m+m Logistic Management**), which is extended by the field
**Automotive**. The following sections describe this chain in dependency order.

### Setting up automotive shipment control

**Who and when.** The administrator sets up this chain once before the first productive shipping day; the key user
maintains the filter templates. The setup is a prerequisite for the section **Daily work in the Shipment Planning
worksheet** and the **Release** action there.

**Sequence in dependency order:**

1. **First**, classify the **Customer** as automotive-relevant (field **Automotive**, see the section
   *Automotive classification on the customer*). If **Automotive** = **Yes** is set on the customer, then
   Business Central carries this classification over to new sales orders of this customer and enforces it there.
2. **Then**, check the header field **Automotive** on the **Sales Order** (see the section *Automotive classification
   on the sales order*). If the field is set, then the lines of this order are treated as automotive-relevant in
   Shipment Planning and, upon release, assigned a reserved shipment number.
3. **Then**, make sure a **Shipping No. Series** is defined on the sales order. If a series is present, then, upon
   release, the app can draw the **Reserved Shipment No.** from it; if the series is missing, the reservation is
   omitted for that line.
4. **Then**, create a **User Filter Template** of type **Shipment Planning** and set the **Automotive** filter (see the
   section *User Filter Template: setting up the Automotive filter*). If the filter is set, then the worksheet already
   starts with the desired automotive restriction.
5. **Finally**, in daily operations the planner filters the Shipment Planning worksheet and chooses **Release**—this
   completes the chain (see **Daily work in the Shipment Planning worksheet**).

### Automotive classification on the customer

**Process.** The administrator maintains this indicator on the customer before automotive-relevant orders are
recorded. The field originates from **m+m EDI Base** and is the top-level prerequisite of the entire chain; it controls
whether the app applies the shipment number reservation at all for orders of this customer.

**Entry point:** In the **Customer List**, open the customer card and switch to the **EDI** tab.

| Field | Explanation |
|---|---|
| **Automotive** | Controls the automotive relevance of the customer. If **Yes** is set, then every new sales order of this customer is mandatorily considered automotive-relevant and the header field **Automotive** cannot be removed on the order. With **(blank)**, the customer is not automotive-relevant; the field **Automotive** then cannot be set on the order. **Yes:** permanently automotive-relevant, indicator enforced on the order. **No:** customer generally EDI-capable, but not necessarily automotive—the order indicator is selectable. **(blank):** no automotive use, order indicator locked. |

Further reading: The set indicator takes effect in the **Daily work in the Shipment Planning worksheet** (filter and
number reservation).

### Automotive classification on the sales order

**Process.** The header field is derived from the customer when the order is created and is validated by the system.
The sales clerk checks it before the order flows into Shipment Planning.

**Entry point:** Open the **Sales Order** and switch to the **EDI** tab.

| Field | Explanation |
|---|---|
| **Automotive** | Marks the individual sales order as automotive-relevant. If set, then the associated sales lines are captured in the Shipment Planning worksheet via the Automotive filter and, upon release of the shipment planning, assigned a **Reserved Shipment No.**. The field can only be set if the customer is automotive-capable; if the customer is set to **Automotive = Yes**, the indicator on the order cannot be removed. |

### User Filter Template: setting up the Automotive filter

**Process.** The key user maintains one or more filter templates for Shipment Planning per user. This app extends the
template with the field **Automotive**, so that a planner can immediately restrict the worksheet to automotive- or
non-automotive-relevant lines without setting the filter anew every day. The template is used in the section **Daily
work in the Shipment Planning worksheet**.

**Entry point:** From the list of **User Filter Template**, open the corresponding card and there the **Shipment
Planning Filters** tab.

Header and control fields of the template (from **m+m Logistic Management**, so that you can set up the entire page):

| Setup | Explanation |
|---|---|
| **Code** | Unique key of the template. If assigned, then the planner can select the template specifically in the worksheet. |
| **Description** | Plain-text designation. If maintained, then the user finds the appropriate template in the selection more quickly. |
| **User ID** | Assigns the template to a user. If set, then only this user sees and uses the template in their Shipment Planning. |
| **Type** | Defines the area of use of the template. For this app, the type must be **Shipment Planning** so that the template takes effect in the Shipment Planning worksheet. |
| **Default Filter** | If activated, then this template is applied automatically when the worksheet is opened, without the user selecting it manually. |
| **Date Formula** | Determines the relative date frame (e.g. up to today). If maintained, then the **Date Filter** in the worksheet is prefilled. |
| **Automotive** | **Added by this app.** Controls the automotive preselection of the template. If **Yes** is set, then the worksheet, when the template is applied, shows only lines of automotive-relevant sales orders. With **No**, only non-automotive-relevant lines are displayed. With **(blank)**, no Automotive filter takes effect and all lines appear. **(blank):** no restriction. **Yes:** automotive only. **No:** non-automotive only. |

Prefilled filter values of the template (transferred to the filter area of the worksheet when applied):

| Setup | Explanation |
|---|---|
| **Date Filter** | If set, then only lines up to the specified shipment date are displayed in the worksheet. |
| **Shipment Tour Filter** | If set, then only lines of the selected delivery tour(s) are displayed. |
| **Customer Filter** | If set, then only lines of the selected customers are displayed. |
| **Location Filter** | If set, then only lines of the selected locations are displayed. |
| **Post Code Filter** | If set, then only lines with a matching ship-to post code are displayed. |
| **Country/Region Code Filter** | If set, then only lines of the selected country or region are displayed. |
| **Item Category Filter** | If set, then only lines of the selected item category(ies) are displayed. |

**Validation/dependency.** The template takes effect only if its **Type** = **Shipment Planning** and it belongs to
the logged-in user (**User ID**). The Automotive filter of this template is functionally identical to the filter field
**Automotive** in the worksheet (see **Daily work in the Shipment Planning worksheet**).

## Master data

This app does not create its own master data. The relevant master data are the **automotive classification on the
customer** and the classification derived from it on the **sales order**—both are already described in detail in the
section **Setup** as a prerequisite, because they have both a setup and a master data character. Maintain the customer
classification before automotive-relevant orders are recorded; it appears as a column in the sales order list and as a
field on the **EDI** tab of the sales order card.

## Daily work in the Shipment Planning worksheet

The Shipment Planning worksheet is the planner's central workspace. It collects open sales and transfer lines based on
the set filters, lets them be assigned, and triggers release, warehouse document creation, and posting. This app
extends the worksheet with the **Automotive** filter and an **Automotive** column in the lines, and couples the
reservation of the shipment number to the release.

**Control from other pages.** Which lines appear here, and whether a number is reserved, depends on the pages
maintained in the section **Setup**: the **Automotive** classification on the **Customer** and **Sales Order** (feature
activation, mandatory indicator), the **Shipping No. Series** on the sales order (number assignment), and the **User
Filter Template** (UI prefill of the Automotive filter).

### Filter

The filter area of the worksheet determines which lines are collected. This app adds the field **Automotive** to the
filter area; the remaining filters originate from **m+m Logistic Management** and act together.

| Filter field | Explanation |
|---|---|
| **Automotive** | **Added by this app.** If **Yes** is set, then only sales lines whose sales order has the header field **Automotive** set are displayed. With **No**, only lines of non-automotive-relevant orders are displayed. With **(blank)**, no Automotive filter takes effect. **(blank):** no restriction. **Yes:** automotive only. **No:** non-automotive only. |
| **Date Filter** | If set, then only lines up to the specified shipment date are collected. |
| **Shipment Tour Filter** | If set, then only lines of the selected delivery tour(s) are collected. |
| **Customer Filter** | If set, then only lines of the selected customers are collected. |
| **Location Filter** | If set, then only lines of the selected locations are collected. |
| **Post Code Filter** | If set, then only lines with a matching ship-to post code are collected. |
| **Country/Region Code Filter** | If set, then only lines of the selected country or region are collected. |
| **Item Category Filter** | If set, then only lines of the selected item category(ies) are collected. |

### Lines in the worksheet

The lines show the sales and transfer positions to be assigned. This app adds the column **Automotive**; the remaining
columns originate from **m+m Logistic Management** and serve the assignment.

| Field | Explanation |
|---|---|
| **Automotive** | **Added by this app.** If checked, then the line originates from an automotive-relevant sales order; the line flows into the shipment number reservation upon release. Without the indicator, the line is treated like a normal shipment line and receives no reserved number. |
| **Selected** | If marked, then the line is selected for further processing. |
| **Document No.** | Document number of the shipment planning to which the line belongs. |
| **Source Type** | Indicates the source of the line (e.g. sales line). If sales line, then the automotive number reservation applies; other sources are not affected by it. |
| **Source No.** | Number of the source document (e.g. the sales order) from which the reserved shipment no. is drawn. |
| **Item No.** | Item of the line. |
| **Location Code** | Location from which delivery is made; it is part of the grouping for shared number reservation. |
| **Qty. to Assign** | The quantity to be assigned to the shipment. If a value other than 0 is set, then the line is taken into account upon release and reserved if applicable. |
| **Shipment Date** | Planned shipment date of the line. |
| **Ship-to Type** / **Ship-to No.** | Ship-to address type and number; together they determine the grouping in which a reserved shipment no. is reused. |

### Releasing and reserving the shipment number

**Process.** After the assignment, the planner releases the shipment planning. The app hooks into this release and
assigns a fixed shipment number to automotive-relevant sales lines.

1. In **Shipment Planning**, select the line or header to be processed.
2. Choose **Release** (keyboard shortcut Ctrl+F9). For each sales order line with **Qty. to Assign** other than 0, the
   app checks the **Automotive** indicator.
3. If the line is automotive-relevant and still without a **Shipment No.** and without an existing **Reserved Shipment
   No.**, then the app draws the next number from the **Shipping No. Series** of the sales order and enters it as the
   **Reserved Shipment No.**. If a reservation already exists for the same combination of source document, location
   code, and ship-to address, then this number is reused, so that lines belonging together receive the same shipment
   number.
4. With **Reset Status**, you cancel a release again if you need to change the assignment.

**Note on partial assignment.** You do not have to assign the entire order quantity at once. Lines with a partial
quantity in **Qty. to Assign** are reserved upon release in the same way; a complete coverage of the order quantity is
not a condition for the release.

### Creating and posting warehouse documents

**Process.** From the released shipment planning, the planner generates and posts the warehouse shipments. In doing so,
the app carries the reserved number over into the posted document.

1. Choose **Create Warehouse Documents**. When the shipment planning lines are registered, the **Automotive** indicator
   and the **Reserved Shipment No.** are transferred to the registered line.
2. Choose **Post Warehouse Documents**. When the **warehouse shipment** is posted, the app writes the **Reserved
   Shipment No.** into the **Shipment No.** field of the sales order, so that the posted sales shipment receives exactly
   this reserved number.
3. After the sales document is posted, the reserved number is released again: if the posted document carries a shipment
   no. that is still reserved on a planning line, then the app clears the **Shipment No.** field on the sales order, so
   that the number is not assigned twice.

## Header and lines of the shipment planning

In addition to the worksheet, the app also extends the detail view of the shipment planning, so that the planner sees
the automotive relevance directly on the document.

### Header of the shipment planning

**Entry point:** Open **Shipment Planning** and select the desired document.

| Field | Explanation |
|---|---|
| **Automotive Exists** | **Added by this app.** Read-only indicator in the header. If checked, then the shipment planning contains at least one automotive-relevant line; the planner thus knows immediately that a shipment number reservation will be triggered upon release. If the indicator is not set, the document contains no automotive-relevant lines. |

### Lines of the shipment planning

**Entry point:** In the opened **Shipment Planning**, in the lines area (subpage).

| Field | Explanation |
|---|---|
| **Automotive** | **Added by this app.** If checked, then the line is automotive-relevant and is included in the number reservation upon release. |
| **Reserved Shipment No.** | **Added by this app.** Read-only field. Shows the shipment number reserved from the **Shipping No. Series** upon release. If filled, then the later posted warehouse shipment receives exactly this number as the shipment no. If the field is empty, no number was reserved for the line (e.g. because it is not automotive-relevant or already has a shipment no.). |

## History and tracking

The app does not maintain its own history lists. The automotive indicators and reserved numbers are, however, carried
along during registration:

- In the **Registered Shipment Planning** and **Registered Shipment Planning Line**, the **Automotive** indicator and
  the **Reserved Shipment No.** remain available, so that the assignment stays traceable after registration.
- Via the navigation actions of the shipment planning (**Sales Orders**, **Warehouse Shipments**), you move from the
  planning to the generated documents and can there check the assigned **Shipment No.**.

## Typical use cases

The following scenarios show the app in day-to-day business. Each sequence is substantiated via code and translations
of this module.

### Use case 1: Releasing an automotive call-off

- **Trigger:** For an automotive-relevant customer, there is a confirmed sales order that is to be shipped today.
- **Entry point in BC:** The planner opens the **Shipment Planning** of the shipping day and switches to the Shipment
  Planning worksheet.
- **Core sequence:**
  1. In the filter area, they set **Automotive** to **Yes**; the worksheet shows only automotive-relevant sales lines.
  2. They enter the **Qty. to Assign** in the desired lines.
  3. They choose **Release**. For each automotive-relevant line, a **Reserved Shipment No.** is assigned from the
     **Shipping No. Series** of the sales order; in the header, **Automotive Exists** is checked.
  4. They choose **Create Warehouse Documents** and then **Post Warehouse Documents**.
- **Conclusion:** The posted warehouse shipment carries the reserved **Shipment No.**; the assignment remains traceable
  in the registered shipment planning.

### Use case 2: Hiding non-automotive lines

- **Trigger:** On a mixed shipping day, the planner wants to initially exclude the automotive-relevant positions and
  prepare the regular shipment.
- **Entry point in BC:** Open **Shipment Planning**, call up the Shipment Planning worksheet.
- **Core sequence:**
  1. They select a **User Filter Template** in which **Automotive** = **No** is stored, or set the **Automotive** filter
     in the worksheet directly to **No**.
  2. The worksheet shows only lines of non-automotive-relevant orders; automotive positions do not appear.
  3. They assign the displayed lines and process them regularly via **Release** and the warehouse documents.
- **Conclusion:** The automotive-relevant lines remain unprocessed and can be released in a separate run with
  **Automotive** = **Yes**.

### Use case 3: Giving lines that belong together a single number

- **Trigger:** An automotive-relevant order comprises several positions to the same location and the same ship-to
  address, which are to go out as one shipment.
- **Entry point in BC:** **Shipment Planning** and Shipment Planning worksheet, filter **Automotive** = **Yes**.
- **Core sequence:**
  1. The planner assigns all affected lines via **Qty. to Assign**.
  2. Upon **Release**, the app recognizes the same combination of **Source No.**, **Location Code**, and ship-to address
     (**Ship-to Type**/**Ship-to No.**) and assigns all lines the same **Reserved Shipment No.**.
- **Conclusion:** The joint warehouse shipment is posted with a uniform shipment number.

## FAQ and troubleshooting

### 1. Why does an automotive-relevant order not appear in the filtered worksheet?

Check the **Automotive** filter: if it is set to **No**, automotive lines are deliberately hidden. Also check whether
the header field **Automotive** is set on the **Sales Order**—only then is the line considered automotive-relevant.

### 2. Why is the Automotive field not settable on the sales order?

The field can only be set if the associated **Customer** is automotive-capable. If **Automotive** is set to **(blank)**
on the customer, setting it on the order is prevented with a message. First set the indicator on the customer.

### 3. Why can I no longer remove the Automotive indicator on the order?

If the customer is set to **Automotive = Yes**, it is permanently considered automotive-relevant. The order indicator
is then mandatory and cannot be revoked.

### 4. Why does the Reserved Shipment No. remain empty upon release?

A number is only drawn if the line is automotive-relevant, originates from a **sales line**, delivers to a
**customer**, does not yet have a **Shipment No.**, and a **Shipping No. Series** is defined on the sales order. If the
series is missing, the reservation is omitted.

### 5. Why do several lines have the same Reserved Shipment No.?

This is intentional: lines with the same **Source No.**, the same **Location Code**, and the same ship-to address
(**Ship-to Type**/**Ship-to No.**) belong to one shipment and share the same reserved shipment number.

### 6. When does the reserved number actually become the shipment no. of the document?

Upon **posting** the warehouse shipment, the app writes the **Reserved Shipment No.** into the **Shipment No.** field of
the sales order, so that the posted sales shipment receives this number.

### 7. Why is the Shipment No. on the sales order empty again after posting?

After the sales document is posted, the app releases a number still reserved on a planning line by clearing the
**Shipment No.** field on the order. This prevents the same reserved number from being assigned again.

### 8. Do I have to assign the full order quantity before I am allowed to release?

No. Partial quantities in **Qty. to Assign** are also reserved upon **release**; a complete coverage of the order
quantity is not a prerequisite.

### 9. How do I set it up so that my worksheet always shows only automotive lines?

Create a **User Filter Template** of type **Shipment Planning** with **Automotive** = **Yes** and activate **Default
Filter**. When the worksheet is opened, the template is then applied automatically.

### 10. Do I see on the shipment planning header whether automotive-relevant lines are contained?

Yes. The header field **Automotive Exists** is checked as soon as the shipment planning contains at least one
automotive-relevant line.
