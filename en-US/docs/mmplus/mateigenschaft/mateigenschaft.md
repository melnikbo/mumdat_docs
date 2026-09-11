---
title: User Guide m+m Material Properties
---

# User Guide m+m Material Properties

## Introduction

**m+m Material Properties** extends Microsoft Dynamics 365 Business Central with a freely definable property management for items, item variants as well as lots and serial numbers. Items are classified via a **Material Type**; each material type brings a set of **Properties** (e.g. material, diameter, length, standard) whose values are maintained on the item. From these properties the module automatically generates the **Description**, the **Description 2** and a technical **Matchcode**, and it enables a property-based **Material Search** in document lines.

**Target audience:** Primarily the **operational users** who work in documents every day – in Sales, Purchasing, Service and Manufacturing – and who use **Start Material Search** in the document lines to find the matching item or lot by technical characteristics and assign the quantity. The operational audience also includes the users in master data maintenance who classify items and create new base and variant items via templates. **Secondarily**, the guide addresses administrators and key users who configure the fundamentals in the **Material Property Setup**, the **Material Types** and the **Properties**.

**Short process overview.** The typical structure follows a chain from the foundation to daily work:

1. Define **Properties** (the individual characteristics and their data type).
2. Create **Material Types** and assign them properties with standard values, formulas and rules.
3. Assign **Items** to a material type – the properties are inherited, and description and matchcode are calculated.
4. In **documents**, search by properties via **Start Material Search** and transfer the hit into the line.

Within the system, the central objects carry the verified captions **Material Property Setup**, **Properties**/**Property Card**, **Material Types**/**Material Type Card**, **Property Values**, **Item Search** and **Material List**.

---

## Quick Start for Users

The quick start names the shortest path to the most important results. Setup is a prerequisite and therefore comes first.

**A – Setup (once, by the administrator):**

1. Open the **Material Property Setup** page (enter the search term **Material Property Setup** in the search and choose the link of the same name) and define on the **Matchcode** tab whether **Use Extended Matchcode Search** is active.
2. Create the required characteristics under **Properties** (Code, Name, **Data Type**).
3. Create the desired classes under **Material Types** and assign the properties on the **Material Type Card**.

**B – Classify items (master data):**

4. Open the **Item Card** and enter the appropriate material type in the **Material Type Code** field. The properties are adopted; **Description**, **Description 2** and **Matchcode** are calculated based on the formulas of the material type.

**C – Daily work (operational user):**

5. Create a document, e.g. a **Sales Order**, and switch to an empty document line.
6. In the document line, choose the action **Start Material Search** (shortcut `Shift+Ctrl+S`) – alternatively, type a search term into the line field **Matchcode**.
7. In the opened **Item Search**, narrow down using the **property filters**, enter the **Recording Quantity** on the hit and confirm with **OK**. Confirm the prompt **Assign Entry Quantity to Lines?** – item/lot and quantity are transferred into the document line.

The material search does not replace a posting step; it fills the document line. The document is then posted, released or invoiced afterwards just like in the Business Central standard.

---

## Setup

Setup is the densest part of this module. It comprises the central setup page as well as the enablement chains for the three core functions (extended matchcode search, description/matchcode automation, item creation via templates).

### Central setup page "Material Property Setup"

**Process intro.** The administrator configures this page once per company, before the users work with the module. It controls, company-wide, whether and how the extended material search works in document lines, how descriptions are formatted and whether the item variant function is active. The switches set here take effect later in the **daily work on the document** (material search) and in the **Material Types** (variant features).

**Entry point:** Open the page via the search using the search term **Material Property Setup**. It is a company-wide single page (`UsageCategory = Administration`); no superordinate master record exists.

Explanations of the fields on the "Material Property Setup" page:

**"General" tab:**

| Setup | Explanation |
|---|---|
| **Modify fix values for Base Items only** | If set, property values marked as **Fix** may only be changed on items that are marked as **Base Item**; on derived items the fix value stays locked. Without the checkmark, fix values can be changed on any blocked item. |
| **Use Item Variant Features** | If enabled, the variant-related functions (variant matchcode, variant descriptions, properties per item variant) are unlocked and become visible on the Material Type Card. This field is only editable if **Modify fix values for Base Items only** has been set beforehand. |
| **Use Query Search** | If enabled, the property/material search uses performant query lookups for searching across large data volumes. Without the checkmark, the search runs via the standard logic. |
| **Omit Thousand Point for Description** | If set, the thousands separator for numeric values is omitted in **Description** and **Description 2**; otherwise it is shown. |

