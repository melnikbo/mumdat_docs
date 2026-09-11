---
title: Anwenderhandbuch m+m Goods Receipt with Package Management
---

# User Guide m+m Goods Receipt with Package Management

## Introduction

The app **m+m Goods Receipt with Package Management** connects the m+m **Goods Receipt** with the m+m **Package Management**. It makes it possible to assign the individual component lines to a **Package** already during goods receiving in the warehouse, to create new packages directly from a component, and to adopt packages from a **Package Reference**. When the goods receipt is processed, the packages are transferred automatically into the processed goods receipt as well as into a resulting transfer receipt, and they can be printed as labels.

Processing relies entirely on the underlying documents of the goods receipt. The app does not add any documents of its own there; instead it extends the existing **Warehouse Receipt**, the **Transfer Receipt**, the **Package Ledger Entry**, and the associated **Goods Receipt Setup** with package functions.

**Target audience.** The primary users are **operational warehouse staff** and people in goods receiving who record component lines, assign packages, and process goods receipts on a daily basis. Secondarily, the **Setup** chapter is aimed at administrators or key users who configure package processing once.

**Typical path through the app.** The user opens the **Warehouse Receipt**, selects a line or its component lines, uses the package actions to assign a package (or create one), and then starts **Process Warehouse Receipt and Print Packages**. The packages afterwards appear in the processed goods receipt, in the follow-up documents of the transfer, and in the **Package Ledger Entry**.

## Quick Start for Users

The fastest path from setup to the printed package follows the order enforced by the code (first setup, then document, then processing):

1. **Check the setup.** Using **Search**, open the **Goods Receipt Setup** and, on the **Processing** tab, define whether and how packages are printed (**Print Package**), which report is used for this (**Package Print Report ID**), and whether packages are automatically assigned to components (**Automatically Assign Package to Component**). See the **Setup** chapter.
2. **Open the Warehouse Receipt.** Using **Search**, open the **Warehouse Receipt** and select the document to be processed.
3. **Select a component line.** Open the component lines of the goods receipt. In the **Package Status** column, the color indicates whether a line is not yet, partially, or fully assigned to a package.
4. **Assign or create a package.** On the line, choose one of the actions **Package Assignment**, **Create New Package**, or **Create from Package Reference** (see **Daily Work – Component Lines and Packages**).
5. **Process and print.** In the **Warehouse Receipt**, choose the action **Process Warehouse Receipt and Print Packages**. Confirm the processing dialog; afterwards the packages of the report **Processed Goods Warehouse Receipt Packages** are printed.
6. **Check the result.** Review the created packages in the processed goods receipt, in the **Transfer Receipt** (field **Package Status**), and in the **Package Ledger Entry** (fields **Goods Rcpt. Whse. Receipt No.** and **Goods Rcpt. Whse. Rcpt. Line No.**).

The package label print can also be triggered afterwards from the processed goods receipt via the action **Print Packages**.

## Setup

The central configuration of this app resides entirely on the existing page **Goods Receipt Setup** of m+m Goods Receipt. There is no dedicated setup page for this app; the three package fields are inserted into the existing **Processing** tab. BC users therefore see exactly **one** setup page, which is described in full below with regard to package processing.

### Setting up package printing and automatic package assignment

**Who and when.** This setup is performed by an administrator or key user **once, before the first goods receipt with packages**. It controls which report is printed during processing, whether printing happens at all, and whether packages are automatically transferred to production order components during posting. The values later take effect in the **Warehouse Receipt** (action **Process Warehouse Receipt and Print Packages**) as well as when components are posted.

**Access:** Using **Search**, open the **Goods Receipt Setup** page and switch to the **Processing** tab. This is a company-wide setup (one record per company).

When the page is opened, the app automatically enters a default report if none has been stored yet (see **Package Print Report ID**).

