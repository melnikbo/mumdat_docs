---
title: Anwenderhandbuch m+m Unit Conversion
---

# User Manual m+m Unit Conversion

## Introduction

The m+m app **Unit Conversion** (app title: *m+m Unit Conversion*) extends Microsoft Dynamics 365 Business Central with a parallel quantity representation in the three units **KG**, **Meter** and **Piece** – in addition to the standard quantity (**Quantity**). On virtually every item-bearing document, journal and ledger entry, the associated values in KG, Meter and Piece are therefore available alongside the familiar quantity. When a user enters a value in one of the three units, the app automatically calculates the standard quantity as well as the two remaining units based on the stored conversion factors.

**Target audience.** The primary target audience is **operational users** who process documents and journals on a daily basis: purchase clerks, sales clerks, warehouse and production staff who record quantities, assign lots, and post inbound receipts, outbound shipments, consumption and output. The secondary target audience is **administrators and master data owners** who perform the global **KG Meter Piece Setup** and, per item, maintain the conversion factors, the **Qty. Consistency Confirmation** and the rounding.

**Brief process overview.** The administrative entry point is a one-time global **KG Meter Piece Setup** (which unit of measure codes represent KG, Meter and Piece). The master data owner then maintains, per item on the **Item Card**, the theoretical conversion factors, the **Qty. Consistency Confirmation** and, optionally, the rounding. In day-to-day operations, the user records quantities on document lines and journal lines either in **Quantity**, **KG**, **Meter** or **Piece**; the remaining values are calculated automatically. If an item has active **Item Tracking** (lots or serial numbers), the user can deliberately deviate from the theoretical factors – this is referred to as an **inconsistency** and is carried forward across all subsequent documents and ledger entries.

## Quick Start for Users

The following order reflects the dependencies from the code: first the global setup, then the master data per item, and then the daily document work.

1. **Global setup (one-time, administrator).** Use **Search** to open the **KG Meter Piece Setup** page and enter the **KG Unit of Measure Code**, **Meter Unit of Measure Code** and **Piece Unit of Measure Code**. Without these three codes, the entire conversion remains ineffective.
2. **Prepare item (master data owners).** From the item list, open the **Item Card** of the relevant item. Check the **Base Unit of Measure** and, in the **Factors:** area, enter the **Theoretical KG per Meter** and/or **Theoretical KG per Piece**. If required, set the **Qty. Consistency Confirmation** and the values in the **KG:/Meter:/Piece:** areas (**Rounding Precision** and **Rounding Direction**).
3. **Activate item tracking (only if inconsistencies are desired).** If the user is to be able to deviate from the theoretical factors, assign an **Item Tracking Code** on the item card and select *Never Change Quantity* or *Change Quantity On Confirm* in the **Qty. Consistency Confirmation**.
4. **Record document line (operational user).** Create, for example, a sales order or a purchase order. As soon as you enter the item in the line, the fields **KG**, **Meter** and **Piece** are calculated automatically. You can overwrite the value directly in **KG**, **Meter** or **Piece** as you wish – the **Quantity** and the remaining units are recalculated.
5. **Assign lot/serial and, if applicable, create an inconsistency.** Open the item tracking lines, assign a lot and, if required, adjust KG, Meter or Piece. Depending on the **Qty. Consistency Confirmation**, the prompt **“Do you want to recalculate all quantity fields?”** appears.
6. **Post document (standard).** Post the document as usual (inbound/outbound shipment, purchase/sales invoice, output, consumption). The KG, Meter and Piece values – including any inconsistencies – are transferred to the posted documents as well as to item, value, capacity and warehouse (bin) ledger entries.

## Setup

The setup of the Unit Conversion is divided into a **global** base setup (one page per company) and the **item-related** setup on the item card (see chapter *Master Data*). Both build on each other: without the global assignment of the unit of measure codes, the item-related factors do not take effect.

### KG Meter Piece Setup

