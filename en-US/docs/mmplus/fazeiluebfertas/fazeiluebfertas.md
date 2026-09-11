---
title: Anwenderhandbuch m+m Production Order Overview with Production Order Assistant
---

# User Guide m+m Production Order Overview with Production Order Assistant

## Introduction

The m+m app "Production Order Overview with Production Order Assistant" is an extension for Microsoft Dynamics 365 Business Central. It connects two existing m+m modules with one another: the **Production Order Overview** (display of production order lines together with their associated sales lines) and the **Production Order Assistant** (creation of production orders directly from the sales document).

The purpose of this app is narrowly defined: it ensures that the **Production Order Overview** also shows those sales lines from which a production order was created via the **Production Order Assistant**. The Production Order Assistant calculates the quantity to be produced based on the information from the **Sales Order** or **Sales Quote** and not — as is otherwise customary in Business Central — via the **Reservation Entries**. Without this app, the overview would not link such production orders to their originating line, because no reservation entry establishes the connection.

**Target audience:** Primarily, the module is aimed at operational users in production control and sales who work daily with production orders and the triggering sales documents and who need to trace, in the overview, which sales transaction lies behind a production order line. Secondarily, it concerns administration, which provisions the app and its prerequisites once.

**Brief process overview:** A sales transaction (order or quote) triggers a production order via the **Production Order Assistant**. On the production order line the assistant records the reference fields **Prod. Target Type**, **Prod. Target No.** and **Prod. Target Line No.**. In the **Production Order Overview** the user selects a production order line; the subordinate **Sales Lines** view then displays the linked sales line — even when no reservation exists. From there, **Show Document** takes you to the respective document.

## Quick Start for Users

The shortest way to find the triggering sales transaction for a production order line:

1. Open the **Production Order Overview** list via **Tell Me**.
2. Select the desired production order line in the list.
3. Read off the **Sales Lines** view in the lower area. There, the sales line from which the production order was created appears — for orders created via the **Production Order Assistant**, even without a reservation entry.
4. In **Sales Lines**, choose the **Show Document** action to open the associated **Sales Order** or **Sales Quote**.
5. Alternatively, use **Show Document** on the production order line to open the associated **Production Order** and check the fields **Prod. Target Type**, **Prod. Target No.** and **Prod. Target Line No.** in the lines there.

The prerequisite is that the production order was previously created from a sales document via the **Production Order Assistant** (see **Typical Use Cases**). No further settings are required for this app itself.

## Prerequisites and Setup

This app is purely a linkage and brings with it no setup page, no number series, and no master data of its own. It only takes effect once its building blocks are present and ready for use.

### Provision the Dependent Modules

The app requires three m+m modules that must be installed and licensed before use:

1. First, **m+m Production Order Overview** must be present. When this module is installed, the **Production Order Overview** list with the subordinate **Sales Lines** view is available.
2. Next, **m+m Production Order Assistant** must be installed. When this module is active, the **Production Order Assistant** can create production orders from the sales document and set the reference fields **Prod. Target Type**, **Prod. Target No.** and **Prod. Target Line No.** on the production order line.
3. Additionally, the base module **m+m Cloud Base** is required. It provides fundamental technical functions and has no user interface of its own in this process.

If all three modules are present, the present linkage app takes effect automatically — without any further activation. There is no switch that a user or administrator would have to set.

### Production Order Assistant Setup (in the Upstream Module)

In order for production orders with reference fields to be created at all, which this app can evaluate, administration configures the Production Order Assistant once. This setup belongs to the **m+m Production Order Assistant** module and is described in detail there; for the present process, the following categories are primarily relevant:

- the production order status into which a production order created from a **Sales Order** or **Sales Quote** is transferred,
- the default value of the **Create Prod. Order** indicator in the sales line,
- whether a production order is created automatically when a sales order is released.

When these settings are configured, the Production Order Assistant creates production orders with populated reference fields; it is precisely these reference fields that the present app evaluates in order to display the sales line in the overview. Open the associated setup page **Production Order Assistant Setup** via **Tell Me**.

### Permissions

