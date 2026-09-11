---
title: Anwenderhandbuch m+m Goods Receipt with Item Configurator
---

# User Guide m+m Goods Receipt with Item Configurator

This guide describes the **m+m Goods Receipt with Item Configurator** extension
for Microsoft Dynamics 365 Business Central. The extension is a **bridge** between
the **m+m Goods Receipt** (goods intake) and **m+m Item Configurator** modules.
It adds the **Item Configurator** action to the goods receipt document, allowing a
user to create a configured item directly from the document and automatically
insert a matching document line together with its components into the goods receipt.

## 1. Introduction

### Purpose of the module

In many goods intake and finishing processes, the exact, customer-specific
configured item is not determined until the goods are received. Without support, the
user would have to create the configured item in a separate step in the
**Item Configurator**, note down the resulting item number, and then transfer it
manually into the **Warehouse Receipt**.

The extension closes exactly this gap: with a single action on the
Warehouse Receipt document, the user starts the **Item Configurator**, creates the
**Production Part** there, and on returning to the Warehouse Receipt automatically
receives a document line with the new Production Part as well as its **components**.
The manual transfer is eliminated, and item and document stay consistent.

### Target audience

The primary target audience is **operational users** in goods intake or goods
receipt, who record Warehouse Receipt documents every day and need configured items
in the process. Secondarily, the chapter **Prerequisites and Setup** is aimed at
**administrators** and **key users** who install the participating modules and set up
the **Item Configurator** once.

### Brief process overview

1. The user opens a **Warehouse Receipt** document with status **Open**.
2. They start the **Item Configurator** action.
3. In the **Item Configurator** they select a **Template Code** and a
   **Routing Template Code** and run the action **Create Item and Routing**. This
   creates the **Production Part** and the associated **Provided Part**.
4. After the configurator is closed, the extension automatically inserts a line in the
   **Warehouse Receipt** with the new **Production Part** and its **components**.

The actual further processing of the Warehouse Receipt document (creating sales,
production, or assembly orders, posting) is still handled by the base module
**m+m Goods Receipt**; this extension ends with the inserted line.

## 2. Quick start for users

The fastest path from an open document to a configured item:

1. **Ensure setup (once, by the administrator):** The modules
   **m+m Goods Receipt** and **m+m Item Configurator** are installed, and the
   **Item Configurator Setup** is maintained (see chapter 3).
2. Open the desired **Warehouse Receipt** document. The document must have status
   **Open**.
3. On the ribbon, choose the **Item Configurator** action.
4. In the **Item Configurator**, select the **Template Code** and the
   **Routing Template Code**.
5. Run the action **Create Item and Routing**. The **Production Part**
   and the **Provided Part** are created; adjust the routing and
   component lines if needed.
6. Close the **Item Configurator** with **OK**. In the **Warehouse Receipt**, a line
   now appears automatically with the **Production Part** as well as the associated
   **components**.

> If the document is not **Open**, Business Central cancels the action with a
> field check on the **Status** field. First set the document back to **Open**
> before you start the **Item Configurator**.

## 3. Prerequisites and Setup

This extension itself does not come with **its own setup page**. However, it builds
on two upstream modules and requires their correct setup. The order follows from the
app's dependencies.

### 3.1 Dependent modules and installation order

Who sets this up: the **administrator**, once before first use.

The extension depends on the following modules and can only be used together with
them:

| Module | Explanation |
|-------|-------------|
| m+m Cloud Base | Base module; provides the license check that this extension calls at sign-in. If it is missing, the extension cannot be operated properly. |
| m+m Goods Receipt | Provides the **Warehouse Receipt** document to which the **Item Configurator** action is attached, as well as the line and component structure into which the extension writes. |
| m+m Item Configurator | Provides the **Item Configurator** page and its setup; this is where the **Production Part**, **Provided Part**, bill of materials, and routing are created. |

**Procedure:** First the administrator installs the three modules named above (or
ensures that they are installed), then this bridge extension. Only after that is the
**Item Configurator** action available on the Warehouse Receipt document.

