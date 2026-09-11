---
title: Anwenderhandbuch m+m Production Differences with Unit Conversion
---

# User Guide m+m Production Differences with Unit Conversion

## Introduction

The app **m+m Production Differences with Unit Conversion** connects two existing m+m apps with each other: **m+m Production Differences** (over- and underproduction) and **m+m Unit Conversion** (unit conversion KG/Meter/Piece). It is a pure connector app and does not itself provide any page, menu item, or setup page of its own. Its effect arises exclusively in the background: it ensures that, when an output is posted with a deviating quantity (over- or underproduction), the values **KG**, **Meter**, and **Piece** are recalculated correctly and kept consistent across all documents involved.

**Prerequisite** is that the apps **m+m Production Differences** and **m+m Unit Conversion** are installed and set up. Without these two apps the connector app has no function.

**Target audience:** This guide is aimed primarily at **operational users in production** who post feedback on released production orders through the **Production Journal** (actual output), maintain lots in the **Item Tracking Lines**, and work with quantities in **KG/Meter/Piece**. Secondarily, it addresses **administrators** who configure the prerequisites in the two parent apps and assign the permission set.

**Brief process overview:** A released production order is posted through the Production Journal with an actual quantity that is allowed to deviate from the planned quantity. In the Item Tracking Lines, the produced **lot** is recorded with its values in **KG/Meter/Piece**. When posting, the produced and remaining unit values are written back to the production order line. If the **Update Source Document** flag is set on the production order, the connector app additionally updates the associated **Sales Order** and — where delivery is via the warehouse — the **Warehouse Shipment**, in each case including the unit values KG/Meter/Piece.

## Quick Start for Users

The quick start follows the sequence enforced by the code: first the setup in the parent apps, then the daily feedback posting.

1. **Ensure prerequisites (one-time, administration):** In the app **m+m Unit Conversion**, the theoretical conversion factors (theoretical KG per Meter and per Piece) as well as the quantity consistency check are maintained on the **Item Card** of the item. In the app **m+m Production Differences**, over-/underproduction is set up. On the **Released Production Order**, the **Update Source Document** flag is set where required. For details, see *Prerequisites and Setup*.
2. **Open the Released Production Order** and select the relevant line.
3. Use the standard action to open the **Production Journal**.
4. Record the actual quantity as **actual output**; this may deviate from the planned quantity in accordance with the over-/underproduction rules.
5. Open the **Item Tracking Lines**, assign the **lot**, and check or record the values **KG**, **Meter**, and **Piece** for this lot. The controlling **unit field** (Quantity, KG, Meter, or Piece) determines which value is leading.
6. In case of underproduction, when the order is to be completed with the lower quantity: set the **Finished** flag in the Production Journal (confirm the warning if applicable).
7. **Post** the Production Journal. Afterwards, the **Finished KG/Meter/Piece** and the **Remaining KG/Meter/Piece** are available on the production order line, correctly converted.
8. If **Update Source Document** is active, the **Sales Order** (Quantity, **Reserved Quantity**, KG/Meter/Piece) and — if present — the **Warehouse Shipment** are updated automatically; for this the app sets the **Update Linked Document** flag in the background.

## Prerequisites and Setup

This app has no setup page of its own. The entire functional configuration resides in the two parent apps; the connector app itself only needs to be installed and released via its permission set. This chapter therefore describes the **chain of prerequisites** that an administrator establishes in dependency order so that automatic unit conversion takes effect for production differences.

### Setting up unit conversion for production differences

**Process intro:** This configuration concerns the administration or the key user and is carried out **before the first feedback posting** of an affected item. It is the foundation for ensuring that the daily work in the Production Journal (see *Daily Work in the Production Journal*) delivers correct KG/Meter/Piece values and that the sales order is updated automatically along with it. The individual steps reside in the parent apps; the connector app does not add any configurable switch of its own.

**Numbered setup steps (in dependency order):**