The app includes the permission set **All permissions** (object name `MuM PLPA Permission`). When you assign this permission set to a user or a user group, the person concerned receives the execution rights for the linkage logic of this app. The permission set determines which actions a user may perform within this extension and thereby governs the technical access to the linkage function. For the mere display of the **Sales Lines** in the **Production Order Overview**, the permissions of the upstream modules as well as the standard permissions for production and sales documents are additionally required.

## How the Linkage Works

This section explains what the app does in the background, so that users can correctly interpret the display in the **Production Order Overview**. The control is fully automatic; there is no additional user interface.

### Starting Point in the Production Order Overview

The **Production Order Overview** list shows production order lines. For each selected line, the subordinate **Sales Lines** view displays the associated sales lines. In the standard logic of the overview, Business Central determines these sales lines via the **Reservation Entries** or the item entries — that is, via a quantity-based reservation between sales demand and production.

Production orders that the **Production Order Assistant** creates directly from a sales document, however, calculate their quantity from the information of the sales transaction and not via reservation entries. For such orders there is therefore not necessarily a reservation entry that connects the sales line with the production. Without the present app, the **Sales Lines** view would remain empty in this case.

### What the App Adds

The app recognizes the reference fields set by the Production Order Assistant on the production order line and marks the named sales line in addition to the standard logic. Three fields of the production order line are decisive:

| Field | Explanation |
|------|-------------|
| **Prod. Target Type** | When this field is populated, the production order originates from a sales transaction and the app displays the associated sales line. The value determines in which document type the app searches for the line: **Sales Order** — the app searches for the line in the sales order; **Sales Quote** — the app searches for the line in the sales quote. If the field is empty, there is no reference from the Production Order Assistant and the display follows solely the standard logic via reservation entries. |
| **Prod. Target No.** | When this field is populated, it refers to the document number of the triggering **Sales Order** or **Sales Quote**; the app uses this number to select exactly the correct document in the **Sales Lines** view. |
| **Prod. Target Line No.** | When this field is populated, it refers to the specific line number within the sales document; only this makes the exact originating line, and not just the document, appear in **Sales Lines**. |

The three fields are set by the Production Order Assistant and are not manually editable on the production order line. If all three are populated, the app marks the matching sales line and presents it in the overview. If the **Prod. Target Type** is empty, only the reservation-based standard logic takes effect.

### The "Sales Lines" View

The subordinate **Sales Lines** view is read-only and serves for information. It shows the key commercial data of the linked sales line — in particular the associated customer, the document reference (document type and document number), the quantities, and the outstanding quantity as standard data of the sales line. The following column is added from the upstream module:

| Field | Explanation |
|------|-------------|
| **Sell-to Customer Name** | Shows the name of the customer of the sales line. When you go through several production order lines, you can thereby recognize, without an additional document call, for which customer the respective production is intended. |

Via the view, actions are available to continue working from the sales line:

- **Show Document** — opens the associated sales document (**Sales Order** or **Sales Quote**).
- **Reservation Entries** — shows the reservation entries for the sales line.
- **Item Tracking Lines** — opens the item tracking of the sales line.

### Actions of the Production Order Overview

At the level of the production order line, the **Production Order Overview** offers the following actions (from the upstream module) that facilitate the transition to further processing:

- **Show Document** — opens the production order in the matching status.
- **Change Status** — starts the status change of the production order.
- **Components** — opens the production order components of the line.
- **Prod. Journal** — opens the production journal (only for a released production order).
- **Routing** — opens the routing of the production order.

## Typical Use Cases

The following examples show the end-to-end process from the triggering event to the evaluation in the **Production Order Overview**. All screens and actions correspond to the existing modules; the present app ensures in each case that the sales line becomes visible in the overview.

### Use Case 1: Trace a Production Order from a Sales Order

**Trigger:** A customer calls and asks about the delivery date for an ordered, manufactured item. Production control wants to quickly check which production order belongs to this sales order.

**Entry point in BC:** The production order was created beforehand: in the **Sales Order**, the **Create Prod. Order** indicator was set on the relevant line and a production order was created via the **Production Order Assistant** action. In the **Production Order Assistant**, quantity, routing, **Due Date** and **Components** were checked and confirmed with **OK**. In doing so, the assistant set **Prod. Target Type** = **Sales Order** on the production order line, along with the associated **Prod. Target No.** and **Prod. Target Line No.**.

