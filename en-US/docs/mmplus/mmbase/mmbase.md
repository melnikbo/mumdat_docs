---
title: "m+m Base: Anwenderhandbuch"
---

# m+m Base User Guide

## Introduction

**m+m Base** is a base module for **Microsoft Dynamics 365 Business Central** (BC). It bundles several
independent functional areas that extend the sales and purchasing process:

- **Credit limit check** – blocks the release of sales orders and the posting of warehouse shipments
  when a customer's credit limit is exceeded, with insurance-based limit determination and
  user-specific tolerance.
- **Document status** – a freely configurable status model for documents (e.g. sales order, purchase order) that
  executes stored events at every status change and logs every change.
- **Date types** – date-driven determination of a latest delivery or receipt date from the
  requested date, with language-dependent document text.
- **Blanket sales orders and blanket purchase orders** – additional fields for validity, mandatory acceptance and the callable
  blanket quantity.
- **Foreign trade default values** – pre-population of transaction specification, transport method and area of origin in new
  sales and purchase documents.
- **Packaging viewer** – a graphical visualization of the packaging arrangement.

**Target audience.** This guide is aimed primarily at **operational BC users** in sales and
purchasing back office who release orders, advance documents, capture dates and call off quantities from
blanket orders every day. It also addresses **administrators and key users** who maintain the setup and
the master data.

**Brief process overview.** Before first use, an administrator sets up the central functions
(credit limit, document status, date types, foreign trade) and maintains the associated master data (customer credit limit,
credit insurers, statuses, status events). During daily work these settings then take effect automatically: the
credit limit check kicks in on **Release** and **Post**, the document status is advanced via the actions
**Next Status** / **Previous Status** / **Manual Status**, and the date type calculates
the latest delivery or receipt date when the requested date is changed.

The permissions for all functions of this module are combined in the permission set **MuM MB All**;
this defines which actions users are allowed to perform and is assigned to users via
permission management.

---

## Quick Start for Users

Order by dependency: **first setup**, then master data, then daily work.

**A. Activate the credit limit check (administrator).**
1. Use **Search** to open the **Credit Limit Setup** page and set **Credit Limit** to active.
2. In the **Check** group, define which amounts are included (**Open Items**,
   **Open Orders**, **Delivery Bills Not Invoiced**, **Unposted Sales
   Invoices**).
3. In the **If Credit Limit Exceeds** group, define whether **Prevent Sales Order Release**
   and/or **Prevent Warehouse Shipment Posting** apply.
4. Use **Search** to open the **User Setup** and store per user the
   **Credit Limit Tolerance %** as well as **Allow Modify Credit Limit**.

**B. Release a customer's credit limit (back office).**
1. Open the **Sales Order** and choose **Release**.
2. If the used amount is above the credit limit but within your tolerance, confirm the dialog;
   the operation is logged in **Credit Limit Log** and continued.
3. If the amount is above the tolerance, the release is cancelled with an error message.

**C. Advance the document status (back office).**
1. Open the document; if a status model is set up, the **Status Code** field is visible.
2. Choose **Next Status** (or **Previous Status** or **Manual Status**).
3. Stored **Status Events** are executed; the change appears in the
   **Doc. Status Change Log**.

**D. Use the date type in a document (back office).**
1. In the sales order/purchase order, capture a **Requested Delivery Date** or receipt date.
2. Choose a **Date Type**; the **Latest Delivery Date** or **Latest Receipt Date** field is
   calculated automatically.

---

## Setup

Setup is the most extensive part of this module. Each of the following H3 sections describes an
independent function with its fields and the path from setup to daily use.

### Setting up the credit limit check

**Who/when.** An administrator sets up the **Credit Limit Setup** once per company, before the
credit limit check is used in sales. The check later takes effect when orders are released and
warehouse shipments are posted (see **Daily work in the sales order**). You maintain the associated customer master data
under **Customer Credit Limit** and **Customer Card** (see **Master Data**).

**Entry point:** Use **Search** to open the **Credit Limit Setup** page (company-wide
single setup).

The page is divided into three areas: **General**, **Check** (only active when **Credit Limit** is set)
and **If Credit Limit Exceeds**.

