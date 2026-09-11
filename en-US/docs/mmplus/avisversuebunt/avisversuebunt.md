---
title: Anwenderhandbuch m+m Logistic Management with Logistic Differences
---

# User Guide m+m Logistic Management with Logistic Differences

## Introduction

This extension is a link between two m+m apps that already exist: **m+m Logistic Management** (advice notification and shipment planning) and **m+m Logistic Differences** (over- and underdelivery control). It ensures that the rules for over- and underdelivery take effect not only when posting standard documents, but already **during advice notification and shipment planning**, whenever quantities are assigned to document lines there.

Functionally, the extension adds an additional control to the planning lines: the **Order Complete** flag (in advice notification as well as in shipment planning). With this flag, the user signals that no further deliveries or receipts will follow for the affected source line despite a quantity difference. Without this flag, the extension checks when the **Qty. to Assign** is entered whether the planned quantity is permitted according to the rules stored in **m+m Logistic Differences**, and blocks or confirms it accordingly.

**Target audience.** This guide is primarily aimed at the **operational users** in goods receipt, shipping, and logistics who process advice notifications and shipment plannings every day and assign quantities in the process. Secondarily, it concerns **administrators and key users** who set up the over- and underdelivery rules in **m+m Logistic Differences** – without this setup, the additional control has no effect.

**Short process overview.** In the **m+m Logistic Differences** setup, the administrator defines whether and to what extent over- and underdeliveries are allowed in purchasing and sales. The operational user then enters the quantity to be assigned in the **Advice Notification** or in the **Shipment Planning**; the extension checks this quantity against the rules. If the sum of the already posted, already assigned, and newly assigned quantity deviates from the original quantity, the user sets the **Order Complete** flag if required to deliberately close the line.

## Quick Start for Users

The fastest path to a correctly checked quantity assignment. The setup (step 1) is a one-time prerequisite performed by the administrator; steps 2 to 5 belong to the daily work.

1. **Check the setup (prerequisite, administrator).** On the **Over Under Delivery Setup** page (app **m+m Logistic Differences**), make sure that **Purchase** or **Sales** is activated and that a suitable **Control Method** is stored in the defaults or in the item setup. Without an active setup, no additional check takes place (see chapter **Setup**).
2. **Open the planning line.** Open the relevant **Advice Notification** or **Shipment Planning** and, in the lines, select the source line for which you want to assign a quantity.
3. **Enter the Qty. to Assign.** In the **Qty. to Assign** field, enter the quantity you want to allocate to this line. When you leave the field, the extension checks the permitted over-/underdelivery. If the rule is violated, you receive – depending on the setup – a warning with a confirmation option or an error message.
4. **For underdelivery: set the flag.** If the line is to be closed despite a lower quantity, set the **Order Complete** checkbox in the line. The flag can only be set if the underdelivery rules allow it (see chapter **Daily Work**).
5. **Register or post.** Continue with the usual process of the app **m+m Logistic Management**: release and **Register** the advice notification or the shipment planning. The flag is thereby transferred to the follow-up documents (warehouse receipt, warehouse shipment, purchase/sales line) and to the registered lines.

## Setup

This extension has **no setup page of its own**. Its behavior is controlled entirely by the setup of the dependent app **m+m Logistic Differences**. The following section therefore describes which settings there activate the additional check in advice notification and shipment planning and how they interact. The field values are evaluated by the program code of this extension (among others, the flags for active over-/underdelivery as well as the control method).

### Setting up over- and underdelivery

**Process intro.** This setup is performed by the **administrator or key user once before first use**. It determines whether the quantity assignment in advice notification and shipment planning is additionally checked at all and how strictly. If no over-/underdelivery is active, the assignment behaves as in the standard, and the **Order Complete** flag has no effect. The values set here are consumed by the daily work areas **Advice Notification** and **Shipment Planning** (cross-reference: chapters **Daily Work in Advice Notification** and **Daily Work in Shipment Planning**).

**Getting there:** Use the **Search** action to open the **Over Under Delivery Setup** page. This company-wide setup (one record per company) has no superordinate document line and is therefore opened – as intended in the app **m+m Logistic Differences** – via the search.

The following settings of the **Over Under Delivery Setup** page and of the associated item setup control the behavior of this extension:

| Setup | Explanation |
|-------------|-------------|
| **Purchase** | If activated, the over-/underdelivery controls take effect throughout the purchasing process. Only then does this extension check the **Qty. to Assign** in advice notifications for purchase orders; if it is deactivated, the quantity is accepted without an additional check. |
| **Sales** | If activated, the controls take effect throughout the sales process. Only then does this extension check the **Qty. to Assign** in shipment plannings for sales and transfer lines; without activation, the additional check is omitted. |
| **Control Method** | Determines how a deviation is evaluated. **Default:** The standard behavior of Business Central applies without an additional limit. **Percentage:** The permitted over- or underdelivery is calculated as a percentage of the original quantity. **Absolute Value:** The permitted deviation results from a fixed quantity value. If the assignment deviates outside the limit determined this way, it is – depending on **Warning** – blocked or presented for confirmation. |
| **Control Value** | If set, this value defines the concrete limit for the chosen **Control Method** (percentage or absolute quantity). It is related to the original quantity in order to determine the maximum permitted over- or underdelivery quantity against which the **Qty. to Assign** is checked. |
| **Warning** | If activated, the user receives a warning on a rule violation that can be confirmed or declined; if declined, the permitted quantity is accepted. If deactivated, an impermissible **Qty. to Assign** is rejected with an error message and must be corrected. |

**Control types in the defaults/item setup (the "Defines" field).** For each rule it is specified whether it concerns an over- or an underdelivery:

- **Overdelivery:** The rule takes effect when more is delivered or assigned than originally planned in the purchase, sales, or transfer process. In this extension it is evaluated when the sum of the posted, assigned, and newly assigned quantity **exceeds** the original quantity.
- **Underdelivery:** The rule takes effect when less is delivered or assigned. In this extension it is evaluated when the sum **falls below** the original quantity. Only when an underdelivery is permitted can the **Order Complete** flag be set.

**Applies-to Type (scope of the rule).** In the item setup, the **Applies-to Type** determines for which business-partner or document scope a specific rule applies. This extension evaluates the rule per source of the planning line:

- **Vendor** / **All Vendors:** For advice notifications from purchase orders. The check is performed against the vendor of the underlying purchase line.
- **Customer** / **All Customers:** For shipment plannings from sales orders. The check is performed against the customer of the underlying sales line.
- **Transfer:** For shipment plannings from transfer orders. The check is performed against the source location of the transfer line.

Using the **Applies-to Type** and **Applies-to No.** fields, the rule is narrowed down to a specific vendor, customer, or a specific transfer if required.

**Numbered activation steps (dependency order).** This is how an administrator activates the additional quantity check in advice notification and shipment planning end to end:

1. **First**, open **Over Under Delivery Setup** and activate **Purchase** (for advice notification) or **Sales** (for shipment planning). If activated, the controls are switched on in principle in the respective process.
2. **Next**, in the **Defaults** or in the **item setup**, define the **control types** (**Defines** = Overdelivery/Underdelivery), the **Control Method**, and the **Control Value**. If set, this determines the permitted range of the quantity deviation.
3. **Then**, use the **Warning** field to decide whether a rule violation appears as a confirmable warning or as a hard error message.
4. **Finally**, the operational user uses the settings in the daily routine: they enter the **Qty. to Assign** in the advice notification or shipment planning and, for a permitted underdelivery, set the **Order Complete** flag (cross-reference: chapter **Daily Work**).

**Dependency note.** The program code of this extension reads the active purchase/sales flags and the control method from the setup of **m+m Logistic Differences**. If these are not present or not active, every additional check is omitted, and the **Order Complete** flag has no controlling effect.

## Daily Work in Advice Notification

The advice notification comes from the app **m+m Logistic Management** and is used to plan advised quantities for a purchase order and to register them later. This extension adds the **Order Complete** flag to the **Advice Notification Lines** and enables the over-/underdelivery check during quantity assignment.

**Controlling setup.** Whether and how a check is performed results from the **Over Under Delivery Setup** page (the **Purchase**, **Control Method**, **Control Value**, **Warning** flags; see chapter **Setting up over- and underdelivery**). If purchase is not activated there, the additional check is omitted.

**Getting there:** Open the **Advice Notification** from the purchase order or via the advice notification list of the app **m+m Logistic Management** and switch to the **Advice Notification Lines**.

### Fields of the advice notification line (added by this extension)

In addition to the standard columns of the app **m+m Logistic Management** (among others **Item No.**, **Description**, **Location Code**, **Variant Code**, **Unit of Measure Code**, **Quantity**, **Outstanding Quantity**, **Qty. to Assign**), the advice notification line shows the following field added by this extension:

| Field | Explanation |
|------|-------------|
| **Order Complete** | If activated, the user signals that the source line is closed despite a shortfall in quantity and that no further receipts are expected. The flag can only be set if the underdelivery rules of the setup allow it; if no underdelivery is permitted, the checkbox is reset automatically. When registering, the value is transferred to the purchase line or the warehouse receipt, so that the outstanding quantity is not planned any further. |

