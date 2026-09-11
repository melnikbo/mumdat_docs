---
title: Anwenderhandbuch m+m Invoice Purchase Receipt with Unit Conversion
---

# User Guide m+m Invoice Purchase Receipt with Unit Conversion

## Introduction

This module extends the existing **Invoice Purchase Receipt** workflow with the three conversion quantities **KG**, **Meter** and **Piece**. In addition to the classic quantity in the base unit of measure, Business Central thus tracks in parallel, for each purchase receipt line, how much weight (KG), length (Meter) and piece count was received, already invoiced, not yet invoiced and consumed. During invoicing, these conversion quantities are automatically kept in sync with the purchase invoice, the reservation entries and the item reclassification journal.

The module is a bridge extension: it has no setup page and no master data card of its own. Its entire visible surface consists of additional columns in the **Invoice Purchase Receipt** list, plus three editable columns (**KG To Invoice**, **Meter To Invoice**, **Piece To Invoice**) through which you control a partial invoicing down to the exact quantity.

**Target audience:** Primarily the **operational users in invoice verification and goods receipt** who invoice purchase receipts every day and thereby check weight, length or piece count — for example in steel and metal trading, where a coil delivery is tracked in KG and Meter. Secondarily, the guide addresses administrators and key users who set up the prerequisites for the quantity conversion (section **Setup**).

**Short process overview:** The user opens the **Invoice Purchase Receipt** page, selects the receipt lines that are not yet fully invoiced, checks or limits the quantities to be invoiced (also separately by KG, Meter or Piece) and then triggers invoicing via the **Mandatory Withdrawal** action. The conversion quantities are automatically carried over into the follow-up documents.

## Quick start for users

Prerequisite: The quantity conversion is set up (see **Setup**) and the purchase receipt has already been posted, so that it appears in the list.

1. Use **Search** to open the **Invoice Purchase Receipt** page. The list automatically shows only lines with an open quantity (**Quantity** greater than 0).
2. Find the line to be invoiced by **Document No.**, **Vendor No.** or **Lot No.**. In the columns **KG Not Invoiced**, **Meter Not Invoiced** and **Piece Not Invoiced**, check which conversion quantities are still open.
3. *(Optional for partial invoicing)* Enter the desired partial quantity in **KG To Invoice**, **Meter To Invoice** or **Piece To Invoice**. The respective value must not exceed the associated not-invoiced quantity; **Quantity To Invoice** is automatically recalculated to match.
4. Run the **Mandatory Withdrawal** action. If an unposted purchase invoice already exists for the line, first confirm the safety prompt.
5. The purchase invoice is created or supplemented with the conversion quantities KG, Meter and Piece. These values are at the same time carried over into the reservation entries and — when lot tracking is used — into the item reclassification journal.
6. *(Optional)* Use the **Set Vendor Invoice No.** action to set the vendor invoice number for the selected lines.

This short sequence corresponds to the full invoicing workflow; you find the detailed explanation under **Daily work: Invoice Purchase Receipt**.

## Setup

For the module itself, **no additional setup** is required in the web client. In the Extension Management, the app **m+m Invoice Purchase Receipt with Unit Conversion** and its dependencies (m+m Cloud Base, m+m Invoice Purchase Receipt, m+m Unit Conversion) must be installed.

However, for values to actually appear in the columns **KG**, **Meter** and **Piece**, the business prerequisites of the quantity conversion must be met. These prerequisites are maintained in the dependency **m+m Unit Conversion** and subsequently take effect in the **Invoice Purchase Receipt** list. The following section describes this chain in dependency order.

### Setting up the prerequisites for the quantity conversion

**Who sets it up and when:** The administrator or key user sets up the quantity conversion once per item, before purchase receipts of these items are invoiced. The settings are later consumed in daily work on the **Invoice Purchase Receipt** page (see **Daily work**).

**Sequence in dependency order:**

1. **First**, in the **m+m Unit Conversion** module you store the conversion factors per item and unit of measure (e.g. KG per Meter and KG per Piece). Once these factors are set, Business Central can calculate the values for KG, Meter and Piece from the captured base quantity; without factors, the conversion columns remain 0.
2. **Then**, when the goods receipt is posted, the conversion quantities are tracked on the purchase receipt line. Once the purchase receipt is posted, the quantities are available as starting values for invoicing; the **Invoice Purchase Receipt** list reads them from the posted receipt line or — when lot tracking is used — from the item ledger entries.
3. **Finally**, in day-to-day business the user opens the **Invoice Purchase Receipt** page and triggers invoicing via **Mandatory Withdrawal**. When this step is carried out, the module automatically transfers the conversion quantities into the purchase invoice and the reservation entries.

