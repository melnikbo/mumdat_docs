---
title: Anwenderhandbuch m+m Drop- and Special Shipment
---

# User Guide m+m Drop- and Special Shipment

## Introduction

The **m+m Drop- and Special Shipment** app extends Microsoft Dynamics 365 Business Central with a largely automated handling of **drop shipments**, **special orders** and **release business**. It links the **sales order** to the **purchase order** created from it, so that Sales and Purchasing work on the same transaction together without having to link the documents manually.

The three business types differ in the goods flow and in the posting logic:

- **Drop Shipment:** The vendor ships the item directly to the customer; the goods do not pass through your own warehouse. Sales order and purchase order are linked. As soon as Purchasing posts the purchase receipt, the sales shipment of the sales order is posted automatically in the background.
- **Special Order:** The ordered goods first arrive at your own company (e.g. for repacking or further processing) and are only then shipped to the customer. Here the sales shipment is **not** posted automatically, but manually by Sales.
- **Release Business:** An extension of the special order. In addition, the ship-to fields ("Ship-to") from the sales order are transferred to the purchase order, so the vendor can ship directly to the destination address stored in the order. When **Release Business** is set, **Special Order** is set automatically as well.

### Target Audience

The primary target audience is the **operational users in Sales and Purchasing** who record, release and post orders and purchase orders on a daily basis: Sales creates the sales order, flags the line via the **Purchasing Code**, selects the **Vendor No.** and triggers the purchase order; Purchasing processes the created purchase order and posts the receipt and invoice. Secondarily, this guide is aimed at **administrators and key users** who set up the **purchasing codes** and the **locations** once (see chapter *Setup*).

### Short Process Overview

The user flags a sales line via a suitably configured **Purchasing Code** and a location released for that purpose, releases the sales order and automatically creates the associated **purchase order** through an action. The transaction is then posted in Purchasing and Sales depending on the business type. Setting up the purchasing codes and locations is therefore the prerequisite for the daily work and is described first.

## Quick Start for Users

The quick start shows the shortest path from a configured system to the created purchase order. The setup (steps 1–2) is performed once by the administrator; the daily work (from step 3 on) takes place in Sales.

1. **Set up purchasing code** (once, administrator): In **Purchasing Codes**, create a code and, depending on the business type, activate **Drop Shipment**, **Special Order** or **Release Business** (see *Setup › Purchasing Codes*).
2. **Release location** (once, administrator): On the desired **Location** (Location Card page), set the appropriate flags **Drop Shipment**, **Special Order** and/or **Release Business** (see *Setup › Locations*).
3. **Create sales order:** Open a new **Sales Order** and record the customer as well as the item line with a **Location Code** (a location with the matching flag).
4. **Set purchasing code in the sales line:** In the sales line, select the configured **Purchasing Code**. This automatically flags the line as **Selection For Purch. Order**; if the location is configured incorrectly, the purchasing code cannot be selected.
5. **Check/enter Vendor No.:** In the sales line, verify the **Vendor No.** If it is missing and no vendor is stored on the item or the stockkeeping unit either, no purchase order can be created.
6. **Release sales order:** Release the sales order via the standard **Release** function. Without release (status **Released**), the creation aborts with an error message.
7. **Create purchase order:** In the sales order, choose the action **Create Special/Drop/Release Purchase Order**. Confirm the prompt **"Should the Purch Order(s) be opened?"** with **Yes** to open the automatically created **Purchase Order** directly.
8. **Post:** Drop Shipment – Purchasing posts the receipt and the sales shipment is posted automatically. Special Order/Release Business – Sales posts the sales shipment manually (see *Warehouse and Subsequent Documents*).

## Setup

Setup is performed entirely in Microsoft Dynamics 365 Business Central. It consists of two mutually coordinated areas: the **purchasing codes**, which determine the business type of a sales line, and the **locations**, which define which location may be used for which business type. Both work together: A purchasing code can only be selected in the sales line if the location chosen there is set up accordingly. Therefore, administrators first set up the locations and the purchasing codes before users work with them in day-to-day business.

### Setting Up Purchasing Codes

