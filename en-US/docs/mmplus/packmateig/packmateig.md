---
title: Anwenderhandbuch m+m Package Management with Material Properties
---

# User Guide m+m Package Management with Material Properties

## Introduction

The app **m+m Package Management with Material Properties** connects two existing m+m applications: package management (**Package Setup**, **Package References**) and material properties (**Material Types**, **Properties**). It makes it possible to assign a package structure no longer just to a single item, but to entire **Material Types** or to a selection of items defined by properties – the **Property Filter**. As a result, you maintain a packaging rule once, centrally, instead of storing it individually on every affected item.

**Target audience.** The primary users are operational employees who maintain **Package References** in day-to-day business and assign the appropriate package to a material type or a property filter (packaging planning, work preparation, warehouse). The secondary audience is administrators and key users who store the number series in the **Package Setup** and prepare the **Material Types** and **Properties** in the master data.

**Brief process overview.** First the administrator sets up the **Property Nos.** in the **Package Setup**. In the master data the user maintains the **Material Types** and their **Properties** (Material Properties base module). Then – if a selection narrowed down by properties is needed – the user creates a **Package Reference Property Filter Card** and there defines the **Lines** with **Property Code** and **Filter Value**. Finally, via the **Package References** action, the user opens the **Package References** page and assigns the specific package to the chosen **Product Type** (material type or property filter).

## Quick Start for Users

The following sequence matches the dependency chain in the code: first setup, then master data, then the assignment.

1. **Setup (one-time):** Using **Search**, open the **Package Setup** page and, on the **General** tab, enter a number series under **Property Nos.**. Without this entry no property filter card can be created.
2. **Select material type:** Using **Search**, open the **Material Types** list and select the row of the desired material type.
3. **Direct assignment (Product Type Material Type):** In the row, choose the **Package References** action. The **Package References** page opens, pre-filtered to this material type. Create a line, fill in **Package Reference No.**, **Package Type** and **Package No.**, and close with **OK**.
4. **Property-based assignment (Product Type Property Filter):** Using **Search**, open the **Package Reference Property Filter List**, create a **Package Reference Property Filter Card** with a new line, select the **Material Type Code**, and, in the **Lines** subtab, capture a **Property Code** and a **Filter Value** for each characteristic.
5. **Assign a package to the property filter:** On the property filter card, choose the **Package References** action. On the **Package References** page (pre-filtered to the Product Type Property Filter), create the package as in step 3.

This module has **no** posting or release run. The work ends with saving the package reference; there is no message, no document, and no posting.

## Setup

The setup of this module is deliberately lean, because the app adds only a single configuration value: the **Property Nos.**. This value, however, controls the entire property-based chain and is therefore described here in full and in process context.

### Package Setup – added fields

**Who/when/why.** The administrator stores this value once before first use, company-wide. The **Package Setup** is a company-wide setup page (one record per company) of the base module and is opened via **Search**. The app adds one field to the page on the **General** tab.

**Entry point:** Using **Search**, open the **Package Setup** page, **General** tab.

| Setup | Explanation |
|---|---|
| **Property Nos.** | If a number series is stored here, the system automatically assigns the next available number from this series to the **No.** field when a new **Package Reference Property Filter Card** is created; if the field is empty, creating a property filter card is aborted with an error message. Without this setup, the property-based package assignment therefore cannot be used. |

Additionally visible on the same page are the fields of the base module **Package**. For the property-based assignment only the **Property Nos.** is relevant; the other controls of the base module available on the **General** tab concern general package management:

| Setup (base module, context) | Explanation |
|---|---|
| **Vertical Partition Symbol** / **Horizontal Partition Symbol** | If a symbol is set, package management uses this character to represent vertical or horizontal partitions within a package structure; this has no effect on the property filters. |
| **Package Assignment** | Controls, in the base module, how packages are assigned to documents; not relevant for the property-based reference. |
| **Item Reclass Template Name** / **Item Reclass Batch Name** | If set, the base module uses this journal template or journal batch for item-related reclassifications (transfers) of package management; not required for the property filters. |

