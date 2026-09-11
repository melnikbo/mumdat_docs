---
title: Anwenderhandbuch m+m Warehouse Job Overview with Package Mgt.
---

# User Guide m+m Warehouse Job Overview with Package Mgt.

## Introduction

The **m+m Warehouse Job Overview with Package Mgt.** module connects the handheld masks of the **Warehouse Job Overview**
with package management. It extends the scanner interface of the Warehouse Job Overview with three new **view types**
for packages and with two new actions that let the user create packages directly at the mask, assign them to a document,
edit their quantity to handle, or remove package assignments again.

The module itself does **not** provide a page of its own in the Business Central interface. It inserts its functions
into the already existing mask configuration of the Warehouse Job Overview and accesses the master data of package
management. Operation therefore takes place on two levels: the administrator configures the masks in Business Central,
and the warehouse worker works with the handheld device.

**Target group.** The primary target group is the **operational warehouse workers** who pick and transfer at the
handheld device and capture packages in the process. The secondary target group is **administrators and key users** who
set up the view types, actions, and field assignments once and assign the masks to the devices and users.

**Short process overview.** The typical path from entry point to result is:

**Warehouse Job Setup → mask configuration (view type + action) → field assignment per view area →
User Device Setup → handheld: warehouse job line → view Packages → action Assign Packages To Document**

A prerequisite for operational use is that the package master data (package, package category, package group) are
maintained in **m+m Package Management**. This master data is not created in this module but in package management.

## Quick Start for Users

The quick start follows the order enforced by the program flow: **first the setup**, then the assignment to the users,
and only then the work at the device.

**A. Setup (administrator, one time)**

1. Make sure that packages, package categories, and package groups are created in **m+m Package Management**. Without
   package stock, no package can be assigned at the mask.
2. Open the **Warehouse Job Setup** via **Search** and check the mask control (see the *Setup* section).
3. Open the mask configuration of the Warehouse Job Overview and create a new **view type** — depending on your needs
   **Packages**, **Existing Packages**, or **Qty. Existing Packaging**.
4. For the view type, assign the fields to be displayed (**Field Name** / **Field No.**) per **view area**
   (**Header Information**, **Line Information**).
5. Create the required actions for the view type: **Assign Packages To Document** and/or **Assign Existing Packaging**,
   supplemented by standard actions such as **Delete**, **OK**, and **Close**.
6. Assign the mask to the respective **device** or user via **User Device Setup**.

**B. Daily work (warehouse worker, at the device)**

1. On the handheld device, open the **warehouse job line** to be processed.
2. Switch to the **Packages** view.
3. Choose the **Assign Packages To Document** action. The **Create Package** dialog opens.
4. Capture **Number Of Packages**, **Location**, and **Bin** and confirm with **OK**.
5. For a package that already physically exists, choose the **Existing Packages** view and the
   **Assign Existing Packaging** action instead.
6. To correct a quantity, switch to the **Qty. Existing Packaging** view and edit the **Qty. to Handle** field. To remove
   an assignment, choose **Delete**.

If the package stock at the bin is not sufficient, the action aborts with the message *"There is not enough packaging
material in the storage area."* (see *FAQ and Troubleshooting*).

## Setup

The setup of this module does not consist of a dedicated setup page but of **extensions to the existing mask control of
the Warehouse Job Overview**. The administrator creates the new view types and actions, assigns the fields, and
distributes the masks to the devices. All pages mentioned in this chapter belong to the base module **Warehouse Job
Overview**; this module only adds new **view type** and **action type** values there.

**Entry point:** **Search → Warehouse Job Setup**, or the mask configuration of the Warehouse Job Overview.

**Permissions.** The module ships the permission set **MuM WJPM All** (caption *All Warehouse Job permissions*). This
permission set determines the permissions for the **Document Packages** intermediate table as well as for the used
Warehouse Job Overview and package objects, and defines which actions the users may perform at the mask. Assign the
permission set to the users who are to work with the package views.

### Set up view types and actions for packages

**Who and when.** This setup is performed by the administrator or key user **once before first use** — and again
whenever another mask or another device is added. It unlocks package handling on the handheld mask. The views and
actions configured here are consumed by the warehouse worker later in the chapter *Daily Work at the Warehouse Mask*.

**What this setup achieves.** Only when a view type and the associated actions have been created and assigned to a device
do the package functions appear at the handheld at all. Without this setup, the mask remains limited to the standard
warehouse functions and the user sees no package view.

**Enablement steps (in dependency order):**

1. **First**, ensure the package master data: In **m+m Package Management**, package, package category, and package
   group must exist. If no packages with stock are available, the later **Assign Packages To Document** action at the
   device fails.
