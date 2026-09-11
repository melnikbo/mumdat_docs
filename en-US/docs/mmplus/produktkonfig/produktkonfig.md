---
title: Anwenderhandbuch m+m Product Configurator
---

# User Guide m+m Product Configurator

## Introduction

The **Product Configurator** makes it possible, within a sales, purchase, or production document, to
determine a matching item based on material properties or – if no matching item exists – to create one
automatically. Instead of having to know an item number up front, the user selects a **Material Type** in the
document line, enters the desired property values (e.g. diameter, material, length), and in return receives
the matching item, including its variant, in the line.

**Target audience.** This guide is primarily aimed at **operational users** who capture document lines every
day – sales and purchase office staff as well as users in production preparation (capturing production BOM
lines). Secondarily, it addresses **administrators and master data managers** who set up the material types,
property categories, visibility rules, and text templates before the configurator can be used.

**Short process overview.** The workflow follows a fixed chain:

1. A **Material Type** is activated on the **Material Type Card** on the **Product Configurator** tab and
   released for specific document types.
2. Categories and a sequence are assigned to the properties of the material type via **Product Configurator
   Categories**; exactly one category is the **Main Category**.
3. Optionally, **visibility rules**, **extended texts**, and a **rule flow** are set up.
4. In the document, the user fills the **Product Configurator Material Type** field in the line; this opens
   the **Product Configurator** dialog, in which the property values are captured.
5. On leaving with **OK**, the system searches for a matching item or creates a new item via the stored item
   template and writes the item and variant back into the document line.

This module does not post anything itself and does not create posted documents; it extends document entry
with property-based item lookup and creation.

---

## Quick Start for Users

The order follows the technical dependency: setup first, then daily use.

**Setup (one-time, performed by administrator/master data manager):**

1. Open **Material Types** (via **Search**), select the desired material type, and open the **Material Type
   Card**. On the **Product Configurator** tab, activate the **Use For Product Configurator** field, enter an
   **Item Template Code**, choose the **Search Option**, and select the document types (**Sales Order**,
   **Sales Quote**, … ) in which the configurator may be used.
2. On the Material Type Card, use **Related -> Product Configurator Categories** to open the **Material
   Property Category Relations** view and create at least one category with **Sequence 0** (main category),
   and assign categories to the properties.
3. In the property table of the Material Type Card, flag the required properties as **Mandatory** and set
   **Display Type** where appropriate.

**Daily use (users):**

1. Capture a document line (e.g. in the **Sales Order**) and select the **Product Configurator Material
   Type** field in the line.
2. In the opened **Product Configurator** dialog, enter the property values in the main category and in the
   additional **categories**.
3. In the **Not Filled Mandatory Fields** FactBox, check whether any **mandatory fields** are still open.
4. Confirm with **OK**: the system finds or creates the item and transfers the item and variant into the
   document line. **Cancel** discards all entries.

---

## Setup

The setup is the most extensive part of this module and the prerequisite for any later use. All the setup
pages below are reached via the **Material Type Card** (m+m Material Types base module), not via the global
**Search** function. If one of the associated actions is grayed out, then in most cases the **Use For
Product Configurator** field has not yet been activated on the Material Type Card.

### Setting up the Product Configurator for a material type

**Entry point:** **Material Types** (via **Search**) -> select line -> **Material Type Card** ->
**Product Configurator** tab.

**Process intro.** The administrator or master data manager performs this setup once per material type,
before the configurator is used in a document for the first time. It determines whether a material type is
configurable at all, which template new items are created from, how the search is performed, and in which
document types the configurator appears. The flags set here directly control whether the **Product
Configurator Material Type** field in the respective document line offers the material type for selection at
all (see **Daily Work in the Product Configurator**).