| Setup | Explanation |
|---|---|
| **Credit Limit** (General) | When enabled, the entire credit limit check of this module is switched on; only then do the fields of the **Check** and **If Credit Limit Exceeds** areas become editable and the m+m credit limit fields become visible on the **Customer Card**. Without this flag no check takes place. |
| **Open Items** (Check) | When enabled, the customer balance (open items) is included in the checked total; this way the credit limit applies to already invoiced, still open amounts. |
| **Open Orders** (Check) | When enabled, the customer's open orders are included in the check; the amount of the order currently being released is deducted once so that it is not counted twice. |
| **Delivery Bills Not Invoiced** (Check) | When enabled, delivered but not yet invoiced values are counted; this way the credit limit also accounts for goods that have already left the premises. |
| **Unposted Sales Invoices** (Check) | When enabled, not yet posted sales invoices are included; this way the check also captures invoices under creation. |
| **Skip If Credit Limit Zero** (Check) | When enabled, no check is performed for a credit limit of 0 (the document passes through unhindered); without the flag, 0 counts as a strict limit that every document total exceeds. |
| **Prevent Sales Order Release** (If Exceeds) | When enabled, the **Release** of a sales order is cancelled when the credit limit is exceeded; without the flag, the release is not interfered with despite the exceedance. |
| **Prevent Warehouse Shipment Posting** (If Exceeds) | When enabled, the **Post** of a warehouse shipment (or the registration of the pick) is cancelled when the limit is exceeded; this way the shipment can only be carried out after the limit has been clarified. |

**Process steps (dependency order).**
1. **First** customer master data: store the credit limit on the customer or via **Customer Credit Limit** and the
   **Credit Insurer** (see Master Data).
2. **Then** global activation: set **Credit Limit** in the **Credit Limit Setup** and choose the
   check components.
3. **Then** per user: store the tolerance in the **User Setup** (see below).
4. **Finally** during daily work: the check kicks in automatically on **Release** and **Post**.

**User-specific tolerance (User Setup).**

**Who/when.** The administrator stores a tolerance and a modification right per user in the **User
Setup**, before the credit limit check is used productively.

**Entry point:** Use **Search** to open the **User Setup** and choose the desired
user line.

| Setup | Explanation |
|---|---|
| **Credit Limit Tolerance %** | Defines the percentage tolerance by which this user is allowed to exceed the credit limit. When a value > 0 is set and the document total is within the limit thus increased, a confirmation dialog appears instead of a cancellation; if the user confirms, the operation is continued and logged in **Credit Limit Log**. With 0 there is no tolerance and the exceedance leads directly to cancellation. |
| **Allow Modify Credit Limit** | When enabled, this user may perform the **Edit List** action on the **Customer Credit Limit** page and change credit limit lines; without the flag the list is read-only for that user. |

Depending on the check flags, the check logic sums up the document amount, balance, open orders, delivered
and unposted amounts of the customer and compares the result with the customer's **Credit Limit (LCY)**. Whether it
is calculated net or gross is controlled by the **Calculate Without VAT** flag on the **Customer Card**
(see Master Data).

### Setting up document status

**Who/when.** An administrator sets up the status model, before documents (e.g. sales order, purchase order)
are to be run through a defined status flow. Users later use the stages via the
status actions on the document (see **Daily work in the sales order**). Setup is done in
dependency order: first the individual statuses, then the events to be triggered, then the chaining per
document type, and finally the assignment of the events.

**Entry point:** Use **Search** to open the **Document Status** page. From there you reach the associated
maintenance pages via the actions **Status**, **Status Event** and **Status Event Assignment**.

**1. Maintain statuses** – In **Document Status**, open the **Status** action.

| Field | Explanation |
|---|---|
| **Status Code** | Unique code of the status stage (e.g. the short key of the processing state) that the document and assignments refer to. |
| **Status Description** | Plain-text label of the stage; shown to the user in the **Manual Status** selection. |
| **Style Text** | Defines the color highlighting with which the status code is displayed on the document; serves for quick visual classification of the processing state. |

**2. Maintain status events** – In **Document Status**, open the **Status Event** action. A
status event refers to an object to be executed.

