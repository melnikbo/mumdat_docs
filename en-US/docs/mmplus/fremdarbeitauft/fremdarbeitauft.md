---
title: Anwenderhandbuch m+m Subcontracting
---

# m+m Subcontracting User Guide

## Introduction

The **m+m Subcontracting** module represents **subcontract work** (subcontracting/contract processing) in Microsoft Dynamics 365 Business Central as a standalone document: the **Subcontract Order**. With it, the user controls the entire process when an operation or an item is outsourced to an external vendor (subcontractor) — from the outbound shipment to the vendor, through the receipt of the processed goods, to the invoicing of the processing service.

A subcontract order consists of a **header** (vendor, addresses, dates, locations, status), the **order lines** (the source documents to be processed, such as a production order or sales order, including lots/serial numbers), and the **groups** (the quantity- and value-based bundled positions that go out and come back in and are invoiced). Each group can additionally carry **item charges**, an **Ext. Description**, and assigned **lots/serial numbers**. Postings create **Subcontract Order Entries** and — via the **purchase order** managed in the background — posted receipts and purchase invoices.

**Target audience:** Primarily **operational users** who work with subcontracting on a daily basis — production control, work preparation, purchasing/planning, and warehouse staff who create subcontract orders, release them, post outbound and inbound, and invoice. **Secondarily**, the **Setup** chapters and the master data preparation address **administrators and key users** who configure the module once.

**Typical entry point:** A subcontract order is usually not created on a blank page, but **from an existing document**: from a **sales order line** (action **Create Subcontract Order** in the sales order) or from a **released production order** with an operation at a work center marked as subcontracting. The user then continues working in the **Subcontract Orders** list and on the **Subcontract Order** document page.

## Quick Start for Users

The quick start shows the shortest end-to-end path. It assumes a **one-time setup** by the administrator (see the **Setup** chapter); the daily work then follows a fixed sequence.

**Prerequisite (one-time, administrator):**

1. Open **Search**, call up the **Subcontract Order Setup** page, and enter the **number series** in the **Subcontract Order Nos.** field (mandatory field for the document number).
2. On the same page, enter the report IDs for **Subcontract Order**, **Subcontract Shipment**, and **Subcontract Pick Up** if printing is required.
3. Ensure that at least one **work center** with a filled **Vendor** field (Subcontractor No.) exists as a subcontracting work center.

**Daily flow (operational user):**

1. Create the subcontract order — from the **sales order line** via **Create Subcontract Order**, from the **production order** via the subcontracting operation, or manually in **Subcontract Orders** (New action). The status is **Open**.
2. On the **Subcontract Order** page, check/complete the **order lines** and **groups** (item, quantity, price, and item charges if applicable).
3. Choose the **Release** action (status becomes **Released**).
4. Choose **Post Outbound** — confirm the **Post Outbound?** prompt; the outbound quantity is posted (status becomes **In Process**).
5. After the return delivery: choose **Post Inbound** — confirm the **Post Inbound?** prompt; the receipt is posted.
6. Choose **Post Invoicing** — confirm the **Post Invoicing?** prompt; the purchase invoice is created and the document can be set to **Invoiced**.

This sequence (**Release → Post Outbound → Post Inbound → Post Invoicing**) is the mandatory posting order; it is repeated with the same action names in the **Posting Flow** chapter and in the **Typical Use Cases**.

## Setup

Setup is performed **once** by the **administrator** or **key user** before first use. All settings are located centrally on **one** page: **Subcontract Order Setup**.

**Entry point:** Open **Search** and call up **Subcontract Order Setup**. This is a company-wide single-record setup (`UsageCategory = Administration`); on first opening, the system creates the setup record automatically. Since there is no parent list, **Search** is the intended entry point here.

The page is divided into the **No. Series**, **Reports**, and **Production** tabs. The following table documents all fields the administrator can maintain.

