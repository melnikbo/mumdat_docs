---
title: Anwenderhandbuch m+m Label Management with Package Management
---

# User Guide m+m Label Management with Package Management

## Introduction

The app **m+m Label Management with Package Management** connects the two modules **m+m Label Management** (label and barcode printing) and **m+m Package Management** (packaging administration) in Microsoft Dynamics 365 Business Central. It is a pure integration extension: it does not add any cards, lists or documents of its own, but instead extends existing pages of the two base modules with a few additional fields and ensures that **package information is automatically carried over onto labels and into barcodes**.

The benefit for the user: When printing labels from a warehouse or document process, the package details (for example **Package No.**, **Package Code**, **Package Group No.** or the **Quantity in Package**) no longer have to be entered manually. They are determined from the package data of the document and output at the position defined in the label layout. In addition, a **Label Type Code** can be defined per package, which is inherited when the document packages are created.

**Target audience.** This guide is aimed primarily at **operational users** who create packages and print labels in day-to-day business – for example in goods receipt, goods shipment, picking or packing. Secondarily, it addresses **administrators and key users** who set up the label types and their fields in the **m+m Label Management** module and maintain the package master data (package references and package BOMs) in **m+m Package Management**.

**Prerequisite.** This app requires the base modules **m+m Label Management** and **m+m Package Management** as well as **m+m Cloud Base** to be installed and configured. The setup of label types, reports, barcodes and default values is carried out entirely in the **m+m Label Management** module; the creation of packages, package references and package BOMs in the **m+m Package Management** module. This guide describes exclusively the **additional fields and the automatic linkage** that are provided by the integration app.

### Process overview

1. **Setup (administrator):** In the fields of a label type or a barcode field, the new **Package Field** field defines which package information is to be printed.
2. **Master data (key user):** In the **Package BOM** and in the **Package References**, a **Label Type Code** is stored per package.
3. **Daily work (user):** When the document packages are created (for example from a package BOM or a package reference), the **Label Type Code** is automatically carried over onto the document package.
4. **Output:** When labels are printed for a warehouse, sales or purchase document, the configured **Package Field** values are determined per package and output on the label or barcode.

## Quick start for users

The fastest route to a printed label with package details – in order of dependencies:

1. **Check the setup (one-time, administrator).** Use the search function (**Tell me what you want to do**) to open the **Label Type Fields** page. In the required line, set the **Package Field** field to the package information that is to be printed (for example **Package No.**). For a field of type **Barcode**, use the **Label Barcode Fields** page instead, and there likewise the **Package Field** field.
2. **Store the label type on the package (key user).** In the **Package BOM** (or in the **Package References**), enter the appropriate label type in the **Label Type Code** field.
3. **Create document packages (user).** In the document process, create the packages as usual from the package BOM or package reference. The **Label Type Code** is automatically carried over onto the respective document package.
4. **Print the label (user).** Trigger the label print in the usual warehouse/document process. The app determines the values configured under **Package Field** per package and outputs them on the label or barcode. Check the result in the label preview of the base module.

**Important:** Package values are only printed if the corresponding package fields are also maintained in the process. If the package data is missing, the label position remains empty.

## Setup

The actual label setup (label types, reports, barcodes, default values, barcode separators) is carried out entirely in the **m+m Label Management** base module and is documented there. The integration app adds **one** field to each of **two** setup pages: **Package Field**. Through this field, the administrator controls which package information appears at the respective field position during printing.

Both pages are company-wide setup pages of the label module and are opened – as is usual in the base module – via the Business Central search function (**Tell me what you want to do**). They are assigned to a label type; the lines maintained there determine which fields are written to the label or into the barcode, and in which order.

### Setting up the Package Field on a label type

**Process entry.** This setup is carried out once by the **administrator** before users print labels with package details. It adds a package source to the field list of a label type. The selection made here is later evaluated automatically during day-to-day label printing (section **Warehouse, documents and label printing**).

