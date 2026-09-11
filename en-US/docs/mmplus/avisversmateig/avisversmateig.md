---
title: Anwenderhandbuch m+m Logistic Management with Material Properties
---

# User Guide m+m Logistic Management with Material Properties

## Introduction

The **m+m Logistic Management with Material Properties** extension connects two existing m+m modules with each other: logistic **Advice Notification** (shipment and goods-receipt planning) and **Material Properties** (properties per lot, item and material type). It adds an InfoBox to the **Item Tracking Assignment Lines** page that displays the **material properties of the selected lot** and – if desired – lets you edit them directly.

The business benefit: while a user assigns lots to an advice-notification line, they can see without switching pages which properties (e.g. test values, dimensions, quality characteristics) are stored on the respective lot. This makes it possible to select the correct lot based on its material properties instead of looking at the lot number in isolation.

**Target audience:** primarily **operational users** in goods receipt, shipping and logistics who process advice notifications every day and assign lots to the lines. Secondarily **administrators and master-data owners** who set up the material properties and assign a material type to the items, so that properties are available on the lots in the first place.

**Short process overview:** the administrator activates the **Material Property Setup**, creates **Material Types** with **properties** and assigns a material type to the items via the **Material Type Code**. Once lots receive properties in this way, the InfoBox then displays these in the **Item Tracking Assignment Lines** dialog as soon as a user selects a lot there.

This extension itself has **no setup or master-data page of its own**. It uses the pages of the m+m Logistic Management and m+m Material Properties modules. So that the user can fully configure and operate the page, the associated prerequisites are documented alongside in this handbook.

## Quick Start for Users

The quick start follows the dependency order: first the one-time setup, then the master data, and afterwards the daily work in the document.

1. **Check prerequisite (one-time, administrator):** In the **Material Property Setup** page, material property management is activated. If the setup is missing, no properties are available on the lots and the InfoBox stays empty.
2. **Create material type and properties (master data, administrator):** In **Material Types**, create a material type and, via the **Material Type Card**, assign it the desired **properties**.
3. **Set material type on the item (master data):** On the **Item Card**, store the material type in the **Material Type Code** field. When it is set, the lots of this item inherit the properties of the material type.
4. **Open document (daily work):** Open the **Advice Notification** and, in the line, call the assignment dialog via the action **Line → Item Tracking Assignment Lines**.
5. **Assign lot:** Via **Select &Entries** or **Assign Lot No.**, set the **Lot No.** and enter the **Qty. to Assign**.
6. **Read/edit properties:** The **Properties** InfoBox shows the material properties of the lot for the marked line. If needed, change the **Value** directly in the InfoBox.
7. **Finish:** Close the dialog with **OK**. The assignment is saved; changed property values are applied to the lot (Lot No. Information).

## Setup

Since the extension does not bring its own setup page, the setup is limited to **one prerequisite** from the m+m Material Properties module, which must be active for the InfoBox to display data.

### Set up material properties for item tracking

**Process intro:** The **administrator** performs this setup once **before first use**. It is the basis for the InfoBox in the **Item Tracking Assignment Lines** page (see chapter *Daily Work*) displaying properties for the lot at all. The chain runs from the central setup through the master data to the user's action in the document.

**Entry point:** Open the **Material Property Setup** page via **Search** (this is a company-wide setup page without a superordinate document page).

**Numbered setup steps (in dependency order):**

1. **First**, activate material property management in the **Material Property Setup** page. If the setup exists and is active, then the properties of lots are maintained when lots are created and updated, and are later available in the InfoBox; without an active setup, the InfoBox stays empty.
2. **Then** create the **Material Types** and assign each material type its **properties** via the **Material Type Card** (see chapter *Master Data*). If a material type has properties, then items and lots of this material type inherit exactly these properties.
3. **Next**, set the **Material Type Code** on the **Item Card** (see chapter *Master Data*). If an item carries a material type, then the appropriate property lines are generated for its lots.
4. **Finally**, in the daily routine, the user opens the **Item Tracking Assignment Lines** and selects a lot line. If a lot is marked, then the **Properties** InfoBox displays the material properties of exactly this lot (operational closing of the chain; see chapter *Daily Work*).

| Setup | Explanation |
|---|---|
| **Material Property Setup** (company-wide, one-time) | If this setup is active, then material properties are maintained company-wide and displayed in downstream pages – including the InfoBox of the item tracking assignment; if it is missing, then no properties are available to the user in the assignment page. |

**Dependency note:** The InfoBox only shows properties if the lot has received properties via the chain above. If the **Material Type Code** is missing on an item, the InfoBox stays empty for its lots.

For this extension, only the **activation** of material property management is decisive as a prerequisite. You carry out the detailed field maintenance of material types and properties in the master data (see the following chapter).

## Master Data

The master data relevant for the InfoBox is maintained in the m+m Material Properties module. Two master-data surfaces control which properties the user later sees in the assignment page.

### Material Types and Properties

**Process intro:** The **master-data owner** creates material types **before first use** and assigns properties to them. The properties maintained here form the template that is later inherited by items and lots and appears in the InfoBox of the **Item Tracking Assignment Lines** page.