| Setup | Explanation |
|---|---|
| **Use For Product Configurator** | When activated, the material type is configurable: only then can document types, item template, and search option be maintained and the actions **Product Configurator Categories**, **Visibility of Properties and Categories**, and **Product Configurator Rule Flow** be called. When deactivated, all document flags are reset; deactivation is blocked as long as entries exist for this material type under **Visibility of Properties and Categories**. |
| **Item Template Code** | When set, the configurator uses this configuration template to create a new item as soon as no item is found for the entered properties. Without an item template, automatic item creation is not possible – the configurator can then only find items that already exist. The template must be activated. |
| **Search Option** | Determines which properties are checked during item search. **Unique Search:** all entered properties are checked; if no match is found, the system directly creates a new item via the item template. **Search Only Fix:** only the properties that have the **Fix** flag set on the **General** tab of the property table are checked; **Sales Property** and **Purchase Property** are ignored in this search. This option cannot be set if a **Default Value** is stored for non-fixed properties. |
| **Sales Quote** | When activated, the configurator is available in sales quote lines; the **Product Configurator Material Type** field offers the material type for selection there. Can only be set if **Use For Product Configurator** is active. |
| **Sales Blanket Order** | When activated, the configurator can be used in sales blanket order lines. Can only be set if **Use For Product Configurator** is active. |
| **Sales Order** | When activated, the configurator can be used in sales order lines. Can only be set if **Use For Product Configurator** is active. |
| **Purchase Quote** | When activated, the configurator can be used in purchase quote lines. Can only be set if **Use For Product Configurator** is active. |
| **Purchase Blanket Order** | When activated, the configurator can be used in purchase blanket order lines. Can only be set if **Use For Product Configurator** is active. |
| **Purchase Order** | When activated, the configurator can be used in purchase order lines. Can only be set if **Use For Product Configurator** is active. |
| **Production Order** | When activated, the configurator can be used in production order lines. Can only be set if **Use For Product Configurator** is active. |
| **Production BOM** | When activated, the configurator can be used in production BOM lines. Can only be set if **Use For Product Configurator** is active. |

**Setup steps in dependency order:**

1. **First**, activate **Use For Product Configurator** – without this flag, all further fields and actions
   are locked.
2. **Then** enter an **Item Template Code** so that a new item can be created when no match is found.
3. **Next**, choose the **Search Option** and activate the required document types.
4. **Finally**, assign categories to the properties (see next section) – this is mandatory, because only
   categorized properties appear in the configurator.

> Note: A correctly set up material type is essential for the configurator to function. It is advisable to
> flag all properties as **Mandatory** whose values are used in the **Item Description Formula** or in the
> match code formula.

### Setting up categories and sequence

**Entry point:** **Material Type Card** -> **Related -> Product Configurator Categories** ->
**Material Property Category Relations**.

**Process intro.** Here the administrator determines in which **sequence** and under which **category code**
the properties of a material type appear in the configurator. Exactly one category per material type is the
**main category** (Sequence 0); its properties are shown in the upper-left area of the configurator. The
sequence is especially important when rules are used, because dependent properties must be known at the
right time. This setup takes effect immediately in the **Product Configurator** dialog (see **Daily Work**).

| Field | Explanation |
|---|---|
| **Sequence** | When set, the value determines the display position of the category in the configurator. **Sequence 0** defines the **main category** and is mandatory; per material type, 0 may only be assigned once. |
| **Category Code** | When selected, the value assigns the line to a property category; only properties with a category code appear in the configurator. The code is selected from the property categories or newly created via **+New** (descriptive codes such as “DIMENSION” make the assignment easier). |
| **Category Description** | Shows the description of the selected category; it is derived automatically from the category code and serves for orientation in the list. |
| **Material Type Code** | When set, the value assigns the relation to the respective material type; for new lines it is already prefilled from the calling context. |
| **Property Name** | Shows the designation of the material type and serves as a label in the list. |
| **Main Category** | Indicates whether the line is the main category (Sequence 0). The main category is not shown in the configurator as a separate category; its properties appear directly in the first area. |

**Actions on this page:**

- **Create Main Category:** When executed, the action creates a line with Sequence 0 for the current
  material type. It is only available as long as no main category exists yet.
- **Extended Texts:** Opens the **Extended Text Assignment Worksheet** for the material type (see the
  section *Setting up extended texts per material type and category*).

**Enablement steps:** First use **Create Main Category** to create Sequence 0, then assign category codes and
ascending sequences to the remaining properties via new lines. When leaving the page, the system checks that
a main category exists and otherwise points this out. Bulk assignments are possible via the property table
(see **Master Data**).

### Setting up the visibility of properties and categories

**Entry point:** **Material Type Card** -> **Related -> Visibility of Properties and Categories** ->
**Visibility of Properties and Categories List** -> line -> card
**Visibility of Properties and Categories**.

**Process intro.** With this setup, the administrator hides individual properties or entire categories
depending on a value entered in the configurator. Example: if the value “round” is entered for bar material,
“thickness” and “width” can be hidden because only “diameter” is relevant. The rule applies only once the
triggering value is actually set; with an empty trigger value nothing is hidden. The setup takes effect in
the **Product Configurator** dialog.

