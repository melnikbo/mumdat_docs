---
title: Anwenderhandbuch m+m Production Order Assistant with Ext. Prod. Information
---

# User Guide m+m Production Order Assistant with Ext. Prod. Information

## Introduction

This guide describes the functions of the app **m+m Production Order Assistant with Ext. Prod. Information** in Microsoft Dynamics 365 Business Central. The app is a lightweight extension that makes the **extended production properties** of a production order directly visible and editable within the **Production Order Assistant**.

The app does not bring its own setup or master data pages. It builds on three m+m base modules and connects their data with the Production Order Assistant:

- **m+m Production Order Assistant** – provides the **Production Order Assistant** page with the **Routing** and components subpages.
- **m+m Ext. Production Information** – supplies the **Actual Value** and the **Mandatory Actual Value** per property (operation or capacity context).
- **m+m Material Properties** – supplies the actual data structure of the properties (property code, standard value, value, calculation formula, etc.).

**What the app does:** When the user selects an operation in the **Routing** in the Production Order Assistant, the **Ext. Prod. Properties** FactBox on the right shows the properties stored for that operation. Using the **Edit** action, the user opens a page in which the values of the operation can be entered and changed. In addition, the app ensures in the background that, when routing lines are copied from a simulated production order, the extended production properties are copied along with them.

**Target audience:** The primary audience are **operational users in production control and work scheduling** who prepare a production order via the Production Order Assistant and, per operation, check the technical properties or capture the **Actual Value**. Planners and administrators are only indirectly affected: the underlying properties are maintained in the base modules (Material Properties or Ext. Production Information); this app adds no configuration of its own there.

**Brief process overview:** Open the production order in the Production Order Assistant → mark the operation in the **Routing** → read the **Ext. Prod. Properties** FactBox → adjust the values via **Edit** if needed → close the page; the FactBox refreshes.

## Quick start for users

The fastest path to the extended production properties of an operation:

1. Open the **Production Order Assistant** for the desired production order (it is called from the base module m+m Production Order Assistant, usually from the sales line).
2. In the **Routing** subpage, mark the row of the operation whose properties you want to see.
3. On the right, in the **Ext. Prod. Properties** FactBox, read the properties of this operation (property code, standard value, **Value**, and where applicable **Actual Value**).
4. If you want to capture or change a value, choose the **Edit** action in the FactBox. The **Ext. Prod. Properties** page opens.
5. In the page, enter the desired **Value** or **Actual Value** and close the page. The FactBox then displays the changed values, refreshed.

> Note: This app contains no setup. Which properties an operation actually has is determined by the stored routing and the property definitions of the base modules. If no properties are defined for an operation, the FactBox remains empty.

## The "Ext. Prod. Properties" FactBox in the Production Order Assistant

The FactBox is the central display area of this app. It is automatically inserted by the app as the first FactBox in the Production Order Assistant and is linked to the **Routing** subpage: it always shows the properties of the operation **currently marked in the routing**. When the user switches rows in the routing, the content of the FactBox changes accordingly.

**Entry point:** Open the Production Order Assistant → **Routing** subpage → mark the operation row → **Ext. Prod. Properties** FactBox on the right. There is no separate call via **Search**; the FactBox appears only within the Production Order Assistant.

The FactBox is **read-only** – it serves as a quick overview. To change values, use the **Edit** action (see the next section).

### Fields of the FactBox

By default, the fields that show the user the operation and its values at a glance are visible. Additional fields are present but hidden and can be shown when needed via the column selection.

| Field | Explanation |
|---|---|
| **Property Code** | Technical code of the property. When a code is set, the row identifies a concrete property of the operation; the FactBox shows only rows with a set property code so that the user does not see structural empty rows. |
| **Description** | Descriptive name of the operation or the structure. When a structure row is present, this field helps the user orient themselves as to which operation the properties below belong. |
| **Standard Value** | The standard value predefined by the property definition. When no individual **Value** has been captured, production continues to work with this standard value; if the user captures a differing **Value**, this takes the place of the standard value. |
| **Value** | The property value valid for this operation. When a value is entered here, this is the authoritative target value of the property for the operation; it is processed further by the base modules when the production order is later posted. |
| **Actual Value** | The value actually achieved (from the m+m Ext. Production Information module). This field is only visible when the FactBox shows a capacity context; when an actual value is captured, it documents the actual result of the operation against the planned **Value**. |
| **Property Value Name** | Spelled-out name of the selected property value (for properties with stored value lists). When the property works with value lists, the user sees the plain text here instead of the internal value. Hidden by default. |
| **Value Permitted From** | Lower limit of the permitted value range. When a lower limit is set, the user immediately sees from which value the property is valid; this limit is checked during capture in the Edit page. Hidden by default. |
| **Value Permitted To** | Upper limit of the permitted value range. Analogous to "Value Permitted From", this field shows up to which value the property is valid. Hidden by default. |
| **Unit of Measure** | Unit of measure of the property. When a unit is stored, the user knows in which magnitude the **Value** or **Actual Value** is to be given (e.g. mm, kg). Hidden by default. |
| **Calculation Formula** | Formula with which the value is calculated automatically. When a calculation formula is stored, the **Value** is derived from the formula and cannot be entered freely; without a formula, the user enters the value manually. Hidden by default. |
| **Operation No.** | Number of the operation to which the property belongs. This field is hidden by default and is only evaluated in structure rows; it ensures the assignment of the property to the correct operation. |
| **Display Order** | Controls the order in which the properties appear relative to one another. When the display order is maintained, the user sees the properties in the desired functional sort order. Hidden by default. |
| **Data Type** | Data type of the property. The data type determines how the **Value** is to be entered and interpreted. Hidden by default; the permitted values are described in the **Data Type** section. |

