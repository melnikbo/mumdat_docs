---
title: Anwenderhandbuch m+m Logistic Differences
---

# m+m Logistic Differences User Guide

## Introduction

The **m+m Logistic Differences** extension controls **over- and underdelivery** of quantities in Microsoft Dynamics 365 Business Central. For many companies it is essential to allow or prevent, in a controlled manner, that more or less is shipped, received, picked, or posted than originally agreed, because such differences have far-reaching consequences for the supply chain, inventory, and pricing.

On every quantity-relevant action, the app compares the current quantity with a stored **Original Quantity** and applies one of three reactions per setup: the difference is allowed silently, it triggers a **Warning** with a confirmation dialog, or it is blocked with an error message. The controls apply in **Purchase**, **Sales**, in **Transfer**, at **Warehouse Receipt** and **Warehouse Shipment**, in the **warehouse activities** (Pick, Put-away, Movement), in the **Item Journals**, and during **Component Pick** from manufacturing.

**Target audience.** This guide is aimed primarily at **operational users** who process and post documents every day: buyers, sales order processors, warehouse and picking staff. They enter quantities in sales, purchase, transfer, and warehouse documents and decide in the dialog about permissible differences. The secondary audience is **administrators and key users**, who store the tolerance rules in the setup and in the master data.

**Process overview.** The administrator activates the control per process and defines the control method and value (**Over Under Delivery Setup**), optionally refines the rules by item or partner (**Over Under Delivery Item Setup**), and creates defaults (**Over Under Delivery Defaults**). In daily operation, the user sets the **Original Quantity**, changes the quantity to be shipped/received, and reacts to a warning or error. Every confirmed difference is documented in an audit-proof manner in the **Over Under Delivery Action Logs**.

---

## Quick Start for Users

The following steps lead from an empty system to the first controlled overdelivery. The order follows the technical dependency: setup first, then document.

1. **Open the setup.** Use **Search** to open the **Over Under Delivery Setup** page. It is a company-wide setup page (one record per company).
2. **Activate the process.** On the **General** FastTab, set the required flag, e.g. **Sales Overdelivery Active** for sales. Without this flag the app does not check the process.
3. **Check the defaults.** In the **Defaults** subform, review the line for **Sales / Overdelivery**, choose a **Control Method** (e.g. **Absolute Value**) and enter a **Control Value** (e.g. 10). Set **Warning** if the user should be allowed to confirm the limit.
4. **(Optional) Specific rule.** In the **Over Under Delivery Item Setup**, create a more granular rule for a specific customer, vendor, location, or item.
5. **Create a document.** Open a **Sales Order** and enter a line with a **Quantity** (e.g. 10). The app automatically writes the **Original Quantity**.
6. **Change the quantity.** Change **Qty. to Ship** beyond the tolerance (e.g. 21). With **Warning** active, a confirmation dialog appears; with **Warning = No**, an error message appears. On rejection the value is reset to the maximum allowed quantity; on confirmation the difference is accepted and logged.
7. **(Underdelivery) Close the document.** If you want to end a line despite a remaining quantity, set the **Order Complete** flag on the document line and confirm the prompt about updating the quantity.

For pure document checking, steps 5–7 are sufficient, provided the setup is already in place.

---

## Setup

Setup is the most extensive part of this app. Before first use, an administrator defines here **which** processes are checked, **how** differences are controlled, and **whether** the user may exceed limits by confirmation.

### Setting Up Over/Underdelivery Control

**Who/when/what for.** The administrator performs this central setup once per company before the first document processing. It enables the check per process and defines the default behavior that all documents in the **Daily Work** chapter rely on.

**Getting there:** Use **Search** to open the **Over Under Delivery Setup** page. It is a company-wide setup page; when it is opened for the first time, the record together with its defaults is created automatically.

#### Process activation (General FastTab)

Each flag switches the control for a process completely on or off.

