---
title: Anwenderhandbuch m+m Ext. Production Information
---

# User Guide m+m Ext. Production Information

## Introduction

The app **m+m Ext. Production Information** extends Microsoft Dynamics 365 Business Central with **extended production properties** and with **material tracking** along the production chain. Production-related additional information — such as temperatures, times, programs, test values or texts — is stored on **Work Centers** and **Routings** and then accompanies the item through **Sales Quote**, **Sales Order**, **Purchase Order**, **Production Order** and **Production Journal** all the way into the **Capacity Ledger Entries**.

**Target audience:** The module is primarily aimed at **operational users** in sales, purchasing and production who capture document lines, calculate production orders and post in the **Production Journal** on a daily basis. Secondarily, it is aimed at **administrators and production planners** who set up the master data (Work Centers, Routings, Material Types) and the automatic routing determination.

**Short process overview:** For each **Work Center** and each **Routing** operation, the administrator stores the desired properties and their **Default Values**. Via the **Material Type**, a **Master Routing No.** is assigned so that Business Central can automatically determine the appropriate **Routing** and its properties when a sales or purchase line is captured. The sales user opens the **Ext. Prod. Properties** from the document line and adjusts values. When a **Production Order** is created from the order, Business Central takes over the routing and properties; when posting in the **Production Journal**, the values are transferred into the **Capacity Ledger Entries** and permanently documented there.

> Note on terminology: In this guide, **Work Center** refers to the capacity-bearing group, **Machine Center** to the individual machine capacity, **Lot** to lot-based batch tracking and **Transfered** to the flag of a material tracking line that has already been handed over to production.

---

## Quick start for users

The quick start follows the sequence enforced by the code: first setup and master data, then working with documents, and finally posting.

1. **Setup/master data (one-time, administrator).**
   1. Open the **Material Type** and enter the **Master Routing No.** in the **Ext. Prod. Properties** group; if required, enable **Use Material Tracking for Sales**.
   2. Open a **Work Center** and use the **Ext. Properties** FactBox with **Edit** to capture the properties and their **Default Value**.
   3. Flag properties whose result must be captured before posting with **Mandatory Actual Value**.
2. **Capture a sales line (sales user).** Create an item line in the **Sales Order**. Business Central sets the **Routing No.** automatically (from item, item reference or master routing). Use the line action **Ext. Prod. Properties** to open the editor and adjust values.
3. *(optional)* **Assign a lot.** If **Use Material Tracking for Sales** is active on the Material Type, assign lots via the material search; the assignment appears in **Material Tracking Entries** (line action).
4. **Create a production order.** Release the sales order and create the **Production Order**. When calculating the production order, Business Central takes over the **Routing**, the **Ext. Prod. Properties** and — if present — the material tracking as components.
5. **Post in the Production Journal.** Open the **Production Journal** for the production order and post via **Posting → Post**. If the **Actual Value** is missing for a property flagged with **Mandatory Actual Value**, Business Central aborts with a message.
6. **Check the result.** After posting, you will find the transferred properties as **Ext. Prod. Properties** in the FactBox of the **Capacity Ledger Entries**.

---

## Setup

The setup of this module consists less of a classic setup page than of a **multi-stage master data and activation chain**. The actual control resides in the master data (Material Type, Work Center, Routing, Item Reference). This chapter first describes the setup page and then the two activation chains.

### Ext. Prod. Properties Setup

**Access:** via the global **Tell Me** function (Administration category).

The **Ext. Prod. Properties Setup** page is a company-wide setup page (one record per company). In the shipped version it contains **no configurable fields**; it merely creates the technical setup record as soon as it is opened for the first time. Therefore no field values need to be maintained. The entire functional configuration is done via the master data of the following sections.

> Permissions: The included permission set **MuM AP Permission** determines the permissions for all tables, pages and codeunits of the module. It defines which actions users can perform on the material tracking entries, the property data and the sales-production link. Assign it to the roles that work with extended production properties.

### Set up automatic routing determination