**Header – trigger:**

| Field | Explanation |
|---|---|
| **Material Type Code** | Shows the material type the rule applies to; prefilled from the calling context and not editable. Only material types with active **Use For Product Configurator** are allowed. |
| **Material Description** | Shows the description of the material type for orientation; derived automatically. |
| **Property Code** | When set, this property determines the trigger for the hiding; the properties of the material type can be selected. |
| **Property Description** | Shows the name of the trigger property; derived automatically. |
| **Value** | When set, the hiding becomes active exactly when this value is entered for the trigger property in the configurator. For properties with stored **property values**, the selection is made from that list; numeric or date values are checked against the **Data Type**. |
| **Data Type** | Shows the data type of the trigger property (e.g. Text, Decimal, Integer, Date); it controls the value check and is derived automatically. |
| **Use Property Values** | Indicates whether the property uses a fixed value list. If so, the entered **Value** is checked against the allowed **property values**. |

**Lines – objects to be hidden:**

| Field | Explanation |
|---|---|
| **Hidden Type** | Determines what is hidden. **Property:** when selected, a single property is hidden. **Category:** when selected, an entire category with all its properties is hidden. When the hidden type is changed, the code is reset. |
| **Hidden Code** | When set, the value designates the specific property or category to be hidden. The main category and properties of the main category cannot be hidden – the attempt is rejected with a message. |
| **Hidden Description** | Shows the designation of the hidden object; derived automatically from the code. |

**Enablement steps:** First define the property code and value as the trigger in the header, then store the
**Hidden Type** and **Hidden Code** per entry in the lines. One trigger can cause several hidings. For hidden
objects, the configurator automatically adopts the property's stored default value.

### Setting up extended texts per material type and category

**Entry point:** **Material Property Category Relations** -> **Extended Texts** action ->
**Extended Text Assignment Worksheet**.

**Process intro.** In this worksheet, the administrator assigns **text templates** of the m+m Extended Text
module to a material type per category and process. When creating or finding an item via the configurator,
the system combines these templates and uses them to create the extended texts of the new item – separated
by print type (FactBox, report, email). This connects the configuration with the document text output of the
Extended Text module.

| Field | Explanation |
|---|---|
| **Category Code** | When set, the value assigns the text assignment to a property category. |
| **Category Description** | Shows the description of the category; derived automatically. |
| **Template No.** | When set, the value refers to the text template to be used; the **Print Type** is adopted from it automatically. An empty value is not allowed when saving. |
| **Template Description** | Shows the description of the text template; derived automatically. |
| **Print Type** | Shows or determines for which output channel the template applies (FactBox, report, or email); it is adopted from the template and controls the process selection. |
| **Process Group** | When set, the value assigns the assignment to a process group; setting a process group clears any single process that may be set. The selection is limited to process groups of the chosen print type. |
| **Process** | When set, the value assigns the assignment to a single process; setting a process clears any process group that may be set. The selection is limited to processes of the chosen print type. |
| **Process Object Name** | Shows the target object determined from the process (e.g. a page or a report); not editable. |
| **Process Object Type** | Shows the object type of the process target. **Report:** the process target is a report. **Page:** the process target is a page. **(empty):** no object type determined (e.g. when a process group is used instead of a single process). |
| **Sequence** | When set, the value determines the combination order of the templates per process/process group. **0 is not allowed**; per process or process group, a sequence may only be assigned once. |

In the **Texts** FactBox area, the text preview belonging to the template is shown.

**Enablement steps:** First choose a template no. and its print type per category, then assign either a
single **Process** or a **Process Group** (not both), and finally assign a unique **Sequence > 0**. When
configuring later, the system generates the item's extended texts from these assignments.

### Extending the description and match code formula with text templates

**Entry point:** **Material Type Card** -> associated **Item Description Formula** page (m+m Material Types
base module).

**Process intro.** The configurator uses the material type's **Item Description Formula** to automatically
calculate the description of newly created items. This extension adds to the formula entry the option of
including an **Extended Text Template** in the formula instead of a property code or fixed text. An analogous
extension (**Extended Text Template** field and **Add Extended Text Template** action) is available on the
**Create Lot/Serial No. Description Formula** page.

