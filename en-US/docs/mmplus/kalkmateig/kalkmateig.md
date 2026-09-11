---
title: Anwenderhandbuch m+m Calculation with Material Properties
---

# User Guide m+m Calculation with Material Properties

## Introduction

The app **m+m Calculation with Material Properties** extends the m+m app **Calculation** in Microsoft Dynamics 365 Business Central with the evaluation of **material properties** within a calculation. It makes it possible to derive an item's calculation price not only from fixed line values, but additionally from the **properties** of the material: depending on the stored **material type**, **property** and its **value**, defined **costs** flow into the calculation line.

In addition, the app provides two further derivation methods for calculation lines: the direct transfer of a numeric **document property value** into the line, as well as a freely definable **calculation formula** that combines property values and arithmetic operators. Finally, an **item** can be flagged so that, when a sales line is entered, a calculation is automatically created, certified, and its **sales price** is written into the line.

**Target audience:** This guide is aimed primarily at **operational users in sales and calculation** who enter sales documents, open calculations and maintain their properties. Secondarily, it addresses **administrators and key users** who set up the calculation templates, the material property costs and the item flag.

**Brief process overview:** The administrator first stores the **material property costs** and extends a **calculation template** with the new **field type**. In day-to-day business, the calculation is created either automatically when a sales line is entered (if the item is flagged accordingly) or manually via the **Create/Open Calculation** action on the document line. The user can subsequently adjust the **properties** of a calculation via the **Edit Properties** action and have it recalculated.

A prerequisite is that the dependent apps **m+m Calculation** and **m+m Material Properties** are installed and set up: the **material types** and **properties** come from the m+m Material Properties app, and the **calculation template** and the calculation document come from the m+m Calculation app.

## Quick start for users

The fastest path from setup to the calculated price. The setup steps are a prerequisite and must be performed in this order; only afterwards does the daily work follow.