**Process intro.** This chain is set up once by the **administrator/production planner** before the first document is captured. It ensures that the correct **Routing** is drawn automatically when a sales or purchase line is created, without the user having to select it manually. The chain is consumed in the **daily work in sales and purchasing** (see the section there on the **Routing No.**).

**Numbered setup steps (in dependency order):**

1. **Maintain the Material Type.** Open the **Material Type** and enter the **Master Routing No.** in the **Ext. Prod. Properties** group. When set, Business Central uses this routing as a fallback value as soon as no routing is stored for an item, neither on the item nor on an item reference. Without an entry and without a routing on the item, calling the properties reports **No Routing found/set!**.
2. **Assign the item to the Material Type.** Assign the **Material Type** to the item (field on the item card from the m+m Material Properties module) and, if necessary, store a **Routing** on the item itself. If a routing is set on the item, it takes precedence over the master routing.
3. *(optional)* **Customer-specific item reference.** Store a differing **Routing No.** in the **Item Reference** (reference type Customer). When set, this routing is preferred for documents of this customer (order: Item Reference → Item → Master Routing).
4. **Result in the document line.** In **Sales Order**, **Sales Quote** and **Purchase Order**, the **Routing No.** is set automatically when the item line is captured. The routing must have the status **Certified**; otherwise no property structure can be generated.

**Validation/dependency note:** The Material Type enforces the **Master Routing No.** only when no other routing can actually be determined. The item reference allows a differing Routing No. only with **Reference Type Customer**.

### Set up maintaining extended production properties (master data)

**Process intro.** The **administrator/production planner** defines once which properties are maintained on which capacity and with which **Default Values**. These values are inherited into the sales/production lines in daily work and adjusted there if necessary (cross-link: **Daily work** and **Production Order and Production Journal**).

**Numbered setup steps (in dependency order):**

1. **First** store the default values on the **Work Center** (see Master Data → *Work Center*). If a **Default Value** is set here, it is automatically taken over into **Value** and serves as a default for all operations of this capacity.
2. **Then** check each **Routing** operation (see Master Data → *Routing*): Business Central takes the operation's properties preferably from the routing; if it finds none there, it inherits them from the assigned **Work Center**.
3. **Finally** flag the properties whose result the worker must capture before posting: set the **Mandatory Actual Value** field. When enabled, Business Central checks during posting in the Production Journal that an **Actual Value** is present for every such property.

**Operational conclusion:** The worker enters the **Actual Values** in the **Production Journal** and posts; without an actual value for a mandatory property, the posting is rejected (cross-link: **Production Order and Production Journal**).

### Set up material tracking in sales

**Process intro.** This optional chain activates the lot-precise reservation of raw material in sales and its handover to the production order. It is used above all in the steel/lot environment and consumed in daily work via the **Material Tracking Entries**.

**Numbered setup steps:**

1. **Activate the Material Type.** Set the **Use Material Tracking for Sales** flag on the **Material Type**. When enabled, Business Central replaces the standard lot assignment with this module's material tracking when lots are assigned via the material search in sales; the assigned lots are stored as **Material Tracking Entries** on the sales line. Without the flag, Business Central's standard lot assignment remains active.
2. **Assign a lot in sales.** The user assigns lots in the sales line via the material search (see **Daily work**). The assignment lands quantity-precise — for bin-mandatory locations by **Bin Code** — in the **Material Tracking Entries**.
3. **Handover to the production order.** When the production order created from the sales order is calculated, the material tracking entries not yet **transfered** are created as **Production Order Components** and, if no purchase order assignment exists, reserved by **Lot No./Serial No.**. Afterwards the entry is flagged as **Transfered**.

---

## Master Data

### Work Center: Ext. Properties and default values

**Process intro.** Here the administrator defines which properties a **Work Center** basically brings along and with which **Default Value**. These default values are the basis for all routings that use this capacity and are inherited all the way into sales and production.

**Access:** Open the **Work Centers** via the global **Tell Me** function. You can maintain the properties in two ways: in the **Work Centers** list via the **Ext. Properties** FactBox, or in the individual work center. In the FactBox, choose **Edit** to open the editor in which properties are captured, changed or deleted.

The editor (**Ext. Prod. Properties**) shows the following fields for the work center:

| Field | Explanation |
|---|---|
| **Property Code** | When set, this code assigns a defined property from the property master to the capacity; editable only at master data level (Work Center). |
| **Default Value** | If a value is set, it is automatically taken over into **Value** and serves as a default for all operations and documents that inherit this property. |
| **Property Value Name** | Shows the plain-text name of the currently stored value (e.g. for value-list-based properties); serves for control and is not captured manually. |
| **Mandatory Actual Value** | When enabled, the associated **Actual Value** must be filled in the Production Journal before posting; if it is missing, the posting is rejected. Without the flag, the actual value is optional. |
| **Value Allowed From** | When set (only for numeric properties), this value limits the allowed lower bound; captured values below it are rejected. |
| **Value Allowed To** | When set (only for numeric properties), this value limits the allowed upper bound. |
| **Unit of Measure** | Shows the unit of measure of the property; ensures unambiguous interpretation of numeric values in document and entry. |
| **Calculation Formula** | When stored (only for numeric properties), the value is calculated automatically and the **Value** field is locked. Use the assist edit to open the formula builder. |
| **Display Order** | Controls the sorting of the properties in all views; lower values appear first. |
| **No.** / **Description** / **Type** | Show the assigned capacity (number, name and **Type** — Work Center or Machine Center); not editable, serve to assign the value to the operation. |
| *(hidden helper fields)* **Data Type**, **Use Property Values** | Internally control the field properties (numeric/text, value list) and are not maintained directly; they determine whether **Value Allowed From/To** and the calculation formula are editable. |

**Process step:** For each capacity, capture the required properties and their **Default Value**; set **Mandatory Actual Value** where the result must later be posted mandatorily. These values are then inherited into routing, sales and production (cross-link: **Routing**, **Daily work**, **Production Order and Production Journal**).

### Routing and Routing Version: properties per operation

**Process intro.** On the **Routing** (and per **Routing Version**), the inherited properties become visible per operation and can be overridden operation-specifically. This allows differing specifications per production step to be stored without changing the master values of the capacity.

**Access:** Open the **Routings** via the global **Tell Me** function and call a routing via the **No.**. On the right-hand side, the **Ext. Properties** FactBox shows the properties of the selected operation. For versioned routings, this applies analogously in the **Routing Version**.

The **Ext. Properties** FactBox shows (read-only) per operation:

| Field | Explanation |
|---|---|
| **Property Name** | Shows the name of the property that applies to this operation. |
| **Default Value** | Shows the default value inherited from the work center (visible only for capacity properties). |
| **Value** | Shows the currently valid value; if it differs from the **Default Value**, it is highlighted in color so that adjusted values are immediately recognizable. |
| **Mandatory Actual Value** | Indicates whether an actual value is mandatory for this property in the Production Journal. |
| **Actual Value** | Shows the captured actual value (visible only in the posting-related views). |
| **Unit of Measure** | Shows the unit of measure of the property. |

**Inheritance logic (from the code):** When creating/changing an operation, Business Central takes the properties preferably from the **Routing**; if it finds none there, it inherits them from the assigned **Work Center** or the **Machine Center**. When copying routing lines, the properties of the source routing are carried along. If a routing line is deleted, the associated properties are removed.

### Material Type: master routing and material tracking

**Process intro.** The **Material Type** (master data from m+m Material Properties) controls two behaviors of this module: the automatic routing determination and the lot-precise material tracking in sales. The administrator maintains it per material type before items of this type are used in documents.

**Access:** Open the **Material Types** and there the card of a material type; the additional fields are located in the **Ext. Prod. Properties** group.

| Field | Explanation |
|---|---|
| **Master Routing No.** | When set, Business Central uses this routing as a fallback value as soon as no routing is stored for an item of this material type, neither on the item nor on an item reference; only then can extended production properties be generated at all in sales/production. Without an entry and without a routing on the item, calling the properties remains without a structure (message **No Routing found/set!**). |
| **Use Material Tracking for Sales** | When enabled, this module takes over the lot assignment in sales: lots assigned via the material search are stored as **Material Tracking Entries** on the sales line and later handed over to the production order components. Without the flag, Business Central's standard lot assignment remains effective. |

