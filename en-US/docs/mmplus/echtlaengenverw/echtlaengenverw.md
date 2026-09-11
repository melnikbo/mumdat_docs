---
title: Anwenderhandbuch m+m Original Length Management
---

# User Guide m+m Original Length Management

## Introduction

The **m+m Original Length Management** extension enhances the item tracking of Microsoft
Dynamics 365 Business Central with the actual **Length** and the **Original Length** per
lot as well as a **weight distribution based on length**. The module is aimed at steel-processing
operations in which lot-tracked items (bars, tubes, profiles, coils) are recorded in meters and
weighed via a KG-per-meter conversion.

**Target audience:** Primarily the **operational users** in goods receipt, warehouse and production who
work with **item tracking** on a daily basis – that is, creating lots, capturing actual lengths and
determining the weight per lot. Secondarily, **administrators and master data managers** are addressed
who set up the length property per **Material Type** and the KG/meter conversion once.

**Brief process overview:**

1. The administrator defines a record property with the **Usage** *Length* (and optionally
   *Original Length*) for each **Material Type** and sets up the units for KG and meter in the
   **KG Meter Piece Setup**.
2. When creating the lot (goods receipt), the user captures the actual **Length** in the
   **Item Tracking Lines** or in **Create Item Tracking**.
3. Via the **Weight Distribution Based On Length** action, the total weight is distributed across the
   individual lots based on the lengths, and the **Quantity (Base)** is set per lot.
4. In the **Lot No. Information** and in the **Prod. Order Job Overview**, **Length** and
   **Original Length** are subsequently available for viewing and further processing.

## Quick Start for Users

The following sequence follows the technical dependency: first setup, then capture, then
weight distribution.

1. **Check setup (once, administrator).** Make sure that the **KG Unit of Measure Code** and the
   **Meter Unit of Measure Code** are set in the **KG Meter Piece Setup**, and that the affected
   **Material Type** has a record property with **Usage** = **Length**. Without this property, the
   length logic remains inactive.
2. **Create lot with length.** For the document line, open the **Item Tracking Lines** and enter the
   actual **Length** per lot – or create the lots via **Create Item Tracking** and capture the
   **Length** there.
3. **Distribute weight.** In the **Item Tracking Lines**, choose the action
   **Weight Distribution Based On Length**.
4. **Confirm values.** Confirm the dialog *"Should the Weight Distribution of the Lot No.'s be executed
   with the following Values?"* (with **Total Length**, **Total Weight** and
   **Actual KG per Meter**) with **Yes**. The module calculates the KG weight per lot and sets the
   **Quantity (Base)**.
5. **Check result.** Verify the distributed quantities in the item tracking lines as well as
   **Length** and **Original Length** in the **Lot No. Information**.

## Setup

The setup of this module consists of master data and global settings that reside in the base modules
**m+m Material Properties** and **m+m Unit Conversion** and are evaluated by Original Length Management.
Without this setup, the length fields are visible but are not filled automatically, and weight
distribution is disabled.

### Setting up length properties per Material Type

**Process intro.** This setup is performed once by the **administrator** or a **master data manager**
before the affected items are posted productively with lot tracking. It defines for which
**Material Type** a length is maintained. Only once a Material Type has a property with the **Usage**
*Length* does the module activate the **Weight Distribution Based On Length** action in the item
tracking lines and fill the length fields automatically. The values maintained here take effect later
in daily work (section **Daily work in item tracking**).

**Entry point:** Open the **Material Type** in the master data of the material properties and call the
property editor (**Record Property**) of the Material Type there. Create one line per Material Type
with the desired **Usage**.

Explanation of the fields of the **Record Property** that this module evaluates:

| Field | Explanation |
|---|---|
| Usage | Defines what the property is used for. If you select **Length**, then the module treats the numeric value as the actual length of the lot; upon posting it is automatically transferred to the lot information and to the item tracking lines and is the basis for weight distribution. If you select **Original Length**, then the original length of the lot is additionally maintained (see separate paragraph below). |
| Lot Property | If enabled, then the property applies per lot (Lot No. level) and can take different values per lot; the module enforces this activation for the usages **Length** and **Original Length** – without the Lot Property set, an error is issued when saving. |
| Data Type | Determines the allowed value format. For **Length** and **Original Length**, the module allows only **Decimal** or **Integer**; other data types are rejected with the message *"When you use the usage … then the data type can only be decimal or integer."* |
| Numeric Value | Contains the evaluated numeric value of the length. If a value is present here, then the module reads it when assembling the item tracking and writes it into the **Length** field of the line. |
| Value | Holds the captured property value as text. When the module writes back a length upon posting, then it updates this value (via validation) so that **Numeric Value** remains consistent. |

**Data Type – allowed values for length properties:**