| Setup | Explanation |
|---|---|
| **Subcontract Order Nos.** (No. Series tab) | If a number series is entered here, the system automatically assigns the next **No.** from this series when each new subcontract order is created. Without an entry, no document can be created — document creation aborts with a note about the missing field. |
| **Subcontract Order** (Reports tab) | If a report ID is entered here, the user can run the **Subcontract Order** action (Reports area) on the document and print the order as a document for the vendor. Without an entry, printing is not possible (the system checks the field when called). |
| **Subcontract Shipment** (Reports tab) | If a report ID is entered here, the user can print the shipment note for the goods going out to the vendor via the **Subcontract Shipment** action. Without an entry, printing is not available. |
| **Subcontract Pick Up** (Reports tab) | If a report ID is entered here, the user can print the pickup document via the **Pickup Document** action. Without an entry, the call aborts with a field check. |
| **No Calc. Prod. Order for Group** (Production tab) | Controls how the production order is created from a group. If enabled, the system creates a production order line directly on **Create Prod. Order** without running the "Refresh Production Order" report — faster, but without automatic component/routing explosion. If not enabled, the production order is fully calculated via "Refresh Production Order" (components and routing are exploded). |

The system field **Primary Key** (technical single-record key) is not maintainable in a visible way and is therefore not documented.

### Setting Up the Number Series

**Process entry point:** The administrator configures the document numbering before the first order creation. The operational user later consumes this setting in **Subcontract Orders → New** or **Create Subcontract Order** (see **Daily Work**).

1. Open **Search** → **Subcontract Order Setup**.
2. In the **No. Series** tab, select a number series in the **Subcontract Order Nos.** field. When set, every new document draws its **No.** automatically from this series; the series must match the intended manual or automatic assignment.
3. Result in the daily flow: When a subcontract order is created, the document immediately receives a unique **No.**; an associated **No. Series** field is logged read-only on the document.

### Setting Up Reports

**Process entry point:** The administrator enters the print reports before documents are sent to vendors. The settings are consumed in the **Reports** area on the document page (see **Daily Work → Printing Reports**).

1. Open **Search** → **Subcontract Order Setup** → **Reports** tab.
2. Enter a report ID for **Subcontract Order**, **Subcontract Shipment**, and **Subcontract Pick Up** respectively. If a field is filled, the associated print action on the document becomes active; if it is empty, the system checks the field when called and prevents printing.
3. Result in the daily flow: The user can print the order, the shipment note, and the pickup document directly from the subcontract order.

### Permissions

The permission set **All permissions** (object "MuM FO Permission") bundles read/write rights on all tables (subcontract order header, line, group line, group charge, group description, entry, setup) as well as execution rights on the module's pages and codeunits. The administrator assigns this set to users; it determines which actions users may perform in the module (create, post, invoice). Without this set, a user cannot open the subcontract order pages.

**License:** The module checks the license at logon via **m+m Cloud Base**. If no valid license is present, the functions are not available; this concerns only the administrator during provisioning.

## Master Data and Prerequisites

The module does **not** bring its own master data cards; it builds on **standard master data** of Business Central. Before first use, the administrator or key user prepares the following data, because the subcontract order checks it during creation and posting.

**Work center with vendor:** Subcontracting requires at least one **work center** whose **Vendor** field (Subcontractor No.) is filled. If the field is filled, the module recognizes the work center as a subcontracting work center: When creating from the sales order line, the system offers only such work centers for selection, and when a production operation is created at this work center, the matching order line in the subcontract order is added automatically. The **Work Center No.** field in the header refers to this work center.

**Vendor:** The **Cust./Vendor No.** entered in the header is the subcontractor. When the vendor is set, the document adopts name, address, contact, **Language Code**, and **Payment Terms Code** from the vendor master and proposes the **Ship-To Address**.

**Item and production order/routing:** For material-related groups and order lines, maintained **items** (with base unit) are required and — for production-based processes — a **production order** with a **routing** whose operation refers to the subcontracting work center. If the operation is missing, the system reports "For one or more lines a Prod. Order Routing Operation is missing!" on outbound.

## Overview: Subcontract Orders

**Entry point:** **Search** → **Subcontract Orders**. The list is the central work overview (`UsageCategory = Lists`); a double-click opens the **Subcontract Order** document.

The list is read-only and shows one subcontract order per line. The columns give a quick overview of vendor, dates, and status.