> Note: Further fields of the **Package Setup** belong exclusively to the base module Package and do not affect the property-based assignment. For using this app, the **Property Nos.** is sufficient.

### Setting up property-based package references

This chain connects four levels: master data of the material properties → global number series → property filter card → operational assignment. It is described here as a coherent process; the individual pages are documented in detail in the following chapters.

**Process entry point.** The chain is configured by a key user in packaging planning before property-based package references are used for the first time in day-to-day business. The result is later used by the user on the **Package References** page (see chapter **Daily Work**).

**Enablement steps in dependency order:**

1. **First**, in the Material Properties base module, maintain the **Material Types** and, per material type, the associated **Properties**. So that a selection list appears in the filter value, activate the **Use Property Values** flag on the respective property: if activated, the user can later select the **Filter Value** from the stored property values; if not activated, they enter the filter freely.
2. **Then** store the **Property Nos.** in the **Package Setup** (see above). If this value is missing, no property filter card can be created in the next step.
3. **Next**, create a **Package Reference Property Filter Card**, select the **Material Type Code**, and, in the **Lines** subtab, define the combination of **Property Code** and **Filter Value** (see chapter **Master Data**). Once a line is filled, it narrows the selection of items to those that match this property characteristic.
4. **Finally**, on the property filter card, open the **Package References** action and assign the specific package to the filter. This completes the chain; the assignment takes effect as soon as a package structure is needed for a matching item (see chapter **Daily Work**).

**Dependency and validation notes.** The **Material Type Code** on the property filter card must be set before a line with a **Property Code** can be captured; when the line is captured, the system checks that the selected property actually belongs to the material type of the card. If the material type is changed or the **Property Code** of a line is cleared or switched, the system automatically resets the associated **Filter Value** so that no unsuitable filter remains.

## Master Data

The app brings its own master data page – the **Package Reference Property Filter Card** – and extends the existing material type pages with a navigation action.

### Material Types and the Package References action

**Who/when/why.** Material types are created and maintained by master data maintenance in the Material Properties base module. The app extends both the **Material Types** list and the **Material Type Card** with the **Package References** action, which assigns a package structure directly to an entire material type. Users apply this action when the same packaging applies to all items of a material type.

**Entry point:** Using **Search**, open the **Material Types** list and select the relevant row; alternatively, open the **Material Type Card** from the row.

The app adds **no** field of its own here; the material type itself (code, description, properties) is maintained in the Material Properties base module. Only the following action is added:

| Action | Explanation |
|---|---|
| **Package References** | If you choose this action on a material type, the **Package References** page opens, pre-filtered to the **Product Type** Material Type and the code of this material type. There you assign one or more packages to the material type; the product and reference columns are hidden, because the reference is already fixed by the selected material type. |

Cross-link: Maintaining the package lines themselves is described in the chapter **Daily Work**; the property-based alternative in the next section.

### Package Reference Property Filter (property filter card and lines)

**Who/when/why.** The key user creates this master data when a packaging rule is to apply not to an entire material type, but only to the items of a material type with certain property characteristics (e.g. only a specific dimension or quality). The card thus defines a named **Property Filter** to which a package is later assigned.

**Entry point:** Using **Search**, open the **Package Reference Property Filter List** and create a **Package Reference Property Filter Card** with a new line; an existing one is opened by selecting the list row.

Header fields of the **Package Reference Property Filter Card** (**General** tab):

| Field | Explanation |
|---|---|
| **No.** | Unique number of the property filter. If you leave the field empty when creating, the system assigns the next number from the **Property Nos.** of the **Package Setup**; if no series is stored, creation is aborted. |
| **Material Type Code** | If you select a material type, the system determines which material type the properties allowed in the lines come from; only afterward can lines with a **Property Code** be captured. The field must be filled before a line is created. |
| **Description** | If you enter text here, it appears as a meaningful designation of the filter in the **Package Reference Property Filter List** and makes it easier to find again. |

Lines in the **Lines** subtab (each line narrows the item selection by one characteristic):

