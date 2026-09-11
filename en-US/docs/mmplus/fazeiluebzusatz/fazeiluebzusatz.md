---
title: Anwenderhandbuch m+m Production Order Overview with Ext. Prod. Information
---

# User Guide m+m Production Order Overview with Ext. Prod. Information

## Introduction

The app **m+m Production Order Overview with Ext. Prod. Information** extends your company's
production order line overview with an additional FactBox showing the
**Ext. Prod. Properties**. When you select a production order line in the
**Prod. Order Line List**, the app displays the **Ext. Prod. Properties** FactBox on the right
and shows there the properties and their values belonging to the selected line.

The app adds **no** columns, actions, reports, or setup pages of its own to the existing list.
Its only visible contribution is this FactBox. The displayed properties themselves are not
maintained in this app; they originate from the extended production information and material
properties that were previously stored on the work center groups and routings and carried over
into the production order through the routing.

**Target audience:** Primarily the operational users in production control and work scheduling who
work with production orders every day and want to see the associated technical properties
(target and actual values) immediately when viewing an order line. Secondarily, it concerns
administrators who set up the underlying properties in the upstream modules.

**Brief process overview:**

1. An administrator stores the extended production properties on work center groups and
   routings (in the upstream modules; see the section *Where the displayed properties come
   from*).
2. When a production order is created or calculated, this information is carried over into the
   routing of the production order.
3. The user opens the **Prod. Order Line List**, selects a line, and reads the values in the
   **Ext. Prod. Properties** FactBox.

## Quick Start for Users

The fastest way to the extended production properties of an order line:

1. Open the **Prod. Order Line List** page via **Tell me**.
2. Select the desired production order line in the list (lines can be identified by the columns
   **Status**, **Prod. Order No.**, and **Item No.**).
3. Read the properties belonging to the line on the right in the **Ext. Prod. Properties**
   FactBox. For each selected line, the FactBox automatically shows the matching values; no
   separate action is required.
4. If needed, compare the specified **Standard Value** with the actually captured **Value** or
   **Actual Value** of the property.

Because the app contains no posting, release, or completion function, the quick start ends with
reading the values. There are no further mandatory steps in this app.

## Ext. Prod. Properties – the FactBox in Detail

The **Ext. Prod. Properties** FactBox is the actual scope of functionality of this app. It is a
pure display FactBox: the app binds it to the currently selected production order line and
automatically filters the associated properties by production order status, production order
number, and line number. You do not need to enter anything.

The following table describes all fields that the FactBox lists per property line.

| Field | Explanation |
|------|-------------|
| **Operation No.** | If the property is assigned to a specific operation of the routing, then you see its number here; this lets you recognize at which point in production the property applies. For properties not tied to an operation, the field remains empty. |
| **Description** | If a description text is stored, then this field shows the plain text for the property or the operation; the user does not have to derive the meaning from the code. |
| **Property Code** | The unique code of the property. When you read a line, then this code identifies which technical characteristic it is (e.g. a dimension or material specification). |
| **Standard Value** | If a default value from the master data was carried over for the property, then it is shown here; it serves as a reference against which you check the actual value. |
| **Value** | If a concrete value of the property was determined for this order line, then it is shown here. If the **Value** deviates from the **Standard Value**, then a different value was deliberately set for this order. |
| **Actual Value** | If a value actually achieved during production was captured, then you see it here; this lets you compare target (Standard Value/Value) and actual directly. The field is only shown for the source types intended for this (e.g. capacity ledger entries). |
| **Property Value Name** | If the property comes from a value list, then this field shows the descriptive designation of the selected value instead of a plain code. |
| **Value Permitted From** | If a lower limit is defined for a numeric property, then it is shown here; you immediately recognize from which value the specification is valid. |
| **Value Permitted To** | If an upper limit is defined, then it is shown here; together with *Value Permitted From*, this yields the permitted value range of the property. |
| **Unit** | If the property value has a unit of measure, then it is displayed here; this makes the numeric value unambiguously interpretable. |
| **Calculation Formula** | If the value of the property is derived from a formula, then the formula is stored here; you can see that the value does not arise manually but by calculation. |
| **Display Order** | Determines the sorting of the properties in the FactBox; if a value is assigned, then the lines appear in this order so that important properties are at the top. |
| **Data Type** | Defines how the value of the property is to be read and checked. The possible values are explained below for each option. |