2. **Then**, create a new **view type** in the mask configuration. Choose the appropriate value:
   - **Packages** — When set, the mask displays the packages to be created or assigned for the document line; a new
     package is created via this view.
   - **Existing Packages** — When set, the mask works with packages that already physically exist for the document
     assignment; the user assigns an existing package instead of creating a new one.
   - **Qty. Existing Packaging** — When set, quantity entry is active at this view; the user can edit the **Qty. to
     Handle** of an existing package directly.
3. **Then**, define the **action type** per view:
   - **Assign Packages To Document** — When this action is triggered, a package is created for the current document line
     and assigned to the document; the **Create Package** dialog opens in the process.
   - **Assign Existing Packaging** — When this action is triggered, a package that already exists is assigned to the
     document line without creating a new package.
   - In addition, the standard actions of the Warehouse Job Overview are available: **Delete** (removes the package
     assignment of the document line), **OK** (completes the entry successfully), and **Close** (ends the view without
     further processing).
4. **Finally**, carry out the field assignment per view area (see next H3) and assign the mask via **User Device Setup**
   (following H3).

**Operational conclusion.** The chain ends at the device: the warehouse worker opens the document line, switches to the
configured view, and triggers the action. The exact procedure is described in the chapter *Daily Work at the Warehouse
Mask*.

### Field assignment per view area

**Who and when.** Also part of the one-time setup. The administrator determines which fields appear in which area of the
mask.

Each view type is populated per **view area**. There are two areas:

- **Header Information** — When fields are assigned to this area, they appear in the header part of the mask and provide
  the user with the context of the document line (e.g. item, lot, location).
- **Line Information** — When fields are assigned to this area, they appear in the line part of the mask, in which the
  user sees and edits the individual packages.

For each row of the field assignment, the following entries are relevant:

| Field | Explanation |
|---|---|
| **Type** | When selected, this value determines for which view type (**Packages**, **Existing Packages**, **Qty. Existing Packaging**) the field assignment applies. |
| **View Area** | When set to **Header Information**, the field appears in the header part; with **Line Information**, in the line part of the mask. |
| **Field Name** | Shows the caption of the assigned field; it is taken automatically from the field caption of the source table when the **Field No.** is selected. |
| **Field No.** | When set, exactly this field of the underlying table is displayed at the mask; the selection is made via a field list that only allows displayable fields. |
| **Table No.** | Determined by the view type: for **Packages** the package table, for **Existing Packages** and **Qty. Existing Packaging** the document package table (**Document Packages**). The user does not have to choose it themselves. |
| **Editable** | When enabled, the user may change the field at the mask; for the **Qty. Existing Packaging** view, entry is unlocked by the system so that the **Qty. to Handle** can be edited. For the remaining package fields, only the **Qty. to Handle** is enterable. |

**Validation note.** When the administrator selects a **Field No.**, the system checks whether the field is permissible
in the source table; fields of technical types (e.g. BLOB, media, RecordID, table filter) are excluded. If the chosen
field number is invalid, the system reports an error on the **Field No.** field.

### Assign masks to users

**Who and when.** After creating the view types, actions, and field assignments, the administrator assigns the mask to
the devices or users. Without this assignment, the configured mask does not reach the handheld.

**Entry point:** **Search → User Device Setup**.

On the **User Device Setup** page, you assign per entry:

| Field | Explanation |
|---|---|
| **Type** | When set to **Device** (or user), this value defines whether the assignment applies to a physical handheld device or a named user. |
| **Code** | When set, this value identifies the specific device or user for which the mask applies. |
| **Language Code** | When set, the mask texts are displayed in the stored language; without a language code, the default language applies. |

**Process step.** First complete the mask configuration, then link the device or user with the mask here; only then are
the package views available at the handheld. This assignment is the last prerequisite for the chapter *Daily Work at the
Warehouse Mask*.

## Data Model: "Document Packages" intermediate table

This module maintains a single table of its own: the intermediate table with the caption **Document Packages**
(technically *MuM WJPM Whse Doc. Assignment*). It stores the package assignment of a document line while the document
line is being processed at the mask, and provides the fields that the administrator can assign to the views. The user
does not maintain this table directly; they see selected fields from it at the handheld mask. The following overview
explains the user-relevant fields.