**Access:** Use the BC **Tell Me** (Search) function to open the **Purchasing Codes** page. The purchasing codes are a company-wide master data list without their own higher-level entry page; opening via **Tell Me** is the intended path here.

**Process context:** The administrator or key user creates the purchasing codes once before first use. A purchasing code decides whether a sales line is treated as a drop shipment, special order or release business. Sales later selects this code in the sales line (see *Daily Work in the Sales Order*). Use the **New** action to create a new code or edit an existing one.

| Setup | Explanation |
|-------------|-------------|
| Code | Unique key of the purchasing activity. When set, the code is available for selection in the sales line in the **Purchasing Code** field and determines the business type there. |
| Description | Plain text for the purchasing activity. When maintained, users see a meaningful label in the selection list instead of just the code and select the correct code more reliably. |
| Drop Shipment | When activated, a sales line with this purchasing code is processed as a **drop shipment**: The line is flagged as **Selection For Purch. Order**, the chosen location must carry the **Drop Shipment** flag, and when the receipt is posted later the sales shipment is posted automatically as well. |
| Special Order | When activated, the sales line is processed as a **special order**: The goods first pass through your own warehouse, the line is flagged as **Selection For Purch. Order**, and the location must carry the **Special Order** flag. The sales shipment is posted manually later. |
| Release Business | When activated, the sales line is processed as a **release business**; in addition, the ship-to fields from the sales order are transferred to the created purchase order. When activated, the system mandatorily also sets **Special Order**; without Special Order set, Release Business cannot be saved. |

**Dependency (from AL):** For a release purchasing code, **Special Order** and **Release Business** must be set together – the system enforces this on save. If **Release Business** is removed again, the system re-checks the combination.

The purchasing code is also available as a column in the **Purchasing Codes** list; there the **Release Business** flag likewise appears as an additional column, so users can identify release-capable codes directly in the overview.

### Setting Up Locations

**Access:** Use **Tell Me** to open the **Locations** and, via the **Edit** action, the **Location Card**; alternatively Locations list → line → open card. The three flags are located on the **General** FastTab of the Location Card.

**Process context:** For each location the administrator defines for which business types this location may be used within the scope of the app. These flags act as a barrier in the sales line: Only if the location chosen in the line carries the flag matching the purchasing code can the purchasing code be set; otherwise the system aborts with an error message (e.g. "The location … can not be use for a Drop Shipment." or "… can not be use for a Special Order.").

| Setup | Explanation |
|-------------|-------------|
| Drop Shipment | When activated, this location may be used in sales lines with a drop shipment purchasing code. Without this flag, selecting a drop shipment purchasing code with the location is rejected. |
| Special Order | When activated, this location may be used for sales lines with a special order purchasing code. Without this flag, selecting a special order purchasing code with the location is rejected. |
| Release Business | When activated, the location is additionally released for release business. When activated, the system automatically also sets **Special Order**, because the release business is technically built on the special order; a pure release location without Special Order is therefore not possible. |

**Dependency (from AL):** Setting **Release Business** automatically validates **Special Order** = Yes. To select a special order or release purchasing code, the system additionally checks that the sales line carries a **Location Code** (mandatory field) and that the location has the **Special Order** flag.

> The Location Card is a standard Business Central page with numerous additional fields (address, warehouse logistics, bins, etc.). For this app, only the three flags mentioned above on the **General** FastTab are relevant; the remaining fields of the Location Card retain their standard behavior and are not changed here.

### Setting Up a Business Type End-to-End (Interaction of Purchasing Code and Location)

For a user to be able to create a drop, special or release purchase order in day-to-day business, several settings across two pages must match. The administrator sets them up in the following order:

1. **Release location (master data):** Open the **Location Card** of the location through which the business type is to be handled and set the appropriate flag (**Drop Shipment**, **Special Order** or **Release Business**). If this flag is missing, the associated purchasing code cannot be selected in sales lines with this location.
2. **Create purchasing code (global setup):** In **Purchasing Codes**, create a code and activate the same characteristic (**Drop Shipment**, **Special Order** or **Release Business**; for release additionally Special Order). When set, the code is available for selection in the sales line and automatically flags the line as **Selection For Purch. Order**.
3. **Provide vendor (prerequisite):** Make sure that a **Vendor No.** is stored on the item or on the stockkeeping unit (location/variant), or enter it later directly in the sales line. Without a vendor, the creation of the purchase order aborts.
4. **Operational completion (daily routine):** Sales sets the purchasing code in the sales line, releases the order and starts the action **Create Special/Drop/Release Purchase Order** (see *Daily Work in the Sales Order*).

