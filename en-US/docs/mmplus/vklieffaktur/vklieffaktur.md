---
title: Anwenderhandbuch m+m Invoice Sales Shipment
---

# m+m Invoice Sales Shipment User Guide

This guide describes the **m+m Invoice Sales Shipment** extension for Microsoft Dynamics 365 Business Central. The module provides the **Invoice Sales Shipments** page: an overview of all posted sales shipment lines that still contain an open, uninvoiced shipped quantity. From this overview you create, post, print, and send sales invoices — individually, per document, or as a combined invoice per customer.

## Introduction

### Purpose of the module

In Business Central, a sales shipment remains open for invoicing after the warehouse shipment until the shipped quantity has been invoiced in full. Without additional tools, the user has to collect these open shipments one by one through the sales invoice and the function for retrieving shipment lines. The **Invoice Sales Shipments** module bundles exactly this process: it shows all sales shipment lines with an open quantity in a single list and invoices the selected lines with one click.

### Target audience

The primary audience is **operational users in sales and invoicing** who turn posted shipments into invoices on a daily basis and then post, print, or email those invoices. Secondarily, the guide is aimed at **administrators and key users** who assign permissions and set up the automatic combined invoicing via the job queue.

### Brief process overview

1. The warehouse shipment for a sales order is posted as usual; this creates a posted sales shipment with an open, not-yet-invoiced quantity.
2. The user opens the **Invoice Sales Shipments** page. It lists all shipment lines with an open quantity (**Qty. Shipped Not Invoiced** not equal to 0).
3. The user selects one or more lines and starts the **Invoice** action. In the **Options** dialog, they specify posting date, posting, printing, and sending.
4. The module creates one sales invoice per document, posts it on request, and prints or sends the posted document.
5. Alternatively, the same process runs fully automatically as combined invoicing via the job queue.

## Quick Start for Users

The fastest path from an open shipment to a posted invoice:

1. Open the **Invoice Sales Shipments** page via **Search**. (The page is set up as a task page and is therefore directly accessible from the search.)
2. The list shows all sales shipment lines with an open quantity. Lines for which an unposted sales invoice already exists are highlighted in a signal color.
3. Select the line(s) to be invoiced.
4. Choose the **Invoice** action.
5. If an unposted invoice already exists for a selected line, confirm the prompt *"There are unposted sales invoices for this line.\Do you want to proceed anyway?"* with **Yes** if you want to create an additional invoice.
6. In the **Options** dialog, enter the **Posting Date** and enable **Post Invoices** if the created invoice is to be posted immediately. Enable **Print posted document** or **Send posted document** if the posted document is additionally to be printed or sent.
7. Confirm the dialog. The module creates one invoice per shipment document and carries out posting, printing, or sending according to your options.

For recurring mass invoicing, set up the **automatic combined invoicing** instead (see the *Setup* section); it runs through steps 3 to 7 without a user dialog.

## Setup

The module requires **no dedicated setup page** and no master data. For productive use, only the installation of the extension, the assignment of permissions, and — optionally — the setup of automatic combined invoicing are required.

### Extension and permissions

The prerequisite is that the **m+m Invoice Sales Shipment** extension is installed and enabled in Extension Management. No further configuration in the web client is necessary.

For access, the module ships a permission set. It defines which actions users may perform in the module and includes the execution rights for the invoicing page, the two invoicing reports, and the codeunits for event handling and combined invoicing.

| Setup | Explanation |
|-------------|-------------|
| Assign permission set | When you assign the shipped permission set to a user or user group, that user receives the execution rights for the **Invoice Sales Shipments** page, the reports for single and batch invoicing, and the associated processing codeunits. Without this assignment, the page is not operable for the user. |

### Setting up automatic combined invoicing

Anyone who performs the standard case day after day should not trigger invoicing manually but automate it via the **job queue**. For this, the module provides a codeunit that carries out the batch invoicing run without a user dialog.

**Who sets it up:** administrator or key user. **When:** once before the first automated run, then controlled by the recurrence of the job queue entry. **Where the setting flows:** into the daily invoicing run that would otherwise be triggered manually via the **Invoice** action (see *Daily Work*).

Proceed in dependency order:

1. **First**, make sure the extension is installed and the permission set is assigned to the executing user. If this prerequisite is missing, the automatic run aborts with a permission error.
2. **Then**, create a job queue entry that runs the shipped combined-invoicing codeunit (object no. 5399952). When this entry is enabled and scheduled, it automatically processes all sales shipment lines with an open quantity on every run.
3. **Finally**, no further action is needed in the daily routine: the run posts the created invoices and prints the posted documents on its own. Faulty documents are not posted but flagged with an error text (see *History and Error Tracking*).