**Interaction with the Qty. to Assign.** When you enter the **Qty. to Assign** in the line, the extension checks upon leaving the field the sum of the already posted quantity (**Quantity Received**), the already assigned quantity, and the new quantity against the **original quantity**:

- If the sum is **above** the original quantity and no overdelivery is permitted, the quantity is rejected or presented for confirmation.
- If the sum is **below** the original quantity and no underdelivery is permitted, this counts as a partial receipt; the line remains open. Only when underdelivery is permitted and the **Order Complete** flag is set is the line closed.

## Daily Work in Shipment Planning

The shipment planning also comes from the app **m+m Logistic Management** and plans shipment quantities for sales orders and transfer orders. This extension adds the **Order Complete** flag to the **Shipment Planning Lines** and enables the over-/underdelivery check during quantity assignment.

**Controlling setup.** Whether and how a check is performed results from the **Over Under Delivery Setup** page (the **Sales**, **Control Method**, **Control Value**, **Warning** flags; see chapter **Setting up over- and underdelivery**). If sales is not activated there, the additional check is omitted.

**Getting there:** In the **Shipment Planning assignment and warehouse control** (app **m+m Logistic Management**, reachable via **Search**), open the desired line, first set a **customer filter**, use the **Select Lines** action to choose the orders to be processed, and then switch to the **Shipment Planning Lines**.

### Fields of the shipment planning line (added by this extension)

In addition to the standard columns of the app **m+m Logistic Management** (among others **Selected**, **Item No.**, **Description**, **Location Code**, **Variant Code**, **Unit of Measure Code**, **Quantity**, **Outstanding Quantity**, **Qty. to Assign**, **Open**), the shipment planning line shows the following field added by this extension:

| Field | Explanation |
|------|-------------|
| **Order Complete** | If activated, the user signals that the source line (sales or transfer line) is closed despite a shortfall in quantity and that no further deliveries will take place. The flag can only be set if the underdelivery rules of the setup allow it; otherwise the checkbox is reset automatically. When registering, the value is transferred to the sales line or the warehouse shipment, so that the outstanding quantity is not planned any further. |

**Source of the line (customer or transfer).** Based on the source, the extension recognizes which rule applies: for a sales line it checks against the rules for **Customer** / **All Customers**, for a transfer line against the rule for **Transfer**. The check mechanism via the **Qty. to Assign** corresponds to that of the advice notification (see above).

## Posting and registration flow

This extension does not introduce a posting run of its own; it hooks into the existing check points of the app **m+m Logistic Management**. The flow in which the flag and the quantity check take effect is:

1. **Select the line** in the **Advice Notification** or in the **Shipment Planning assignment and warehouse control**.
2. **Enter the Qty. to Assign** in the line. The extension checks the permitted over-/underdelivery. With **Warning** = active a confirmation prompt appears, with **Warning** = inactive an error message.
3. **For a permitted underdelivery**, set the **Order Complete** flag in the line to deliberately close the source line.
4. **Release** the advice notification or shipment planning in the usual process of the app **m+m Logistic Management**.
5. **Register** the advice notification or shipment planning. In doing so, the extension transfers the flag to the follow-up documents: to the **purchase line** or **sales line**, to the **warehouse receipt** or **warehouse shipment**, and to the **registered** advice notification or shipment planning line.
6. **Post** the warehouse receipt or warehouse shipment in the standard process of Business Central. If the flag is set, the remaining outstanding quantity is not carried forward as an open underdelivery.

**Note on partial quantities.** As long as underdelivery is permitted, lines may be deliberately closed with a lower quantity; balancing the outstanding quantity is not enforced. Without a set flag, a line that falls short remains open and can be supplemented in further deliveries.

## History, registered documents, and archive

The flag is carried not only in the active planning lines, but also in the downstream data sets, so that the decision made remains traceable:

| Area | Explanation |
|---------|-------------|
| **Registered advice notification** (registered advice notification line) | When registering, the value of the **Order Complete** flag is transferred from the advice notification line to the registered line and remains visible there as a closed decision. |
| **Registered shipment planning** (registered shipment planning line) | When registering, the value of the **Order Complete** flag is transferred from the shipment planning line to the registered line. |
| **Advice notification line (archive)** | The archived advice notification line also carries the **Order Complete** flag, so that archived transactions reflect the state set at the time. |

These data sets contain the flag as a field; the extension does not add any actions or list filters of its own here.

## FAQ and Troubleshooting