**"Matchcode" tab:**

| Setup | Explanation |
|---|---|
| **Use Optimized Matchcode Search Parameter** | If enabled, an optimized search parameter is used in the matchcode search that speeds up the determination of hits. |
| **Use Extended Matchcode Search** | If enabled, the extended **Item Search** (property, lot and inventory search) is available in the document lines and the subsequent filter fields become editable. Without the checkmark, only the simple matchcode transfer remains; when deactivating, all downstream search options are reset. |
| **Omit Thousand´s point** | If set, the thousands separator is suppressed in the search results of the extended matchcode search. |

*"Lot Reservation" subgroup:*

| Setup | Explanation |
|---|---|
| **Sales Quote** | If enabled, the lot recorded in the item search is already reserved in the **Sales Quote**; the assigned quantity is thereby blocked for other documents. Only editable when the extended matchcode search is active. |
| **Sales Order** | If enabled, the recorded lot is reserved in the **Sales Order**, so that the promised inventory is secured for later delivery. Only editable when the extended matchcode search is active. |

*"Location" subgroup:*

| Setup | Explanation |
|---|---|
| **Warehouse Location** | If enabled, the extended search includes the warehouse location in the inventory and availability determination; the hits are then shown by location. Only editable when the extended matchcode search is active. |

*"Quantity Recording" subgroup:*

| Setup | Explanation |
|---|---|
| **Assign Complete Quantity** | Controls what the availability check refers to during recording. **Item:** availability is evaluated at item level. **Item Tracking:** availability is evaluated at the item tracking level (lot/serial number), so that the recording quantity is checked exactly against the tracked stock. Only editable when the extended matchcode search is active. |

*"Filter" subgroup:*

| Setup | Explanation |
|---|---|
| **Item Search** | If enabled, the extended search searches the item level. If the checkmark is removed, **Show All** is deactivated at the same time. Only editable when the extended matchcode search is active. |
| **Lot Search** | If enabled, the extended search additionally searches the lot level and shows hits per lot; in doing so, **Show All** is deactivated. Only editable when the extended matchcode search is active. |
| **Show All** | If enabled, items without stock are shown as well; the module then forces **Item Search** active and **Lot Search** as well as **In Order** inactive. This lets users see the complete assortment, not only stock-bearing hits. Only editable when the extended matchcode search is active. |
| **In Order** | If enabled, open order quantities are also included in availability (Item Search and Lot Search are activated in the process, **Show All** deactivated), so that users can take into account quantities already ordered but not yet received. Only editable when the extended matchcode search is active. |
| **Item stock summary** | If enabled, the stock per item is shown summed across locations, instead of showing each inventory line individually. Only editable when the extended matchcode search is active. |
| **Split Option** | Determines how a recording quantity is distributed across several hits. Available value **Manual:** users distribute the quantity across the hits themselves. Only editable when the extended matchcode search is active. |

*"Search Properties" subgroup:*

| Setup | Explanation |
|---|---|
| **Matchcode Material Type** | Determines the material type whose properties are offered as filter criteria in the extended matchcode search. If a material type is set, users start the search directly with the matching property filters. Only editable when the extended matchcode search is active. |
| **Ignore Standard Values in Ext. Search** | If enabled, properties that only carry their standard value are not preset as filters in the extended search; users start with empty filters and specifically set their own criteria. Only editable when the extended matchcode search is active. |

**"Material Search" tab:**