**Values of the "Data Type" field (option field):**

- **Text:** The value is kept as free text; no number or date check takes place.
- **Integer:** The value is a whole number; when captured, a valid integer must be entered,
  otherwise the input is rejected.
- **Decimal:** The value is a decimal number; only valid decimal values are accepted, which makes
  range limits (*Value Permitted From/To*) evaluable.
- **Date:** The value is a date; it is interpreted and checked as a date.

**Visibility logic (what you see and why):** The FactBox toggles individual areas depending on
the source of the selected line:

- For a production order line, the properties are shown with their structure (e.g. operation
  reference).
- For an operation-related source, only lines with a filled **Property Code** are shown, so that
  the FactBox is not overloaded with empty characteristics.
- For sources with actual capture (e.g. capacity ledger entries), the **Actual Value**
  additionally becomes visible.

This control happens automatically; you do not have to set the visibility yourself.

## Where the Displayed Properties Come From (Prerequisite)

For the FactBox to display any values at all, the extended production properties must have been
maintained beforehand. This maintenance does **not** take place in this app, but in the upstream
modules for extended production information and material properties. It is important for the user
to understand how the data finds its way into the FactBox:

1. **First,** an administrator stores the properties and their default values on the work center
   groups or on the routings. If a **Standard Value** is set there, then it is later carried over
   as a default into the production order.
2. **Then,** Business Central carries over these specifications into the routing of the production
   order when a production order is created or calculated. When the production order is calculated,
   then the line- and operation-related properties that the FactBox later filters are created.
3. **Finally,** the user reads the carried-over values in the **Prod. Order Line List** through the
   **Ext. Prod. Properties** FactBox.

If the FactBox remains empty for a line, then no extended production properties were maintained for
the associated item or operation, or they have not yet been carried over into the production order.
The fix takes place in the upstream modules, not in this app.

## The Host List "Prod. Order Line List" at a Glance

The FactBox appears on the **Prod. Order Line List** page. This list is part of the upstream module
for the production order line overview; the present app does not change its columns but merely adds
the FactBox. For orientation, the most important columns you need to find and classify a line are
described here.

| Field | Explanation |
|------|-------------|
| **Status** | Shows the processing state of the production order. If you are looking for open orders, then filter via this column (e.g. on *Released*). |
| **Prod. Order No.** | The number of the production order; it establishes the reference between line and order and is part of the link to the FactBox. |
| **Item No.** | The item to be produced on the line; using this column you recognize which product the displayed properties concern. |
| **Variant Code** | If the item is kept in variants, then this code narrows down the specific variant. |
| **Description** | Plain-text designation of the item; makes it easier to find the right line without knowing the number. |
| **Description 2** | Supplementary second designation, if maintained. |
| **Location Code** | If a location is assigned, then the column shows where production or put-away takes place. |
| **Quantity** | The planned production quantity of the line; the reference quantity for evaluating the properties. |
| **Remaining Quantity** | If not the entire quantity has been completed yet, then you see the remaining quantity here. |
| **Routing No.** | The routing of the line; it is the source of the operation-related properties that the FactBox shows. |
| **Production BOM No.** | The production BOM assigned to the line. |
| **Unit Cost** | The unit cost of the line as a business reference figure. |

Further standard columns of the base module (including costs in reporting currency, base
quantities, planning flexibility, overhead, dimensions, and start and end dates) are also available
but are not explained individually here, since they belong to the standard scope of the production
order line and are not changed by this app.

**Linked areas of the same list:** Below the line list, the page shows the associated areas
**Assigned Prod. Order Component** and **Sales Lines**; on the right, next to the new
**Ext. Prod. Properties** FactBox, there are also the standard FactBoxes of the base module for
operations and material components. These areas belong to the base module and serve the application
as additional context when reading the properties.