## Master Data

The app does not bring its own master data tables; instead it extends existing standard Business Central master data with controlling flags. Two master data areas are functionally relevant: the **Purchasing Code** (classification of the purchasing activity) and the **Location** (permitted business types). Both are described above under *Setup* with a full field table, because they also form the central configuration of the app.

### Purchasing Code as a Master Record

The **Purchasing Code** is the master record that Sales selects in the sales line. Via the **Release Business** flag (an additional column in **Purchasing Codes** and in the overview list), the user recognizes which codes trigger a release business. When maintained: once during setup and for new business types. Where effective: as the **Purchasing Code** field in the sales line; the selection directly controls the further processing (see *Daily Work in the Sales Order*). Details and all fields: *Setup › Purchasing Codes*.

### Location as a Master Record

The **Location** carries the three release flags **Drop Shipment**, **Special Order** and **Release Business**. When maintained: when setting up the warehouses and whenever a location is to be released for a further business type. Where effective: when selecting the purchasing code in the sales line – the location decides whether the business type is permitted. Details and all fields: *Setup › Locations*.

## Daily Work in the Sales Order

The daily work takes place in the **Sales Order**. The prerequisites are the purchasing codes and locations described under *Setup*: The purchasing code determines the business type, the location releases the business type, and the Vendor No. controls which vendor is ordered from. Without this configuration, the purchasing code cannot be set and the purchase order cannot be created.

### Fields in the Sales Line

The app adds three fields to the sales line (the **Lines** subpage of the sales order). The remaining columns of the sales line (e.g. **No.**, **Description**, **Quantity**, **Location Code**, **Purchasing Code**) are standard Business Central fields and retain their standard behavior.

| Field | Explanation |
|------|-------------|
| Vendor No. | The vendor from whom the goods are ordered. If a vendor is stored on the item or the stockkeeping unit when the purchasing code is set, the system fills this field automatically; otherwise you enter the vendor manually. The field can only be maintained if the line is flagged as **Selection For Purch. Order**. If no Vendor No. can be determined, the creation of the purchase order aborts with a message. |
| Selection For Purch. Order | Controls whether the line is considered by the action **Create Special/Drop/Release Purchase Order**. When activated, the line flows into the purchase order to be created. The system sets the flag automatically when a drop/special/release purchasing code is selected and removes it when the purchasing code is removed or changed to a neutral code. Setting it manually without **Drop Shipment** or **Special Order** in the line is rejected by the system with an error message. |
| Release Business | Flags the line as release business. The field is not editable and is derived by the system from the selected purchasing code. When set, the purchase order creation additionally transfers the ship-to fields from the sales order to the purchase order, and the created purchase order likewise carries the **Release Business** flag. |

### Procedure: Creating a Purchase Order from the Sales Order

The order is fixed in the code; follow it, otherwise the process aborts.

1. **Open the sales order** and record the item line with the desired **Location Code**.
2. **Select purchasing code:** In the sales line, set the appropriate **Purchasing Code**. If the column is not visible, show it via personalization. The system then flags the line as **Selection For Purch. Order** and – if available – takes over the **Vendor No.** from the item or stockkeeping unit. If the location does not match the business type, the selection is rejected with an error message.
3. **Ensure Vendor No.:** Add the **Vendor No.** in the line if it was not filled automatically.
4. **Release sales order:** Release the order via the standard **Release** action (status **Released**). Without release, the system refuses the purchase order creation.
5. **Create purchase order:** In the ribbon, choose the action **Create Special/Drop/Release Purchase Order**. The system collects all lines of the order that are flagged as **Selection For Purch. Order** and not yet assigned to a purchase order, and creates one **Purchase Order** per vendor from them (or appends the line to a purchase order of the same vendor already created in the same run).
6. **Show purchase order:** Confirm the prompt **"Should the Purch Order(s) be opened?"** with **Yes**. If exactly one purchase order was created, the **Purchase Order** opens; if several, the list of purchase orders opens.

