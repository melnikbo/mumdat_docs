---
title: Anwenderhandbuch m+m Semifinished Items
---

# User Guide m+m Semifinished Items

## Introduction

**m+m Semifinished Items** extends the manufacturing control of Microsoft Dynamics 365 Business Central with
the automatic creation of **Semi-Finished Items** and the associated **transfer** of the components
between the locations of the involved **Work Centers**. The module automatically splits a multi-level
production order into several production order lines – one line per
semi-finished stage –, finds or creates the matching semi-finished item based on **Material Properties**
and automatically creates **Transfer Orders** for the material flow between the work centers.

**Target audience.** Primarily this guide is aimed at **operational users in manufacturing** –
production planners and shop-floor workers who release production orders, post operation feedback, post the
output and trigger the split (**Split Order**). Secondary readers are **administrators and
work planners** who set up the work centers, routings, material types and material properties
(chapters *Setup* and *Master Data*).

**Brief process overview.** The typical path through the module:

1. The administrator marks a **Work Center** as **Semi-Finished Item** and stores
   **Material Properties** there.
2. In the **Routing**, the relevant **operation** is likewise marked as **Semi-Finished Item**;
   per operation, **Material Property Changes** (target values of the semi-finished item) are maintained and
   the **Split Option** is set in the routing header.
3. A **Firm Planned Production Order** is created from the sales order or manually.
4. On sales release, on production order release or manually via **Split Order**, the system splits the order,
   creates or finds the semi-finished items and creates the **Transfer Orders**.
5. When the output is posted, the transfers are processed automatically; via the transfer receipt the
   operation is set to **Finished** when required. When needed, the user creates the
   **following semi-finished order**.

All field, page and action names in this guide correspond to the German user interface of
Business Central. The BC search is referred to throughout as **Tell Me**.

---

## Quick Start for Users

The quick start describes the shortest path to the result. **First** the setup (one-time only, by
the administrator), **then** the daily work. Use the linked chapters for the
complete field tables.

**Setup (one-time, administrator) – in dependency order:**

1. **First** open the **Material Type** (Material Types list → card) and, in the field
   **Semi Finished Item Template**, store the item template from which new semi-finished items are created.
   See *Setup → Set up Semi-Finished Item Split*.
2. **Then** open the **Work Center** (Work Centers list → card) and activate the field
   **Semi-Finished Item**. Via the action **Material Properties**, maintain the assignment
   *Component Material Type → Semi-Finished Material Type → Property*.
3. In the **Routing**, mark the relevant **operation lines** as **Semi-Finished Item**, per
   operation capture the target values via the action **Material Property Changes**, and in the
   routing header choose the **Split Option**.
4. For the material flow, provide the **Locations** of the work centers, **Transfer Routes** (with
   **In-Transit Code**) and the number series for transfer orders. See *Setup →
   Set up the Transfer of Semi-Finished Components*.

**Daily work (operational user):**

1. Create a **Firm Planned Production Order** or generate it from the **Sales Order** and refresh it.
   Note: A **Released Production Order** with semi-finished operations that have not yet been split is
   not permitted – first create a firm planned order.
2. Run **Split Order** – automatically on sales release or on production order release (depending on the
   Split Option) or manually via the action **Split Order** on the production order. The system creates the
   semi-finished lines and the **Transfer Orders**.
3. **Release** the production order and process the operations normally.
4. **Post output** (production journal / output posting): The associated **transfer** is posted
   automatically and the **prod. order component** is moved to the destination location.
5. After the transfer receipt, the system sets the operation to **Finished** – provided
   **Semi Finished Finish Operation Option = When posting the transfer receipt**.
6. When needed, run the action
   **Create Following Semi-Finish Order** on the **Released Production Order**.

---

## Setup

The setup is the most extensive part of this module. It is performed in
**Microsoft Dynamics 365 Business Central** by the administrator or work planner, before the
operational production starts. The module requires two configuration tracks that build on each other:
the **Semi-Finished Item Split** (which operations create semi-finished items and how these are found)
and the **Transfer of Semi-Finished Components** (how the material flows between the locations).

### Set up Semi-Finished Item Split