**Dependency note:** The actual KG-per-Meter and KG-per-Piece factors are determined per line from the posted purchase receipt line; if the line is lot-tracked, the factors are instead read from the matching item ledger entry of the lot. If an actual factor is missing, the theoretical factor is used. Therefore maintain the factors completely so that the recalculated quantities are correct.

### Permissions

The module ships with the permission set **m+m PIUC Permission** (display name “All permissions”). It defines the permissions for the extension's two processing codeunits and determines which actions a user can carry out in connection with the quantity conversion. Assign this permission set to the users who invoice purchase receipts; the actual invoicing permission (access to the **Invoice Purchase Receipt** page and the underlying purchase documents) is additionally controlled via the permission sets of the base modules.

## Daily work: Invoice Purchase Receipt

All daily work takes place on the **Invoice Purchase Receipt** page. This page belongs to the base module; the present extension supplements it with the conversion columns KG, Meter and Piece, each in five variants (quantity, invoiced, not invoiced, consumed, to invoice).

**Entry point:** Use **Search** to open the **Invoice Purchase Receipt** page. The page is a company-wide task list and has no superordinate master data page; entering it via **Search** is therefore the intended way. On opening, the page automatically filters to lines with **Quantity** greater than 0, so that only receipt lines still to be invoiced appear.

**Controlling setup:** Whether and with which values the conversion columns are filled depends entirely on the item's quantity conversion (module **m+m Unit Conversion**, see **Setting up the prerequisites for the quantity conversion**). If no conversion factors are stored there, KG, Meter and Piece remain at 0, and invoicing is only possible via the base quantity.

### Columns of the line list

Business Central shows both the fields of the base module and the conversion columns supplemented by this extension on one screen in the line list. The following table documents the entire visible line.

**Identification and header data (from the base module, not editable):**

| Field | Explanation |
|------|-------------|
| Document No. | Number of the posted purchase receipt. When you select a line, all actions refer to exactly this document. |
| Posting Date | Posting date of the posted purchase receipt; used for the chronological classification of the open invoicing. |
| Vendor Shipment No. | Shipment number of the vendor. When you see several shipments of the same vendor, you distinguish them by this. |
| Vendor Invoice No. | Invoice number of the vendor. If it is still empty, you can add it via the **Set Vendor Invoice No.** action. |
| Vendor No. | Number of the vendor of the shipment. |
| Vendor Name | Name of the vendor; makes it easier to find the correct line without resorting to the number. |
| Vendor Address | Address of the vendor (control information for the line). |
| Location Code | Location of the posted receipt line; relevant when the same goods are held at several locations. |
| Bin Code | Bin within the location. |
| Type | Line type from the purchase receipt. The quantity conversion of this module only takes effect for the type **Item**; for other types (e.g. G/L account) KG, Meter and Piece remain without function. |
| No. | Item number of the line. |
| Description | Item description. |
| Description 2 | Additional item description. |
| Lot No. | Lot number of the line. When a lot is set, the module determines consumed and invoiced conversion quantities lot-specifically from the item ledger entries. |
| Lot Description | Description of the lot (control information). |
| Unit of Measure | Base unit of measure of the quantity (plain text). |
| Variant Code | Item variant of the line, if tracked. |
| Unit of Measure Code | Code of the base unit of measure; serves the module as the source unit for the conversion to KG, Meter and Piece. |

**Base quantities (from the base module, not editable except “Quantity To Invoice”):**

| Field | Explanation |
|------|-------------|
| Quantity | Total quantity received in the base unit of measure. Basis of all conversions. |
| Quantity Invoiced | Already invoiced portion of the quantity. |
| Quantity Not Invoiced | Still open portion of the quantity, to be invoiced. |
| Consumed Quantity | Already consumed portion (consumption / negative adjustment) according to the item ledger entries. |
| Quantity To Invoice | The quantity that will be settled with the next invoicing. When you enter a conversion quantity (KG, Meter or Piece), this value is automatically recalculated; if you enter it directly, you must not set it greater than the not-invoiced quantity. |

### Conversion columns of this extension

This extension adds the following 15 columns. KG, Meter and Piece each occur in five variants that correspond to the base quantities. All columns except the three “to invoice” ones are display fields and not editable.

**Received conversion quantities (display):**

| Field | Explanation |
|------|-------------|
| KG | When the item has a KG conversion, this column shows the received weight of the line in KG. It is the reference quantity for “KG Invoiced”, “KG Not Invoiced” and “KG To Invoice”. |
| Meter | When a Meter conversion exists, this column shows the received length of the line in Meter. |
| Piece | When a Piece conversion exists, this column shows the received piece count of the line. |