The automatic run uses fixed defaults: it filters the sales shipment lines to an open quantity, uses the **Work Date** as the posting date, posts the invoices (**Post Invoices** active), and prints the posted documents (**Print posted document** active). Whether a created invoice becomes a single or a combined invoice is controlled by the **Combine Shipment** flag on each shipment line (see *Combined Invoice per Customer*).

## Daily Work: Invoice Sales Shipments

The **Invoice Sales Shipments** page is the central workspace of the module. It is read-only and shows only sales shipment lines whose shipped quantity has not yet been fully invoiced (internal list filter: **Qty. Shipped Not Invoiced** not equal to 0). Sorting is by **Document No.** and line number.

### Getting started

Open the page via **Search** using the term *Invoice Sales Shipments*. The page is set up as a task page and is therefore directly accessible from the search; there is no need to open a higher-level document or a master data card.

### Columns of the overview

The following table describes the columns visible in the overview and those that can additionally be shown. All columns originate from the sales shipment line and are not editable.

| Field | Explanation |
|------|-------------|
| Document No. | Number of the posted sales shipment that the line originates from. Serves as the leading grouping criterion: lines with the same **Document No.** are combined into one invoice per document. The column is highlighted for better readability. |
| Bill-to Customer No. | Invoice recipient of the shipment line. If it differs from the sell-to customer, the invoice is issued to this deviating bill-to customer; for the combined invoice, lines are bundled by this customer. Lines with an already existing unposted invoice are highlighted in color in this column. |
| Sell-to Customer No. | Sell-to customer of the shipment line. Hidden by default; can be shown if you need to distinguish between the sell-to and the bill-to customer. |
| Type | Line type of the sales shipment line (e.g. Item, G/L Account). Determines which result line is created during invoicing. |
| No. | Number of the item or account of the line. |
| Variant Code | Variant of the item; hidden by default, relevant for variant-managed items. |
| Description | Description of the line as it is carried over into the invoice. |
| Description 2 | Supplementary description of the line. |
| Currency Code | Currency of the shipment line; hidden by default. If set, the created invoice is created in this currency. |
| Shortcut Dimension 1 Code | Value of the first shortcut dimension; hidden by default. Carried over into the invoice during invoicing. |
| Shortcut Dimension 2 Code | Value of the second shortcut dimension; hidden by default. Carried over into the invoice during invoicing. |
| Location Code | Location of the shipment; hidden by default. |
| Unit of Measure Code | Sales unit of measure of the line. |
| Quantity | Shipped quantity of the line. |
| Unit of Measure | Base unit of measure of the line; hidden by default. |
| Appl.-to Item Entry | Reference to the item ledger entry to be applied; hidden by default, relevant for item tracking. |
| Job No. | Project reference of the shipment line; hidden by default. |
| Shipment Date | Date of the warehouse shipment of the line; hidden by default. |
| Quantity Invoiced | Quantity of the line already invoiced. Shows how much of the shipped quantity has already been invoiced. |
| Qty. Shipped Not Invoiced | Still open, uninvoiced shipped quantity. Only lines with a value not equal to 0 appear in the list; this value is invoiced during invoicing. |

Lines for which an **unposted** sales invoice already exists are displayed in color as a hint. This lets the user recognize before invoicing that an open invoice has already been created for this shipment line, and avoid double invoicing.

### Actions of the overview

All of the actions below are additionally available in the menu bar as promoted actions.

| Action | Explanation |
|--------|-------------|
| Invoice | Invoices the selected shipment lines. When you trigger the action, the **Options** dialog opens; the module then creates one sales invoice per Document No. and posts, prints, or sends it according to the chosen options. |
| Show Document | Opens the associated **Posted Sales Shipment** for the selected line so that you can review the source document. |
| Show Unposted Sales Invoices | Opens the **Sales Lines** of the already existing unposted invoice for the selected line. If no matching unposted invoice line exists, the action is disabled. |
| Dimensions | Opens the dimensions of the selected line to view the dimension values. |
| Item Tracking Entries | Opens the **Item Tracking Lines** of the selected line (serial/lot information of the shipment). |

### The "Options" dialog during invoicing