**Who and when.** The administrator sets up this track once per production scenario, before the
first production order is split. It defines which operations create a semi-finished item,
from which template new semi-finished items are created, and with which target values. The setup is
consumed in daily operation by the function **Split Order** (see *Daily Work on the Production Order*).

**Numeric order of the setup steps (dependency order from the code):**

1. **First** store the template per **Material Type** (Master Data → *Material Type as Semi-Finished Stage*).
2. **Then** mark the **Work Center** as a semi-finished station and maintain its
   **Material Properties** (Master Data → *Work Center as Semi-Finished Station*).
3. **Next** set the marking and the **Material Property Changes** per **operation**
   (Master Data → *Operations and Material Property Changes*).
4. **Then** set the **Split Option** in the routing header (see *Routing: Controlling the Split*).
5. **Optionally** enable the **Optimized Semi-Finished Item Search** (see below).
6. **Finally**, in daily operation, the user triggers **Split Order**.

#### Routing: Controlling the Split

**Entry point:** Routings (list) → **Routing** (card) → tab **General**.

The routing header controls **when** a production order is automatically split, and documents whether
a routing originated from a split.

| Field | Explanation |
|---|---|
| **Split Option** | Defines when the automatic split of the production order is triggered. The values are explained below per option. Only settable as long as the routing is **not** a split routing and does **not** have the status *Certified*; if there is no operation line marked as a semi-finished item, setting it is rejected with the message "Cannot find a semi finish routing line!". |
| **Splitted Routing** | If activated, this routing is a duplicate **automatically created** by the split; it is set by the system and is not manually editable. This is how you distinguish generated routings from the originally maintained ones. |
| **Original Routing No.** | For a split routing, references the **number of the source routing** from which it was copied. This makes the origin of a generated routing traceable; for manually maintained routings the field remains empty. |

**Values of the Split Option (complete):**

- **(blank):** **No** automatic split takes place. The user can only trigger the split manually
  via **Split Order**.
- **On Sales Release:** If set, the system automatically splits the production order created from a
  sales order **as soon as the sales order is released** and components as well as
  material property changes exist. Ideal when the semi-finished structure should already be fixed at
  sales release.
- **On Prod. Order Release:** If set, the split takes place automatically **when the
  production order is released** (status change to *Released*). Suitable when the split should only be
  created at the point of the production release.

**Validation/dependency.** A split routing (**Splitted Routing** = active) cannot receive a
split option (the system checks that **Original Routing No.** is empty). As long as no
semi-finished operation line exists, the option cannot be set. Cross-link: you maintain the semi-finished
marking of the operations under *Master Data → Operations and Material Property Changes*.

#### Optimized Semi-Finished Item Search

**Entry point:** Material Property Setup (card of the base module *m+m Material Properties*) → group
**Semi Finish Item**.

This setup controls the procedure by which the module finds an already existing semi-finished item
matching the required properties.

| Setup | Explanation |
|---|---|
| **Use Optimized Semi Finish Search** | If activated, the split uses the internal, quantity-optimized property search (query over the property values, sorted by hit count per property) to determine a matching semi-finished item; for large item inventories this reduces the search time. If deactivated, the standard property search of the base module is used. In both cases: if **exactly one** item is found, it is used; if **several** are found, the user selects manually; if **none** is found, the system creates a new semi-finished item from the **Semi Finished Item Template**. |

**Process reference.** The search is executed during **Split Order**. Hit determination relies on the
target values stored in the **Material Property Changes** and the material properties of the
component. Cross-link: *Daily Work on the Production Order*.

### Set up the Transfer of Semi-Finished Components

**Who and when.** The administrator sets up the logistics once, before the first split
production order is posted. It defines **between which locations** the semi-finished material is moved
and how the automatically created **Transfer Orders** are posted. The setup is consumed
in daily operation when posting the output and the transfer receipt.

**Numeric order of the setup steps:**

1. **First** store a **Location** per work center (field **Location** on the work center) as well as
   the production bin (To-Production bin). If the source and destination locations are
   different, the system creates a transfer; if they are identical, the transfer is omitted and
   the **Semi Finished Finish Operation Option** is automatically reset to **(blank)**.
2. **Then** set up a **Transfer Route** with **In-Transit Code** for each required location combination.
   If the route's in-transit code is missing, no transfer order can be created.