**Core process:**

1. Open the **Production Order Overview** via **Tell Me**.
2. Select the relevant production order line.
3. In the **Sales Lines** view, read off the linked order line with the customer (**Sell-to Customer Name**), document reference and quantities.
4. Choose **Show Document** to open the **Sales Order** directly and inform the customer of the status.

**Conclusion:** The relationship between production and sales order is documented without a manual search; no further postings are required in this app.

### Use Case 2: Check a Production Order from a Sales Quote

**Trigger:** An internal note requests the review of a production order that has already been prepared on the basis of a still-open **Sales Quote**. Because no order exists yet, there is typically no reservation entry.

**Entry point in BC:** The production order was previously created from the quote line via the **Production Order Assistant** action. The assistant set **Prod. Target Type** = **Sales Quote** as well as **Prod. Target No.** and **Prod. Target Line No.**.

**Core process:**

1. Open the **Production Order Overview** via **Tell Me**.
2. Select the production order line for the quote.
3. In the **Sales Lines** view, the quote line appears — even though no reservation entry exists, because the app evaluates the reference fields.
4. If needed, open the **Sales Quote** with **Show Document**.

**Conclusion:** The review is complete; the origin of the production order from the quote is clearly documented.

## FAQ and Troubleshooting

### 1. Why do I not see a line in the "Sales Lines" view, even though a production order exists?

The sales line is only displayed if either a reservation entry establishes the connection or the production order line contains the reference fields of the Production Order Assistant. Check whether **Prod. Target Type**, **Prod. Target No.** and **Prod. Target Line No.** are populated. If they are empty, the production order was not created from a sales document via the **Production Order Assistant**.

### 2. What does an entry in "Prod. Target Type" mean?

A populated value indicates that the production order originates from a sales transaction via the **Production Order Assistant** and that the quantity calculation was performed from the sales document — not via reservation entries. The value **Sales Order** refers to an order, the value **Sales Quote** to a quote as the origin.

### 3. Why is the sales line displayed even though there is no reservation entry?

That is precisely the purpose of this app: it supplements the reservation-based standard logic with the reference fields of the Production Order Assistant. As a result, the triggering sales line appears even when no reservation exists.

### 4. Do I have to activate or set up the app?

No. There is no separate setup page and no activation switch. As soon as the three required modules are installed, the linkage takes effect automatically.

### 5. Why can I not find a separate setup page for this app via "Tell Me"?

This app brings no setup of its own. The only thing configured is the upstream Production Order Assistant on the **Production Order Assistant Setup** page. Whether and in which status production orders with reference fields are created depends on its settings.

### 6. Can I change the "Prod. Target No." or "Prod. Target Line No." fields myself?

No. These fields are set by the **Production Order Assistant** and are read-only on the production order line. They serve solely to trace the origin.

### 7. I created a production order manually — why does no sales line appear?

Production orders created manually or via planning carry no reference fields of the Production Order Assistant. For them, only the standard logic via reservation entries takes effect. If no reservation entry exists, the **Sales Lines** view remains empty accordingly.

### 8. What role does the "Check Status" of the Production Order Assistant play for the display?

The **Check Status** documents the review state of the production order created by the assistant, with the values **Open** (created, not yet checked), **In Progress** (review running), **Confirmed** (released) and **Rejected** (discarded). For the display of the sales line in the overview, only the presence of the reference fields is decisive; the **Check Status** does not control the display, but provides information about the processing state.

### 9. How do I quickly get from the overview to the triggering document?

In the **Sales Lines** view, choose the **Show Document** action. Depending on the origin, it opens the **Sales Order** or the **Sales Quote**. At the level of the production order line, by contrast, **Show Document** opens the production order.

### 10. The expected customer name is missing in the "Sell-to Customer Name" column — what is the cause?

The column shows the customer name of the linked sales line. If the name is missing, either no sales line is linked (see question 1) or the underlying customer is not set in the sales document. Check the originating document via **Show Document**.
