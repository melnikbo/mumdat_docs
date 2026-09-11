---
title: Anwenderhandbuch m+m Subcontracting Steel
---

# m+m Subcontracting Steel User Guide

## Introduction

The **m+m Subcontracting Steel** extension enhances the **m+m Subcontracting** module (Subcontract Order) with functions for the steel industry. It adds three building blocks to the existing subcontract order:

- the **quantity-accurate capture in KG, Meter and Piece** on group lines, order lines and order entries – in parallel to the standard quantity and at every posting stage (outbound, inbound, to invoice, invoiced),
- the **capture and posting of scrap quantities** on the group line, which is distributed proportionally to the related production orders on inbound,
- the **integration with the Prod. Order Job** (automatic finishing on inbound) and with **shipment planning** (shipment tours on the header, subcontract orders in shipment planning).

The extension brings **no pages of its own**. All fields and actions appear on the existing pages of the subcontract order as well as in shipment planning. The user therefore continues to work with the familiar documents; this guide describes **which additional fields and actions** are added there and **how they steer the daily workflow**.

**Target audience.** The guide is aimed primarily at **operational users** who work with the subcontract order every day: they capture group and order lines, post outbound and inbound, enter scrap quantities, invoice and plan shipment. Addressed secondarily are **administrators and key users** who perform the setup (global setup flags, quantity conversion, shipment tours, permissions).