- **Decimal:** Length with decimal places (e.g. 6.250 m). Recommended for meter-precise capture.
- **Integer:** Length without decimal places. Permitted if whole meters are sufficient.
- All other data types are blocked for the usages **Length**/**Original Length** and trigger the
  error message mentioned above.

**Usage – the values added by this module:**

- **Length:** The lot maintains an actual length. If set, then the value is transferred into the
  **Length** field when generating the item tracking, when creating the lot information, and when
  posting, and serves as the basis for weight distribution.
- **Original Length:** The lot additionally maintains the original length. If set, then the module
  writes the length value as the original length when the lot information is first created – but only
  as long as **no item ledger entry** yet exists for the lot. This keeps the initial length of a lot
  unchanged after the first inventory posting.

> Note: The usage **Length**/**Original Length** may be assigned **only once** per Material Type. If
> you create a second property with the same usage, the system aborts with
> *"There is already one usage with the value … assigned."*

**Process steps (dependency order):**

1. First, create the **Material Type** or select the existing Material Type.
2. Then, in the **Record Property** of this Material Type, capture a line with
   **Usage** = **Length**, **Lot Property** enabled and **Data Type** = **Decimal**
   (or **Integer**).
3. Optionally, add a second line with **Usage** = **Original Length** (same
   Lot Property/Data Type rules).
4. Finally, assign this **Material Type** to the affected **items** (field
   **Material Type Code** on the item or on the item variant) – only then does the logic take effect in
   day-to-day operations.

**Validation / dependencies:** When saving the property, the module checks that
**Lot Property** is set, that the **Data Type** is decimal or integer, and that only
one property of the respective **Usage** exists per Material Type. If no Material Type with a
length property is assigned to the item, the **Weight Distribution Based On Length** action remains
disabled.

### Setting up the KG/meter conversion

**Process intro.** This global setup is performed once per company by the **administrator**. It
determines which base units apply for **KG** and **meters** and how the weight calculated from the
length is rounded. Weight distribution in the item tracking lines mandatorily accesses this setup.

**Entry point:** Open the **KG Meter Piece Setup** via **Search**. It is a
company-wide setup with exactly one record; there is no higher-level call via a list.

| Setup | Explanation |
|---|---|
| KG Unit of Measure Code | Defines the item unit of measure that is interpreted as weight in KG. If the **Base Unit of Measure** of the item matches this code, then weight distribution adopts the calculated KG weight directly as **Quantity (Base)**. If the code is empty, weight distribution aborts with a field check message. |
| Meter Unit of Measure Code | Defines the item unit of measure that is interpreted as length in meters. If the **Base Unit of Measure** of the item matches this code, then weight distribution sets the length as the quantity to be moved in meters as **Quantity (Base)**. If the code is empty, weight distribution aborts with a field check message. |
| KG Rounding Direction (on the item) | Determines how the KG weight calculated per lot is rounded. See the value list below. |
| KG Rounding Precision (on the item) | Defines the rounding increment for the KG weight (e.g. 0.001 or 1). If set, then the module rounds the calculated weight to this precision according to the rounding direction. |

**KG Rounding Direction – allowed values:**

- **Round Up:** The calculated KG weight is always rounded up to the next higher rounding step.
  Choose this if weights must never be underestimated.
- **Round Down:** The weight is always rounded down to the next lower step. Choose this if
  conservative downward rounding is desired.
- **Commercially Rounded:** The weight is rounded commercially (0.5 and up). Default choice for
  balanced rounding.

**Process steps:**

1. First, set the **KG Unit of Measure Code** and the **Meter Unit of Measure Code** in the
   **KG Meter Piece Setup**.
2. Then, define the **KG Rounding Direction** and the **KG Rounding Precision** on the **item**.
3. Finally, the **Weight Distribution Based On Length** action becomes available in day-to-day
   operations (see **Daily work in item tracking**).

### Permissions

The extension ships the permission set **m+m Original Length Management** (object name
*MuM OL Permission*). It comprises the execution permission for the length logic (codeunit
*MuM OL Length Management*) and thereby determines the permissions for automatic length and
weight determination. Assign this permission set to all users who work length-based with item
tracking.

## Master Data

### Lot No. Information: Length and Original Length

**Process intro.** The **Lot No. Information** is the place where the user views the length-related
values of a lot. The two fields are not captured manually but are read as
calculated fields (FlowFields) from the record property of the lot. The master data is maintained in
the course of lot creation and postings (see **Daily work**); here the user checks the result.

**Entry point:** Open the overview of the **Lot No. Information** (lot list). The two
columns appear in addition to the standard fields of the lot.