| Field | Explanation |
|---|---|
| **No.** | Unique document number of the subcontract order from the number series. |
| **Cust./Vendor No.** | Number of the subcontractor to whom the processing is outsourced. |
| **Cust./Vendor Name** / **Cust./Vendor Name 2** | Name of the vendor; updates with the vendor selection in the header. |
| **Cust./Vendor Address** / **Cust./Vendor Address 2** | Street/address supplement of the vendor. |
| **Cust./Vendor City** | City of the vendor. |
| **Cust./Vendor Post Code** | Post code of the vendor. |
| **Cust./Vendor Country/Region Code** | Country/region of the vendor. |
| **Document Date** | Creation date of the document (proposal: work date). |
| **Status** | Processing state of the order (see values below). |
| **Outbound Location Code** | Location from which the goods go out to the vendor. |
| **Outbound Date** | Planned/used date of the outbound shipment to the vendor. |
| **Inbound Date** | Planned/used date of the receipt from the vendor. |
| **Your Reference** | Free reference field of the user. |
| **External Document No.** | Document number of the vendor for the order. |
| **Prod. Order Job Status** | Production progress of the underlying production order (see values below). |

**Status** (option, each value controls the permitted follow-up actions):

- **Open:** Document in progress; lines, groups, and item charges are editable; posting is not yet possible. Only from **Open** is **Release** allowed.
- **Released:** Document committed; lines are locked. From this status, **Post Outbound** is possible.
- **In Process:** The outbound has been (partially) posted; the document is in ongoing outbound/inbound and invoicing. **Post Inbound** and **Post Invoicing** are only possible in this status.
- **Invoiced:** All quantities/amounts to be invoiced are posted; the process is complete.
- **Canceled:** The order was canceled. (The associated action is hidden by default.)

**Prod. Order Job Status** (option, read-only; reflects the production progress):

- **Open:** The associated production operation has not yet been started.
- **Started:** The production of the operation is running.
- **Interrupted:** Production is interrupted.
- **Partly Finished:** The operation is partly reported as finished.
- **Finished:** The operation is completely reported as finished.

## Daily Work on the Subcontract Order

The **Subcontract Order** document page is the central work surface. It controls its behavior via the settings maintained on **Subcontract Order Setup** (number series for the **No.**, report IDs for the print actions). The document is divided into the **header** (**General**, **Outbound & Inbound**, **Ship-To Address**, **Informations** tabs), the **Lines** subpage (order lines), and the **Groups** subpage.

**Entry point:** from **Subcontract Orders** via line drill-down, or from the **sales order** via the sales order line with the action **Show Subcontract Order** / **Create Subcontract Order**. The document page itself is not reachable via **Search** (`UsageCategory = None`).

### Header (General tab)

| Field | Explanation |
|---|---|
| **No.** | Document number; drawn from the number series when created. Via the assist-edit, a connected number series can be selected before the first assignment. |
| **Cust./Vendor No.** | Subcontractor. When set, the system fills name, address, contact, **Language Code**, **Payment Terms Code**, and the **Ship-To Address** from the vendor master. |
| **Cust./Vendor Name** / **Cust./Vendor Name 2** | Name of the vendor (adopted from the master, can be overwritten). |
| **Sell-to Contact** | Contact of the vendor; the selection offers only contacts of the vendor. |
| **Sell-to Contact** (Name) | Display name of the selected contact. |
| **Cust./Vendor Address** / **Cust./Vendor Address 2** | Street and supplement of the vendor. |
| **Cust./Vendor City** / **Cust./Vendor Post Code** / **Cust./Vendor Country/Region Code** / **Cust./Vendor County** | Address components of the vendor; city and post code are checked against the post code table. |
| **Document Date** | Creation date; the proposal is the work date. |
| **Outbound Date** | Date of the outbound shipment to the vendor. When set, **Posting Date (Outbound)** is preset at the same time. |
| **Inbound Date** | Date of the receipt. When set, **Posting Date (Inbound)** is preset at the same time. |
| **Promised Inbound Date** | Return delivery date promised by the vendor. |
| **Order Confirmation Date** | Date of the vendor's order confirmation. |
| **Order Conf. Comment** | Free-text comment on the order confirmation. |
| **Posting Date (Outbound)** | Posting date for the outbound shipment; mandatory for **Post Outbound**. |
| **Posting Date (Inbound)** | Posting date for the receipt; mandatory for **Post Inbound**. |
| **Posting Date (Invoicing)** | Posting date for the invoicing; mandatory for **Post Invoicing**. |
| **Payment Terms Code** | Payment term for the resulting purchase invoice. |
| **Status** | Processing state (read-only; set via the actions; see values in the Overview chapter). |
| **Language Code** | Language of the vendor for document printing/communication. |
| **Your Reference** | Free reference of the user. |
| **External Document No.** | Document number of the vendor. |
| **External Invoice No.** | External invoice number; controls the grouping of item charges per invoice during invoicing. |