**Brief process overview.** The user creates a **subcontract order** or has it generated from a production or sales process. On the **group lines** they capture, alongside the quantity, the values in **KG**, **Meter** and **Piece**, optionally via **Matchcode**/**Start Material Search**. They post the **outbound** to the subcontractor, later the **inbound** back; on inbound, **scrap quantities** are posted proportionally and – when setup is active – the related **Prod. Order Job** lines are automatically finished. The order is then **invoiced**. For the physical logistics, the open subcontract orders can be scheduled in **shipment planning**.

---

## Quick Start for Users

The following steps lead to the result in dependency order (first setup, then document, then posting). Details are in the respective chapters.

1. **Check setup (one-time, administrator).** Open **Subcontract Order Setup** and define whether **Finish POJ on Inbound** should be activated. Ensure that the quantity conversion (KG/Meter/Piece) and – if shipment planning is used – the **shipment tours** are set up (see the **Setup** chapter).
2. **Open the subcontract order.** Select the desired **subcontract order** and switch to the **subcontract order group lines**.
3. **Capture quantity and units.** Enter the **Quantity** in the group line; the fields **KG**, **Meter** and **Piece** are filled via the item's quantity conversion or can be overwritten manually. Alternatively, choose **Start Material Search** or enter a **Matchcode** to adopt the item and capture quantities.
4. **Post outbound.** Post the outbound to the subcontractor. The values in **Outbound KG/Meter/Piece** flow into **Posted Outbound KG/Meter/Piece**.
5. **Capture scrap quantity (if offcuts occur).** Before the inbound, enter the **Scrap Qty.** in the group line.
6. **Post inbound.** Post the return. This updates **Inbound KG/Meter/Piece** into **Posted Inbound KG/Meter/Piece**, posts the **Scrap Qty.** proportionally to the production orders (**Posted Scrap Qty.**) and – when setup is active – automatically finishes the matching **Prod. Order Job** lines.
7. **Invoice.** Invoice the group lines; **KG/Meter/Piece to Invoice** are transferred to **KG/Meter/Piece Invoiced**.
8. **Plan shipment (optional).** Open **shipment planning** and choose the **Subcontract Orders** action to schedule the open outbound and inbound movements of the subcontract orders.

---

## Setup

The setup of this extension comprises one global flag on the document setup as well as several **prerequisites in dependent modules** (quantity conversion, material search, shipment tours) that must be active so that the steel-specific fields and actions take effect in the daily workflow. All information originates from the program code of this extension.

### Subcontract Order Setup – Prod. Order Job

This setup is performed once per company by the **administrator**. It controls whether the completion of the external operations in the **Prod. Order Job** happens automatically on return.

**Access:** Open the central **Subcontract Order Setup** page (the company-wide setup card of the subcontracting module). As this is a company-wide single-record setup without a superordinate list, access is via the setup of the subcontracting module or via **Search**.

| Setup | Explanation |
|-------|-------------|
| **Finish POJ on Inbound** | When activated, posting the **inbound** of a group line automatically sets the lines belonging to the operation in the **Prod. Order Job** to **finished**. The user therefore does not need to additionally close the operation manually in the Prod. Order Job. When deactivated, the Prod. Order Job remains unchanged and the completion of the operations must be done separately there. Automatic finishing requires the dependent module *m+m Production Order Job Overview*. |

#### Setting up Finish POJ on Inbound

This process chain connects a global setting with an action in the daily workflow. It is configured by the **administrator** before first use and takes effect in the **Daily Work** chapter (post inbound).

1. **Create prerequisite.** Ensure that the **Prod. Order Job** module (m+m Production Order Job Overview) is installed and that the external operations of the affected production orders are managed there. If this prerequisite is missing, no operation can be finished on inbound.
2. **Set the global flag.** In **Subcontract Order Setup**, activate the **Finish POJ on Inbound** flag. When set, the system links each inbound posting with the matching work center, the production order and the operation and marks the found Prod. Order Job lines as finished.
3. **Completion in the daily workflow.** The operational user later posts the **inbound** of the group line (see **Daily Work**). With this posting the chain is closed: the external operation is considered completed without the user having to open the Prod. Order Job separately.

### Setting up quantity conversion for subcontract orders

The steel-specific quantity fields **KG**, **Meter** and **Piece** are not captured freely but derived from the item master data via the **quantity conversion**. This setup resides in the dependent module *m+m Unit Conversion* and is the prerequisite for the fields on group and order lines being filled automatically.

This is configured by the **administrator/key user** before first use; the values are applied in the **Daily Work** chapter during line capture.

1. **Define the units of conversion.** In the quantity conversion setup, specify which units of measure count as the **KG**, **Meter** and **Piece** unit. When these units are set, the system recognizes the matching base size when the item changes and converts the remaining sizes.
2. **Maintain theoretical conversion values on the item.** Enter the theoretical conversion values (KG per meter, KG per piece) on the item. When maintained, **KG**, **Meter** and **Piece** are automatically calculated from a captured **Quantity**; if the values are missing, the derived sizes remain empty and must be captured manually.
3. **Application in the daily workflow.** As soon as the user changes **Quantity**, **KG**, **Meter** or **Piece** in the group line or switches the **Item No.**, the system recalculates the remaining quantity fields consistently (see **Daily Work**). This keeps the quantity and the steel-typical units in sync across all posting stages.

> Note on material search: Via the **Matchcode** and the **Start Material Search** action on the group lines, the **item search** of the module *m+m Material Properties* is called. Its setup takes place entirely in that dependent module; this extension merely embeds the search into the group line and adopts item, variant, unit as well as the **capture quantity** in KG/Meter/Piece.

### Setting up shipment planning for subcontract orders

So that open subcontract orders appear in **shipment planning** and shipment tours can be assigned, the shipment tours of the module *m+m Logistic Management* must be set up.

Configured by the **administrator/planner**; the result is used in the **Daily Work** (header fields) and **Shipment Planning** chapters.

1. **Create shipment tours.** Maintain the **shipment tour** master data (with carrier and carrier service). When shipment tours exist, they can be selected on the subcontract order as **Outb. Ship. Tour Code** and **Inb. Ship. Tour Code**.
2. **Assign shipment tours on the document.** The user selects the tour codes on the subcontract order (see **Daily Work**). When set, the system adopts the carrier and the carrier service from the tour into the corresponding outbound and inbound carrier fields of the document.
3. **Scheduling in shipment planning.** In **shipment planning**, the planner runs the **Subcontract Orders** action. When executed, the system collects all released or in-progress subcontract orders with an open outbound or inbound quantity and makes them available for tour planning (see the **Shipment Planning** chapter).

### Permissions

The extension delivers a permission set (**MuM FOST Permission**) that bundles the access rights to the additional table fields and the new logic. The administrator assigns this permission set to the users or user groups who work with subcontract orders. The permission set determines the permissions for the steel-specific extension fields and complements the permissions of the base module; it defines which actions the users may perform on the extended fields.

---

## Daily Work on the Subcontract Order

The subcontract order is the central document of this extension. The steel-specific fields are distributed across the **document header**, **group lines**, **order lines** and the **document overview**. The actual posting logic (outbound, inbound, invoicing) is provided by the base module; the extension adds the values in KG/Meter/Piece and the scrap quantity to every stage.

**Controlling setup:** The behavior of this document is controlled by the **Subcontract Order Setup** page (flag **Finish POJ on Inbound**), by the **quantity conversion** (KG/Meter/Piece derivation, see Setup) as well as by the **shipment tour** master data. Before working here, these setups should be complete.

### Document header – shipment tours and shipment planning

The document header of the subcontract order receives fields for tour control and counters for shipment planning. Functionally they follow on from the standard fields **Outbound/Inbound Target Location Code** and are located on the **Outbound & Inbound** tab.

| Field | Explanation |
|-------|-------------|
| **Outb. Ship. Tour Code** | When a shipment tour code is set for the outbound, the system adopts the carrier and the carrier service from the associated **shipment tour** into the outbound carrier fields of the document; in addition, the document is assigned to this tour when collected in shipment planning. Without an entry, the outbound remains tour-neutral. |
| **Inb. Ship. Tour Code** | When a shipment tour code is set for the inbound, the system similarly adopts carrier and carrier service into the inbound carrier fields and assigns the inbound to this tour in shipment planning. Without an entry, the inbound remains tour-neutral. |
| **Shipment Planning Lines** | Shows the number of still-open (unregistered) shipment planning lines for this subcontract order. When the value is greater than 0, a scheduling already exists that has not yet been registered – an indication that shipment is prepared but not yet completed. |
| **Reg. Shipment Planning Lines** | Shows the number of already **registered** shipment planning lines for this subcontract order. When the value is greater than 0, shipment for this document has already been firmly scheduled. |

### Document overview (subcontract order list)

In the overview of the subcontract orders, the shipment planning key figures are additionally available, so that the planner can recognize the planning status per document without opening the document.

| Field | Explanation |
|-------|-------------|
| **Outb. Ship. Tour Code** | Outbound shipment tour code of the document. The column is delivered hidden by default and can be shown when needed via personalization; when shown, it indicates which tour the outbound is assigned to. |
| **Inb. Ship. Tour Code** | Inbound shipment tour code of the document. Likewise hidden by default; when shown, it indicates the tour assignment of the inbound. |
| **Shipment Planning Lines** | Number of open shipment planning lines of the document. When greater than 0, a scheduling is prepared but not yet registered. |
| **Reg. Shipment Planning Lines** | Number of registered shipment planning lines of the document. When greater than 0, shipment is firmly scheduled. |

### Subcontract order group lines

The group line is the central working level: here the user captures quantity and units, starts the material search and enters the scrap quantity. The steel-specific quantity fields accompany every posting stage of the base quantity (outbound, inbound, to invoice, invoiced) and are kept consistent via the quantity conversion – except for **Scrap Qty.** and **Matchcode**.

#### Material search and Matchcode

| Field / Action | Explanation |
|----------------|-------------|
| **Matchcode** | When a matchcode is entered, the system opens the **item search** (Material Properties) with this matchcode as a filter and adopts the selected item together with variant, unit and capture quantity into the line. If the **Item No.** is subsequently cleared, the matchcode is also removed so that line and matchcode remain consistent. |
| **Start Material Search** (action) | Opens the **item search** without a prior matchcode. When the user adopts a hit, the system fills Item No., Variant Code, Unit of Measure Code, Matchcode as well as **KG**, **Meter**, **Piece** from the capture and validates the **Quantity**. This allows a group line to be filled via search instead of direct entry. |

#### Quantities in KG, Meter and Piece

The following fields are available for each posting stage. They are linked via the quantity conversion with the respective base quantity (Quantity, outbound quantity, inbound quantity, quantity to invoice).

| Field | Explanation |
|-------|-------------|
| **KG** | Weight of the planned group line quantity in kilograms. When the user changes KG, the system recalculates **Meter** and **Piece** as well as the base **Quantity** according to the item conversion; the line can thus be captured either weight-, length- or piece-driven. |
| **Meter** | Length of the group line quantity in meters. When changed, KG, Piece and Quantity are recalculated consistently. |
| **Piece** | Piece count of the group line quantity. When changed, KG, Meter and Quantity are recalculated consistently. |
| **Outbound KG** / **Outbound Meter** / **Outbound Piece** | Outbound quantity still to be posted in KG/Meter/Piece. When the base **outbound quantity** is changed, these values are carried along automatically; they indicate which weight or which length/piece count goes to the subcontractor at the next outbound. |
| **Posted Outbound KG** / **Posted Outbound Meter** / **Posted Outbound Piece** | Quantity already delivered to the subcontractor in KG/Meter/Piece. These values are increased with each outbound posting and are not editable; they document the cumulative material outflow. |
| **Inbound KG** / **Inbound Meter** / **Inbound Piece** | Inbound quantity still to be posted in KG/Meter/Piece (return from the subcontractor). When the base **inbound quantity** is changed, these values are carried along. If the posted outbound exceeds the posted inbound, the system automatically proposes the difference as the open inbound quantity. |
| **Posted Inbound KG** / **Posted Inbound Meter** / **Posted Inbound Piece** | Inbound quantity already reported back (posted) in KG/Meter/Piece. Increased with each inbound posting and not editable; documents the cumulative return. |
| **KG to Invoice** / **Meter to Invoice** / **Piece to Invoice** | Quantity still to be invoiced in KG/Meter/Piece. When the base **quantity to invoice** is changed, these values are recalculated; they determine which weight/which length enters the next invoicing. |
| **KG Invoiced** / **Meter Invoiced** / **Piece Invoiced** | Quantity already invoiced in KG/Meter/Piece. Increased with each invoicing and not editable. |

#### Scrap Qty.

| Field | Explanation |
|-------|-------------|
| **Scrap Qty.** | Quantity of the offcuts/scrap incurred during the external operation, which the user captures before the inbound. When a value is captured and the **inbound** is posted, the system distributes the not-yet-posted scrap quantity (**Scrap Qty. − Posted Scrap Qty.**) proportionally by line quantity to the production orders of the associated order lines and updates it into **Posted Scrap Qty.**. If the value is 0 or already fully posted, no scrap posting occurs. |
| **Posted Scrap Qty.** | Scrap quantity already posted. Increased on the inbound posting by the distributed scrap quantity and not editable; indicates how much scrap has already been allocated to the production orders. |

> Posting order (from the program code): On **post outbound**, the outbound units are transferred into the posted outbound units. On **post inbound**, first the inbound units are transferred into the posted inbound units, then the **Scrap Qty.** is posted proportionally and – when the setup **Finish POJ on Inbound** is active – the matching Prod. Order Job lines are finished. On **invoicing**, the "to invoice" units are updated into "invoiced". Partial postings are allowed; the document does not have to be posted completely in one go.

### Subcontract order group lines – list view (group list)

The list view of the group lines shows the same quantity fields in KG/Meter/Piece as the line view (Quantity, Outbound, Posted Outbound, Inbound, Posted Inbound, to invoice, invoiced) as well as **Scrap Qty.** and **Posted Scrap Qty.**. The columns serve to give a quick overview of the processing status of multiple lines and update with the respective postings. Matchcode and the **Start Material Search** action are not available in this list view; they are reserved for the detailed line view.

### Order lines

On the **order lines** of the subcontract order, the units **KG**, **Meter** and **Piece** of the line quantity are additionally maintained.

| Field | Explanation |
|-------|-------------|
| **KG** | Weight of the order line quantity in kilograms. When the value is captured or adopted from the source document (production order, sales line, item ledger entry), the system recalculates Meter, Piece and Quantity of the line consistently. |
| **Meter** | Length of the order line quantity in meters; consistent with KG, Piece and Quantity. |
| **Piece** | Piece count of the order line quantity; consistent with KG, Meter and Quantity. |

The values of the order lines are filled from the respective source document on creation and summed into the associated group line; this keeps the header, group and line levels aligned in a quantity-accurate manner.

---

## Shipment Planning

Shipment planning (module *m+m Logistic Management*) bundles the outbound and inbound movements to be planned from various document types. This extension makes **subcontract orders** available as a source type of their own in shipment planning.

**Controlling setup:** The prerequisites are set-up **shipment tours** and **Outb./Inb. Ship. Tour Codes** set on the document (see **Setup** and **Daily Work**).

### Adopting subcontract orders into planning

**Access:** Open **shipment planning** and choose the **Subcontract Orders** action.

When the action is executed, the system collects all subcontract orders with status **Released** or **In Progress** and provides a planning line per group line – both for the **outbound** (route to the subcontractor) and for the **inbound** (return). Only lines with a still-open quantity are considered:

- for the **outbound**, as long as the quantity is greater than the posted outbound quantity,
- for the **inbound**, as long as the quantity is greater than the posted inbound quantity,
- and only if no planning line for this source/direction exists yet.

The planning lines carry the open quantities in **KG**, **Meter** and **Piece** as well as the net/gross weight (from the open KG). As the delivery address, the ship-to address of the document is used for the outbound, and the address of the target location (**Inbound Target Location Code**) for the inbound; the dates used are the **Outbound Date** and **Inbound Date** respectively, and the tour is the respective **Outb./Inb. Ship. Tour Code**.

### Direction of the planning line

On the group line, the (system-set, non-editable) field **Ship. Planning Direction** controls for which transport direction a planning line is created:

- **(blank):** No direction has been determined for the line yet; on collection it is assigned to a direction depending on the open outbound/inbound quantity.
- **Outbound:** The planning line concerns the **outbound** to the subcontractor; the quantity used is the open outbound quantity, the address is the ship-to address of the document.
- **Inbound:** The planning line concerns the **inbound** (return); the quantity used is the open inbound quantity, the address is the target location of the inbound.

### From shipment planning back to the document

From within shipment planning, the underlying subcontract orders can be called up directly: via the document selection of shipment planning, the **subcontract order overview** is opened for the source type **Subcontract Order**; from a single planning line, the associated **subcontract order** is shown. This way the planner switches between planning and document without a detour.

---

## History: Subcontract Order Entries

Posted transactions are managed in the base module as **subcontract order entries**. This extension adds the units of the respective posting to the entries so that the posted material flow is also traceable in a quantity-accurate manner.

| Field | Explanation |
|-------|-------------|
| **KG** | Weight of the posted quantity of this entry in kilograms. The value is adopted into the entry from the respectively posted unit of the group line on outbound, inbound or invoicing and documents the quantity-accurate posting history. |
| **Meter** | Length of the posted quantity of this entry in meters; adopted analogously from the posting. |
| **Piece** | Piece count of the posted quantity of this entry; adopted analogously from the posting. |

Via the entries, it is possible to trace per posting (outbound, inbound, invoicing) which weight, which length and which piece count were moved – in addition to the standard entry quantity.

---

## FAQ and Troubleshooting

### 1. Why are KG, Meter and Piece filled automatically after capturing the quantity?
Because the steel-specific quantity fields are linked with the base quantity via the **quantity conversion** (module *m+m Unit Conversion*). When you change **Quantity**, **KG**, **Meter** or **Piece**, the system recalculates the respective other sizes from the item conversion values (KG per meter, KG per piece). You can use any of the sizes as the leading size.

### 2. What happens if no conversion values are stored on the item?
Then KG/Meter/Piece cannot be derived automatically from the quantity and remain empty or must be captured manually. Maintain the theoretical conversion values on the item so that the derivation works (see **Setting up quantity conversion for subcontract orders**).

### 3. Why does the matchcode change when I remove the item?
When the **Item No.** field is cleared, the **Matchcode** of the group line is reset automatically. This prevents a matchcode from remaining without an associated item and being misleading in the next search.

### 4. How do I fill a group line faster than by direct entry?
Use the **Start Material Search** action or enter a **Matchcode**. Both open the **item search**; when a hit is adopted, Item No., Variant Code, Unit of Measure Code, Matchcode as well as KG/Meter/Piece and the quantity are adopted into the line.

### 5. When is the scrap quantity actually posted?
Only on **post inbound**. The system posts the still-open scrap quantity (**Scrap Qty. − Posted Scrap Qty.**) and distributes it proportionally by line quantity to the production orders of the order lines. Before the inbound posting, the scrap quantity is only captured but not posted.

### 6. Why was my captured scrap quantity not posted on inbound?
Because the still-open scrap quantity is 0 or negative – for example when **Posted Scrap Qty.** has already reached the captured **Scrap Qty.**. The system posts only a positive remaining quantity; if none is open, the scrap posting is omitted.

### 7. Do I still have to finish the external operation manually in the Prod. Order Job?
Only if the **Finish POJ on Inbound** flag in **Subcontract Order Setup** is deactivated. If it is activated, the system finishes the matching Prod. Order Job lines automatically with the inbound posting.

### 8. Why is no operation finished on inbound despite active setup?
The automatic completion requires the **Prod. Order Job** module (m+m Production Order Job Overview) and needs a matching assignment of work center, production order, production order line and operation. If the system finds no matching Prod. Order Job lines, there is nothing to finish.

### 9. Why does a subcontract order not appear in shipment planning?
Only subcontract orders with status **Released** or **In Progress** are adopted, and only group lines with an **open** outbound or inbound quantity for which **no** planning line exists yet. If the quantity is already fully posted or already scheduled, no new planning line is created.

### 10. Can I plan the outbound and inbound of a subcontract order separately and post in partial quantities?
Yes. Outbound and inbound are planned separately via the **Ship. Planning Direction** field as **Outbound** or **Inbound**. Postings are allowed in partial quantities; the posted units (Posted Outbound/Inbound KG/Meter/Piece) are increased continuously until the quantity is complete.

---

## Typical Use Cases

### Use case 1: Have steel profiles processed externally with KG/Meter capture

**Trigger.** A production order contains an external operation; the steel profiles are to be taken to a subcontractor, processed there and brought back. The responsible user receives the note from production.

**Access in BC.** The user opens the associated **subcontract order** and switches to the **subcontract order group lines**.

**Core flow.**
1. In the group line, they select the item via **Start Material Search** (item search) or via **Matchcode**; item, variant, unit and capture quantity are adopted. Alternatively, they capture **Quantity**; **KG**, **Meter** and **Piece** are filled via the quantity conversion.
2. They post the **outbound** to the subcontractor; **Outbound KG/Meter/Piece** are transferred into **Posted Outbound KG/Meter/Piece**.
3. After the return, they post the **inbound**; **Inbound KG/Meter/Piece** are updated into **Posted Inbound KG/Meter/Piece**.
4. They invoice; **KG/Meter/Piece to Invoice** transfer into **KG/Meter/Piece Invoiced**.

**Completion.** The posted material flow is traceable in a quantity-accurate manner (KG/Meter/Piece) in the **subcontract order entries**.

### Use case 2: Return with offcuts and automatic completion of the operation

**Trigger.** The subcontractor reports the inbound of the processed parts and communicates an incurred offcut/scrap quantity.

**Access in BC.** The user opens the **subcontract order** and the relevant **group line**. Prerequisite: In the **Subcontract Order Setup**, **Finish POJ on Inbound** is activated (see **Setup**).

**Core flow.**
1. They enter the reported **Scrap Qty.** in the group line.
2. They post the **inbound**. The system first updates the inbound units, then distributes the open **Scrap Qty.** proportionally by line quantity to the production orders of the order lines and increases **Posted Scrap Qty.**.
3. With the same inbound posting, the system automatically sets the matching **Prod. Order Job** lines to **finished**.

**Completion.** The external operation is considered completed, the scrap is allocated to the production orders, and the return is documented as a **subcontract order entry** – without the user having to open the Prod. Order Job separately.