**Process intro.** This page is configured by the **administrator once per company**, before the app is used for the first time. It defines which **unit of measure codes** created in Business Central are interpreted by the app as KG, as Meter and as Piece. Only once all three codes are set does the app perform a conversion on items and documents (in the code, `GetAndTestSetup` checks all three fields; if one is missing, the conversion aborts silently). The factors maintained on the item card (see *Master Data*) require this setup.

**Entry point:** Use **Search** to open the **KG Meter Piece Setup** page and click the link of the same name. The page is a single record (card) and is created automatically when opened.

| Setup | Explanation |
|---|---|
| **KG Unit of Measure Code** | When set, the app treats the selected unit of measure code system-wide as the weight unit KG. Only items whose **Base Unit of Measure** matches one of the three codes maintained here are converted; without this entry, no KG conversion takes place and the KG fields remain empty. |
| **Meter Unit of Measure Code** | When set, the selected unit of measure code applies system-wide as the length unit Meter. As a result, the Meter fields are available on documents and journals and are calculated from the theoretical factors; if the entry is missing, the Meter column has no value. |
| **Piece Unit of Measure Code** | When set, the selected unit of measure code applies system-wide as the piece unit. Only then are the Piece fields populated and transferred to subsequent documents; without an entry, the Piece conversion does not take place. |

The **Units** area consolidates the three assignments. The technical field **Primary Key** is a system-internal key field and has no meaning for the user.

> **Prerequisite/dependency.** The three unit of measure codes must already exist in the standard **Units of Measure** setup of Business Central. As long as not all three fields are filled, no conversion takes place – not even on items that have already been prepared. The actual activation per item then takes place via the theoretical factors on the item card (see *Master Data → Item Card*).

### Permissions

The app ships with the permission set **KG Mtr. Piece**. The administrator assigns this permission set to the users or user groups; it determines the permissions for the objects provided by the app (setup table, conversion logic and the additional fields) and defines which actions users may perform within the scope of the Unit Conversion. The assignment is made via the standard management of permission sets in Business Central.

## Master Data

After the global setup, the conversion is activated and controlled per item. Master data maintenance determines **whether** an item is converted (theoretical factors), **how** manual deviations are handled (Qty. Consistency Confirmation) and **how precisely** rounding occurs (rounding precision/direction). In addition, lot/serial control the actual factors and the work center controls the times calculation.

### Set up Unit Conversion per item (Item Card)

**Process intro.** This setup is performed by the **master data owner** as soon as an item is to be managed in KG, Meter and Piece – usually when the item is first created or converted. The **theoretical factors** maintained here are required by the system to calculate the KG, Meter and Piece values in all processes (see *Usage Examples*). If only one of the two factors is filled, only the conversion between those two units is possible; the respective other unit remains empty. If both factors are empty, all three quantity fields remain empty.

**Entry point:** From the **item list**, open the **Item Card** of the item. There, the app adds the areas **Factors:**, **Qty. Consistency Conf.:** as well as **KG:**, **Meter:** and **Piece:**.

#### Factors and Rounding

| Setup | Explanation |
|---|---|
| **Theoretical KG per Meter** | When filled, the app converts between KG and Meter on all documents and journals (Meter = KG ÷ factor, or KG = Meter × factor). In addition, with standard conversion active, the app automatically creates the matching **item unit of measure**. Prerequisite: the item's **Base Unit of Measure** is one of the three codes stored in the global setup, otherwise the entry is rejected with a field message. Already posted ledger entries prevent a change of the factor. |
| **Theoretical KG per Piece** | When filled, the app converts between KG and Piece. With base unit Piece and an empty factor, the factor “KG per Meter” is also reset and the associated item unit of measure is removed. Same prerequisite and lock on posted ledger entries as with “Theoretical KG per Meter”. |
| **KG Rounding Precision** | When greater than 0, every automatically calculated KG quantity is rounded to this precision (e.g. 0.001). At 0, no rounding takes place and the rounding direction is set to **No Rounding**; a negative value is rejected with a field message. |
| **KG Rounding Direction** | Determines the direction in which calculated KG values are rounded. Only editable when a rounding precision > 0 is stored. See values below. |
| **Meter Rounding Precision** | When greater than 0, calculated Meter values are rounded to this precision; at 0, no rounding. |
| **Meter Rounding Direction** | Determines the rounding direction for calculated Meter values; only editable with precision > 0. See values below. |
| **Piece Rounding Precision** | When greater than 0, calculated Piece values are rounded to this precision; at 0, no rounding. |
| **Piece Rounding Direction** | Determines the rounding direction for calculated Piece values; only editable with precision > 0. See values below. |