| Field | Explanation |
|---|---|
| **Event ID** | Unique code of the event, referenced in the **Status Event Assignment**. |
| **Event Description** | Plain-text label of the event. |
| **Object Type** | Defines which object type is executed when the status is reached. **Codeunit** (program logic) and **Report** are used; if the administrator chooses Codeunit, `Codeunit.Run` is executed on the status change, and for Report the report is started. Other technical object types in the selection (Table, XMLport, Page, Query, etc.) do not trigger any execution. |
| **Object ID** | Number of the object to be executed; if it is 0, no event is executed on the status change. |
| **Object Name** | Name of the selected object; shown for verification. |

**3. Chain document statuses** – Maintain the status sequence per **Table ID** and **Document Type** directly in the
**Document Status** list.

| Field | Explanation |
|---|---|
| **Table ID** / **Table Name** | Determines for which document table (e.g. Sales Header) the status sequence applies; the table name is reloaded for verification. |
| **Document Type** | Determines for which document type within the table (e.g. Order) the line applies; this way separate status sequences can be defined per document type. |
| **Status Code** / **Status Description** | The status stage of this line; the description is reloaded. |
| **Previous Status** | Status code the **Previous Status** action leads back to. If the field is empty, this is the first status: new documents of this table/document type receive this status automatically upon creation. |
| **Next Status** | Status code the **Next Status** action advances to. If the field is empty, the chain ends at this stage. |

The **Recalculate Order** action in the **Document Status** list re-orders the sequence of the status flow for
the selected table/document type and thereby ensures a consistent predecessor/successor chain after you have
inserted or removed stages.

**4. Assign status events** – In **Document Status**, open the **Status Event Assignment** action; it
opens the assignments filtered to the marked table/document type/status code.

| Field | Explanation |
|---|---|
| **Table ID** | Document table the assignment applies to. |
| **Document Type** | Document type within the table. |
| **Status Code** / **Status Description** | Target status upon whose reaching the events are executed. |
| **Event ID** / **Event Description** | The status event to be executed. |
| **Order** | Determines the order in which multiple events of the same target status are processed; execution is ascending by this value. |

The internal **Order** number (Sequence No.) is assigned automatically upon creation and is not
editable; to control the execution order, use the **Order** field.

**Operational conclusion.** The status flow is triggered during daily work via the document actions **Next Status**,
**Previous Status** and **Manual Status**; every change executes the assigned events in the
defined order and writes an entry to the **Doc. Status Change Log** (see
**History and Logs**).

### Setting up date types

**Who/when.** An administrator or key user maintains the **Date Types**, before users have a latest delivery or receipt date
determined in the sales order, in the purchase order or in the blanket document. The
date type is later applied via the **Date Type** field in the document (see **Daily work**).

**Entry point:** Use **Search** to open the **Date Types** list.

| Field | Explanation |
|---|---|
| **Code** | Unique key of the date type, selected in the document in the **Date Type** field. |
| **Description** | Plain-text label of the date type. |
| **Type** | Controls how the latest date is calculated from the requested date. All values: **Fix:** the latest date results from applying the **Date Formula** to the requested date. **From / To:** the latest date equals the requested date unchanged. **CW:** the latest date is set to the end of the calendar week of the requested date. **Pick Up:** no date is determined (self-collection, the field stays empty). **Date Period Week / Month / Quarter / Year:** the latest date is set one week, one month, one quarter or one year after the requested date. |
| **Date Formula** | Editable only for **Type = Fix**. When set, it is applied to the requested date to calculate the latest date; for other types an entry leads to an error message. |
| **Calculate Latest Delivery/Goods Rec. Date** | When enabled, the latest delivery or receipt date in the document is calculated automatically when the date type or requested date is changed. This flag and **… Editable** are mutually exclusive. |
| **Latest Del./Goods Rec. Date Editable** | When enabled, the user may enter the latest date in the document manually (no automatic calculation). This flag and **… Calculate** are mutually exclusive. |
| **Document Text** | Stores a multi-line text for the date type; it can be translated per language (see below) and serves as a date-related informational text. |

**Language-dependent document text (translation).**

**Entry point:** In **Date Types**, open the **Translation** action; it opens the **Document Text
Translation** page, filtered to the marked date type.

| Field | Explanation |
|---|---|
| **Language** | Language code for which a separate document text is stored; this way the appropriate text appears depending on the document language. |
| **Language Name** | Plain-text name of the language; shown for verification. |
| **Document Text** | The translated text for the chosen language. |