### 3.2 Setting up the Item Configurator

Who sets this up: the **administrator** or **key user**, once, before the first
configured item is created from a Warehouse Receipt. This setup takes effect later in
chapter 5 (Detailed process) when the **Item Configurator** action is run.

**Entry point:** Open the **Item Configurator Setup** via **Search**, by entering the
search term *Item Configurator Setup* and choosing the corresponding link.
(This page belongs to the **m+m Item Configurator** module and is a
company-wide setup.)

For the interaction with the Warehouse Receipt, the following fields are especially
relevant:

| Setup | Explanation |
|-------------|-------------|
| Prefix Production Part | If a character string is stored here (e.g. "FT"), it is prefixed to every item number of a **Production Part**; from this identifier the user recognizes that this is the configured Production Part that the extension inserts into the Warehouse Receipt line. |
| Finished Item No. Series | If a number series is stored here, the **Item Configurator** assigns the item number of the **Production Part** automatically from this series; without a configured series, no Production Part can be created and therefore no line can be inserted into the Warehouse Receipt. |

> Beyond the fields named above, the **Item Configurator Setup** has additional
> fields (e.g. configuration template for provided parts, default component
> quantity). These belong to the **m+m Item Configurator** module and are described in
> detail there; for the bridge process, the two mandatory settings named above are
> sufficient.

**Prerequisite/dependency:** In the configurator, you can only select templates that
are released for the Item Configurator. If no matching **Template** and no
**Routing Template Code** exist, the user cannot create a Production Part in
chapter 5.

### 3.3 Permissions

Who sets this up: the **administrator**.

The extension delivers the permission set **All permissions**
(`MuM GRIC Permission`). It defines which objects a user may run, and includes the
execute permission for the extension's central processing logic
(codeunit **MuM GRIC Item Config. Mgt.**). Assign this permission set to the users
who are to use the **Item Configurator** action in the Warehouse Receipt.
The permissions for the Warehouse Receipt document itself and for the Item
Configurator are granted through the permission sets of the respective base modules.

## 4. The "Item Configurator" action in the Warehouse Receipt

The only user interface that this extension itself adds is the **Item Configurator**
action on the **Warehouse Receipt** document. So that the user can employ this action
sensibly, the following first describes the document fields relevant to the bridge
process and then the action itself.

**Controlling setup:** Whether and how the inserted line is processed further is
controlled by the document's processing flags (**Post Components**, **Create Sales
Order**, **Create Production Order**, **Create Assembly Order**). Their default values
are set by the administrator in the **m+m Goods Receipt** base module's setup; on the
individual document the user can override them (see chapter 5).

### 4.1 Entering the document

**Entry point:** Open the list of Warehouse Receipt documents of the
**m+m Goods Receipt** module and choose the desired document, or create a new
document. Make sure that the document has status **Open**.

### 4.2 Header fields of the document (relevant to the bridge process)

The Warehouse Receipt document shows a number of header fields. The following are
relevant for the interaction with the **Item Configurator**:

| Field | Explanation |
|------|-------------|
| No. | Unique document number of the Warehouse Receipt. If it is assigned from the number series, Business Central assigns the document uniquely; the inserted Production Part line references exactly this number. |
| Status | Controls whether the document may be edited (see value list below). Only when **Open** can the **Item Configurator** action be run. |
| Receipt Date | If set, it documents the actual goods receipt day of the document; it controls the chronological classification of the goods receipt. |
| Document Date | If set, it records the document date, which is used for evaluation and tracking of the goods receipt. |
| Post Components | If enabled, the components of the inserted Production Part line are posted along with this goods receipt; without the flag, the components remain unposted and serve only for documentation. |
| Create Sales Order | If enabled, the base module creates a sales order for the recorded customer from this goods receipt; if it is not set, no sales document is created. |
| Create Production Order | If enabled, the base module creates a production order from the Production Part line to produce the configured item; without the flag, no production is triggered. |
| Create Assembly Order | If enabled, the base module creates an assembly order from the line; without the flag, no assembly takes place. |
| Production Order Type | If set, the base module uses exactly this order type when creating the production order; it determines the number series and behavior of the created production order. |
| Sell-to Customer No. | If set, it assigns the goods receipt to a customer; this customer is transferred into the created sales order when **Create Sales Order** is active. |
| Sell-to Customer Name | Shows the name of the assigned customer; serves to verify the selected customer. |
| Receipt Location Code | If set, the received quantities are posted to this location; it determines where the goods are received. |
| Blocked Location Code | If set, goods to be received as blocked are posted to this blocked location; it separates released from blocked goods. |
| External Shipment No. | If set, it records the vendor's delivery note number and enables the later assignment of the goods receipt to the external document. |
| External Order No. | If set, it refers to the order number in the customer's numbering system and eases communication with the customer. |
| Requested Delivery Date | If set, it documents the delivery date requested by the customer and flows into a created sales order. |