**Entry point:** Use **Tell me what you want to do** to open the **Label Type Fields** page.

On the **Label Type Fields** page, the administrator maintains one or more field lines per label type and label process. These lines originate from the base module; the integration app adds the **Package Field** field in the same line. The user sees a single page with base and extension fields.

| Field | Explanation |
|------|-------------|
| **Label Type Code** | Assigns the line to a label type. If set, the field configuration applies to all labels of this type. |
| **Label Process** | Assigns the line to a label process (for example goods receipt, goods shipment). If set, the line is only evaluated in this process. |
| **Report Field Type** | Defines whether the field is a text field or a **Barcode** field. If **Barcode** is selected, the **Package Field** field is disabled at this position; the package source for barcodes is maintained instead on the **Label Barcode Fields** page. |
| **Table No.** / **Field No.** | Source table and field from which the default value is read. If a table/field is set, the base module prints this field value. |
| **Custom Value** | Fixed text value that is printed instead of a table field. If filled, it takes precedence: when **Package Field** is set, an existing **Custom Value** is removed so that the package source and the free text do not overlap. |
| **Package Field** | Controls which package information is printed onto the label. If a value other than **(blank)** is set, the app determines the corresponding package value per package during printing and writes it at this field position. When the value is changed, dependent table/field references or an existing **Custom Value** are cleared after a confirmation prompt, so that exactly one source is active per line. |

**Values of the "Package Field" field (task-relevant):**

- **(blank):** No package value is output; the line behaves as in the base module (table field or **Custom Value**).
- **Package No.:** During printing, the package number of the respective document package is output.
- **Package Code:** During printing, the package code of the document package is output.
- **Quantity in Package:** During printing, the quantity to be handled of the document package (field **Qty. to Handle**) is output as a quantity value.
- **Package Group No.:** During printing, the package group number of the document package is output (grouping of several packages into one group).

**Procedure.**
1. **First**, select the line of the required label type and process (fields **Label Type Code** / **Label Process**).
2. **Then**, set **Package Field** in this line to the required package source.
3. **Finally**, the user checks in the label preview of the base module at which position the package value appears.

**Dependency note.** The **Package Field** field is locked as soon as the **Report Field Type** has the value **Barcode** – for barcodes, use the **Label Barcode Fields** page (see below). If a **Custom Value** is entered, the system removes a previously set **Package Field** value after a confirmation prompt, and vice versa; this ensures that exactly one value source remains effective per field line.

### Setting up the Package Field in a barcode field

**Process entry.** This setup is carried out by the **administrator** when a piece of package information is to be printed not as plain text but **within a barcode**. A barcode is composed of several barcode fields; each field can have its own source. The selection made here is inserted into the assembled barcode content during label printing (section **Warehouse, documents and label printing**).

**Entry point:** Use **Tell me what you want to do** to open the **Label Barcode Fields** page.

This page too originates from the base module; the integration app adds the **Package Field** field in the same line.

| Field | Explanation |
|------|-------------|
| **Label Type Code** | Assigns the barcode field to a label type. If set, the barcode is generated for labels of this type. |
| **Label Process** | Assigns the barcode field to a label process. If set, the field is only evaluated in this process. |
| **Table No.** / **Field No.** | Source table and field for the barcode component. If set, this field value is included in the barcode. |
| **Custom Value** | Fixed text component of the barcode. If filled, the previously set package value is removed when **Package Field** is set, so that the barcode component is unambiguous. |
| **Package Field** | Controls which package information is written as a component into the barcode. If a value other than **(blank)** is set, the app appends the determined package value to the barcode content during printing; the components are joined with the separator of the barcode type and then encoded as a barcode. |

**Values of the "Package Field" field in the barcode:**

- **(blank):** No package value is included in the barcode.
- **Package No.:** The package number is included as a barcode component.
- **Package Code:** The package code is included as a barcode component.
- **Quantity in Package:** The quantity to be handled (**Qty. to Handle**) is included as a barcode component.
- **Package Group No.:** The package group number is included as a barcode component.