**Process steps.** 1. **First** create the date type with type, date formula and calculate/editable flags. 2. **Then**, if needed, capture a translation of the document text per language. 3. **Finally** select the
date type in the document via the **Date Type** field; the latest date is calculated or released.
Date types that are already used in documents cannot be deleted or renamed and can only be changed after
a prompt.

### Foreign trade default values

**Who/when.** An administrator stores default values for foreign trade once per company, so that new
sales and purchase documents are pre-populated automatically. The values are used during daily work when
a new document is created (see **Daily work**).

**Entry point:** Use **Search** to open the **Sales & Receivables Setup** or the
**Purchases & Payables Setup**; the fields are located there in the **Foreign Trade** group.

| Setup | Explanation |
|---|---|
| **Default Transaction Specification** | When set, this transaction specification is automatically transferred to the document field **Transaction Specification** when a new sales order or a new purchase order is created; the user does not have to enter it manually. |
| **Default Transport Method** | When set, this transport method is automatically transferred to the **Transport Method** field when the document is created. |
| **Default Area** | When set, this area of origin is automatically transferred to the **Area** field when the document is created. |

The three pre-populations take effect exclusively when a document is **newly created**; existing documents remain
unchanged and the values can be overwritten in the document at any time.

---

## Master Data

### Customer Card – credit limit fields

**Who/when.** Sales or accounts receivable maintains on the customer how the credit limit is determined and
calculated. The fields are only visible when the **Credit Limit Setup** is active. The information is used
on every credit limit check (see **Daily work**).

**Entry point:** From the customer list open the **Customer Card** and switch to the area with the
credit limit.

| Field | Explanation |
|---|---|
| **Credit Limit (LCY)** (m+m) | Shows the credit limit determined from the lines of the **Customer Credit Limit** page and is not directly editable; a double-click (DrillDown) opens the customer's **Customer Credit Limit** list. When the Credit Limit Setup is active, this field takes the place of the manual standard credit limit. |
| **Calculate Without VAT** | When enabled, the credit limit check for this customer is calculated on a net basis (document amount and included balances without VAT); without the flag the check is performed on a gross basis incl. VAT. |

If the current balance exceeds the credit limit, the credit limit field on the card is highlighted in color as unfavorable
– an immediate visual cue for the clerk.

### Customer Credit Limit and Credit Insurers

**Who/when.** Customer administration maintains one or more credit limit lines per customer, often backed by
a **Credit Insurer** and with a validity. From the lines valid on the work date, the customer's
**Credit Limit (LCY)** is summed up and written back to the customer automatically.

**Entry point:** Open the **Customer Credit Limit** list via the DrillDown from the **Credit Limit (LCY)** field of the
**Customer Card** (filtered to the customer) or as a standalone list via **Search**. To edit,
choose the **Edit List** action (only available when the **Allow Modify Credit Limit** flag is set
in your **User Setup**).

| Field | Explanation |
|---|---|
| **Customer No.** | Customer the credit limit line applies to. When changed, the customer's summed credit limit is recalculated. |
| **Customer Name** | Name of the customer; reloaded. |
| **Credit Insurer Code** | Refers to an entry of the **Credit Insurer**; assigns the limit line to an insurer. |
| **Credit Insurer Name** | Name of the insurer; reloaded. |
| **Insurance Type** | Controls the time limitation of the line. **Limited:** coverage ends at a fixed date; the **Insured To** field is then mandatory (otherwise an error message). **Unlimited:** coverage applies without an end date; **Insured To** can stay empty. |
| **Insured From** | Start of the validity of the limit line. Only lines whose period includes the work date are included in the summed credit limit. |
| **Insured To** | End of the validity; mandatory for **Limited**. An empty date means unlimited validity from **Insured From**. |
| **Limit Amount** | Amount with which this line contributes to the customer's credit limit. The sum of all valid lines yields the customer's **Credit Limit (LCY)**. |
| **Comment** | Free text for the line (e.g. background of the coverage). |

You maintain **Credit Insurers** as a simple master data list (call via **Search**):

| Field | Explanation |
|---|---|
| **Code** | Unique key of the insurer; referenced in the **Customer Credit Limit** line. |
| **Name** | Name of the credit insurer. |