| Setup | Explanation |
|-------------|-------------|
| Print Package | Defines whether and how package labels are printed when the goods receipt is processed. **No Printing:** During processing no package report is printed; the package assignment remains purely data-side. **Per Package:** A label of the stored report is created for each individual package. **Per Package Group:** Printing is bundled per package group; correspondingly, the allocation **Per Package Group** is used on the warehouse receipt line so that the quantity to be assigned is determined per group. |
| Package Print Report ID | Determines the report that is run for the package print. If the field is empty, the app automatically enters the supplied report **Processed Goods Warehouse Receipt Packages** when the setup is opened and during processing; store a different report here if you use your own label layout. The report stored in this way is used both for **Process Warehouse Receipt and Print Packages** and for the subsequent action **Print Packages**. |
| Automatically Assign Package to Component | When enabled, the existing physical packages are automatically transferred to the linked production order component when the goods receipt item journal is posted; the user does not have to assign the packages to the component manually. Without this flag, this automatic transfer is omitted, and the component remains without a package reference until an assignment is made manually. |

**Process steps of the setup.**

1. **First**, decide under **Print Package** whether printing should occur and whether per package or per package group. For **Per Package Group**, make sure that the relevant warehouse receipt lines use the allocation **Per Package Group**.
2. **Then**, check or store the desired report under **Package Print Report ID**. If you leave the field empty, the default report is set automatically.
3. **Finally**, enable **Automatically Assign Package to Component** if packages are to be transferred to production order components during posting without an extra step.

The effect of these fields in day-to-day operation is described in the chapter **Daily Work – Component Lines and Packages** as well as in **Process Warehouse Receipt and Print Packages**.

## Master Data and Allocation Control

This app maintains no master data cards of its own (no team, error, or profile master data). The only master-data-related control point is the **Allocation** on the warehouse receipt line, which is extended by a package value.

### Allocation "Per Package Group" on the warehouse receipt line

On the warehouse receipt line of m+m Goods Receipt, the **Allocation** field (2nd allocation, field **Allocation 2**) controls how the output quantity is distributed across the components. This app adds the additional value **Per Package Group** to this selection.

| Field | Explanation |
|------|-------------|
| Allocation → **Per Package Group** | If the allocation **Per Package Group** is selected on the warehouse receipt line, the quantity to be assigned per component is based on the quantity of the associated package group (field **Qty. to Handle** of the package), and the number of allocations corresponds to the **Total Number of Packages** of the component. This results in exactly one allocation per package group. |

**Validation rule (from the code).** When the allocation **Per Package Group** is selected, the warehouse receipt line may have only **one** component line that does not carry the **Package Status** **Package**. If several such component lines exist, the system aborts the selection with an error message. Therefore set the allocation while the line still contains only a single open component, and bundle further quantities via packages.

The relationship to the setup: The value **Per Package Group** works together with the setting **Print Package → Per Package Group** (chapter **Setup**), so that allocation and label printing are based on the same grouping.

## Daily Work – Component Lines and Packages

The actual package work takes place on the **component lines of the warehouse receipt**. This page is controlled by the settings of the **Goods Receipt Setup** (**Processing** tab): there it is defined whether and how printing occurs and whether packages are automatically transferred to components. The following description assumes an opened **Warehouse Receipt** and its component lines.

### Additional columns of the component line

The app adds the following fields to the component line:

| Field | Explanation |
|------|-------------|
| Package Status | Indicates how far the component line has already been assigned to a package. The field is not editable and is updated from the associated item journal line when the line is accessed. It is color-highlighted (see values below). **(empty):** The line is not yet assigned to a package — the package assignment still has to be made. **Full:** The line quantity is fully assigned to a package (green, "favorable"). **Partially:** Only part of the quantity is assigned (yellow, "ambiguous") — a remaining quantity is left. **Package:** The line is itself a package line (highlighted); such lines are locked and can neither be changed nor assigned as a component of their own. |
| Total Number of Packages | Shows the number of packages created for this warehouse receipt line (number of package lines in the document packages). The value is calculated continuously; a zero is hidden. It serves as the basis for the allocation **Per Package Group** (see **Master Data and Allocation Control**). |
| Package Reference No. | Refers to a stored **Package Reference** (packing specification) and pre-fills the package structure from it. On entry, the app checks and adopts the reference based on item, variant, quantity, and customer of the goods receipt. The field can only be selected while the **Package Status** is **(empty)** and the line quantity is greater than 0; otherwise the system reports that the reference cannot be selected because the quantity is 0 or the item has already been assigned to a package. |