| Field | Explanation |
|---|---|
| **Document Type** | When set, this value assigns the row to a package document type of package management (e.g. **Item Journal Transfer**); from this it is derived in which document the package is created. |
| **Document No.** | When filled, the row references the specific document to which the package belongs. |
| **Line Type** | When set to item, partition, or package, this value controls whether the row describes an item, a partial quantity (partition), or a package; for item/partition, the target package is used as the parent package, for package the package itself. |
| **Package Category** | When set, this value restricts the permissible package codes; only packages of the chosen category are allowed. |
| **Package Code** | When set, this value determines the package type (template) of the assigned package. |
| **Package No.** | When filled, this value identifies the specific physical package. |
| **Package Group No.** / **Package Group Code No.** | When filled, these values group packages that belong together into a package group; they link the mask row with the grouping of package management. |
| **Item No.** | When filled, this value names the item whose quantity is in the package. |
| **Variant Code** | When filled, this value specifies the item variant. |
| **Lot No.** | When filled, this value assigns the quantity contained in the package to a lot; required for lot tracking. |
| **Serial No.** | When filled, this value assigns the quantity to a serial number. |
| **Location Code** | When set, this value determines the location from which the packaging material is taken and against which the stock is checked. |
| **Bin Code** | When set, this value determines the bin within the location; the stock check of the package is performed against this bin. |
| **Qty. to Handle** | When the user changes this value in the **Qty. Existing Packaging** view, the quantity of the package to be handled is reset and validated; this is the only quantity field freely enterable at the mask. |
| **Do Not Consume Package** | When enabled, the package is retained during further processing and is not posted as consumed; without the flag, the package is consumed in the subsequent process. |
| **Net Weight** | Shows the calculated net weight of the package content; the field is not editable and serves for information. |
| **Physical Qty.** / **Remaining Physical Qty.** | Show the physical quantity of the package that is actually present or still open; they support the user in checking how much has already been handled. |
| **Document Line Qty.** | Shows the quantity of the associated document line as a reference value for package filling. |
| **Description** / **Description 2** | When filled, these free texts provide a caption of the package for display at the mask. |
| **Package Ledger Posted** / **Package Warehouse Posted** | Indicate whether the package has already been posted to the package ledger or the package warehouse; the posting itself is performed by package management, not this module. |
| *Technical key and status fields* | Not maintained by the user: **Prod. Order Line No.**, **Journal Template Name**, **Journal Batch Name**, **Entry No.**, **Document Line No.**, **Sorting No.**, **Sequence Line No.**, **Level**, **Partition Type**, **Partition Code**, **Physical RecordId**, **Source Document Type**, **Source Document No.**, **Source Line No.**, **Source Prod. Order Line No.**, **Physical Handled**, **Warehouse Job Relation**, **Package Parent Code No.**, **Package Parent No.**. These fields technically link the mask row with the document, journal, and package structure and are filled by the system. |

## Daily Work at the Warehouse Mask

**Controlling setup.** Which views and actions are offered to the warehouse worker at the handheld results entirely from
the mask configuration and the assignment under **User Device Setup** (see chapter *Setup*). If a user does not see a
view described here, the corresponding view type, action, or device assignment has not yet been set up.

At the handheld device, the warehouse worker opens the **warehouse job line** they want to process and switches to one of
the three package views. The available views and actions are:

### Packages view — create and assign a new package

When the user chooses the **Packages** view and the **Assign Packages To Document** action, the system first checks the
package stock at the bin. If stock is available, the **Create Package** dialog opens. There the user captures:

| Field | Explanation |
|---|---|
| **Number Of Packages** | When set, the specified number of identical packages is created and assigned to the document line. |
| **Location** | When set, the packaging material is taken from this location and the stock there is checked. |
| **Bin** | When set, withdrawal and stock check are performed against this bin. |

After confirmation with **OK**, the system creates the packages, assigns them to the document line, and populates them
with the item/quantity data of the line. Afterward, the package is ready in the package management document for further
processing.

### Existing Packages view — assign an existing package

When the user chooses the **Existing Packages** view and the **Assign Existing Packaging** action, the system assigns a
package that already physically exists to the document line without creating a new one. The user uses this view when the
package already exists and only needs to be linked to the current document line.

### Qty. Existing Packaging view — edit the quantity to handle

In the **Qty. Existing Packaging** view, quantity entry is unlocked. Here the user edits the **Qty. to Handle** field to
correct the quantity to be handled of an already existing package. The system validates the entered quantity; other
fields of this view are read-only.

### Remove package assignment

Via the **Delete** action, the user removes the package assignment of the current document line from the **Document
Packages** intermediate table. The underlying document line remains; only the package assignment is deleted.

**Warehouse and posting relation.** This module creates the package assignment and sets the **Qty. to Handle**; the
actual posting of the packages to the **Package Ledger** and **Package Warehouse** (fields **Package Ledger Posted** /
**Package Warehouse Posted**) as well as the creation of the item ledger entries is performed by **m+m Package
Management** in the further course of the transfer or posting process.