3. **Next** store the number series for transfer orders in the Inventory Setup. Without this
   number series, the automatic creation of the transfer order is aborted.
4. **Per semi-finished operation**, set the **Semi Finished Finish Operation Option** (see table below), so that
   the operation is correctly completed at the transfer receipt.
5. **Finally**, in daily operation the transfer is processed automatically when the output is posted.

**Semi Finished Finish Operation Option** (on the operation or prod. order routing line):

| Field | Explanation |
|---|---|
| **Semi Finished Finish Operation Option** | Defines how the last semi-finished operation is completed when the created semi-finished material is delivered to the next location via a transfer. Only editable if the line is marked as a **Semi-Finished Item**. It requires that the **Location** of the operation differs from the location of the work center – otherwise the message "The Location Code between the Routing Line and Work Center has to be different" appears. |

**Values (complete):**

- **(blank):** The operation is **not** completed by the transfer receipt; the status results
  from the normal feedback. It is set automatically when the operation and
  work center location are identical (no transfer needed).
- **When posting the transfer receipt:** If set, the operation is automatically set to **Finished**
  as soon as the **transfer receipt** is posted and the received quantity covers the remaining quantity of the
  **prod. order component**. Thus the physical goods receipt at the destination location simultaneously completes
  the operation.

**Validation/dependency.** The transfer is only created for components whose location differs from the
work center location. For subcontracted (external) operations with a stored
vendor number, the module controls the posting of the transfer differently (no automatic posting as long as
the subsequent operation is also subcontracted). Cross-link: *Transfer, Inventory and Following Orders*.

### Permissions

For access to the objects of this module, the extension provides the permission set **MuM SF All**
(caption "All permissions"). This permission set determines the read, write, modify
and delete rights for the tables, pages and codeunits of the semi-finished item module and defines which
actions users may perform in the module. It must be assigned to a role or a user before working with
the semi-finished item split.

---

## Master Data

The master data of this module consists of markings and assignments on existing manufacturing and
item master data as well as two dedicated maintenance pages (**Material Properties** and
**Material Property Changes**). They control which objects are treated as a semi-finished stage and with
which target values semi-finished items are created.

### Work Center as Semi-Finished Station

**Entry point:** Work Centers (list) → **Work Center** (card).

**Process reference.** The administrator marks those work centers at which semi-finished items
are created. This marking is the basis for the associated operations in the routing to be treated as
semi-finished items and to be split at the **Split Order**. The marking is automatically transferred from the
work center to operation and prod. order routing lines.

| Field | Explanation |
|---|---|
| **Semi-Finished Item** | If activated, this work center is treated as a semi-finished station: New operation lines with this work center automatically receive the semi-finished marking, and the associated production order is extended by its own semi-finished stage at the **Split Order**. Without this marking, the work center remains a normal capacity resource without automatic semi-finished creation. |

**Action on the card:**

- **Material Properties** – opens the maintenance list of the material properties for this work center
  (only active if **Semi-Finished Item** is set). See *Maintaining Material Properties*.

**Delete behavior.** If a work center is deleted, the system automatically removes the associated
**Material Properties**.

#### Maintaining Material Properties

**Entry point:** Work Center card → action **Material Properties** (opens the page
**Material Properties**; the page is not reachable via **Tell Me** and is called exclusively via this
action).

**Process reference.** Here the administrator defines, per work center, the translation from the
**Component Material Type** into the **Semi-Finished Material Type** and the relevant **Property**. This
assignment controls which properties are transferred from the input material to the semi-finished item at
the **Split Order**.

| Field | Explanation |
|---|---|
| **Component Material Type** | Defines the material type of the incoming component for which this rule applies. At the **Split Order**, this material type determines which component properties are drawn upon. |
| **Semi-Finished Material Type** | Defines the material type of the semi-finished item to be created. When searching for or creating the semi-finished item, this material type is used; the property values are checked against its permitted limits. |
| **Property** | Determines the specific property (property code) that is mapped from the component to the semi-finished item. The selection is restricted to the properties of the chosen **Semi-Finished Material Type**. |

**Validation.** If the administrator changes **Component Material Type**, **Semi-Finished Material Type** or
**Property** of an already used line, the system automatically deletes the dependent
**Material Property Changes** so that no conflicting target values remain.

### Material Type as Semi-Finished Stage

