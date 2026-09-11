---
title: Anwenderhandbuch m+m Production Order Assistant with Drop-/Special Shipment
---

# User Guide m+m Production Order Assistant with Drop-/Special Shipment

## Introduction

The app **m+m Production Order Assistant with Drop-/Special Shipment** is an extension for "Microsoft Dynamics 365 Business Central". It acts as a **connector** between two m+m modules: the **m+m Production Order Assistant** and the **m+m Drop-/Special Shipment**. The app does not add any pages of its own; instead, it ensures that both modules interact correctly within a shared sales process.

Specifically, the app governs two things:

- For sales lines flagged as **Release Business**, **no** automatic production order is created when the sales order is released. Instead, these lines are handled through the purchase order of the Drop-/Special Shipment.
- The **Production Order Assistant** can – controlled via a setup option – also be invoked for sales lines with a **Special Order**, even though the assistant would block such lines by default.

**Target audience:** This guide is aimed primarily at **operational users in sales and purchasing** who work with sales orders on a daily basis – that is, who enter sales lines, release orders, create purchase orders from the sales order, and start the Production Order Assistant from the sales line. Secondarily, it addresses **administrators and key users** who configure the **Prod. Assistent Setup**, the **Purchasing Codes**, and the **Locations** before first use.

**Brief process overview:** The user creates a sales order and flags a line via the **Purchasing Code** as a drop shipment, special order, or release business. After the order is released, the user creates the associated **Purchase Order** through an action in the sales order. For lines with a special order, the **Production Order Assistant** can additionally be started from the sales line to create a production order.

## Quick Start for Users

The quick start shows the shortest path to the result. Setup is a prerequisite and therefore comes first.

**One-time setup (administrator/key user):**