**Invoiced conversion quantities (display):**

| Field | Explanation |
|------|-------------|
| KG Invoiced | When this line has already been invoiced, the already invoiced weight in KG is shown here. When you invoice again, this reduces the still open quantity “KG Not Invoiced”. |
| Meter Invoiced | Already invoiced length in Meter; acts analogously on “Meter Not Invoiced”. |
| Piece Invoiced | Already invoiced piece count; acts analogously on “Piece Not Invoiced”. |

**Not yet invoiced conversion quantities (display):**

| Field | Explanation |
|------|-------------|
| KG Not Invoiced | Results from “KG” minus “KG Invoiced”. When this value is greater than 0, weight is still open for invoicing; it is at the same time the upper limit for “KG To Invoice”. |
| Meter Not Invoiced | Open, not yet invoiced length in Meter; upper limit for “Meter To Invoice”. |
| Piece Not Invoiced | Open, not yet invoiced piece count; upper limit for “Piece To Invoice”. |

**Consumed conversion quantities (display):**

| Field | Explanation |
|------|-------------|
| Consumed KG | When consumption or negative adjustment entries exist for the item's lot, this field sums their weight in KG. The value is deducted from the open quantity, so that already consumed quantities are not proposed for invoicing again. |
| Consumed Meter | Sums the consumed or negatively adjusted length in Meter (lot-specifically) and reduces the proposed quantity to invoice accordingly. |
| Consumed Piece | Sums the consumed or negatively adjusted piece count (lot-specifically) and reduces the proposed quantity to invoice accordingly. |

**Conversion quantities to invoice (editable):**

| Field | Explanation |
|------|-------------|
| KG To Invoice | When you enter a value here, you determine how much weight will be settled with the next invoicing; the module automatically recalculates “Quantity To Invoice” from it. The value must not exceed “KG Not Invoiced” — otherwise Business Central aborts with the message “KG to Invoice must not be greater than KG Not Invoiced”. |
| Meter To Invoice | When you enter a value here, invoicing is controlled length-based and “Quantity To Invoice” is recalculated accordingly. The value must not exceed “Meter Not Invoiced” (otherwise the message “Meter to Invoice must not be greater than Meter Not Invoiced”). |
| Piece To Invoice | When you enter a value here, invoicing is controlled piece-based and “Quantity To Invoice” is recalculated. The value must not exceed “Piece Not Invoiced” (otherwise the message “Piece to Invoice must not be greater than Piece Not Invoiced”). |

**Interplay of the editable fields:** You control the invoicing quantity either via the base quantity **Quantity To Invoice** or via one of the three conversion quantities. As soon as you change one of these fields, the module automatically aligns the others. For example, you can invoice exactly 500 KG of a coil without having to convert the corresponding base quantity yourself.

### Actions of the page

The actions of the **Invoice Purchase Receipt** list that are relevant for this module:

| Action | Explanation |
|--------|-------------|
| Mandatory Withdrawal | Starts the invoicing of the selected lines. When an unposted purchase invoice already exists for the line, a confirmation prompt appears beforehand. The action creates or supplements the purchase invoice line and thereby transfers the conversion quantities KG, Meter and Piece into the invoice, the reservation entries and — when lot tracking is used — into the item reclassification journal. |
| Set Vendor Invoice No. | Opens a dialog in which you assign the vendor invoice number to the selected lines. |
| Show Document | Opens the associated posted purchase receipt for the selected line. |
| Show Unposted Purchase Invoices | Shows the already existing, not yet posted purchase invoice for the selected line. The action is only available when a matching unposted invoice line exists. |

### Automatic quantity carry-over in the background

During invoicing, the module carries over the conversion quantities without any further action by the user. When the line carries **no** lot, KG, Meter and Piece are written directly from the purchase receipt line into the purchase invoice line. When the line is **lot-tracked**, the module sums the invoiced and consumed conversion quantities lot-specifically from the item ledger entries and distributes them across the reservation entries onto the invoice line. In addition, during the reclassification posting the same KG, Meter and Piece values are carried over into the item reclassification journal and the associated reservation entries, so that inventory movements remain consistent with the invoiced quantity. For the user this means: it is enough to check the quantity to invoice and run **Mandatory Withdrawal** — the conversion happens automatically and entry-accurate.

## FAQ and Troubleshooting

### 1. Why are there only zeros in the columns KG, Meter and Piece?