### 1. Why is my Qty. to Assign rejected with an error message?
The entered quantity violates an over- or underdelivery rule, and in the **Over Under Delivery Setup** the **Warning** field is not activated for this case. Without a warning, an impermissible quantity is rejected hard. Correct the quantity or – if desired for business reasons – adjust the setup.

### 2. Why does only a warning appear instead, which I can confirm?
Because the **Warning** field is activated in the setup. In that case you may deliberately confirm a deviation; if you decline, the permitted quantity is accepted.

### 3. Why can I not set the "Order Complete" flag?
The flag can only be set for a **permitted underdelivery**. If no underdelivery is allowed in the current case, or if there is no underdelivery at all, the checkbox is removed automatically again when saving.

### 4. What exactly does the flag do?
It signals that the source line is closed despite a lower quantity. The outstanding quantity is no longer planned as an open underdelivery, and the value is transferred when registering to the purchase/sales line, warehouse receipt/warehouse shipment, and the registered line.

### 5. Why does no additional check happen at all during quantity assignment?
Because in the **Over Under Delivery Setup** neither **Purchase** (for advice notification) nor **Sales** (for shipment planning) is activated, or no control rule has been stored. This extension only evaluates an existing, active setup.

### 6. Does the check also apply to transfers in shipment planning?
Yes. If the shipment planning line comes from a transfer order, the extension checks against the rule with **Applies-to Type** = **Transfer** and the source location of the transfer line.

### 7. Which quantity does the check use – the document quantity or another quantity?
The decisive one is the **original quantity** of the source line. It is compared with the already posted quantity, the already assigned quantity, and the newly entered **Qty. to Assign**.

### 8. Why does my checkbox disappear after I changed the quantity on the purchase order?
If the quantity of the source line is changed, further receipts or deliveries become possible again; a previously set "complete" flag is therefore reset. Set it again after the last assignment.

### 9. Why is the field called "Order Complete" in both advice notification and shipment planning?
Both labels map to the same English UI caption **Order Complete**. In German they read *Bestellung komplett* in advice notification (referring to purchase orders) and *Auftrag komplett* in shipment planning (referring to sales or transfer orders). Functionally the flag has the same effect in both cases.

### 10. Do I have to balance the outstanding quantity exactly before I may close?
No. With a permitted underdelivery you may deliberately close the line with a lower quantity via the flag. A forced balancing of the outstanding quantity to zero only exists if your setup does not allow underdeliveries.

## Typical use cases

### Use case 1: A purchase order is underdelivered and deliberately closed

1. **Trigger.** A supplier reports by phone that it can only deliver part of the ordered quantity and that no remaining delivery will follow.
2. **Entry in BC.** The user opens the **Advice Notification** from the purchase order and switches to the **Advice Notification Lines**.
3. **Core flow.** They enter the actually advised partial quantity in the **Qty. to Assign** field. Since underdelivery is permitted in purchasing, the extension reports – depending on **Warning** – a confirmable warning. To close the line definitively, the user sets the **Order Complete** checkbox. They then release the advice notification.
4. **Conclusion.** When **registering** the advice notification, **Order Complete** is transferred to the purchase line and the warehouse receipt. After posting the warehouse receipt, no open outstanding quantity remains for further planning.

### Use case 2: A sales order is overdelivered in shipment planning

1. **Trigger.** Shipping reports internally that a slightly higher quantity is to be shipped for a customer than provided for in the order.
2. **Entry in BC.** The user opens the **Shipment Planning assignment and warehouse control**, filters via the **customer filter** on the customer, uses **Select Lines** to choose the order line, and opens the **Shipment Planning Lines**.
3. **Core flow.** They enter the higher quantity in the **Qty. to Assign** field. If an overdelivery with **Control Method** and **Control Value** is stored in sales and the quantity is within the limit, it is – depending on **Warning** – accepted or presented for confirmation; if it exceeds the limit, an error message appears.
4. **Conclusion.** After **Release** and **Register** of the shipment planning, the checked quantity flows into the warehouse shipment and the posted sales shipment.

### Use case 3: Closing a transfer with a partial quantity

1. **Trigger.** In a transfer between two locations, less stock is available than planned; the remainder is no longer transferred.
2. **Entry in BC.** The user opens the **Shipment Planning** for the transfer and switches to the **Shipment Planning Lines**.
3. **Core flow.** They enter the available **Qty. to Assign**. The extension checks against the rule with **Applies-to Type** = **Transfer**. If the underdelivery is permitted, the user sets **Order Complete** to close the transfer line.
4. **Conclusion.** After **registering**, the flag is transferred to the warehouse shipment of the transfer; the quantity not transferred does not remain as an open underdelivery.