1. **Master data first – Item Card (m+m Unit Conversion):** First, on the **Item Card**, you maintain the theoretical conversion factors (theoretical KG per Meter and per Piece) and the quantity consistency check. If these factors are maintained, then unit conversion automatically calculates the related values in KG, Meter, and Piece when a lot is created; if the factors are missing, only the base quantity without conversion remains available for the item. This page is opened via **Tell Me** using the term for the Item Card.
2. **Global setup – KG Meter Piece Setup (m+m Unit Conversion):** Next, on the **KG Meter Piece Setup** page, you check the company-wide settings (unit codes for KG, Meter, and Piece, rounding rules). If the unit codes are assigned correctly here, then the unit fields in documents and in item tracking are maintained with the correct units of measure. You open this page via **Tell Me** using the term "KG Meter Piece Setup".
3. **Global and item-specific setup – over-/underproduction (m+m Production Differences):** After that, in the over-/underproduction setup, you define the range within which the actual quantity may deviate from the planned quantity (control method Default, Percentage, or absolute value, with a value and optional warning). If a warning is permitted, then the user can exceed the limit by confirming it; if only an error is permitted, then the deviating quantity is blocked. These rules determine which over- or underproduction can be posted in the Production Journal at all.
4. **Document-specific flag – Update Source Document on the production order (m+m Production Differences):** Set the **Update Source Document** flag on the **Released Production Order** if the source document is to be updated along with it. If this flag is enabled, then after the feedback posting the system updates the associated **Sales Order** (Quantity and **Reserved Quantity**) and — through the connector app — also its unit values KG/Meter/Piece; if it is not set, the sales order remains unchanged and only the production order is updated.
5. **Permission – this app (m+m Production Differences with Unit Conversion):** Assign the supplied permission set **MuM OPUC Gen. Perm** to the relevant user groups. This permission set defines which actions users may perform with the app's two processing codeunits; without this permission the automatic conversion cannot be executed during posting.

**Operational conclusion:** Once steps 1 through 5 are in place, the connector app takes effect fully automatically when the Production Journal is posted. The user triggers the chain through the normal feedback posting; see *Daily Work in the Production Journal*.

### Controlling unit field

The behavior of the conversion is controlled by the **unit field** (technical name of the field: **Unit Field Modified**). This field originates from the m+m Unit Conversion app and is evaluated by the connector app to decide which value is compared as leading in case of a deviation.

| Field | Explanation |
|---|---|
| **Unit field** | Determines which quantity value is leading during the check and back-calculation. The permitted values and their effect: **Quantity:** The standard quantity is used for the calculation; the additional fields KG/Meter/Piece do not act as leading. **KG:** If selected, the produced or to-be-completed quantity is checked and back-calculated against the lot via the **Finished KG**. **Meter:** If selected, the **Finished Meter** is the leading value for the check and back-calculation. **Piece:** If selected, the **Finished Piece** is leading. |

### Interaction of the flags

For the user these flags are normally not visibly editable; they are set by the system and document how the conversion took place. Knowing them helps in understanding the process and in troubleshooting.

| Field | Explanation |
|---|---|
| **Update Source Document** | Flag on the Released Production Order (app m+m Production Differences). If set, then after posting the Production Journal the linked sales order is updated including **Reserved Quantity** and unit values; if not set, the sales order remains unchanged. |
| **Update Linked Document** | Technical flag that this app sets on the **Sales Line** and on the **Warehouse Shipment** line. If set, then unit conversion uses for this line the actual factors taken over from production (**Actual KG per Meter** and **Actual KG per Piece**) instead of the theoretical factors of the Item Card; as a result, the unit values in the subsequent document match exactly the actually produced lot. If it is not set, the line continues to calculate with the theoretical factors. This field is set exclusively by the system. |
| **Do not reconvert** | Flag from the m+m Unit Conversion app. If set, then the system takes over the KG/Meter/Piece determined from production unchanged and does not recalculate them once more via the theoretical factors; as a result, the actually produced quantity is retained. If not set, an automatic reconversion can take place. |
| **Unit Field Modified** | Tracks which unit value (Quantity, KG, Meter, or Piece) was leading during the last processing. If set, then this value controls which of the fields Finished KG/Meter/Piece is used for the check and back-calculation. |

## Daily Work in the Production Journal

The daily work takes place entirely on the standard and m+m pages of production; this app acts in the background. The controlling settings reside in the pages described under *Prerequisites and Setup* (Item Card, KG Meter Piece Setup, over-/underproduction setup, **Update Source Document** flag). The following process describes how the user posts feedback for a lot.

### Feedback posting with a deviating quantity