### Header: Outbound & Inbound

| Field | Explanation |
|---|---|
| **Outbound Location Code** | Location from which the goods go out to the vendor. When set, the generated purchase order uses this location. |
| **Outb. Ship. Agent Code** | Shipping agent for the outbound. When changed, the Outb. Ship. Agent Service Code is reset. |
| **Outb. Ship. Agent Service Code** | Shipping agent service of the outbound agent (dependent on the Outb. Ship. Agent Code). |
| **Outb. Ship. Method Code** | Shipment method of the outbound. |
| **Inbound Location Code** | Location at which the returned goods are received. |
| **Inb. Ship. Agent Code** | Shipping agent for the inbound. When changed, the Inb. Ship. Agent Service Code is reset. |
| **Inb. Ship. Agent Service Code** | Shipping agent service of the inbound agent (dependent on the Inb. Ship. Agent Code). |
| **Inb. Ship. Method Code** | Shipment method of the inbound. |

### Header: Ship-To Address

| Field | Explanation |
|---|---|
| **Ship-To No.** | Reference to an alternate ship-to address. |
| **Ship-To Name** / **Ship-To Name 2** | Name of the ship-to location at the vendor. |
| **Ship-To Address** / **Ship-To Address 2** | Street and supplement of the ship-to location. |
| **Ship-To City** / **Ship-To Post Code** / **Ship-To Country/Region Code** / **Ship-To County** | Address of the ship-to location; city/post code are checked against the post code table. |

### Header: Informations

| Field | Explanation |
|---|---|
| **Purchase Order No.** | Number of the purchase order managed in the background (read-only); created when the order is generated and carries the receipt and invoice. |
| **Outbound Posted** | Flag (read-only). When set, the outbound shipment has already been posted; releasing again leads directly to the **In Process** status. |
| **Inbound Posted** | Flag (read-only). When set, the receipt is posted. |
| **Invoiced** | Flag (read-only). When set, all positions to be invoiced are invoiced. |

### Order Lines

The **Lines** subpage shows the order lines of **Line Type Order** — the concrete source positions (production order/sales order) that are subcontracted.

| Field | Explanation |
|---|---|
| **Group Line No.** | Assigns the order line to a **group**. When changed, the line is included in the relevant group by quantity and value. |
| **Prod. Order Status** | Status of the source production order (values: **(blank)**, **Planned**, **Firm Planned**, **Released**, **Finished**). Only with **Released** are outbound/production-relevant follow-up actions possible. |
| **Prod. Order No.** | Number of the source production order. |
| **Prod. Order Line No.** | Line number in the source production order. When set, the matching operation number is determined automatically. |
| **Prod. Order Operation No.** | Operation of the production order at the subcontracting work center; controls the later output posting of the operation. |
| **Work Center No.** | Subcontracting work center (vendor) of the line. |
| **Sales Order No.** | Source sales order (if the subcontracting originates from sales). |
| **Sales Order Line No.** | Line number in the source sales order. |
| **Item No.** | Item to be processed. |
| **Variant Code** | Item variant (hidden by default). |
| **Description** / **Description 2** | Item description. |
| **Quantity** | Quantity to be processed for the line. When changed, the record is saved immediately and included in the group. |
| **Promised Delivery Date** | Date promised by the vendor (hidden by default). |
| **Purchase Order No.** / **Purchase Order Line No.** | Link to the purchase order line (hidden by default). |

Line actions:

- **Create Prod. Order:** Creates a production order from the order line (status selection **Planned**/**Firm Planned**/**Released**); then sets the source information in the line.
- **Show Prod. Order:** Opens the linked production order in the matching status.
- **Show Sales Order:** Opens the linked sales order.
- **Split Line:** Splits a line by quantity (prompt **Split Line?**; action hidden by default).

