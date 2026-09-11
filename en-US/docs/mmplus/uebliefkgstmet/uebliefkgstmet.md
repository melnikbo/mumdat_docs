---
title: Anwenderhandbuch m+m Logistic Differences with Unit Conversion
---

# User Guide m+m Logistic Differences with Unit Conversion

## Introduction

The **m+m Logistic Differences with Unit Conversion** extension is a pure connector app. It has no pages, cards, setup pages, or fields of its own; instead, it connects the two already existing modules **Over Under Delivery** (Logistic Differences) and **Unit Conversion (KG/Meter/Piece)** in the background. Its entire effect occurs automatically when warehouse receipts and warehouse shipments are posted.

Functionally, the app solves the following problem: when a warehouse receipt or warehouse shipment is posted and the quantity actually delivered or received differs from the quantity originally ordered or requested (over- or underdelivery), the unit conversion to **KG**, **Meter**, and **Piece** must be recalculated against the quantity actually posted. Without this connection, the converted values would remain based on the original quantity and would not match the posted quantity. The app ensures that the unit conversion is consistently recalculated on the basis of the quantity for every over- or underdelivery posting in the warehouse.

**Target audience:** This guide is primarily aimed at operational warehouse users who post **warehouse receipts** and **warehouse shipments** — especially in processes where over- or underdeliveries are permitted and where items are additionally managed in KG, Meter, and Piece. Secondarily, it concerns administrators who set up the underlying modules; the app itself requires no setup of its own.

**Short process overview:** The user posts a warehouse receipt or warehouse shipment with a quantity that differs from the original quantity. The **Over Under Delivery** module checks this deviation against the configured control method. During posting, this app resets the control field **Unit Field Modified** of the affected document line to **Quantity**, so that the **Unit Conversion** module recalculates the values **KG**, **Meter**, and **Piece** from the posted quantity.

## Quick Start for Users

The app works fully automatically. There is no action, button, or page that the user needs to open for this app. The benefit takes effect as soon as the two base modules are set up and the app is installed.

Prerequisite (one-time, by the administrator):

1. First, set up the **Unit Conversion** per item: enter the conversion factors **Theoretical KG per Meter** and **Theoretical KG per Piece** on the **Item Card**. When these factors are filled, the system calculates the KG, Meter, and Piece values from the quantity; without factors, these fields remain empty.
2. Then set up the **Over Under Delivery**: on the **Over Under Delivery Setup** page, define per process (Purchase, Sales, Transfer) whether over- and underdeliveries are controlled, and use the **Control Method** and the **Control Value** to define the range within which quantity deviations are permitted.
3. Make sure the **m+m Logistic Differences with Unit Conversion** app is installed. After that, no further configuration is required.

Day-to-day workflow (by the user):

1. Open the **warehouse shipment** or the **warehouse receipt** for the order or the purchase order.
2. Enter the quantity to actually be delivered or received in the line — even if it differs from the **Original Quantity**.
3. Post the document. If the deviation is recognized and accepted by the setup as an over- or underdelivery, the converted KG, Meter, and Piece values of the line are automatically recalculated from the posted quantity.
4. After posting, check the quantities and the converted KG/Meter/Piece values on the document line or on the posted document. They now match the quantity actually posted.

## Prerequisites and Setup

This app comes with **no setup pages and no fields of its own**. It is controlled exclusively through the setup of its three dependencies. Perform the setup in the following order, because the Unit Conversion provides the data basis for the later recalculation, and the Over Under Delivery is what first permits the deviating quantity.

### Set Up Unit Conversion per Item

Who sets it up: administrator or master data owner, before first use, per item. This setup provides the conversion factors with which the app later, during posting, updates the KG/Meter/Piece values. It takes effect in day-to-day work in the warehouse postings (see the **Daily Work** section).

The conversion is stored on the **Item Card**. If you want to use the automatic conversion between the KG, Meter, and Piece units in your processes, then setups are required per item.

| Setup | Explanation |
|-------------|-------------|
| **Theoretical KG per Meter** | If you enter a factor here, the system converts the quantity into the KG and Meter value; without this factor, the conversion between KG and Meter remains empty for items measured in linear meters. |
| **Theoretical KG per Piece** | If you enter a factor here, the system converts the quantity into the KG and Piece value; without this factor, the conversion between KG and Piece remains empty. |

Numbered steps:

1. Use the BC search (**Search**) to open the item list and open the **Item Card** of the affected item.
2. Enter the conversion factors **Theoretical KG per Meter** and/or **Theoretical KG per Piece**. If only one of the two factors is filled, then only the conversion between those two units is possible; the respective other unit remains empty. If no factors are filled at all, then KG, Meter, and Piece remain empty.
3. Repeat this for all items that are managed in the warehouse with deviating delivery quantities and unit conversion.

Completion of the chain: The actual benefit — the recalculation of KG/Meter/Piece against the posted quantity — takes effect later automatically when the warehouse receipt or warehouse shipment is posted (see **Daily Work**).

### Set Up Over Under Delivery

