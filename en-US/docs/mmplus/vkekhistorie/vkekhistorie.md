---
title: Anwenderhandbuch m+m Sales Purchase History
---

# m+m Sales Purchase History User Guide

## Introduction

The **m+m Sales Purchase History** extension gives users of
**Microsoft Dynamics 365 Business Central** a condensed overview of all purchase and
sales documents down to **document line level**. It answers the everyday question "What
have we moved with this customer or vendor — and with this item — in the past?" without
requiring you to open each document type individually.

The extension collects open, archived, and posted document lines (exclusively lines of
type **Item**) for a customer or vendor, optionally narrowed to an item and a variant as
well as to a search period, and groups them by document type. The result is shown on two
dedicated overview pages — **Sales History** and **Purchase History** — as a temporary,
read-only list.

**Target audience.** The primary audience is **operational users** in day-to-day sales and
purchasing — internal sales, order entry, purchasing clerks — who want fast access to the
document line history of a business partner or item while working on a document. The
secondary audience is administrators, who configure the **History Setup** page once.

**Short process overview.**

1. An administrator defines, per area (sales/purchase) in **History Setup**, the default
   search period and the document types preselected by default.
2. The user opens **Sales History** or **Purchase History** — either directly via the
   search or from within a sales/purchase document.
3. The user sets filters (customer/vendor, item, variant, search period), runs
   **Build History**, and analyzes the lines; via **Show Document** they jump to the
   original document.

This extension writes **no** postings and changes **no** documents. It is purely an
analysis and navigation aid.

## Quick Start for Users

The fastest route to a result. Setup is a prerequisite and therefore comes first.

1. **One-time setup (administrator):** Use **Search** to open the **History Setup** page
   and enter, on the **Sale** tab and the **Purchase** tab, a date formula each (field
   **Sales History Period (Date Formula)** or **Purchase History Period (Date Formula)**)
   as well as the areas to be shown by default.
2. **Open the history:** Use **Search** to open the **Sales History** page (or
   **Purchase History**). Alternatively, open it directly from a document — see the
   chapter *History in Sales and Purchase Documents*.
3. **Set filters:** In the **Filter** area, enter the **Customer No.** (or **Vendor No.**)
   and check the prefilled **Searchperiod**. Optionally narrow down to **Item No.** and
   **Variant Code**.
4. **Build the history:** Choose the **Build History** action (F9). The lines are
   determined based on the filters and the area selection and are shown in the line area.
5. **Narrow down and open:** Click a document type in the **Area Filter** to see only its
   lines; via **Total** you return to the overall view. Select a line and choose
   **Show Document** to open the original document.

Note: Without at least one filter criterion besides the search period, the page reports
**No Filter defined!** and cancels the build.

## Setup

Setting up this extension is deliberately lean: there is **one** company-wide setup page
and **one** permission set. **No** number series and **no** master data are required.

### History Setup

**Who/when/why.** This page is configured by an administrator **once before first use**
per company. It is a company-wide single record and controls two things: the **default
search period** (as a date formula) and the **document types preselected by default**
(areas) that are already active when the sales or purchase history is opened. The user
later consumes both settings on the history pages (see *Sales History and Purchase
History*).

**Getting started:** Use **Search** to open the **History Setup** entry and click the
link of the same name. The setup record is created automatically the first time it is
opened. The page is divided into the two tabs **Sale** and **Purchase**, each with the
**Date** group and the **Areas** group.

**Sale tab**

| Setup | Explanation |
|---|---|
| **Sales History Period (Date Formula)** | Defines the analysis horizon for the sales history. If you enter, for example, `-1Y`, then when the sales history is opened the **Searchperiod** is automatically prefilled to "one year ago through today" and the document lines are filtered to this time window. Without a date formula, the sales history reports an error for the Sales History Period field when opened. |
| **Sales Quote** | If enabled, the **Quotes** area is preselected when the sales history is opened and open sales quote lines are included in the build; without the flag this area is initially hidden and can be added on demand via the area selection. |
| **Sales Quote Archive** | If enabled, archived sales quote lines are additionally included in the build; this way you also see quote versions that have already been deleted/archived. |
| **Sales Order** | If enabled, open sales order lines are included in the build by default — the most common use case for ongoing customer processes. |
| **Sales Order Archive** | If enabled, archived order versions (earlier versions) are shown as well. |
| **Sales Blanket Order** | If enabled, sales blanket order lines are included, e.g. to check call-off quantities against blanket agreements. |
| **Sales Blanket Order Archive** | If enabled, archived sales blanket orders are additionally considered. |
| **Sales Shipment** | If enabled, posted sales shipment lines are included in the build — relevant for delivery evidence and quantity reconciliation. |
| **Sales Invoice** | If enabled, posted sales invoice lines are shown — the basis for revenue and condition inquiries. |
| **Sales Credit Memo** | If enabled, posted sales credit memo lines are included, e.g. for complaint and return analyses. |
| **Sales Return Order** | If enabled, open sales return order lines are included in the build. |
| **Sales Return Order Arc.** | If enabled, archived sales return orders are additionally considered. |

