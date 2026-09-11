---
title: Anwenderhandbuch m+m Production Order Job Overview with Test Certificate Mgt.
---

# User Guide m+m Production Order Job Overview with Test Certificate Mgt.

## Introduction

The app **m+m Production Order Job Overview with Test Certificate Mgt.** extends the **Prod. Order Job Overview** view in Microsoft Dynamics 365 Business Central with the test data from Test Certificate Management. In the line list of the Prod. Order Job Overview, users see the **Test Status** and the associated **Test Certificate No.** directly for each operation, without having to open the production order or the test certificate separately.

**Target audience:** This module is aimed primarily at the **operational users in production** – workers, foremen, and production control – who start, partially finish, and finish operations in the Prod. Order Job Overview. For these users, the test status is the decisive additional information before an operation is reported. Secondarily, the module concerns **Quality Assurance**, which maintains the test certificates and samples, as well as **Administration**, which grants the permissions.

**Brief process overview:** The user opens the **Prod. Order Job Overview** via the search, narrows the list down using **Work Center No.** and optionally **Machine Center No.**, and receives one line per operation. For each line, the module displays the **Test Status** and the **Test Certificate No.** and, in the **Test Characteristics FactBox**, shows the test characteristics of the assigned test certificate. Using a drill-down function, the user navigates directly to the **Test Certificate Card** or to the **Samples**. The user then reports the operation back in the usual Prod. Order Job Overview workflow (**Start**, **Partially Finish**, **Finish**).

The test data is transferred **automatically** from the operation of the production order into the line of the Prod. Order Job Overview; the user does not have to enter the test status manually.

## Quick Start for Users

The fastest path from opening the list to reporting an operation with a passed test status:

1. Open **Prod. Order Job Overview** via **Search**.
2. In the **Work Center No.** field, select the responsible work center. All operations of this work center appear.
3. Optionally set the **Machine Center No.** field to narrow the list down to a single machine center (not mandatory).
4. Select the desired operation line. The line shows the **Test Status** (color-coded) and the **Test Certificate No.**.
5. If the **Test Status** = **Blocked** (red), first clarify the test certificate: either click **Test Status** or **Test Certificate No.** in the line to open the **Test Certificate Card**, or use the **Open Test Certificate Samples** action to switch to the **Samples** and complete the test data.
6. Start the operation: **Start** action.
7. For a partial quantity: **Partially Finish** action – the operation remains open for the remaining quantity.
8. Upon full completion: **Finish** action – the operation is set to **Finished**.

> The prerequisite is that a test certificate is assigned to the operation in the routing of the production order. If no test certificate is stored, **Test Status** = **(empty)** and **Test Certificate No.** remain empty; the reporting workflow is not affected by this.

## Prerequisites and Permissions

This module is a pure integration extension and does not bring its own setup pages, number series, or master data. For the test data to appear in the Prod. Order Job Overview, the following building blocks must be present:

1. The app **m+m Production Order Job Overview** provides the **Prod. Order Job Overview** view and the reporting workflow (**Start**, **Partially Finish**, **Finish**). It is a prerequisite because this module extends its line list.
2. The app **m+m Test Certificate Management** provides the test certificates, the **Test Certificate Card**, and the **Samples**. It is a prerequisite because the test status and the test certificate number originate from this source.
3. A test certificate must be assigned to the operation (routing of the production order). Only then does the module fill **Test Status** and **Test Certificate No.** in the Prod. Order Job Overview line.

**Permissions:** The extension delivers the permission set **MuM PJTC All**. This defines which actions users may perform in connection with the test data in the Prod. Order Job Overview; it covers the execution of the two processing codeunits and access to the **Test Characteristics FactBox**. Administration assigns this permission set in addition to the permissions of the two base modules. Without the permissions of the base modules, the Prod. Order Job Overview itself cannot be used.

## Daily Work in the Prod. Order Job Overview

The **Prod. Order Job Overview** is the central work list of this module. The following sections describe the components added by the module and how they fit into the existing reporting workflow. The user opens the view via **Search**; it is a superordinate work list and is not called from a master data card.

### Entry Point and Filters

**Entry point:** **Search** → **Prod. Order Job Overview**. The user then narrows the list down using the two header filters. The filter for the work center is the superordinate level, the filter for the machine center is the optional subordinate level.

| Filter field | Explanation |
|------------|-------------|
| **Work Center No.** | When set, only the operations of the selected work center are shown. This filter is the usual entry point: the user first selects their work center and then sees all open operations for it. |
| **Machine Center No.** | When additionally set, the list is restricted within the work center to a single machine center. This filter is optional; without it, all machine centers of the work center remain visible. |

Both filters are part of the base view; the extension does not add any further filters.

### New Columns in the Line List

For each operation line of the Prod. Order Job Overview, the module displays two additional columns. They appear at the end of the line and are not editable – the values are transferred automatically from the operation (see *Automatic Transfer of the Test Data*).