| Field | Explanation |
|---|---|
| Length | Shows the current actual length of the lot. If a record property with **Usage** = **Length** exists for the lot, then the field shows its **Numeric Value**; if the length changes (e.g. through consumption in production), the displayed value updates accordingly. |
| Original Length | Shows the original length of the lot at the time of the first inventory posting. If a property with **Usage** = **Original Length** exists, then the field shows its **Numeric Value**; after the first inventory posting this value remains unchanged and serves as a reference for the initial length. |

Both fields are **not editable** – they reflect the underlying lot property.
Therefore, maintain length values via capture in item tracking, not in the lot list.

## Daily work in item tracking

Daily work takes place in item tracking. Which fields and actions are active is
controlled by the setup: the actual **Length** is only filled automatically and the
action **Weight Distribution Based On Length** is only offered when the associated **Material Type** has
a length property (section **Setting up length properties per Material Type**) and the
**KG Meter Piece Setup** is complete (section **Setting up the KG/meter conversion**).

### Item Tracking Lines: capturing length

**Entry point:** Via the **Item Tracking Lines** action for a document or journal line, open the page
**Item Tracking Lines**.

| Field | Explanation |
|---|---|
| Length | Captures or shows the actual length per lot. If the actual length of the lot is to be controlling (Material Type with length property present), then the module automatically enters the length known from the lot property and you can adjust it; the value is the basis for the subsequent weight distribution. |

**Column caption "Remaining Length":** If the supply/delivery view of item tracking is
not visible, the module captions the same column as **Remaining Length**. This lets the
user recognize in the consumption view which remaining length of the lot is still available, instead of
the length originally supplied.

### Action: Weight Distribution Based On Length

**Entry point:** Open the calculation via the **Weight Distribution Based On Length** action (in the
**Item Tracking Lines**, promoted on the ribbon). The action is only active when
the item is assigned to a **Material Type** with a length property.

Flow of the action:

1. In the **Item Tracking Lines**, select the relevant lot lines.
2. Choose **Weight Distribution Based On Length**.
3. Confirm the dialog *"Should the Weight Distribution of the Lot No.'s be executed with the following
   Values?"*. The dialog shows **Total Length**, **Total Weight** and the resulting
   **Actual KG per Meter**. With **Yes** the distribution is performed, with **No** it is cancelled.
4. The module calculates the weight per lot from **Length × Actual KG per Meter**, rounds according to
   the item's **KG Rounding Direction**/**KG Rounding Precision** and sets the **Quantity (Base)**
   depending on the item's base unit of measure: if it matches the **KG Unit of Measure Code**, the KG
   weight is adopted; if it matches the **Meter Unit of Measure Code**, the meter value is adopted.
5. Additionally, the module writes the determined **Actual KG per Meter** back into the lot information
   and updates the totals of the item tracking lines.

**Field reference in the confirmation dialog:**

- **Total Length:** Sum of the lengths of all selected lot lines. If 0, the module internally
  calculates with the factor 1 to avoid a division by zero.
- **Total Weight:** Sum of the KG values of the selected lines.
- **Actual KG per Meter:** Total weight divided by total length – the conversion factor with
  which each lot is subsequently valued.

### Creating lots with length

**Entry point:** When creating multiple lots, open the page **Create Item Tracking**.

| Field | Explanation |
|---|---|
| Length | Captures the actual length per newly generated lot. If you enter a length here, then this value is transferred into the generated lot line when creating the item tracking and is subsequently available for weight distribution as well as in the lot information. |

Create the lots as usual; the captured **Length** is passed on to the resulting
item tracking lines.

### Lengths in the Prod. Order Job Overview

**Process intro.** In the **Prod. Order Job Overview** (production order job overview of the steel
module), the extension adds the **Length** field in each of the lot- and material-related views. This
way, the production user sees directly on the order which length is maintained per assigned lot or per
base material. The values are drawn automatically from the lot property when assigning/capturing the
lot and are re-determined when the Lot No. changes.

**Entry point:** Open the **Prod. Order Job Overview** and work in the sub-views for lots,
material and remaining lots.

| View | Field | Explanation |
|---|---|---|
| Lots (assigned lots) | Length | Shows/captures the length of the lot assigned to the operation. If you choose the **Lot No.** or create a line, then the module determines the length from the record property of the lot and writes a changed value back into the lot property upon confirmation. |
| Material (base material) | Length | Shows the remaining length of the assigned base material. If the material line is changed, then the module updates the length value of the associated lot (writing back into the lot property). The column title in this view is **Remaining Length**. |
| Remaining Lots | Length | Shows/captures the length of a remaining lot (remaining length left after production consumption). If you choose the **Lot No.** here or create the line, then the module adopts the length from the property and writes back changes so that the remaining length of the lot is maintained correctly. |

## Typical use cases

### Use case 1 – Goods receipt: capturing actual lengths and distributing weight

1. **Trigger:** A delivery of steel bars arrives at goods receipt. The actual meter lengths
   of the individual coils deviate from the nominal length and must be captured exactly.