**Purchase tab**

| Setup | Explanation |
|---|---|
| **Purch. History Period (Date Formula)** | Defines the analysis horizon for the purchase history. If you enter, for example, `-1Y`, then when the purchase history is opened the **Searchperiod** is prefilled accordingly and the document lines are filtered to this time window. Without a date formula, the purchase history reports an error for the Purch. History Period field when opened. |
| **Purch. Quote** | If enabled, the **Quotes** area is preselected when the purchase history is opened and open purchase quote lines are included in the build. |
| **Purch. Quote Archive** | If enabled, archived purchase quote lines are additionally included. |
| **Purch. Order** | If enabled, open purchase order lines are included in the build by default — the most common use case in purchasing. |
| **Purch. Order Archive** | If enabled, archived order versions are shown as well. |
| **Purch. Blanket Order** | If enabled, purchase blanket order lines are included, e.g. to reconcile call-offs against blanket agreements. |
| **Purch. Blanket Order Arc.** | If enabled, archived purchase blanket orders are considered. |
| **Purch. Rcpt.** | If enabled, posted purchase receipt lines (goods receipts) are included in the build — relevant for receipt evidence. |
| **Purch. Invoice** | If enabled, posted purchase invoice lines are shown — the basis for price and condition inquiries. |
| **Purch. Credit Memo** | If enabled, posted purchase credit memo lines are included. |
| **Purch. Return Order** | If enabled, open purchase return order lines are included in the build. |
| **Purch. Return Order Arc.** | If enabled, archived purchase return orders are considered. |

**Setup procedure.**

1. **First**, enter the **Sales History Period (Date Formula)** on the **Sale** tab and the
   **Purch. History Period (Date Formula)** on the **Purchase** tab — without a date
   formula the respective history page cannot be opened meaningfully.
2. **Then**, on both tabs under **Areas**, enable the document types that should usually be
   immediately visible for your users. This preselection is a default setting and can be
   adjusted at any time on the history page via the **Area Selection**.
3. **Finally**, direct your users to the history pages or to the document action (see
   *History in Sales and Purchase Documents*).

Note: The area flags in the setup are pure **defaults**. The user can set them differently
per session on the history page; the setup only determines the initial state.

### Permissions