**Process.** When a line is inserted, changed or deleted, the system sums up all limit amounts of the customer
valid on the work date and writes the result back into the customer's credit limit. This way the
credit limit always reflects the currently effective insurance commitments and is used by the credit limit check during
daily work.

---

## Daily work in the sales order and in the purchase order

This area is controlled by several setups: by the **Credit Limit Setup** and the **User
Setup** (release/posting block and tolerance), by the **Document Status** setup (visibility and
advancement of the status code), by the **Date Types** (calculation of the latest date) as well as by the
**Foreign Trade** default values (pre-population of new documents). The following fields and actions are added by m+m Base to the
standard documents **Sales Order** and **Purchase Order**.

### Document header

| Field | Explanation |
|---|---|
| **Date Type** | Selection of the date type; when changed – depending on the date type – the **Latest Delivery Date** or **Latest Receipt Date** is calculated. After a prompt (**Do you want to update lines?**) the date type is transferred to the document lines. Changeable only when the document status is **Open**. |
| **Latest Delivery Date** (Sales) / **Latest Receipt Date** (Purchase) | The latest date determined from the date type. Editable only if the date type has **… Editable** set; otherwise it is calculated and locked. |
| **Status Code** | Shows the current document status (in color per Style Text). Only visible when a **Document Status** is set up for the document table/document type. New documents automatically receive the first status of the chain. |

When a document is newly created, it additionally adopts the **Foreign Trade** default values (transaction specification, transport method,
area of origin) from the respective setup.

### Status actions

| Action | Explanation |
|---|---|
| **Next Status** | Advances the document to the **Next Status** stored in the **Document Status** chain, executes the assigned **Status Events** in their order and logs the change. If no successor is defined, the status stays unchanged. |
| **Previous Status** | Reverts to the **Previous Status** (also with event execution and logging). |
| **Manual Status** (sales order only) | Opens the **Status** selection list with all permitted other status codes; after the selection it switches directly to that status. This way intermediate stages can be skipped when the process allows it. |

### Credit limit check on release and posting

This check is not a separate action but kicks in automatically in standard actions:

1. **Release** of a sales order: if **Credit Limit** and **Prevent Sales Order Release** are active, the
   document total is checked against the customer's credit limit.
2. **Post** of a warehouse shipment (or register the pick): if **Credit Limit** and **Prevent Warehouse
   Shipment Posting** are active, the same check is performed.
3. If the total is within your **Credit Limit Tolerance %** tolerance, the prompt appears whether the
   process should be continued despite the credit limit exceedance; upon confirmation the exceedance is logged in
   **Credit Limit Log** and the operation is continued.
4. If the total is outside the tolerance, the operation is cancelled with an error message (the release
   or posting does not take place).

In addition, a net amount is carried along with every payment application in the customer ledger entry, so that the
net check (**Calculate Without VAT**) calculates correctly for open items as well.

### Document lines

| Field | Explanation |
|---|---|
| **Date Type** | Date type per line; transferred to the lines when the document header is changed (after a prompt), but can differ per line. |
| **Latest Delivery Date** / **Latest Receipt Date** | Line-related latest date, calculated or editable analogous to the header. |
| **Outstanding Net Amount** (sales line) | Shows the not yet invoiced net portion of the line (proportionally from open quantity and line amount); serves to assess the open order volume. |

---

## Blanket sales orders and blanket purchase orders

**Who/when.** Sales or purchasing back office works with **blanket sales orders** and
**blanket purchase orders** when quantities are called off over a period. m+m Base adds validity and
quantity fields that make the call-off transparent.

**Entry point:** Open the blanket sales order or the blanket purchase order via the respective document list.

### Header fields

| Field | Explanation |
|---|---|
| **Valid From** | Start of the validity of the blanket document; transferred to all lines when changed, so that the lines receive the same validity start. |
| **Valid Until** | End of the validity; likewise transferred to the lines. |
| **Mandatory Acceptance** | When enabled, the document marks a binding acceptance of the blanket quantity; this serves as the basis for the further processing and evaluation of binding contracts. |
| **Date Type** / **Latest Delivery Date** | Date control as in the order/purchase order (see **Daily work**). |

