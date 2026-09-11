---
title: Anwenderhandbuch m+m Posting Options
---

# m+m Posting Options User Guide

## Introduction

The **m+m Posting Options** extension controls which **posting options** users are still allowed to select at all when posting a document. In the Microsoft Dynamics 365 Business Central standard, BC offers several options when posting a sales or purchase document (**Ship**, **Invoice**, **Ship and Invoice**). This extension makes it possible to restrict this offering company-wide, so that only the operationally desired options appear when posting.

Control is handled separately for three areas:

- **Sales (R) Order Posting Options** — sales orders and sales return orders,
- **Purch (R) Order Posting Options** — purchase orders and purchase return orders,
- **Whse. Shipment Posting Options** — warehouse shipments from the warehouse.

**Target audience:** This guide is aimed primarily at the **operational users** in sales, purchasing, and the warehouse who post documents daily and experience the restricted selection when posting. Secondarily, it concerns **administrators** and key users who maintain the single central setup page once.

**Brief process overview:** An administrator defines, per area, on the **Posting Option Setup** page which posting option is to apply. As soon as a user then triggers the **Post** action (or **Post and New** / **Post and Send**) in a sales order, a purchase order, or a warehouse shipment, the stored rule takes effect: instead of the full standard menu, only the configured selection appears, or the posting runs through directly without any prompt.

The extension adds **no** new fields to sales, purchase, or warehouse shipment documents, and creates **no** documents, lists, or posted history of its own. It has exactly **one** setup page; the entire effect unfolds within the existing posting dialog of the standard documents.

## Quick Start for Users

The fastest route to a result consists of a one-time setup and the subsequent daily use when posting.

**First — setup (one-time, by an administrator):**

1. Open the **Posting Option Setup** page. To do so, enter the term `Posting Option Setup` in the BC search (**Tell me**) and choose the link of the same name.
2. In the **Sales (R) Order Posting Options** field, set the desired restriction for sales.
3. In the **Purch (R) Order Posting Options** field, set the desired restriction for purchasing.
4. In the **Whse. Shipment Posting Options** field, set the desired restriction for the warehouse shipment.
5. Leave a field on **Standard** if the unchanged BC behavior is to apply in the respective area. The entries are saved immediately; no release or activation action is required.

**Then — daily use (by the operational users when posting):**

1. Open the document (e.g., **Sales Order**, **Purchase Order**, or **Warehouse Shipment**) and enter the lines as usual.
2. Trigger the posting via **Post**, **Post and New**, or **Post and Send**.
3. Instead of the full standard menu, only the selection stored in the setup appears:
   - With a single option, the posting is executed directly with that option (only one menu line).
   - With two permitted options, you choose between the two offered lines.
   - With **Standard**, BC behaves unchanged.
4. Confirm the selection; the document is posted accordingly.

## Setup

The entire configuration of the extension takes place on **one** company-wide page: **Posting Option Setup**. There is exactly one record per company; the page creates this record automatically the first time it is opened.

### Setting up Posting Options

**Who and when:** An administrator or key user performs this setup **once before the first productive use** and only adjusts it when operational requirements change. It applies **company-wide** for all users and all affected documents. The options set here later take effect when posting **sales orders/return orders**, **purchase orders/return orders**, and **warehouse shipments** (see the section **Daily Work: Posting with Restricted Options**).

**Prerequisite:** The **m+m Posting Options** extension must be installed in **Extension Management**. A number series, a location, or any other master data are **not** required — the page works with a single, automatically created setup record.

**Access:** Open the page via **Tell me** using the term `Posting Option Setup`. The page is set up as a company-wide administration page (category **Administration**) and has **no** parent list or master data card from which it would be opened; access via **Tell me** is therefore the intended and only route.

In the **General** area, three fields are available. Each field controls **one** document area independently of the others.

| Setup | Explanation |
|-------------|-------------|
| **Sales (R) Order Posting Options** | Defines which posting options are offered when posting a **sales order** or a **sales return order**. If a value other than **Standard** is selected, the extension replaces the standard menu when posting with the restricted selection defined here (for the values, see below). |
| **Purch (R) Order Posting Options** | Defines which posting options are offered when posting a **purchase order** or **purchase return order**. If a value other than **Standard** is selected, only the configured selection is shown when posting; in purchasing, "Ship" corresponds to the receipt of the order (for the values, see below). |
| **Whse. Shipment Posting Options** | Defines which posting options are offered when posting a **warehouse shipment**. If a value other than **Standard** is selected, the warehouse shipment is restricted to the configured selection when posting (for the values, see below). |

#### Values for Sales (R) Order and Purch (R) Order