**Entry point:** Open the **Released Production Order**, select the production order line, and use the standard action to open the **Production Journal**.

1. Record the actually produced quantity as **actual output**. Over- or underproduction is permitted within the scope of the configured rules.
2. Open the **Item Tracking Lines** and assign the **lot**. For the lot the values **KG**, **Meter**, and **Piece** are maintained; if theoretical factors are maintained, unit conversion calculates these values automatically from the quantity.
3. If needed, change one of the values KG, Meter, or Piece. If you change a value manually, then the quantity consistency check stored on the Item Card decides whether the remaining values are recalculated automatically. In doing so, the connector app checks that the assigned unit values match the reported quantity.
4. Leave the Item Tracking Lines. The app reconciles the produced unit values against the quantity to be processed.

### Full and partial feedback

If the produced quantity is below the planned quantity and the order is to be completed with this lower quantity, set the **Finished** flag in the Production Journal. If the quantity is below the configured minimum quantity for underproduction, then — provided the rule permits a warning — a warning appears that you must confirm; if you decline, the **Finished** flag cannot be set and the posting remains a partial feedback. A partial feedback is explicitly permitted; it is not required that the produced quantity equals the planned quantity.

### Posting and write-back

**Post** the Production Journal afterwards. After posting, the connector app writes the values back to the production order line:

- **Finished KG / Finished Meter / Finished Piece** are increased by the unit values just posted.
- **Remaining KG / Remaining Meter / Remaining Piece** are updated as the difference between the order quantity and the finished quantity in the respective unit.
- The **Do not reconvert** flag is set so that the actually produced values are not overwritten via the theoretical factors.
- The **Unit Field Modified** is updated with the value that was last leading (Quantity, KG, Meter, or Piece).

In this way it remains traceable at all times how much has already been finished in KG, Meter, and Piece, and how much is still open per unit.

## Linked Documents: Sales Order and Warehouse Shipment

The connector app extends two document tables by one technical flag each so that the unit values from production are taken over into the subsequent documents. These fields are not intended for manual editing; they are set exclusively by the system.

### Sales Order

If **Update Source Document** is active on the production order, the app updates the linked sales order after posting. On the **Sales Line**, the unit values from production are taken over and the **Update Linked Document** flag is set.

| Field | Explanation |
|---|---|
| **Update Linked Document** (Sales Line) | If set, then unit conversion calculates this sales line with the actual factors originating from the produced lot (**Actual KG per Meter** / **Actual KG per Piece**) and not with the theoretical factors of the Item Card; as a result, the values **KG/Meter/Piece** and **Outstanding Order KG/Meter/Piece** on the sales line correspond exactly to the actually produced quantity. If it is not set, the line calculates with the theoretical factors. Set automatically. |

In addition, the unit values derived from production are updated on the sales line (in each case in KG, Meter, and Piece): the current quantities as well as the open quantities (**Outstanding Order KG/Meter/Piece**). The **Quantity** and **Reserved Quantity** of the sales order are also updated in accordance with the posted production quantity.

### Warehouse Shipment

If the sales order is delivered via a **Warehouse Shipment**, the app transfers the flag when the warehouse shipment line is created.

| Field | Explanation |
|---|---|
| **Update Linked Document** (Warehouse Shipment line) | If set, then unit conversion uses for this warehouse shipment line the actual factors of the produced lot (**Actual KG per Meter** / **Actual KG per Piece**); as a result, the warehouse shipment shows exactly the actually produced KG/Meter/Piece and not values generated computationally from the theoretical conversion. If it is not set, the line calculates with the theoretical factors. The flag is taken over automatically from the associated sales line when the warehouse shipment line is created. |

## FAQ and Troubleshooting

### 1. Why do I need this app in addition to m+m Production Differences and m+m Unit Conversion?
Both apps work each on their own. However, as soon as you post an over- or underproduction for an item with unit conversion (KG/Meter/Piece), the unit values must be adjusted to the deviating quantity and taken over into the subsequent documents. It is precisely this coupling that the connector app provides; without it, the unit values would remain inconsistent in case of a deviating quantity.

### 2. Where do I find the setup page of this app?
There is none. The app does not come with a page of its own. The configuration takes place on the **Item Card** and the **KG Meter Piece Setup** (m+m Unit Conversion) as well as in the over-/underproduction setup and via **Update Source Document** on the production order (m+m Production Differences). See *Prerequisites and Setup*.