### Groups

The **Groups** subpage bundles the positions to be outsourced by quantity and value. Here the user controls the quantities to be issued, received, and invoiced, as well as prices and item charges.

| Field | Explanation |
|---|---|
| **Line No.** | Internal number of the group. |
| **Item No.** | Item of the group. When set, description and base unit are adopted from the item. |
| **Variant Code** | Item variant (hidden by default). |
| **Description** / **Description 2** | Item description of the group. |
| **Quantity** | Total quantity of the group. When set, **Amount** (= Quantity × Price) and the item charges are recalculated. |
| **Outbound Qty.** | Quantity that goes out to the vendor on the next **Post Outbound**. |
| **Posted Outbound Qty.** | Already posted outbound quantity (read-only). When increased, the open **Inbound Qty.** is updated automatically. |
| **Inbound Qty.** | Quantity that is posted back on the next **Post Inbound**. |
| **Posted Inbound Qty.** | Already posted inbound quantity (read-only). When increased, the open **Qty. To Invoice** is updated automatically. |
| **Qty. To Invoice** | Quantity that is invoiced on the next **Post Invoicing**. When set, **Amount To Invoice** (= Qty. To Invoice × Price) is calculated. |
| **Qty. Invoiced** | Already invoiced quantity (read-only). |
| **Price** | Processing price per unit. When changed, Amount and Amount To Invoice are recalculated. |
| **Amount** | Total amount of the group (Quantity × Price). |
| **Amount To Invoice** | Amount to be invoiced. When set manually, **Fixed Amount To Invoice** is activated and the amount remains unchanged on quantity changes. |
| **Fixed Amount To Invoice** | Flag. When set, the entered invoicing amount stays fixed and is not overwritten from Quantity × Price. |
| **Invoiced Amount** | Already invoiced amount (read-only). |
| **Item Charges** | Flag (read-only). When set, item charge lines exist for this group. |
| **Charge Amount** | Sum of the group's item charges (read-only, hidden by default). |
| **Total Amount** | Amount plus Charge Amount (read-only). |
| **Total Invoiced Amount** | Invoiced amount including item charges (read-only). |
| **Source Type** | Source of the group (values: **(blank)**, **Prod. Order**, **Purchase Order**, **Purch. & Prod. Order**). Determined automatically from the set source documents. |
| **Source Vendor No.** | Vendor of the source purchase order (for material-related procurement). |
| **Source Purch. Order No.** / **Source Purch. Order Line No.** | Linked source purchase order. |
| **Source Purch. Or. Proc.-Status** | Procurement progress of the source purchase order (**(blank)**, **In Process**, **Partly Received**, **Received**). |
| **Source Prod. Order Status** | Status of the source production order (**(blank)**, **Planned**, **Firm Planned**, **Released**, **Finished**). |
| **Source Prod. Order No.** / **Source Prod. Order Line No.** | Linked source production order. |
| **Source Prod. Ord. Proc.-Status** | Production progress of the source (**(blank)**, **In Process**, **Partly Produced**, **Produced**). |
| **Assigned Lots/Serials** | Number of assigned lots/serial numbers (read-only). Via the drill-down, the **Lot/Serial Lines** list opens. |

Group actions:

- **Item Charges:** Opens the item charge lines of the group (see H3 below).
- **Ext. Description:** Opens the extended description text of the group (see H3 below).
- **Create Purchase Order:** Creates a source purchase order at the **Source Vendor No.** for material procurement (mandatory fields Source Vendor No. and Item No.).
- **Show Purchase Order:** Opens the linked source purchase order.
- **Create Prod. Order:** Creates a production order for the group (status selection **Planned**/**Firm Planned**/**Released**); with or without a calculation run depending on the **No Calc. Prod. Order for Group** setup.
- **Show Prod. Order:** Opens the linked production order.

#### Item Charges

**Process entry point:** The operational user maintains item charges (e.g. setup, transport, or minimum-quantity surcharges) per group so that they arise as additional invoice positions during invoicing. Call: In **Groups**, select the line and choose the **Item Charges** action.