### Line fields

| Field | Explanation |
|---|---|
| **Valid From** / **Valid Until** | Line-related validity, pre-populated from the header. |
| **Outstanding Blanket Sales Order Quantity** (Sales) / **Outstanding Blanket Purchase Order Quantity** (Purchase) | Shows the sum of the still open quantities of all order/purchase lines created from this blanket line; makes visible how much has already been called off and how much is still open. |
| **Available Blanket Quantity** | Shows the still callable remaining quantity of the blanket line (open quantity less the outstanding order quantity already bound in orders/purchase orders). The value is updated automatically when the calling lines are created, changed and deleted. |
| **Date Type** / **Latest Delivery Date** | Date control per line. |

**Process.** When a user creates a sales order from a blanket sales order (or changes/deletes order lines
with a blanket reference), the system recalculates the **Available Blanket Quantity** of the associated blanket line.
This way the back office sees at any time which quantity can still be called off from the blanket.

---

## History and Logs

### Credit Limit Log

**Entry point:** Use **Search** to open the **Credit Limit Log** list (read-only history,
descending by entry).

Every exceedance permitted within the user tolerance is documented here.

| Field | Explanation |
|---|---|
| **Entry No.** | Sequential number of the log entry. |
| **Source No.** | Document number at which the exceedance occurred. |
| **Process** | Operation in which the check was performed. **Sales Order:** check on release. **Warehouse Shipment:** check on posting. **(empty):** legacy entry from a check method that has since been replaced (obsolete), without a process assignment. |
| **Customer No.** / **Customer Name** | Affected customer. |
| **User ID** | User who confirmed the exceedance. |
| **Datetime** | Time of the confirmation. |
| **Credit Limit** | The customer's credit limit valid at the time. |
| **Credit Limit Incl. Tolerance** | The maximum permitted limit, increased by the user tolerance. |
| **Tolerance %** | The applied tolerance of the user. |
| **Actual Used Credit Limit** | The checked, actually used amount including the triggering document. |

### Doc. Status Change Log

**Entry point:** Open it via the **Log** action on the **Document Status** page or via **Search**
(read-only history, descending by time).

| Field | Explanation |
|---|---|
| **Entry No.** | Sequential number of the log entry. |
| **Table ID** / **Table Name** | Document table whose status was changed. |
| **Record Id** | Internal record reference to the affected document. |
| **Document Type** | Document type of the document. |
| **From Status** | Status before the change. |
| **To Status** | Status after the change. |
| **Date/Time** | Time of the status change. |
| **User** | User who triggered the change. |

Via the **Open Related Record** action you jump directly to the logged document; if it no longer
exists, a corresponding note appears.

---

## Packaging Viewer

The **Packaging Viewer** is a graphical add-on tool (JavaScript add-in) that represents containers and packages
spatially. On the left it shows the overview lists **Container** and **Package** and on the right the graphical
arrangement. Via the **Refresh** action the display is recalculated and updated. The viewer
serves to illustrate the packaging placement; it is not a posting function.

> Note: m+m Base also contains a technical diagram/flow editor with sample data. This serves to
> demonstrate data structures and is not part of operational daily business.

---

## FAQ and Troubleshooting

### Why can a sales order not be released?
If the **Credit Limit** and **Prevent Sales Order Release** flags are set in the **Credit Limit Setup**
and the checked total of the customer exceeds his credit limit (beyond the tolerance), the
release is cancelled with an error message. Clarify the credit limit or the open amounts before you
release again.

### Why can a warehouse shipment not be posted?
Analogous to the release, the check kicks in on posting when **Credit Limit** and **Prevent Warehouse Shipment Posting** are active
and the limit is exceeded. The warehouse shipment only becomes postable after clarification.

### How may I exceed the credit limit despite the exceedance?
Store (or have the administrator store) a **Credit Limit Tolerance %** in the **User Setup**.
If the total is within this tolerated range, a prompt appears instead of the cancellation; after
confirmation the operation continues and is logged in **Credit Limit Log**.

### Why is nothing checked at all with credit limit 0?
If the **Skip If Credit Limit Zero** flag is set in the **Credit Limit Setup**, no check is performed for
a credit limit of 0. Without this flag, 0 counts as a strict limit that every
document total exceeds.