After you have selected one or more lines and chosen **Invoice**, the prompt *"There are unposted sales invoices for this line.\Do you want to proceed anyway?"* appears first — provided an unposted invoice already exists for a selected line. Confirm with **Yes** and an additional sales invoice is created in addition to the existing one.

The **Options** dialog then opens with the following fields:

| Setup | Explanation |
|-------------|-------------|
| Posting Date | Date used for posting the created invoice. If one of the replace flags is active and no date has been entered here, processing aborts with the message *"A posting date must be entered."*. The work date is prefilled. |
| Replace Posting Date | When enabled, the posting date of the created invoice is replaced with the **Posting Date** entered above; otherwise the posting date determined by the standard process is retained. |
| Replace Document Date | When enabled, the document date of the created invoice is replaced with the **Posting Date** entered above; otherwise the determined document date is retained. |
| Calc. Inv. Discount | When enabled, the module runs the invoice discount calculation before posting, so that a cross-line discount is determined. Prerequisite: in the Sales & Receivables Setup, the automatic invoice discount calculation must not be active; otherwise a check prevents the use of this option. |
| Post Invoices | An unposted invoice is always created first. If this option is enabled, the invoice is posted in the same run; otherwise it remains as an unposted sales invoice for later review. |
| Print posted document | When enabled, the posted invoice document is printed via the configured report selection after successful posting. Enabling it forces **Post Invoices** on and switches **Send posted document** off, since only a posted document can be printed. |
| Send posted document | When enabled, the posted document is sent according to the customer's document sending profile (e.g. by email). Enabling it forces **Post Invoices** on and switches **Print posted document** off. |

Interplay of the options: if you disable **Post Invoices**, then **Print posted document** and **Send posted document** are automatically disabled as well, because without posting no posted document is created. **Print posted document** and **Send posted document** are mutually exclusive.

### What happens in the background during invoicing

So that you can classify the result correctly, here is the process carried out by Business Central: the module groups the selected shipment lines by **Document No.** and creates one sales invoice per document. Into the invoice header it carries over the sell-to or bill-to customer, the replaced posting and document date if applicable, the **Ship-to Code**, the **Currency Code**, the shortcut dimensions, and — from the associated sales order — the payment terms and shipment method. The shipment lines are then read in as invoice lines via the standard function for retrieving shipment lines. If **Calc. Inv. Discount** is active, the discount calculation follows; if **Post Invoices** is active, the invoice is posted and — depending on the option — printed or sent.

## Combined Invoice per Customer

Via the **Combine Shipment** flag on each sales shipment line, the module controls whether a customer's shipments are combined into **one** invoice.

| Field | Explanation |
|------|-------------|
| Combine Shipment | Flag on the sales shipment line. When set, all affected shipment lines of the same bill-to customer are merged into a common sales invoice in the batch run; if it is not set, a separate invoice is created per shipment document. |

The flag is **not** maintained manually on the invoicing page but is set automatically when the sales shipment is posted: the module carries over the value of the standard **Combine Shipment** field from the sales document onto the resulting shipment line. When a sales order with active combine shipment is shipped, the associated shipment line carries the flag and is bundled in the automatic run with the other combine-shipment lines of the same customer.

The batch report **Batch Invoice Sales Shpt.** evaluates this flag: lines with combine shipment are collected per bill-to customer and merged into one invoice; all other lines are invoiced individually per shipment document. Before creating, the run uses the standard block check to verify whether the customer is blocked for sales invoices.

## History and Error Tracking

The module does not keep its own history list. However, for tracking failed runs it extends the standard list of sales invoices with an error column.

### Error text on the sales invoice list

During automatic or batch invoicing, the creation or posting of an individual invoice can fail (e.g. blocked customer, missing information). So that an error does not abort the entire run, the module catches it per document, discards empty invoice headers, and records the cause.

| Field | Explanation |
|------|-------------|
| Error Text | Filled on the sales invoice header in the batch run if the creation or posting of this invoice failed. When a value is present, the field contains the last error message that occurred and points the clerk to the invoice that needs to be reviewed; on successful processing the field remains empty. |

The **Error Text** column is shown at the end of the **Sales Invoices** list. Through it, after an automatic run, the user recognizes at a glance which invoices could not be posted and for what reason, and can rework them specifically.

## FAQ and Troubleshooting

### 1. Why does a sales shipment line not appear in the overview?

The **Invoice Sales Shipments** page shows only lines with an open quantity (**Qty. Shipped Not Invoiced** not equal to 0). If the shipped quantity has already been fully invoiced, the line disappears from the list.