2. **Entry point in BC:** The warehouse worker opens the purchase/goods receipt line and calls the
   **Item Tracking Lines**. Prerequisite: The **Material Type** of the item has the
   length property (see **Setting up length properties per Material Type**).
3. **Core flow:** Per lot, he enters the measured **Length**. Then he chooses
   **Weight Distribution Based On Length**, confirms the dialog with **Total Length**, **Total Weight**
   and **Actual KG per Meter** with **Yes**. The module distributes the weight, sets the
   **Quantity (Base)** per lot and writes the **Actual KG per Meter** into the lot information.
4. **Conclusion:** After posting the line, **Length** and **Original Length** are available in the
   **Lot No. Information**; the original length remains unchanged from the first inventory posting
   onward.

### Use case 2 – Creating multiple lots with length

1. **Trigger:** For one goods receipt line, several lots each with their own length are to be created.
2. **Entry point in BC:** From item tracking, the user opens the page
   **Create Item Tracking**.
3. **Core flow:** He creates the desired number of lots and captures the **Length** per lot. The
   values are passed to the resulting **Item Tracking Lines**.
4. **Conclusion:** In the item tracking lines he can then directly perform the
   **Weight Distribution Based On Length** (see use case 1, step 3).

### Use case 3 – Documenting remaining length in production

1. **Trigger:** In production, only part of a lot is consumed; the remaining length
   is to be documented on the production order.
2. **Entry point in BC:** The production user opens the **Prod. Order Job Overview** and switches to the
   view **Lots** or **Remaining Lots**.
3. **Core flow:** He chooses the **Lot No.** and checks/captures the **Length** of the remaining lot.
   The module draws the value from the lot property and writes a change back upon confirmation.
   In the **Material** view, the **Remaining Length** column shows the still available length of the
   base material.
4. **Conclusion:** The updated length is then visible in the **Lot No. Information**;
   the **Original Length** is retained as the initial value.

## FAQ and Troubleshooting

### 1. Why is the "Weight Distribution Based On Length" action greyed out?

The action is only active when the item is assigned to a **Material Type** that has a
record property with **Usage** = **Length**. If the length property of the
Material Type is missing or no **Material Type Code** is assigned to the item, the action remains disabled.

### 2. What happens when I confirm "Weight Distribution Based On Length"?

The module sums the lengths and weights of the selected lots, determines the **Actual KG
per Meter** and calculates the weight per lot from **Length × factor**. It then rounds according to the
**KG Rounding Direction** and sets the **Quantity (Base)** according to the base unit of measure (KG or meter).

### 3. Why does weight distribution abort with a field check message?

The calculation requires that both the **KG Unit of Measure Code** and the **Meter Unit of Measure
Code** are filled in the **KG Meter Piece Setup**. If one of the two codes is missing, the
module tests the field and aborts with a field check message.

### 4. Why can I not create a second length property for a Material Type?

Per Material Type, the **Usage** **Length** (or **Original Length**) is only allowed once. A
second entry of the same usage is rejected with *"There is already one usage with the value …
assigned."*, so that the length value remains unique.

### 5. Why do I get the message that the data type may only be decimal or integer?

For the usages **Length** and **Original Length**, the module requires a numeric **Data Type**.
If the data type of the property is neither **Decimal** nor **Integer**, saving is prevented with the
message *"When you use the usage … then the data type can only be decimal or integer."*.

### 6. Why must the property be marked as a Lot Property?

Length and original length are maintained per lot. The module therefore checks upon saving that the
**Lot Property** is enabled; if it is not, the field check fails. Only this way can each
Lot No. receive its own length value.

### 7. Why does the "Original Length" no longer change after the first posting?

The **Original Length** is set when the lot information is first created and is only
written back as long as **no item ledger entry** yet exists for the lot. After the first
inventory posting it remains unchangeable as the initial value, while the **Length** reflects the current
(remaining) length.

### 8. Why is the same column called "Length" in one place and "Remaining Length" in another?

In the supply/delivery view of item tracking, the column shows the supplied **Length**. If this
view is not visible (consumption view), the module captions the same column as **Remaining
Length**, so that the user recognizes the remaining length of the lot that is still available.

### 9. Where does the "Length" value in the item tracking lines come from if I do not enter anything?

If a record property with **Usage** = **Length** exists for the lot, the module reads its
**Numeric Value** when assembling the item tracking and enters it automatically into the field
**Length**. You can then adjust the pre-filled value.

### 10. Why is my length changed in the Prod. Order Job Overview transferred to the lot?

If you change the **Length** or the associated **Lot No.** in the **Prod. Order Job Overview** in the
views **Lots**, **Material** or **Remaining Lots**, the module writes the new value back into the
record property (**Length**) of the lot. This keeps the production view and
lot information consistent.