| Field | Explanation |
|---|---|
| **Extended Text Template** | When set, a text template can be included in the description formula. The field is only editable as long as neither a property code nor a fixed text value is set; conversely, the three inputs lock each other so that exactly one source applies per formula element. |

**Action:**

- **Add Extended Text Template:** When executed, the action adds the selected text template to the item
  description formula. It is only active when an **Extended Text Template** is selected.

**Enablement step:** Select the extended text template, add it to the formula with **Add Extended Text
Template**; the configurator then calculates the item description from it.

### Setting up the rule flow of the Product Configurator

**Entry point:** **Material Type Card** -> **Product Configurator Rule Flow** action.

**Process intro.** Via the **rule flow** (m+m Standard Rule Management module), the administrator can specify
that, when property values are entered in the configurator, values are automatically calculated or set. In
addition, a **direct rule code** can be stored per property, which is executed directly when the value is
changed in the configurator.

| Setup | Explanation |
|---|---|
| **Product Configurator Rule Flow** (action) | When executed, the action opens the rule flow belonging to the material type; if none exists yet, a new one is created automatically. Rules defined in the rule flow are processed on every value entry in the configurator and can automatically fill dependent properties. |
| **Direct Rule Code** (property) | When set, the stored rule is executed immediately as soon as the value of this property is changed in the configurator, and, depending on the data type, writes the calculated result back into the property. Other properties with a direct rule code are also re-evaluated in the process. |

**Enablement steps:** First open the rule flow with **Product Configurator Rule Flow** and create the desired
rules; then – if needed – assign a **Direct Rule Code** to individual properties. Further details on rule
definition are described in the documentation of m+m Standard Rule Management.

### Permissions

The permission set **Product Configurator all permissions** (m+m PK Permission) bundles all tables, pages,
and codeunits of the Product Configurator. Assigning this set to a user group determines which actions users
can perform in the Product Configurator – from maintaining the category relations and visibility rules to
opening the configurator in the document line. Without this permission set, the associated pages and actions
are not available.

---

## Master Data

### Property table – display and category assignment

**Entry point:** **Material Type Card** -> property table (**General** tab, m+m Material Types base module).

**Process intro.** In the material type's property table, the master data managers maintain the individual
properties. This extension adds the **Display Type** to the table and an action for quick category
assignment. The values maintained here – in particular **Mandatory**, **Fix**, **Default Value**, and
**Display Type** – directly control how the property behaves and is displayed in the **Product Configurator**
dialog.

| Field | Explanation |
|---|---|
| **Display Type** | When set, the value determines the color or typographic display of the property in the configurator. Allowed values and their effect: **(empty):** standard display; non-editable properties are shown dimmed (gray). **Standard:** neutral standard display. **StandardAccent** (blue): blue highlight. **Strong** (bold): bold font. **StrongAccent** (bold blue): bold and blue. **Attention** (red italic): red-italic warning display. **AttentionAccent** (blue italic): blue-italic. **Favorable** (bold green): bold-green as a positive marking. **Unfavorable** (bold & italic red): red-bold-italic as a clear warning. **Ambiguous** (yellow): yellow highlight for ambiguous values. **Subordinate** (gray): dimmed, subordinate display. |

In addition, the following base fields of the property table control the behavior in the configurator
(maintained in the m+m Material Types base module):

| Field | Explanation |
|---|---|
| **Mandatory** | When activated, the property must receive a value in the configurator; leaving with **OK** is only possible once no mandatory field is open anymore. If a **Default Value** is stored, the mandatory field counts as prefilled. |
| **Fix** | When activated, the property is included in the item search for the **Search Option** “Search Only Fix”; non-fixed properties are ignored for this search option. |
| **Default Value** | When set, the property is already prefilled with this value in the configurator; for hidden properties, the configurator adopts this value automatically. |
| **Sales Property / Purchase Property** | When activated, the property is assigned to the sales or purchase side; with the search option “Search Only Fix”, these properties are ignored. |
| **Value Filter / Value Group Filter** | When set, the filters restrict the **property values** available for selection in the configurator. |

**Action:**

- **Assign Category from Product Configurator:** When executed, the action assigns a previously chosen
  **Category Code** to all marked properties in a single step. This is the bulk variant of the assignment
  from the section *Setting up categories and sequence*.

### Marking text templates as a Product Configurator category

**Entry point:** template list of the m+m Extended Text module (via **Search**) -> **Templates**.