**Values of the rounding direction (KG, Meter, Piece alike):**

- **No Rounding:** The calculated value is truncated to the precision, without rounding up or down.
- **Round Up:** The calculated value is always rounded up to the next precision step.
- **Round Down:** The calculated value is always rounded down to the next precision step.
- **Commercially Rounded:** The calculated value is rounded commercially (from 5 upwards it is rounded up, up to 4 it is rounded down). This value is preset automatically as soon as a precision > 0 is set for the first time.

> If a rounding precision is set to 0, the app automatically sets the associated rounding direction to **No Rounding**; conversely, when a rounding direction is set to **No Rounding**, the precision is reset to 0.

#### Qty. Consistency Confirmation and inconsistencies

| Setup | Explanation |
|---|---|
| **Qty. Consistency Confirmation** | Determines how the system reacts when a user enters a deviating value in one of the three quantity fields KG, Meter or Piece in an item tracking line. The selected value decides whether **inconsistencies** (deviations from the theoretical factors) may arise at all. See values below. |

**Values of the Qty. Consistency Confirmation:**

- **Always Change Quantity:** A manually changed value always overwrites the values calculated via the theoretical factors; the remaining quantity fields are recalculated automatically. Inconsistencies are **not** possible. In this mode, the conversion uses the standard function of Business Central; when the theoretical factors are entered, the corresponding **item units of measure** are created automatically.
- **Never Change Quantity:** Values not changed manually are **never** recalculated automatically when a value is entered in KG, Meter or Piece. If the user enters a manual value, an inconsistency always arises. In this mode, the system requires an **Item Tracking Code** to be set; the conversion is performed via the app instead of via the standard item units of measure. All existing item units of measure except the base unit are removed, and the attempt to create a new item unit of measure is rejected with an error message.
- **Change Quantity On Confirm:** When a value is changed manually, the dialog **“Do you want to recalculate all quantity fields?”** appears. If the user confirms with *Yes*, the remaining fields are calculated automatically via the theoretical factors; with *No*, the deviating value is retained and an inconsistency arises. This mode too requires an **Item Tracking Code** and removes the additional item units of measure as with “Never Change Quantity”.

**Process steps to enable inconsistencies (in dependency order):**

1. **First** ensure the global setup: the three unit of measure codes are set in the **KG Meter Piece Setup**.
2. **Then** assign an **Item Tracking Code** on the item card (mandatory for “Never Change Quantity” and “Change Quantity On Confirm”).
3. **Next** enter the theoretical factors **Theoretical KG per Meter** and/or **Theoretical KG per Piece**.
4. **Finally** set the **Qty. Consistency Confirmation** to *Never Change Quantity* or *Change Quantity On Confirm*.
5. **In day-to-day operations**, the user can then record KG, Meter or Piece deviatingly in the item tracking lines of a document (see *Usage Examples*).

> **Relationship to daily work.** With conversion active, the fields KG, Meter and Piece are populated automatically on the document lines; the Qty. Consistency Confirmation controls whether the assignment of a lot or a manual entry creates an inconsistency. Processes that post a **new** lot (e.g. purchase order, output in production, receipt via the item journal) allow inconsistencies to be created. Processes that use an **existing** lot (e.g. lot selection in the sales order, consumption lot in production) calculate with the factors already present and no longer allow any change.

#### Item overview columns (inventory)

The app extends the **Item Card** and the **item list** with read-only key figures in KG, Meter and Piece. These mirror existing standard quantity fields of Business Central in the three units and update automatically from the ledger entries and open documents. They are documented here as a group, as they do not represent maintainable setup:

- **Inventory** in KG, Meter and Piece (sum of item ledger entries) – visible on the item card and item list.
- **On order** key figures (purchase, sales, production, components, service, project, assembly, assembly component) each in KG, Meter and Piece – an informational mirror of the respective standard “quantity on …” fields.
- **Reserved** quantities in KG, Meter and Piece (inventory as well as purchase/sales orders).

### Set up times calculation per work center (Work Center Card)

**Process intro.** This setting is maintained by the master data owner per **work center** in production. It determines which of the units is used for the work center's times calculation, thereby extending the Unit Conversion with the capacity reference.

**Entry point:** From the work center list, open the **Work Center Card** and select the field **Times Calculation Unit** (in the unit cost calculation area).

| Setup | Explanation |
|---|---|
| **Times Calculation Unit** | Determines which unit the times calculation of this work center refers to. When a specific value is selected, the capacity or time determination is performed on the basis of this unit. See values below. |

**Values of the Times Calculation Unit:**

- **Quantity:** The times calculation is based on the standard quantity.
- **KG:** The times calculation is based on the KG quantity.
- **Meter:** The times calculation is based on the Meter quantity.
- **Piece:** The times calculation is based on the Piece quantity.

### Actual factors per lot/serial (Lot No. / Serial No. Information Card)

**Process intro.** While the item card specifies the **theoretical** factors, an **actual** (measured) factor can be stored per individual lot or serial number. This is maintained by the warehouse or quality owner when a specific lot deviates from the theoretical value. When converting a document, the priority rule applies: if an actual factor is maintained on the **Serial No. Information Card**, it is used; otherwise the factor of the **Lot No. Information Card**; otherwise the theoretical factor of the item card (in the code: `GetActualKGPer`).

**Entry point:** You open the information card from the **item tracking lines** of a document or from the item's lot/serial number overview, by selecting the relevant lot or serial number.

| Field | Explanation |
|---|---|
| **Theoretical KG per Meter** / **Theoretical KG per Piece** | Adoption of the theoretical factors from the item card as the initial value for this lot/serial. |
| **Actual KG per Meter** | When filled, the app uses this measured factor for all conversions of this lot instead of the theoretical value – thereby the documents reflect the real characteristics of the lot. |
| **Actual KG per Piece** | When filled, this measured value applies to the conversion between KG and Piece of this lot/serial and takes priority over the theoretical factor. |
| **Inventory KG / Meter / Piece** | Read-only inventory of the lot/serial in the three units. |
| **Expired Inventory KG / Meter / Piece** | Read-only portion of the stock whose expiration date has passed, in the three units. |

> The **Serial No. Information Card** carries the same fields with identical meaning; it is not listed separately here. Attempts to delete a lot or serial number information card for which item ledger entries already exist are rejected by the system with an error message (e.g. “You cannot delete the Lot No. Information Card because one or more item ledger entries exist.”).

## Inconsistencies – the central concept

An **inconsistency** exists when the KG, Meter and Piece values of a line do **not** correspond to the theoretical ratio stored on the item card. Inconsistencies are intended and reflect real deviations (e.g. a lot that weighs more per meter than the theoretical average).

- Inconsistencies are **only** possible when the item has **active item tracking** (lots or serial numbers) and the **Qty. Consistency Confirmation** is set to *Never Change Quantity* or *Change Quantity On Confirm*.
- With **Always Change Quantity**, inconsistencies are excluded; the conversion runs via the standard item units of measure of Business Central.
- Inconsistencies are created in processes with a **new** lot (purchase order, output, item journal). In processes with an **existing** lot, the factors are fixed.
- Once recorded, inconsistencies are carried forward across the entire document chain and into the item, value, capacity and warehouse (bin) ledger entries.

## Daily Work on Documents and Journals

The app adds the units KG, Meter and Piece on all relevant documents and journals – in purchasing, sales, in transfer, in service, in projects, in assembly, in production, as well as in warehouse and item journals. The operating principle is the same everywhere; it is described representatively on the sales line.

### Quantity entry on the document line

As soon as an item (with maintained factors) is entered in a line, the app populates the associated fields **KG**, **Meter** and **Piece**. The user can record the quantity in each of the units:

| Field | Explanation |
|---|---|
| **KG** | When the user enters a value here, the app recalculates the **Quantity**, the **Meter** and the **Piece** from the stored factor and remembers that KG was last used for entry. The line's standard quantity is validated accordingly. |
| **Meter** | When the user enters a value here, Quantity, KG and Piece are derived from the factor; the line uses Meter as the leading entry unit. |
| **Piece** | When the user enters a value here, Quantity, KG and Meter are derived from the factor; the line uses Piece as the leading entry unit. |
| **Quantity** (standard) | When the user changes the standard quantity, the app recalculates KG, Meter and Piece from the theoretical factors. |

> If the user changes the **Unit of Measure Code** or the **Item No.** of the line, the app re-determines the valid factors and recalculates the units. If the user changes the **Location Code**, the quantity to ship in the three units is updated.

The conversion applies to all quantity-bearing fields of the line – besides the quantity, also the quantity to ship, shipped, to invoice and invoiced, the outstanding quantity, and the reserved quantity; each in KG, Meter and Piece. On the sales line overview, the columns **KG**, **Meter** and **Piece** are shown by default; further unit variants (e.g. to ship) can be shown via the column selection.

### Overviews and drill-downs

- **Procurement planning:** The lines of the order planning show additionally **KG to Order**, **Meter to Order** and **Piece to Order** – the quantity to be procured per unit.
- **Applied item ledger entries:** The application overview shows **Applied KG**, **Applied Meter** and **Applied Piece** – the portion applied in the three units.
- **Production journal:** The lines show additionally **Consumption KG**, **Consumption Meter** and **Consumption Piece**.
- **Item, value, capacity and warehouse (bin) ledger entries** carry the posted KG, Meter and Piece values per posting, so that the three units remain visible throughout the entire traceability.

## Usage Examples (typical use cases)

The following workflows correspond to the calculation and posting logic stored in the code as well as the guided processes of the Unit Conversion. All examples presuppose that the global **KG Meter Piece Setup** has been performed and that the item has theoretical factors as well as – for inconsistencies – an Item Tracking Code.

### Purchase order with inbound receipt

1. **Trigger.** A vendor delivers material that is managed in-house in KG, Meter and Piece; purchasing creates a purchase order for it.
2. **Entry point in BC.** Open the **purchase order** and enter the item no. in the line. The fields **KG**, **Meter** and **Piece** are calculated automatically, as are the associated values for the current shipment, the quantity already received, the reserved quantity, the current invoice and the inbound overage quantity.
3. **Core workflow.** Open the **item tracking lines** and assign a **lot**. The lot is initially created with the theoretical factors of the item card. Now change, for example, the **Meter**, while KG and Piece are to remain constant: with **Change Quantity On Confirm**, the dialog **“Do you want to recalculate all quantity fields?”** appears – confirm with *No* to create an **inconsistency**. When leaving the item tracking lines, the inconsistencies are transferred to the posting-relevant quantity fields of the order line.
4. **Completion.** Create and post the **inbound receipt** and then the **purchase invoice**. All quantity fields including the inconsistency are transferred to the posted purchase receipt, the item and value ledger entries as well as – for locations with bins – the warehouse (bin) ledger entries.

### Production including consumption

1. **Trigger.** A production order is to be produced and the material consumption posted in the three units.
2. **Entry point in BC.** Create a **production order** (any status; posting is done on released orders). The Unit Conversion fields are present on all statuses and are calculated with the theoretical factors on creation – also in the production order components.
3. **Core workflow.** Open the **production journal**; depending on the manufacturing setup, consumption and output lines appear with the fields **Consumption KG/Meter/Piece**. In the item tracking of the consumption line, select an **existing lot**; its inconsistencies are adopted – the conversion factors can no longer be changed here. For the output, a **new lot** can be created via item tracking, for which you – e.g. with *Change Quantity On Confirm* – deliberately create new inconsistencies by confirming with *No*.
4. **Completion.** Run the **Post** function in the production journal. Through the output, the fields on the production order are updated; item, value and capacity ledger entries (as well as possibly warehouse/bin ledger entries) are created with the respective inconsistencies. The **Times Calculation Unit** maintained for the work center determines which unit the times calculation is based on.