| Setup | Explanation |
|---|---|
| **Purchase Overdelivery Active** | When activated, the app checks in purchasing every quantity to be received that exceeds the Original Quantity; without the flag, purchasing stays on the Business Central standard and overdeliveries are not controlled. |
| **Purchase Underdelivery Active** | When activated, the control applies as soon as less is received in purchasing than originally agreed; this enables the controlled closing of remaining quantities via **Order Complete**. |
| **Sales Overdelivery Active** | When activated, the app checks in sales every ship quantity above the Original Quantity and triggers a warning or error depending on the rule. |
| **Sales Underdelivery Active** | When activated, the app controls sales shipments below the Original Quantity and allows the controlled closing of partial shipments. |
| **Transfer Overdelivery Active** | When activated, a quantity to be shipped above the Original Quantity is controlled on transfer orders. |
| **Transfer Underdelivery Active** | When activated, the app controls transfers below the Original Quantity and enables the closing of remaining quantities. |
| **Item Journal Overdelivery Active** (Item Journal) | When activated, the app checks in the Item Journal posted quantities above the Original Quantity; without the flag, the journal quantity is not checked against a tolerance. |
| **Item Journal Underdelivery Active** (Item Journal) | When activated, the app controls quantities below the Original Quantity in the Item Journal. |
| **Component Pick Overdelivery Active** | When activated, the app checks quantities to be handled above the Original Quantity when picking production components; this makes it possible to take more material if the rule allows it. |
| **Component Pick Underdelivery Active** | When activated, the app controls component picking below the Original Quantity and allows controlled closing. |

#### Fixed Price on Over/Underdelivery

These four flags control whether a quantity change triggered by the over/underdelivery may trigger a price recalculation in the document.

| Setup | Explanation |
|---|---|
| **Purchase Fixed Price for Overdelivery** | When activated, the purchase price stays unchanged on an overdelivery; when writing the posted quantity back to the purchase line, the app suppresses the recalculation so that the originally agreed price is retained. |
| **Purchase Fixed Price for Underdelivery** | When activated, the purchase price stays unchanged on an underdelivery; without the flag, a reduced quantity can retrigger a price tier. |
| **Sales Fixed Price for Overdelivery** | When activated, the sales price stays fixed on an overdelivery; the app prevents the recalculation of the line price during the automatic quantity update after the warehouse posting. |
| **Sales Fixed Price for Underdelivery** | When activated, the sales price stays fixed on an underdelivery, even if the reduced quantity would otherwise result in a different price tier. |

#### Update Quantity From Tracking

In the **Update Quantity From Tracking** group, the administrator defines per area how the app behaves when a total quantity that differs from the document quantity is captured via the **Item Tracking Lines**. Each field is an option with the same three values.

| Setup | Explanation |
|---|---|
| **Purchase** | Controls writing the quantity captured from item tracking back into the purchase line. |
| **Sales** | Controls writing the tracking quantity back into the sales line. |
| **Transfer** | Controls writing the tracking quantity back into the transfer line. |
| **Warehouse Receipt** | Controls the behavior for a differing tracking quantity in the warehouse receipt. |
| **Warehouse Shipment** | Controls the behavior for a differing tracking quantity in the warehouse shipment. |
| **Warehouse Activity** | Controls the behavior in pick and put-away activities. |
| **Item Journal** | Controls the behavior in the Item Journal (subgroup **Journals**). |
| **Transfer Journal** | Controls the behavior in the transfer journal. |
| **Phys. Inventory Journal** | Controls the behavior in the physical inventory journal. |
| **Revaluation Journal** | Controls the behavior in the revaluation journal. |

The option values per field mean:

- **Standard:** The Business Central standard behavior applies; the app does not automatically update the document quantity from tracking.
- **Everytime:** If the quantity captured in tracking differs from the document quantity, the document quantity is set to the tracking quantity without a prompt.
- **Question:** On a difference, the prompt *"The assigned Quantity … is different then the document quantity … Do you want to update quantity on the document?"* appears before the update; the document quantity is adjusted only after confirmation.

#### Permissions

