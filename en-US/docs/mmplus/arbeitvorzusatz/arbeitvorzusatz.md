---
title: Anwenderhandbuch m+m Prod. Order Job Overview with Ext. Prod. Information
---

# User Guide m+m Prod. Order Job Overview with Ext. Prod. Information

## Introduction

The app **m+m Prod. Order Job Overview with Ext. Prod. Information** extends the **Prod. Order Job Overview** in Microsoft Dynamics 365 Business Central with an additional factbox labeled **Ext. Prod. Properties**. This factbox displays the extended production properties stored for the currently selected operation – for example property code, standard value, actual value, permitted value range, unit of measure, calculation formula, and data type.

The practical benefit: the user sees the production properties relevant to an operation directly next to the job line and no longer has to switch between the overview and the property pages of the work center group. The factbox automatically follows the selected line.

**Target audience.** The primary audience is **operational users in production control** – workers, shift supervisors, and production controllers who process the pending operations of a work center group in the Prod. Order Job Overview and need the target values per operation. Production planners who maintain the properties beforehand at the work center group or in the routing benefit secondarily.

**Brief process overview.** A production planner stores the extended production properties at the work center group or in the routing (this is done in the underlying m+m modules and is a prerequisite, see the section **Prerequisites**). The operational user then opens the **Prod. Order Job Overview**, selects their **work center group**, and reads the associated values for each job line from the **Ext. Prod. Properties** factbox.

This app itself adds no setup pages, no master data cards, no documents, no postings, and no reports. It provides only the factbox described above in the Prod. Order Job Overview and links it to the matching operation.

## Quick Start for Users

The fastest route to the extended production properties of an operation:

1. Use **Search** to open the **Prod. Order Job Overview**. The Prod. Order Job Overview is a central overview page and is opened directly through Search; there is no upstream master data record from which it would be opened.
2. In the filter area, enter the desired work center group under **Work Center No.**. The overview then displays the operations of this work center group; the name appears read-only under **Work Center Name**.
3. Narrow the list further if needed: **Machine Center No.** (a single machine center within the group – optional), **Prod. Order No.** (a single production order – optional), as well as **Date**, **Sort By**, **Hide Finished**, and **Hide Open**.
4. In the line list, select the desired **operation**.
5. On the right, in the **Ext. Prod. Properties** factbox, read the properties stored for the selected operation. When you change the selected line, the factbox refreshes automatically.

If no properties are maintained for an operation, the factbox remains empty – in that case, maintenance according to the section **Prerequisites** is required first.

## Prerequisites

For the **Ext. Prod. Properties** factbox to display values, two conditions must be met:

- **App installation.** This app must be installed. A separate setup within the app is not required: after installation, the factbox appears automatically in the Prod. Order Job Overview. There is no setup page and no switches to activate in this app.
- **Maintained production properties.** The values displayed come from the extended production properties that were previously stored at the **work center group** or in the **routing**. This maintenance is done in the underlying m+m modules (Material Properties and Ext. Production Information) and is therefore the actual business prerequisite. If a **Property Code** with values is maintained for an operation, the factbox displays that property; if no property code is stored, the line does not appear in the factbox.

So if the factbox remains empty for an operation even though properties are expected there, first check whether the extended production properties are maintained at the associated work center group or in the routing.

## The Prod. Order Job Overview as Entry Point

The Prod. Order Job Overview is the working surface on which this app builds. It shows the operations of a work center group as a list. The app does not change this list itself – it merely adds another factbox on the right. In order for you to select the correct line and for the factbox to display the matching properties, the following filters of the Prod. Order Job Overview are especially relevant.

### How the factbox follows the selected line

The **Ext. Prod. Properties** factbox is tied to the currently selected job line. Internally, the app links the factbox to the matching extended production properties via the **Prod. Order Status**, the **Prod. Order No.**, the **operation**, and the production order line of the selected line. For you as a user, this means: you control the display solely through line selection – there is no need to open or reload separately.

The following filters of the Prod. Order Job Overview determine which lines are displayed at all, and thus for which operations you can view the factbox. They belong to the base overview; this app does not change them, they are described here for orientation.

