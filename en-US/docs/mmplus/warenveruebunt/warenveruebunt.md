---
title: Anwenderhandbuch m+m Goods Receipt with Logistic Differences
---

# User Manual m+m Goods Receipt with Logistic Differences

## Introduction

This manual is intended for the **operational users in goods receipt and purchasing** who record and post incoming goods in the **m+m Goods Receipt** module. The secondary audience is administrators who set up the permissions and the rules for underdeliveries.

The **m+m Goods Receipt with Logistic Differences** extension connects two existing modules: **m+m Goods Receipt** (recording and posting of goods receipts from goods orders) and **m+m Over-/Underdelivery** (rules for over- and underdeliveries). It adds exactly one additional indicator to the line of a **Purchase Order** (the goods receipt document): **Order Complete**.

With this indicator you resolve a common logistics situation: a vendor delivers **less** than ordered and will **not** deliver the remaining quantity later. Without the extension the order would remain open with an outstanding remaining quantity. If, instead, you set **Order Complete** on the affected line and enter the actually delivered **Quantity**, then when the **Purchase Order** is processed the quantity of the underlying purchase order line is reduced to the delivered quantity and the order is closed despite the difference. The logistic quantity gap is thereby balanced out.

**Short process overview**

1. The user opens the affected **Purchase Order** and selects the line to be posted.
2. They enter the actually delivered **Quantity** and, for a final underdelivery, set the **Order Complete** indicator.
3. They start the **Process Purchase Order** action.
4. The extension reduces the quantity of the purchase order line to the delivered quantity, transfers the **Order Complete** indicator, and the goods receipt is posted; the order is closed.

## Quick start for users

Prerequisite: In the **Over-/Underdelivery** setup, **Underdelivery** is allowed for purchasing (see the *Setup* chapter), you hold the **MuM GROS All** permission, and the associated purchase order is **Released**.

Post a final underdelivery (minimal path):

1. Use **Search** to open the **Purchase Orders** list and open the affected **Purchase Order** from the line (double-click).
2. On the **Lines** FastTab, select the line of the underdelivered item.
3. In **Quantity**, enter the actually delivered quantity (less than the ordered quantity).
4. On the same line, set the **Order Complete** indicator.
5. Choose the **Process Purchase Order** action.

After processing, the goods receipt is posted with the delivered quantity and the purchase order line is closed. For a **complete** delivery, leave **Order Complete** empty and process the **Purchase Order** as usual.

## Setup

The extension itself does **not** provide its own setup page. However, for the **Order Complete** indicator to take effect, three prerequisites from the base modules must be met. These are described here in dependency order so that an administrator can fully activate the function.

### Setting up underdelivery with document closing

**Process intro.** An administrator performs this setup **once before first use**. It determines whether an underdelivery is allowed in purchasing at all. Only then can a user, in their daily work, set the **Order Complete** indicator on the line of the **Purchase Order**. The result of this setup is applied in the chapter *Daily work on the Purchase Order document*.

**Procedure in dependency order**

1. **First**, use **Search** to open the setup page of the **Over-/Underdelivery** (base module m+m Over-/Underdelivery) and activate the control for **Purchase**. When purchasing is activated, the rules for over- and underdeliveries take effect in goods receipt and purchasing processes; without this activation no controlled underdelivery, and therefore no document closing via **Order Complete**, is possible.

2. **Then** define the control method and the permitted range for the **Underdelivery**. The following settings come from the base **Over-/Underdelivery** setup and are decisive for the **Order Complete** indicator:

| Setup | Explanation |
|-------------|-------------|
| Purchase | If activated, underdeliveries in purchasing are controlled and the **Order Complete** indicator can be set on the line; if the setting is empty, every line remains open until the delivery is complete and **Order Complete** has no effect. |
| Underdelivery Control Type | If a control type is set for the underdelivery, the system checks when **Order Complete** is set whether the delivered quantity lies within the permitted range; otherwise the operation is rejected or a warning is shown. |
| Control Method | Determines how the permitted underdelivery range is calculated. **Default:** the standard behavior of Business Central applies. **Percentage:** the permitted range is derived from a percentage of the original quantity. **Absolute Value:** the permitted range is derived from a fixed quantity value. |
| Control Value | If a control value is stored, it limits the permitted deviation (as a percentage or as an absolute value depending on the control method); only within this value is an underdelivery with **Order Complete** allowed. |
| Warning | If the warning is activated, the user can nevertheless confirm the underdelivery after a prompt and set **Order Complete** even outside the otherwise rigid range; if the warning is deactivated, an impermissible underdelivery is prevented with an error message. |

> This page belongs to the base module **m+m Over-/Underdelivery**. Further fields of this setup (e.g. item-specific rules, defaults per vendor) are not required for document closing via **Order Complete** and are described in the manual of the base module; for the present extension the fields listed above are sufficient.