> The remaining fields of the Material Type card (e.g. **Material Type Code**, **Description**) belong to the base module m+m Material Properties and here serve only to identify the material type; they are not relevant for the two controls mentioned above.

### Item Reference: customer-specific Routing No.

**Process intro.** Via the **Item Reference**, the administrator stores a differing routing per **Customer** when a customer orders the same item with a different production sequence.

**Access:** Open the **Item References** for the item (list or entries); the additional column is at the end of the line.

| Field | Explanation |
|---|---|
| **Routing No.** | When set, this routing is determined preferentially for document lines of this customer, ahead of the item's routing and the master routing. The value is allowed only with **Reference Type Customer**; only **certified** routings are permitted. |

---

## Daily work in sales and purchasing

Daily work takes place in the standard documents; this module adds a column and line actions there. Which values appear is preconfigured via the **Master Data** (Work Center, Routing, Material Type) and the **Setup** (automatic routing determination) — see the corresponding sections above.

### Sales Quote and Sales Order

**Access:** Open the **Sales Order** (or the **Sales Quote**) via the global **Tell Me** function and capture an item line.

In the document line, the module adds the **Routing No.** column and, in the line menu bar, two actions:

| Field/Action | Explanation |
|---|---|
| **Routing No.** (column) | When you create an item line, Business Central sets the Routing No. automatically (Item Reference → Item → Master Routing of the Material Type). If you change the Routing No. manually and extended production properties already exist for the line, Business Central asks **Existing ext. Prod. Properties will be deleted. Continue?**; if you confirm, the old properties are discarded and the routing version is drawn anew. |
| **Ext. Prod. Properties** (action) | Use the action to open the **Ext. Prod. Properties Editor**. On the first call, Business Central generates the property structure from the routing (per operation, with inherited default values). You adjust the **Values**; differing values are highlighted. Prerequisite: line type **Item** and a set **No.**; the action is available only in **Quote** and **Order**. |
| **Material Tracking Entries** (action) | Use the action to open the line's **Material Tracking Entries** (see chapter *History*). Here you see the quantities assigned to the lots. |

**Status dependency:** If the line is coupled to a purchase order via a drop shipment or a special order reference, the editor opens **read-only**, because the properties are then controlled by purchasing.

### Purchase Order

**Access:** Open the **Purchase Order** and capture an item line.

| Field/Action | Explanation |
|---|---|
| **Routing No.** (column) | Determined automatically when the item line is captured (Item Reference → Item). For drop shipment/special order, the Routing No. is taken over from the associated sales line instead. |
| **Ext. Prod. Properties** (action) | Opens the editor for the purchase line. Prerequisite: document type **Quote** or **Order**, line type **Item**, a set **No.**, and the line must not be a drop shipment/special order (otherwise read-only, unless the intercompany status is **New**). |

> For **drop shipment** or **special order**, Business Central automatically transfers the extended production properties from the linked sales line into the purchase line when the purchase line is inserted/changed; the purchase line itself then does not allow a manual routing change.

### Ext. Prod. Properties Editor (document line)

The editor opened from the document line displays the properties **in a tree** per operation. It contains the same fields as the master data editor, with the following particularities for working with documents:

| Field | Explanation |
|---|---|
| **Operation No.** | Shows the operation to which the properties indented below it belong; the main line per operation is highlighted. |
| **Description** | Shows the name of the operation or the property. |
| **Sequence** | When editable, it determines the later sequence of the operations in the production order; changeable only on the operation's main line and only as long as no production order operations exist yet. |
| **Value** | The value of the property that can be captured by the user; locked when a **Calculation Formula** is stored. Deviations from the **Default Value** are highlighted. |
| **Source** | Shows where the property originates. **Purchase:** taken over from a purchase line. **Sales:** taken over from a sales line. **Routing:** directly from the routing operation. **Work Center:** inherited from the capacity. |

**Editability:** For a **finished** production order as well as for read-only opened documents, the editor is not editable.

---

## Production Order and Production Journal

### From the Sales Order to the Production Order