The permission set **MuM OS Permission** belongs to the app. It defines which actions users may perform in the tables and pages of the over/underdelivery functionality and thereby determines the permissions for the setup, item setup, document setup, and action log. Assign this permission set to the roles that maintain tolerance rules or are supposed to confirm differences.

#### Over Under Delivery Defaults

**Who/when/what for.** The **Defaults** define the default behavior per combination of **Applies-to Type** and **Defines**. The administrator maintains them directly in the **Defaults** subform of the setup page. They apply whenever no more specific item setup exists and are copied into the **Document Setup** when a document is processed.

**Getting there:** The **Defaults** subform is shown directly on the **Over Under Delivery Setup**. If lines are missing, the **Create Defaults** action generates the ten default lines (All Customers, All Vendors, Transfer, Item Journal, Component Pick – each for overdelivery and underdelivery).

| Setup | Explanation |
|---|---|
| **Applies-to Type** | Shows the reference scope of the default line (e.g. All Customers, All Vendors, Transfer). The field is not editable because the defaults are created by the system. |
| **Defines** | Indicates whether the line controls the **Overdelivery** or the **Underdelivery**; not editable. |
| **Control Method** | Defines how the difference is limited (see values below). |
| **Control Value** | If the Control Method is Percentage or Absolute Value, the limit value is entered here (mandatory field, otherwise locked). For Percentage, values between 0 and 100 are allowed. |
| **Warning** | When activated, the user may exceed the limit via a confirmation dialog (the difference is logged); when not activated, exceeding the limit is blocked with an error. Relevant only for Percentage/Absolute Value. |

Values of the **Control Method**:

- **Default:** On over- or underdelivery, the Business Central standard behavior applies; no dedicated limit value is checked and no control value is expected.
- **Percentage:** The permissible difference is calculated as a percentage of the Original Quantity (for overdelivery, Original Quantity + percent; for underdelivery, Original Quantity − percent).
- **Absolute Value:** The permissible difference is a fixed quantity amount above or below the Original Quantity.

**Process steps (end-to-end activation).** First, use **Create Defaults** to create the defaults and store Control Method/Value and Warning per line; then set the process flag on the **General** FastTab (e.g. **Sales Overdelivery Active**); finally, the rule applies in daily operation as soon as the user changes the quantity beyond the tolerance in a **Sales Order** (see **Daily Work on the Document**). You then define more granular exceptions in the **Over Under Delivery Item Setup**.

---

## Master Data

The actual tolerance rules maintained by the user reside in the **Over Under Delivery Item Setup**. From the master data cards (Customer, Vendor, Item, Location), the user reaches the filtered view of these rules directly.

### Setting Up Specific Rules in the Item Setup

**Who/when/what for.** Key users maintain more specific rules than the defaults here, before or during ongoing use – for example "Vendor X may underdeliver Item Y by an absolute 5 pcs". These rules override the defaults and are copied into the **Document Setup** when a document is processed. They are consumed in the **Daily Work on the Document** chapter.

**Getting there:**
- From the master data card or list: open, for example, the **Customer Card** and choose the **Over Under Delivery** action. Business Central opens the **Over Under Delivery Item Setup** filtered to this customer. The same action is available on **Vendor**, **Item**, and **Location** (card and list respectively).
- Alternatively via **Search** or via the **Over Under Delivery Item Setup** action on the setup page (unfiltered overall list).

