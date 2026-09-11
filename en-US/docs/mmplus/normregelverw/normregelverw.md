---
title: Anwenderhandbuch m+m Aided Data Management
---

# m+m Aided Data Management User Guide

The **m+m Aided Data Management** app provides **rule-based data management** in Microsoft Dynamics 365 Business Central: you define **rules** once and, in **rule flows**, assign them to a **material type**. As soon as an item of that material type is unblocked, the system automatically checks and sets the item master data – properties, material filters, routings and production BOMs – according to your rules. The module replaces manual, error-prone maintenance steps with traceable, reusable automation.

## Introduction

### Purpose of the module

The module automates the build-up of item master data. Instead of manually populating every new item with property values, routing operations and BOM components, you set up **rules** that calculate, compare, look up or write values into target fields. Several rules are logically linked in a **rule flow** (with **If/Else/End** branches) and assigned per area to a **material type**. Execution happens automatically when the item is **unblocked**.

### Target audience

- **Operational users in item creation and production engineering** are the primary audience: they create items, set the **Material Type**, maintain property values and **unblock** the item so that the rule flows build up its master data.
- **Key users and administrators** are the secondary audience: they configure the **Rule Setup** and define **rules** and **rule flows**.

### Brief process overview

The typical path through the module follows this chain:

1. Perform the **Rule Setup** (number assignment for routings and production BOMs).
2. Define **rules** (one behavior per **Rule Type**, optionally with a **Rule Matrix** and **Rule Properties**).
3. Chain the rules into a **rule flow** on the **Material Type Card** (Property, Material Filter, Routing, Production BOM and Prod. Order Routing rule flow).
4. In day-to-day operations, create an item with a matching **Material Type**; the item is automatically set to **Blocked**.
5. **Unblock** the item – the rule flows run in sequence and build up the master data.

## Quick start for users

This quick start describes the shortest path from an empty system to an automatically built item. The setup steps are a prerequisite and therefore come first.

1. **Open Rule Setup** (via **Search**) and define how **Routing Nos From** and **Prod. BOM Nos From** are assigned (**No. Series** or **Item No.**).
2. **Define rules:** Open the **Rules** list (via **Search**), choose **New** and create one rule with a suitable **Rule Type** per automation step. For lookup logic, maintain **Rule Properties** and the **Rule Matrix**.
3. **Set up the rule flow:** In the material type overview, open the desired line, call up the **Material Type Card** and, in the **Rule Flow** action group, choose the appropriate flow, e.g. **Property Rule Flow**. In the **rule flow**, chain the rules via the **Line Type** column.
4. **Create an item** and set the **Material Type**. The item is automatically set to **Blocked** as soon as the material type owns a rule flow.
5. **Unblock the item.** On unblocking, the rule flows run in a fixed order (Property → Material Filter → Routing → Production BOM) and build up the master data.

> Note: The actual "posting" of this module is the **unblocking** of the item. There is no separate posting or release document; the rule flow is the only action triggered by the user.

## Setup

The setup consists of a central setup page and the subsequent definition of the rules. It is the basis for the entire automation and is performed by the key user or administrator before first use.

### Rule Setup

**Process entry:** The administrator defines once per company how the module assigns new routing and production BOM numbers when a rule creates a routing or a production BOM. This setting later controls the rule types **Use Routing Operation** and **Use Prod. BOM Component**.

**Entry:** Open the **Rule Setup** page via **Search**. It is a company-wide single page; on first opening, the record is created automatically.

| Setup | Explanation |
|---|---|
| **Routing Nos From** | Determines where the number of a routing newly created by a rule comes from. When **No. Series** is selected, the new routing receives a sequential number from the number series; when **Item No.** is selected, the item number is used as the routing number, so that the item and routing carry the same number. |
| **Prod. BOM Nos From** | Determines where the number of a production BOM newly created by a rule comes from. When **No. Series** is selected, the number is assigned sequentially; when **Item No.** is selected, the production BOM carries the item number, which simplifies matching the item and BOM. |