### Actions on the component line

The line actions in the **Line** menu cover the three ways to form a package for a component:

| Action | Explanation |
|--------|-------------|
| Package Assignment | Opens the package assignment of the package management for the item journal line belonging to the row. Here the user assigns the existing quantity to existing packages. The action is disabled if the line already has the **Package Status** **Package**. |
| Create New Package | Creates a new package from the component line and distributes the quantity to be assigned evenly across the newly created packages; the remaining quantity is added to the last package. Packages of the line that were formed earlier are retained and are not filled again. |
| Create from Package Reference | Creates the packages based on the **Package Reference No.** entered on the line, i.e. according to the stored packing specification, and then combines package components of the same type on the line. The action is disabled if the line already has the **Package Status** **Package**. |

**Sequence for package formation.**

1. **First**, select the component line and check the **Package Status**. Only lines with status **(empty)**, **Full**, or **Partially** can be edited; lines with status **Package** are locked.
2. **Then**, choose the appropriate approach: fill existing packages (**Package Assignment**), form a new package (**Create New Package**), or create according to specification (**Create from Package Reference** after entering the **Package Reference No.**).
3. **Finally**, check the updated **Package Status** and the **Total Number of Packages** of the line before you process the goods receipt.

**Locking behavior (from the code).** A component line with **Package Status** **Package** cannot be changed; the system rejects changes with a message. If the package status of a line is reset to **(empty)**, the app simultaneously removes the **Package Reference No.**.

## Process Warehouse Receipt and Print Packages

The conclusion of the daily work is processing the goods receipt. This flow connects the standard processing of the goods receipt with the package print from the **Goods Receipt Setup**.

### Processing from the Warehouse Receipt

**Access:** In the **Warehouse Receipt**, you find the action **Process Warehouse Receipt and Print Packages** on the ribbon under **Process** (also available as a promoted action).

Flow (from the code):

1. In the **Warehouse Receipt**, select the document and the action **Process Warehouse Receipt and Print Packages**.
2. Confirm the processing dialog of the goods receipt (Yes/No). Upon confirmation, the goods receipt is processed.
3. After processing, the app determines the associated **processed goods receipt** and starts, for its documents, the report stored under **Package Print Report ID** — by default **Processed Goods Warehouse Receipt Packages**.
4. The report is output as a print preview/print; depending on the **Print Package** setting, printing occurs per package or per package group. If **Print Package** is set to **No Printing**, the goods receipt is processed but no label is printed.

### Reprinting package labels

**Access:** In the **processed goods receipt**, you find the action **Print Packages** under **Reports** (also as a promoted action).

Using this action, you reprint the package labels for the selected processed documents without processing the goods receipt again. Here, too, the report stored under **Package Print Report ID** is used.

### Report "Processed Goods Warehouse Receipt Packages"

The supplied report **Processed Goods Warehouse Receipt Packages** is the standard label report. It outputs the processed goods receipt with its packages and generates one barcode (Code 128) per package from production order and package data.

| Field in the report | Explanation |
|-----------------|-------------|
| Customer No. / Sell-to Customer Name | Customer of the processed goods receipt for whom the packages are intended. |
| External Order No. | External purchase/order number of the customer for the document. |
| External Shipment No. | External shipment number of the customer for the document. |
| Processed Warehouse Receipt No. | Number of the processed goods receipt the packages originate from. |
| Receipt Date | Receipt date of the goods receipt. |
| Item No. | Item of the respective package or package position. |
| Package No. | Number of the printed package; together with the superordinate package it forms the label structure. |
| Quantity | Quantity of the item position in the package. |