**Entry point:** Open the **Material Types** list; select a line and open the **Material Type Card** via the action. There you maintain the assigned **properties**.

| Field | Explanation |
|---|---|
| **Property Code** | If you assign a property code to a material type, then this property is subsequently available on all items and lots of this material type and is displayed as a line in the InfoBox. |
| **Property Name** | If a property name is maintained, then this plain text appears as the label of the property line in the InfoBox, so that the user recognizes the property without knowing the code. |
| **Standard Value** | If you store a standard value, then this value is applied as a suggestion as long as no differing value is recorded on the specific lot; if the lot's value differs from the standard value, the InfoBox highlights the value in color. |
| **Unit** | If a unit is maintained, then the property value is interpreted and displayed in the InfoBox with this unit of measure, so that the user classifies values correctly in business terms. |
| **Display Order** | If you assign a display order, then the properties are sorted in the InfoBox in exactly this order; this way the most important characteristics are at the top. |

**Validation note:** Only properties that are assigned to a material type are inherited by its items and lots. Without an assignment, the system does not create a property line for the lot.

### Material Type on the Item (Item Card)

**Process intro:** The **master-data owner** links every relevant item to a material type. Only this link ensures that the item's lots receive properties, which the user sees in the assignment page.

**Entry point:** Open the item list and, within it, the **Item Card** of the item.

| Field | Explanation |
|---|---|
| **Material Type Code** | If you set a material type code on the item, then the lots of this item take over the properties of the assigned material type and the InfoBox of the item tracking assignment displays them; if the field stays empty, then the item has no material properties and the InfoBox stays empty for its lots. |

**Cross-reference:** The user consumes the material type set here in the chapter *Daily Work* – the InfoBox in the **Item Tracking Assignment Lines** page accesses exactly these properties.

## Daily Work: Lot Assignment with Material Properties

This is the core function of the extension. The **Item Tracking Assignment Lines** page is a modal dialog that the user opens from a logistics document in order to assign lots or serial numbers to the document lines. The extension adds the **Properties** InfoBox to this dialog.