**Values of the option field (identical for both fields):**

- **No. Series:** The number is drawn from a number series when created; the item and routing or production BOM have different numbers.
- **Item No.:** The number matches the item number; for every item, a routing or production BOM with the same name is created.

## Master data

The master data of this module are the **rules** themselves, their **Rule Matrix** and **Rule Properties**, as well as the assignment of the rules to **material types** via rule flows. In addition, rules can be assigned as **direct rules** directly on a record property.

### Defining rules

**Process entry:** The key user creates exactly one rule per automation step. The **Rule Type** determines the behavior and shows only the fields required for it on the card. Rules are later used in rule flows or assigned as a direct rule on a property.

**Entry:** Open the **Rules** list via **Search** and choose **New**; the list opens the **Rule** card. A rule cannot be renamed, and special signs such as `. ; # $` are not allowed in the **Code**.

#### General fields of the rule

| Field | Explanation |
|---|---|
| **Code** | Unique identifier of the rule. When set, the rule can be selected in rule flows and as a direct rule code; renaming it afterwards is not possible. |
| **Description** | Plain-text label. When set, it appears in lists and in the **Rule Flow Editor** as the node title and makes selecting the rule easier. |
| **Rule Type** | Determines the behavior of the rule and controls which field groups are visible and editable on the card. When you change the rule type, values that no longer fit are cleared automatically. The individual values are described below. |
| **Value Type** | Sets the data type of the result (**Boolean, Date, Date-Time, Decimal, Integer, Text, Time**). When the rule type or a selected property dictates the type, the value type is set automatically; for **Get Value** and **Get Constant** you choose it yourself. It controls which constant field and which return column of the rule matrix are used. |
| **Direct** | When enabled, the rule can be assigned directly on a record property (**Direct Rule Code**) and executed without a rule flow. Only allowed for the rule types **Set Property, Set Property Attribute, Set Value Filter** and **Set Value Group Filter**; for other rule types, setting it is prevented. |
| **Material Type Code in Matrix** | When enabled, the **Material Type Code** column is shown in the rule matrix, so that the same rule can return different values per material type. When toggling, the existing matrix is deleted after a confirmation prompt. |
| **Use Defaults** | When enabled (only for **Set Property**), the card shows the **Defaults** group; if the rule matrix finds no match, the default value stored there is returned instead of returning no result. |
| **Output Text** | Text for the rule types **Message, Confirm** and **Error**. When set, it is displayed to the user; a placeholder `%1` is replaced by the value of the assigned variable. If the text is missing, execution aborts with an error message. |

#### Values of the Rule Type

The **Rule Type** has an empty initial value and the following forms; each describes what happens when the rule is executed:

- **(blank):** Rule with no behavior – serves only as a placeholder until a rule type is chosen.
- **Get Property:** Reads the property value (**Property** via **Material Type Code** and **Property Code**) of the item and returns it as the result; typically used as input for comparisons or further rules.
- **Set Property:** Determines a value (from a variable, formula or rule matrix) and writes it into the record property of the item; can be controlled per property combination via **Matrix**.
- **Set Property Attribute:** Sets a **Property Attribute** (see below) of the record property, e.g. makes the property mandatory or invisible, instead of writing a value.
- **Get Value Filter / Set Value Filter:** Reads or writes the **value filter** of a record property; controls which values are permitted for the property.
- **Get Value Group Filter / Set Value Group Filter:** Reads or writes the **value group filter** of a record property.
- **Get Value:** Determines a value via a variable, formula or **Rule Matrix** and returns it without writing it.
- **Get Constant:** Returns a fixed constant value of the type chosen in the **Value Type**.
- **Formula:** Calculates an expression; property values are inserted into the **Formula** with `#Code#`, variables with `$Variable$`. If **Return Expression** is active, the text is returned, otherwise the calculation result as a decimal value.
- **Message / Confirm / Error:** Displays the **Output Text** to the user as a message, presents a Yes/No **Confirm** (result Yes/No) or aborts with an **Error** message.
- **Set Item Field:** Writes the determined value into a selectable field of the **Item** (via **Field Name**/**Field No.**).
- **Apply Item Template:** Applies an **Item Template** (via **Item Template Code** or a determined value) to the item.
- **Use Routing Operation:** Copies a routing operation from a source **Routing** into the item's routing; the target number follows the **Rule Setup**.
- **Set Routing Operation Field:** Writes the determined value into a field of a routing operation line.
- **Use Prod. BOM Component:** Copies a component line from a source **Production BOM** into the item's production BOM.
- **Set Prod. BOM Component Field:** Writes the determined value into a field of a production BOM component line.
- **Use Prod. Order Routing Operation:** Inserts a routing operation into the **Prod. Order Routing** when the production order is recalculated.
- **Set Prod. Order Routing Operation Field:** Writes the determined value into a field of a prod. order routing operation line.
- **Get Material Filter / Set Material Filter:** Reads or sets a **Material Filter** of the item; **Material Filter Type** distinguishes between a material type and a property filter.
- **Round:** Rounds a decimal value according to **Rounding Precision** and **Rounding Direction**.
- **Replace:** Replaces the **Search Value** with the **Replace Value** in the determined text.
- **Contains:** Checks whether the determined text contains the **Search Value** (result Yes/No); **Case Sensitivity** controls the accuracy.

#### Rule-type-dependent field groups

Depending on the **Rule Type**, the **Rule** card shows additional groups. The following table describes the fields then visible.

| Group / Field | Explanation |
|---|---|
| **Material Filter** – **Material Filter Type** | Visible for **Get/Set Material Filter**. When set to material type, the rule works with a material type filter and shows the **Constant**; for a property filter it shows **Property**. |
| **Property** – **Material Type Code**, **Property Code**, **Property Name**, **Use Property Values** | Visible for all property rule types. When **Property Code** is set, the data type from the property is adopted into the **Value Type**; **Property Name** and **Use Property Values** are reloaded from the property. |
| **Property Attribute** – **Property Attribute** | Visible for **Set Property Attribute**. Determines which attribute of the property is set; the value type is automatically set to Boolean. |
| **Constant** – **Text Constant, Decimal Constant, Integer Constant, Boolean Constant, Date Constant, Time Constant, Date-Time Constant** | Visible for **Get Constant** (and for a material filter with material type). Only the field matching the **Value Type** is editable; its content is returned as a fixed value. |
| **Defaults** – the same constant fields as **Default Text/Decimal/Integer** etc. | Visible for **Set Property** with **Use Defaults** active. If the rule matrix returns no match, the default value stored here is written. |
| **Formula** – **Formula**, **Return Expression** | Visible for **Formula**. When **Return Expression** is active, the rule returns the assembled text; otherwise the calculated decimal result. |
| **Output Text** – **Output Text** | Visible for **Message/Confirm/Error**; the displayed text with the optional placeholder `%1`. |
| **Item** / **Routing** / **Production BOM** (field variant) – **Field No.**, **Field Name** | Visible for the "Set … Field" rule types. Via AssistEdit you select the target field; only supported field types are allowed, otherwise "Field Type not allowed!" appears. |
| **Item Template** – **Item Template Code** | Visible for **Apply Item Template**. |
| **Routing** – **Routing No.**, **Routing Version Code**, **Routing Operation No.** | Visible for **Use Routing Operation**. When no matrix is maintained, **Routing Operation No.** is directly editable; with a matrix, the routing operation is determined per combination. |
| **Production BOM** – **Prod. BOM No.**, **Prod. BOM Version Code**, **Prod. BOM Line No.** | Visible for **Use Prod. BOM Component**; analogous to the routing with optional matrix control. |
| **Round** – **Rounding Precision**, **Rounding Direction** | Visible for **Round**. **Rounding Direction** can be **Nearest Value**, **Round up** or **Round down**. |
| **Replace** – **Search Value**, **Replace Value** | Visible for **Replace**. |
| **Contains** – **Search Value**, **Case Sensitivity** | Visible for **Contains**. |

**Values of the Rounding Direction:**

- **Nearest Value:** Rounds to the nearest value (up or down).
- **Round up:** Always rounds to the larger number.
- **Round down:** Always rounds to the smaller number.

**Values of the Property Attribute:**

- **(blank):** No attribute – the rule sets no attribute value.
- **Mandatory:** When set, the record property is marked as a required field.
- **Not Editable:** When set, the user can no longer change the property value.
- **Not Visible:** When set, the property is hidden during entry.
- **Zero is Value:** When set, the value 0 is treated as a valid value and not as "empty".

### Rule Properties

**Process entry:** As soon as a rule determines its result from a **Rule Matrix**, here you define which properties span the matrix at which **Position** and how the comparison is made. Without at least one rule property with a position, the matrix cannot be opened ("No Properties or Positions defined for Rule Matrix!").

**Entry:** On the **Rule** card, open the **Properties** action; the **Rule Properties** page is sorted by **Position**.

| Field | Explanation |
|---|---|
| **Property Code** | Selects the property that forms a column group of the matrix. When set, the **Data Type** is adopted from the property and – if no position has been assigned yet – the next free position is set. |
| **Property Name** | Displays the name of the selected property; serves as a check. |
| **Data Type** | Displays the data type of the property (Text, Integer, Decimal, Date). It controls which matrix column (Text/Integer/Decimal) is used and which filter method is permitted. |
| **Position** | Sets the order of the property in the matrix (1–10). If a position is already occupied, "Position … already used for Property Code …!" appears. |
| **Filter Method** | Determines how the property value is checked against the matrix values. For numbers and dates, the method must be the same in all positions, otherwise "Filter Method for Integer/Decimal and Date must be the same in all Positions!" appears. |
| **Additional Empty Search** | When enabled, in addition to the value search, a search with an empty value is performed, so that matrix rows without a concrete value also count as a match. |

**Values of the Filter Method:**

- **equal (=):** Matches matrix rows with an exactly equal value.
- **from (>=):** Matches rows whose limit value is less than or equal to the property value (lower bound).
- **to (<=):** Matches rows with an upper bound.
- **over (>):** Matches rows strictly above.
- **under (<):** Matches rows strictly below.
- **unequal (<>):** Matches rows with a differing value.
- **from/to:** Value range; the matrix additionally receives a second (secondary) column for the upper bound.

### Rule Matrix

**Process entry:** The **Rule Matrix** is the lookup table of a rule: for each combination of the positions defined in the **Rule Properties**, you store the return value. This way, the same rule returns different results depending on the property values (and optionally per **Material Type**).

**Entry:** On the **Rule** card, open the **Matrix** action. On exit, the system cleans up direct values of the rule that are no longer needed.

The columns are shown dynamically according to the rule properties:

| Field group | Explanation |
|---|---|
| **Line No.** | Sequential number of the matrix row. |
| **Material Type Code** | Only visible when **Material Type Code in Matrix** is active on the rule. When set, the row applies only to items of this material type. |
| **Text 1**–**Text 10** | Search columns for properties of data type Text; only the columns of the occupied positions are shown. |
| **Decimal 1**–**Decimal 10** and **Sec. Decimal 1**–**Sec. Decimal 10** | Search columns for decimal properties; the secondary column is used as the upper bound with the filter method **from/to**. |
| **Integer 1**–**Integer 10** and **Sec. Integer 1**–**Sec. Integer 10** | Search columns for integer properties; the second column again serves as the upper bound with **from/to**. |
| **Return Value Text/Decimal/Integer/Boolean/Date/Time/Date-Time** | Result column; the column matching the rule's **Value Type** is shown. Its value is returned when the row is matched across the positions. |

> Basic principle of evaluation: The system filters the matrix position by position according to the item's current property values. If a match remains at the end, its return value is used; if none remains and **Use Defaults** is active, the default value takes effect.

### Material Type and rule flows

**Process entry:** On the **Material Type Card**, you connect the previously defined rules into **rule flows**. There is a separate rule flow per area (Property, Material Filter, Routing, Production BOM, Prod. Order Routing), which is executed when an item of this material type is unblocked. The associated rule flow IDs are stored on the material type.

**Entry:** In the material type overview, open the desired line and call up the **Material Type Card**. The following actions are available in the **Rule Flow** action group; each opens (and, on first call, creates) the appropriate rule flow.

| Action | Explanation |
|---|---|
| **Property Rule Flow** | Opens the rule flow that determines and sets the item's **properties** on unblocking. |
| **Material Filter Rule Flow** | Opens the rule flow that builds up the item's **material filter** for the source material search. |
| **Routing Rule Flow** | Opens the rule flow that fills the item's **routing** with routing operations. |
| **Prod. BOM Rule Flow** | Opens the rule flow that fills the item's **production BOM** with components. |
| **Prod. Order Routing Rule Flow** | Opens the rule flow that builds up the **prod. order routing** when a production order is recalculated. |

**Basic fields of the Material Type Card (for navigation):**

| Field | Explanation |
|---|---|
| **Code** | Unique code of the material type; the rule flow is assigned via it. |
| **Description** | Plain-text name of the material type. |

**Important automation:** When a material type that owns one or more rule flows is set on an item, the item is automatically set to **Blocked**. This prevents an item with incomplete master data not yet built up by the rules from being used in documents. You can now calmly maintain the input data (e.g. property values) while the item is blocked. This behavior is described in the chapter **Automation in day-to-day operations**.

### Direct rules on record properties

**Process entry:** Not every automation needs a rule flow. For simple, immediately effective logic, you assign a rule marked as **Direct** directly on a record property. It is executed as soon as the user changes the **Value** of this property.

**Entry:** On the item or on the material type, open the **record properties** (property lines). There the app adds the **Direct Rule Code** column.

| Field | Explanation |
|---|---|
| **Direct Rule Code** | Accepts one or more direct rule codes (separated by semicolons). When set, each stored rule is executed when the property value changes. In the selection, only rules marked as **Direct** whose **Material Type Code** matches the line are offered; unsuitable rule types or a differing **Property Code** are rejected. |

For orientation, this line carries along the verified base fields of the record property: **Property Name**, **Value**, **value filter**, **value group filter** as well as the attributes **Mandatory**, **Not Editable**, **Not Visible** and **Zero is Value**. A direct rule can set exactly these values or attributes.

## Creating and editing rule flows

A **rule flow** is an ordered, indented program made up of rules, branches and variables. It is assigned per area on a material type (see **Material Type and rule flows**) and processed when the item is unblocked.

### Rule Flow (line view)

**Entry:** via one of the rule flow actions of the **Material Type Card**. The **Rule Flow** page shows the lines of the flow; the indentation represents the **If/Else/End** levels.

| Field | Explanation |
|---|---|
| **Flow** | Shows the readable text of the line (e.g. "If (…) then", "Rule …", "Message …"). Serves as a check of the flow and is not editable. |
| **Line Type** | Determines the type of the line. On change, the levels are recalculated and fields that no longer fit are cleared. The values are described below. |
| **Rule Code** | Selects the **rule** to be executed. When set, the variable is cleared and the **Value Type** is adopted from the rule. For **Message/Confirm/Error**, only rules of the corresponding rule type are available for selection. |
| **Variable** | Alternative to the rule code: refers to a **Rule Flow Variable** of the same flow. When set, the rule code is cleared. |
| **Compare Sign** | Only for **If (Compare)**: operator (=, <>, >, >=, <, <=) for comparing the left with the right side. |
| **Compare Rule Code** | Right side of a comparison when it comes from a rule. |
| **Compare Variable** | Right side of a comparison when it comes from a variable; excludes the compare rule code. |
| **Value Type** | Shows the value type of the line (from a rule or variable) and controls the data type of the comparison. |

**Values of the Line Type:**

- **(blank):** Line not yet determined.
- **Rule:** Executes the rule chosen under **Rule Code**.
- **If (True):** Beginning of a block that is executed only if the rule/variable Boolean = true.
- **If (False):** Beginning of a block that is executed only if the result is "false".
- **If (Compare):** Beginning of a block that is executed if the comparison (left side **Compare Sign** right side) matches.
- **Else:** Inverts the condition of the associated If block.
- **End:** Closes an If/Else block; processing returns to the previous level.
- **Message:** Displays the rule's output text to the user as a note.
- **Confirm:** Presents a Yes/No prompt; the result can control a branch.
- **Error:** Aborts the flow with an error message.
- **Set Variable:** Writes the rule result into the assigned **Variable**, so that later lines can access it.

### Rule Flow Editor

**Process entry:** The **Rule Flow Editor** is the graphical alternative to the line view: you drag rule and branch nodes and connect them into a flow. It is suitable for modeling complex flows clearly.

**Entry:** In the **Rule Flow**, open the **Flow Editor** action. After saving, the line view appears with the prompt **"Is the flow correct?"**; if you confirm with Ok, the flow is adopted, otherwise the previous state is restored.

### Rule Flow Variables

**Process entry:** **Rule Flow Variables** hold intermediate results of a flow or supply context values (e.g. the work date). They are used in lines as the left or right comparison side or as the target of **Set Variable**.

**Entry:** In the **Rule Flow**, open the **Variables** action.

| Field | Explanation |
|---|---|
| **Variable** | Unique name of the variable within the flow. If a variable in use is deleted, "The Rule Flow Variable is in use." appears. |
| **Variable Type** | Determines where the variable value comes from (see values below). On change, the appropriate value fields become editable. |
| **Property Code** | Only for variable type **Item Property**: the property whose value the variable supplies. |
| **Value Type** | Data type of the variable (**Boolean, Date, Date-Time, Decimal, Integer, Text, Time**); controls which value field is editable. |
| **Value Text / Value Decimal / Value Integer / Value Boolean / Value Date / Value Time / Value Date-Time** | Fixed start value for variable type **Normal**; only the field matching the **Value Type** is editable. |

**Values of the Variable Type:**

- **Normal:** Free, fixed value entered in the appropriate value field.
- **Companyname:** Supplies the name of the current company.
- **Workdate:** Supplies the work date of Business Central.
- **Current Date:** Supplies today's date.
- **Current Time:** Supplies the current time.
- **Current Date-Time:** Supplies the current timestamp.
- **Item Material Type:** Supplies the material type of the processed item.
- **Item Property:** Supplies the value of the property chosen under **Property Code**.
- **Item Field - Base Item:** Supplies a field value of the base item.

## Automation in day-to-day operations

This chapter describes when and how the configured rule flows take effect automatically in day-to-day operations. All triggers are standard operations on the item or on the production order; there is no separate document.

### Setting the material type blocks the item

If you set the **Material Type** on an item and this material type owns at least one rule flow, the item is automatically set to **Blocked**. This prevents an item with incomplete master data not yet built up by the rules from being used in documents. You can now calmly maintain the input data (e.g. property values) while the item is blocked.

### Unblocking the item runs the rule flows

On **unblocking** the item (the **Blocked** indicator is removed), the material type's rule flows run in a fixed order:

1. **Property Rule Flow** – determines and sets the property values.
2. **Material Filter Rule Flow** – builds up the material filter.
3. **Routing Rule Flow** – fills the routing.
4. **Prod. BOM Rule Flow** – fills the production BOM.

Afterwards, the item is available with fully built master data.

### Direct rule on value change

If the user changes the **Value** on a **record property** and a **Direct Rule Code** is stored, the rule is executed immediately – without unblocking and without a rule flow. This way, dependent property values can be updated instantly.

### Prod. order routing on the production order

When the routing of a production order is recalculated – as well as when a production order is created from a sales line – the material type's **Prod. Order Routing Rule Flow** is executed and builds up the production order's routing.

## Permissions

For operation, the module provides the **Rule General** permission set. It determines the permissions for the objects of the rule-based data management and specifies which actions users with this set can perform on rules, rule matrices, rule properties and rule flows. Assign the permission set to the roles that maintain rules or unblock items.

## FAQ and troubleshooting

### Why is my item automatically blocked when I set the material type?

Because the chosen **Material Type** owns at least one rule flow. The system blocks the item so that it is not used with incomplete master data; the rules build up the data only on **unblocking**.

### How do I start the automation – where is the "Post" button?

There is no posting or release document. The automation is triggered by **unblocking** the item. On unblocking, the rule flows run automatically.

### In which order do the rule flows run?

On unblocking, the **Property Rule Flow**, then the **Material Filter Rule Flow**, then the **Routing Rule Flow** and finally the **Prod. BOM Rule Flow** are executed. The **Prod. Order Routing Rule Flow** runs separately when the production order is calculated.

### Why can't I delete a rule?

Because it is still in use. If the rule is included in a **rule flow line** (as **Rule Code** or **Compare Rule Code**) or as the **Direct Rule Code** of a property, the system reports "Rule … is used. Delete not possible!" or "… is used as direct Rule!". Remove the usages first.

### Why can't I rename a rule's code or use special signs?

Renaming is blocked ("Rename Code is not allowed!") so that existing references remain valid. Special signs such as `. ; # $` are not allowed in the **Code**, because they would serve as control characters in formulas and filters.

### Why can't I open the matrix?

The **Rule Matrix** requires at least one **Rule Property** with a **Position**. If it is missing, "No Properties or Positions defined for Rule Matrix!" appears. Maintain the rule properties first.

### Why does the system report "Filter Method … must be the same in all Positions"?

For properties of data type **Integer**, **Decimal** or **Date**, the same **Filter Method** must be used across all positions so that the matrix evaluates unambiguously. Set all numeric positions to the same method.

### Why does a rule return no value even though the matrix is maintained?

Presumably no matrix row matches the item's current property values. Enable **Use Defaults** on the rule and store a default value, or supplement with **Additional Empty Search** so that rows without a concrete value are also matched.

### When do I use a direct rule instead of a rule flow?

Use a rule marked as **Direct** on the **record property** when an automation should take effect immediately on every **Value** change, without unblocking the item. For multi-stage, branched logic, use a **rule flow**.

### Why can't I delete a property?

Because it is used in a rule or rule property. The system reports "Property … is used in Rule …!" when the property is included in a rule, a rule property, as a **Direct Rule Code** or in a rule flow line of the material type. Remove these usages first.

## Typical use cases

### A new item is built automatically via material type

- **Trigger:** Production engineering receives the internal request to create a new item for a known product group (material type) whose properties, routing and BOM should follow the standard of that group.
- **Entry in BC:** Open the item overview and create an item via **New**. In the item, set the **Material Type**. If the material type owns rule flows, the item is immediately set to **Blocked**.
- **Core flow:** Maintain the necessary input values on the item's **record properties** (prerequisite: the rules and rule flows of the material type are configured as described in the chapter **Master data**). Then remove the **Blocked** indicator (**unblock**). Now the **Property Rule Flow**, **Material Filter Rule Flow**, **Routing Rule Flow** and **Prod. BOM Rule Flow** run one after another.
- **Completion:** The item is unblocked and carries the properties set by the rules as well as – if configured – an automatically filled routing and a production BOM. It can now be used in documents.

### Changing a property value triggers a direct rule

- **Trigger:** A user adjusts a property value on an existing item (e.g. a dimension) on which further properties depend.
- **Entry in BC:** On the item, open the **record properties**. In the line of the relevant property, a **Direct Rule Code** is stored (prerequisite: a rule marked as **Direct** was assigned as described in the chapter **Direct rules on record properties**).
- **Core flow:** Change the **Value** of the property. Immediately after entry, the system executes the stored rule(s) – e.g. **Set Property**, **Formula** or **Set Value Filter** – and updates the dependent properties.
- **Completion:** The derived property values or attributes are set without the item having to be blocked and unblocked again.