**Entry point:** Material Types (list) → **Material Type** (card) → tab **General**.

**Process reference.** Per material type, the administrator stores the item template from which new
semi-finished items are created, if no matching item is found at the **Split Order**.

| Field | Explanation |
|---|---|
| **Semi Finished Item Template** | Defines the item template (configuration template for items) from which a new semi-finished item is created when the property search returns no existing item. If stored, the new item is created with the number series and the default values of the template, marked as a **Semi-Finished Item** and filled with the determined property values. Without a template, no new semi-finished item can be created automatically. Only enabled item templates are permitted. |

### Operations and Material Property Changes

**Entry point:** **Routing** (card) → subpage **Routing Lines**.

**Process reference.** At the operation level, the administrator decides which operation creates a
semi-finished item, how it is completed at the transfer receipt, and which target values the
semi-finished item should receive.

| Field | Explanation |
|---|---|
| **Semi-Finished Item** | If activated, this operation creates its own semi-finished stage at the **Split Order**. When activating, the system automatically creates the associated **Material Property Changes** (empty target values per property of the work center); when deactivating, these are removed again. The value is set automatically from the work center's marking when the work center is applied. |
| **Semi Finished Finish Operation Option** | Controls the completion of the operation via the transfer receipt (for values see *Setup → Set up the Transfer of Semi-Finished Components*). Only editable if **Semi-Finished Item** is set. |

**Action on the operation line:**

- **Material Property Changes** – opens the target value maintenance for this operation (only active if
  **Semi-Finished Item** is set; the page is not reachable via **Tell Me** and is opened exclusively
  via this action).

**Delete behavior.** If an operation line is deleted or the semi-finished marking is removed, the
system deletes the associated **Material Property Changes**.

#### Capturing Material Property Changes

**Entry point:** Operation line → action **Material Property Changes** (page
**Material Property Changes**).

**Process reference.** Here the administrator defines the concrete **target values** per property with which the
semi-finished item is searched for or created. The lines are created automatically from the material properties
of the work center; the administrator adds the values.

| Field | Explanation |
|---|---|
| **Component Material Type** | Shows the material type of the component (not editable); serves the assignment of the property. |
| **Semi-Finished Material Type** | Shows the material type of the semi-finished item (not editable); determines the permitted properties and value limits. |
| **Property** | Shows the property (not editable) whose target value is captured. |
| **Value** | Defines the target value of the property for the semi-finished item. For numeric properties the value is checked against **Value Permitted From/To** and formatted type-correctly; for properties with value lists (**Use Property Values**) the value must be contained in the value list, otherwise "Value … is not allowed/found in Property Values!" appears. |
| **Property Value Name** | Shows the plain-text name for the entered value (from the value list; not editable). |
| **Unit of Measure** | Shows the unit of measure of the property (not editable). |
| **Value Permitted From** | Defines the lower limit for numeric target values. If set, the system rejects values below this limit. |
| **Value Permitted To** | Defines the upper limit for numeric target values. If set, the system rejects values above this limit. |

**Values by data type (property).** The underlying **Data Type** of the property determines the
check of the **Value** field:

- **Text:** Free text; no numeric limit check. If property values are enabled, the text must be in the
  value list.
- **Decimal:** The value must be a valid decimal number and lie within **Value Permitted From/To**;
  otherwise the error "must not be less than …/must not be larger than …".
- **Integer:** Like Decimal, but rounded to a whole number.
- **Date:** The value must be a valid date ("cannot be converted to …").

### Item as Semi-Finished Item

**Entry point:** Items (list) → **Item Card** → FactBox **Item**.

**Process reference.** Semi-finished items are usually created automatically at the **Split Order** and
marked in the process. On the item card the marking is visible and – for manual master data maintenance –
settable.

| Field | Explanation |
|---|---|
| **Semi-Finished Item** | If activated, this item is marked as an automatically created or maintained semi-finished item. The marking flows into the lot information and is taken into account in the property search. On automatic creation, the system sets the marking and lifts the temporary block (**Blocked**) of the new item again after the creation is completed. |

### Lot as Semi-Finished Item

**Entry point:** **Lot No. Information Card** → tab **General**.

**Process reference.** For traceability, the module also marks lots as semi-finished items.