| Field | Explanation |
|---|---|
| **Charge No.** | Item/G-L reference of the item charge (Item Charge). |
| **Description** | Designation of the item charge. |
| **Price** | Price per unit of the item charge. |
| **Charge Unit of Measure** | Unit of the item charge (hidden by default). |
| **Qty. per Item Unit of Measure** | Conversion quantity per item unit (hidden by default). |
| **Allocation Base** | Basis for determining the amount. Values: **(blank)**, **Quantity**, **Quantity (KG)**, **Quantity (Pcs.)**, **Quantity (Meter)**, **Lump-Sum**. **(blank)/Quantity:** Amount = Quantity × Price; **Quantity (KG)/Quantity (Pcs.)/Quantity (Meter):** reference to the respective physical quantity; **Lump-Sum:** fixed amount independent of the quantity (hidden by default). |
| **Amount** | Calculated item charge amount. |
| **Amount To Invoice** | Portion of the item charge to be invoiced. |
| **Invoiced Amount** | Already invoiced portion (read-only). |
| **Payment Terms Code** | Payment term of the item charge; controls the grouping per invoice (hidden by default). |
| **External Invoice No.** | External invoice number of the item charge; controls the invoice grouping (hidden by default). |
| **Gen. Prod. Posting Group** | Gen. product posting group for the posting (hidden by default). |
| **VAT Prod. Posting Group** | VAT product posting group (hidden by default). |
| **Tax Group Code** | Tax group (hidden by default). |

Note: The system does not allow different **Payment Terms Codes** or **posting groups** for the same reference and reports this on entry.

#### Ext. Description

**Process entry point:** The user enters longer description texts for the group (e.g. processing instructions for the vendor). Call: In **Groups**, the **Ext. Description** action.

| Field | Explanation |
|---|---|
| **Text** | Free-text line(s) of the extended description; appears on the associated documents/printouts. If at least one text is entered, the **Ext. Description** flag is set on the group. |

#### Lot/Serial Lines

**Process entry point:** Shows the lots or serial numbers assigned to the group. These lines (line type **Lot/Serial**) arise automatically from the item ledger entries of production or the receipts; the user calls them via the drill-down in the **Assigned Lots/Serials** field in the group. The list is read-only.

| Field | Explanation |
|---|---|
| **Item No.** | Item of the lot/serial number. |
| **Variant Code** | Variant of the item. |
| **Description** / **Description 2** | Item description. |
| **Lot No.** | Assigned lot. |
| **Serial No.** | Assigned serial number. |
| **Quantity** | Quantity of the assigned lot/serial number. |

### Printing Reports

From the **Reports** area of the document, the user prints the configured documents:

- **Subcontract Order** — the order as a document for the vendor.
- **Subcontract Shipment** — the shipment note for the outbound goods.
- **Pickup Document** — the pickup document.

Each action checks whether the associated report ID is entered in the setup; if it is missing, printing is not possible (see **Setting Up Reports**).

## Posting Flow

The subcontract order runs through a fixed sequence of status and posting actions. The user finds these actions in the **Release** and **Post** areas of the document.

1. **Create and enter (status Open):** Enter the header, order lines, and groups; set quantities (**Outbound Qty.**), prices, and item charges if applicable.
2. **Release:** Action **Release**. Sets the status from **Open** to **Released** (only possible from **Open**). The lines are locked afterward. If an outbound has already been posted, releasing again leads directly to **In Process**.
3. **Post Outbound:** Action **Post Outbound**. Confirm the **Post Outbound?** prompt. Prerequisite: status **Released** or **In Process**, a filled **Posting Date (Outbound)**, and at least one group with a non-zero **Outbound Qty.** (otherwise "Nothing to post!"). The system posts the outbound quantity, creates a subcontract order entry of **Entry Type Outbound**, increases **Posted Outbound Qty.**, and sets the status to **In Process** and **Outbound Posted** = yes.
4. **Post Inbound:** Action **Post Inbound**. Confirm the **Post Inbound?** prompt. Prerequisite: status **In Process**, a filled **Posting Date (Inbound)**, and at least one group with a non-zero **Inbound Qty.** The system posts the receipt of the purchase order managed in the background, creates an entry of **Entry Type Inbound** (Posted Document Type **Shipment**), and updates **Posted Inbound Qty.** If a group has been fully received, the associated **Prod. Order operation** is reported as **Finished** automatically.
5. **Post Invoicing:** Action **Post Invoicing**. Confirm the **Post Invoicing?** prompt. Prerequisite: a filled **Posting Date (Invoicing)** and an open **Qty. To Invoice** or an open **Amount To Invoice** (for item charges). The system posts one purchase invoice per **External Invoice No.** and **Payment Terms Code**, creates entries of **Entry Type Invoicing**, and then asks **Set Subcontract Order Status to "Invoiced"?**. For already invoiced documents, **Subcontract Order already invoiced. Continue invoicing?** appears additionally.
6. **Completion/correction:** Via **Invoiced**, the document is set to **Invoiced** manually; via **Reopen**, it returns to **Open** (only from **Released**, **In Process**, or **Invoiced**). The **Cancel** action (status **Canceled**) is hidden by default.