Both fields have the same set of values. The effect applies exclusively to the **Order** and **Return Order** document types of the respective area.

- **Standard:** When set, the BC standard behavior remains unchanged; when posting, the full standard menu appears and the extension does not intervene.
- **Only Shipment:** When set, only **Ship** is offered when posting (in purchasing the receipt, in sales the shipment; for return orders the respective opposite goods movement). Only one menu line appears, so the document is shipped or received without any further choice — it is not invoiced.
- **Only Invoice:** When set, only **Invoice** is offered when posting. The document is only invoiced; no goods movement takes place via this option.
- **Only Ship and Invoice:** When set, only the combined option **Ship and Invoice** is offered when posting. Goods movement and invoicing occur in one step; a pure shipment or pure invoice is not selectable via this option.
- **Invoice/Ship and Invoice:** When set, **two** lines appear for selection when posting: **Invoice** or **Ship and Invoice**. The user decides case by case whether to only invoice or additionally ship.
- **Ship/Ship and Invoice:** When set, **two** lines appear for selection when posting: **Ship** or **Ship and Invoice**. The user decides case by case whether to only ship or additionally invoice.

> Note on return orders: The extension takes the document type into account automatically. In sales, "Ship" corresponds to the shipment for an order and to the return (receipt) for a return order; in purchasing, "Ship" corresponds to the receipt for an order and to the return shipment for a return order. In all cases, the menu line is labeled uniformly as **Ship** or **Invoice**.

#### Values for Whse. Shipment

The **Whse. Shipment Posting Options** field has a reduced set of values, because a pure invoice is not possible with a warehouse shipment.

- **Standard:** When set, the BC standard behavior of the warehouse shipment remains unchanged; the extension does not intervene.
- **Only Shipment:** When set, the warehouse shipment is only **shipped** when posting (warehouse shipment without invoice). Only one menu line appears.
- **Only Ship and Invoice:** When set, the warehouse shipment is posted together with the **invoice** when posting (shipment and invoice in one step).

**Setup sequence in order of dependency:**

1. **First**, install the extension in **Extension Management** (prerequisite).
2. **Then** open **Posting Option Setup** via **Tell me**; the setup record is created automatically the first time it is opened.
3. **Next**, set the desired value per area (**Sales (R) Order Posting Options**, **Purch (R) Order Posting Options**, **Whse. Shipment Posting Options**); each field takes effect immediately and independently.
4. **Finally**, the operational users verify the effect when posting in the respective document (see **Daily Work** and **Typical Use Cases**).

## Daily Work: Posting with Restricted Options

This section describes how the values set in **Posting Option Setup** affect everyday posting. Daily work is controlled exclusively via the setup page (see **Setting up Posting Options**); the extension makes no visible changes to the documents themselves.

The extension automatically intervenes in the posting process of the following documents:

- **Sales Order** and **Sales Return Order** — controlled by **Sales (R) Order Posting Options**,
- **Purchase Order** and **Purchase Return Order** — controlled by **Purch (R) Order Posting Options**,
- **Warehouse Shipment** — controlled by **Whse. Shipment Posting Options**.

### Posting Flow on the Sales and Purchase Document

1. Select the document (**Sales Order**, **Sales Return Order**, **Purchase Order**, or **Purchase Return Order**) and enter or review the lines.
2. Trigger the posting via one of the standard actions **Post**, **Post and New**, or **Post and Send**.
3. Before the actual posting, the extension checks the stored posting option of the area and replaces the standard selection menu:
   - **Standard** — the unchanged BC standard menu appears.
   - Single option (**Only Shipment**, **Only Invoice**, **Only Ship and Invoice**) — only the one permitted menu line appears; the posting is executed with that option.
   - Double option (**Invoice/Ship and Invoice**, **Ship/Ship and Invoice**) — two lines appear; you choose the desired one.
4. If the selection is canceled (no entry chosen), the posting is **not** executed.
5. Confirm the selection; the document is posted accordingly.

### Posting Flow on the Warehouse Shipment

1. Open the **Warehouse Shipment** and select the lines to be posted.
2. Trigger the posting of the warehouse shipment.
3. The extension replaces the selection menu according to **Whse. Shipment Posting Options**:
   - **Standard** — unchanged BC behavior.
   - **Only Shipment** — the warehouse shipment is only shipped.
   - **Only Ship and Invoice** — the warehouse shipment is shipped and invoiced.
4. Confirm the selection; the warehouse shipment is posted accordingly.

## Permissions

The extension includes a permission set that bundles full access to the objects of the extension.

| Setup | Explanation |
|-------------|-------------|
| **All permissions** (permission set **MuM PV All Perm.**) | Determines the permissions for the objects of the extension. When this set is assigned to a user or a user group, that user can open the **Posting Option Setup** page and read and edit the setup data. The permission set defines which actions users can perform on the setup data; without this assignment, the setup is not editable. |