| Field | Explanation |
|---|---|
| **Semi-Finished Item** | If activated, this lot belongs to a semi-finished item. The system sets the marking automatically when the item ledger entry is created: on an **output** from a semi-finished production order based on the prod. order line, otherwise based on the item master. This allows semi-finished lots to be identified in the lot information and in evaluations. |

---

## Daily Work on the Production Order

The operational work takes place on the **Production Order**. The relevant actions and additional fields of this
module are controlled by the setup described above: The **semi-finished marking** of the
work centers and operations, the **Material Property Changes** per operation, the
**Split Option** in the routing as well as the **transfer logistics** (locations, routes, in-transit code)
determine when and how the system splits, searches/creates and transfers. Cross-link: *Setup* and
*Master Data*.

### Create and Split a Production Order (Split Order)

**Entry point:** **Firm Planned Production Order** or **Released Production Order** → action area
**Functions** → **Split Order**.

**Important rule.** A **Released Production Order** with semi-finished operations that have not yet been split
is not permitted. If the system tries to calculate such an order,
this appears: "You are not allowed to create Released Production Order with Routing Lines that cointains
Work Center that will produce Semi-Finished Item. Please Create Firm-Planned Order." Therefore first create a
**Firm Planned Production Order**.

**Sequence of the split (what first / what next):**

1. **First** create the firm planned production order with item, quantity, routing and components,
   or generate it from the sales order and refresh it.
2. **Then** trigger the split:
   - **Automatically** with **Split Option = On Sales Release**, as soon as the sales order is
     released,
   - **automatically** with **Split Option = On Prod. Order Release**, as soon as the production order is
     released,
   - **manually** via the action **Split Order**. If there are no splittable lines, the system reports
     "There are no lines to be splitted.".
3. **Result:** The system creates its own **production order line** per semi-finished stage, copies or
   finds the matching **routing**, searches for or creates the **semi-finished item** (property search or
   **Semi Finished Item Template**), creates the **prod. order components** of the following stages, creates the
   **Transfer Orders** and sets the marking **Splitted Lines** on the production order.

**Manual item selection.** If the property search returns **several** hits, the system opens the
item list for the manual selection of the semi-finished item; for **one** hit it is used automatically,
for **no** hit a new item is created from the template.

### Operations and Additional Fields in the Prod. Order Routing

**Entry point:** Production Order → line → **Operations** (prod. order routing).

In the prod. order routing, the semi-finished additional fields are visible and the target value maintenance is reachable.

| Field | Explanation |
|---|---|
| **Semi-Finished Item** | Indicates (not editable) that this operation creates a semi-finished item. Results from the work center or the routing. |
| **Semi Finished Finish Operation Option** | Controls the completion of the operation via the transfer receipt (values as in the setup). Only editable if **Semi-Finished Item** is set. |

**Action:** **Material Property Changes** – opens the (order-related) target values of the operation
(page **Material Property Changes**). These contain the same fields as in the master data
(Component Material Type, Semi-Finished Material Type, Property, Value, Property Value Name, Unit of Measure, Value
Permitted From, Value Permitted To) and are taken over from the master data at the **Split Order**.

### Create Following Semi-Finish Order

**Entry point:** **Released Production Order** → action area **Functions** →
**Create Following Semi-Finish Order**.

**Process reference.** When a semi-finished operation is completed (last operation of the semi-finished line
with status **Finished**) and remaining quantity is still open, this action opens the **Prod. Order Line overview**
of the affected semi-finished lines, from which the following order for the further production is triggered or
selected. This is how you continue the production of the next stage without losing the connection to the
originating order.

---

## Transfer, Inventory and Following Orders

The material flow between the work centers takes place via automatically created **Transfer Orders**.
This chapter describes what happens on posting and which additional fields link the transfer lines with the
production order.

### Automatic Transfer When Posting the Output

**Sequence (what first / what next):**

1. **First** the user posts the **output** of a semi-finished operation (production journal or
   output posting).
2. **Then** the module automatically determines the associated **transfer lines** (link via the
   additional fields, see below), reserves the lot and posts – depending on the location setting – either via
   **Warehouse Shipment/Receipt** or directly the **Transfer Shipment** and **Transfer Receipt**.