This extension ships with the permission set **All permissions** (object "MuM SPH
Permission"). It defines which actions a user may perform on the tables, pages, codeunits,
and queries of this extension, and grants read/write access to the setup table as well as
execution rights for the history pages. Assign this permission set to the users who are to
work with the sales or purchase history. Because the two history line tables are built
**temporarily** per session, no permanent data records are created that would need to be
authorized separately.

## Sales History and Purchase History

The two history pages are functionally identical; they differ only in the business partner
(**customer** in the sales history, **vendor** in the purchase history) and in individual
price/quantity columns. Both are **read-only** worksheet pages: you cannot change
documents here, only analyze them and jump to the original document.

Each history page is divided into **four areas**: **Filter**, line area, **Area Filter**,
and **Area Selection**. The analysis horizon (search period) and the preselected document
types come from the **History Setup** page (see *Setup*).

### Filter

In the **Filter** area you narrow down which document lines are built. Besides the search
period, **at least one additional** criterion must be set, otherwise the page reports
**No Filter defined!**.

**Sales History – Filter**

| Filter field | Explanation |
|---|---|
| **Customer No.** | If set, only lines of the specified customer are built. This is the central filter criterion of the sales history. |
| **Item No.** | If set, the lines are additionally restricted to this item; the search then switches from customer reference to item reference, so that you can also analyze by item without a Customer No. When an Item No. is set, a previously set variant code is reset. |
| **Variant Code** | If set, the lines are additionally filtered to this item variant. The lookup opens the **Item Variants** page, filtered to the previously entered Item No. |
| **Searchperiod** | If set, only document lines within the specified date range are built. The value is prefilled from the **Sales History Period (Date Formula)** of the setup when opened and can be overwritten. |

**Purchase History – Filter**

| Filter field | Explanation |
|---|---|
| **Vendor No.** | If set, only lines of the specified vendor are built. This is the central filter criterion of the purchase history. |
| **Item No.** | If set, the lines are additionally restricted to this item; the search then switches to item reference. When an Item No. is set, a previously set variant code is reset. |
| **Variant Code** | If set, the lines are additionally filtered to this item variant. The lookup opens the **Item Variants** page, filtered to the previously entered Item No. |
| **Searchperiod** | If set, only document lines within the specified date range are built. The value is prefilled from the **Purch. History Period (Date Formula)** of the setup when opened and can be overwritten. |

### Line Area

In the line area all document lines are shown that match the filter criteria and the
current area selection. The lines are not editable. The following table describes the
columns shown by default; further columns are present but initially hidden (see *Further
columns hidden by default*).

**Sales History – Line columns (default display)**

| Field | Explanation |
|---|---|
| **Document Type** | Origin of the line. Values: **(blank)** (total lines or posted documents without document status), **Quote**, **Quote Archive**, **Order**, **Order Archive**, **Blanket Order**, **Blanket Order Archive**, **Shipment**, **Invoice**, **Credit Memo**, **Return Order**, **Return Order Archive**. Based on this value, **Show Document** jumps to the matching document. |
| **Document No.** | Number of the source document the line comes from. |
| **Document Line No.** | Line number within the source document. |
| **Sell-to Customer Name** | Name of the customer per the document header. |
| **Sell-to City** | City of the customer per the document header. |
| **Sell-to Country/Region Code** | Country/region code of the customer per the document header. |
| **Document Date** | Document date of the source document; filtered, among other things, by the search period. |
| **Order Date** | Order date of the source document (blank for credit memos). |
| **Status** | Document status of the line. Values: **(blank)** – posted documents (shipment, invoice, credit memo) carry no document status; **Open** – document in process, not yet released; **Released** – document released; **Pending Approval** – document in the approval workflow; **Pending Prepayment** – document awaiting prepayment. |
| **Item No.** | Item of the document line (only lines of type Item are built). |
| **Variant Code** | Item variant of the document line. |
| **Cross-Reference No.** | Cross-reference number (item reference) of the document line. |
| **Description** | Description of the document line. |
| **Description 2** | Additional description of the document line. |
| **Location Code** | Location of the document line. |
| **Bin Code** | Bin of the document line. |
| **Unit Of Measure Code** | Unit of measure of the document line. |
| **Quantity** | Document quantity of the line. |
| **Quantity Shipped** | Quantity already shipped (for open/archived orders). |
| **Quantity Invoiced** | Quantity already invoiced. |
| **Unit Price** | Sales price (unit price) of the document line. |
| **Line Discount %** | Line discount as a percentage. |
| **Line Discount Amount** | Line discount as an amount. |
| **Line Amount** | Line amount of the document line. |
| **Purchasing Code** | Purchasing code of the document line (standard BC field for purchasing control). |
| **Ship-To Code** | Code of the alternative ship-to address. |
| **Item Charges** | Flag or value for item charges of the document line. |

**Purchase History – Line columns (default display).** The layout corresponds to the
sales history; the differences are the business partner reference and individual
price/quantity columns:

| Field | Explanation |
|---|---|
| **Document Type** | Like the sales history, but with purchase-side values: **(blank)**, **Quote**, **Quote Archive**, **Order**, **Order Archive**, **Blanket Order**, **Blanket Order Archive**, **Shipment** (receipt), **Invoice**, **Credit Memo**, **Return Order**, **Return Order Archive**. |
| **Document No.** / **Document Line No.** | Number and line number of the source document. |
| **Buy-from Vendor Name** | Name of the vendor per the document header. |
| **Buy-from City** | City of the vendor per the document header. |
| **Buy-from Country/Region Code** | Country/region code of the vendor. |
| **Document Date** / **Order Date** | Document or order date of the source document. |
| **Status** | Like the sales history: **(blank)**, **Open**, **Released**, **Pending Approval**, **Pending Prepayment**. |
| **Item No.** / **Variant Code** / **Cross-Reference No.** | Item, variant, and cross-reference number of the document line. |
| **Description** / **Description 2** | Description and additional description of the document line. |
| **Location Code** / **Bin Code** / **Unit Of Measure Code** | Location, bin, and unit of measure. |
| **Quantity** | Document quantity of the line. |
| **Quantity Received** | Quantity already received (delivered). |
| **Quantity Invoiced** | Quantity already invoiced. |
| **Direct Unit Cost** | Purchase price (direct unit cost) of the document line. |
| **Line Discount %** / **Line Discount Amount** / **Line Amount** | Discount and amount of the document line. |
| **Purchasing Code** / **Ship-To Code** / **Item Charges** | Purchasing code, ship-to code, and item charges. |

**Further columns hidden by default.** Both history pages carry further columns that can
be shown via personalization. They are initially hidden for a better overview:
**Document Version No.** and **Doc. No. Occurrence** (filled only for archive documents),
**Sell-to Customer Name 2 / Buy-from Vendor Name 2**, **Sell-to Address / Address 2** or
**Buy-from Address / Address 2**, **Sell-to Post Code / Buy-from Post Code**, **Posting
Date**, **Quantity (Base)**, **Outstanding Quantity**, **Outstanding Qty. (Base)**, **Qty.
Shipped (Base) / Qty. Received (Base)**, and **Qty. Invoiced (Base)**. These fields provide
the same data reference as the visible columns, but in the base unit of measure or for
address and archive details.

### Area Filter

The **Area Filter** shows, for each document type, the number of document lines found in
parentheses (e.g. **Orders (12)**). It serves as a quick indicator and as a jump target:

- Click a document type, then only the lines of this document type are shown in the line
  area; the active document type is highlighted.
- Click **Total**, then all built lines are shown again.

The Area Filter comprises the same document types as the Area Selection: **Quotes**,
**Archived Quotes**, **Orders**, **Archived Orders**, **Blanket Orders**, **Archived
Blanket Orders**, **Shipments**, **Invoices**, **Credit Memos**, **Return Orders**,
**Archived Return Orders**, as well as **Total** (in the purchase history correspondingly
**Quotes**, **Orders**, **Blanket Orders**, etc.).

### Area Selection

The **Area Selection** is initially hidden. Show it via the **Area Selection View/Hide**
action. Here you set, per session, **which** document types are to be built at all. The
default comes from the **History Setup** page.

Important: If you change the area selection, you must then run **Build History** again so
that the lines are re-determined with the changed selection.

### Actions

| Action | Explanation |
|---|---|
| **Build History** | Determines the matching document lines based on the filter criteria and the area selection and shows them in the line area. Previous results are discarded and rebuilt. If, besides the search period, no further filter criterion is set, **No Filter defined!** is reported. (Keyboard shortcut F9.) |
| **Show Document** | Opens the corresponding original document for the selected line. Depending on the **Document Type**, the matching document is opened — e.g. **Sales Quote**, **Sales Order**, or a posted sales shipment/invoice/credit memo (in the purchase history correspondingly **Purchase Quote**, **Purchase Order**, etc.). |
| **Area Selection View/Hide** | Shows or hides the **Area Selection** area so that you can adjust the document types to be shown. |

## History in Sales and Purchase Documents

Users do not necessarily have to open the history via the search. In the relevant sales and
purchase documents, the history is provided directly as an action and is prefilled with the
filter criteria of the current document. This saves the manual entry of the customer/vendor
number and item.

**Sales documents.** In the **Sales Quote** and **Sales Order** documents you find the
**Sales History** action in two places:

- **In the document header** (also as a promoted action in the ribbon): Use the
  **Sales History** action to open the **Sales History** page. The **Customer No.** of the
  document is passed as a filter; the history is built immediately.
- **In the document line** (action on the line subpage): Select an item line and choose
  **Sales History**. In addition to the **Customer No.**, the **Item No.** and **Variant
  Code** of the line are passed. The line action requires the line to be of type **Item**.

**Purchase documents.** In the **Purchase Quote** and **Purchase Order** documents you find
the **Purchase History** action analogously:

- **In the document header** (also a promoted action): Opens the **Purchase History** with
  the **Vendor No.** of the document.
- **In the document line**: Opens the **Purchase History** with **Vendor No.**, **Item
  No.**, and **Variant Code** of the selected item line; here too the line must be of type
  **Item**.

In both cases the history page opens with the prefilled filters. There you can apply
further filters, change the **Area Selection** and reload via **Build History**, as well as
jump to other documents via **Show Document**.

## FAQ and Troubleshooting

### Why does the message "No Filter defined!" appear when building?
Because no filter criterion besides the **Searchperiod** is set. Enter at least the
**Customer No.** (or **Vendor No.**) or an **Item No.** and run **Build History** again.

### Why can't I change any lines in the history?
Both history pages are deliberately read-only and work on a temporary result list. They
serve exclusively for analysis and navigation. You make changes in the original document,
which you open via **Show Document**.

### Why are some document lines I expect missing?
Check three things: Is the matching **Document Type** enabled in the **Area Selection**?
Is the **Document Date** within the **Searchperiod**? And is it an **item line**? Only lines
of type **Item** are built — G/L account, resource, or text lines do not appear.

### Why do I see no new lines after changing the area selection?
The area selection only takes effect after building again. Run the **Build History** action
once more after each change to the area selection.

### How do I narrow down to a specific item or variant?
In the filter area, enter the **Item No.**; the search then switches to item reference. For
a variant, additionally set the **Variant Code** — the lookup opens the **Item Variants**
page, already filtered to the Item No. Caution: When entering a new **Item No.**, a
previously set **Variant Code** is automatically reset.

### Where does the prefilled search period come from?
From the **History Setup** page: the **Sales History Period (Date Formula)** or **Purch.
History Period (Date Formula)** stored there is converted, when the history is opened, into
a concrete search period "calculated from today." You can overwrite the value afterwards.

### What does the number in parentheses in the Area Filter mean?
It shows the number of built document lines per document type, e.g. **Invoices (8)**. A
click on the document type filters the line area to exactly this document type; **Total**
lifts the filter again.

### Why is nothing shown in the "Status" field for posted documents?
Posted documents — **Shipment**, **Invoice**, and **Credit Memo** — carry no document
status; their **Status** therefore remains **(blank)**. A status such as **Open** or
**Released** appears only for open and archived documents (quote, order, blanket order,
return order).

### Why does "Open history" from the document open a filled list directly?
Because the document action passes the filters of the current document (customer/vendor
no., and additionally item and variant from the line) and builds the history immediately.
This way you see the matching transactions without an intermediate step.

### Do I need special rights to open the history?
Yes. Assign the affected users the permission set delivered with the extension (object "MuM
SPH Permission"). It grants the necessary execution rights for the history pages and access
to the setup.

## Typical Use Cases (Usage Examples)

### Customer inquiry about earlier shipments and invoices

**Trigger.** A customer calls and asks which quantities of an item they received in the past
year and what they were charged for it.

**Getting started in BC.** Use **Search** to open the **Sales History** page. (Alternatively,
if you already have a document of this customer open, via the document action
**Sales History**.)

**Core procedure.**
1. In the **Filter** area, enter the **Customer No.** of the caller.
2. Check the prefilled **Searchperiod** (e.g. the past year) and adjust it if needed;
   optionally set the **Item No.**.
3. In the **Area Selection**, make sure that **Shipments** and **Invoices** are enabled, and
   run **Build History**.
4. Click **Shipments** in the **Area Filter** to see only the delivery quantities, then
   **Invoices** for the invoiced amounts.
5. Select a line and choose **Show Document** to give the customer details from the posted
   sales shipment or invoice.

**Conclusion.** No posting is created; the information is based entirely on the existing
documents. Via **Show Document** you can print or send the original document if needed
(standard functions of the respective document).

### Price and condition check when entering a purchase order

**Trigger.** A purchasing clerk enters a new **Purchase Order** and wants to check at what
price the same item was last procured from this vendor.

**Getting started in BC.** In the purchase order, select the item line and choose the
**Purchase History** action in the line. The **Purchase History** page opens with prefilled
**Vendor No.**, **Item No.**, and, if applicable, **Variant Code**.

**Core procedure.**
1. The history is already built; check the **Searchperiod** and extend it if needed.
2. Click **Invoices** in the **Area Filter** to see the most recently invoiced **Direct Unit
   Cost** values; via **Orders** you recognize procurements that are still open.
3. Compare **Direct Unit Cost**, **Line Discount %**, and **Line Amount** of the historical
   lines with your current order.
4. For follow-up questions, use **Show Document** to open the earlier **Purchase Order** or
   the posted purchase invoice.

**Conclusion.** With the price information gained this way, you finish entering the order
line. Here too, the history itself changes nothing in the document.
