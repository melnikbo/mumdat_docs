---
title: Anwenderhandbuch m+m Logistic Management with Additional Lot Information
---

# User Guide m+m Logistic Management with Additional Lot Information

## Introduction

The **m+m Logistic Management with Additional Lot Information** extension links the additional lot information with the item tracking of logistics documents. It adds lot-related details (vendor lot no., origin, manufacturer, original lot) to the **Item Tracking Lines** and provides an action that creates **multiple lots at once** from an open assignment quantity.

**Target audience:** Primarily **operational users in purchasing and warehouse logistics** who record lot-tracked items during goods receipt and maintain the item tracking of a purchase document. The extension has **no setup page of its own and no master data of its own**; after installation, the additional fields and the action are immediately available in the Item Tracking Lines. No separate configuration is required.

**Brief process overview:** For a purchase document line, the user opens the **Item Tracking Lines**, records one lot or – via the **Create Multiple Item Tracking** action – several lots, adds the lot-related additional details, and then posts the document. During posting, the recorded values are passed to the **Lot No. Information Card** and the reservation entries, so that the additional information stays permanently attached to the lot.

## Quick Start for Users

The fastest path from the document line to the posted lot:

1. Open the **purchase document** (e.g. a **Purchase Order**) that has a line for a lot-tracked item.
2. Select the item line and open the **Item Tracking Lines** via **Line**.
3. Record the lot:
   - **Single lot:** Enter the lot number in **Lot No.** and fill in the additional columns (see below).
   - **Multiple lots automatically:** Choose the **Create Multiple Item Tracking** action. In the **Item Trck. Create Lots – Lot No.** dialog, specify the desired count under **Number Of Lots** and fill in the shared additional details. Confirm with **OK**.
4. Verify that the total of the assigned quantities (**Qty. to Assign**) matches the document quantity to be tracked.
5. **Post** the purchase document (receive/ship). The additional details are thereby passed to the **Lot No. Information Card**.

> The **Create Multiple Item Tracking** action is available in the **item tracking for purchasing**. It is not offered in sales documents; there, the additional columns are still visible and readable.

## Daily Work: Item Tracking Lines with Additional Details

This extension takes effect exclusively in the **Item Tracking Lines** of a document. It extends the existing item tracking assignment with lot-related additional columns and with an action for creating multiple lots. The base columns of item tracking (among others **Lot No.**, **Qty. to Assign**, **Unit of Measure Code**, **Item No.**, **Variant Code**) remain unchanged; the following sections describe the fields and actions that this app displays **in addition**.

### Additional Columns in the Item Tracking Lines

The app displays the following additional columns in the line table. If a line is assigned a **Lot No.** for which a **Lot No. Information Card** already exists, these fields are filled **automatically** from the card when the lot no. is confirmed; if the lot no. is cleared again, they are automatically reset.

| Field | Explanation |
|------|-------------|
| **Vendor Lot No.** | If set, the lot number assigned by the vendor is carried on the assignment line and passed to the Lot No. Information Card during posting; this preserves traceability back to the vendor lot. When the document is posted, vendor lot information is created for this number if needed. |
| **Vendor Internal Lot No.** | If set, the vendor's internal lot number is additionally carried along; this enables reconciliation with delivery papers that bear the vendor's in-house lot identifier. |
| **Bundle** | If enabled, the lot is flagged as a bundle (e.g. a steel bundle); the flag is passed to the Lot No. Information Card and is available there for evaluation and further processing. If the option is not set, the lot is treated as an individual quantity without a bundle flag. |
| **Country/Reg. Of Orig. Code** | If set, the country or region of origin of the lot is recorded and passed to the lot during posting; this supports proofs of origin and country-based evaluations. |
| **Purchased from Vendor No.** | Automatically taken from the purchase line (vendor of the order) when creating multiple lots and is not manually editable. This makes it possible at any time to see which vendor the lot was sourced from. |
| **Manufacturer Code** | If set, the manufacturer of the lot is recorded and passed to the Lot No. Information Card; the associated **Manufacturer Name** is additionally available there. This allows the lot to be assigned to its producer. |
| **Original Item No.** | Filled when the lot was linked to an original item from a production; shows the item number of the original lot. The field is not editable and serves for tracing back to the original item used. |
| **Original Variant Code** | If an original lot is linked with a variant, the variant of the original item is shown here. Not editable. |
| **Original Lot No.** | If the lot is linked via an original item to a further lot, the original lot number is shown here; this makes the source lot from production traceable. Not editable. |