3. **Next** the **prod. order component** of the following stage is moved to the destination location (and bin);
   for lot-tracked items the lot is passed through via the reservation.
4. **Finally** the system sets the operation to **Finished** – with **Semi Finished Finish Operation Option = When
   posting the transfer receipt** and sufficient received quantity.

**Partial quantities.** Partial outputs and partial deliveries are permitted; the module processes the
respective posted quantity and only closes the operation once the received quantity covers the remaining quantity of the
component. There is no artificial lock "close only on complete quantity balancing".

### Link Fields on the Transfer Line

The following fields connect a **transfer line** with the triggering production order and are set by the
system (not editable):

| Field | Explanation |
|---|---|
| **Semi-Finished Item Prod. Order No.** | Shows the production order from which this transfer originated. This uniquely assigns the transfer to the semi-finished process. |
| **Semi-Finished Item Prod. Order Line No.** | Shows the production order line (semi-finished stage) to which the transfer belongs. |
| **Semi-Finished Item Prod. Order Component Line No.** | Shows the prod. order component that is delivered to the destination location by this transfer. |

### Internal Origin and Control Fields (Traceability)

For the internal chaining of the semi-finished stages, the module maintains additional, system-set fields on the
production order and operation lines. They are relevant for traceability and
are not maintained manually:

| Field | Explanation |
|---|---|
| **Semi-F. Source Line No.** (prod. order line) | References the original production order line from which the semi-finished stage was derived. |
| **Splitted Lines** (production order) | If activated, this production order has already been split; a renewed automatic split is omitted. |
| **Semi Finished Next Operation No.** / **Semi Finished Prev. Operation No.** (prod. order routing) | Chain the semi-finished operations in their order and control when the last operation of the stage is reached. |
| **Next Semi Finished Prod. Order Line No.** (prod. order routing) | References the following production order line to which the material is transferred. |

---

## History, Tracing and Markings

The module does not maintain its own history or log pages. Tracing relies on
markings on existing master data and documents:

- **Lot No. Information Card – Semi-Finished Item:** marks lots that originate from semi-finished items
  (set automatically when posting the item ledger entry). This is how you identify semi-finished lots in the
  lot evaluation.
- **Routing Card – Splitted Routing / Original Routing No.:** marks automatically created
  (split) routings and their origin.
- **Production Order – Splitted Lines:** shows that a production order has already been split.
- **Transfer Line – Semi-Finished Item Prod. Order No./Line No./Component Line No.:** connect each
  transfer with its origin in the production order.

Via these fields, the entire path from the originating order through the created semi-finished items and the
transfers up to the following stage can be traced.

---

## FAQ and Troubleshooting

### Why am I not allowed to create a released production order with semi-finished operations?

Because the split must take place on a firm planned order. If a released order to be calculated contains
operations with semi-finished work centers, the system aborts with a corresponding message
and demands a **Firm Planned Production Order**. Create the order firm planned, split it,
and only release it afterwards.

### Why does Split Order report "There are no lines to be splitted."?

Because there are no operations marked as **Semi-Finished Item** (with a valid
work center) in the order. Check whether the work center is marked as **Semi-Finished Item**
and whether the relevant **operation lines** have adopted the marking.

### When does the system split automatically, and when do I have to trigger Split Order manually?

That depends on the **Split Option** in the routing header: **On Sales Release** splits on release of the
sales order, **On Prod. Order Release** on release of the production order. If the option is **(blank)**,
no automatic split takes place – then you trigger **Split Order** manually.

### How does the system know which semi-finished item it should use?

It searches for a matching item based on the target values stored in the **Material Property Changes** and the
component properties. For **one** hit it is used, for
**several** hits the item list appears for selection, for **no** hit a new item is created from the
material type's **Semi Finished Item Template**.

### What happens if I have not stored a Semi Finished Item Template?

If the search finds no existing item and no **Semi Finished Item Template** is stored on the material type,
no new semi-finished item can be created – the split then delivers no item for this stage.
Store an enabled item template per material type.

### Why can I not set the Split Option in the routing?

The option is only settable if the routing is **not certified**, is **not** a split routing
(empty **Original Routing No.**) and at least one operation line marked as a **Semi-Finished Item**
exists. Otherwise "Cannot find a semi finish routing line!" appears.