| Filter field | Explanation |
|---|---|
| **Work Center No.** | When set, the operations are limited to the selected work center group; the overview then loads its lines. This is the top-level entry point – without a work center group, the list stays empty. |
| **Work Center Name** | Taken read-only from the selected work center group; serves only to confirm that the correct group is set. |
| **Machine Center No.** | When set, the lines are additionally limited to a single machine center within the group. Optional – selection at the work center group level is sufficient if you want to see all machine centers of the group. |
| **Machine Center Name** | Taken read-only from the selected machine center; serves as a check. |
| **Prod. Order No.** | When set, only the operations of the specified (released) production order are displayed. Optional; without a value, all matching production orders appear. |
| **Date** | When set, the overview filters to the specified date; this lets you, for example, show the relevant operations for a given day. |
| **Sort By** | Determines the order in which the operations are displayed; changes the order of the list, not its content. |
| **Hide Finished** | When enabled, already finished operations are hidden, so you can concentrate on work that is still open. |
| **Hide Open** | When enabled, open operations are hidden; useful when you specifically want to look up operations that are already completed. |

## The "Ext. Prod. Properties" Factbox

This is the only surface this app adds, and at the same time its core. The factbox appears at the right edge of the Prod. Order Job Overview. For each selected operation, it shows the associated extended production properties as a list. The fields are display fields – you read the target values and the achieved actual value in them; the values are maintained at the work center group or in the routing (see **Prerequisites**).

The factbox contains the following columns:

| Field | Explanation |
|---|---|
| **Operation No.** | Shows the operation to which the property line belongs. When you select a line in the Prod. Order Job Overview, you see here which operation the properties listed below are assigned to – this lets you clearly relate the values to a work step. |
| **Description** | Shows the plain text for the property line or the operation. This lets you recognize what the property is about without resorting to codes. |
| **Property Code** | Shows the code of the production property. When a property code is set, the line counts as an actually maintained property; lines without a property code are not displayed in this factbox, so you see only relevant properties. |
| **Standard Value** | Shows the specified target value of the property. You orient yourself by this value when performing the operation; if the actual value deviates from it, this is an indication of a deviation from the specification. |
| **Value** | Shows the value of the property valid for this specific production run. If this value deviates from the **Standard Value**, it is the order-specific specification that takes precedence over the general standard. |
| **Actual Value** | Shows the value of the property actually recorded. When an actual value is present, you can compare it directly against **Standard Value** or **Value** and thereby assess the production status of the operation. |
| **Property Value Name** | Shows the plain name for the set value when the property works with a value list. This lets you read a coded value as an understandable label. |
| **Value Permitted From** | Shows the lower limit of the permitted value range. If the actual value falls below this limit, the property is outside the specification – a direct check indicator at the workstation. |
| **Value Permitted To** | Shows the upper limit of the permitted value range. If the actual value exceeds this limit, the property is outside the specification. |
| **Unit of Measure** | Shows the unit of measure of the property (e.g. for length, weight, or temperature). This lets you interpret Standard Value, Value, and Actual Value correctly and avoid confusing the order of magnitude. |
| **Calculation Formula** | Shows the stored formula used to calculate a numeric value of the property. When a formula is set, the value results from a calculation and is not entered freely; this explains why a value arises automatically. |
| **Display Order** | Determines the order in which the properties appear in the factbox. When the order is maintained, the properties most important for the operation are at the top, so you see the essentials first. |
| **Data Type** | Indicates what kind of value the property carries. The data type determines how **Value**, **Standard Value**, and **Actual Value** are to be read and whether a permitted value range is meaningful. The possible options are: |

The possible options of the **Data Type** field:

- **Text:** The property carries a free text value. A permitted value range (from/to) and a calculation formula do not apply here; you read the value as a character string.
- **Decimal:** The property carries a decimal value. A permitted value range **Value Permitted From** / **Value Permitted To** can be evaluated, and a **Calculation Formula** can be stored.
- **Integer:** The property carries an integer value. As with **Decimal**, the value range and calculation formula can be evaluated, but without decimal places.
- **Date:** The property carries a date value. The value is to be read as a date; a numeric from/to range with a calculation formula is not intended for this.

## Permissions

The app ships with the permission set **MuM PJAP Perm**. It is assignable and determines the permissions for executing the app logic that links the factbox to the matching operation. Assign this permission set to the users who work with the extended production properties in the Prod. Order Job Overview. The permission set specifies that the associated app function may be executed; the visibility of the individual property values themselves is governed by the permissions of the underlying production and property data.

## FAQ and Troubleshooting

### 1. Why don't I see an "Ext. Prod. Properties" factbox in the Prod. Order Job Overview?
Check whether the app is installed and whether the factbox area on the right is shown. After installation, the factbox is displayed automatically as an additional factbox in the Prod. Order Job Overview; if the factbox area is collapsed, show it again via personalization.