**Process intro.** This extension adds a flag to the text templates of the Extended Text module that signals
that a template is assigned to a Product Configurator category. In this way, master data managers can see in
the template maintenance which templates are used in the context of the Product Configurator.

| Field | Explanation |
|---|---|
| **Assigned in Product Configurator Category** | When set, the field indicates that the text template is assigned to a Product Configurator category; it serves as an overview during template maintenance and points to its use in the configurator text flow. |

---

## Daily Work in the Product Configurator

This section describes daily use by operational users. Availability in a document line depends directly on
the setup of the material type (see **Setting up the Product Configurator for a material type**): only
material types with active **Use For Product Configurator** and a checked document flag are available for
selection.

### Opening the configurator from a document line

The entry point is identical in all supported documents. In the document line, the **Product Configurator
Material Type** field is filled:

1. Open the document line and select the **Product Configurator Material Type** field in the line. The
   selection is restricted to material types released for the respective document type.
2. After selection, the system sets the line type to Item, saves the line, and opens the **Product
   Configurator** dialog.

Supported document lines (each with the **Product Configurator Material Type** field):

- **Sales:** Sales Quote, Sales Order, Sales Blanket Order.
- **Purchase:** Purchase Quote, Purchase Order, Purchase Blanket Order.
- **Production:** Production BOM lines as well as planned, firm planned, released, and finished production
  order lines.

> In production order lines, the configurator is only editable as long as neither a reservation nor a
> capacity ledger entry exists for the line. Otherwise the configurator opens for viewing only, and on
> opening the system points out the existing reservation or capacity ledger entry.

### Structure of the Product Configurator dialog

The **Product Configurator** dialog is divided into several areas:

- **Top left – main category:** the properties of the main category (Sequence 0) with the columns **Property
  Value**, **Property Value Name**, and **Unit**. The header shows material type, document number, and line
  number.
- **Top right – categories:** the **Assigned Categories** overview of the material type (excluding the main
  category). Clicking a category shows its properties.
- **Bottom – line area:** the properties of the selected category with **Description**, **Property Value**,
  **Property Value Name**, and **Unit**.
- **FactBoxes – Mandatory Fields / Not Filled Mandatory Fields:** all properties flagged as **Mandatory**. As
  soon as a mandatory field receives a value, it disappears from **Not Filled Mandatory Fields**; the display
  changes from red to green.
- **Print Type** and the FactBox of the extended text document types control or show the associated text
  outputs; via the **Preview** action, the composed text can be viewed in the text editor.

**Value entry.** Values are entered directly or selected from the stored **property values** via lookup.
After each entry, the rule flow is executed and the visibility filters are rebuilt – dependent properties or
categories can thereby be shown or hidden.

### Completion: finding or creating the item

1. Fill all **mandatory fields** until the **Not Filled Mandatory Fields** area is empty.
2. Confirm with **OK**. The system first checks whether all mandatory values of the main category have been
   captured, and then searches for a matching item:
   - **Match found:** the item and, if applicable, the variant are transferred into the document line.
   - **No match, Search Option “Unique Search”:** a new item is created directly via the **Item Template
     Code**, and the extended texts are generated from the text assignments.
   - **No match, but base item present:** an item variant is created from the base item and populated with
     the entered property values.
   Newly created items carry the **Created By Product Configurator** flag and are briefly blocked during the
   value transfer.
3. **Cancel** discards all entries; interim saving and resuming later is not possible.

> If a mandatory field is not filled, the system prevents leaving with **OK** and names the missing property
> together with its category. If no item is found or created, the system asks whether the page should be
> closed anyway.

### Extended texts in the production BOM

In production BOM lines, the **Extended Texts** action is available in addition to the **Product
Configurator Material Type** field. When executed, it opens the extended text worksheet for the item of the
line, so that the texts generated in the configurator flow can be viewed and maintained.

---

## Typical Use Cases

### Capturing a configured item in the sales order

**Trigger.** A customer calls and needs bar material in a specific dimension for which no item exists yet.

**Entry point in BC.** The user opens the customer's **Sales Order** and creates a new line. In the line,
they select the appropriate material type in the **Product Configurator Material Type** field; the **Product
Configurator** dialog opens.

**Core workflow.**
1. Capture the basic characteristics (e.g. material) in the main category.
2. Select the additional categories via the **Assigned Categories** and enter their property values.
   Visibility rules automatically hide properties that are not needed.