1. **Check properties and material types (prerequisite, app m+m Material Properties).** Make sure that the required **material types** and **properties** including their data type are already maintained, because the material property costs refer to them.
2. **Store material property costs.** Open the **Material Property Costs** list via search and enter, for each combination of **Material Type Code**, **Property Code** and **Value** (or **Value**/**To Value** as a range), the associated **Cost**. See *Setup → Setting up material property costs*.
3. **Extend the calculation template.** In **Calculation Templates**, open the desired template and, in a line, set the **Field Type** to **Material Property Cost** (or to **Use Document Property Value** or **Use Calculation Formula**). See *Setup*.
4. **(Optional) Flag the item for automatic calculation.** On the **Item Card**, in the **Prices & Sales** FactBox, set the **Automatically Calculate** flag. See *Setup → Setting up automatic calculation*.
5. **Create the calculation in the document.**
   - *Automatically:* In the **Sales Order**, enter a line with the flagged **item** and a **quantity**. When the quantity is confirmed, the calculation is created, set to **Certified**, and the **sales price** is written into the line as the unit price.
   - *Manually:* On the document line, choose **Line → Function → Create/Open Calculation** and the desired **calculation template**.
6. **(If required) Adjust properties.** Open the **calculation** and choose the **Edit Properties** action to change the property values and have the calculation recalculated.

## Setup

Setup is the most extensive part of this app and is to be carried out in Business Central. It comprises three areas that build on one another: the **material property costs** (cost matrix), the **calculation template** (which derivation method a line uses), and the **automatic calculation** on the item. In addition, this section describes the supplied **permission**.

All three functional derivation methods of this app are controlled via **one** new set of values of the **Field Type** field in the **calculation template**. The app adds three values to the field type:

| Field Type (value) | Explanation |
|---|---|
| **Material Property Cost** | When a template line receives this field type, the calculation determines the line value from the stored **material property costs**: for each property of the assigned **material type**, the matching cost rate is looked up and summed. Without this field type, the line keeps its previous derivation. |
| **Use Document Property Value** | When set, the calculation transfers the **numeric** value of a property stored in the document (calculation header) directly as the line value. Only properties of data type **Decimal** or **Integer** are allowed; otherwise the calculation aborts with a message. |
| **Use Calculation Formula** | When set, the calculation computes the line value from a freely defined **calculation formula** that combines numeric document properties, numbers and the operators `+ - * / ^` as well as parentheses. If the formula is invalid, the calculation is aborted with a message. |

> Note: The **Field Type** field also contains the values already defined by the base app m+m Calculation. Only the three values listed above are added and controlled by this app.

### Setting up material property costs

**Who/when:** The administrator or key user sets up the material property costs **before the first calculation**. They are the cost basis from which the **Material Property Cost** field type in the calculation template (see below and *Daily work*) obtains its line value.

**Entry point:** Open the **Material Property Costs** list via search (the list is available under *Administration* and can be found via search).

The list forms a matrix: for a **material type** and one of its **properties**, a **cost rate** is stored for a specific **value** – or for a value range from **Value** to **To Value**.

| Field | Explanation |
|---|---|
| **Material Type Code** | When set, the cost rate applies only to calculations of items of this **material type**; the selection is made from the material types maintained in m+m Material Properties. If the field is left empty, the rate applies across material types for the specified property. |
| **Property Code** | When set, the cost rate refers to this **property** of the material type (mandatory field). The selection is made from the properties stored in the system. This determines which property controls the cost contribution. |
| **Value** | When set, the cost rate applies for exactly this property value. For properties with a stored value list (**Use Property Values** = Yes), only valid property values can be selected. For numeric or date properties, **Value** forms the lower bound of a range. |
| **To Value** | When set, **Value** to **To Value** defines a **range**: the cost rate applies if the document's property value lies within this range. **To Value** must be greater than **Value**, otherwise the message "Cannot be smaller or equal than the first value." appears. If **To Value** is left empty, the rate applies only to the exact **Value**. |
| **Cost** | When set, this is the amount that flows into the calculation line of the **Material Property Cost** field type when there is a match. Several matching properties are added together. |
| **Use Property Values** | Display field: if Yes, the associated property has a fixed value list, and the **Value**/**To Value** fields allow only these valid property values; if No, free numeric or date entries and ranges are possible. The field is derived from the property and is not editable. |

**Data-type-dependent value determination (from the code):** The property's data type (**Data Type**: Text, Decimal, Integer, Date – defined in m+m Material Properties) determines how **Value**/**To Value** are interpreted:

- **Decimal / Integer:** The input is converted into a **Numeric Value** (rounded for Integer). During calculation, the range **Value ≤ document value ≤ To Value** applies.
- **Date:** The input is interpreted as a **Date Value**; the calculation checks **Value ≤ document date ≤ To Value**.
- **Text / value list:** The value is checked for **equality**.

If an input cannot be converted into the property's data type, the message "(Value) cannot be converted to (Data Type)." appears.

**Process steps (activating the material property costs in the calculation):**

1. **First**, in m+m Material Properties, make sure that the **material type** and **property** (with the appropriate **data type**) exist – without this master data, no cost rates can be created.
2. **Then**, in **Material Property Costs**, store the **Cost** for each combination of **Material Type Code**, **Property Code** and **Value**/**To Value**.
3. **Next**, in the **calculation template**, set a line to the **Material Property Cost** field type (see *Setting up the calculation template*).
4. **Finally**, the cost contribution is created automatically in day-to-day business as soon as a calculation is computed for an item of this material type (see *Daily work → Calculation and properties*).

Cross-link: The costs stored in this way take effect via the **Material Property Cost** field type in *Setting up the calculation template* and appear in the result under *Daily work*.

### Setting up the calculation template (field type)

**Who/when:** The administrator extends the existing **calculation template** of the m+m Calculation app before the template is used in day-to-day business. Creating a calculation template itself is described in the documentation of the m+m Calculation app; this app merely adds the control via the **Field Type** and three additional fields on the template line.

**Entry point:** In **Calculation Templates**, open the desired template; the lines are edited in the template's subform. (Accessible via the calculation templates of the m+m Calculation app, not via a dedicated page of this app.)

On the template line, in addition to the base fields (including **Field Type**, **Description**, **Value**), the following fields added by this app are available. They are each only editable when the appropriate **Field Type** is selected:

| Field | Explanation |
|---|---|
| **Material Type** | Only editable when the field type is **Material Property Cost**. When set, only the material property costs of this **material type** are used in the calculation; the selection is made from the material types from m+m Material Properties. When the field type is switched away from **Material Property Cost** again, the system clears this entry automatically. |
| **Document Property Code** | Only editable when the field type is **Use Document Property Value**. When set, the line takes the numeric value of this document property directly. Only properties of data type **Decimal** or **Integer** can be selected. When the field type is switched away, the entry is cleared automatically. |
| **Calculation Formula** | Only editable when the field type is **Use Calculation Formula**. When set, the line calculates its value from this formula. Via the assist function (AssistEdit) on the field, the formula editor of the m+m Material Properties app opens, in which property codes, numbers, parentheses and the operators `+ - * / ^` are assembled. When the field type is switched away, the formula is cleared automatically. |

**Important – dependent field maintenance (from the code):** If the user changes a line's **Field Type** away from one of the three app values, the system automatically resets the respective associated detail field (**Material Type**, **Document Property Code** or **Calculation Formula**) so that no contradictory entries remain.

**Process steps:**

1. **First**, create the line in the calculation template and choose the **Field Type**.
2. **Then** – depending on the field type – maintain the **Material Type**, the **Document Property Code** or the **Calculation Formula**.
3. **Next**, use the template in the document; the chosen field type determines where the line value comes from during calculation (see *Daily work*).

### Setting up automatic calculation

**Who/when:** The administrator flags individual **items** so that their **sales price** is automatically determined from a calculation when a sales line is entered. This requires that a **default calculation template** is set up in the m+m Calculation app for the item or the customer/item combination.

**Entry point:** **Items** (list) → open **Item Card** → **Prices & Sales** FactBox.

| Field | Explanation |
|---|---|
| **Automatically Calculate** | When activated, entering a sales line with this item automatically creates or reuses a calculation, certifies it, and writes the resulting **sales price** as the unit price into the document line. When deactivated, the item behaves as in the standard – the price is not calculated automatically. |

**Process steps (end-to-end activation):**

1. **First**, set up a **default calculation template** in m+m Calculation that applies to the item. If it is missing, the system reports during the automatic run: "No calculation template could be determined for item (No.). Set up a default calculation template."
2. **Then** – if material property costs are to flow in – extend the template with the appropriate **Field Type** according to *Setting up the calculation template*.
3. **Next**, set the **Automatically Calculate** flag on the **Item Card**.
4. **Finally**, the price is created automatically in day-to-day business when the document line is entered (see *Daily work → Automatic calculation in the sales document*).

Cross-link: The operational trigger is described in *Daily work* and in *Typical use cases → Auto-calculation in the sales order*.

### Permissions

The app supplies the permission set **m+m Calculation with Material Properties**. It defines which actions users can perform in this app: it comprises full access (read, modify, insert, delete) to the **Material Property Cost** table as well as the execution rights for the **Material Property Costs** page, the **Edit Properties** dialog and the associated processing codeunits. Assign this permission set to the users who are to maintain material property costs or edit the properties of a calculation.

## Master data

### Material Property Costs

The central master data table introduced by this app is the **Material Property Costs** list. It is both a setup and a master data object: it permanently describes which **cost contribution** results from which combination of **material type**, **property** and **value** (range). The complete field description, the data-type logic and the creation process are documented in *Setup → Setting up material property costs*.

**Where the values take effect:** The records are evaluated in every calculation whose template line carries the **Material Property Cost field type** and whose item has a matching **material type**. The cost contribution then appears as the line value in the **calculation** (see *Daily work*).

### Flagging an item for auto-calculation

The item is the master record on which automatic calculation is activated. The **Automatically Calculate** field added for this purpose on the **Item Card** is fully described in *Setup → Setting up automatic calculation*. Administrators maintain this flag per item; in the sales document it decides whether the price is calculated automatically.

> The material types and properties themselves are master data of the **m+m Material Properties** app and are maintained there. This app only refers to them.

## Daily work: calculation and properties

These sections are controlled by the setup: the **Field Type** of the calculation template used (see *Setup*) determines where each line obtains its value, the **material property costs** supply the cost contributions, and the item flag **Automatically Calculate** decides on the automatic process. The following areas describe the document interfaces that this app extends.

### Calculation header: Edit Properties

On the **calculation** (calculation header), the app adds the **Edit Properties** action (in the ribbon among the process actions, additionally as a promoted action) as well as a FactBox that displays the current **properties** of the calculation header.

**Entry point:** **Calculations** (list) → open **calculation** → **Edit Properties** action.

Flow of the **Edit Properties** action (from the code):

1. If the calculation is **certified**, the system asks: "The calculation (No.) is certified. Do you want to set it to 'Under Development' to edit the properties?" Only after confirmation is the status set to **Under Development**; otherwise the action aborts. A calculation that is neither **certified** nor **Under Development** cannot be edited this way (message: "Only certified calculations can be edited this way …").
2. If there is a link to a **sales line**, the system asks: "Do you want to update the property values of the calculation with the current properties of the linked sales line?" On confirmation, the properties of the sales line are transferred into the calculation header.
3. The property editor opens as the **Edit Properties** dialog. Changes act directly on the properties of the calculation header.
4. When closing with **OK**, the calculation is **recalculated**. When closing with **Cancel** (or via the window close icon), all changes are discarded and the previous state is restored.

Editing is only possible in the **Under Development** status; therefore a certified calculation is reset before editing, after a confirmation prompt.

### Calculation lines: Document Property Code and Calculation Formula

In the subform of the **calculation** (calculation lines), the app adds two fields that – analogous to the template – are editable depending on the line's **Field Type**:

| Field | Explanation |
|---|---|
| **Document Property Code** | Only editable when the line has the **Use Document Property Value** field type. When set, the line reads the numeric value of this document property from the calculation header and uses it as the line value. |
| **Calculation Formula** | Only editable when the line has the **Use Calculation Formula** field type. When set, the line calculates its value from the formula. Via the assist function on the field, the formula editor opens, which offers property codes of the calculation header, numbers, parentheses and operators. |

The line's **Material Type** field is filled with the **Material Property Cost** field type and is not editable in the lines; it documents for which material type the cost contribution was determined.

**Value determination during calculation (from the code):** When calculating a line, the app checks the **Field Type** and determines the value accordingly:

- **Material Property Cost:** For each property of the calculation header that matches the line's **material type**, the cost rate is looked up in **Material Property Costs** (exact **Value**, otherwise numeric range **Value ≤ x ≤ To Value**, otherwise date range) and summed.
- **Use Document Property Value:** The **numeric** value of the document property is transferred directly (only data type Decimal/Integer allowed).
- **Use Calculation Formula:** The formula is evaluated, with property codes being replaced by their numeric values; unknown codes are substituted as 0.

Before the lines are calculated, the app ensures that the calculation header carries the document properties of its **primary source** (the linked sales line), so that lines of the **Use Document Property Value** and **Use Calculation Formula** field types do not yield 0.

### Automatic calculation in the sales document

If an **item** is flagged with **Automatically Calculate** (see *Setup*), the following process runs automatically when the sales line is entered – without the user manually opening the calculation:

1. The user enters a line of type **Item** in the **Sales Order** (or another sales document) and confirms the **quantity**.
2. Only while the document status is **open** does the app create or use a **calculation** for this line and determine the associated **default calculation template**.
3. The calculation is computed and set to **Certified**.
4. The resulting **sales price** – rounded according to the rounding precision from the General Ledger Setup – is written as the **unit price** into the sales line.

If a matching default calculation template is missing, the system reports this (see *Setup → Setting up automatic calculation*). The automatic run is protected against reentry and is only triggered for non-temporary item lines.

## FAQ and troubleshooting

### 1. Why do no material property costs flow into my calculation?
Check three points: the template line must have the **Material Property Cost field type**, the item must have a **material type**, and a matching record must exist in **Material Property Costs** (same **Material Type Code**, **Property Code** and a matching **Value** or range). If one of these points is missing, the cost contribution remains 0.

### 2. Why can I not fill in the "Material Type" / "Document Property Code" / "Calculation Formula" field in the template?
These fields are each only editable when the appropriate **Field Type** is selected: **Material Type** with **Material Property Cost**, **Document Property Code** with **Use Document Property Value**, and **Calculation Formula** with **Use Calculation Formula**. Set the **Field Type** first.

### 3. What happens if I subsequently change a line's field type?
The system automatically clears the detail field belonging to the old field type (**Material Type**, **Document Property Code** or **Calculation Formula**) so that no contradictory entries remain. You must maintain the detail field for the new field type again.

### 4. Why do I get the message "To Value cannot be smaller or equal to the first value"?
For a numeric range in **Material Property Costs**, **To Value** must be strictly greater than **Value**. Correct the upper range value or leave **To Value** empty if the rate is to apply only to the exact **Value**.

### 5. Why does "(Value) cannot be converted to (Data Type)" appear?
The entered **Value** or **To Value** does not match the property's **Data Type** (e.g. text instead of a number for a numeric property). Enter a value in the correct data type.

### 6. Why does the system report that only numeric document properties are allowed for a calculation formula?
In a **calculation formula** and with **Use Document Property Value**, only document properties of data type **Decimal** or **Integer** may be used. If the formula refers to a text or date property, the calculation aborts with this message. Use only numeric properties.

### 7. Why is my calculation formula reported as invalid?
The formula contains an expression that cannot be evaluated (e.g. a missing parenthesis or an invalid character string). Allowed are numbers, property codes and the operators `+ - * / ^` with parentheses. Use the formula editor via the assist function on the **Calculation Formula** field to assemble valid expressions.

### 8. Why can I not edit the properties of a calculation?
Editing via **Edit Properties** is only possible in the **Under Development** status. A **certified** calculation is automatically set to **Under Development** after a confirmation prompt. A calculation that is neither certified nor under development cannot be edited this way.

### 9. Why is no price automatically calculated when I enter a sales line?
Automatic calculation only runs if the **item** carries the **Automatically Calculate** flag, the line is of type **Item**, and the document status is **open**. The run is triggered when the **quantity** is confirmed. If the flag is missing or the document is already released, automatic calculation is omitted.

### 10. Why do I get "No calculation template could be determined for item (No.)"?
For automatic calculation, a **default calculation template** for the item (or the customer/item combination) must be set up in the m+m Calculation app. Set up a suitable default template so that the automatic calculation finds a template.

## Typical use cases

### Auto-calculation in the sales order

1. **Trigger:** The internal sales team receives an order by phone for an item whose price results from material properties (e.g. depending on a customer number or a material key figure).
2. **Entry point in BC:** The user opens a **Sales Order** and enters a line of type **Item** with the relevant **item** and the **quantity**. The item is flagged with **Automatically Calculate** via the **Item Card**.
3. **Core flow:** When the **quantity** is confirmed, the app creates a **calculation** in the background, determines the **default calculation template**, computes the calculation, sets it to **Certified** and writes the determined **sales price** as the unit price into the line. If material property costs are involved, the steps from *Setup → Setting up material property costs* are required beforehand.
4. **Completion:** The user sees the automatically set price in the document line and continues the sales order in the standard way. If required, subsequent reworking of the underlying calculation is possible via *Adjusting the properties of a calculation*.

### Adjusting the properties of a certified calculation

1. **Trigger:** After feedback from sales, the calculation price of an already-calculated order must be adjusted because a material property has changed.
2. **Entry point in BC:** The user opens the relevant **calculation** via **Calculations** and chooses the **Edit Properties** action.
3. **Core flow:** Because the calculation is **certified**, the user confirms the prompt to set it to **Under Development**. Optionally, they adopt the current properties of the linked **sales line**. In the **Edit Properties** dialog, they adjust the property values. With **OK**, the calculation is **recalculated**; with **Cancel**, the previous state is retained.
4. **Completion:** The recalculated value is available in the calculation and – for linked documents – as the basis for the further sales process.