## FAQ and Troubleshooting

### 1. Why do I not see a package view at the handheld?

The view appears only if a matching **view type** (Packages, Existing Packages, or Qty. Existing Packaging) has been
created in the mask configuration and the mask has been assigned to the device or user via **User Device Setup**. Check
both setup steps.

### 2. What does the message "There is not enough packaging material in the storage area" mean?

When creating a package, the system checks the package stock at the specified bin. If the stock of the packaging
material is zero or not sufficient, the **Assign Packages To Document** action aborts with this message. Ensure
sufficient package stock at the location/bin or choose a different bin.

### 3. Why can I only edit the quantity to handle?

At the package views, only the **Qty. to Handle** field is enterable; all other fields are read-only. In the **Qty.
Existing Packaging** view, quantity entry is additionally unlocked by the system. This keeps the package structure
consistent while the user adjusts the quantity.

### 4. How do I assign an already existing package without creating a new one?

Switch to the **Existing Packages** view and choose **Assign Existing Packaging**. This assigns the existing package to
the document line without the **Create Package** dialog and a new creation.

### 5. What exactly happens when I trigger "Assign Packages To Document"?

The system checks the package stock, opens the **Create Package** dialog, and after confirmation with **OK** creates the
specified **Number Of Packages**, assigns them to the document line, and populates them with the item and quantity data
of the line. Afterward, the package is available in the package document.

### 6. Why is my field not displayed in the mask?

A field appears only if it is assigned in the **field assignment** to the matching **view area** (**Header Information**
or **Line Information**) with a valid **Field No.**. Technical field types (e.g. BLOB, media) are not selectable and
cannot be displayed.

### 7. What does the "Do Not Consume Package" flag mean?

When **Do Not Consume Package** is enabled, the package is retained in the subsequent process and is not posted as
consumed. Without this flag, the package is consumed in the further course.

### 8. Why is the net weight not editable?

The **Net Weight** is calculated from the package content and serves only for information. It cannot be changed at the
mask; instead, change the underlying quantity or item data.

### 9. How do I recognize whether a package has already been posted?

The **Package Ledger Posted** and **Package Warehouse Posted** fields indicate whether the package has been posted to
the package ledger or the package warehouse. The posting itself is performed by **m+m Package Management**, not this
module.

### 10. How do I remove an incorrect package assignment?

At the mask, choose the **Delete** action. This removes the package rows of the current document line from the **Document
Packages** intermediate table; the document line itself remains.

## Typical Use Cases

### Use case 1: Create a new package during picking

**Trigger.** A warehouse worker picks a transfer and needs a new package for the withdrawn goods in order to pack the
quantity cleanly and forward it.

**Entry in BC.** At the handheld device, the worker opens the relevant **warehouse job line** and switches to the
**Packages** view.

**Core procedure.**
1. The worker chooses the **Assign Packages To Document** action.
2. The system checks the package stock at the bin; if stock is available, the **Create Package** dialog opens.
3. The worker captures **Number Of Packages**, **Location**, and **Bin** and confirms with **OK**.
4. The system creates the packages, assigns them to the document line, and populates them with the item, lot, and
   quantity data of the line.

**Conclusion.** The package is ready in the package management document. The later posting of the package ledger and
package warehouse takes place in the downstream transfer process performed by package management.

### Use case 2: Assign already packed goods

**Trigger.** The goods are already packed in a physically existing package; the worker only needs to assign this package
to the current document line.

**Entry in BC.** The worker opens the **warehouse job line** and switches to the **Existing Packages** view.

**Core procedure.**
1. The worker chooses the **Assign Existing Packaging** action.
2. The system links the existing package with the document line without creating a new package.

**Conclusion.** The assignment is set; a **Create Package** dialog does not appear in this case.

### Use case 3: Correct a quantity or remove an assignment

**Trigger.** During packing, the worker notices that the captured quantity is incorrect, or a package was accidentally
assigned to the wrong line.

**Entry in BC.** The worker opens the **warehouse job line**.

**Core procedure.**
1. To correct the quantity, the worker switches to the **Qty. Existing Packaging** view and edits the **Qty. to Handle**
   field; the system validates the new quantity.
2. To remove an incorrect assignment, the worker chooses the **Delete** action; the package assignment of the row is
   removed from the **Document Packages** intermediate table.

**Conclusion.** After the correction, the worker can process the line again via **Assign Packages To Document** or
**Assign Existing Packaging** and complete the operation with **OK**.