When a **Production Order** is created from a released **Sales Order** and calculated, Business Central automatically performs several steps of this module (verified in the code):

1. **Take over the routing.** If a **Routing No.** is set on the sales line, it is transferred together with the **Routing Vers. Code** to the production order line.
2. **Build operations from the sequence.** If no operations exist yet for the production order line, Business Central creates them from the **Sequence** stored in the properties and calculates the operation costs.
3. **Inherit properties.** The extended production properties of the sales line are taken over into the production order line.
4. **Hand over material tracking.** Material tracking entries of the sales line that are not **transfered** are created as **Production Order Components**; without a purchase order assignment, a reservation is made per **Lot No./Serial No.**. Afterwards the material tracking entry is flagged as **Transfered**.

When changing the status of the production order (e.g. from *Planned* to *Released*), the properties and the sales-production link are moved along; when a production order line is deleted, the associated properties are removed and handed-over material tracking entries are released again.

Via the lines of the **Production Order Lines** (in all statuses: *Simulated*, *Planned*, *Firm Planned*, *Released*, *Finished*), the **Ext. Prod. Properties** action is available to view the properties of the line or — except for *Finished* — to adjust them.

### Ext. Properties on the Production Order Routing

On the **Prod. Order Routing** page, the **Ext. Prod. Properties** FactBox shows, for each selected operation, its properties and values (read-only). This allows the production planner to check, before release, which specifications apply per operation.

### Posting in the Production Journal

**Access:** Open the **Production Journal** for the **Released Production Order** (or the corresponding actual-report journal). In the **Ext. Properties** FactBox, you see and capture the properties per operation; the **Actual Value** field is editable here.

**Posting sequence:**

1. Capture the **Actual Values** of the properties for each operation.
2. Post via **Posting → Post**.
3. **Mandatory check:** For lines of type **Work Center**, Business Central checks every property with **Mandatory Actual Value** before posting. If the **Actual Value** is missing, the posting is rejected with a message (in essence: *"Actual Value in Ext. Prod. Properties cannot be empty"* with an indication of the affected **Property Name**).
4. After successful posting, the properties and their **Actual Values** are transferred into the **Capacity Ledger Entries** (see *History*).

> Note: This module does not provide its own actions such as "Finish partially" or "Finish"; it uses the standard posting logic of Business Central. Partial postings are permitted as far as Business Central allows them; the extended properties are carried along with every posting.

---

## History: Capacity Ledger Entries and Material Tracking Entries

### Capacity Ledger Entries

**Access:** For the **Released Production Order**, open the **Capacity Ledger Entries** via **Related → Order → Entries → Capacity Ledger Entries**. In the **Ext. Prod. Properties** FactBox, you see the documented properties and **Actual Values** for each posted capacity ledger entry. This makes it permanently traceable after posting with which values an operation was actually carried out.

### Material Tracking Entries

**Access:** Open the **Material Tracking Entries** via the line action of the same name on a sales line (the page has no search entry of its own).

| Field | Explanation |
|---|---|
| **Item No.** | Shows the tracked item. |
| **Variant Code** | Shows the variant, provided the item is variant-tracked. |
| **Lot No.** | Shows the assigned lot of the raw material. |
| **Serial No.** | Shows the assigned serial number, provided it is serial-tracked. |
| **Quantity** | Shows the quantity assigned to the lot (split per bin for bin-mandatory locations). |
| **Transfered** | When enabled, the entry has already been handed over as a production order component and is not created again at the next production order calculation. |
| *(can be shown if needed)* **Location Code**, **Bin Code**, **Unit of Measure Code**, **Purchase Order No.**, **Purchase Order Line No.** | Show origin and warehouse details of the assignment; the purchase order information refers to the origin purchase order of the lot. |
| *(technical, hidden by default)* **Entry No.** and the **Source** fields (Source Type/Subtype/No./Line No. etc.) | Identify the document line to which the tracking belongs; hidden when called from the sales line, since it is already unambiguous by the context. |

---

## Typical use cases

### Use case 1: Customer order with extended production properties

**Trigger:** A customer orders a manufactured item by e-mail with special specifications (e.g. a specific length or temperature).