**Dependency note.** If the source table (**Table No.**) or the **Custom Value** is changed in the line, the system automatically resets the previously set **Package Field** value. This ensures it is always unambiguous per barcode component whether it originates from a table field, free text or a package source.

## Master data

In addition to the setup fields, the integration app adds the **Label Type Code** field to two **package master data pages** of the m+m Package Management module. This field defines which label type applies later to the document packages created from this package. The **Label Type Code** each refers to a label type maintained in the m+m Label Management module (page **Label Types**).

### Storing the label type in the Package BOM

**Process entry.** This master data is maintained by the **key user** when building the package BOMs – that is, before packages are created from a BOM in day-to-day business. The **Label Type Code** maintained here determines which label type is carried over when the document packages are created from this BOM (see **Daily work**).

**Entry point:** Use **Tell me what you want to do** to open the **Package BOM** and select the required BOM; the positions are displayed in the **Package BOM Lines** subform.

The package BOM (page **Package BOM**) has a header with **Status** and a lines subform. The integration app adds the **Label Type Code** column in the lines.

| Field | Explanation |
|------|-------------|
| **Package Code** | Identifies the package position of the line (from the base module). |
| **Line Type** | Distinguishes package and item lines. **Package:** the line describes a package – only here can the **Label Type Code** be maintained. **Item:** the line describes an item contained in the package – the **Label Type Code** is not entered here directly, but is derived automatically from the parent package. |
| **Description** / **Quantity** | Description and quantity of the line (from the base module). |
| **Label Type Code** | If a label type is set in a package line, then all **item lines** of the same package automatically adopt the same **Label Type Code**; when the document packages are created later, this label type is carried along. The field is only editable if the **Line Type** has the value **Package**. |

**Procedure.**
1. **First**, open the required **Package BOM**. As long as its **Status** has the value **Open**, the lines are editable.
2. **Then**, enter the **Label Type Code** in the package line (**Line Type** = **Package**). The contained item lines receive the code automatically.
3. **Finally**, set the **Status** of the BOM to **Released** if required; released BOMs are no longer editable.

**Validation note.** The **Label Type Code** is checked against the label types (page **Label Types**); only codes created there are permitted.

### Storing the label type in the Package References

**Process entry.** This master data is maintained by the **key user** in the **Package References** – the rules that assign a default package to an item, customer or vendor. The **Label Type Code** maintained here is carried over when the document packages are created from a reference (see **Daily work**). The package references are opened in the m+m Package Management module via the **Package References** action on the respective master cards (for example the item or vendor card).

**Entry point:** On the respective master card, open the **Package References** action; the **Package References** page opens.

The integration app adds the **Label Type Code** column to this page.

| Field | Explanation |
|------|-------------|
| **Package Reference No.** | Unique number of the reference rule (from the base module). |
| **Product Type** / **Item No.** | Define for which item or item group the reference applies. |
| **Reference Type** / **Reference No.** | Define for which business partner (for example customer, vendor) the reference applies. |
| **Package Type** | Type of the reference source. If the value is **Package BOM**, **no** **Label Type Code** may be set here – in this case the label type is maintained in the **Package BOM** (see validation note). For other values (for example **Package Category**), direct maintenance of the label type is permitted. |
| **Package No.** / **Quantity per Package** | Specific package and conversion quantity of the reference (from the base module). |
| **Label Type Code** | If set, the stored label type is carried over onto the document package when the document packages are created from this reference. |

**Procedure.**
1. **First**, open the required reference via the **Package References** action.
2. **Then**, check the **Package Type**: For **Package BOM**, maintain the label type in the BOM; otherwise enter the **Label Type Code** directly in the reference line.
3. **Finally**, the label type is automatically available the next time document packages are created from this reference.

**Validation note.** If the user sets a **Label Type Code** in a reference with **Package Type** = **Package BOM**, the system reports: *"You must define Label Type Code in Package BoM!"* and prevents the entry. In this case the label type belongs in the **Package BOM**, so that it is correctly inherited per package position when the BOM is resolved.