**Partial quantities:** Outbound and inbound as well as invoicing are **partial-quantity capable**. The user can post in several runs; the system updates the open quantities (Inbound Qty., Qty. To Invoice) automatically after each posting. There is no requirement to close the document only when the quantities are fully balanced.

## History: Subcontract Order Entries

**Entry point:** On the **Subcontract Order** document, the **Entries** action. The **Subcontract Order Entries** list logs every outbound, inbound, and invoicing process read-only.

| Field | Explanation |
|---|---|
| **Entry No.** | Consecutive entry number. |
| **Document No.** | Subcontract order to which the entry belongs. |
| **Document Group Line No.** | Affected group. |
| **Entry Type** | Process type. **Outbound:** outbound shipment to the vendor; **Inbound:** receipt from the vendor; **Invoicing:** invoicing. |
| **Posting Date** | Posting date of the process. |
| **Quantity** | Posted quantity. |
| **Posted Document Type** | Type of the created posted document. **(blank):** no posted document; **Shipment:** posted receipt; **Invoice:** posted purchase invoice. |
| **Posted Document No.** | Number of the created posted document. |
| **Purchase Order No.** | Associated purchase order. |
| **Posting No.** | Internal posting run number (bundles entries that belong together). |
| **Invoice Type** | Type of the invoicing position. **(blank):** no invoicing; **Group Line:** invoicing of a group quantity; **Charge:** invoicing of an item charge. |
| **Invoiced Amount** | Invoiced amount of the entry. |
| **Invoiced Amount Fixed** | When set, the invoice amount was fixed manually and not derived from Quantity × Price. |
| **Invoiced Charge Amount** | Invoiced item charge portion. |
| **External Invoice No.** | External invoice number of the vendor. |
| **Payment Terms Code** | Payment term of the invoicing entry. |

Action **Show Posted Document:** Depending on the **Posted Document Type**, opens the **Posted Purchase Receipt** (Shipment) or the **Posted Purchase Invoice** (Invoice).

## Typical Use Cases

### Case 1: Subcontracting from a Sales Order

**Trigger:** A customer orders an item whose processing (e.g. coating, hardening) is to be outsourced to an external subcontractor. Sales has already entered the sales order.

**Entry point in BC:** The user opens the **sales order**, selects the relevant line in the sales order lines, and chooses the action **Create Subcontract Order**. If no subcontracting work center is specified yet, the system offers the work centers with an entered vendor for selection.

**Core flow:**