| Field | Explanation |
|---|---|
| **Defines** | If **Overdelivery** is selected, the line applies to quantities above the Original Quantity; for **Underdelivery**, to quantities below it. Mandatory field – without a selection the line cannot be saved. |
| **Applies-to Type** | Defines the reference scope of the rule (values below). On change, the Applies-to No. is cleared. |
| **Applies-to No.** | If Applies-to Type names a specific vendor, customer, location, or journal template, the corresponding number is entered here (mandatory in this case); for "All …" the field stays empty. |
| **Product Type** | If **Item** is selected, the rule applies only to a specific item; for **All Items**, to all items of the reference scope. |
| **Product No.** | Editable only if Product Type = Item. Determines the item to which the rule applies. |
| **Description** | Shows the description text of the selected item (not editable). |
| **Variant Code** | If set, the rule is restricted to a specific variant of the item. |
| **Control Method** | As in the defaults: **Default** (BC standard), **Percentage**, or **Absolute Value**. |
| **Control Value** | Limit value for Percentage/Absolute Value; only editable then and, in that case, a mandatory field. |
| **Unit of Measure Code** | If set, the absolute control value refers to this unit of measure; for Product Type = Item, the Unit of Measure Code is mandatory. |
| **Warning** | When activated, the user can exceed the limit by confirmation (with a log entry); when not activated, exceeding the limit is blocked with an error. |

Values of **Applies-to Type** in the item setup:

- **All Vendors:** The rule applies to purchase and receipt processes of all vendors.
- **Vendor:** The rule applies only to the vendor named in **Applies-to No.**.
- **All Customers:** The rule applies to sales, shipment, and picking processes of all customers.
- **Customer:** The rule applies only to the named customer.
- **Transfer:** The rule applies to transfer processes; the number refers to a location (origin).
- **Item Journal:** The rule applies to an item journal; the number refers to the journal template.
- **Component Pick:** The rule applies to the picking of production components (no Applies-to No.).

Values of **Product Type**:

- **All Items:** The rule applies to all items of the selected reference scope.
- **Item:** The rule applies only to the item specified in **Product No.** (Unit of Measure Code then mandatory).

**Process steps.** First select **Defines** (Over/Underdelivery), then **Applies-to Type** and, if applicable, **Applies-to No.**, then optionally item/variant/unit, and finally **Control Method**, **Control Value**, and **Warning**. The line is validated on save (Applies-to No. and item/unit requirements). If no matching item setup exists, the **Defaults** apply. If you delete a customer, vendor, item, variant, or location, the app automatically removes the associated item setup lines.

### Item Tracking

**Who/when/what for.** If an item is managed with **item tracking** (serial/lot numbers), the user captures the quantities in the **Item Tracking Lines**. When these lines are closed, the app checks whether the total quantity captured there violates the over/underdelivery rule of the document.

**Getting there:** On the document line via **Line → Item Tracking Lines**.

**Process.** If the user changes the **Quantity (Base)** beyond the tolerance and closes the page, a warning or an error is triggered – depending on **Warning**. If the warning is accepted, the system takes the total quantity into the document line and adjusts **Quantity** and **Qty. to Ship**; the prompt follows the value configured in **Update Quantity From Tracking** (**Standard/Everytime/Question**).

---

## Daily Work on the Document

The daily check takes place directly in the standard documents. The behavior is controlled by the previously described **Over Under Delivery Setup** page (process activation, control method) and **Over Under Delivery Item Setup** page (specific rules); the rule actually applied is recorded per document in the **Over Under Delivery Document Setup**. The extension adds the same two line fields and the same line action to all supported documents.

### Line Fields and Action (all documents)

The app adds these fields to the line subform of **Sales Order**, **Purchase Order**, **Transfer Order**, in the **Item Journals**, and in all warehouse document lines (Warehouse Receipt, Warehouse Shipment, Pick, Put-away, Movement).

| Field | Explanation |
|---|---|
| **Original Quantity** | Contains the originally agreed quantity against which every later change is checked. When this field is set and the current quantity differs, the over/underdelivery control applies; if it is 0, no check takes place. The field is not directly editable. |
| **Order Complete** | When activated, the user declares the line completed despite a remaining quantity, so that no further shipments/receipts are expected. Can be set only for underdelivery and only if an already posted quantity > 0 exists; when set, the document quantity is reduced to the already shipped/received quantity after confirmation. If the user then changes the quantity, the flag is removed automatically. |

Line action:

- **Set Original Quantity** (on the **Lines** FastTab): After a prompt, replaces the **Original Quantity** with the current **Quantity** and resets **Order Complete**. Use this action when the agreed quantity has legitimately changed and future checks should run against the new value. The change is logged.