## Daily work: creating packages and inheriting the label type

In day-to-day business, the user creates **document packages** from the master data – either from a **Package BOM** or from a **Package Reference**. The integration app automatically steps in and transfers the **Label Type Code** maintained in the master data onto the respective document package. The user does **not** have to enter the label type again in the document.

This behaviour is controlled by the setup and the master data from the previous chapters: The **Label Type Code** originates from the **Package BOM** or **Package References** (see **Master data**), and **what** is printed later is determined by the **Package Field** field on **Label Type Fields** or **Label Barcode Fields** (see **Setup**).

**Inheritance paths (automatic, without any additional action by the user):**

- **From the Package BOM:** When the document packages are created from a package BOM, the **Label Type Code** maintained in the package line is carried over onto the created document package.
- **From a Package Reference:** When the document packages are created from a package reference, the **Label Type Code** maintained there is carried over onto the document package.
- **From the sales line:** When the document packages are populated from a sales line, a **Label Type Code** kept on the sales line is carried along and transferred onto the document package.

**Line update.** In the **Package BOM Lines** (page **Package BOM**), the system updates the display immediately as soon as a **Label Type Code** is changed in a package line, so that the inherited values in the item lines are visible right away.

## Warehouse, documents and label printing

The actual **label printing** is triggered in the usual warehouse or document process of the base module. During printing, the integration app automatically establishes the link between the document, its packages and the label fields and determines the values configured under **Package Field** per package.

### Supported documents and processes

When resolving the packages for printing, the app determines the source document based on the document type of the document package. The following are supported:

| Document type of the document package | Determined source document |
|-------------------------------|------------------------|
| **Warehouse Receipt** (label process) | Warehouse receipt header and line – for purchase order, sales return order and inbound transfer. |
| **Warehouse Shipment** (label process) | Warehouse shipment header and line – for sales order, purchase return order and outbound transfer. |
| **Sales Order** | Sales header and line (order). |
| **Sales Return Order** | Sales header and line (return order). |
| **Purchase Order** | Purchase header and line (order). |
| **Purchase Return Order** | Purchase header and line (return order). |
| **Transfer (inbound/outbound)** | Transfer header and line. |
| **Item Journal** | Item journal line. |

If no matching source document is found, the app skips the package; no package values are then written onto the label.

### Sequence of label printing with package values

1. **First**, the app determines all document packages assigned to the printed document.
2. **Then**, it determines the source document per package (see table above).
3. **Next**, the values are set for each label field line: table field, **Custom Value** or – if **Package Field** is set – the determined package value (**Package No.**, **Package Code**, **Quantity in Package** or **Package Group No.**).
4. **For barcode fields**, the components – including the set **Package Field** values – are joined with the separator of the barcode type and encoded as a barcode.
5. **Finally**, the label is generated as in the base module or displayed in the preview.

**Prerequisite for output:** The package fields must be maintained in the process. If they are missing, the corresponding label or barcode position remains empty.

## FAQ and troubleshooting

### 1. Why does no package information appear on the label even though I have configured a Package Field?

Values are only output if the package data is also maintained in the process and document packages are assigned to the document. If the package details are missing or the app does not find a matching source document for the document type, the label position remains empty.

### 2. Why can I not select the Package Field in a line?

On the **Label Type Fields** page, the **Package Field** field is disabled as soon as the **Report Field Type** has the value **Barcode**. For barcodes, maintain the package source on the **Label Barcode Fields** page.

### 3. Why is my Custom Value deleted when I set a Package Field?

Only one value source may be active per field line. If you set a **Package Field**, the system removes an existing **Custom Value** after a confirmation prompt (and vice versa), so that free text and package source do not overlap.

### 4. Why do I get the message "You must define Label Type Code in Package BoM!"?