The report is the default value of the field **Package Print Report ID**; you store your own layout via this field (see **Setup**).

## Transfer and Follow-up Documents

The app transfers the package assignment automatically into the follow-up processes of the goods receipt, in particular into the transfer that results from a processed goods receipt document.

### Package Status in the Transfer Receipt

The **Transfer Receipt** of the goods receipt is extended by the **Package Status** on the line. The line thereby shows the same assignment logic as the goods receipt.

| Field | Explanation |
|------|-------------|
| Package Status | Adopts the package status from the associated transfer line and shows in color how far the transfer line is assigned to a package. **(empty):** not yet assigned. **Full:** fully assigned (green). **Partially:** partially assigned (yellow) — remaining quantity open. The field is not editable and is updated when the line is accessed. |

In addition, the transfer receipt shows an info box **Component Package Structure**, which represents the package structure for the selected transfer line.

**Line action.**

| Action | Explanation |
|--------|-------------|
| Package Assignement - Receipt | Opens the package assignment of the package management for the transfer line belonging to the row, so that the incoming goods of the transfer can be assigned to a package. |

**Automatic transfer (from the code).** When a transfer order for raw material is created from a processed goods receipt document, the app automatically transfers the physical packages of the source document as document packages of the transfer shipment. Likewise, when the transfer lines are retrieved, the **Package Status** from the transfer line is adopted into the line of the transfer receipt. As a result, the user finds the packages again in the transfer without an extra step.

### Goods receipt reference in the Package Ledger Entry

The **Package Ledger Entry** of the package management is extended by the reference to the goods receipt, so that every posted package can be traced back to the warehouse receipt line.

| Field | Explanation |
|------|-------------|
| Goods Rcpt. Whse. Receipt No. | Number of the goods receipt the package originates from. Enables tracing a package ledger entry back to the original warehouse receipt document. |
| Goods Rcpt. Whse. Rcpt. Line No. | Line number of the goods receipt the package originates from. Together with the **Goods Rcpt. Whse. Receipt No.** it enables the line-precise assignment of the package ledger entry. |

## History and Tracking

This app does not create any history or log pages of its own. Tracking is done via the existing documents and entries:

- The **processed goods receipt** documents the completed goods receipts along with their packages and allows reprinting via **Print Packages**.
- The **Package Ledger Entry** shows, via **Goods Rcpt. Whse. Receipt No.** and **Goods Rcpt. Whse. Rcpt. Line No.**, which goods receipt a package originated from.
- In the **Transfer Receipt**, the **Package Status** is visible per line, so that open and completed package assignments of the transfer can be tracked.

## FAQ and Troubleshooting

### 1. Why can I not select a package reference on a component line?
The **Package Reference No.** can only be entered while the line has the **Package Status** **(empty)** and the line quantity is greater than 0. If the quantity is 0 or the item has already been assigned to a package, the system reports that the reference cannot be selected. Check the quantity and package status of the line.

### 2. Why can I no longer change a component line?
Lines with **Package Status** **Package** are locked. The system rejects changes with the note that lines with this package status cannot be changed. Edit the package itself instead, or reset the assignment.

### 3. What do the colors in the "Package Status" column mean?
The color reflects the degree of assignment: **Full** is shown in green ("favorable"), **Partially** in yellow ("ambiguous"), and **Package** highlighted. The empty status remains without highlighting and means: no assignment yet.

### 4. Why is no package label printed during processing?
If, in the **Goods Receipt Setup**, the field **Print Package** is set to **No Printing**, the action processes the goods receipt but prints no label. Set the value to **Per Package** or **Per Package Group** so that the report is run.

### 5. Which report is used for the package print?
The report stored under **Package Print Report ID**. If the field is empty, the app automatically enters the supplied report **Processed Goods Warehouse Receipt Packages** — both when the setup is opened and during processing. For your own layout, store your report there.