| Field | Explanation |
|---|---|
| **Property Code** | If you choose a property code, you determine which characteristic of the material type is filtered on. The system only allows properties that belong to the material type of the header; if the code does not fit, the entry is rejected. |
| **Property Name** | Displays the name of the selected property. The field is determined automatically from the **Property Code** and is not editable. |
| **Filter Value** | If you set a value, the system filters the items to those whose property characteristic matches this value. Via the lookup function (AssistEdit) in the field the following applies: if **Use Property Values** is activated on the property, you select one or more stored values from a list (multiple selection is applied as an OR combination); otherwise the Material Search dialog opens, in which you assemble the filter expression. If you clear the **Property Code**, the **Filter Value** is automatically reset. |

**Process steps.** First select the **Material Type Code**, then create a line with **Property Code** and **Filter Value** for each desired characteristic, and finally, via the **Package References** action (see below), assign the package.

| Action | Explanation |
|---|---|
| **Package References** | If you choose this action on the property filter card, the **Package References** page opens, pre-filtered to the **Product Type** Property Filter and the **No.** of this filter. There you store the package for exactly this property filter. |

**Deletion behavior.** When deleting a property filter card, the system checks whether a package reference already exists for this filter; if so, deletion is prevented with the note "A Package Reference exists." The associated **Lines** are automatically removed when the card is deleted. Likewise, the system prevents the deletion of a **Material Type** or a **Property** as long as it is still used in a package reference or in a property filter line.

## Daily Work: Package References

The actual assignment of a package takes place on the **Package References** page of the base module. This page is extended by the app with the **Material Type Code** column and is opened pre-filtered via the **Package References** action – from the material type, from the material type card, or from the property filter card.