Who sets it up: administrator or purchasing/sales owner, before first use, company-wide and optionally per item. This setup determines whether a quantity deviating from the original quantity is permitted at all during posting — and thereby when the recalculation by this app is triggered in the first place. It takes effect in the **Daily Work** section.

On the **Over Under Delivery Setup** page, you define general rules per process. On the **General** tab, Boolean fields enable or disable control entirely per process; on the **Defaults** tab, you define the default behavior for over- and underdelivery.

| Setup | Explanation |
|-------------|-------------|
| **Purchase** | When enabled, the controls for over- and underdelivery apply throughout the entire purchasing process; if the switch is off, no checks take place in purchasing. |
| **Sales** | When enabled, the controls for over- and underdelivery apply throughout the entire sales process; without activation, sales remains unchecked. |
| **Transfer** | When enabled, the controls apply in the transfer process; without activation, quantity deviations on transfers are not controlled. |
| **Control Method** | Determines how a permitted deviation is calculated. **Default:** The standard behavior of Business Central applies; no additional rule takes effect. **Percentage:** The permitted over- or underdelivery is calculated as a percentage share of the original quantity. **Absolute Value:** The permitted deviation is calculated as a fixed amount added to or subtracted from the original quantity. |
| **Control Value** | When the Control Method **Percentage** or **Absolute Value** is selected, this value defines the permitted amount of the deviation; with the **Default** method it has no effect. |
| **Warning** | When enabled, the user can exceed the quantity limit by confirmation and still perform the posting; if the warning is not enabled, an error message prevents the impermissible quantity. Every confirmed exceedance is logged. |

Numbered steps in dependency order:

1. Use the BC search (**Search**) to open the **Over Under Delivery Setup** page.
2. On the **General** tab, enable the processes (**Purchase**, **Sales**, **Transfer**) for which quantity deviations are to be controlled. When a process is enabled, over- and underdeliveries are checked there.
3. On the **Defaults** tab, define the **Control Method** and the **Control Value**. With this you determine which deviation from the **Original Quantity** may be posted at all.
4. Decide, via the **Warning** field, whether a deviation is allowed by confirmation (warning active) or prevented by an error message (warning inactive).
5. Optional: Use the **Over Under Delivery Item Setup** to store item-specific special rules if individual items require deviating tolerances.

Completion of the chain: Only when a deviation is permitted here and the user posts a deviating quantity in the warehouse is the control field **Unit Field Modified** set to **Quantity** by this app and the conversion recalculated (see **Daily Work**).

## Daily Work: Posting Warehouse Receipts and Warehouse Shipments with a Quantity Deviation

The daily effect of this app is controlled by the pages described in the **Prerequisites and Setup** section: the **Item Card** provides the data basis via the conversion factors, and the **Over Under Delivery Setup** decides whether a deviating quantity is permitted. The app itself has no fields and no actions of its own in these documents; it intervenes exclusively at the moment of posting.

### What the App Does Automatically During Posting

When a warehouse shipment or a warehouse receipt with a deviating quantity is posted, the app sets the **Unit Field Modified** field of the document line to the value **Quantity**. This tells the Unit Conversion module that it must derive the calculated values from the quantity, and it recalculates **KG**, **Meter**, and **Piece** using the item's theoretical factors — matching the quantity actually posted rather than the original quantity.

This happens in two posting paths:

1. **Standard warehouse posting:** when posting warehouse receipts and warehouse shipments via the standard warehouse documents.
2. **Over-/underdelivery posting:** when the Over Under Delivery module transfers the deviating quantity into the associated purchase or sales line during posting.

In both cases, the behavior is identical for the user: they enter and post the actual quantity; the converted values follow automatically.

### Process at the Warehouse Shipment (Sales/Transfer)

| Field | Explanation |
|------|-------------|
| **Original Quantity** | Shows the quantity originally requested for the line. If the quantity actually delivered differs from it, this value serves the Over Under Delivery module as the reference for the tolerance check. |
| **Qty. to Ship** | Enter the quantity actually to be delivered here. If this value differs from the Original Quantity, the deviation is checked against the setup and, during posting, the unit conversion is recalculated. |
| **Complete** | When set, the system treats the line with the reduced quantity as fully delivered and does not allow any further delivery; the field can only be set if the underdelivery rules permit it. |
| **Unit Field Modified** | Control field for the unit conversion. This app sets it to **Quantity** automatically during posting, so that KG, Meter, and Piece are derived from the posted quantity. The user does not have to maintain this field themselves. |

Steps:

1. Open the **warehouse shipment** for the relevant document.
2. Enter the quantity actually to be delivered in the line in the **Qty. to Ship** field.
3. If the quantity deviates, confirm or prevent the over-/underdelivery according to the setup (warning or error).
4. If needed, set **Complete** when the line is finally delivered with the reduced quantity.
5. Post the warehouse shipment. The app sets **Unit Field Modified** to **Quantity**; the KG, Meter, and Piece values are recalculated from the posted quantity.

### Process at the Warehouse Receipt (Purchase)

The warehouse receipt behaves as a mirror image of the warehouse shipment.