| Field | Explanation |
|------|-------------|
| **Test Status** | Shows the test state of the operation and is color-highlighted. When the value is set, the user recognizes at a glance, before reporting, whether the test is open, passed, or blocked. Clicking the column opens the **Test Certificate Card** of the assigned test certificate. The individual values are explained below. |
| **Test Certificate No.** | Contains the number of the test certificate assigned to the operation. When filled, it references the specific test certificate in Test Certificate Management; if no test certificate is assigned, the field remains empty. Clicking the column likewise opens the **Test Certificate Card** of this test certificate. |

**Values of the Test Status field** (each value controls what the user should do before reporting):

- **(empty):** No test certificate is assigned to the operation. No test action is required; the operation can be reported normally.
- **Test:** A test certificate is assigned to the operation, but a final result is not yet available. The user should check or complete the test data before finishing. The line is highlighted neutrally.
- **Passed:** The test has been completed successfully. The operation can be reported without any further test action. The line is highlighted positively (green).
- **Blocked:** The test has not passed or is blocked. The user should **not** finish the operation without clarification; the test certificate must first be clarified via the **Test Certificate Card** or the **Samples**. The line is highlighted negatively (red).

> The color highlighting serves for quick orientation in the list: green for **Passed**, red for **Blocked**, neutral for **Test**. The test status is a display and decision aid and does not change the technical reporting workflow of the Prod. Order Job Overview; in particular, it does not automatically prevent finishing. The assessment of whether reporting is permitted when **Blocked** is made by the user in accordance with the operational guidelines.

For orientation, the base view additionally shows, among other things, the **Production Order No.**, the **Item No.**, the **Operation No.**, as well as **Quantity** and **Remaining Quantity** for each operation line. These columns belong to the base module; **Test Status** and **Test Certificate No.** supplement them at the end of the line.

### Test Characteristics FactBox

In addition to the columns, the module displays the **Test Characteristics FactBox** on the right. It is coupled to the **Test Certificate No.** of the currently selected line and shows the test characteristics (lines) of the assigned test certificate. This way, the user sees the characteristics and their default values without having to open the test certificate.

| Field | Explanation |
|------|-------------|
| **Test Group Code** | Shows the test group of the characteristic. When filled, it assigns the characteristic to a group in Test Certificate Management and helps the user recognize related characteristics. |
| **Characteristic Description** | Describes the individual test characteristic in plain text, so that the user recognizes what is being tested without having to refer to codes. |
| **Default Value 1** | Shows the first default value of the characteristic. When set, it serves the user as a target/reference value for the test. |
| **Default Value 2** | Shows the second default value of the characteristic (e.g. a second limit or alternative). When set, it supplements **Default Value 1** as a further reference. |

The FactBox is display-only (not editable). The characteristic lines without an assigned test certificate remain empty. Technically non-visible control fields of the FactBox (the internal **Test Certificate No.** of the line as well as a print option) are hidden and are not relevant to the user.

### Open Test Certificate Samples Action

In the ribbon of the Prod. Order Job Overview, the module adds the (also pinned as a processing action) **Open Test Certificate Samples** action.

Use the **Open Test Certificate Samples** action to open the samples of the test certificate belonging to the selected line:

- If exactly **one** sample exists for the test certificate, the **Sample** (single card) opens directly.
- If **several** samples exist, the **Samples** list opens, from which the user selects the desired sample.

If no valid **Test Certificate No.** is assigned to the selected line, nothing happens. This way, the user can view the sample data directly from the Prod. Order Job Overview and – in Test Certificate Management – complete it before finishing the operation.

### Drill-Down to the Test Certificate Card

Via the **Test Status** and **Test Certificate No.** columns, the user drills down to the **Test Certificate Card** of the assigned test certificate with a click. Click one of these columns to open the **Test Certificate Card** to view the test certificate in detail. After the card is closed, the module updates the line automatically: the current **Test Status** and the **Test Certificate No.** are read again from the operation of the production order and displayed in the line. Changes to the test certificate thus take immediate effect on the display in the Prod. Order Job Overview.

### Automatic Transfer of the Test Data

The **Test Status** and the **Test Certificate No.** are not entered manually but are determined automatically. When building the line list of the Prod. Order Job Overview, the module reads the associated operation of the production order for each operation line and transfers the stored test status and the test certificate number from there into the displayed line. The assignment is made via production order, production order line, and **Operation No.**.

Practical consequence for the user:

- If the test certificate or its status changes at the operation, the change appears automatically in the line the next time the list is built, or after drilling down to the **Test Certificate Card**.
- Since the values are derived, the **Test Status** and **Test Certificate No.** columns are not editable in the Prod. Order Job Overview.

### Placement in the Reporting Workflow

The test data is a decision aid within the existing reporting workflow of the Prod. Order Job Overview. The complete workflow is:

1. Open **Prod. Order Job Overview** via **Search**.
2. Set **Work Center No.** (superordinate filter).
3. Optionally set **Machine Center No.** (subordinate filter).
4. Select the operation line and check the **Test Status**; if **Blocked**, clarify via **Test Certificate Card** or **Open Test Certificate Samples**.
5. **Start** – the operation is set to **Started**.
6. **Partially Finish** – for partial quantities; the status changes to **Partly Finished** and the remaining quantity stays open.
7. **Finish** – upon full completion; the status changes to **Finished**.

The **Start**, **Partially Finish**, and **Finish** actions as well as the associated posting page belong to the base module **m+m Production Order Job Overview**; this module neither hides nor adds a posting step. For the details of the posting dialog, the documentation of the base module applies.

## Typical Use Cases

The following scenarios show how the test data is used in day-to-day business. All steps correspond to the workflow described above and implemented in the code.

### Use Case 1: Clarify a blocked test certificate before finishing

**Trigger:** A worker wants to finish an operation and sees a line highlighted in red in their work list.

**Entry in BC:** They open the **Prod. Order Job Overview** via **Search** and select their work center in the **Work Center No.** field.

**Core workflow:** In the line of the relevant operation, **Test Status** = **Blocked**. The worker clicks the **Test Status** column and navigates to the **Test Certificate Card**. There they recognize that the test did not pass. They clarify the case with Quality Assurance. After the card is closed, the Prod. Order Job Overview updates the line automatically. Only once the test certificate – in Test Certificate Management – is set to **Passed** and the line appears green does the worker report the operation.

**Completion:** The worker selects **Finish**; the operation is set to **Finished**.

### Use Case 2: Record sample data and partially finish an operation

**Trigger:** For an ongoing operation, there is a note that sample values must be documented before the partial report.

**Entry in BC:** The user opens the **Prod. Order Job Overview** via **Search**, sets **Work Center No.** and optionally **Machine Center No.**, and selects the operation line.

**Core workflow:** In the **Test Characteristics FactBox**, they see the test characteristics with **Characteristic Description** and the **Default Value 1**/**Default Value 2**. Using the **Open Test Certificate Samples** action, they switch to the **Samples** of the test certificate and enter the values there. They then return to the Prod. Order Job Overview; the **Test Status** of the line is updated.

**Completion:** Since only a partial quantity is finished, the user selects **Partially Finish**. The status changes to **Partly Finished**, and the remaining quantity stays open for a later report. After the remaining quantity is completed, they finish the operation later with **Finish**.

## FAQ and Troubleshooting

### 1. Why is the test status empty for a line in the Prod. Order Job Overview?
Because no test certificate is assigned to the operation in the routing of the production order. The module transfers **Test Status** and **Test Certificate No.** only when a test certificate is stored at the operation. Without an assignment, both fields remain empty, and no test action is required.

### 2. How do I open the test certificate for a line?
Click **Test Status** or **Test Certificate No.** in the line. Both columns drill down to the **Test Certificate Card** of the assigned test certificate.

### 3. What do the colors in the Test Status column mean?
Green stands for **Passed**, red for **Blocked**, neutral for **Test** (test certificate assigned, but no result yet). **(empty)** means: no test certificate assigned. The color is an orientation aid for the decision before reporting.

### 4. Can I finish an operation with the test status Blocked?
The module does not technically prevent finishing. **Blocked** is a warning that the test did not pass. Whether reporting is permitted depends on the operational guidelines; clarify the case beforehand via the **Test Certificate Card** or the **Samples**.

### 5. Why can I not change Test Status and Test Certificate No.?
Both columns are not editable because their values are derived automatically from the operation of the production order. You make changes at the test certificate in Test Certificate Management; the display in the Prod. Order Job Overview is then updated automatically.

### 6. The test certificate was changed – why do I not see the new status immediately?
The values are re-determined when the line list is built or after drilling down to the **Test Certificate Card**. After the **Test Certificate Card** is closed, the module updates the line automatically; alternatively, rebuilding the list is sufficient.

### 7. What does the Test Characteristics FactBox show?
It shows the test characteristics (lines) of the test certificate that is assigned to the currently selected line – with **Test Group Code**, **Characteristic Description**, as well as **Default Value 1** and **Default Value 2**. The FactBox is display-only.

### 8. What is the Open Test Certificate Samples action for?
It opens the **Samples** of the test certificate belonging to the selected line. If there is exactly one sample, the **Sample** opens directly; if there are several, the **Samples** list opens for selection. This way, you reach the sample data directly from the Prod. Order Job Overview.

### 9. I do not have permission for the test data – why is that?
The permission set **MuM PJTC All** is required for the test data in the Prod. Order Job Overview. In addition, the permissions of the base modules **m+m Production Order Job Overview** and **m+m Test Certificate Management** must be present. Contact your administration.

### 10. I do not see the new columns and the FactBox – what should I do?
Check whether the app is installed, whether the permission set **MuM PJTC All** is assigned, and whether the two base modules are present. If the columns are hidden in your personal view, use personalization to show **Test Status** and **Test Certificate No.** again. If the values remain empty, no test certificate is assigned to the operation (see question 1).