The remaining header areas of the document — the **Ship-to** address (delivery
address and shipment method) as well as the **Document information** areas (creation
and modification data) — control shipment or serve for logging. They are not changed
by the **Item Configurator** action and belong to the standard scope of the base
module **m+m Goods Receipt**.

#### Value list for the "Status" field

The **Status** field controls which actions are permitted on the document. For the
extension, the decisive point is that the **Item Configurator** action is only
allowed when **Open**:

- **Open:** The document is being edited and may be changed. Only in this status can
  the **Item Configurator** action be run and a Production Part line be inserted.
- **In progress:** The document is currently being processed. The
  **Item Configurator** action is not possible; first set the document back to
  **Open**.
- **Released:** The document is released and intended for further processing or
  posting. Changes via the **Item Configurator** are no longer possible.

> The three values named are the status forms confirmed via the translation files.
> The base module internally uses further intermediate states for processing control;
> for the use of the **Item Configurator** action, the only relevant point is that the
> document is **Open**.

### 4.3 The "Item Configurator" action

The **Item Configurator** action is placed on the document's ribbon in the processing
area as the first action.

**Open the configurator window of the same name via the Item Configurator action.**
When called, Business Central first checks whether the document has status **Open**.

- If the document is **Open**, the **Item Configurator** opens as a modal
  window (see chapter 5).
- If the document is not **Open**, Business Central cancels with a field check on
  **Status**; no configurator is opened and no line is inserted.

## 5. Detailed process

This chapter describes the complete process that the **Item Configurator** action
triggers — from the configurator window to the inserted document line.

### 5.1 The Item Configurator

After the action is started, the **Item Configurator** window opens. Here the user
selects the templates for the item to be created:

| Field | Explanation |
|------|-------------|
| Template | Shows the underlying item template; it determines which master data values are transferred into the created **Production Part**. |
| Template Code | If selected, this configuration template is used to create the master data of the **Production Part**; the values preset in the template are carried over into the new item. |
| Routing Template Code | If selected, the specified existing routing serves as a template for the routing of the Production Part to be created; without a selection, no routing can be created. |

The following actions are then available:

- **Create Item and Routing:** When run, the **Production Part** and the associated
  **Provided Part** are created based on the selected templates, a component line is
  created, and the routing lines are shown for editing. Only after that does the
  document have an item that the extension can take over.
- **Not finished configuration:** When run, the configuration is flagged as
  not finished; the item remains in progress and can be completed later.

The area of the component and routing lines belongs to the module
**m+m Item Configurator** and is described in detail there. For the bridge process it
is sufficient to fully create the **Production Part** and close the window with **OK**.

### 5.2 Take-over back into the Warehouse Receipt

As soon as the user closes the **Item Configurator**, the extension determines the
created **Production Part** and takes it over into the Warehouse Receipt document. For
items created as the last stage of a multi-stage routing (without a subsequent
operation), the created Production Part is additionally taken over safely via an
internal buffer, so that the most recently created item number is always used.

The extension then **automatically** inserts a new line into the Warehouse Receipt:

- The line number is assigned consecutively (increased by 10,000 relative to the
  last line of the document).
- The **Item No.** field of the line is filled with the new **Production Part**.
- The associated **components** are then created for this line.

If the configurator is closed without a created Production Part (empty Production
Part number), or the item does not exist, the extension inserts **no** line; the
document remains unchanged.

### 5.3 Line fields of the inserted Production Part line

The inserted line appears in the line area of the Warehouse Receipt. For control by
the user, the following fields are especially relevant:

| Field | Explanation |
|------|-------------|
| Block Components | If enabled, the components belonging to this Production Part are blocked and not released for posting; without the flag, the components are ready for processing. |
| Item No. | Contains the number of the created **Production Part**; through it the Warehouse Receipt line is uniquely assigned to the configured item. |
| Description | Shows the description of the Production Part; it comes from the item's master data and serves for recognition in the document. |
| Quantity | If recorded, it defines how many units of the Production Part are received or processed further; follow-up orders and component requirements are based on this quantity. |
| Unit of Measure Code | If set, it determines the unit in which the quantity is kept (e.g. piece); it controls the quantity conversion in follow-up documents. |
| Variant Code | If set, it specifies the item variant of the line; the variant is carried over into follow-up orders. |
| Location Code | If set, it determines the location to which the line is received; it controls the goods receipt of the line. |

Further line fields (allocation/lot size details, rounding precision, routing number
of the line, as well as the origin details for the source document) are maintained by
the base module for further processing and, for the line inserted by the
configurator, are as a rule not to be entered manually.

### 5.4 Components of the Production Part line

For each inserted Production Part line, the extension creates the associated
**components**. The document shows these in the component area:

| Field | Explanation |
|------|-------------|
| Item No. | Contains the number of the component; it designates the material that goes into the Production Part. |
| Description | Shows the description of the component and serves to verify the correct material. |
| Quantity per | If set, it indicates how many units of the component are needed per unit of Production Part; it determines the quantity-dependent material requirement. |
| Quantity | If set, it shows the total quantity of the component for the line quantity of the Production Part; it controls the actual consumption. |
| Expected Quantity | If set, it shows the expected component quantity and serves to reconcile planning and actual receipt. |
| Unit of Measure Code | If set, it determines the unit of measure of the component; it controls the quantity conversion. |
| Location Code | If set, it determines the location from which or to which the component is posted. |
| Bin Code | If set, it specifies the bin within the location for the component. |
| Provided Item | If enabled, the component is flagged as a part provided by the customer; it is treated not as a separate purchase but as a provided item. |

Further component fields that are hidden by default (geometry details such as length,
width, weight, depth, as well as the calculation formula and the second description)
serve special calculations of the base module and are not shown to the user by
default.

### 5.5 Summarized process (posting or processing chain)

This extension performs **no posting or release of its own**. Its contribution ends
with the inserted line; the further processing is handled by the base module. The
complete process:

1. Select **Warehouse Receipt** document with status **Open**.
2. Run the **Item Configurator** action (opens the modal window).
3. Select **Template Code** and **Routing Template Code** and run **Create Item and
   Routing**; close with **OK**.
4. The extension automatically inserts the **Production Part** line together with its
   **components**.
5. The further processing (creating a sales, production, or assembly order, posting
   components, releasing and posting the document) is done via the standard functions
   of the **m+m Goods Receipt** module.

## 6. System behavior and events

Besides the visible action, the extension contains background logic that the user
does not operate directly, but whose effect they should be aware of:

- **Take-over of the Production Part for multi-stage routings:** If, when creating in
  the Item Configurator, a semi-finished item is created as the last stage (without a
  subsequent operation), the extension remembers its item number and uses exactly this
  one when inserting the line. This way the most recently created Production Part is
  always taken over into the Warehouse Receipt.
- **License check at sign-in:** When signing in to the company, the extension checks
  the extension's license via the **m+m Cloud Base** module. This ensures that the
  **Item Configurator** action is only available with a valid license.

## 7. FAQ and Troubleshooting