**What the system transfers in the process:** Drop shipment lines receive the standard **Drop Shipment** flag in the purchase order and the link to the sales order; the customer's ship-to address is transferred to the purchase order header as the customer. Special order lines are carried as **Special Order** in the purchase order. Release lines are likewise carried as special order; in addition, the "Ship-to" fields (code, name, address, city, country) are copied from the sales order to the purchase order header.

### Switching Between Sales Order and Purchase Order

For release business, users can switch between the linked documents at any time:

- **From the purchase order to the sales order:** In the purchase line, choose the action **Release Business › Sales Order**. The system opens the associated sales order (read-only), provided the purchase line carries the **Release Business** flag and has a special order link.
- **From the sales order to the purchase order:** In the sales line, choose the action **Release Business › Purchase Order**. The system opens the linked purchase order; if the purchase order is already posted, the posted purchase receipt is shown instead (the card for exactly one document, otherwise the overview).

## Warehouse, Posting and Subsequent Documents

After releasing and posting the purchase order, the business type decides the further posting flow. In doing so, the app intervenes in the standard posting and links the purchase and sales document via reservations.

### Posting Flow by Business Type

- **Drop Shipment:** Purchasing releases the purchase order and posts the **receipt** (purchase receipt). Since the goods go directly from the vendor to the customer, the **sales shipment** of the linked sales order is posted automatically in the background. Purchasing can only post the purchase invoice after Sales has posted the sales invoice.
- **Special Order:** Purchasing posts the receipt into your own warehouse. The **sales shipment** is **not** posted automatically, but must subsequently be posted manually by Sales. Purchasing can post the purchase invoice independently, even before the sales invoice.
- **Release Business:** Behaves in posting like the special order (manual sales shipment), but physically ships to the address transferred from the sales order.

### Reservation and Linking

When copying a purchase line into the item ledger entries (posting of the receipt), for special order and release business the app establishes a reservation link between the purchase order line and the associated sales line. This assigns the incoming quantity to the correct sales line; open remaining quantities are distributed proportionally until the sales line is covered. If the sales line is connected to a production order component, the app instead transfers the reservation to the matching production order component. This linking runs in the background without user intervention.

### Posted Documents and Traceability

On the **Posted Purchase Receipt**, the app carries the **Release Business** flag as well, so that release transactions remain recognizable even after posting. From the sales order, the associated posted purchase receipt can be called up via **Release Business › Purchase Order** when the purchase order is already posted. After the shipment postings, the item ledger entries of the transaction show the expected inventory (for drop shipment without a warehouse receipt).

## Permissions

The app delivers the permission set **"All permissions"** (object name MuM DS Permission). It is assignable and determines the permissions for the app's own objects: It grants read and write rights to the internal buffer table as well as the execution rights for the app's two codeunits. The permission set thereby defines which actions users can perform in connection with the purchase order creation. Assign this set to the users who create drop, special and release purchase orders. For the actual document processing (sales order, purchase order, posting), the standard Business Central permissions additionally apply.

## Typical Use Cases

The following scenarios show how the three business types are triggered in everyday work and handled in Business Central. All steps correspond to the flow stored in the code.

### Drop Shipment: Customer Orders a Stock Item Without Own Inventory

**Trigger:** A customer orders an item by phone that the company does not stock. The item is to be shipped directly from the vendor to the customer.

**Access in BC:** Sales creates a new **Sales Order** and records the item line with a location that carries the **Drop Shipment** flag.

**Core flow:**
1. In the sales line, select the **Purchasing Code** with the **Drop Shipment** flag – the line becomes **Selection For Purch. Order**, the **Vendor No.** is taken from the item.
2. Check the **Vendor No.**
3. **Release** the sales order.
4. Start the action **Create Special/Drop/Release Purchase Order**.
5. Confirm the prompt **"Should the Purch Order(s) be opened?"** with **Yes** – the created **Purchase Order** opens.

**Completion:** Purchasing releases the purchase order and posts the receipt; the sales shipment is posted automatically. Sales then posts the sales invoice, after which Purchasing posts the purchase invoice.