| Setup | Explanation |
|---|---|
| **Default Material Search View Type** | Determines the preset view of the **Material Search**/**Material Balances**. **Item & Location:** structured first by item, then by location. **Item:** purely item-based. **Item Tracking:** structured by lot/serial number. **Location & Item:** structured first by location, then by item. This way, users open the search directly in the structure suited to their work area. |

**"Purchase" tab:**

| Setup | Explanation |
|---|---|
| **Reassign Comp. on Whse. Rcpt.** | If enabled, the assigned components are reassigned when posting a warehouse receipt, so that the property/lot assignment matches the actual warehouse receipt. |

☞ Please note that all filter, lot reservation, location, quantity and search property fields are only editable when **Use Extended Matchcode Search** is enabled. If you deactivate this switch, all downstream options are automatically reset.

### Setting up the extended matchcode search

**Process intro.** This chain unlocks the property-based **Item Search** in document lines. The administrator configures it together with a key user before the first document processing. The function is used in the **daily work on the document** via the action **Start Material Search** (see the section "Material Properties in Documents").

Numeric enablement steps in dependency order:

1. **First**, define per material type on the **Material Type Card** the **Item Matchcode Formula** (and, if needed, the **Lot/Serial Matchcode Formula**). If a matchcode formula is set, the module calculates a unique matchcode for each assigned item, which the later document search accesses.
2. **Then**, in the **Material Property Setup** on the **Matchcode** tab, activate the field **Use Extended Matchcode Search**. If enabled, the filter, lot reservation and search property fields become editable and the extended search is available in the document lines.
3. **Next**, set the desired filters (**Item Search**, **Lot Search**, **Show All**, **In Order**, **Item stock summary**), the **Split Option**, if applicable the **Matchcode Material Type** and the lot reservation per document type. Each switch determines which level is searched and which quantity is reserved (see the field table above).
4. **Finally**, users use the action **Start Material Search** or the line field **Matchcode** in the document line. This closes the chain (details in the section "Material Properties in Documents").

☞ Please note: if the extended matchcode search is not activated, the item search reports on opening that the function must be activated in the setup.

### Setting up the description and matchcode automation

**Process intro.** This chain ensures that an item's **Description**, **Description 2** and **Matchcode** are created automatically from its properties. The key user sets it up in the master data; it takes effect when the **Material Type Code** is assigned on the item (see "Master Data → Items").

1. **First**, define the required characteristics under **Properties** with Code, Name and **Data Type** (see "Master Data → Properties").
2. **Then**, assign these properties to the material type on the **Material Type Card** in the **Record Properties** subpage and set per property the **Standard Value**, **Display Order** and, if applicable, a **Calculation Formula**.
3. **Next**, via **Description Templates → Item Description Template**, store the **Item Description Formula** and the **Description 2 Formula** per language, and via **Matchcode → Item Matchcode Template** the **Item Matchcode Formula**. If a formula is set, description/matchcode are recalculated on every value change.
4. **Finally**, users assign the **Material Type Code** on the **item**. If a material type code is set, the module inherits the properties to the item and calculates Description, Description 2 and Matchcode. You update existing items via the actions **Update Item Descriptions** or **Update Item Matchcodes** on the Material Type Card.

### Setting up item creation via templates

**Process intro.** This chain enables the fast creation of new base and variant items per material type. The key user sets it up in the master data; the users trigger the creation later on the **Item Card**.

1. **First**, on the **Material Type Card**, open the **Create Item Template** page via **Item Templates → Template For Base Item Copy** or **Template For Variant Item**.
2. **Then**, in the template, use the copy switches to define which item components are adopted during creation (see the field table under "Master Data → Item Creation").
3. **Finally**, users use the actions **Create Variant Item** or **Copy Base Item** on the **Item Card**. If a template is set, the new item is created according to the copy switches of the material type.

---

## Master Data

The master data forms the foundation: properties and their values, material types with property assignment, as well as the extensions on item and item variant.

### Properties and Property Card

**Process intro.** A **Property** is a single technical characteristic (e.g. material, diameter, length). The key user creates properties before the material types, since material types build on them. Properties later appear as filters in the **Material Search** and as values in description and matchcode.

**Entry point:** Open the **Properties** list via the search; from a row you reach the **Property Card**.

Explanations of the fields on the "Property Card":

| Field | Explanation |
|---|---|
| **Code** | Unique key of the property; freely selectable, but must be unique. |
| **Name** | Descriptive name of the property, as shown to the users in search and assignment. |
| **Table No.** | Optional: if a table is set, the property draws its permitted values from this table instead of from freely maintained property values. The table must have exactly one primary key. |
| **Table Caption** | Shows, for control purposes, the caption of the table chosen under **Table No.** (read-only). |
| **Field No.** | For a table-bound property, the field of the source table whose values are adopted (selectable for the Item table). |
| **Field Caption** | Shows, for control purposes, the caption of the chosen field (read-only). |
| **Data Type** | Determines the format and validation of the value. **Text:** any text. **Integer:** whole number. **Decimal:** decimal number (with unit/decimal places). **Date:** date value. Only editable as long as no table is set. |
| **Use Property Values** | If enabled, only the values maintained under **Property Values** are permitted for this property; the users choose from a fixed list instead of typing freely. |
| **Category Code** | Assigns the property to a **Property Category** and thereby groups its display in cards and search. |
| **Unit of Measure** | For numeric data types, the unit of measure (e.g. mm, kg) that is shown next to the value and output in descriptions. |

Explanations of the actions on the "Property Card":

| Action | Explanation |
|---|---|
| **Property Values** | Opens the list of permitted **Property Values** of this property. Only active if **Use Property Values** is set. |
| **Translations** | Opens the translations of the property name for multilingual descriptions. |

☞ Please note: as soon as a property is assigned to at least one record, the data type, unit of measure, table binding and the switch **Use Property Values** can no longer be changed.

### Value Setup (Property Values, Value Groups, Categories)

**Process intro.** For properties with a fixed value list, the key user maintains the permitted **Property Values**. These values limit the entries on the item and serve as a selection in the **Material Search**. **Property Categories** and **Property Value Groups** structure the display and bundle values for filtering, respectively.

**Entry point:** Open the **Property Card** and choose the action **Property Values**. You open categories and value groups via the lists of the same name (**Property Categories**, **Property Value Groups**) from the search.

Explanations of the fields of the "Property Values":

| Field | Explanation |
|---|---|
| **Value** | The permitted value of the property. For numeric or data type properties, the value is checked against the format on recording. |
| **Name** | Descriptive designation of the value, shown to the users in addition to the value. |
| **Group Code** | Assigns the value to a **Property Value Group**; the group can be used to jointly restrict values in search and filter. |

Explanations of the fields of the "Property Categories" and "Property Value Groups":

| Field | Explanation |
|---|---|
| **Code** | Unique key of the category or value group; freely selectable, must be unique. |
| **Description** | Descriptive designation by which users recognize the category/value group. |

### Material Types and Material Type Card

**Process intro.** The **Material Type** is the central classification: it bundles a set of properties and the formulas for description and matchcode. The key user creates material types before items are classified. Each item is assigned to exactly one material type via the **Material Type Code**; the assignment controls inheritance, calculation and search in daily work.

**Entry point:** Open the **Material Types** list via the search; from a row you reach the **Material Type Card**.

Explanations of the fields on the "Material Type Card" ("General" tab):

| Field | Explanation |
|---|---|
| **Code** | Unique key of the material type (max. 20 characters); freely selectable, must be unique. |
| **Description** | Descriptive designation of the material type, as shown to the users in selection and search. |
| **Activate Duplicate Check** | If enabled, an item newly assigned to a material type is automatically **blocked** until the users unblock it after checking; this way, accidental duplicates are caught before release. Without the checkmark, the item stays unchanged. |
| **No. of Items** | Shows, read-only, how many items are assigned to this material type. |
| **Item Matchcode Formula** | Formula from which the unique **Matchcode** of the assigned items is calculated. If set, the material search in the document lines accesses this matchcode. It is assembled graphically via the action **Item Matchcode Template**. |
| **Item Variant Matchcode Formula** | As above, but for item variants. Only visible if **Use Item Variant Features** is enabled in the setup. |
| **No. Of Item Variants** | Shows, read-only, the number of item variants of this material type (only with the variant feature active). |
| **Lot/Serial Matchcode Formula** | Formula for the matchcode at lot/serial number level; enables search and identification down to the lot. |

Explanations of the actions on the "Material Type Card":

| Action | Explanation |
|---|---|
| **Item Description Template** | Opens the **Item Description Templates** per language, in which the **Item Description Formula** and **Description 2 Formula** are stored. |
| **Item Variant Description Template** | Opens the description templates for item variants (only with the variant feature active). |
| **Lot/Serial Description Template** | Opens the description templates for lots and serial numbers. |
| **Update Item Descriptions** | Recalculates Description/Description 2 of all assigned items based on the current templates. |
| **Update Item Variant Descriptions** | As above, for item variants (only with the variant feature active). |
| **Update Lot/Serial Descriptions** | Updates the descriptions at lot/serial number level. |
| **Item Matchcode Template** | Assembles the **Item Matchcode Formula** graphically. |
| **Item Variant Matchcode Template** | Assembles the variant matchcode formula (only with the variant feature active). |
| **Serial/Lot Matchcode Template** | Assembles the lot/serial matchcode formula. |
| **Update Item Matchcodes** | Recalculates the matchcodes of all assigned items. |
| **Update Item Variant Matchcodes** | Updates the variant matchcodes (only with the variant feature active). |
| **Update Lot/Serial Matchcodes** | Updates the matchcodes at lot/serial number level. |
| **Template For Base Item Copy** | Opens the **Create Item Template** for the creation of base items (see "Item creation via templates"). |
| **Template For Variant Item** | Opens the template for the creation of variant items. |
| **Transfer Standard Value to Item Value** | Transfers, for the marked record properties, the **Standard Value** of the material type into the **Value** of the assigned items. |
| **Transfer Standard Value to Item Variant Value** | As above, for item variants (only with the variant feature active). |

Explanations of the fields of the "Record Properties" subpage (property assignment of the material type):

| Field | Explanation |
|---|---|
| **Property Code** | References the assigned **Property**. Through this row, the property becomes part of the material type and of all assigned items. |
| **Property Name** | Shows, read-only, the name of the property. |
| **Standard Value** | Default value that is adopted when the material type is assigned to the item. If set, every new item starts with this value; deviating values on the item are highlighted. Only editable on the material type. |
| **Value** | The concrete property value on the record. Empty on the material type itself; it is maintained on the item (visible there as "Value" or interpreted value). |
| **Fix** | If enabled, the value counts as a fix value; its change is – depending on the setup **Modify fix values for Base Items only** – only allowed on the base item and only when the item is blocked. |
| **Purchase Property** | If enabled, the property is editable/relevant as a value in purchase documents; otherwise it stays read-only there. |
| **Sales Property** | If enabled, the property is editable/relevant in sales documents. |
| **Lot Property** | If enabled, the property is editable/relevant at lot level and is available in the lot search. |
| **Mandatory** | If enabled, the value must be filled on the item; missing mandatory values are shown to the user as a required field. |
| **Not Editable** | If enabled, the value cannot be changed on the item (e.g. because it comes from a source table). |
| **Not Visible** | If enabled, the property is hidden by default on the item; users can show hidden properties when needed. |
| **Zero is Value** | If enabled, for numeric properties the value 0 counts as a valid value (not as "empty"); it affects mandatory checking and calculation. Only permitted for the data type Integer/Decimal. |
| **Usage** | Additional usage flag of the property (in the standard, only the empty value **(empty)** is available; extendable via extensions). |
| **Property Value Name** | Shows, read-only, the name of the chosen property value. |
| **Value Permitted From** | Lower limit for numeric properties; smaller values are rejected. Only editable for a numeric data type. |
| **Value Permitted To** | Upper limit for numeric properties; larger values are rejected. Only editable for a numeric data type. |
| **Unit of Measure** | Shows the unit of measure of the property (read-only, from the property). |
| **Calculation Formula** | Formula with which the value is calculated automatically from other properties. If set, the value can no longer be edited manually on the item. It is assembled via the graphical formula assistant. |
| **Display Order** | Determines the order in which the properties are displayed on the item and in the search. |
| **Category Code** / **Category Description** | Assigns the row to a property category or shows its description. |
| **Value Filter** / **Value Group Filter** | Restricts the selectable property values to a value range or a **Property Value Group**. |

*As read-only helper columns, the subpage additionally carries **Numeric Value**, **Date Value**, **Data Type** and **Use Property Values**; they only mirror the recorded **Value** or the **Data Type** and require no separate maintenance.*

☞ Please note: when a material type is deleted, all assignments are removed from the affected items and the material type code on the item is cleared. Changes to the property assignment can, on a prompt, be synchronized into all assigned items (**Should the property be modified in all items that are assigned to this material type?**).

### Items

**Process intro.** On the **item** (Item Card/Item List), the module connects the classification with the concrete master record. The users in master data maintenance assign a material type to the item and maintain the property values; from this, Description, Description 2 and Matchcode are created. These values then control the material search in the documents.

**Entry point:** Open the **Item List** and choose an item or create a new one; the detailed maintenance takes place on the **Item Card**.

Explanations of the fields added by the module on the "Item Card" / "Item List":

| Field | Explanation |
|---|---|
| **Description 2** | Second description line of the item; with the description automation active, it is calculated from the **Description 2 Formula** of the material type. |
| **Material Type Code** | Assigns the item to a **Material Type**. If a material type code is set, the module inherits the properties of the material type to the item, calculates Description, Description 2 and Matchcode, and – with the material type's **Duplicate Check** active – blocks the item until release. |
| **User-Defined Matchcode** | If enabled, users may overwrite the matchcode manually; without the checkmark, the matchcode is calculated exclusively from the formula. |
| **Matchcode** | The technical search key of the item. Only changeable manually if **User-Defined Matchcode** is set; otherwise automatically from the material type formula. |
| **Base Item** | If enabled, the item counts as a base item and serves as a template for variant/copy creation; only on base items can fix values (depending on the setup) be edited. |
| **Base Item No.** | Shows, read-only, the underlying base item from which this item was derived. |
| **Copied From Item No.** | Shows, read-only, the item from which this item was copied. |

In addition, the module displays the **"Properties" info box** (properties of the item) on the Item Card and Item List. There, users maintain the item's property values and show hidden properties via **Show Hidden Properties**.

Explanations of the actions on the "Item Card":

| Action | Explanation |
|---|---|
| **Material List** | Opens the **Material List** filtered to the item and shows its structure (Base Item, Copied From, Item Variant). |
| **Create Variant Item** | Creates a new variant item from the base item via the stored template. |
| **Copy Base Item** | Copies the base item via the stored template to a new base item. Only possible if it is a base item. |
| **Material Filter** | Opens the **Item Material Filter** page (see "Material Filter"). Called via the path **Related → Item → Material Filter** in the ribbon of the Item Card. |

**Item Variants.** On the **Item Variants** page, the module adds the fields **Matchcode** and **User-Defined Matchcode** (meaning as on the item) as well as the "Properties" info box for the variant-related property values. Via the action **Copy Variant**, users create a new variant from an existing one. These fields are only relevant if **Use Item Variant Features** is enabled in the setup.

### Item creation via templates

**Process intro.** The **Create Item Template** page defines, per material type and creation type (Base Item/Variant Item), which components are adopted when copying an item. The key user maintains the template; the users trigger the creation on the Item Card.

**Entry point:** Material Type Card → **Item Templates → Template For Base Item Copy** or **Template For Variant Item**.

Explanations of the fields on the "Create Item Template" card (each switch: if enabled, the named component is adopted into the new item):

| Field | Explanation |
|---|---|
| **General Item Information** | If enabled, the general item master data is adopted into the new item. |
| **Units of measure** | Adopts the units of measure of the source item. |
| **Dimensions** | Adopts the dimensions. |
| **Picture** | Adopts the item picture. |
| **Comments** | Adopts the comments. |
| **Planning** | Adopts the planning parameters. |
| **Sales Prices** | Adopts the sales prices. |
| **Sales Line Disc.** | Adopts the sales line discounts. |
| **Purchase Prices** | Adopts the purchase prices. |
| **Purchase Line Disc.** | Adopts the purchase line discounts. |
| **Troubleshooting** | Adopts the troubleshooting data (Service). |
| **Resource Skills** | Adopts the resource skills (Service). |
| **Item Variants** | Adopts the item variants. |
| **Translations** | Adopts the translations. |
| **Extended Texts** | Adopts the extended texts. |
| **BOM Components** | Adopts the BOM components. |
| **Item Vendors** | Adopts the item vendors. |
| **Attributes** | Adopts the item attributes. |
| **Item Cross References** | Adopts the item cross references. |
| **Item References** | Adopts the item references. |
| **Stockkeeping Units** | Adopts the stockkeeping units (SKU). |
| **Copy Variant Items** | Only visible for creation type Base Item: if enabled, the associated variant items are created as well during copying. |
| **Unblock New Item** | If enabled, the newly created item is unblocked directly; otherwise it stays blocked until the users check and release it. |

### Material Filter

**Process intro.** Via the **Item Material Filter**, users store per item the search context by which the item is found in the property-based search – either via a **Material Type** or via concrete **property filters**. This lets you control by which criteria an item can be found in the material search.

**Entry point:** Open the path **Related → Item → Material Filter** from the Item Card.

Explanations of the fields of the "Item Material Filter":

| Field | Explanation |
|---|---|
| **Item No.** | The item to which the filter applies (usually preset and hidden). |
| **Type** | Determines the filter type. **Material Type:** the item is delimited via a material type; only **one** Material Type row is permitted per item. **Property Filter:** the item is delimited via a concrete property with a filter value. |
| **Code** | References – depending on **Type** – the material type or the property. |
| **Filter Value** | For **Property Filter**, the value or value range; selectable via the assistant. For **Type = Material Type**, the field stays empty. |
| **Manual** | Shows, read-only, that the row was recorded manually. |

☞ Please note: per item, only **one** row of type **Material Type** is permitted (**Only one Material Type Code per Item allowed!**). Further restrictions are made via rows of type **Property Filter**.

---

## Material Properties in Documents

**Process intro.** In the document lines (Sales, Purchase, Service, Assembly, Manufacturing, Transfer, as well as journals and warehouse activities), the module adds the same function: the line field **Matchcode** and the action **Start Material Search**. The prerequisite is **Use Extended Matchcode Search** enabled in the **Material Property Setup** (see "Setting up the extended matchcode search"). The search fills the document line with item/lot and quantity – it is a recording aid and does not replace a posting step.

**Entry point:** Open a document, e.g. the **Sales Order**, and switch to a document line.

**Flow of the material search in a document line:**

1. In the document line, choose the action **Start Material Search** (`Shift+Ctrl+S`) – or type a search term into the line field **Matchcode**. The **Item Search** opens.
2. Narrow down by technical characteristics using the **property filters** (**Properties Filter** tab or the action **Search By Properties**). Use **Remove Filters** to reset the filters.
3. On the **Item** tab, choose a hit; for lot/serial-tracked items, additionally choose the matching lot on the **Lots** tab. The info boxes **Item - Properties** and **Lot No. - Properties** show the characteristics of the marked hit.
4. Enter the **Recording Quantity**. The fields **Open Quantity**, **Document Line Quantity** and **Assigned Quantity** show the reconciliation against the document line.
5. Confirm with **OK**. Confirm the prompt **Assign Entry Quantity to Lines?** – the chosen item or lot and the quantity are transferred into the document line; with **Lot Reservation** active, the lot is reserved at the same time.

Explanations of the central fields of the "Item Search":

| Field | Explanation |
|---|---|
| **Recording Quantity** | The quantity that is to be transferred from the hit into the document line. |
| **Open Quantity** | Shows the remaining quantity of the document line not yet assigned. |
| **Document Line Quantity** | Shows the total quantity of the document line. |
| **Assigned Quantity** | Shows the quantity already assigned via the search. |
| **Unit of Measure** | The unit in which the recording takes place. |
| **Requested Delivery Date** | Adopts or shows the requested delivery date of the line for the reservation check. |

In posted documents (e.g. posted shipments, invoices, warehouse receipts), the module shows the **Matchcode** in the lines, so that the technical identifier remains traceable even after posting. A search history is available as the info box **Item Search History**.

☞ Please note: if the extended matchcode search is not activated, the item search indicates that the function must first be enabled in the **Material Property Setup**.

### Material Search and Material Balances

Besides the document-related search, the standalone analyses **Material Search** and **Material Balances** are available. In the **Material Search** (dialog), users choose the **Material Type** at the top and set a **Filter Value** per property below; the result delivers the matching items/stock. The **Material Balances** show the accumulated stock by the set **View Type** and can be refreshed via **Update Data**; **Search By Properties** filters by properties, and **Card** opens the item.

Explanations of the filter fields of the "Material Balances":

| Filter field | Explanation |
|---|---|
| **Item No.** | If set, the stock is filtered by this item number. |
| **Matchcode** | If set, the stock is filtered by this matchcode. |
| **Location Code** | If set, the stock is filtered by this location. |
| **Bin Code** | If set, the stock is filtered by this bin. |
| **Lot No.** | If set, the stock is filtered by this lot. |
| **View Type** | Determines the structure of the result list (Item/Location/Item Tracking – values as in the setup). |

---

## FAQ and Troubleshooting

### Why can I no longer change the data type of a property?
As soon as a property is assigned to at least one record (material type or item), the module locks the data type, unit of measure, table binding and the switch **Use Property Values** (**The property '…' cannot be changed because it was assigned at least to one record.**). First remove the assignments or create a new property.

### Why is my item blocked as soon as I set the material type code?
If the assigned **Material Type** has the switch **Activate Duplicate Check** set, the module blocks the item automatically so that you can check it for duplicates before release. Unblock the item manually after the check.

### Why can't the matchcode be entered directly on the item?
The **Matchcode** is calculated from the formula of the material type. It is only changeable manually if you activate **User-Defined Matchcode** on the item; otherwise the calculation overwrites your entry.

### Why can't I change a fix property value?
If the value is marked as **Fix** and **Modify fix values for Base Items only** is set in the setup, you may only change it on a **Base Item** and only when the item is blocked (**Fix value modification is allowed for Base Item only!**). Check the **Base Item** flag and the block status.

### Why does the system require the item to be blocked before I change values?
Changes to fix or controlled property values on the item are only allowed if the item is blocked (**Item … must be blocked for modification!**). Block the item, change the value and then release it again.

### Why does no material search appear in the document line?
The extended **Item Search** in document lines is only available if **Use Extended Matchcode Search** is enabled in the **Material Property Setup**. Without this activation, the search reports that the function must first be enabled.

### Why can't I record a value – it is "not allowed"?
For properties with **Use Property Values**, only the maintained **Property Values** are permitted (**Value "…" is not allowed/found in Property Values!**). First maintain the desired value under **Property Values** or choose an existing one.

### Why is a numeric value shown outside my entry?
Numeric properties check the limits **Value Permitted From** and **Value Permitted To**; values below/above are rejected (**must not be less than / must not be larger than …**). In addition, the module formats the value according to unit and decimal places.

### Why can't I edit the value of a property on the item?
If the property is bound to a source table (e.g. the item itself) or has been marked as **Not Editable**, the module adopts the value automatically (**You cannot change the value when the value will be transfered from the Item Table.**). Likewise, a stored **Calculation Formula** locks the manual entry.

### Why don't I see all properties on the item?
Properties marked as **Not Visible** are hidden by default. Via the action **Show Hidden Properties** in the Properties info box, you show them (provided your permissions allow this).

---

## Typical Use Cases

The following scenarios show realistic triggers and the chronological flow in Business Central. All named pages and actions exist in the module.

### 1. Set up a new material type with properties

- **Trigger:** A key user is to model a new material class (e.g. round steel) in the system.
- **Entry in BC:** Open the **Properties** list via the search and create the characteristics (e.g. material as Text, diameter and length as Decimal with **Unit of Measure** mm).
- **Core flow:** Open the **Material Types** list, create a new material type and switch to the **Material Type Card**. In the **Record Properties** subpage, assign the previously created properties, set **Standard Value**, **Display Order** and – where sensible – **Value Permitted From/To** or a **Calculation Formula**. Assemble the **Item Matchcode Formula** via **Item Matchcode Template** and the description formulas via **Description Templates → Item Description Template**.
- **Completion:** The material type is ready for assignment to items; via **Transfer Standard Value to Item Value**, standard values can be transferred into existing items.

### 2. Classify an item and generate the description automatically

- **Trigger:** A new item is to be assigned to a material class and labeled automatically.
- **Entry in BC:** Open the **Item List** and the item in question on the **Item Card**.
- **Core flow:** Enter the appropriate material type in the **Material Type Code** field. The module inherits the properties, calculates **Description**, **Description 2** and **Matchcode**, and blocks the item – with **Duplicate Check** active. Maintain the concrete property values in the **Properties** info box; mandatory fields (**Mandatory**) are highlighted.
- **Completion:** Check the calculated description and the matchcode and lift the item's block.

### 3. Find the matching item in the sales order via properties

- **Trigger:** A customer inquires by phone about material by technical specification (material, diameter, length), without knowing the item number.
- **Entry in BC:** Open the **Sales Order** and switch to an empty document line.
- **Core flow:** Choose the action **Start Material Search** (`Shift+Ctrl+S`). In the **Item Search**, narrow down by the named characteristics using the **property filters**, choose the matching hit on the **Item** tab (with lot requirement additionally on the **Lots** tab) and enter the **Recording Quantity**. Confirm with **OK** and the prompt **Assign Entry Quantity to Lines?**.
- **Completion:** Item/lot and quantity are in the order line; with **Lot Reservation** active, the lot is reserved. The order is then processed further just like in the standard.

### 4. Create a variant item from a base item

- **Trigger:** For an existing base item, a new characteristic (e.g. a different length) is needed.
- **Entry in BC:** Open the base item on the **Item Card**.
- **Core flow:** Choose the action **Create Variant Item**. Based on the **Template For Variant Item** stored on the material type, the module creates a new item and adopts the components chosen in the template. Maintain the deviating property values; description and matchcode are recalculated.
- **Completion:** The new variant item carries the reference **Base Item No.** and is visible in the structure of the base item via the **Material List**.
