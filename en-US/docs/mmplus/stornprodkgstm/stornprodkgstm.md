---
title: Anwenderhandbuch m+m Undoing Production with Unit Conversion
---

# m+m Undoing Production with Unit Conversion User Guide

## Introduction

The **m+m Undoing Production with Unit Conversion** app is a connector app for **Microsoft Dynamics 365 Business Central**. It links the cancellation of production postings with the KG/Meter/Piece unit conversion. When a user cancels an already posted output or consumption entry in the **Production Journal**, this app ensures that the KG, Meter, and Piece conversion values of the original **Item Ledger Entry** are carried over to the newly created cancellation line in the journal. This keeps the KG/Meter/Piece information consistent even after cancellation and rolls it back properly.

The app itself does **not** add any pages, setup pages, or master data of its own. It works entirely in the background and hooks into the existing cancellation process of the **m+m Undoing Production** app by carrying along the additional quantity fields of the **m+m Unit Conversion** app.

### Target audience

The primary target audience is **operational users in manufacturing** — production control and warehouse staff who record output and consumption postings daily in the **Production Journal** of a released production order and cancel them when necessary. Administrators are only secondarily affected, because the app does not require any setup of its own; their task is limited to installing the required apps (see **Prerequisites**).

### Short process overview

1. A user has posted an output and/or consumption entry in manufacturing. For this posting, the **KG**, **Meter**, and **Piece** values as well as the conversion factors were recorded in the **Item Ledger Entry** via the **m+m Unit Conversion** app.
2. If the user determines that the posting was wrong, they cancel it in the **Production Journal** using the **Cancel Posting** action.
3. Business Central creates new lines in the **Production Journal** for the cancellation (reversal postings). In doing so, this app transfers the conversion values of the original **Item Ledger Entry** to the cancellation lines.
4. The user posts the cancellation lines. As a result, the KG/Meter/Piece values are rolled back correctly.

## Prerequisites

For this app to take effect, the following apps must be installed. Without these apps, neither the cancellation action nor the conversion fields are available in the **Production Journal**.

| Prerequisite | Explanation |
|---------------|-------------|
| **m+m Undoing Production** | Provides the **Cancel Posting** action in the **Production Journal** and the underlying cancellation run. If this app is missing, no production posting can be cancelled and this connector app has no point of attachment. |
| **m+m Unit Conversion** | Provides the conversion fields **KG**, **Meter**, **Piece** as well as the actual and theoretical KG-per-Meter/Piece factors in the **Item Ledger Entry** and in the **Item Journal Line**. If this app is missing, the fields to be transferred do not exist. |
| **m+m Cloud Base** | Base app of the m+m applications; technical foundation, no user-facing operation. |

A dedicated setup of this connector app is not required. There are no number series, no setup page, and no master data that the user has to maintain. Activation happens solely by installing the apps named above.

## Quick start for users

The fastest way to roll back an incorrect production posting, including KG/Meter/Piece values:

1. Open the released **production order** whose posting is to be cancelled, and open the **Production Journal**.
2. In the **Production Journal**, choose the **Cancel Posting** action.
3. In the request dialog, set the desired options: **Correct Consumption** and/or **Correct Output**, plus **Cancel Quantity** per area, or additionally **Cancel Times** for output.
4. Confirm the dialog with **OK**. After a prompt, Business Central first deletes existing journal lines and then opens selection windows with the cancellable **Item Ledger Entries** or capacity ledger entries. Select the lines to be cancelled and confirm with **OK**.
5. Business Central creates new cancellation lines in the **Production Journal**. In doing so, the app transfers the values **KG**, **Meter**, **Piece** as well as the actual and theoretical KG-per-Meter/Piece factors from the selected **Item Ledger Entry** to the new **Item Journal Line**.
6. Check the created lines and run the **Post** function. With the posting, the KG/Meter/Piece values are rolled back correctly.

For consumption cancellation with a **Lot No.** or Serial No., the item tracking of the original posting is carried along automatically; a manual re-entry of the lot is not required.

## Conversion fields in the cancellation

On every cancellation — both for the **output** (finish posting) and for the **consumption** posting — this app transfers exactly the following fields from the original **Item Ledger Entry** to the newly created **Item Journal Line**. The values are set before Business Central validates the quantity of the cancellation line, so that the reversal posting carries the same conversion values as the original posting.