The older **Manufacturer Code** value from an earlier version is automatically carried over during an upgrade into the **Manufacturer Code** field mentioned above; an additional, technically obsolete manufacturer code field is hidden and has no meaning for the user.

### Action: Create Multiple Item Tracking

When a quantity to be tracked must be split across multiple lots (typical during goods receipt of a delivery that arrives in several bundles or lots), this action saves you from manually creating each individual line.

**Procedure:**

1. Open the **Item Tracking Lines** for the purchase document line.
2. Choose the **Create Multiple Item Tracking** action (also reachable via the keyboard shortcut Alt+C).
3. The **Item Trck. Create Lots – Lot No.** dialog opens. Record the following details:

| Field | Explanation |
|------|-------------|
| **Number Of Lots** | Specify how many lots are to be created. When you enter a value, the still-open assignment quantity (**Qty. to Assign** less the quantity already assigned) is split evenly across this count; the split is rounded to the item's rounding precision, and any remaining remainder is added to the last lot. The action can be run more than once if needed. |
| **Bundle** | If enabled, all created lots are flagged as a bundle (e.g. steel); the value is transferred to every new line. |
| **Country/Reg. Of Orig. Code** | If set, all created lots receive this country of origin; the entry is passed to every new line. |
| **Vendor Lot No.** | If set, the vendor lot number is transferred to the created lines. |
| **Vendor Internal Lot No.** | If set, the vendor's internal lot number is transferred to the created lines. |
| **Manufacturer Code** | If set, the manufacturer code is transferred to the created lines. |

4. Confirm with **OK**. The system creates as many item tracking lines as specified under **Number Of Lots**, automatically assigns each line a new **Lot No.** from the number series stored on the item, distributes the open quantity across the lines, and transfers the additional details recorded in the dialog to every line.

> **Note:** If the still-open assignment quantity is zero, no split is possible and the notice *"Quantity is 0. Division is not possible."* appears – first record the quantity to be tracked in the document line. A prerequisite for the automatic lot number assignment is that a lot number series is stored on the item; if it is missing, the system points this out.

### How the Additional Details Are Linked to the Lot

The recorded values are not only visible on the document line but are permanently linked to the lot:

- During **posting** of the document, the details of the item tracking line (vendor lot no., internal lot no., country of origin, bundle, manufacturer code, original item/lot) are transferred to the **Lot No. Information Card**; the card is created if needed.
- If an existing **Lot No. Information Card** is subsequently changed, the associated, still-open item tracking lines are automatically reconciled with the new values. This keeps the document line and the lot master data consistent.
- If you select an already-known **Lot No.** on a line, the additional fields are pre-filled automatically from the existing Lot No. Information Card. If you clear the lot no., the additional fields are cleared again.

## Permissions

The extension ships the assignable permission set **MuM ASAI Permission**. It defines which actions the internal functions of this app (among others the management of the item tracking additional details as well as the install and upgrade routines) are allowed to perform. Assign this permission to the users who work with purchase documents and item tracking. Beyond that, the actual visibility of the documents and item tracking lines is determined by the standard permissions of Business Central and the logistics modules.

## Typical Use Cases

### Use Case 1: Goods Receipt of a Delivery with Multiple Lots

**Trigger:** Purchasing receives a delivery of a lot-tracked item that arrives in several bundles or lots; the packing slip lists multiple lot numbers.

**Entry point in BC:** The user opens the corresponding **Purchase Order**, selects the item line, and opens the **Item Tracking Lines** via **Line**.