### Sales order with outbound shipment and pick

1. **Trigger.** A customer orders material that is managed in KG, Meter and Piece.
2. **Entry point in BC.** Open the **sales order** and enter the item no. The fields **KG**, **Meter** and **Piece** are calculated for quantity, quantity to ship and shipped, reserved quantity, quantity to invoice and invoiced.
3. **Core workflow.** Assign an **existing lot** in the **item tracking lines**. Its inconsistencies are adopted into the sales line; the conversion factors are fixed for an existing lot. From the document, create the **outbound shipment** and from it the **pick**; the quantity fields of the pick lines mirror the lot and its inconsistencies.
4. **Completion.** **Register** the pick and **post** the outbound shipment; the values including inconsistencies pass to the registered pick, the posted sales shipment, the item and value ledger entries as well as, if applicable, the warehouse (bin) ledger entries. Finally, post the **sales invoice**, whose lines adopt the inconsistencies of the shipment.

## FAQ and Troubleshooting

### 1. Why are no KG, Meter or Piece values calculated on my document lines?
Because a prerequisite is missing. The app only calculates when all three unit of measure codes are set in the **KG Meter Piece Setup**, the item's **Base Unit of Measure** matches one of these codes, and at least one theoretical factor is maintained on the item card. If any of these is missing, the unit fields remain empty.

### 2. Why can't I enter a theoretical factor on the item card?
Because the item's **Base Unit of Measure** does not match any of the three units (KG, Meter, Piece) stored in the global setup. In this case, the system rejects the entry with a field message on the base unit of measure code. First check the global setup and the item's base unit.

### 3. Why can the theoretical factor of an item no longer be changed?
Because **ledger entries or open documents/journals** already exist for this item. The app checks this (`TestNoOpenEntriesExist`) and prevents a subsequent factor change, so that already calculated quantities do not become inconsistent.

### 4. When does an inconsistency arise and when not?
An inconsistency arises only when the item has active **item tracking** and the **Qty. Consistency Confirmation** is set to *Never Change Quantity* or *Change Quantity On Confirm* and the user enters a unit value deviating from the factors. With *Always Change Quantity*, the values are always recalculated – inconsistencies are then excluded.

### 5. Why does the prompt “Do you want to recalculate all quantity fields?” appear?
Because for the item the **Qty. Consistency Confirmation** = *Change Quantity On Confirm* is set. Confirm with *Yes* to recalculate the remaining units from the factors, or with *No* to keep your deviating value (an inconsistency).

### 6. Why were my additional item units of measure deleted when switching to “Never Change Quantity”?
Because in the modes *Never Change Quantity* and *Change Quantity On Confirm*, the conversion is performed via the app instead of via the standard item units of measure. The app therefore removes all item units of measure except the base unit and prevents the creation of new item units of measure with an error message. In these modes, an **Item Tracking Code** is also mandatory.

### 7. Why do calculated KG/Meter/Piece deviate slightly from one another?
Because a **rounding precision** and a **rounding direction** apply per unit. Depending on the setting (No Rounding, Round Up, Round Down, Commercially Rounded), the calculation result is rounded differently. Check the rounding fields in the KG:/Meter:/Piece: area of the item card.

### 8. Why can't I select the rounding direction?
Because the associated **rounding precision** is still 0. The rounding direction field is only editable when a precision > 0 is stored. Enter a precision first.

### 9. Why can't I change the conversion factors when consuming an existing lot?
Because in processes with an **existing** lot (e.g. consumption lot in production, lot selection in the sales order) the factors of the lot are fixed. New inconsistencies arise only in processes that post a **new** lot (purchase order, output, item journal).

### 10. Why can't a Lot No. or Serial No. Information Card be deleted?
Because **item ledger entries** already exist for this lot or serial number. The system rejects the deletion attempt with an error message, in order to preserve the traceability of the posted quantities.