This message appears when you enter a **Label Type Code** in a **Package Reference** with **Package Type** = **Package BOM**. In this case the label type belongs in the **Package BOM**, not in the reference, so that it is correctly inherited per package position.

### 5. Why can I not enter a Label Type Code in an item line of the Package BOM?

The **Label Type Code** is only editable in lines with **Line Type** = **Package**. Item lines receive the code automatically from their parent package.

### 6. Where does the label type on my document package come from?

It is inherited automatically when the document packages are created: from the **Package BOM**, from a **Package Reference** or from a sales line. Manual entry on the document package is not required.

### 7. Which package values can I print on a label?

Via **Package Field**, the values **Package No.**, **Package Code**, **Quantity in Package** and **Package Group No.** are available. **Quantity in Package** outputs the quantity to be handled (**Qty. to Handle**) of the document package.

### 8. Why does my Label Type Code in the Package BOM not change immediately in the item lines?

Inheritance onto the item lines occurs when the **Label Type Code** is validated in the package line; the line display is updated immediately in the process. Check whether you entered the value in a package line (not in an item line).

### 9. Can I include package information in a barcode?

Yes. In the required line on the **Label Barcode Fields** page, set the **Package Field** field. The value is included as a component in the barcode during printing and joined with the remaining components using the separator of the barcode type.

### 10. Do I have to set up the app separately, or are the base modules sufficient?

The app requires the base modules **m+m Label Management** and **m+m Package Management** to be set up. In addition, you only maintain the new fields: **Package Field** on **Label Type Fields** or **Label Barcode Fields** and **Label Type Code** in **Package BOM** or **Package References**. No further setup steps arise from this app.

## Typical use cases

### Use case 1: Printing the package number on the shipping label

**Trigger.** A sales order is to be shipped; the package number should be visible on the package label so that shipping can uniquely assign each package.

**Entry point in BC.** The administrator opens the **Label Type Fields** page once via **Tell me what you want to do** and, in the line of the shipping label type (label process **Warehouse Shipment**), sets the **Package Field** field to **Package No.**.

**Core process.**
1. The key user stores the appropriate **Label Type Code** in the relevant **Package Reference** or **Package BOM**.
2. In the warehouse shipment process for the sales order, the user creates the document packages; the **Label Type Code** is carried over automatically.
3. During label printing, the app determines the **Package No.** per package and prints it at the configured position.

**Conclusion.** The user checks the label preview of the base module and prints the labels; each package bears its package number.

### Use case 2: Package quantity in goods receipt as a barcode

**Trigger.** During the warehouse receipt of a purchase order, the quantity per package is to be captured as a barcode in order to speed up the subsequent put-away.

**Entry point in BC.** The administrator opens the **Label Barcode Fields** page via **Tell me what you want to do** and, in the line of the goods receipt label type (label process **Warehouse Receipt**), sets the **Package Field** field to **Quantity in Package**.

**Core process.**
1. The key user ensures that the affected packages have a valid **Label Type Code** via the **Package BOM** or **Package Reference**.
2. In the warehouse receipt process for the purchase order, the document packages are created; the label type is inherited.
3. During printing, the app inserts the **Quantity in Package** (value from **Qty. to Handle**) as a component into the barcode and encodes it.

**Conclusion.** The printed barcode contains the package quantity and can be scanned during put-away.

### Use case 3: Centrally controlling the label type via the Package BOM

**Trigger.** For a multi-level package BOM (pallet with cartons), the correct label type should apply automatically per package level, without maintaining the item lines individually.

**Entry point in BC.** The key user opens the **Package BOM** via **Tell me what you want to do** and selects the relevant BOM (**Status** = **Open**).

**Core process.**
1. In the package line (**Line Type** = **Package**), the key user enters the **Label Type Code**.
2. All item lines of this package adopt the code automatically; the display is updated immediately.
3. The key user sets the **Status** of the BOM to **Released** if required.

**Conclusion.** When the document packages are created from this BOM, all levels carry the correct label type; the subsequent label print uses the **Package Field** values configured per label type.