## Permissions

The app ships its own permission set **All permissions**. It is assignable and determines the
permissions for the objects provided by this app. Since the app has no data tables of its own apart
from the FactBox, the set essentially comprises the execution right on the internal app object.

To visibly display the FactBox contents, users additionally need the read permissions of the
upstream modules (extended production information and material properties), since the displayed data
originates from their tables. Assign the permission set to all users who work with the
**Prod. Order Line List** and are to view the extended production properties.

## Typical Use Cases

The following scenarios show how the FactBox is used in day-to-day work. Both procedures are pure
read/check operations, since the app contains no posting or change functions.

### Use Case 1: Checking a Production Order Before Processing

1. **Trigger:** An employee in production control receives a released production order for review,
   by phone or via an internal message.
2. **Entry in BC:** They open the **Prod. Order Line List** via **Tell me** and select the relevant
   order line by **Prod. Order No.** and **Item No.**
3. **Core procedure:** The **Ext. Prod. Properties** FactBox appears automatically on the right. For
   each property, the employee checks the **Property Code**, the **Standard Value**, and the value
   actually set, **Value**, together with the **Unit**. If the **Value** deviates from the
   **Standard Value**, they clarify the cause before production starts.
4. **Completion:** The process ends with the visual check; no further steps are required in this
   app.

### Use Case 2: Target/Actual Comparison of a Property

1. **Trigger:** From production comes the query whether an achieved measured value is within the
   specification.
2. **Entry in BC:** The user opens the **Prod. Order Line List** and selects the matching line.
3. **Core procedure:** In the **Ext. Prod. Properties** FactBox, they read the **Standard Value** or
   **Value** (target) and the **Actual Value** for the relevant property and compare both against
   **Value Permitted From** and **Value Permitted To**. Using **Data Type** and **Unit**, they
   classify the number correctly.
4. **Completion:** They report the result of the comparison back; capturing the actual value takes
   place in the module that keeps the actual values, not in this app.

## FAQ and Troubleshooting

### 1. Why do I suddenly see an additional FactBox in the Prod. Order Line List?
Because this app attaches the **Ext. Prod. Properties** FactBox to the list. It appears to the right
of the standard FactBoxes and shows the properties of the respectively selected order line.

### 2. How is the FactBox related to the selected line?
The app links the FactBox firmly to the production order status, **Prod. Order No.**, and line
number of the selected line. When you select a different line, then the FactBox updates
automatically.

### 3. Why does the FactBox remain empty for a line?
Because no extended production properties were maintained for the associated item or operation, or
they have not yet been carried over into the production order. Maintenance takes place in the
upstream modules on work center groups and routings.

### 4. Can I change values in the FactBox?
In this app the FactBox is designed as a display. You make changes to properties and values where
the properties are maintained (upstream modules), not in the **Prod. Order Line List**.

### 5. What does the difference between Standard Value, Value, and Actual Value mean?
The **Standard Value** is the default from the master data, the **Value** is the target value
determined for this order, and the **Actual Value** is the value actually achieved. The comparison
shows whether an order deviates from the specification.

### 6. Why is the Actual Value not shown on every line?
Because the **Actual Value** is only made visible for source types with actual capture (e.g.
capacity ledger entries). For pure planning lines, no actual capture is intended, so the field
remains hidden.

### 7. What does the Data Type field tell me?
It defines how the value is to be read: **Text** as free text, **Integer** as a whole number,
**Decimal** as a decimal number, and **Date** as a date. For numeric data types, the limits
*Value Permitted From/To* are evaluable.

### 8. What are "Value Permitted From" and "Value Permitted To" for?
They specify the permitted value range of a numeric property. If an **Actual Value** lies outside
these limits, then this is an indication of a deviation that you should check.

### 9. In what order are the properties displayed?
By the **Display Order** of the property. This way, functionally important characteristics are at
the top and visible without scrolling.

### 10. Which permissions do I need to see the FactBox?
You need the permission set of this app as well as the read permissions of the upstream modules from
whose tables the displayed properties originate. Without these read rights, the FactBox remains
empty even though data is present.