### 3. What happens if I produce more than planned (overproduction)?
Within the configured rules, the higher quantity is permitted; when the limit is exceeded, a warning or an error appears depending on the rule. After posting, the **Finished KG/Meter/Piece** are increased accordingly. If **Update Source Document** is active, the Quantity and **Reserved Quantity** of the sales order are raised beyond the original quantity.

### 4. What happens in case of underproduction when I want to complete the order?
Set the **Finished** flag in the Production Journal. If the quantity is below the minimum quantity for underproduction, this is only permitted if the rule allows a warning; after confirmation you can post with the lower quantity. If you decline, the posting remains a partial feedback.

### 5. Which value is leading during the check — Quantity, KG, Meter, or Piece?
This is controlled by the **unit field** (**Quantity**, **KG**, **Meter**, **Piece**). The selected value determines which of the fields **Finished KG/Meter/Piece** is used for comparison with the lot.

### 6. Why do KG/Meter/Piece in the sales order not match the theoretical conversion after production?
Because, when **Update Linked Document** is active, the line calculates with the **actual** factors of the produced lot (**Actual KG per Meter** / **Actual KG per Piece**) and not with the theoretical factors of the Item Card. This is intended: the sales order is meant to reflect the actually produced values.

### 7. Why is my sales order not updated at all after posting the production?
In that case, the **Update Source Document** flag is not set on the production order. Without this flag, the system updates only the production order, but not the linked sales order.

### 8. Can I set the "Update Linked Document" field myself?
No. It is a technical flag set by the system on the sales line and on the warehouse shipment line. It serves to control the conversion and is not intended for manual maintenance.

### 9. Why are my manually changed KG, Meter, or Piece values not recalculated?
After the write-back from production, the **Do not reconvert** flag is set so that the actually produced values are retained. In addition, the quantity consistency check of the Item Card decides whether and how manual changes recalculate the remaining unit fields.

### 10. I cannot trigger the automatic conversion — what is the cause?
Check whether the permission set **MuM OPUC Gen. Perm** is assigned. It defines which actions users may perform with the app's processing codeunits; without this permission the conversion is not executed during posting.

## Typical Use Cases

The following examples show the process in Business Central. All pages and fields described are populated through the two parent apps and the connector app; no fictitious company or test scenarios are used.

### Use Case 1: Underproduction of a lot (meter goods)

**Trigger:** Production reports that less was produced than planned for an order involving meter goods, and the order is to be completed with this lower quantity.

**Entry point in BC:** Open the **Released Production Order** and select the line. Use the standard action to open the **Production Journal**.

**Core process:**
1. Record the actually produced quantity as **actual output**.
2. Open the **Item Tracking Lines**, assign the **lot**, and check the value **Meter**; the **unit field** is set to **Meter**, so that the check is performed via the **Finished Meter**.
3. Since the quantity is below the planned one, set the **Finished** flag. If a warning about underproduction appears, confirm it.
4. **Post** the Production Journal.

**Conclusion:** On the production order line there are now the **Finished Meter** (and the KG and Piece derived from them) as well as the remaining **Remaining Meter**. The **Do not reconvert** flag is set, so that the actually produced values are retained.

### Use Case 2: Overproduction with update of the sales order

**Trigger:** More is produced than ordered for a customer-related order. On the production order, **Update Source Document** is active so that Sales sees the actual quantities.

**Entry point in BC:** Open the **Released Production Order** and the associated **Production Journal**.

**Core process:**
1. Record the higher quantity as **actual output**. When the overproduction limit is exceeded, confirm the warning, provided the rule permits this.
2. In the **Item Tracking Lines**, assign the **lot** with its values **KG/Meter/Piece**.
3. **Post** the Production Journal.

**Conclusion:** Since **Update Source Document** is active, the connector app updates the **Sales Order**: Quantity and **Reserved Quantity** are raised, and on the **Sales Line** the unit values KG/Meter/Piece as well as **Outstanding Order KG/Meter/Piece** are taken over from production; the **Update Linked Document** flag is set. If the order is subsequently delivered via a **Warehouse Shipment**, the warehouse shipment line takes over this flag and shows the actually produced KG/Meter/Piece.