1. The system creates a **subcontract order** (status **Open**), adopts the vendor (from the work center), item, quantity, and the link to the sales order into the **order line**.
2. On the document, the user completes the **groups** (quantity, price, item charges if applicable) as well as **Outbound Date**/**Inbound Date** and locations.
3. Action **Release** (status **Released**).
4. Action **Post Outbound** → confirm the **Post Outbound?** prompt (status **In Process**).
5. After the return delivery, action **Post Inbound** → confirm the **Post Inbound?** prompt.
6. Action **Post Invoicing** → confirm the **Post Invoicing?** prompt; then confirm **Set Subcontract Order Status to "Invoiced"?**.

**Completion:** Via **Entries**, the user checks the resulting subcontract order entries (outbound, inbound, invoicing) and opens the posted purchase invoice via **Show Posted Document**. Optionally, they print **Subcontract Shipment** and **Pickup Document** beforehand.

### Case 2: Subcontracting Operation from a Released Production Order

**Trigger:** In a released production order, an operation is entered at a work center whose **Vendor** field is filled — this operation is performed externally.

**Entry point in BC:** When creating or changing the production operation at the subcontracting work center, the module automatically adds the matching **order line** in the subcontract order (or creates a new subcontract order if needed). The user opens the document via **Subcontract Orders** or from the production order line.

**Core flow:**

1. In the **Groups**, the user checks the quantity and the **Price** of the processing; for material provisioning, they create the source documents via **Create Purchase Order** or **Create Prod. Order**.
2. The user sets the **Outbound Qty.**, releases the document via **Release**, and posts the outbound shipment to the vendor with **Post Outbound**.
3. After output posting and return delivery, they post the receipt with **Post Inbound**; the module reports the associated **Prod. Order operation** as **Finished** automatically upon complete receipt (visible in the **Prod. Order Job Status**).
4. With **Post Invoicing**, the purchase invoice for the processing service is created.

**Completion:** The progress can be read from **Source Prod. Ord. Proc.-Status** (Partly Produced/Produced) and from the **Status** of the document; the entries are located in **Subcontract Order Entries**.

## FAQ and Troubleshooting

### Why can't a new subcontract order be created?
In the **Subcontract Order Setup**, no number series is entered in the **Subcontract Order Nos.** field. Without this series, the **No.** cannot be assigned and creation aborts. The administrator enters the series (see **Setting Up the Number Series**).

### Why can I no longer change the lines?
As soon as the document reaches the **Released** (or **In Process**) status via **Release**, the header, order lines, and groups are locked; the system reports "Status must be 'Open'!". Via **Reopen**, the document returns to **Open**, after which editing is possible again.

### Why does "Nothing to post!" appear when posting?
There is no open quantity for the selected process: On **Post Outbound**, no **Outbound Qty.** is set in any group; on **Post Inbound**, no **Inbound Qty.**; and on **Post Invoicing**, neither **Qty. To Invoice** nor **Amount To Invoice**. The user enters the corresponding quantity in the group.

### Why can't I post the inbound?
**Post Inbound** requires the **In Process** status, which only arises from the prior **Post Outbound**. Additionally, the **Posting Date (Inbound)** must be filled. If the status is still **Released**, post the outbound first.

### What happens if an operation for the processing is missing?
On outbound, the system checks whether each order line is assigned to a released Prod. Order operation. If the assignment is missing, "For one or more lines a Prod. Order Routing Operation is missing!" or "No Prod. Order Routing Lines found!" appears. The user assigns **Prod. Order No.**, **Prod. Order Line No.**, and **Prod. Order Operation No.** correctly in the order line.

### Why is a group shown as "Produced" or "Received" even though I posted nothing?
The fields **Source Prod. Ord. Proc.-Status** and **Source Purch. Or. Proc.-Status** automatically reflect the progress of the source documents: On production output (item ledger entry "output"), the status switches to **Partly Produced**/**Produced**; on receipt of the source purchase order, to **Partly Received**/**Received**. These values are display fields and are maintained by the system.

### Why does my entered invoicing amount no longer change automatically?
As soon as **Amount To Invoice** is entered manually, the system activates **Fixed Amount To Invoice**. When this flag is set, the entered amount stays fixed and is not overwritten when quantity or price changes. To reset, remove the flag or re-validate the Qty. To Invoice.

### How are several invoices of one vendor invoiced separately?
During invoicing, the system groups the positions per **External Invoice No.** and **Payment Terms Code** into separate purchase invoices. If the user enters different external invoice numbers or payment terms in the groups or item charges, several invoices are created accordingly. For the same item charge reference, differing payment terms or posting groups are not allowed.

### Why do I find only some of the assigned lots/serial numbers?
The **Lot/Serial Lines** arise automatically from the item ledger entries of production (output) and the receipts. Only after the corresponding postings does the **Assigned Lots/Serials** counter in the group increase; via its drill-down, the complete list opens. Before posting, no lines exist yet.

### Why is there a purchase order number on the document that I did not create?
The module keeps a **purchase order** in the background for the receipt and the invoicing; its number appears read-only in the **Purchase Order No.** field. This order is managed automatically on posting and removed again when the subcontract order is deleted. Via **Show Purchase Order**, the user can view it.