| Field | Explanation |
|------|-------------|
| **Original Quantity** | Shows the quantity originally ordered for the line as the reference for the tolerance check on over- or underdelivery. |
| **Qty. to Receive** | Enter the quantity actually received here. If it differs from the Original Quantity, the system checks the deviation against the setup and recalculates the unit conversion during posting. |
| **Complete** | When set, the purchase order line is considered fully completed with the received quantity; further warehouse receipts against this line are then no longer possible. |
| **Unit Field Modified** | Set automatically to **Quantity** by the app during posting, so that KG, Meter, and Piece are derived from the received quantity. |

Steps:

1. Open the **warehouse receipt** for the relevant purchase order.
2. Enter the quantity actually received.
3. Confirm or prevent a quantity deviation according to the setup.
4. Post the warehouse receipt. The app sets **Unit Field Modified** to **Quantity**; the converted values are recalculated from the received quantity.

## Typical Use Cases

### Underdelivery in Sales with Unit Conversion

**Trigger:** A warehouse employee picks a sales order for a steel item that is managed in Piece and at the same time converted into KG and Meter. During picking it turns out that only a smaller quantity can be delivered; the customer accepts the partial quantity as a complete delivery.

**Entry point in BC:** The employee opens the **warehouse shipment** belonging to the sales order.

**Core flow:** In the line, they enter the quantity that can actually be delivered in the **Qty. to Ship** field, which is below the **Original Quantity**. Since **Sales** is enabled and the **Warning** is switched on in the **Over Under Delivery Setup** module, they confirm the underdelivery. They set **Complete** because no remaining delivery is to follow. They then post the warehouse shipment.

**Completion:** During posting, the app sets **Unit Field Modified** to **Quantity**. The unit conversion recalculates KG and Meter from the quantity of pieces actually delivered. On the posted document, quantity, KG, and Meter match.

### Overdelivery in Purchasing with Unit Conversion

**Trigger:** During the warehouse receipt of a coil delivery, the vendor delivers somewhat more than ordered. The excess quantity is permitted within the agreed tolerance.

**Entry point in BC:** The goods receipt employee opens the **warehouse receipt** for the purchase order.

**Core flow:** They enter the actually received, higher quantity. Since **Purchase** is enabled in the **Over Under Delivery Setup** module and a **Control Method** with a **Control Value** is stored for overdeliveries, the system checks the excess quantity. If it is within the tolerance, it is accepted; otherwise, depending on the setting, a **Warning** or an error message appears. They post the warehouse receipt.

**Completion:** During posting, the app sets **Unit Field Modified** to **Quantity**; KG, Meter, and Piece are recalculated from the received excess quantity and are shown consistently on the line.

## FAQ and Troubleshooting

### Do I have to set up anything for this app?
No. The **m+m Logistic Differences with Unit Conversion** app has no setup page and no fields of its own. Only the base modules **Unit Conversion** (on the **Item Card**) and **Over Under Delivery** (on the **Over Under Delivery Setup** page) are set up.

### Why do my KG/Meter/Piece values change only after posting?
Because the app intervenes precisely at the moment the warehouse receipt or warehouse shipment is posted. At that point, it sets the **Unit Field Modified** field to **Quantity**, whereupon the unit conversion derives the values from the posted quantity.

### Why do KG, Meter, and Piece remain empty even though a quantity was posted?
Because no conversion factors are stored on the **Item Card**. Without **Theoretical KG per Meter** and/or **Theoretical KG per Piece**, the system cannot calculate the derived values and leaves them empty.

### Why is only one of the KG/Meter/Piece units calculated?
Because only one of the two theoretical factors is filled on the **Item Card**. In that case, only the conversion between the two linked units is possible; the respective other unit remains empty.

### Why does the system not allow a deviating delivery or receipt quantity at all?
Because no deviation is permitted in the **Over Under Delivery Setup** module for the relevant process. If the **Control Method** is set to **Default** or the process (**Purchase**, **Sales**, **Transfer**) is not enabled, no extended tolerance applies and the unit conversion is not re-triggered by this app.

### Why do I get an error message during posting instead of a prompt?
Because the **Warning** field is not enabled in the setup. If the **Warning** is switched off, an error message prevents the impermissible quantity; only with the **Warning** enabled can the user override the deviation by confirmation.

### Is it logged when I confirm an over- or underdelivery?
Yes. Every over- or underdelivery confirmed via **Warning** is recorded by the base module in the over-/underdelivery logs. This app adds nothing to that and does not change the logging behavior.

### Do I have to set the Unit Field Modified field myself?
No. This control field is set to **Quantity** automatically by the app during posting. Manual intervention is not required in the interplay of these posting paths.

### Does the recalculation also apply to transfers?
The app intervenes in the posting paths for warehouse receipt and warehouse shipment. For transfers, the **Transfer** process must be enabled separately in the **Over Under Delivery Setup** module so that a deviating quantity is permitted there at all.

### What happens if I set Complete but delivered less?
Then the system treats the line with the reduced quantity as fully completed and does not allow any remaining delivery. The **Complete** field can only be set if the underdelivery rules permit it; the unit conversion is recalculated against the reduced quantity during posting.