### 6. How do I print packages afterwards without processing again?
Open the **processed goods receipt** and choose the action **Print Packages** under **Reports**. This outputs the labels of the selected documents again without processing the goods receipt once more.

### 7. Why do I get an error message with the allocation "Per Package Group"?
With the allocation **Per Package Group**, the warehouse receipt line may have only **one** component line that does not carry the package status **Package**. If several such component lines exist, the system aborts the selection. Reduce the open components or bundle quantities via packages.

### 8. When are packages automatically transferred to a production order component?
Only if the field **Automatically Assign Package to Component** is enabled in the **Goods Receipt Setup**. Then, when the goods receipt item journal is posted, the app transfers the physical packages to the linked production order component. Without the flag, the transfer is omitted.

### 9. How do I find out which goods receipt a posted package originates from?
Open the **Package Ledger Entry**. The fields **Goods Rcpt. Whse. Receipt No.** and **Goods Rcpt. Whse. Rcpt. Line No.** refer, line-precisely, to the original goods receipt.

### 10. Why does the package quantity differ between the newly created packages?
With **Create New Package**, the app distributes the quantity to be assigned evenly across the packages and adds the remaining quantity to the **last** package. As a result, the last package may contain a slightly different quantity than the others.

## Typical Use Cases

### Use Case 1: Goods receipt with new package formation and label printing

**Trigger.** An announced delivery arrives in the warehouse, whose components are to be packed and labeled for a sales order.

**Access in BC.** The user opens the **Warehouse Receipt** via **Search** and selects the relevant document. Prerequisite: In the **Goods Receipt Setup**, **Print Package** is set to **Per Package** (see **Setup**).

**Core flow.**
1. The user opens the component lines and checks the **Package Status** column — the lines are set to **(empty)**.
2. On the line, they choose **Create New Package**; the app forms the packages and distributes the quantity. The **Package Status** changes to **Full** or **Partially**, and the **Total Number of Packages** increases accordingly.
3. Back in the **Warehouse Receipt**, the user chooses **Process Warehouse Receipt and Print Packages** and confirms the dialog.

**Conclusion.** After processing, the app prints the report **Processed Goods Warehouse Receipt Packages** per package. The packages are afterwards traceable in the **processed goods receipt** and in the **Package Ledger Entry** (with **Goods Rcpt. Whse. Receipt No.**).

### Use Case 2: Packing according to a stored specification (Package Reference)

**Trigger.** A fixed packing specification applies to a customer; the incoming goods are to be packaged exactly accordingly.

**Access in BC.** The user opens the **Warehouse Receipt** and its component lines.

**Core flow.**
1. They enter the **Package Reference No.** in the component line (only possible with package status **(empty)** and quantity > 0). The app checks the reference based on item, variant, quantity, and customer.
2. Next, they choose the line action **Create from Package Reference**; the packages are created according to the specification, and package components of the same type are combined.
3. The user processes the document via **Process Warehouse Receipt and Print Packages**.

**Conclusion.** The packages formed according to specification are printed and are available in the processed goods receipt as well as in the **Package Ledger Entry**.

### Use Case 3: Transfer of raw material with adopted packages

**Trigger.** A transfer order is created from a processed goods receipt to bring raw material to another location; the packages already formed are to be retained.

**Access in BC.** The user opens the **Transfer Receipt** of the goods receipt.

**Core flow.**
1. When the transfer order is created, the app automatically transfers the physical packages of the goods receipt document as document packages of the transfer shipment.
2. The user retrieves the transfer lines; the **Package Status** is adopted from the transfer line and displayed per line. Via the info box **Component Package Structure**, they check the package structure.
3. If necessary, they assign incoming goods to a package via the line action **Package Assignement - Receipt**.

**Conclusion.** The transfer receipt shows the correct **Package Status** per line; the packages remain assigned throughout and traceable in the **Package Ledger Entry**.