### Document Actions (Header)

In the document header (**Related/Navigate** ribbon), the app provides the **Over Under Delivery** group:

- **Document Setup**: Opens the **Over Under Delivery Document Setup** for the current document. Here the user sees and changes the rule determined specifically for this document.
- **Action Logs**: Opens the **Over Under Delivery Action Logs** filtered to the current document.

### Over Under Delivery Document Setup

**Who/when/what for.** The document setup is the per-document copy of the default or item rule. The user opens it via the **Document Setup** document action to review the rule applicable to this document or to adjust the **Control Value**.

**Getting there:** In the document (e.g. **Sales Order**) via **Over Under Delivery → Document Setup**. The page is not reachable via **Search**, only from within the document.

| Field | Explanation |
|---|---|
| **Document Line No.** | Links the rule to the document line (not editable). |
| **Defines** | Shows whether the rule concerns over- or underdelivery (not editable). |
| **Applies-to Type** | Reference scope of the determined rule (not editable). |
| **Applies-to No.** | Specific vendor/customer/location of the rule (not editable). |
| **Product Type** | All Items or Item (not editable). |
| **Product No.** | Affected item (not editable). |
| **Description** | Item description (not editable). |
| **Variant Code** | Affected variant (not editable). |
| **Control Method** | Applied method: Default, Percentage, or Absolute Value (not editable; taken from the default/item setup). |
| **Control Value** | Only editable if the Control Method is not Default; here the user can fine-tune the limit for exactly this document. |
| **Unit of Measure Code** | Unit of measure of the absolute control value (not editable). |
| **Warning** | Shows whether the limit can be exceeded by confirmation (not editable). |

**Update** action: Re-determines the document setup lines based on the current document lines and rules. Use it if lines or master data rules have changed after the first opening.

### Process on a Quantity Change

If the user changes **Qty. to Ship** in the sales order (or, in purchasing, the quantity to be received; in a transfer, the quantity to be shipped) beyond the permissible limit, the following check runs:

1. Select the line on the document and change **Qty. to Ship**.
2. The app compares the planned total quantity (already shipped + to ship) with the limit calculated from **Control Method** and **Control Value**.
3. **Within the tolerance:** The quantity is accepted without a message.
4. **Outside + Warning = No:** An error message appears stating the current restrictions and the maximum or minimum allowed quantity; the change is rejected.
5. **Outside + Warning = Yes:** The confirmation dialog *"… would you still want to continue?"* appears. On **Yes**, the quantity is accepted and an entry is written in the **Action Logs**; on **No**, it is reset to the allowed quantity.
6. **Close an underdelivery:** If less is shipped than agreed and the remainder is to be dropped, set **Order Complete**. The app allows this only for underdelivery and a posted quantity > 0, asks *"The assigned Quantity … Do you want to update quantity on the document?"* and sets the document quantity to the shipped quantity.

On **Drop Shipment**, after posting, the app updates both the purchase line and the sales line according to the applicable over- or underdelivery rule.

---

## Warehouse, Picking, and Follow-up Documents

The over/underdelivery control also applies in the warehouse processes. The prerequisite is that the respective process is activated in the **Over Under Delivery Setup** (**Warehouse Receipt**, **Warehouse Shipment**, **Warehouse Activity**, **Component Pick …**). The line fields **Original Quantity** and **Order Complete** and the **Set Original Quantity** action are available in all warehouse document lines as described in the **Daily Work** chapter.

### Warehouse Receipt, Warehouse Shipment, and Pick

- **Warehouse Receipt** (from a purchase order or an inbound transfer): When capturing the quantity to be received, the app checks against the purchase or transfer rule. Via the header action **Over Under Delivery → Document Setup** you open the rule applicable to the origin document; via **Action Logs** the associated confirmations.
- **Warehouse Shipment** (from a sales order or an outbound transfer): Analogously, the quantity to be shipped is checked; the document actions open the document setup or the log of the origin document (sales or transfer).
- **Pick** and **Put-away** (warehouse and inventory pick/put-away): When changing the quantity to be handled, the control applies for sales, purchase, transfer, or component pick – depending on the origin of the line. The header actions of the pick and put-away also open **Document Setup** and **Action Logs**.