3. **Afterwards**, make sure that the users hold the **MuM GROS All** permission (see *Permissions*) and that a valid license is available (see *License*).

**Operational conclusion.** Once these steps are met, the function is triggered in daily work by the **Process Purchase Order** action as soon as **Order Complete** is set on the line and a **Quantity** lower than the order is entered (cross-reference: *Daily work on the Purchase Order document*).

### Permissions

The extension ships the assignable permission set **MuM GROS All**. It determines the permissions for executing the associated processing logic.

| Setup | Explanation |
|-------------|-------------|
| Permission set **MuM GROS All** | If this permission set is assigned to a user or a user group, that user may run the processing in which the **Order Complete** indicator is evaluated during posting; without this permission the line quantity is not automatically adjusted during processing. The permission set defines which actions the user may perform within this extension. |

### License

At sign-in, the extension checks once whether a valid license is available for the installed app.

| Setup | Explanation |
|-------------|-------------|
| Valid license of the app | If a valid license is available, the **Order Complete** function is available when the **Purchase Order** is processed; without a valid license the processing logic cannot be executed. This check runs automatically in the background and requires no user input. |

## Daily work on the Purchase Order document

This extension takes effect exclusively when editing the **Purchase Order** document. The behavior is controlled by the **Over-/Underdelivery** setup (cross-reference: *Setting up underdelivery with document closing*): only if the underdelivery is allowed there for purchasing can the **Order Complete** indicator be set on the line.

**Entry point:** Use **Search** to open the **Purchase Orders** list and open the individual **Purchase Order** from the desired line. The list is only for navigation; per document it shows the columns **No.**, **Status**, **Document Date**, and the receipt date.

### Document header of the Purchase Order

The header of the **Purchase Order** identifies the vendor and the document. For document closing via **Order Complete**, the **Status** is above all decisive.

| Field | Explanation |
|------|-------------|
| No. | Unique document number of the **Purchase Order**; it identifies the document in the list and history. |
| Buy-from Vendor No. | If the vendor is entered here, the system relates the supplier and associated defaults to this vendor; without a vendor no line can be processed. |
| Buy-from Vendor Name | Displays the name of the vendor selected under **Buy-from Vendor No.** for verification. |
| Document Date | Document date of the **Purchase Order**; it is used for assigning and evaluating the document. |
| Status | Controls which actions are possible. **Open:** document in progress, lines can be changed, no processing yet. **In Progress:** the document is in an intermediate state of processing. **Released:** the document is released and can be processed. The underlying purchase order must also be **Released** during processing, otherwise the processing is rejected. |
| Receipt Location Code | If a receipt location is stored, the lines are received by default to this location; it determines where the delivered quantity is posted. |

> The remaining header areas (ship-to address, creation and modification information, external shipment data) come from the base module and do not affect the **Order Complete** indicator; they are not required for the procedure described here.

### Lines of the Purchase Order

On the **Lines** FastTab you record the items and quantities of the goods receipt. This extension adds the last column **Order Complete** to the line. The user sees base fields and the extension field on **one** screen; therefore both are documented together here.

| Field | Explanation |
|------|-------------|
| Item No. | If you select the item here, the system takes the description and unit from the item card; the line refers to this item. |
| Item Reference No. | If an item reference (e.g. a vendor item number) is entered, the associated item is determined automatically; this eases recording based on the vendor's documents. |
| Description | Displays the item's description; it can be adjusted for verification. |
| Description 2 | Additional description line of the item for supplementary information. |
| Quantity | Enter the actually delivered quantity here. If the entered quantity is less than the ordered quantity and **Order Complete** is set, then during processing the quantity of the purchase order line is reduced to this quantity and the order is closed. |
| Unit of Measure Code | Determines the unit of measure of the entered **Quantity**; changing the unit recalculates the base quantity accordingly. |
| Variant Code | If the item is managed with variants, the variant code determines which variant is received. |
| Receipt Location Code | If a receipt location is set, the quantity of this line is received to this location. |
| Receipt Bin Code | If the location is bin-mandatory, the bin code determines the exact bin of the receipt. |
| **Order Complete** | Set this indicator when the actually delivered **Quantity** is less than the ordered quantity and **no** remaining delivery will follow. When the indicator is set and the quantity is below the ordered quantity, the system reduces the purchase order line to the delivered quantity during processing, transfers the indicator to the purchase order line, and closes the order so that no further goods receipts are possible. If the indicator is **not** set (or the full quantity was delivered), the standard procedure remains unchanged and a remaining quantity stays open. The indicator can only be set within the configured underdelivery rules. |

