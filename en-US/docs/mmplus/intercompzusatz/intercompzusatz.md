---
title: Anwenderhandbuch m+m Ext. Production Information with Intercompany
---

# User Guide m+m Ext. Production Information with Intercompany

## Introduction

The **m+m Ext. Production Information with Intercompany** extension connects the material tracking from the production information with the cross-company document exchange of **m+m Intercompany**. It ensures that the lot and serial information assigned to a purchase document (the **Material Tracking Entries**) is also transferred when a sales order is automatically created in the partner company. In addition, it enables the buyer to select a **Lot** directly from the inventory of the **IC Partner**.

**Target audience:** Primarily these are **operational users in Purchasing** who process purchase orders with an intercompany reference and maintain the material tracking in the process. Secondarily, the extension concerns users in **Sales** of the partner company, in whose sales order the transferred material tracking entries appear, as well as administrators who set up the intercompany document exchange.

**Brief process overview:** In a **Purchase Order** intended for intercompany dispatch, the user opens the **Material Tracking Entries** from the item line. If the document is flagged for IC dispatch (**Send IC Document**) and is in **IC Status** **New**, the user can assign a lot from the partner company via the **Select Lot No. from IC Partner** action. When the intercompany process subsequently creates the corresponding **Sales Order** in the partner company, the recorded material tracking entries are automatically copied into the matching **Sales Line**. This keeps the lot and serial assignment consistent across both companies without having to record it twice.

This extension provides **no** setup pages, master data, or reports of its own. It supplements existing documents with two actions and with an automatic transfer that runs in the background. The necessary basic settings come from the underlying modules **m+m Intercompany** and **m+m Ext. Production Information**.

## Quick Start for Users

The fast route from the purchase order to cross-company consistent material tracking:

1. **Check prerequisites (one-time, by the administration):** The **IC Partner** is set up in **m+m Intercompany**, and the document exchange is active. See section **Prerequisites and Setup**.
2. **Open the purchase order:** Open the relevant **Purchase Order** and make sure that the header is intended for intercompany dispatch (**Send IC Document** enabled) and has **IC Status** **New**.
3. **Select the item line:** In the **Lines**, select the desired **Purchase Line** of type Item.
4. **Open the Material Tracking Entries:** In the line actions, choose **Material Tracking Entries**. The page is editable as long as the document is in **IC Status** **New**.
5. **Select the lot from the IC Partner:** On the **Material Tracking Entries** page, choose the **Select Lot No. from IC Partner** action and, in the following selection dialog, assign the **Lot No.** (and, if applicable, **Serial No.**) up to the outstanding quantity of the line.
6. **Run the intercompany process (via m+m Intercompany):** As soon as the intercompany process creates the **Sales Order** in the partner company, the assigned **Material Tracking Entries** are automatically copied into the matching **Sales Line** — no further recording step is necessary.

There is **no** posting, release, or finish action in this extension. The only actively triggered step is the lot assignment (step 5); the transfer to the partner company (step 6) runs automatically.

## Prerequisites and Setup

This extension has **no setup page of its own**. The function is activated exclusively via already existing flags of the base and dependency modules. The following overview formally describes which preconditions must be met so that the two actions are available and the automatic transfer takes effect.

### Setting up the prerequisites for the lot selection from the IC Partner

**Process intro:** This preparation is carried out by the **administration** or the key user **before first use**. It defines under which conditions a user in Purchasing may assign a **Lot** from the **IC Partner** and when the assigned entries are transferred into the partner **Sales Order**. The setting is later applied in section **Material Tracking Entries on the Purchase Document**.

Perform the steps in dependency order:

1. **Set up the IC Partner in the m+m Intercompany module.** First, set up the **IC Partner** and the intercompany document exchange in the **m+m Intercompany** module. When the IC Partner including outbox/inbox details is stored, then the extension can determine the associated partner company and access its data when creating the sales order. Without a configured IC Partner, no transfer takes place.
2. **Flag the purchase order for IC dispatch (Send IC Document).** In the header of the **Purchase Order**, set the **Send IC Document** flag. When **Send IC Document** is enabled, then the **Select Lot No. from IC Partner** action on the **Material Tracking Entries** page is unlocked; if the flag is not set, the action remains disabled, because without IC dispatch no partner lot can be assigned.
3. **Keep the IC Status New.** Make sure that the document has **IC Status** **New** while the material tracking is being maintained. When the **IC Status** is **New**, then the **Material Tracking Entries** page is editable and assignments are possible; if the document leaves this status, the page becomes read-only so that assignments that have already been transferred or are being processed cannot be changed afterwards.
4. **Operational conclusion in the daily workflow.** The chain ends with the user action **Select Lot No. from IC Partner** in the **Material Tracking Entries** (see section **Material Tracking Entries on the Purchase Document**). The subsequent transfer into the partner sales order happens automatically (see **Intercompany Transfer of the Material Tracking**).

This single configuration chain controls both capabilities of the extension — the manual lot selection and the automatic transfer. Both rely on the same configured IC Partner and the same IC document; a separate second setup is not required.

