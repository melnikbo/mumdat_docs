---
title: Anwenderhandbuch m+m Unit Conversion with Logistic Management
---

# User Guide m+m Unit Conversion with Logistic Management

## Introduction

The m+m "Unit Conversion with Logistic Management" app combines
**unit conversion** (KG / Meter / Piece) with the documents of Advice
Notification and Shipment Planning in "Microsoft Dynamics 365 Business Central".
As soon as an item is maintained in **KG**, **Meter** and **Piece**, these three
quantity measures are also available in the **Advice Notification**, in the
**Shipment Planning** and in the **Item Tracking Assignment**. When the user
enters one of these measures, the app calculates the other two automatically and
transfers the assigned quantities into the downstream logistic documents
(purchase line, sales line, transfer line, warehouse receipt line, warehouse
shipment line).

The app brings **no pages of its own, no actions of its own and no setup pages
of its own**. It supplements existing pages of the base modules with additional
quantity columns and calculates in the background. The user interface therefore
remains the familiar interface of the Advice Notification and Shipment Planning;
what is new are the **KG**, **Meter**, **Piece** columns and their derived values.

### Target audience

The primary target audience are **operational users** in Purchasing, Sales and
Logistics who work with the Advice Notification and Shipment Planning every day:
they capture documents, assign quantities and trigger the **Register** step. The
secondary target audience are **administrators** who set up the prerequisites
(see [Setup](#setup)).

### Prerequisites

The app is an extension and requires the following m+m apps to be installed and
set up:

- m+m Cloud Base
- m+m Unit Conversion
- m+m Logistic Management (Advice Notification and Shipment Planning)

Without these base modules the extended quantity fields are not available.

### Brief process overview

1. An item is maintained in **Unit Conversion** with KG, Meter and Piece values.
2. The user captures a document (**purchase order**, **sales order** or
   **transfer order**).
3. From the document an **Advice Notification** (inbound) or a **Shipment
   Planning** (outbound) is created. The **KG**, **Meter** and **Piece** fields
   are transferred along; the additional fields are populated.
4. The user assigns the desired quantity in one of the three units; the app
   converts the other two units.
5. With **Register** the base module transfers the assigned quantities into the
   downstream documents.

---

## Quick start for users

The quick start describes the shortest paths. The prerequisite is always a
completed [Setup](#setup).

### Quick start A — Inbound via the Advice Notification

1. Open the **purchase order** via **Tell me** and enter a line with an item
   that is maintained in KG/Meter/Piece.
2. Create the **Advice Notification** via the **Create Advice Notification**
   action. The **KG**, **Meter** and **Piece** fields are transferred from the
   order.
3. On the **Advice Notification** line, enter the quantity in exactly **one**
   unit — for example **KG To Assign**. The app fills in **Meter To Assign** and
   **Piece To Assign** automatically.
4. Run the **Register** step of the Advice Notification. The assigned quantities
   are transferred into the warehouse receipt line or purchase line.

### Quick start B — Outbound via the Shipment Planning

1. Open the **sales order** via **Tell me** and enter a line with a
   KG/Meter/Piece item.
2. Open the **Shipment Planning** via **Tell me** and create a shipment planning
   line from the order. The **KG**, **Meter** and **Piece** fields appear.
3. On the **Shipment Planning** line, enter the quantity in exactly **one** unit
   — for example **Meter To Assign**. The app fills in **KG To Assign** and
   **Piece To Assign** automatically and updates **Gross Weight** and **Net
   Weight**, provided the item has a KG unit.
4. In the **Shipment Planning** list, choose the **Register** action. The
   assigned quantities are transferred into the warehouse shipment, sales or
   transfer line.

> Order of steps: first **Setup**, then the document (purchase/sales order),
> then **Advice Notification** or **Shipment Planning**, then **Register**.

---

## Setup

The app itself has **no setup page of its own**. To use it, it is sufficient to
meet the prerequisites of the base modules and to set two existing setup fields
correctly. The administrator performs this setup once per company, before the
operational users start working with the Advice Notification and Shipment
Planning.

### Set up unit conversion for Advice Notification and Shipment Planning

**Who and when:** the administrator sets this up once per company, before the
first Advice Notification or Shipment Planning with KG/Meter/Piece is created.
The settings then take effect in the daily work in
[Advice Notification](#daily-work--advice-notification) and
[Shipment Planning](#daily-work--shipment-planning).

**Numbered setup steps (in dependency order):**

1. **Install the base apps.** Make sure that m+m Cloud Base, m+m Unit Conversion
   and m+m Logistic Management are installed. If these apps are missing, then
   the additional KG/Meter/Piece fields are not shown on the logistic documents
   and no conversion takes place.
2. **Maintain the item master in Unit Conversion.** For each item, enter the
   theoretical values for KG per Meter and KG per Piece in the Unit Conversion.
   If these values are maintained, then the app can calculate the other two from
   an entered unit; without these values the derived quantities remain empty.
3. **Define the unit of measure code for KG.** Open the **KG Meter Piece Setup**
   via **Tell me** and enter the **Unit of Measure Code for KG**. If a unit of
   measure code for KG is set, then the Shipment Planning uses the assigned KG as
   **Gross Weight** and **Net Weight** of the shipment planning line; if it is
   empty, this weight determination is omitted.
4. **Define the default quantity for the Shipment Planning.** Open the
   **Shipment Planning Setup** via **Tell me** and set the **Qty. to Assign
   Default Value** (see the value table below). If a default value is set, then
   the Shipment Planning automatically proposes the corresponding KG, Meter and
   Piece quantity when a line is created.

**Operational conclusion:** in daily work, the user enters the assigned quantity
on the advice notification or shipment planning line and triggers **Register**;
see [Daily work — Shipment Planning](#daily-work--shipment-planning).

#### Setup fields

| Setup | Explanation |
|---|---|
| **Unit of Measure Code for KG** (KG Meter Piece Setup) | If a unit of measure code is entered here and the item has this KG unit or theoretical KG values, then the Shipment Planning uses the assigned KG as **Gross Weight** and **Net Weight** of the line; if the field is empty, weights are not derived from the KG. |
| **Qty. to Assign Default Value** (Shipment Planning Setup) | Defines which quantity is automatically proposed as KG/Meter/Piece to assign when a shipment planning line is created. See the value table. |

**Values of "Qty. to Assign Default Value":**

- **Finished Quantity:** when the shipment planning line is created, the quantity
  already finished on the assigned production order (less quantities already
  planned) is proposed as KG/Meter/Piece to assign. Suitable when only quantities
  actually produced are to be shipped.
- **Outstanding Quantity:** when the shipment planning line is created, the open
  quantity of the document (less quantities already planned) is proposed as
  KG/Meter/Piece to assign. Suitable when the entire remaining open document
  quantity is to be planned.

### Permissions

The app ships the permission set **MuM ASUC Permission**. This permission set
determines the permissions for running the three calculation codeunits of the
app. It defines that a user may run the automatic KG/Meter/Piece conversion in
Advice Notification, Shipment Planning and Item Tracking Assignment. Assign it to
the users who work with these documents.

---

## Daily work — Advice Notification

The **Advice Notification** is called via **Tell me** or via the **Advice
Notifications** or **Create Advice Notification** action from within a document.
When a KG/Meter/Piece item is carried over from a **purchase order** into an
Advice Notification, the app transfers the **KG**, **Meter** and **Piece** fields
and populates the additional fields. The assignment quantities maintained here
then control which quantities the **Register** step transfers into the warehouse
receipt or purchase line (see [Setup](#setup)).

### Fields in the Advice Notification subform and in the advice notification lines

The app adds the following columns to the advice notification lines and the
subform.

| Field | Explanation |
|---|---|
| **KG** | Shows the total KG of the line from the Unit Conversion. If the item has KG values, then this value serves as the basis for converting the assignment quantities. |
| **Piece** | Shows the total quantity of the line in Piece. |
| **Meter** | Shows the total quantity of the line in Meter. |
| **KG To Assign** | If you enter a value here, then the app calculates **Meter To Assign** and **Piece To Assign** as well as the assigned **Qty. to Assign** from it and updates the line immediately. |
| **Meter To Assign** | If you enter a value here, then the app calculates **KG To Assign** and **Piece To Assign** from it and updates the assigned quantity. |
| **Piece To Assign** | If you enter a value here, then the app calculates **KG To Assign** and **Meter To Assign** from it and updates the assigned quantity. |
| **Outstanding KG** | Shows the KG not yet advised. When assignments are entered, then the outstanding value decreases accordingly. |
| **Outstanding Piece** | Shows the Piece not yet advised. |
| **Outstanding Meter** | Shows the Meter not yet advised. |

> You do not have to calculate the three units consistently yourself: it is
> enough to enter **one** unit. A partial assignment is permitted — it is not
> required that all three units are fully balanced before you leave the line.

### Additional fields on the purchase order and in the advice notification purchase lines

On the **purchase order subform** and in the advice notification purchase lines,
these quantity columns are additionally available.

| Field | Explanation |
|---|---|
| **KG for Advice Notif.** / **Meter for Advice Notif.** / **Piece for Advice Notif.** | If you enter one of these measures (or the quantity for the Advice Notification) on the purchase line, then the app calculates the respective other two units and makes them available for creating the Advice Notification. |
| **KG Advice Notification** / **Meter Advice Notification** / **Piece Advice Notification** | Shows in summary which KG/Meter/Piece of this purchase line are already assigned in open Advice Notifications. When an Advice Notification is created or changed, then the value updates. |
| **KG Regist. Advice Notif.** / **Meter Regist. Advice Notif.** / **Piece Regist. Advice Notif.** | Shows in summary which KG/Meter/Piece of this purchase line are already posted in **registered** Advice Notifications. |

---

## Daily work — Shipment Planning

The **Shipment Planning** is called via **Tell me** or via the **Shipment
Planning** action from within a document. When a KG/Meter/Piece item is carried
over from a **sales order** or **transfer order** into the Shipment Planning, the
**KG**, **Meter** and **Piece** fields appear in the Shipment Planning as well.
Which quantity is proposed on creation is controlled by the **Qty. to Assign
Default Value** from the [Setup](#setup).

### Fields in the Shipment Planning subform and in the shipment planning lines

| Field | Explanation |
|---|---|
| **KG To Assign** | If you enter a value here, then the app calculates **Meter To Assign** and **Piece To Assign**, updates the **Qty. to Assign** and, when a unit of measure code for KG is set, derives **Gross Weight** and **Net Weight**. |
| **Meter To Assign** | If you enter a value here, then the app calculates **KG To Assign** and **Piece To Assign** and updates the assigned quantity. |
| **Piece To Assign** | If you enter a value here, then the app calculates **KG To Assign** and **Meter To Assign** and updates the assigned quantity. |

### Shipment planning assignment with inventory

In the shipment planning assignment with inventory, the app additionally shows
the source and planning quantities per unit. These columns provide an overview of
which quantities are open, finished and intended for the Shipment Planning.

| Field | Explanation |
|---|---|
| **KG** / **Meter** / **Piece** | Shows the total quantity of the document line in the respective unit. |
| **Outstanding KG** / **Outstanding Meter** / **Outstanding Piece** | Shows the open quantity per unit that has not yet been shipped. |
| **Finished KG** / **Finished Meter** / **Finished Piece** | Shows the quantity finished from assigned production orders per unit. When the "Finished Quantity" default value is set, then this value forms the basis for the assignment proposal. |
| **KG For Shipment Planning** / **Meter For Shipment Planning** / **Piece For Shipment Planning** | Shows the quantity proposed for the Shipment Planning per unit (default value less quantities already planned). If you accept this assignment, then the values are written as assignment quantities into the shipment planning line. |

### Transfer and downstream documents

Besides sales, the Shipment Planning also covers the **transfer**. When a
shipment planning line is created from a transfer line, the app proposes the open
KG/Meter/Piece as assignment quantities. After **Register**, the app transfers
the assigned units into the downstream documents:

- **Sales:** into the sales line or into the **warehouse shipment** line.
- **Transfer:** into the **transfer order** line or into the **warehouse
  shipment** line.
- **Inbound (Advice Notification):** into the purchase line or into the
  **warehouse receipt** line.

### Register

The Shipment Planning is concluded via the **Register** action in the **Shipment
Planning** list. This action belongs to the base module; the app ensures that the
assigned KG/Meter/Piece quantities are fully transferred into the downstream
documents. After registering, the quantities are available for tracking in the
**Registered Shipment Planning**.

---

## Item Tracking Assignment

When an item is maintained with **Lot No.** or **Serial No.**, the user assigns
the tracking in the **Item Tracking Assignment**. Here too, the app adds the
three units so that the assignment can be made not only in the base quantity but
also in KG, Meter and Piece.

| Field | Explanation |
|---|---|
| **KG To Assign** | If you enter a value here, then the app calculates **Meter To Assign** and **Piece To Assign** and updates the **Qty. to Assign** of the assignment line. |
| **Meter To Assign** | If you enter a value here, then the app calculates **KG To Assign** and **Piece To Assign**. |
| **Piece To Assign** | If you enter a value here, then the app calculates **KG To Assign** and **Meter To Assign**. |

When several lots or serial numbers are selected, the app sums the selected
quantities. In the selection overview, the following are additionally available:

| Field | Explanation |
|---|---|
| **Selected KG for Assignment** / **Selected Meter for Assignment** / **Selected Piece for Assignment** | If you enter one of these measures on the selection line, then the app converts the other two and forms the base quantity. |
| **Total KG for Assignment** / **Total Meter for Assignment** / **Total Piece for Assignment** | Shows the sum of the selected quantities per unit across all selected lots or serial numbers. |

The KG/Meter/Piece assigned in the Item Tracking Assignment are written back to
the associated advice notification or shipment planning line, so that the
quantities remain consistent across the entire process.

---

## History, archive and tracking

After **Register**, the quantities are traceable in the registered documents and
in the archive. There the app shows the same assignment columns as in the active
lists.

| Area | Explanation |
|---|---|
| **Registered Advice Notification** | Shows **KG To Assign**, **Meter To Assign** and **Piece To Assign** of the registered Advice Notification in the lines. Serves to track which quantities per unit were actually advised. |
| **Registered Shipment Planning** | Shows **KG To Assign**, **Meter To Assign** and **Piece To Assign** of the registered Shipment Planning in the lines and in the subform. |
| **Advice Notification — Archive** | Shows **KG**, **Meter**, **Piece** in the archived subform, as well as the assigned quantities of the archived advice notification version. |
| **Registered Item Tracking Assignment** | Shows **KG To Assign**, **Meter To Assign** and **Piece To Assign** of the registered assignment. |

---

## FAQ and troubleshooting

### 1. Why do no KG/Meter/Piece fields appear in the Advice Notification?

The fields are only populated when the item is maintained in **Unit Conversion**
with KG, Meter or Piece values and the base modules are installed. Check the
theoretical KG values of the item and the [Setup](#setup).

### 2. Do I have to enter all three units myself?

No. It is sufficient to enter **one** unit (KG, Meter or Piece) to assign. The
app calculates the other two units and the quantity to assign automatically.

### 3. What happens when I change "KG To Assign"?

The app recalculates the corresponding **Meter To Assign** and **Piece To
Assign** from the new KG value, updates the **Qty. to Assign** and refreshes the
line display immediately.

### 4. Why does the calculated quantity deviate slightly?

The conversion is based on the KG per Meter or KG per Piece of the item. If an
**actual** KG value (e.g. per lot) is available, the app uses it; otherwise the
**theoretical** value. Different reference values lead to different results.

### 5. How is the weight of the Shipment Planning determined?

If a **Unit of Measure Code for KG** is entered in the **KG Meter Piece Setup**
and the item has KG values, the app sets **Gross Weight** and **Net Weight** of
the shipment planning line equal to the assigned KG. Without a unit of measure
code for KG, this derivation is omitted.

### 6. Which quantity does the Shipment Planning propose on creation?

This is controlled by the **Qty. to Assign Default Value** in the **Shipment
Planning Setup**: **Finished Quantity** proposes the finished quantity,
**Outstanding Quantity** the open document quantity — in each case less
quantities already planned.

### 7. Why is the proposed quantity smaller than expected?

From the finished or open quantity, the app subtracts the quantities already
planned in other, not-yet-completed shipment planning lines, so that no quantity
is planned twice.

### 8. Can I assign partial quantities?

Yes. You can assign partial quantities in the Advice Notification and the
Shipment Planning; it is not required that all units are fully balanced before
you leave the line or run **Register**.

### 9. How do I assign quantities to a lot or serial number?

Use the **Item Tracking Assignment**. There you enter the KG/Meter/Piece to
assign per **Lot No.** or **Serial No.**; the app sums the selection and writes
the quantities back to the advice notification or shipment planning line.

### 10. Where can I see which quantities have already been registered?

On the purchase or sales line, the **KG/Meter/Piece Advice Notification** fields
show the openly assigned quantities and the **KG/Meter/Piece Regist. Advice
Notif.** fields show the already registered quantities. The registered documents
themselves carry the same assignment columns (see
[History](#history-archive-and-tracking)).

---

## Typical use cases

### Use case 1 — Warehouse receipt of a coil (Advice Notification)

**Trigger:** a vendor announces the delivery of coils by phone, which are
maintained in **KG**, **Meter** and **Piece**.

**Entry point in BC:** the user opens the **purchase order** via **Tell me** and
creates the **Advice Notification** via **Create Advice Notification**.

**Core flow:** on the **Advice Notification** line, the user enters the advised
quantity in **KG To Assign**. The app calculates **Meter To Assign** and **Piece
To Assign** and updates the line. The user then triggers the **Register** step.

**Conclusion:** the assigned quantities are transferred into the warehouse
receipt or purchase line; the registered Advice Notification shows the posted
KG/Meter/Piece.

### Use case 2 — Customer call-off (Shipment Planning)

**Trigger:** a customer calls off a partial quantity for a delivery date.

**Entry point in BC:** the user opens the **sales order** via **Tell me** and
then the **Shipment Planning** via **Tell me**.

**Core flow:**

1. The user creates a **Shipment Planning** line from the order; depending on the
   **Qty. to Assign Default Value**, a quantity is proposed.
2. If necessary, the user overwrites **Meter To Assign**; the app calculates **KG
   To Assign** and **Piece To Assign** and updates **Gross Weight**/**Net
   Weight**.
3. In the **Shipment Planning** list, the user chooses the **Register** action.

**Conclusion:** the quantities are transferred into the sales or **warehouse
shipment** line; the **Registered Shipment Planning** documents the process.

### Use case 3 — Transfer between locations

**Trigger:** for an internal inventory balancing, material is to be transferred
between two locations.

**Entry point in BC:** the user opens the **transfer order** via **Tell me** and
then the **Shipment Planning** via **Tell me**.

**Core flow:** when the shipment planning line is created from the transfer line,
the app proposes the open **KG/Meter/Piece To Assign**. The user adjusts one
unit; the app converts the others. Then the user chooses **Register**.

**Conclusion:** the assigned quantities are transferred into the **transfer
order** or **warehouse shipment** line and are available for tracking in the
**Registered Shipment Planning**.