3. Check the **Not Filled Mandatory Fields** FactBox until it is empty and green.
4. Confirm with **OK**. If the system finds no matching item, it creates a new item via the **Item Template
   Code**, including description (Item Description Formula) and extended texts, and transfers it into the
   order line.

**Completion.** The order line now contains the configured item; the further order processing (prices,
delivery, invoicing) takes place in the BC standard.

### Making a new material type configurable

**Trigger.** A new product range is to be handled via the configurator in the future.

**Entry point in BC.** The administrator opens **Material Types** (via **Search**), selects the material
type, and opens the **Material Type Card**.

**Core workflow.**
1. On the **Product Configurator** tab, activate **Use For Product Configurator**, set the **Item Template
   Code** and **Search Option**, and check the document types.
2. Via **Related -> Product Configurator Categories**, create the **main category** (Sequence 0) and assign
   categories to the properties.
3. In the property table, flag the mandatory properties as **Mandatory** and set **Display Type**.
4. Optionally, store hiding rules via **Related -> Visibility of Properties and Categories** and define rules
   via **Product Configurator Rule Flow**.

**Completion.** The material type is now available in the released document types in the **Product
Configurator Material Type** field.

### Configuration in the production BOM

**Trigger.** A component is to be determined property-based for a production item.

**Entry point in BC.** The user opens the **Production BOM** and creates a component line. In the line, they
select the material type in the **Product Configurator Material Type** field.

**Core workflow.**
1. The **Product Configurator** dialog opens; the property values are captured.
2. With **OK**, the component (item/variant) is determined or created and transferred into the BOM line.
3. Via the **Extended Texts** action, the associated texts of the component can be viewed.

**Completion.** The production BOM contains the configured component for further production planning.

---

## FAQ and Troubleshooting

### 1. Why can't I select the Product Configurator Categories action?

The action is only active when the **Use For Product Configurator** field is activated on the **Material Type
Card** on the **Product Configurator** tab. If the flag is not set, **Product Configurator Categories**,
**Visibility of Properties and Categories**, and **Product Configurator Rule Flow** remain grayed out.

### 2. Why can't Use For Product Configurator be deactivated?

Deactivation is blocked as long as entries exist for this material type under **Visibility of Properties and
Categories**. First remove these entries; afterwards the flag can be cleared, whereby all document flags are
reset.

### 3. Why doesn't a property appear in the Product Configurator?

Only properties assigned to a **Category Code** are shown in the configurator. Assign the property to a
category via **Product Configurator Categories** or via the **Assign Category from Product Configurator**
action. In addition, the property may be hidden by a visibility rule.

### 4. Why does the system require a main category?

Per material type, exactly one category must carry **Sequence 0** (main category). Its properties appear in
the first area of the configurator. If the main category is missing, the system points this out when leaving
the **Material Property Category Relations**. Create it via **Create Main Category**.

### 5. Why can't I leave the configurator with OK?

As long as properties flagged as **Mandatory** without a value still appear in the **Not Filled Mandatory
Fields** FactBox, leaving with **OK** is prevented. The system names the missing property together with its
category. Fill all mandatory fields until the area is empty and green.

### 6. What happens if no item is found for my entries?

With the **Search Option** “Unique Search”, the system creates a new item directly via the **Item Template
Code**. If a base item exists, a variant is created from it instead and populated with the property values.
Without a stored **Item Template Code**, item creation is not possible.

### 7. Why isn't a property flagged as mandatory shown as not filled?

If a **Default Value** is stored for a mandatory property, the mandatory field counts as already filled. The
property then appears in the **Mandatory Fields** area, but not in **Not Filled Mandatory Fields**.

### 8. What does the Search Option “Search Only Fix” do?

With this option, the item search checks only properties with the **Fix** flag set on the **General** tab;
**Sales Property** and **Purchase Property** are ignored. The option cannot be set if a **Default Value** is
stored for non-fixed properties.

### 9. Why does a category or property suddenly disappear during entry?

Via **Visibility of Properties and Categories**, it may be set up that a specific value hides further
properties or entire categories (e.g. value “round” hides “thickness” and “width”). Hidden objects
automatically adopt their **Default Value**. The main category and its properties cannot be hidden.

### 10. Why can I only view the configurator in a production order line?

As soon as a reservation or a capacity ledger entry exists for the production order line, the configurator
opens read-only. On opening, the system points out the existing reservation or capacity ledger entry. Release
the reservation to be able to edit the configuration again.