> The technical source columns of the line (Source Type, Source Subtype, Source Document, Source No., Source Line No., Source Subline No.) are not editable and serve only for tracing back to the original purchase order line. They are filled by the system and require no input.

### Line action and processing

On the document, the status actions of the **Change Status** group are available (**Release**, **Notify**, **In Progress**, **Reopen**) as well as the actions **Get Purchase Order Lines** and **Process Purchase Order**.

- **Get Purchase Order Lines:** Use the **Get Purchase Order Lines** action to open the selection of open purchase order lines in order to transfer lines into the **Purchase Order**.
- **Process Purchase Order:** Use the **Process Purchase Order** action to open the processing of the document. For each line, it is checked whether **Order Complete** is set and the delivered **Quantity** is lower than the ordered quantity. If this is the case, the system reduces the quantity of the purchase order line to the delivered quantity, transfers **Order Complete**, and then posts the goods receipt.

**Posting procedure for document closing**

1. On the **Purchase Order**, select the underdelivered line.
2. In **Quantity**, enter the delivered quantity and set **Order Complete**.
3. Choose **Process Purchase Order**.
4. Before posting, the system reduces the quantity of the purchase order line to the delivered quantity and sets **Order Complete** there.
5. The goods receipt is posted; the purchase order line is closed and no outstanding remaining quantity remains.

## Typical use cases

### Use case 1: Completing a final underdelivery

**Trigger.** A vendor reports by phone or e-mail that, of 100 ordered pieces, they will deliver only 95 and will not deliver the remaining 5 later.

**Entry point in BC.** The user opens the **Purchase Orders** list via **Search** and opens the affected **Purchase Order**. The prerequisite is that the associated purchase order has the status **Released** and that the underdelivery is set up in purchasing.

**Core procedure.**
1. On the **Lines** FastTab, the user selects the item's line.
2. In **Quantity**, they enter the delivered 95 pieces.
3. They set the **Order Complete** indicator because no remaining delivery will follow.
4. They choose the **Process Purchase Order** action.

**Conclusion.** The extension reduces the purchase order line to 95 pieces, transfers **Order Complete**, and the goods receipt for 95 pieces is posted. The order is closed; no 5 pieces remain as an outstanding remaining quantity.

### Use case 2: Complete delivery without the indicator

**Trigger.** An order is delivered in full in the ordered quantity.

**Entry point in BC.** The user opens the **Purchase Orders** list via **Search** and the affected **Purchase Order**.

**Core procedure.**
1. On the **Lines** FastTab, the user checks the delivered **Quantity**.
2. They leave **Order Complete** empty, since there is no underdelivery.
3. They choose **Process Purchase Order**.

**Conclusion.** Because **Order Complete** is not set, the special logic of the extension does not take effect; the goods receipt is posted for the full quantity in the standard procedure.

## FAQ and Troubleshooting

### 1. What is the "Order Complete" indicator for?
It closes an order despite an underdelivery. When you set it and post a **Quantity** lower than ordered, the system reduces the purchase order line to the delivered quantity and no longer allows any further goods receipts.

### 2. Why can I not set "Order Complete"?
The indicator is only permitted within the configured underdelivery rules. Check in the **Over-/Underdelivery** setup whether **Purchase** is activated and an underdelivery is allowed. Without this setup the indicator has no effect.

### 3. What happens if I set "Order Complete" but deliver the full quantity?
Nothing special. If the delivered **Quantity** is not less than the ordered quantity, the extension skips its special logic and the goods receipt is posted in the standard procedure.

### 4. What happens if I do not set "Order Complete" and deliver less?
Then the order remains open with an outstanding remaining quantity. Only the posted partial quantity is received; further goods receipts remain possible.

### 5. Must the purchase order be released?
Yes. During processing, the system checks that the underlying purchase order has the status **Released**. If it is not released, the processing is rejected with an error message.

### 6. How do I start the actual posting?
Via the **Process Purchase Order** action on the document. This action checks the lines, applies the **Order Complete** logic, and posts the goods receipt.

### 7. Is my recorded quantity changed at closing?
The **Quantity** you entered remains the posted goods receipt quantity. What is changed is the **purchase order line**: its quantity is reduced to the delivered quantity so that no remaining quantity stays open.

### 8. Can I continue to receive in several partial deliveries?
Yes. As long as you do not set **Order Complete**, you can receive across several goods receipts. Only when no remaining delivery will come do you set **Order Complete** at the last receipt.

### 9. Which permission is required?
The permission set **MuM GROS All** must be assigned to the user. It determines the permissions for executing this extension's processing logic.

### 10. Why is the function not available after installation?
At sign-in, a valid license of the app is checked. If a valid license is missing, the processing logic cannot be executed. In this case, contact your administration.