1. Open **Prod. Assistent Setup** via **Search** and enable the option **Create Prod. Order on Sales Order For Special Order** if the Production Order Assistant is to be used for Special Order lines. In addition, define the **Prod. Order Status f. Sales Order**.
2. Open **Purchasing Codes** via **Search** and create a code with **Special Order** and **Release Business** set (for a release business, both checkmarks must be set).
3. Open **Locations** via **Search**, call up the relevant **Location Card**, and enable **Release Business** (or **Drop Shipment**/**Special Order**).

**Daily work (sales/purchasing):**

4. Create a **Sales Order**, enter the item line, and set the **Purchasing Code** created in step 2 on the line. This sets **Special Order** and **Release Business** on the line.
5. On the sales line, enable **Selection For Purch. Order** and, if required, enter a **Vendor No.**
6. **Release** the sales order (status **Released**).
7. In the sales order, invoke the action **Create Special/Drop/Release Purchase Order**.
8. Confirm the prompt "Do you want to open the purchase order?" with **Yes**; the created **Purchase Order** opens.
9. *(Optional, for Special Order lines without Release Business)* On the sales line, open the assistant via **Line → Prod. Assistant** and create a production order with **OK**.

## Setup

Setup is performed in "Microsoft Dynamics 365 Business Central". Because this app controls the interplay between the Production Order Assistant and the Drop-/Special Shipment, three configuration areas are relevant: the central **Prod. Assistent Setup**, the **Purchasing Codes**, and the **Locations**. The latter two, together with a global option, form the activation chain for the release business.

### Prod. Assistent Setup

**Entry point:** Open the **Prod. Assistent Setup** page via **Search**.

**Who/when:** This page is configured by the administrator or key user **once before first use**. It is a company-wide setup (one record per company). The options set here control the status with which, and the conditions under which, the Production Order Assistant creates production orders from the sales document – and whether this is also permitted for lines with a **Special Order**. The app **m+m Production Order Assistant with Drop-/Special Shipment** evaluates the option **Create Prod. Order on Sales Order For Special Order** (see the section *Interplay of the Modules*).

| Setup | Explanation |
|-------------|-------------|
| **Prod. Order Status f. Sales Quote** | When a production order is created from a sales quote, it receives the status selected here. Permitted values are **Simulated**, **Planned**, **Firm Planned**, and **Released**; the status **Finished** is not allowed and is rejected. **Simulated:** non-binding proposal without reservation/posting. **Planned:** scheduled, but not yet firmly scheduled. **Firm Planned:** firmly scheduled, intended for production. **Released:** released for production, output postings possible. |
| **Prod. Order Status f. Sales Order** | When a production order is created from a sales order, it receives the status selected here. Values as above: **Simulated**, **Planned**, **Firm Planned**, **Released** (not **Finished**). The value determines whether the created orders are only simulated or already appear firmly in production planning. |
| **Set Confirm Status for Prod. Order Check** | When enabled, the production order created via the Production Order Assistant (and its associated line) receives the check status "Confirmed"; without this option, the check status remains "Open". This makes it immediately apparent for downstream checks that the order was confirmed via the assistant. |
| **Reset Sales Quote Prod. Order Formula** | When a date formula is stored, simulated production orders for sales quotes are automatically cleaned up after this period expires; if the field remains empty, no automatic deletion takes place. This prevents the accumulation of simulated orders for quotes that were never converted. |
| **Create Prod. Order on Sales Order Release** | When enabled, a production order is automatically created for the affected lines upon **Release** of the sales order; without the option, the user creates the production order manually via the **Prod. Assistant** action. For lines with **Release Business**, this automatic creation is suppressed by the present app (see *Interplay of the Modules*). |
| **Confirm Create Prod. Order on Sales Order Release** | When enabled, a confirmation prompt appears upon release before production orders are created; the user decides per release. This option requires that **Create Prod. Order on Sales Order Release** is active (otherwise it is rejected during validation). |
| **Prefill Create Prod. Order in Sales Lines** | Defines how the line field **Create PO** is prefilled in new sales lines. **None:** no prefill; the user sets the checkmark per line themselves. **All:** in all new lines **Create PO** is prefilled, so that a production order is intended without any further action. This option, too, requires an active release automation. |
| **Create Prod. Order on Sales Order For Special Order** | When enabled, the Production Order Assistant may also be run for sales lines with a **Special Order**; if the option is not set, the assistant blocks such lines and reports that no production order may be created for Special Order lines. **This is the central control option of this app** for the assistant path. |
| **Delete assigned Prod. Order on Sales Order delete** | When enabled, the associated production orders created from a sales order are also deleted when the sales order is deleted; without the option, orphaned production orders remain and must be removed manually. |
| **Notify Salesperson by Status Change** | When enabled, the responsible salesperson receives a notification as soon as the status of a production order created from sales changes; without the option, no automatic information is sent to sales. |

Note: The technical field for transferring item tracking from the production order to the sales order is disabled in the current program version and is no longer shown to the user; it is therefore not listed here.

### Setting Up the Release Business

The release business requires a chain of **master data** and **setup** before it can be used in day-to-day operations. Whoever configures the release business first creates the purchasing code, then flags the locations, and finally invokes the function in the sales order. The order follows from the checks in the program.

**First – create the purchasing code for the release business**

**Entry point:** Open the **Purchasing Codes** page via **Search**. Create a new code via **New** or edit an existing one.

The **Purchasing Code** is the standard Business Central master data table used to flag a sales line as a drop shipment or special order. The Drop-/Special Shipment module adds the **Release Business** flag here. The user in sales later selects the code on the sales line; via the code, the flags are automatically copied into the line.

| Setup | Explanation |
|-------------|-------------|
| **Code** | When a code is assigned, it is available for selection on the sales line in sales; it is the key through which the following flags are transferred into the line. |
| **Description** | Descriptive text for the purchasing code; helps sales make the correct selection on the sales line. |
| **Drop Shipment** | When set, the vendor delivers the items directly to the customer; the sales shipment is posted automatically after the purchase receipt. |
| **Special Order** | When set, the ordered item is first delivered to your own company (e.g. for repacking or further processing) and only afterwards to the customer; the sales shipment is posted manually. |
| **Release Business** | When set, the line works like a special order, but in addition the "Ship-to" fields are transferred from the sales order to the created purchase order. Prerequisite: In the purchasing code, **Special Order** and **Release Business** must both be set. |

**Next – flag the locations for the release business**

**Entry point:** Open the **Locations** list via **Search** and call up the relevant **Location Card**.

For each location, the administrator specifies for which business types this location may be used within the Drop-/Special Shipment. When creating the purchase order, the program checks the location of the sales line: if the line is a release business, the location must carry the **Release Business** flag, otherwise the process is aborted.

| Setup | Explanation |
|-------------|-------------|
| **Drop Shipment** | When set, this location may be used in sales lines with a drop shipment; without the flag, a drop shipment via this location is rejected during the purchasing process. |
| **Special Order** | When set, this location may be used in sales lines with a special order; otherwise the purchasing process aborts for Special Order lines at this location. |
| **Release Business** | When set, this location may be used for Release Business lines. When this checkmark is set, **Special Order** is automatically activated as well, since the release business builds on the special order. |

**Finally – operational trigger**

After the sales order has been released, the user creates the purchase order via the action **Create Special/Drop/Release Purchase Order** (see *Daily Work on the Sales Order*). If, in addition, the option **Create Prod. Order on Sales Order For Special Order** is active in the **Prod. Assistent Setup**, the Production Order Assistant can also be used for Special Order lines (see the next section).

### Enabling Production Orders for Special Order Lines

This second, independent activation concerns the **Production Order Assistant**. It is set by the administrator in the **Prod. Assistent Setup** and used in day-to-day operations via the sales line.

1. **Process prerequisite:** In the **Prod. Assistent Setup**, enable the option **Create Prod. Order on Sales Order For Special Order**. If this option is not set, the Production Order Assistant blocks every sales line flagged as a **Special Order**.
2. **Define the production order status** via **Prod. Order Status f. Sales Order** so that the created production orders receive the desired planning status.
3. **Operational completion:** On the sales line, the user opens the assistant via **Line → Prod. Assistant** and creates the production order with **OK** (see *Daily Work on the Sales Order*).

Note on delimitation: For lines with **Release Business**, no production order is created upon release (this is suppressed by the present app). Such lines run exclusively through the purchase order path of the release business.

### Permissions

The app ships the permission set **All permissions** (internal access, assignable). It defines the permissions for executing the integration logic of this app (the codeunit connecting the Production Order Assistant and the Drop-/Special Shipment). The administrator assigns this permission set to the users who work with release business and the Production Order Assistant in the sales order. For the actual sales, purchasing, and production processes, the standard Business Central permissions as well as those of the two base modules apply additionally.

## Daily Work on the Sales Order

The central document for the user is the **Sales Order**. The affected fields and actions are added to the sales line by the two base modules; the present app controls their interplay in the background.

**Controlling setup:** The behavior in this chapter is determined by the **Prod. Assistent Setup** (assistant path and release automation), the **Purchasing Codes** (flagging the line as drop shipment/special order/release business), and the **Locations** (permissibility per business type). These areas are described in the *Setup* chapter.

### Fields on the Sales Line

These fields appear in the lines of the sales order and originate from the two base modules.

| Field | Explanation |
|------|-------------|
| **Create PO** | When set, the creation of a production order is intended for this line; the assistant or the release automation only processes lines with the checkmark set. The prefill is controlled by the option **Prefill Create Prod. Order in Sales Lines** in the setup. |
| **Vendor No.** | When set, the purchase order created from it is directed to this vendor; if the field remains empty, the program determines the vendor via the stockkeeping unit of the item or the item itself. The field may only be filled if **Selection For Purch. Order** is set. |
| **Selection For Purch. Order** | When set, this line is included in the purchase order when the action **Create Special/Drop/Release Purchase Order** is invoked; only selected lines are processed. The checkmark can only be set if the line is flagged as a **Special Order** or **Drop Shipment**, otherwise an error message appears. |
| **Release Business** | Indicates that this line is a release business. The field is set automatically via the selected **Purchasing Code** and is not directly editable. When set, the "Ship-to" fields of the sales order are copied into the purchase order during purchase order creation, and upon order release **no** automatic production order is created for this line. |

### Action: Prod. Assistant

**Open the assistant via the Prod. Assistant action:** On the sales line, via **Line → Prod. Assistant**. The assistant calculates the quantity to be produced and creates a production order for the line with **OK** (status according to **Prod. Order Status f. Sales Order**). The prerequisite is that the line field **Create PO** is set. If the line is a **Special Order**, the option **Create Prod. Order on Sales Order For Special Order** must additionally be active in the **Prod. Assistent Setup**; otherwise the call is rejected for this line. If the user cancels the assistant, the previously created simulated production order is deleted again.

### Action: Create Special/Drop/Release Purchase Order

**Open the purchase order process via the Create Special/Drop/Release Purchase Order action:** in the released sales order via the document actions. The action processes all lines with **Selection For Purch. Order** set and creates one **Purchase Order** per vendor from them. The exact procedure is described in the section *Posting and Purchase Order Procedure*.

### Calling the Linked Documents

After the purchase order has been created, the sales order and the purchase order are linked to each other:

- On the purchase line, the user opens the associated **Sales Order** via the corresponding call.
- On the sales line, the user opens the linked **Purchase Order** via the **Purchase Order** action.

### Posting and Purchase Order Procedure

The procedure for a release business follows from the program and must be observed in the following order:

1. In the **Sales Order**, enter the line: item, quantity, and **Purchasing Code** with release business. This sets **Special Order** and **Release Business** on the line.
2. Enable **Selection For Purch. Order** on the line; set the **Vendor No.** if required.
3. **Release** the sales order (status **Released**). Purchase order creation requires a released order. For Release Business lines, no automatic production order is created upon release.
4. Invoke the action **Create Special/Drop/Release Purchase Order**. The program checks the location (for a release business, the location must carry the **Release Business** flag), determines the vendor (line **Vendor No.**, otherwise stockkeeping unit, otherwise item) and creates one **Purchase Order** per vendor. For a release business, the "Ship-to" fields of the sales order are copied into the purchase order.
5. Confirm the prompt **"Do you want to open the purchase order?"** with **Yes**. For a single purchase order, the **Purchase Order** opens; for multiple purchase orders, the list of purchase orders opens.
6. Continue with the further standard process in Business Central: **release the purchase order** and post the purchase receipt. Via the line calls, the linked **Sales Order** can be displayed from the purchase order and the **Purchase Order** from the sales order at any time.

Partial quantities are permitted: not all lines have to be selected and ordered at the same time. The user can order selected lines and add further lines later; lines already linked to a purchase order are not processed again.

## Interplay of the Modules (Control Logic)

This chapter describes what the app **m+m Production Order Assistant with Drop-/Special Shipment** contributes itself. It intervenes at two points of the Production Order Assistant – both concern exclusively sales lines with **Release Business** set:

- **At order release:** When a sales line is flagged as **Release Business**, the app suppresses the automatic creation of a production order. These lines are handled via the **Purchase Order** of the release business, not via a production order.
- **When the Production Order Assistant is called directly:** When a sales line is flagged as **Release Business**, the app overrides the assistant's standard checks depending on the setup. If the option **Create Prod. Order on Sales Order For Special Order** is not set, the block against Drop Shipment lines remains in effect. This ensures that Release Business lines do not inadvertently also create a production order.

For users this means: **Release Business lines** go through the purchase order path (action **Create Special/Drop/Release Purchase Order**); plain **Special Order lines** without release business can additionally use the **Production Order Assistant**, provided the setup allows it.

## Typical Use Cases

### Use Case 1: Release Business to a Customer's Delivery Address

**Trigger:** A customer orders an item by phone that is not in stock and is procured via a supplier; the goods are to go to a specific delivery address of the customer.

**Entry point in BC:** The user in sales opens the **Sales Orders** via **Search** and creates a new **Sales Order** for the customer.

**Core procedure:**

1. On the sales line, enter the item and quantity and select the **Purchasing Code** with release business. This sets **Special Order** and **Release Business** on the line.
2. Enable **Selection For Purch. Order** and – if a specific supplier is desired – set the **Vendor No.** Ensure that the location of the line carries the **Release Business** flag.
3. **Release** the sales order (status **Released**). For the Release Business line, no production order is deliberately created here.
4. Invoke the action **Create Special/Drop/Release Purchase Order**. The "Ship-to" fields of the sales order are copied into the created **Purchase Order**.
5. Confirm the prompt with **Yes**; the **Purchase Order** opens.

**Completion:** Purchasing releases the **Purchase Order** and posts the purchase receipt in the standard process. Via the line calls, you can switch between **Sales Order** and **Purchase Order** at any time.

### Use Case 2: Production Order for a Special Order

**Trigger:** A customer orders an item that must first be produced or processed and therefore first comes into your own company (special order).

**Entry point in BC:** The user opens the relevant **Sales Order** and goes to the sales line.

**Core procedure:**

1. Check the prerequisite: In the **Prod. Assistent Setup**, **Create Prod. Order on Sales Order For Special Order** is enabled.
2. On the sales line, select the **Purchasing Code** with **Special Order** and set the field **Create PO**.
3. On the line, open the assistant via **Line → Prod. Assistant**.
4. In the assistant, check the calculation and create the production order with **OK** (status according to **Prod. Order Status f. Sales Order**).

**Completion:** The created production order appears with the configured status in production planning. If **Set Confirm Status for Prod. Order Check** is active in the setup, the order additionally carries the check status "Confirmed".

## FAQ and Troubleshooting

### 1. Why is no production order created when releasing a sales order with a Release Business line?

This is the intended behavior of this app. For lines with **Release Business**, the app suppresses the automatic production order creation upon order release. These lines are handled as a purchase order via the action **Create Special/Drop/Release Purchase Order**.

### 2. Why does the Production Order Assistant block my Special Order line?

The assistant rejects lines with a **Special Order** as long as the option **Create Prod. Order on Sales Order For Special Order** is not enabled in the **Prod. Assistent Setup**. Enable this option to unlock the assistant for such lines.

### 3. Why can't the Selection For Purch. Order field be set?

The checkmark can only be set if the sales line is flagged as a **Special Order** or **Drop Shipment**. First select a suitable **Purchasing Code** on the line; only then is **Selection For Purch. Order** permitted.

### 4. Why can't I enter a Vendor No. on the sales line?

The **Vendor No.** may only be filled if **Selection For Purch. Order** is set on the line. First set the selection checkmark and then select the vendor.

### 5. Why does purchase order creation abort with a note about the location?

When creating the purchase order, the program checks the location of the line. For a **Release Business**, the location must carry the **Release Business** flag on the **Location Card** (analogously **Special Order** or **Drop Shipment** for the other business types). Add the missing flag to the location.

### 6. Why does the Create Special/Drop/Release Purchase Order action require a released order?

Purchase order creation requires the sales order status **Released**. Release the sales order before invoking the action.

### 7. Which vendor is used if I do not store a Vendor No. on the line?

The program determines the vendor in this order: first the **Vendor No.** of the line, then the stockkeeping unit of the item for the location, then the vendor stored on the item. If none of these is filled, the program reports that no vendor was selected for the item and that no purchase order can be created for the line.

### 8. What does the production order status in the Prod. Assistent Setup mean?

The value selected via **Prod. Order Status f. Sales Order** or **Prod. Order Status f. Sales Quote** defines the status of newly created production orders: **Simulated** (non-binding proposal), **Planned** (scheduled), **Firm Planned** (firmly scheduled), or **Released** (released for production). The status **Finished** is not permitted.

### 9. Why does a list open after purchase order creation instead of a single purchase order?

If multiple purchase orders are created from the selected lines (e.g. for different vendors), the program opens the list of these purchase orders after confirmation with **Yes**. For exactly one purchase order, it opens directly.

### 10. How do I find the matching sales order for a purchase order – and vice versa?

From the purchase line, you open the linked **Sales Order** via the corresponding call. From the sales line, you open the associated **Purchase Order** via the **Purchase Order** action. Both documents are permanently linked to each other after purchase order creation.