### Special Order: Goods Are Processed In-House Before Delivery

**Trigger:** A customer orders an item that must be repacked or processed in-house before delivery. The goods should therefore first come into your own warehouse.

**Access in BC:** New **Sales Order**; item line with a location that carries the **Special Order** flag.

**Core flow:**
1. In the sales line, select the **Purchasing Code** with the **Special Order** flag (Location Code is mandatory) – the line becomes **Selection For Purch. Order**.
2. Check or enter the **Vendor No.**
3. **Release** the sales order.
4. Run the action **Create Special/Drop/Release Purchase Order** and confirm the prompt with **Yes**.

**Completion:** Purchasing posts the receipt into the warehouse. After the internal processing, Sales posts the **sales shipment manually** and subsequently the sales invoice.

### Release Business: Drop Shipment to a Different Ship-to Address

**Trigger:** A customer orders goods that the vendor is to ship directly to a ship-to address stored in the sales order that differs from the customer.

**Access in BC:** New **Sales Order** with the "Ship-to" fields maintained; item line with a location that carries the **Release Business** flag (and thus **Special Order**).

**Core flow:**
1. Select the **Purchasing Code** with the **Release Business** flag in the sales line – the line becomes **Selection For Purch. Order** and is flagged as **Release Business**.
2. Ensure the **Vendor No.**
3. **Release** the sales order.
4. Start the action **Create Special/Drop/Release Purchase Order** and confirm with **Yes**.
5. In the opened **Purchase Order**, verify that the "Ship-to" fields were transferred from the sales order.

**Completion:** Purchasing releases the purchase order and posts the shipment to the transferred address; Sales posts the sales shipment manually. Via **Release Business › Sales Order** (in the purchase order) or **Release Business › Purchase Order** (in the sales order), users switch between the documents at any time.

## FAQ and Troubleshooting

### 1. Why can't the purchasing code be selected in the sales line?
The chosen location is not released for the business type. On the **Location Card**, set the appropriate flag (**Drop Shipment**, **Special Order** or **Release Business**). Without this flag, the system rejects the selection.

### 2. What happens if I set a drop shipment purchasing code without a matching location?
The system aborts with the message "The location … can not be use for a Drop Shipment." First activate **Drop Shipment** on the Location Card.

### 3. Why does the system require a Location Code for special order and release business?
For special order and release business, the **Location Code** in the sales line is mandatory, because the goods physically pass through your own warehouse and the location must carry the associated **Special Order** flag. Without a Location Code, the selection of the purchasing code aborts.

### 4. Why is "Special Order" set automatically when activating "Release Business"?
The release business is technically built on the special order. That is why the system enforces **Special Order** automatically when **Release Business** is set – both in the purchasing code and on the Location Card.

### 5. Why can't I create the purchase order even though the line looks correct?
The sales order is not released. The creation requires the status **Released**; first release the order via **Release**.

### 6. What happens if no Vendor No. is found?
If the system finds a **Vendor No.** neither in the sales line nor on the item or stockkeeping unit, it aborts with the message "No transaction can be created for the sales line … No vendor no. has been selected for Item …". Enter the Vendor No. in the line.

### 7. How are multiple lines with the same vendor processed?
The system bundles lines of the same vendor in the same run into **one** purchase order; further lines are appended to the purchase order already created for this vendor. For different vendors, multiple purchase orders are created.

### 8. Why are some lines skipped during creation?
Only lines with the **Selection For Purch. Order** flag set, with type **Item**, with a **Purchasing Code** set and without an already assigned purchase order number are considered. Lines that do not meet these conditions are disregarded.

### 9. Why is my sales shipment posted automatically for a drop shipment?
For a drop shipment, the goods go directly from the vendor to the customer. That is why, when the receipt is posted, the system posts the associated **sales shipment** automatically as well. For special order and release business this deliberately does not happen – here you post the sales shipment manually.

### 10. How do I get from the sales order to the created purchase order (and back)?
Use the action **Release Business › Purchase Order** in the sales order and the action **Release Business › Sales Order** in the purchase order. If the purchase order is already posted, the call from the sales order opens the posted purchase receipt instead.