| Field | Explanation |
|------|-------------|
| **KG** | If a KG value was stored in the original item ledger entry, it is carried over to the cancellation line; as a result, the reversal posting posts back the same KG quantity and the KG inventory remains consistent after the cancellation. |
| **Meter** | If a Meter value was stored in the original item ledger entry, it is carried over to the cancellation line; the reversal posting thereby fully rolls back the posted meters. |
| **Piece** | If a Piece value was stored in the original item ledger entry, it is carried over to the cancellation line; the reversal posting thereby cancels the posted piece count consistently with the KG and Meter quantities. |
| **Actual KG per Meter** | If an actual KG-per-Meter factor was stored in the original item ledger entry, it is carried over to the cancellation line; as a result, the reversal posting uses the same actual conversion factor as the original posting and does not create a deviating KG/Meter relation. |
| **Actual KG per Piece** | If an actual KG-per-Piece factor was stored in the original item ledger entry, it is carried over to the cancellation line; the reversal posting thereby rolls back KG and Piece using the same actual factor. |
| **Theoretical KG per Meter** | If a theoretical KG-per-Meter factor was stored in the original item ledger entry, it is carried over to the cancellation line; this keeps the theoretical reference factor of the reversal posting identical to the original posting, and deviations between the actual and theoretical value remain traceable. |
| **Theoretical KG per Piece** | If a theoretical KG-per-Piece factor was stored in the original item ledger entry, it is carried over to the cancellation line; the reversal posting thereby carries along the same theoretical KG-per-Piece factor. |

This field transfer is the entire functional scope of the app. It takes effect exclusively within the cancellation run of the **m+m Undoing Production** app and only when the **m+m Unit Conversion** app provides the fields named above.

## Daily work in the Production Journal

The app has no user interface of its own. The user works entirely in the standard and m+m pages of manufacturing. The relevant entry point is the released **production order** and the **Production Journal** opened from it.

### Entry point: Opening the Production Journal

**Entry point:** From the list or card of the released **production order**, open the **Production Journal** via the associated action. For all KG/Meter/Piece fields to be present in the journal lines, the apps named under **Prerequisites** must be installed.

In the **Production Journal**, the user records consumption and output lines as usual and posts them via the **Post** function. Only when an already posted entry is to be reversed does the cancellation process come into play, into which this app hooks.

### The Cancel Posting action

**Entry point:** In the **Production Journal**, choose the **Cancel Posting** action. This action comes from the **m+m Undoing Production** app and is the only entry point through which the conversion fields of this connector app take effect.

After the action is invoked, a request dialog with the following options opens. The entries determine which posting type is cancelled and whether quantities or times are reversed by a reversal posting.

| Setup | Explanation |
|-------------|-------------|
| **Correct Consumption** | When set, the component consumption postings are offered for cancellation; Business Central then creates reversal posting lines for the consumption and this app transfers the KG/Meter/Piece values of the original consumption item ledger entries to these lines. |
| **Cancel Quantity** (**Consumption** area) | When set, the posted consumption quantities are cancelled by a reversal posting; without this option, the consumption quantity remains unchanged and no consumption cancellation line is created. |
| **Correct Output** | When set, the output (finish posting) of the finished item is offered for cancellation; the resulting reversal posting lines receive the KG/Meter/Piece values of the original output item ledger entry via this app. |
| **Cancel Quantity** (**Output** area) | When set, the posted output quantities are cancelled by a reversal posting; the app carries along the conversion values of the associated item ledger entries. |
| **Cancel Times** (**Output** area) | When set, the posted times of the output are cancelled by a reversal posting from the capacity ledger entries; this time cancellation does not affect any KG/Meter/Piece values, but exclusively the posted capacity times. |

If the user confirms the dialog with **OK**, further selection windows open depending on the options set:

1. On prompt, Business Central first deletes all existing journal lines in the affected journal batch.
2. If quantity cancellation of the **output** is enabled, the selection of the **Item Ledger Entries** (outputs) opens; the user selects individual, none, or all lines. For each selected line, Business Central creates an output reversal posting and this app transfers its KG/Meter/Piece values.
3. If time cancellation is enabled, the selection of the capacity ledger entries opens; here only times are cancelled.
4. If quantity cancellation of the **consumption** is enabled, the selection of the consumption **Item Ledger Entries** opens; for each selected line, Business Central creates a consumption reversal posting and this app transfers its KG/Meter/Piece values.
5. If reservations exist for the selected outputs, Business Central asks before the transfer whether to continue; upon confirmation, the affected reservations are released.

Afterwards, the cancellation lines are in the **Production Journal**. The user checks them and runs the **Post** function to complete the cancellation.

### Item tracking during cancellation

If the original **Item Ledger Entry** carries a **Lot No.** or Serial No., the cancellation run carries this item tracking over to the cancellation line automatically and establishes the application to the original entry. The user does not have to re-enter the lot. The KG/Meter/Piece values of this app are always taken from the same selected item ledger entry, independently of item tracking.

## Typical use cases