After the warehouse posting, the app writes the actually moved quantity back to the origin line (sales/purchase/transfer) and – if **Order Complete** is set – marks the line as completed. If the matching **Fixed Price** is active, the price stays unchanged.

### Component Pick (Manufacturing)

When picking production components, the app checks the quantity to be taken against the **Component Pick** rule. Within the absolute tolerance (relative to already registered and open pick lines), the app allows the quantity and bypasses the standard check "quantity to handle greater than open quantity"; outside it, a warning or error applies as usual.

### Balancing Pick Lines (Take/Place)

For quantity-changing picking, **Take** and **Place** lines must remain equal in quantity. The helper page **Lines** (for the pick lines) supports the user with this: it shows the associated activity lines, allows splitting a line via **Split Line**, and, on close, checks that the sum of the quantities to handle in Take and Place lines match. If they differ, the app reports *"Quantity in Take Lines … must be equal to quantity in Place Lines …"*. Lines already changed on the origin document are locked.

---

## History and Traceability

### Over Under Delivery Action Logs

**Who/when/what for.** Every difference confirmed via a **Warning** as well as every change of the **Original Quantity** is logged in an audit-proof manner. The log helps to trace later who accepted which over- or underdelivery and when.

**Getting there:** Via **Search** (history list), via the **Action Logs** action on the **Over Under Delivery Setup**, or via the **Over Under Delivery → Action Logs** group in any supported document (then filtered to that document). The list is not editable and sorted descending by **Date/Time**.

| Field | Explanation |
|---|---|
| **Source Document** | Refers to the document in which the difference occurred. |
| **Defines** | Whether it was an over- or an underdelivery; for a pure change of the Original Quantity, the value stays empty. |
| **Original Quantity** | The quantity against which the check was performed. |
| **Min/Max Allowed Qty.** | The limit calculated from Control Method/Value (empty if not relevant). |
| **Final Qty.** | The quantity actually accepted after confirmation. |
| **User** | The user who confirmed the difference. |
| **Date/Time** | Point in time of the confirmation. |
| **Set Original Quantity** | When activated, the line documents a manual reset of the Original Quantity (not an over/underdelivery). |

**Open Related Record** action: Jumps from the log line to the associated origin document. If the document no longer exists, the app reports *"Source Document does not exist anymore!"*.

---

## Typical Use Cases

### Use Case 1 — Sales Overdelivery with Warning

**Trigger.** A customer calls and wants to receive 21 pcs at short notice instead of the ordered 10 pcs.

**Getting into BC.** The sales order processor opens the relevant **Sales Order** and switches to the line.

**Core flow.**
1. Prerequisite: In the **Over Under Delivery Setup**, **Sales Overdelivery Active** is set, and the default for Sales/Overdelivery uses **Absolute Value** = 10 with **Warning** = Yes (see **Setup**).
2. The line already carries the **Original Quantity** 10.
3. The user changes **Qty. to Ship** to 21.
4. The app detects that the limit is exceeded (10 + 10 = 20) and shows the confirmation.
5. On **Yes**, 21 is accepted; on **No**, it is reset to 20.

**Conclusion.** The accepted difference appears in the **Over Under Delivery Action Logs** with **Original Quantity** 10, **Min/Max Allowed Qty.** 20, **Final Qty.** 21, and the user name.

### Use Case 2 — Closing a Purchase Underdelivery

**Trigger.** A supplier informs by email that it will no longer deliver the remaining 3 of 10 pcs.

**Getting into BC.** The buyer opens the relevant **Purchase Order**.