> Visibility logic: The columns **Description**/**Property Code** switch depending on context (structure view vs. operation view); in the Production Order Assistant the operation view is active, so the **Property Code** is in the foreground. The **Actual Value** field is only shown in a capacity context.

## The "Ext. Prod. Properties" Edit page

Via the **Edit** action in the FactBox, the user opens the identically named **Ext. Prod. Properties** page as a separate window. Here, the properties of the same operation are shown – unlike the FactBox, however, they are **editable**. After the page is closed, the previously set filters of the FactBox are reapplied so that the display remains consistent.

**Entry point:** **Ext. Prod. Properties** FactBox → **Edit** action.

**Editability:** Whether fields are actually changeable depends on the context of the record. In the operation context of the Production Order Assistant, the value and definition fields are editable; pure display fields (e.g. **Property Value Name**, **Unit of Measure**) remain read-only.

### Fields of the Edit page

| Field | Explanation |
|---|---|
| **Property Code** | Selection of the property. When the user selects a property code in the editable context, they assign a property to the operation; the field is only changeable in the master data context, otherwise it is locked. |
| **Standard Value** | Default value of the property. When the user sets the standard value, it serves as the fallback value as long as no individual **Value** has been captured; the field is only editable in the master data context and only without a **Calculation Formula**. |
| **Value** | Authoritative property value of the operation. When the user enters a value here, it is adopted as the target value and later processed further by the base modules; the field is locked as soon as a **Calculation Formula** is stored (the value is then calculated). |
| **Actual Value** | Value actually achieved. When the user captures an actual value, they document the real result of the operation; the field is only visible and only editable when the context permits an actual value (capacity/feedback context). |
| **Property Value Name** | Plain-text name of the selected property value. This field is always read-only and serves only to verify which value was selected. |
| **Mandatory Actual Value** | Indicator from the m+m Ext. Production Information module. When this indicator is set, an **Actual Value** must be captured for the property before the operation is considered complete; if it is not set, capturing the actual value is optional. Only changeable in the master data context. |
| **Value Permitted From** | Lower limit of the permitted value range. When the user sets a lower limit, later value entries are checked against this limit; the field is only editable in the master data context and only for a numeric **Data Type** (Decimal/Integer). |
| **Value Permitted To** | Upper limit of the permitted value range. Analogous to "Value Permitted From"; likewise only in the master data context and only editable for a numeric data type. |
| **Unit of Measure** | Unit of measure of the property. This field is read-only and takes over the unit stored in the property definition; it shows the user in which magnitude the value is to be given. |
| **Calculation Formula** | Formula for automatic value determination. When a calculation formula is stored, the **Value** is calculated from it and can no longer be entered manually. The field itself cannot be entered directly; via the help function (AssistEdit) the user opens the **Generate Calculation Formula** page, selects the formula there and adopts it with **OK**. Available only in the master data context and only for a numeric data type. |
| **Display Order** | Sort position of the property. When the user changes the display order, the position of the property in the FactBox and page shifts; only editable in the master data context. |
| **Use Property Values** | Indicator of whether the property works with a fixed value list. When enabled, the user selects the **Value** from a stored list instead of entering it freely; without the indicator, free entry is possible. Hidden by default. |
| **Data Type** | Data type of the property (see the **Data Type** section). Read-only and hidden by default; controls input validation and the availability of numeric additional fields. |

### The "Data Type" field – permitted values

The **Data Type** field determines how the **Value** of a property is captured and validated. It is an option field with a fixed value range. The permitted values and their effect for the user:

- **Text:** The property takes free text; no numeric range check is performed, and the **Value Permitted From/To** fields as well as the **Calculation Formula** are not applicable.
- **Integer:** The property takes an integer; the range fields **Value Permitted From/To** and the **Calculation Formula** are available, and the user can capture only integer values.
- **Decimal:** The property takes a decimal number; as with Integer, range checking and the **Calculation Formula** are available, but with decimal places.
- **Date:** The property takes a date; the numeric range check and the calculation formula do not apply, and capture is performed as a date value.

> The value range of this data type comprises exactly these four values. An indicator for Yes/No (Boolean) is **not** included in this field.

### Creating and deleting in the page

Creating and deleting property rows is protected and only allowed in the **master data context**:

- If the user attempts to create a row even though the context does not allow it, Business Central aborts with the message **"Insert not allowed!"**.
- If the user attempts to delete a row even though the context does not allow it, the message **"Delete not allowed!"** appears.

This prevents property definitions – which actually belong to master data maintenance – from being accidentally created or removed in a pure operation/feedback context.

## Automatic transfer of properties when copying routing lines

Besides display and editing, the app contains a background function that saves the user rework: when, in the base module m+m Production Order Assistant, routing lines are copied **from a simulated production order** into a target production order, the extended production properties of the source routing line are **automatically copied along with them**.

Concretely, this means for the user:

- When a routing line is copied, any extended production properties already present in the target line are removed first so that no duplicates arise.
- Subsequently, all properties with a set **Property Code** are transferred from the source row into the target row (including **Standard Value**, **Value** and the definition fields).
- The user therefore does not have to maintain the properties of the copied operation manually again; they are immediately available in the FactBox of the target order.

This function runs without its own button; it is triggered by the copy process of the base module.

## Interplay with the base modules and the capacity ledger entries

This app displays and edits data whose processing takes place in the base modules. For understanding the overall process, the following relationship is important (the actual posting takes place in the base modules, not in this app):

- The **definition** of which properties an operation has comes from the routing and the property definitions of m+m Material Properties.
- The **Actual Value** and the **Mandatory Actual Value** come from m+m Ext. Production Information.
- When the production order is posted (via the production journal of the base modules), the extended production properties are passed on to the **capacity ledger entries** so that the values can later be viewed there.

For this, this app provides the convenient view and capture directly in the Production Order Assistant; the further processing into entries and postings remains the task of the base modules.

## Typical use cases

### Use case 1: Check the production properties of an operation

1. **Trigger:** A work-scheduling employee wants to check, before releasing a production order, which technical properties the second operation carries.
2. **Entry in BC:** They open the **Production Order Assistant** for the production order and, in the **Routing** subpage, mark the row of the relevant operation.
3. **Core flow:** On the right, in the **Ext. Prod. Properties** FactBox, they read the properties of the marked operation: **Property Code**, **Standard Value** and the authoritative **Value**. If needed, they show **Unit of Measure** and **Value Permitted From/To** via the column selection to see the specifications fully. The FactBox is read-only, so they cannot accidentally change anything while checking.
4. **Conclusion:** If all values are correct, they switch to the next operation row; the FactBox refreshes automatically.

### Use case 2: Capture the actual value of an operation

1. **Trigger:** After an operation has been processed, production reports back a measured value that is to be documented.
2. **Entry in BC:** The user opens the **Production Order Assistant**, marks the operation in the **Routing** and chooses the **Edit** action in the **Ext. Prod. Properties** FactBox.
3. **Core flow:** In the opened **Ext. Prod. Properties** page, they enter the **Actual Value** in the relevant property row. If the property is flagged as **Mandatory Actual Value**, this capture is required. If the property contains a **Calculation Formula**, the **Value** is locked and results automatically – the user then only captures the actual value. Creating additional rows is not possible in the operation context (message **"Insert not allowed!"**).
4. **Conclusion:** They close the page. The captured values appear refreshed in the FactBox; further processing into the capacity ledger entries is handled by the base module during posting.

## FAQ and troubleshooting

### 1. Why is the "Ext. Prod. Properties" FactBox empty?
The FactBox shows only properties with a set **Property Code** for the currently marked operation. If no properties are assigned to the operation, it remains empty. Check whether the item's routing contains extended production properties.

### 2. Why does the content of the FactBox change when I click a different row in the routing?
The FactBox is linked to the **Routing** subpage and always shows the properties of the marked operation. The change of display is intentional.

### 3. Why can I not change any values in the FactBox?
The FactBox is intentionally read-only and serves for viewing only. To make changes, use the **Edit** action in the FactBox and work in the opened page.

### 4. Why is the "Value" field locked in the Edit page?
The **Value** field is locked as soon as a **Calculation Formula** is stored for the property. The value is then calculated automatically from the formula and must not be overwritten manually.

### 5. How do I store a calculation formula?
In the row, select the **Calculation Formula** field and open the **Generate Calculation Formula** page via the help function (AssistEdit). Select the formula there and confirm with **OK**. This is only possible in the master data context and only for a numeric **Data Type** (Integer/Decimal).

### 6. Why do I not see the "Actual Value" field?
The **Actual Value** is only shown when the context has a capacity or feedback reference. In the pure structure or target-value view, the field is hidden.

### 7. Why do I get the message "Insert not allowed!"?
Creating new property rows is only allowed in the **master data context**. In the operation/feedback context of the Production Order Assistant, inserting is locked to prevent accidental definitions.

### 8. Why do I get the message "Delete not allowed!"?
Analogous to inserting, deleting property rows is only possible in the master data context. In the operation context it is locked.

### 9. Do I have to capture an actual value for every property?
Only if the property is flagged as **Mandatory Actual Value**. If the indicator is not set, capturing the actual value is optional.

### 10. Why are the properties already fully populated in the copied production order?
When routing lines are copied from a simulated production order, the app transfers the extended production properties automatically into the target order. You therefore do not have to capture them manually again; existing target data is cleaned up beforehand so that no duplicates arise.