**Controlling setup/master data:** Which properties the InfoBox displays is not configured in this dialog, but via the pages **Material Property Setup**, **Material Types**/**Material Type Card** and the **Material Type Code** field on the **Item Card** (see chapters *Setup* and *Master Data*). If no property is stored on the lot, the InfoBox stays empty.

### Entering the Page

**Entry point:** Open the **Advice Notification** (document). Mark the relevant line in the document lines and open the modal assignment dialog via the action **Line → Item Tracking Assignment Lines**. The page is not a menu item that can be called via **Search**; it is opened exclusively from the document line.

### Header Area of the Page

| Field | Explanation |
|---|---|
| **Quantity to Assign:** | Shows the total quantity that must be assigned to the document line. If this value is greater than the quantity already assigned, then lots still have to be recorded. |
| **Quantity Assigned:** | Shows the sum of the quantities already assigned via lot lines. If this value equals the quantity to assign, then the line is fully assigned. |
| **Undefined Quantity:** | Shows the remaining quantity not yet assigned (quantity to assign minus quantity already assigned). If a non-zero value stands here, then a lot assignment is still missing; the system does not allow an assignment beyond the undefined quantity. |

### Line Area of the Page

| Field | Explanation |
|---|---|
| **Lot No.** | If you enter a lot no. or assign it via the selection, then the quantity of this line is assigned to this lot and the InfoBox shows the properties of exactly this lot; the field is only editable if the item is lot-tracked. |
| **Serial No.** | If you record a serial no., then the assignment is related to this serial number; the field is only editable if the item is serial-number-tracked. |
| **Qty. to Assign** | If you enter a quantity here, then the already assigned and the undefined quantity in the header are recalculated immediately; the entry may not exceed the undefined quantity. |

### Actions of the Page

| Action Name | Explanation |
|---|---|
| **Select &Entries** | If you run this action, then an overview of the available lots or serial numbers with their assignable quantities opens; the entries chosen there are taken over as lines into the assignment. |
| **Assign Lot No.** | If you run this action, then the system assigns a lot no. to the current or the selected lines based on the item's lot number series; the InfoBox subsequently shows the properties of the newly assigned lot. |
| **Line → Lot No. Information Card** | If you run this action, then the Lot No. Information Card for the marked lot opens; there you view and maintain central lot information. The action requires a recorded lot no. |
| **Line → Serial No. Information Card** | If you run this action, then the Serial No. Information Card for the marked serial number opens. The action requires a recorded serial no. |

### "Properties" InfoBox (Material Properties of the Lot)

The InfoBox is the actual addition of this extension. It stands to the left or right of the assignment lines and refreshes as soon as the user marks a different lot line. It shows the material properties of the lot that is selected in the marked assignment line and is editable.

| Field | Explanation |
|---|---|
| **Property Name** | Shows the label of the property (e.g. a quality or dimension characteristic) of the lot. If several properties are maintained, then one line appears per property. |
| **Value** | Shows the specific property value of the lot. If you change the value, then the change is saved immediately to the lot (Lot No. Information); if the value differs from the standard value, the InfoBox highlights it in color. The field is editable because the extension embeds the InfoBox as editable. |
| **Standard Value** | Shows the default value stored in the material type. If no own value is recorded on the lot, then the standard value serves as orientation; this field appears when the source is a material type. |
| **Unit** | Shows the unit of measure of the property. If a unit is maintained, then the user classifies the value correctly in business terms (e.g. mm, kg, percent). |
| **Display Order** | Shows or controls the sorting of the property lines. If a display order is assigned, then the properties appear in this order. |

**Hidden fields:** The InfoBox technically carries additional fields (**Property Value Name**, **Category Code** as well as a category description) that are **not visible** by default. They serve the internal linking of property values and categories and are not required for the daily assignment; the user does not have to maintain them.

**Completion:** Once all lines are assigned (undefined quantity = 0) and the properties have been checked or corrected, close the dialog with **OK**. The assignment is saved and is available to the advice notification for further processing.

## FAQ and Troubleshooting

### 1. Why is the "Properties" InfoBox empty even though a lot is assigned?

Because no material properties are stored on the lot. This is the case when the **Material Type Code** is missing on the item or the assigned material type has no properties. Set the material type code on the **Item Card** and assign properties to the **Material Type** via the **Material Type Card**.

### 2. How do I open the "Item Tracking Assignment Lines" page?

Not via **Search**. Open the **Advice Notification**, mark the document line and choose **Line → Item Tracking Assignment Lines**. The dialog is a modal assignment dialog and only reachable from the document line.

### 3. Can I change a property value directly in the assignment dialog?

Yes. The extension embeds the InfoBox as **editable**. Change the **Value** in the InfoBox; the change is saved immediately to the lot (Lot No. Information) and thereafter applies everywhere this lot is used.

### 4. What does the color highlighting of a value in the InfoBox mean?

The value differs from the **Standard Value** of the material type. This way you immediately recognize which lots carry a property value that deviates from the default value.

### 5. Why can't I edit the "Lot No." field?

Because the item is not lot-tracked. The field is only active if the item's item tracking code provides for lot-specific tracking. Analogously, **Serial No.** is only active for serial-number-tracked items.

### 6. Why does the system not allow any further quantity?

Because the **Undefined Quantity** is already zero. In total you can only assign as much as is specified in **Quantity to Assign**. Check the header area: if the undefined quantity is zero, the line is fully assigned.

### 7. How do I assign several lots in one step?

Use the action **Select &Entries**. There you mark several available lots with their quantities and take them over into the assignment together.

### 8. How does a newly created lot get its properties?

Via the material type of the item. As soon as the item carries a **Material Type Code**, the property lines of the material type are generated for its lots; differing values can then be recorded per lot – also directly in the InfoBox.

### 9. In which order do the properties appear in the InfoBox?

In the **Display Order** that is maintained per property in the material type. Adjust the display order in the master data to show the most important characteristics at the top.

### 10. Which prerequisites must be met before first use?

Three steps in dependency order: activate the **Material Property Setup**, create **Material Types** with **properties** and assign the **Material Type Code** to the items. Only after that does the InfoBox in the assignment page display properties.

## Typical Use Cases

### Use Case 1: Checking a lot when advising based on its material properties

**Trigger:** A vendor announces a delivery by e-mail; the user in logistics creates or edits the appropriate **Advice Notification** and has to assign the correct lots to the lines.

**Entry point in BC:** The user opens the **Advice Notification**, marks the relevant document line and calls the assignment dialog via **Line → Item Tracking Assignment Lines**.

**Core flow:**
1. In the assignment line, choose an available **Lot No.** via **Select &Entries** and enter the **Qty. to Assign**.
2. The header updates **Quantity Assigned:** and **Undefined Quantity:**.
3. The user marks the lot line; the **Properties** InfoBox shows **Property Name**, **Value** and **Unit** of the lot.
4. Based on the displayed properties, the user checks whether the lot matches the requirement; if it does not match, they choose a different lot via **Select &Entries**.
5. Once all quantities are assigned (undefined quantity = 0), the user closes the dialog with **OK**.

**Completion:** The lot assignment is saved and is ready for the advice notification for further processing.

### Use Case 2: Correcting a property value of a lot directly in the assignment dialog

**Trigger:** An internal notification states that a test value of a specific lot has to be added or corrected while the lot is being advised.

**Entry point in BC:** As in Use Case 1, the user opens the **Item Tracking Assignment Lines** from the **Advice Notification**.

**Core flow:**
1. The user marks the line with the relevant **Lot No.**
2. In the **Properties** InfoBox, they change the relevant property value in the **Value** field.
3. If the new value differs from the **Standard Value** of the material type, the InfoBox highlights it in color.
4. If needed, the user opens the Lot No. Information Card via **Line → Lot No. Information Card** to check further lot information.

**Completion:** The user closes the dialog with **OK**. The corrected property value is saved to the lot and applies from now on everywhere this lot is used.