Assign this permission set only to the people who are to manage the posting options (usually administrators or key users). For daily posting itself, the standard posting permissions of Business Central are sufficient; the extension takes effect automatically on every posting process, without the operational users needing a permission set of their own.

## Typical Use Cases

The following scenarios show how the extension works in everyday operations. Each flow begins with a trigger outside of Business Central and ends with the posted document.

### Restricting Sales to "Only Shipment"

1. **Trigger:** Sales management wants to prevent sales orders from being accidentally invoiced immediately, because the sales price is not finalized until later. Invoicing is to be carried out exclusively via a separate process.
2. **Entry in BC:** The administrator opens the **Posting Option Setup** page via **Tell me** and sets the **Sales (R) Order Posting Options** field to **Only Shipment**.
3. **Core flow:** A clerk enters a **Sales Order** and triggers **Post**. Instead of the full standard menu, only the **Ship** line appears. The posting ships the order without invoicing.
4. **Conclusion:** The order is shipped; a later invoice is created via the regular invoicing process. An accidental immediate invoice is ruled out.

### Setting Purchasing to "Only Ship and Invoice"

1. **Trigger:** In purchasing, receipt and invoice are always to be posted together, in order to avoid separate partial postings and the associated reconciliation effort.
2. **Entry in BC:** The administrator opens **Posting Option Setup** and sets **Purch (R) Order Posting Options** to **Only Ship and Invoice**.
3. **Core flow:** A purchasing clerk posts a **Purchase Order** via **Post**. Only the **Ship and Invoice** line appears; receipt and invoice are posted in one step.
4. **Conclusion:** The order is received and invoiced. Pure receipts without an invoice are no longer possible via this document.

### Letting Users in Sales Choose Between Two Options

1. **Trigger:** Sales is to remain flexible: in some cases only a shipment is made, in others the order is shipped and invoiced immediately. However, pure invoicing without a shipment is to be ruled out.
2. **Entry in BC:** The administrator sets the **Sales (R) Order Posting Options** field to **Ship/Ship and Invoice** in **Posting Option Setup**.
3. **Core flow:** When posting a **Sales Order**, exactly two lines appear: **Ship** and **Ship and Invoice**. The user selects the appropriate option depending on the situation.
4. **Conclusion:** Depending on the selection, the order is shipped or shipped and invoiced; the undesired "only invoice" option is not available.

## FAQ and Troubleshooting

### 1. Why does the full standard menu still appear when posting?

The area in question is set to **Standard** in **Posting Option Setup**. With **Standard**, the extension deliberately does not intervene and leaves posting to the BC standard. Set the appropriate field to a different value to restrict the selection.

### 2. How do I open the setup if I cannot find a menu entry?

The page has no parent list or card. Enter the term `Posting Option Setup` in the BC search (**Tell me**) and choose the link of the same name.

### 3. Do I have to save or release the setup after setting it?

No. The values are saved immediately. There is no release, activation, or posting action on the setup page; the new rule applies from the next posting process onward.

### 4. Why can I not create a second record in the setup?

The setup is company-wide and exists exactly **once** per company. Creating additional records and deleting the existing one are blocked; the single record is created automatically the first time it is opened.

### 5. Why can I not select the "Only Invoice" option for the warehouse shipment?

The **Whse. Shipment Posting Options** field only knows **Standard**, **Only Shipment**, and **Only Ship and Invoice**. A pure invoice is functionally not intended for a warehouse shipment and is therefore not selectable.

### 6. Why does "Ship" behave differently for a return order than for an order?

The extension takes the document type into account. For an order, "Ship" stands for the regular goods movement (sales: shipment, purchasing: receipt); for a return order, it stands for the opposite movement (sales: receipt of the return, purchasing: return shipment). The menu line is labeled uniformly as **Ship** in both cases.

### 7. What happens if I cancel the selection menu when posting?

If no line is selected, the posting process is aborted and nothing is posted. The document remains unchanged and can be posted again.

### 8. Does the restriction also apply to the "Post and New" and "Post and Send" actions?

Yes. The extension acts on the posting process itself. Regardless of whether you choose **Post**, **Post and New**, or **Post and Send**, the configured selection appears.

### 9. Does the setup apply only to certain users or to all?

The setup applies **company-wide** to all users. A user- or group-specific control of the posting options is not provided.

### 10. Which document types are affected by the sales or purchase setting?

Affected are exclusively the **Order** and **Return Order** document types of the respective area. Other document types (such as quotes or invoices as standalone documents) are not changed by the extension.