**Setup/master data reference.** This transactional page is controlled by the previously maintained master data: the **Package Setup** (Property Nos.), the **Material Types**/**Properties** (Material Properties base module), and the **Package Reference Property Filter Card**. If one of these building blocks is not maintained, the corresponding assignment is not available (see chapters **Setup** and **Master Data**).

**Entry point:** Open the **Package References** page via the **Package References** action – on a material type, on the material type card, or on a Package Reference Property Filter Card. A direct call via **Search** is not intended for the property-based cases, because the page is always opened pre-filtered to the respective **Product Type**.

When opened via one of these actions, the product and reference columns are hidden; visible and to be maintained are in particular:

| Field | Explanation |
|---|---|
| **Package Reference No.** | If you assign a number here, you uniquely identify the individual package assignment; the field is mandatory. |
| **Package Type** | Determines which kind of package is assigned. If you change the package type, the system resets **Qty. per Package** and **Package No.** so that no unsuitable combination remains. |
| **Package No.** | If you choose a package, you determine which specific package (or which package BOM or category) applies to the filtered scope; mandatory field. |
| **Qty. per Package** | If you enter a quantity, it determines how many units are applied per package. For the package type Package Category the field is blocked, because no fixed quantity is permitted there. |
| **Unit of Measure Code** | Defines the unit of measure to which the quantity per package refers. |
| **Variant Code** | Optionally narrows the assignment to a specific item variant. |
| **Description** | Free text to explain the assignment. |
| **Keep Item Tracking Separate** | If activated, the base module keeps the item tracking of this package assignment separate; this controls the behavior of the downstream package processes in the base module. |
| **Material Type Code** (column added by this app) | Shows, for each package reference, the material type of the assigned item. The value is determined automatically from the item and is not editable; it serves to immediately recognize property-based and material-type-based assignments in the list. |

### Product Type – the values added by this app

The **Product Type** of a package reference determines what the assignment refers to. The app extends the selection with three values. The two actions of this app each set the product type automatically, so that the user does not have to choose it manually:

- **Material Type:** The package reference applies to **one** material type. This value is set automatically by the **Package References** action on the material type or the material type card; the material type code is kept as the **Item No.**.
- **All Material Types:** The assignment applies across material types as a default value. This value is available as a selection when a cross-cutting rule without restriction to a single material type is desired.
- **Property Filter:** The package reference applies to all items that match the filter defined on the **Package Reference Property Filter Card**. This value is set automatically by the **Package References** action on the property filter card; the **No.** of the property filter is kept as the reference.

## FAQ and Troubleshooting

### 1. Why can't a property filter card be created?
Because no **Property Nos.** is stored in the **Package Setup**. The system assigns the **No.** from this series; if it is missing, creation is aborted. Enter the number series in the setup first.

### 2. How do I assign a package to an entire material type without maintaining individual items?
Open the **Material Types**, select the row and then the **Package References** action. On the **Package References** page you create the package; the **Product Type** Material Type is set automatically.

### 3. Why can't I select a property code in a filter line?
Because no **Material Type Code** is set yet on the property filter card, or the selected **Property Code** does not belong to this material type. Set the material type code first; afterward only the properties of this material type are permitted.

### 4. Why does my filter value disappear when I change the property code?
This is intentional: when switching or clearing the **Property Code**, the system automatically resets the **Filter Value** so that no value remains that no longer fits the property. Capture the filter value again after the switch.

### 5. When do I get a selection list for the filter value, and when must I enter it freely?
This depends on the **Use Property Values** flag of the respective property. If it is activated, you select the **Filter Value** from the stored property values (also several, as an OR combination); if it is not activated, you assemble the filter in the Material Search dialog.

### 6. Can I allow multiple property values in one filter line?
Yes. Select multiple values in the selection dialog; the system applies them as an OR combination into the **Filter Value**. The package reference then takes effect for items that carry any one of the selected values.

### 7. Why can't I delete a property filter card?
Because a **Package Reference** already exists for this filter. Remove the associated package reference first; afterward the card can be deleted. The **Lines** of the card are automatically removed on deletion.

### 8. Why can't a material type or a property be deleted?
Because it is still used in a package reference or in a property filter line. The system prevents deletion with the note that an entry exists. Release the assignment first, then deletion is possible.

### 9. Do I have to set the product type of the package reference manually?
No. Always open the **Package References** page via the **Package References** action – on the material type the product type **Material Type**, on the property filter card the product type **Property Filter** is preset automatically and the page is pre-filtered accordingly.

### 10. Do I have to post or release anything after assigning?
No. This module has no posting, release, or messaging run. The assignment is effective once the package reference is saved.

## Typical Use Cases

### Use case 1: Package for a selection narrowed down by properties

**Trigger.** Packaging planning receives the requirement that items of a material type with a certain property characteristic (e.g. a specific dimension) should in future receive a special package.

**Entry point in BC.** The user first ensures that the **Property Nos.** is stored in the **Package Setup**. Then, using **Search**, they open the **Package Reference Property Filter List**.

**Core process.** The user creates a **Package Reference Property Filter Card** with a new line, selects the **Material Type Code**, and captures a **Property Code** in the **Lines** subtab. In the **Filter Value** they select the desired value from the list – since **Use Property Values** is active on the property. Then they choose the **Package References** action; on the **Package References** page (Product Type Property Filter, pre-filtered to the filter number) they enter **Package Reference No.**, **Package Type**, **Package No.** and **Qty. per Package**.

**Completion.** Once the package reference is saved, the process is complete; posting or releasing is not required. In the **Package References** list, the user recognizes the assignment by the **Material Type Code** column.

### Use case 2: Package for an entire material type

**Trigger.** The same package applies uniformly to all items of a material type; a restriction via properties is not necessary.

**Entry point in BC.** The user opens the **Material Types** list using **Search** and selects the relevant row (alternatively the **Material Type Card**).

**Core process.** The user chooses the **Package References** action. The **Package References** page opens pre-filtered to the **Product Type** Material Type and the material type code. They create a line and fill in **Package Reference No.**, **Package Type**, **Package No.** as well as **Qty. per Package** and **Unit of Measure Code**.

**Completion.** After saving, the packaging rule applies to the entire material type. Here too there is no downstream posting or release step.