**Core procedure:**
1. Choose the **Create Multiple Item Tracking** action.
2. In the **Item Trck. Create Lots – Lot No.** dialog, enter the **Number Of Lots** (e.g. the number of delivered bundles), enable **Bundle**, and fill in the shared details (**Country/Reg. Of Orig. Code**, **Vendor Lot No.**, **Manufacturer Code**).
3. Confirm with **OK**. BC creates the corresponding number of lines, assigns each line a new **Lot No.**, and splits the quantity.
4. If needed, readjust individual quantities (**Qty. to Assign**) per line until the total matches the document quantity.

**Conclusion:** The user posts the goods receipt (receive). For each lot, the **Lot No. Information Card** is created with the recorded additional details.

### Use Case 2: Record a Single Lot with Vendor and Manufacturer Data

**Trigger:** A mill test certificate is available for a delivered lot; the vendor and manufacturer details are to be documented on the lot in an audit-proof manner.

**Entry point in BC:** From the purchase document line via **Line → Item Tracking Lines**.

**Core procedure:**
1. Enter the **Lot No.** in the line. If the lot is already known as a Lot No. Information Card, the additional fields are pre-filled automatically.
2. Otherwise, manually record **Vendor Lot No.**, **Vendor Internal Lot No.**, **Country/Reg. Of Orig. Code**, and **Manufacturer Code**. The **Purchased from Vendor No.** is derived automatically from the document.
3. Set **Qty. to Assign** so that the item tracking is balanced.

**Conclusion:** During posting of the document, the details are transferred to the **Lot No. Information Card** and are later available for traceability and evaluation.

## FAQ and Troubleshooting

### 1. Why don't I see the "Create Multiple Item Tracking" action in the sales document?
The action is designed for **item tracking in purchasing** and is offered there in the Item Tracking Lines. It is not provided in sales documents; however, the lot-related additional columns remain visible there.

### 2. Why does the message "Quantity is 0. Division is not possible." appear?
The action splits the **still-open** assignment quantity. If it is zero (no quantity, or a quantity that is already fully assigned), there is nothing to distribute. First record the quantity to be tracked in the document line and start the action again.

### 3. Where do the automatically assigned lot numbers come from?
When creating multiple lots, the system draws the next number for each line from the **lot number series** stored on the item. If no lot number series is set up on the item, the action cannot assign numbers and points this out.

### 4. How is the quantity distributed across the individual lots?
The open quantity is divided evenly by the **Number Of Lots** and rounded to the item's rounding precision. Any remainder left over by the rounding is added to the **last** created lot so that the total exactly matches the document quantity.

### 5. Why are some additional fields (e.g. "Original Lot No.") not editable?
The origin fields (**Original Item No.**, **Original Variant Code**, **Original Lot No.**) as well as **Purchased from Vendor No.** are derived by the system from the Lot No. Information Card or from the document and serve for traceability. They are therefore not recorded manually.

### 6. Why are my additional fields filled as soon as I enter a lot no.?
If a **Lot No. Information Card** already exists for the entered **Lot No.**, the system automatically takes over its values into the line. This means known lots do not have to be recorded again.

### 7. What happens to the additional fields when I delete the lot no. again?
If the **Lot No.** is removed from a line, all lot-related additional fields (vendor details, origin, bundle, manufacturer code, original item/lot) are cleared automatically so that no inappropriate values remain on an empty line.

### 8. I subsequently changed a Lot No. Information Card – do I have to adjust the document lines?
No. Changes to a **Lot No. Information Card** are transferred automatically to the associated item tracking lines, so that the document and the lot master data stay consistent.

### 9. What is the "Bundle" flag used for?
**Bundle** marks a lot as a bundle (e.g. a steel bundle). If it is enabled, the flag is passed to the lot and is available for downstream evaluation and further processing; without the flag, the lot is treated as an individual quantity.

### 10. Do I have to set anything up for this extension?
No. The app needs no setup page of its own and no master data. After installation, the additional columns and the **Create Multiple Item Tracking** action are automatically available in the Item Tracking Lines. The only prerequisite for the automatic lot number assignment is a lot number series stored on the item.