Because no conversion factors are stored for the item in the **m+m Unit Conversion** module. Without KG-per-Meter or KG-per-Piece factors, Business Central cannot convert the base quantity; maintain the factors so that the columns are filled.

### 2. Why is a conversion column not taken into account for a line?

The conversion logic only runs for lines of the **Type** “Item”. For other line types (e.g. G/L account), KG, Meter and Piece remain without effect, because no item is available for the conversion.

### 3. Why do I get the message “KG to Invoice must not be greater than KG Not Invoiced”?

You have entered more in **KG To Invoice** than is still open according to **KG Not Invoiced**. Reduce the value to at most the open quantity. The same check applies correspondingly to Meter and Piece.

### 4. Can I invoice a shipment partially?

Yes. Enter less than the open quantity in **Quantity To Invoice** or in one of the three “to invoice” conversion columns. The module allows any partial quantity up to the open quantity; a full settlement is not enforced.

### 5. Why does “Quantity To Invoice” change when I enter “Meter To Invoice”?

Because both fields describe the same invoicing. As soon as you capture a conversion quantity, the module recalculates the matching base quantity via the conversion factors and updates **Quantity To Invoice** automatically — and vice versa.

### 6. What determines the conversion factor that is used?

The module preferentially takes the **actual** factor of the posted purchase receipt line (KG per Meter or KG per Piece). If this is 0, the **theoretical** factor is used. For lot-tracked lines, the factors are instead read from the matching item ledger entry of the lot.

### 7. Why do the invoiced conversion quantities for lots deviate from the simple calculation “KG minus KG Invoiced”?

For lot-tracked lines, the module determines the invoiced quantities entry-accurate from the item ledger entries of the lot (invoiced KG/Meter/Piece) instead of from a simple difference value. In this way, the values remain correct even with several partial invoicings and lots.

### 8. What do the columns “Consumed KG/Meter/Piece” mean?

They sum — lot-specifically — the already consumed or negatively adjusted conversion quantities from the item ledger entries. These quantities are deducted from the open quantity, so that already consumed goods are not proposed for invoicing again.

### 9. Why do I not see a posted shipment in the list at all?

On opening, the page automatically hides all lines with **Quantity** equal to 0. If a receipt line is fully invoiced or carries no open quantity, it no longer appears.

### 10. Do I have to manually add the conversion quantities to the invoice and inventory after invoicing?

No. When running **Mandatory Withdrawal**, the module automatically transfers the conversion quantities into the purchase invoice line, the reservation entries and — when lot tracking is used — into the item reclassification journal. Manual entry afterwards is neither required nor intended.

## Typical use cases

### Use case 1: Invoicing a purchase receipt without lot tracking

**Trigger:** A supplier's invoice arrives by email. It refers to an already posted purchase receipt of an item that is tracked in KG but is not subject to lot tracking.

**Entry into BC:** Use **Search** to open the **Invoice Purchase Receipt** page. The list shows the open receipt lines.

**Core workflow:**
1. Filter or search for the line via **Vendor No.** and **Document No.**.
2. Check **KG Not Invoiced**. If the full open quantity is to be invoiced, leave the “to invoice” fields unchanged.
3. Run **Mandatory Withdrawal** and confirm a prompt that may appear.
4. The module writes the received KG (as well as Meter/Piece, if present) directly from the receipt line into the purchase invoice line and updates the reservation entries.

**Completion:** If needed, use **Set Vendor Invoice No.** to set the vendor invoice number, and check via **Show Unposted Purchase Invoices** that the invoice line was created with the correct KG values.

### Use case 2: Partial invoicing of a lot-tracked coil in Meter

**Trigger:** From a lot-tracked coil (tracked in KG and Meter), for billing reasons only a part is to be invoiced in Meter at first; the rest follows later.

**Entry into BC:** Use **Search** to open the **Invoice Purchase Receipt** page and select the line with the relevant **Lot No.**.

**Core workflow:**
1. Check **Meter Not Invoiced** and **Consumed Meter** to identify the length that is actually still invoiceable.
2. Enter the desired partial quantity in **Meter To Invoice** (at most “Meter Not Invoiced”). **Quantity To Invoice** is automatically recalculated.
3. Run **Mandatory Withdrawal** and confirm the prompt if an unposted invoice already exists.
4. The module determines the invoiced and consumed conversion quantities lot-specifically from the item ledger entries, distributes them across the reservation entries and additionally transfers the values into the item reclassification journal.

**Completion:** The line remains visible in the list with its remaining open quantity. For the later invoicing of the rest, repeat the workflow; the already invoiced meters are accounted for in **Meter Invoiced**.