### 2. Why is a line highlighted in color?

The color highlighting marks shipment lines for which an **unposted** sales invoice already exists. This is a hint to avoid accidental double invoicing.

### 3. What happens if I invoice a highlighted line anyway?

When triggering **Invoice**, the prompt *"There are unposted sales invoices for this line.\Do you want to proceed anyway?"* appears. Confirm with **Yes** and an additional sales invoice is created in addition to the existing one.

### 4. Why does the dialog require a posting date?

If you enable **Replace Posting Date** or **Replace Document Date** but do not enter a date, processing aborts with the message *"A posting date must be entered."*. In this case, enter a valid **Posting Date**.

### 5. Why can "Calc. Inv. Discount" not be used?

The option checks that the automatic invoice discount calculation is disabled in the Sales & Receivables Setup. If this setting is active, the check prevents the use of the option in order to rule out a double discount calculation.

### 6. Why is the invoice not posted even though I invoiced it?

The module always creates an **unposted** invoice first. Only if you enable **Post Invoices** in the dialog is it posted in the same run. Without this flag, the invoice remains as an unposted sales invoice.

### 7. Why are "Print posted document" and "Send posted document" greyed out?

Both options require posting. As long as **Post Invoices** is not active, they are unavailable; enabling either of the two options automatically switches **Post Invoices** on as well. In addition, printing and sending are mutually exclusive.

### 8. Why are several invoices created instead of one combined invoice?

A combined invoice per customer is only created for shipment lines with the **Combine Shipment** flag set. This flag is carried over from the **Combine Shipment** field of the sales document when the shipment is posted. If it is missing, a separate invoice is created per shipment document.

### 9. Where do I see why an automatic run could not post an invoice?

The batch run writes the error cause per document into the **Error Text** field. Show the **Error Text** column in the **Sales Invoices** list to see the affected invoices and the respective message.

### 10. Why is an invoice skipped in the automatic run?

Before creating, the run checks whether the customer is blocked for sales invoices and whether an invoice line already exists for the shipment line. If the customer is blocked or an invoice line already exists, the affected line is not invoiced again; on a genuine error the empty invoice header is discarded and the **Error Text** is filled.

## Typical Use Cases

### Use case 1: Invoice a single shipment after a customer request

**Trigger:** A customer calls and asks for the invoice for a shipment already received.

**Entry point in BC:** The clerk opens the **Invoice Sales Shipments** page via **Search**.

**Core flow:**
1. They find the customer's line(s) by **Bill-to Customer No.** and **Document No.** and select them.
2. Via **Show Document**, they review the associated **Posted Sales Shipment** if needed.
3. They choose **Invoice**.
4. In the **Options** dialog, they enter the **Posting Date**, enable **Post Invoices** and **Send posted document**, and confirm.

**Conclusion:** The invoice is posted and sent according to the customer's document sending profile. The invoiced line disappears from the overview as soon as its open quantity has been fully settled.

### Use case 2: Daily combined invoicing via the job queue

**Trigger:** At the end of the day, all open shipments are to be settled automatically; customers with active combine shipment each receive a single bundled invoice.

**Entry point in BC:** No manual entry — the configured job queue entry starts the combined-invoicing codeunit (see *Setting up automatic combined invoicing*).

**Core flow:**
1. The run filters all sales shipment lines with an open quantity.
2. Lines with the **Combine Shipment** flag are merged per **Bill-to Customer No.** into one invoice; the remaining lines are invoiced individually per **Document No.**.
3. For each document, the run checks the customer block and creates the invoice; it is then posted (**Post Invoices**) and printed (**Print posted document**).

**Conclusion:** All successful invoices are posted and printed. Failed documents can be traced via the **Error Text** in the **Sales Invoices** list.

### Use case 3: Rework a failed invoice from an automatic run

**Trigger:** After the automatic run, accounting reports that no invoice arrived for a customer.

**Entry point in BC:** The key user opens the **Sales Invoices** list and shows the **Error Text** column.

**Core flow:**
1. They filter on filled **Error Text** entries and read the error cause (e.g. blocked customer).
2. They fix the cause in the respective master record.
3. They open **Invoice Sales Shipments** again; since the affected shipment line still carries an open quantity, it reappears in the list.
4. They select the line, choose **Invoice**, enable **Post Invoices**, and confirm.

**Conclusion:** The previously failed invoice is now posted; the open quantity of the shipment line has been settled.