### 2. Why does the factbox stay empty even though I have selected a line?
No extended production properties with a **Property Code** are maintained for the selected operation. The factbox displays only lines with a property code set. Maintain the properties at the associated work center group or in the routing (see **Prerequisites**).

### 3. Do I have to set anything up in this app before I can use it?
No. This app has no setup page and no switches to set. After installation, the factbox is available immediately. The business preparation consists solely of maintaining the production properties at the work center group or routing.

### 4. How do I ensure the factbox matches the correct operation?
In the Prod. Order Job Overview, select the desired line. The factbox automatically ties itself to the **Prod. Order Status**, **Prod. Order No.**, **operation**, and production order line of the selected line and shows exactly the matching properties. Manual reloading is not necessary.

### 5. Why does the actual value deviate from the standard value?
The **Standard Value** is the general specification, the **Value** is the order-specific specification, and the **Actual Value** is the value actually recorded. A deviation between **Actual Value** and **Standard Value**/**Value** is an indication that production deviates from the specification – use this comparison to assess the operation.

### 6. What does an entry under "Value Permitted From" and "Value Permitted To" mean?
These fields specify the permitted value range of the property. If the **Actual Value** is outside this range, the specification is not met. The range is evaluable above all for the data types **Decimal** and **Integer**.

### 7. Why can't I enter a value directly – it appears to be calculated?
A **Calculation Formula** is stored for the property. In this case, the value results from a calculation and is not recorded freely. The formula is part of the property definition and is maintained at the work center group or in the routing.

### 8. In what order do the properties appear in the factbox?
The order follows the **Display Order** field of the respective property. If the display order is maintained, the most important properties are at the top; otherwise they appear in the default sort order.

### 9. How do I recognize how a value is to be read – as a number, text, or date?
By the **Data Type** field: **Text** indicates a free text value, **Decimal** and **Integer** indicate numeric values (with or without decimal places), and **Date** indicates a date value. The data type also determines whether a permitted value range and a calculation formula are meaningful.

### 10. Can I change the production properties in the factbox?
The factbox in the Prod. Order Job Overview serves to display the target values and the actual value for the operation. Maintenance of the properties (standard values, value ranges, formulas) is done at the work center group or in the routing in the underlying modules, not in this factbox.

## Typical Use Cases

The following examples show how the factbox helps in day-to-day work. All the steps described relate exclusively to the Prod. Order Job Overview and the **Ext. Prod. Properties** factbox.

### Use Case 1: Checking target values at an operation

**Trigger.** A worker asks the shift supervisor which specifications apply to the next operation at their work center group.

**Entry in BC.** The shift supervisor uses **Search** to open the **Prod. Order Job Overview** and enters the relevant work center group under **Work Center No.**. Optionally, they narrow further via **Machine Center No.** or **Prod. Order No.**.

**Core procedure.** In the line list, they select the operation in question. On the right, in the **Ext. Prod. Properties** factbox, they read the properties for this operation: **Property Code**, **Standard Value** or **Value** as the specification, **Unit of Measure** for correctly interpreting the order of magnitude, as well as **Value Permitted From** and **Value Permitted To** as the permitted range. From the **Data Type**, they recognize whether it is a numeric, a text, or a date value.

**Conclusion.** The shift supervisor passes the target values they have read to the worker. A separate posting or printing step is not required; the factbox serves as information.

### Use Case 2: Comparing standard and actual value before releasing an operation

**Trigger.** Before the internal release of an operation, it should be checked whether the recorded values are within the specifications.

**Entry in BC.** The production controller uses **Search** to open the **Prod. Order Job Overview**, sets the **Work Center No.**, and uses **Hide Finished** to hide already completed operations in order to concentrate on those still open.

**Core procedure.** They select the operation to be checked. In the **Ext. Prod. Properties** factbox, they compare, line by line, the **Actual Value** with **Standard Value** or **Value** and check whether the actual value lies within **Value Permitted From** and **Value Permitted To**. When they change the selected line, the factbox refreshes automatically, so they can check several operations one after another.

**Conclusion.** If all actual values are within the permitted range, the production controller releases the operation in the usual workflow. In case of deviations, they arrange for clarification at the work center group or in the routing, where the properties are maintained. Here, too, there is no separate posting step in this app – the benefit lies in the immediate target/actual comparison at the job line.