**Access in BC:** The salesperson opens the **Sales Order** via **Tell Me** and captures the item line. Business Central sets the **Routing No.** automatically.

**Core flow:**
1. Via the line action **Ext. Prod. Properties**, the salesperson opens the editor; Business Central generates the property structure from the routing.
2. The salesperson enters the customer specification in the **Value** field; the differing value is highlighted.
3. The order is released and a **Production Order** is created and calculated — routing, operations and properties are taken over.
4. The worker opens the **Production Journal**, enters the **Actual Values** and posts via **Posting → Post**. If a property is flagged as **Mandatory Actual Value** and the actual value is missing, Business Central prevents the posting.

**Conclusion:** In the **Capacity Ledger Entries**, the **Ext. Prod. Properties** FactBox permanently documents the values actually posted.

### Use case 2: Lot-precise material assignment in sales

**Trigger:** For an order in a lot environment, it should already be determined in sales which specific **Lot** of raw material is used.

**Access in BC:** The clerk opens the **Sales Order** and the relevant item line. Prerequisite: **Use Material Tracking for Sales** is enabled on the item's **Material Type**.

**Core flow:**
1. Via the material search, the clerk assigns one or more **Lots** to the item; the assignment is stored quantity-precise (for a bin-mandatory location by **Bin Code**) as **Material Tracking Entries**.
2. Via the line action **Material Tracking Entries**, the clerk checks the **Lot No.** and **Quantity**.
3. When creating/calculating the **Production Order**, the entries not yet **transfered** are created as **Production Order Components** and reserved per **Lot No./Serial No.**.

**Conclusion:** The material tracking entries are flagged as **Transfered**; the reserved lots are in the production order components.

---

## FAQ and Troubleshooting

### 1. Why does the message "No Routing found/set!" appear when calling the Ext. Prod. Properties?
Because no routing could be determined for the line. Business Central searches in the order **Item Reference (Customer) → Item → Master Routing No. of the Material Type**. Store a **certified** routing at one of these places.

### 2. Why can I not use a routing even though it exists?
When generating the property structure, the routing status is checked; only **certified** routings are accepted. Set the routing to **Certified**.

### 3. Why am I asked, when changing the Routing No., whether existing properties are to be deleted?
Because extended production properties already exist for the line. A new routing means a different operation/property structure; if you confirm with **Continue**, the old properties are discarded and rebuilt. If you cancel, the old Routing No. is retained.

### 4. Why can I not complete the posting in the Production Journal?
Because the **Actual Value** is missing for at least one property with the **Mandatory Actual Value** flag. Business Central checks this for lines of type **Work Center** before posting. Enter the missing **Actual Values** in the **Ext. Properties** FactBox.

### 5. Why can the "Value" field of a property not be edited?
Because a **Calculation Formula** is stored for this property; the value is then calculated automatically and the field is locked. Remove the formula in the master data editor if you want to capture the value manually.

### 6. Why is the editor of the Ext. Prod. Properties sometimes read-only?
For **finished** production orders as well as for sales/purchase lines coupled via **drop shipment** or **special order**. In these cases, the properties are controlled by the linked document and must not be changed at this point.

### 7. Why are my assigned lots managed as material tracking entries instead of as normal item tracking?
Because the **Use Material Tracking for Sales** flag is enabled on the **Material Type**. Then this module takes over the assignment and stores it as **Material Tracking Entries**, so that the lots can later be handed over to the production order components.

### 8. Why does a material tracking entry not reappear as a component?
Because it was already created as a component when calculating the production order and thereby flagged as **Transfered**. Transfered entries are not handed over twice. If the production order line is deleted, the flag is reset.

### 9. Why can I not enter a Routing No. on an item reference?
Because the Routing No. is allowed only for item references of **Reference Type Customer**. For other reference types, the field is rejected on saving.

### 10. Where do I see, after production, with which values the item was actually manufactured?
In the **Capacity Ledger Entries** of the production order. Open the Capacity Ledger Entries and show the **Ext. Prod. Properties** FactBox; there you find the posted properties with their **Actual Values**.