### 1. Why is the "Item Configurator" action grayed out or ineffective?

The action can only be run when the document status is **Open**. If the document is
**In progress** or **Released**, Business Central cancels with a field check on
**Status**. Set the document back to **Open**.

### 2. Why was no line inserted after the configurator?

The extension inserts a line only if a **Production Part** was actually created in the
**Item Configurator**. If you closed the window without the action **Create Item and
Routing**, the Production Part number stays empty and no line is created.

### 3. Why does the system report that the Production Part does not exist?

Before inserting, the extension checks whether the item for the determined Production
Part number exists. If the item was not fully created in the configurator or was
deleted in the meantime, the insertion is omitted. Create the Production Part again
via the configurator.

### 4. Why does the Production Part not get a number?

The item number of the Production Part is assigned from the **Finished Item No.
Series** of the **Item Configurator Setup**. If no number series is stored there, no
Production Part can be created. Maintain the setup (chapter 3.2).

### 5. Why can't I select a template in the configurator?

Only templates that are released for the Item Configurator can be selected. If
matching **Template Code** or **Routing Template Code** entries are missing, contact
the administrator; the templates are maintained in the **m+m Item Configurator**
module.

### 6. Why aren't the components of my line posted?

Whether components are posted along is controlled by the header flag **Post
Components**. If it is not enabled, the components serve only for documentation. Enable
the flag if the components are to be posted.

### 7. How do I recognize the created Production Part in the line?

By the **Item No.** field of the inserted line and by the **Prefix Production Part**
(e.g. "FT") that is prefixed to the number. Through this prefix you distinguish the
Production Part from the associated **Provided Part**.

### 8. What is the difference between Production Part and Provided Part?

The **Production Part** is the configured end item that is inserted into the Warehouse
Receipt line. The **Provided Part** is the associated provided part (raw part) in the
bill of materials of the Production Part. Both are created together by the
configurator.

### 9. Why do I have to sign in again for the extension to work?

At sign-in, the extension checks the license via **m+m Cloud Base**. If the license
was only recently activated, signing in again may be required so that the check takes
effect and the action is available.

### 10. Does this extension post the Warehouse Receipt document?

No. The extension only creates the Production Part line and its components. Creating
follow-up orders, posting the components, as well as releasing and posting the
document are done via the standard functions of the **m+m Goods Receipt** module.

## 8. Typical use cases

### 8.1 Configured item for a customer order at goods receipt

**Trigger:** For a customer order, a customer-specific configured part is expected. At
goods receipt, the concrete form of the item is determined and is to be created
directly.

**Entry in BC:** The user opens the relevant **Warehouse Receipt** document (status
**Open**) from the Warehouse Receipt list and records the customer in the header via
**Sell-to Customer No.** as well as the relevant header data (e.g. **Receipt Date**).

**Core process:**
1. Run the **Item Configurator** action.
2. Select **Template Code** and **Routing Template Code** according to the customer
   specification.
3. **Create Item and Routing**; the **Production Part** and **Provided Part** are
   created.
4. Close the window with **OK** — the extension inserts the line with **Item No.**
   (Production Part) and the **components**.
5. If needed, adjust **Quantity** and **Unit of Measure Code** of the line.

**Completion:** If **Create Sales Order** is enabled in the header, the base module
creates the sales order for the recorded customer in the further course. Posting and
release of the document are done via the standard functions of the Goods Receipt.

### 8.2 Ad-hoc configuration on an open Warehouse Receipt document

**Trigger:** While recording an open Warehouse Receipt document, the user notices that
a further configured part is needed that does not yet exist as an item.

**Entry in BC:** The user is already on the open **Warehouse Receipt** document.

**Core process:**
1. Start the **Item Configurator** action directly from the document.
2. Select templates and run **Create Item and Routing**.
3. Close the window — the extension adds a further **Production Part** line at the end
   of the document (consecutive line number) together with its **components**.

**Completion:** The user checks the new line and its components (field **Provided
Item** for provided parts) and continues recording the document. A separate posting by
the extension does not take place.