### Permissions

**Process intro:** The administration assigns the extension's permission set to the users **before first use** so that the underlying logic is allowed to run.

The **MuM INAP Permission** permission set determines the execution permissions for the extension's program logic. It defines which actions the users can perform in connection with the intercompany material tracking by permitting the execution of the two associated codeunits. When this set is assigned to a user, then that user can use the **Select Lot No. from IC Partner** action, and the automatic transfer into the partner company is executed for their transactions; without this set, the extension's logic is not available.

## Material Tracking Entries on the Purchase Document

**Controlling settings:** This transactional area is controlled by flags in the header of the **Purchase Order** that are maintained in **m+m Intercompany**: **Send IC Document** (unlocks the lot selection) and **IC Status** (controls the editability). How these flags are set is described in the section **Setting up the prerequisites for the lot selection from the IC Partner**.

The extension adds an action to the **Purchase Line** of a **Purchase Order** with which the material tracking entries of the line are opened. From there, the lot assignment from the partner company takes place.

### Opening the Material Tracking Entries

**Entry point:** Open the **Purchase Order** → in the **Lines**, select the desired **Purchase Line** → choose the **Material Tracking Entries** action.

The **Material Tracking Entries** action is available in the line actions of the purchase line when the line is an item line with a valid IC Partner item reference (common item no., item, item reference, or vendor item no.). When opening, the extension checks that the line is of type Item. The opened page is **editable** when the document header carries **IC Status** **New**; otherwise it is opened for viewing only.

The **Material Tracking Entries** page shows the following information per assignment:

| Field | Explanation |
|---|---|
| **Entry No.** | Consecutive number of the material tracking entry. When a new entry is created, then the system assigns the number automatically; it serves to uniquely identify the individual lot/serial assignment. |
| **Source Type** | Type of the document from which the entry originates. When the material tracking was opened from a purchase line, then the purchase line is shown here as the source; after the transfer into the partner company, the target entry accordingly references the sales line. |
| **Source No.** | Document number of the source (number of the purchase order or of the sales order). When this value is set, then it uniquely assigns the entry to the specific document. |
| **Source Line No.** | Line number within the source document. When this value is set, then it links the entry to exactly the document line for which the lot was recorded. |
| **Item No.** | Item for which the lot is assigned. When an assignment is made, then the entry adopts the item no. of the purchase line, so that the tracking uniquely applies to the correct item. |
| **Variant Code** | Variant of the item. When the item is managed with variants, then this field ensures that the lot is assigned to the applicable variant and not confused with a different variant. |
| **Lot No.** | Lot assigned from the IC Partner. When a lot no. is entered here, then it is defined which partner lot supplies the line; this value is adopted into the sales order during the intercompany transfer. |
| **Serial No.** | Assigned serial number, if the item is subject to serial numbers. When a serial no. is set, then the tracking is carried out at individual-unit level and is likewise transferred. |
| **Quantity** | Quantity assigned to the lot or serial. When a quantity is recorded, then the still outstanding quantity of the line to be assigned is reduced accordingly; the total of the assignments must not exceed the outstanding quantity of the purchase line. |
| **Location Code** | Location to which the assignment refers. When a location code is set, then it limits the lot assignment to the relevant location so that inventory is distinguished correctly. |

### Select Lot No. from IC Partner

**Entry point:** On the opened **Material Tracking Entries** page, choose the **Select Lot No. from IC Partner** action.

The **Select Lot No. from IC Partner** action is only active when the underlying purchase document carries the **Send IC Document** flag. When the action is executed, then the extension opens the lot selection dialog of the item tracking and offers the still outstanding quantity of the purchase line for assignment. The offered remaining quantity results from the outstanding quantity of the line minus the already assigned quantity.

Assignment sequence:

1. The extension determines the outstanding, not yet assigned quantity of the **Purchase Line**.
2. It opens the selection dialog for the **Lot No.** (for items subject to serial numbers, additionally for the **Serial No.**).
3. The user selects the desired **Lot** from the partner inventory.
4. If the user cancels without a selection (neither **Lot No.** nor **Serial No.** set), then no entry is created.
5. If the selected **Lot** already exists for the same source, same item, same variant, and same location, then the message **"The Lot %1 is already assigned"** appears, and no duplicate entry is created.
6. Otherwise the extension creates a new **Material Tracking Entry** with the selected **Lot No.**, the **Quantity**, and the associated source, item, variant, and location information.

This check ensures that each partner lot is recorded only once per line and location and that the assigned total quantity does not exceed the outstanding quantity of the order.

## Intercompany Transfer of the Material Tracking

**Controlling settings:** The transfer requires an **IC Partner** set up in **m+m Intercompany** and a purchase document intended for IC dispatch (see **Setting up the prerequisites for the lot selection from the IC Partner**).

This process runs **automatically** and requires no separate user action. It takes effect at the moment the intercompany process creates the associated **Sales Lines** in the partner company from the purchase order.

Sequence:

1. The intercompany process of **m+m Intercompany** creates the **Sales Order** and its **Sales Lines** in the partner company.
2. The extension detects this event and, via the **External Document No.** of the sales order and the line number, determines the matching **Purchase Line** in the source company.
3. In the source company, it reads all **Material Tracking Entries** of the purchase line.
4. For each entry found, it creates a corresponding entry in the partner company and references it to the new **Sales Line** (**Source Type** Sales Line, with **Source No.** and **Source Line No.** of the sales order).

The transfer is only performed for documents of type Order and only when a matching purchase line can be determined in the source company. If no matching purchase line is found or the document number is empty, then no entry is copied. This way, the lot and serial data recorded in Purchasing appears in the partner company's sales order without being recorded again.

## Typical Use Cases

### Use case 1: Assign the vendor's lot for an intercompany order

**Trigger:** A buyer receives from the supplying partner company the information about which **Lot** an ordered item comes from and is to record this information on the document.

**Entry point in BC:** The buyer opens the relevant **Purchase Order**. The document header is intended for intercompany dispatch (**Send IC Document** enabled) and is in **IC Status** **New**. In the **Lines**, they select the item line and choose the **Material Tracking Entries** action.

**Core sequence:** On the editable **Material Tracking Entries** page, the buyer chooses the **Select Lot No. from IC Partner** action. In the selection dialog, they assign the **Lot** named by the partner with the **Quantity** to be recorded up to the outstanding quantity of the line. If they try to record the same lot for the same line a second time, the message **"The Lot %1 is already assigned"** points this out. After a successful selection, a new **Material Tracking Entry** appears with **Lot No.**, **Item No.**, **Quantity**, and **Location Code**.

**Conclusion:** The entry remains editable as long as the document has **IC Status** **New**. Further posting or release steps are not required in this extension.

### Use case 2: Lot information reaches the partner sales order automatically

**Trigger:** After Purchasing has maintained the material tracking, the clerk triggers the intercompany process to create the matching **Sales Order** in the supplying company.

**Entry point in BC:** The process requires no manual navigation in this extension. As soon as **m+m Intercompany** creates the **Sales Order** and the **Sales Lines** in the partner company, the transfer is triggered.

**Core sequence:** The extension assigns the newly created **Sales Line** to the original **Purchase Line** via the **External Document No.** and the line number and copies its **Material Tracking Entries** into the partner company. The target entries reference the new sales order with **Source Type**, **Source No.**, and **Source Line No.**.

**Conclusion:** In the partner company, the sales clerk can view the adopted **Material Tracking Entries** on the **Sales Line**. Lots and serial numbers are thereby consistent across both companies without having to be recorded again.

## FAQ and Troubleshooting

### 1. Why is the "Select Lot No. from IC Partner" action greyed out?
The action is only active when the header of the purchase order carries the **Send IC Document** flag. If the document is not intended for intercompany dispatch, the action remains disabled. Set the flag in the document header so that the lot selection is unlocked.

### 2. Why can't I edit the Material Tracking Entries?
The **Material Tracking Entries** page is only editable when the document has **IC Status** **New**. As soon as the document has left this status, the page is opened read-only so that assignments that have already been transferred cannot be changed afterwards.

### 3. What does the message "The Lot %1 is already assigned" mean?
For the same source (purchase line), the same item, the same variant, and the same location, the selected **Lot No.** is already recorded as a material tracking entry. No duplicate entry is created. Select a different lot or correct the existing entry.

### 4. Why is it checked whether the line is an item when opening the Material Tracking Entries?
Material tracking always refers to an item with lot or serial number management. If it is not an item line, no lot can be assigned, and the action aborts with a note about the required line type.

### 5. How much quantity can I assign to a lot?
The still **outstanding quantity** of the purchase line minus the already assigned **quantity** is offered. The total of all assignments can therefore not exceed the outstanding quantity of the line. Partial quantities are permitted; you can record several lots up to the complete allocation of the line.

### 6. Do I have to record the lot again in the partner company's sales order?
No. As soon as the intercompany process creates the **Sales Order** in the partner company, the **Material Tracking Entries** recorded in Purchasing are automatically copied into the matching **Sales Line**. A repeated recording is not necessary.

### 7. Why did no material tracking entries arrive in the sales order?
The transfer only takes place when a matching **Purchase Line** can be determined in the source company. The assignment is made via the **External Document No.** of the sales order and the line number. If the external document number is missing or no matching purchase line exists, no entries are copied.

### 8. For which document type is the transfer performed?
The automatic transfer takes effect for documents of type Order. For other document types, the process is not performed, so that no unexpected entries arise.

### 9. Do I have to post or release after the lot assignment?
No. This extension contains no posting, release, or finish action. The only active step is the assignment of the **Lot**; the adoption into the partner company runs automatically.

### 10. Which permission do I need for the function?
You need the **MuM INAP Permission** permission set. It determines the execution permissions for the extension's program logic and defines which actions you can perform in connection with the intercompany material tracking. Without this set, the function is not available.