### Why do I get "The Location Code between the Routing Line and Work Center has to be different"?

Because the **Semi Finished Finish Operation Option** is only meaningful if material is actually transferred.
If the operation location and work center location are identical, no transfer is needed and the
option is not allowed or is reset to **(blank)**.

### When is a semi-finished operation automatically set to "Finished"?

When the **Semi Finished Finish Operation Option = When posting the transfer receipt** is set and the
posted received quantity of the transfer covers the remaining quantity of the **prod. order component**. Then the system sets the
operation to **Finished** when posting the transfer receipt.

### Why is a property's value rejected?

For numeric properties the **Value** must lie within **Value Permitted From/To** and be convertible into the
correct data type; for properties with **Use Property Values** the value must be in the
stored value list. Otherwise messages such as "must not be less than …", "must not be larger than
…" or "Value … is not allowed/found in Property Values!" appear.

### How do I recognize which lots and routings originate from the semi-finished creation?

Via the markings: **Lot No. Information Card → Semi-Finished Item** for semi-finished lots as well as
**Routing Card → Splitted Routing / Original Routing No.** for automatically created routings.
On the production order, **Splitted Lines** indicates that the split has already taken place.

---

## Typical Use Cases

The following scenarios show the process from the users' perspective. Every screen and every action is stored in the
module's code.

### Use Case 1: Customer Order with Multi-Level Semi-Finished Item

**Trigger.** A customer orders an item by phone whose production runs through several semi-finished stages at
different work centers.

**Entry point in BC.** Sales creates the **Sales Order**. A **Production Order** is created from the
order line. Prerequisite: The routing of the item contains semi-finished operations,
the work centers are marked as **Semi-Finished Item** and the **Material Property Changes**
are maintained (see *Setup* / *Master Data*).

**Core sequence.**
1. The routing header carries **Split Option = On Sales Release**.
2. With the **sales release**, the system splits the production order automatically (**Split Order**): one
   production order line per semi-finished stage, matching semi-finished item searched for or created from the
   **Semi Finished Item Template**, **prod. order components** and **Transfer Orders** created.
3. The production planner releases the order and posts the **output** per operation.
4. When posting, the **transfer** is processed automatically; the last semi-finished operation is set to
   **Finished** at the **transfer receipt** (**Semi Finished Finish Operation Option = When posting the
   transfer receipt**).

**Completion.** When needed, the user starts the following stage via **Create Following Semi-Finish Order**. The
resulting semi-finished lots can be recognized as **Semi-Finished Item** on the **Lot No. Information Card**.

### Use Case 2: Manual Split of a Firm Planned Order

**Trigger.** The work planner proactively creates a production order for a stock item, without
reference to a sales order.

**Entry point in BC.** Create a **Firm Planned Production Order**, capture item/quantity/routing and
refresh it.

**Core sequence.**
1. The routing carries **Split Option = (blank)** or **On Prod. Order Release**; the user wants to trigger the
   split in a controlled manner himself.
2. Via **Functions → Split Order** the split is triggered. If there are no semi-finished operations
   present, the system reports "There are no lines to be splitted.".
3. If the property search returns several matching semi-finished items, the user selects the desired one in the
   item list.
4. The system creates semi-finished lines, components and **Transfer Orders**; on the order,
   **Splitted Lines** is set.

**Completion.** The order is released and posted as in Use Case 1.

### Use Case 3: Post Output and Complete the Operation via the Transfer Receipt

**Trigger.** At a semi-finished work center a partial quantity is finished and is to be passed on to the next
location.

**Entry point in BC.** The worker posts the **output** of the semi-finished operation (production journal or
output posting on the Released Production Order).

**Core sequence.**
1. When posting the output, the module determines the associated **transfer** and posts – depending on the
   location settings – shipment and receipt automatically.
2. The **prod. order component** of the following stage is moved to the destination location; the lot is passed
   through via the reservation.
3. If the received quantity covers the remaining quantity of the component and **Semi Finished Finish Operation Option =
   When posting the transfer receipt** is set, the operation is set to **Finished**.

**Completion.** Partial quantities are correctly updated; the operation only closes once the remaining quantity is
covered. Via the transfer lines (**Semi-Finished Item Prod. Order No.** etc.) the reference to the
production order remains traceable.