**Core flow.**
1. Prerequisite: **Purchase Underdelivery Active** is set; a rule is stored for Purchase/Underdelivery.
2. 7 pcs have already been received (**Qty. to Receive** of the current receipts = 0).
3. The buyer sets the **Order Complete** flag on the purchase line.
4. The app checks that an underdelivery is permitted and the received quantity is > 0, and asks *"The assigned Quantity … Do you want to update quantity on the document?"*.
5. On **Yes**, the order quantity is reduced to 7; further receipts are thereby excluded.

**Conclusion.** The order is closed in terms of quantity; the **Action Logs** action in the document header group **Over Under Delivery** shows the confirmations that were made.

### Use Case 3 — Extra Withdrawal in Component Picking

**Trigger.** In production, while picking a component, it is found that slightly more material must be taken than planned in the production order.

**Getting into BC.** The warehouse staff opens the **Pick** for the production component.

**Core flow.**
1. Prerequisite: **Component Pick Overdelivery Active** is set; for **Component Pick**, a rule with **Absolute Value** and **Warning** is stored.
2. The user increases the quantity to be handled on the pick line beyond the planned quantity.
3. If the extra quantity is within the absolute tolerance (relative to already registered and open pick lines), the app allows it without a standard error.
4. If it is above it, a warning or error appears according to the rule.

**Conclusion.** After posting the pick, the component quantity is adjusted accordingly; confirmed differences appear in the **Action Logs**.

---

## FAQ and Troubleshooting

### 1. Why is a quantity change not checked at all?
The check applies only if the process is activated in the **Over Under Delivery Setup** (e.g. **Sales Overdelivery Active**) and the line has an **Original Quantity** > 0. If the Original Quantity is 0 or the process flag is not set, Business Central behaves as standard.

### 2. Why does an error appear instead of a confirmation dialog?
Because the **Warning** flag is not set in the applicable rule (default, item setup, or document setup). Without a warning, exceeding the limit is blocked with an error; with a warning, the user may continue by confirmation.

### 3. Why can't **Order Complete** be set?
**Order Complete** is intended only for **underdelivery** and only if a quantity > 0 has already been shipped/received. On an overdelivery or without a posted quantity, the app indicates this with a notification.

### 4. Why does my **Order Complete** check mark disappear again?
As soon as the user changes the quantity of the line again, the app removes the flag automatically, so that further shipments/receipts become possible again. Set it again after the final change.

### 5. How does the app know which rule applies to my document?
On processing, the app searches for the most specific rule: first the **Over Under Delivery Item Setup** (item/variant/partner/unit), otherwise the **Defaults**. The result is copied into the **Over Under Delivery Document Setup**, which you can review via the **Document Setup** document action.

### 6. I changed the rule – why doesn't it take effect in the document?
In the document, open **Over Under Delivery → Document Setup** and choose **Update**. The document setup is a copy of the master rule and is thereby re-determined.

### 7. What exactly does the Control Value mean for Percentage?
For **Percentage**, the limit is calculated relative to the Original Quantity: for overdelivery, the Original Quantity plus the percentage; for underdelivery, minus it. Values between 0 and 100 are allowed; otherwise the app reports a range error.

### 8. Why does the price stay the same despite a changed quantity?
Because the matching **Fixed Price** parameter is active (e.g. **Sales Fixed Price for Overdelivery**). Then, when automatically writing the quantity back, the app suppresses the price recalculation so that the original price is retained.

### 9. How do differing quantities in the Item Tracking Lines take effect?
When closing the **Item Tracking Lines**, the app checks the captured total quantity against the rule. Whether the document quantity is then adjusted automatically is controlled by the **Update Quantity From Tracking** option (**Standard/Everytime/Question**) for the respective area.

### 10. Where can I see who approved an overdelivery?
In the **Over Under Delivery Action Logs**. Every difference confirmed via a warning is recorded with **Source Document**, **Defines**, **Original Quantity**, **Min/Max Allowed Qty.**, **Final Qty.**, **User**, and **Date/Time**; via **Open Related Record** you return to the document.