The following scenarios show how the app takes effect in the everyday work of manufacturing. All steps correspond to the actual flow in the **Production Journal** and the cancellation run.

### Use case 1: Reversing an incorrect output of a coil production

**Trigger:** A manufacturing employee reports to production control that an output was posted for a production order with the wrong quantity. The item concerned is managed in KG, but is also converted into Meter and Piece.

**Entry point in BC:** Production control opens the released **production order** and opens the **Production Journal** from it.

**Core flow:**
1. Choose the **Cancel Posting** action.
2. In the dialog, set **Correct Output** and, below it, **Cancel Quantity**; **Cancel Times** remains off, because only the quantity was wrong.
3. Confirm the dialog with **OK** and confirm the journal lines to be deleted.
4. In the selection of the **Item Ledger Entries**, mark the incorrectly posted output and take it over with **OK**.
5. Business Central creates the output reversal posting; the app transfers **KG**, **Meter**, **Piece** as well as the actual and theoretical KG-per-Meter/Piece factors from the selected item ledger entry to the cancellation line.

**Completion:** Production control checks the cancellation line and runs **Post**. The KG/Meter/Piece values of the production order are thereby rolled back and can subsequently be reported correctly anew.

### Use case 2: Cancelling an incorrect consumption posting of a lot-tracked component

**Trigger:** During post-calculation, it is noticed that a component was posted as consumed with the wrong lot for a production order. The component is lot-tracked and is converted into KG/Meter/Piece.

**Entry point in BC:** The user opens the released **production order** and, from it, the **Production Journal**.

**Core flow:**
1. Choose the **Cancel Posting** action.
2. In the dialog, set **Correct Consumption** and, below it, **Cancel Quantity**.
3. Confirm the dialog with **OK** and confirm the prompt to delete the journal lines.
4. In the selection of the consumption **Item Ledger Entries**, mark the affected line with the wrong **Lot No.** and take it over with **OK**.
5. Business Central creates the consumption reversal posting, takes over the original **Lot No.** via **Item Tracking**, and establishes the application to the original entry; the app additionally transfers the KG/Meter/Piece values of the item ledger entry to the cancellation line.

**Completion:** The user posts the cancellation line via **Post**. The consumption is reversed including the lot and conversion values; afterwards, the correct lot can be posted as consumed anew.

## FAQ and troubleshooting

### 1. Why do I need additional apps besides this one?
This app is a pure connector app. The **Cancel Posting** action comes from **m+m Undoing Production**, and the fields **KG**, **Meter**, and **Piece** come from **m+m Unit Conversion**. Without these two apps, there is neither the cancellation nor the conversion fields to be transferred.

### 2. Do I have to set up the app before I can use it?
No. The app has no setup page, no number series, and no master data. It takes effect automatically as soon as it is installed together with the required apps.

### 3. Where do I find the function to cancel a production posting?
In the **Production Journal** of a released production order, via the **Cancel Posting** action. There is no dedicated page for this connector app.

### 4. Which fields exactly does the app transfer?
From the original **Item Ledger Entry**, it transfers the fields **KG**, **Meter**, **Piece**, **Actual KG per Meter**, **Actual KG per Piece**, **Theoretical KG per Meter**, and **Theoretical KG per Piece** to the newly created **Item Journal Line**.

### 5. When exactly are the values set?
The values are set immediately before Business Central validates the quantity of the cancellation line. As a result, the reversal posting carries the same conversion values as the original posting.

### 6. Does the transfer apply to outputs and to consumption postings?
Yes. Both when cancelling an **output** and when cancelling a **consumption** posting, the same KG/Meter/Piece values of the respective original entry are taken over.

### 7. Are KG/Meter/Piece values transferred during time cancellation as well?
No. The **Cancel Times** option acts only on the posted capacity times from the capacity ledger entries. The KG/Meter/Piece values are transferred from the item ledger entries exclusively for quantity cancellation.

### 8. What happens to a lot or serial number during cancellation?
If the original entry carries a **Lot No.** or Serial No., the **Item Tracking** is taken over automatically into the cancellation line and the application to the original entry is established. The conversion values are taken over from the same entry independently of this.

### 9. Why does Business Central ask about deleting journal lines during cancellation?
The cancellation run first deletes existing lines in the affected journal batch so that clean cancellation lines can be created. Confirm this prompt only if the existing lines may actually be discarded.

### 10. After the cancellation, I do not see any KG/Meter/Piece values on the cancellation line — why is that?
The app only transfers values that were present in the original **Item Ledger Entry**. If no KG/Meter/Piece value or no conversion factor was stored there, the cancellation line also remains empty in these fields. Also check whether the **m+m Unit Conversion** app is installed, because otherwise the fields do not exist at all.