### Why is the Credit Limit field on the Customer Card not directly editable?
When the **Credit Limit Setup** is active, the **Credit Limit (LCY)** is summed from the valid lines of the
**Customer Credit Limit** page and updated automatically. Therefore change it via the credit limit lines
(DrillDown) and not directly on the field.

### Why can I not edit the lines in the Customer Credit Limit?
The **Edit List** action is only available when the **Allow Modify Credit Limit** flag is set
in your **User Setup**. Otherwise the list is read-only.

### Why does the system require a date for the insurance type?
For **Insurance Type = Limited** the **Insured To** field is a mandatory field; without an end date an
error message appears. Choose **Unlimited** if the coverage has no end date.

### Why can I not enter the latest delivery date?
The field is only editable when the assigned **Date Type** has the **Latest Del./Goods Rec. Date Editable** flag set.
If instead **… Calculate** is active, the date is determined automatically and locked.

### Why do I see no status code and no status actions on the document?
The **Status Code** field and the **Next/Previous/Manual Status** actions only appear when a status sequence is set up in **Document Status**
for the relevant document table and document type. If none is
set up, the field and actions stay hidden.

### Why does changing the date type also change the document lines?
When the **Date Type** (or the latest date) is changed in the document header, the system prompts with **Do you want to update
lines?**. If you confirm, the date type and latest date are transferred to all document lines;
if you decline, the change stays limited to the header.

---

## Typical Use Cases (Usage Examples)

### Example 1 – Overdue customer: release is blocked

**Trigger.** The back office receives a new order by e-mail from a customer whose account is already heavily
utilized.

**Entry point in BC.** The user opens the relevant **Sales Order** from the order list.

**Core flow.**
1. He chooses **Release**.
2. The active **Credit Limit Setup** (with **Prevent Sales Order Release**) checks the document amount plus
   the set-up components (open items, open orders, etc.) against the customer's **Credit Limit (LCY)**.
3. If the total is within his **Credit Limit Tolerance %**, he confirms the prompt; the
   exceedance is logged in **Credit Limit Log** and the release takes place.
4. Without sufficient tolerance, the release cancels with an error message.

**Conclusion.** After clarification (higher limit via **Customer Credit Limit** or settlement of open items) the
user releases the order; every tolerated exceedance remains traceable in the log.

### Example 2 – Running an order through a defined status process

**Trigger.** An order runs internally through several release stages (e.g. commercial and technical
check), which are mapped as document statuses.

**Entry point in BC.** The clerk opens the **Sales Order**; the current **Status Code** is visible
in color.

**Core flow.**
1. He chooses **Next Status**.
2. The system advances to the successor status stored in the **Document Status** chain.
3. The **Status Events** assigned to the target status are executed in their **Order** (e.g. a
   codeunit or a report).
4. The change is documented in the **Doc. Status Change Log** with from and to status, time and user.

**Conclusion.** If a stage has to be skipped or corrected, the user uses **Manual Status**
or **Previous Status**; every step remains traceable in the log.

### Example 3 – Contractual delivery date via a date type

**Trigger.** A customer agrees by phone that the delivery must take place at the latest at the end of the order
week.

**Entry point in BC.** The back office opens the **Sales Order** and captures the requested delivery date.

**Core flow.**
1. In the **Date Type** field he chooses a date type of type **CW**.
2. The system calculates the **Latest Delivery Date** to the end of the calendar week.
3. To the prompt **Do you want to update lines?** he confirms the transfer to the document lines.

**Conclusion.** The latest date is in the header and lines and serves for date scheduling; with an
editable date type the user could instead set the date manually.

### Example 4 – Calling off a quantity from a blanket sales order

**Trigger.** A planner is to call off a partial quantity from an existing blanket sales order.

**Entry point in BC.** He opens the **Blanket Sales Order** and creates from it a **Sales Order** with the
call-off quantity.

**Core flow.**
1. After the calling order line is created, the system updates the blanket line.
2. The **Outstanding Blanket Sales Order Quantity** field shows the bound, still open quantity.
3. The **Available Blanket Quantity** field shows the remaining, still callable quantity.

**Conclusion.** The planner immediately recognizes how much of the blanket has already been called off and how much is still
available, and plans further call-offs accordingly.
