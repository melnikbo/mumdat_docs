---
title: Anwenderhandbuch m+m Product Configurator with Item Charge Management
---

# m+m Product Configurator with Item Charge Management User Guide

## Introduction

This module is a **bridge** between two m+m extensions: the **Product Configurator** and the **Item Charge Management**. It ensures that an item which is configured through the **Product Configurator** and is thereby flagged with **Create Item Charge** automatically receives a matching **Item Charge (Item)** line in the sales or purchase document. The module itself has no pages or setup fields of its own; it solely connects the existing functions of the two base modules with one another.

**Target audience:** This guide is aimed primarily at **operational users** who work with sales orders and purchase orders on a daily basis — sales support and purchasing clerks who enter configured items and **release** and **post** documents. Secondarily, it addresses **administrators** and **key users** who perform the necessary setup in Item Charge Management and the Product Configurator.

**Short process overview:** The user enters an item line in a document and calls up the **Product Configurator**. If the configuration sets the **Create Item Charge** flag on the line, Item Charge Management recognizes the line as changed on every modification and — controlled by this module — automatically creates or re-creates the associated **Item Charge (Item)** line. At the latest when the document is **released**, the line is present; when the **status is reopened**, it is removed again. The amount and distribution of the item charge follow the setup of the respective **Item Charge**.

## Quick Start for Users

The fastest way from configuration to a posted document with an automatic item charge. The setup (see the **Setup** chapter) must be performed once by an administrator before you can use this flow.

1. **Ensure setup is complete (one-time, prerequisite):** In the **Item Charge**, the **Reference Value** is set and **Transfer Automatically to Document** is set to **Yes** or **On Release**; the corresponding Product Configurator entry sets the **Create Item Charge** flag.
2. **Create the document:** Create a **Sales Order** (or a **Purchase Order**) and enter an item line of type Item.
3. **Configure:** Open the configuration via the **Product Configurator** action in the document line and complete it. This sets the **Create Item Charge** flag on the line.
4. **Check the automatic line:** After the line is saved, the system automatically creates a line of type **Item Charge (Item)** in the same document. Check the quantity and amount.
5. **Release:** Release the document via **Release**. If **Transfer Automatically to Document** is set to **On Release**, the **Item Charge (Item)** line is created at the latest now.
6. **Post:** Post the document via **Post**. The quantity distribution of the item charge line follows the **Quantity/Lump Sum to Ship (Sales)** and **Reference Value Document to Ship (Sales)** fields from the setup.
7. **Correct if needed:** Via **Reopen** you reopen the document; the automatically created **Item Charge (Item)** line is removed in the process and, on renewed release, re-created with the current setup values.

## Setup

This bridge module has **no setup page of its own**. For the automatic flow to work, the settings in the two base modules must match. This chapter describes the setup **in dependency order**: first the global base setup, then the individual **Item Charge** as a master record, and finally the triggering flag from the Product Configurator.

### Item Charge Setup (global base setup)

**Process entry:** This setup is a **company-wide base setup** (one record per company). You open the **Item Charge Setup** page via **Search**. It is maintained once by the administrator before first use and defines the default behavior for calculating item charges on shipment. You then maintain the specific item charges themselves as master data (see **Master Data**).

| Setup | Explanation |
|---|---|
| Reference Value (Calculation) | If a reference value is stored here, it determines what the default calculation of the item charge relates to; without a default, the system behaves like the Business Central standard. |
| Quantity/Lump Sum to Ship (Sales) | If set, the value defines for **Sales** at which shipment point the item charge is transferred by quantity. **(blank)/Standard:** BC standard behavior. **First Shipment (complete):** The item charge is calculated on the first shipment. **Last Shipment (complete):** It is calculated only on the last shipment, when the remaining quantity is 0. **Every Shipment:** For each shipped portion the corresponding portion of the item charge is calculated. |
| Reference Value Document to Ship (Sales) | If set, the value in **Sales** controls the document-related calculation. **(blank)/Standard:** BC standard. **First Shipment:** Calculation on the first shipment, depending on the document. **Last Shipment:** Calculation on the last shipment, when the remaining quantity is 0. |
| Quantity/Lump Sum to Ship (Purchase) | Like **Quantity/Lump Sum to Ship (Sales)**, but for **Purchase**; controls the shipment point of the item charge calculation in purchase documents with the same values. |
| Reference Value Document to Ship (Purchase) | Like **Reference Value Document to Ship (Sales)**, but for **Purchase**. |

> This base setup belongs functionally to Item Charge Management and is only assumed as a prerequisite by this bridge module. The individual timing values are set more finely per **Item Charge** (see below).

### Setting up automatic item charges from the configuration

For a configured item to automatically receive an item charge in the document, a multi-stage setup across several pages is required. This bridge module connects the last two stages automatically.

**Process intro:** The administrator sets up this chain together with the key user **before first use**. In day-to-day operations it is triggered by the **Product Configurator** action in the document line (see **Daily Work in the Document**).

**Setup steps in dependency order:**

1. **Create the Item Charge as a master record** (page **Item Charges**): Create the item charge with **No.**, **Description**, and **Gen. Prod. Posting Group**. When these fields are filled, the item charge can be used in documents and posted correctly to the appropriate G/L account.
2. **Define the reference value:** Set the **Reference Value** of the item charge. If, for example, **Quantity** is selected here, the item charge is calculated per line and by quantity; with **Document** it relates to all lines of the document.
3. **Control the transfer:** Set **Transfer Automatically to Document** to **Yes** (immediate automatic line on creation) or **On Release** (line is created on document release). If **Yes** is selected, the **Reference Value** must not be **Document** — this combination is prevented by the system with an error message.
4. **Set selectability (optional):** Enable **Selectable in Document Line** if the user should additionally be able to select the item charge manually in the document line. When enabled, the item charge appears in the manual selection of the document line.
5. **Store the flag in the Product Configurator:** Ensure that the configuration of the item in question sets the **Create Item Charge** flag on the document line. When this flag is set, Item Charge Management treats the line as changed on every modification and creates the **Item Charge (Item)** line automatically — this is precisely the task of this bridge module.

**Operational completion:** In day-to-day operations the user calls the **Product Configurator** action in the document line; the item charge line is then created automatically (see **Daily Work in the Document** and **Typical Use Cases**).

## Master Data

### Maintaining Item Charges (master data)

**Process intro:** The **Item Charge** is the central master record from which the automatically created document line obtains its values. It is maintained by the administrator/key user and opened via **Search** (list **Item Charges** → card). The values maintained here flow into every automatically generated **Item Charge (Item)** line in day-to-day operations (see **Daily Work in the Document**).

| Field | Explanation |
|---|---|
| No. | When filled, the number identifies the item charge according to the defined number series; it is used on the automatically created document line as the item charge. |
| Description | When filled, this text appears as the line description of the item charge in the document; this lets the user recognize the purpose of the automatically created line. |
| Gen. Prod. Posting Group | When set, the general product posting group links the item charge to the appropriate G/L account on posting according to the posting matrix setup; without it, the item charge cannot be posted correctly. |
| Unit of Measure Code | When set, the unit of measure code determines the unit of the item charge based on the unit of measure table. |
| Reference Value | When set, the reference value controls how the item charge is calculated. **(blank)/Standard:** BC standard. **Lump Sum Partial:** per line with quantity 1. **Document:** related to all lines of the document with quantity 1. **Quantity:** per line, quantity = quantity of the item line. **Lump Sum Total:** flat total amount across the document. |
| Selectable in Document Line | When enabled, the user can manually select or override the item charge in the document line; the flag also serves as a filter marker for the pre-filtered selection. |
| Transfer Automatically to Document | When set, the value defines when the item charge line is created automatically. **(blank):** BC standard behavior without automatic creation. **Yes:** When an item line is created, the item charge is automatically generated as the next line. **Manual:** The user can manually add an item charge line to any sales/purchase line. **On Release:** When the document is released, the system creates the item charge line automatically. For the automatic flow of this bridge module, **Yes** or **On Release** are relevant. |
| Calculation Date | When set, the calculation date determines which date price calculation uses when creating the invoice: **Work Date**, **Posting Date**, **Order Date**, or **Shipment Date**. |
| Reference Value Document to Ship (Sales) | When set, the value in Sales controls at which shipment point the document-related item charge is calculated: **(blank)/Standard**, **First Shipment**, **Last Shipment** (remaining quantity 0). |
| Quantity/Lump Sum to Ship (Sales) | When set, the value in Sales controls the quantity-related shipment point: **(blank)/Standard**, **First Shipment (complete)**, **Last Shipment (complete)**, **Every Shipment**. |
| Reference Value Document to Ship (Purchase) | Like **Reference Value Document to Ship (Sales)**, but for Purchase. |
| Quantity/Lump Sum to Ship (Purchase) | Like **Quantity/Lump Sum to Ship (Sales)**, but for Purchase. |

> The **Calculation Date** is particularly relevant in the case described by the associated process, where the sales price is only set in the invoice via the calculation: in that case the selected date provides the basis for the item charge calculation when the invoice is created.

### Item Charge Assignment

**Process intro:** The **Item Charge Assignment** links an item charge with the document lines it relates to. It is maintained in Item Charge Management and is the basis for the automatically created **Item Charge (Item)** line referencing the item line correctly. For the automatic flow of this bridge module, the user generally does not need to edit the assignment manually — it is created together with the automatic line. Via the **Item Charge Assignments** action in the document line, the user can view and adjust the assignment if needed.

## Daily Work in the Document (Sales and Purchase)

This chapter describes how the bridge module acts in the document. The controlling settings are located on the **Item Charges** and **Item Charge Setup** pages (see **Setup**) as well as in the configuration of the **Product Configurator**; there the administrator defines which reference value applies, whether the transfer takes place automatically or on release, and which item sets the **Create Item Charge** flag.

### Configuration in the document line

**Entry:** In the sales or purchase document line, open the configuration via the **Product Configurator** action. After the configuration is completed, the system enters the **Create Item Charge** flag on the line.

| Field/Action | Explanation |
|---|---|
| Product Configurator (Action) | When called, the configuration screen for the line opens; upon completion the configuration values and — depending on the configuration — the **Create Item Charge** flag are written to the line. |
| Create Item Charge | When set on the line, Item Charge Management treats the line as changed on every modification and automatically creates or re-creates the associated **Item Charge (Item)** line; if the flag is not set, the line remains a normal item line without an automatic item charge. |

### Automatic item charge line

As soon as the **Create Item Charge** flag is set, the bridge takes effect:

- On every change of the document line, Item Charge Management checks for differences. In this case this module always reports the line as changed, so that the **Item Charge (Item)** line is re-evaluated correctly.
- If no existing automatic line is deleted on save, the module triggers the (re-)creation of the **Item Charge (Item)** line with **Transfer Automatically to Document = Yes**. This way a line whose amount had in the meantime fallen back below the minimum value receives its item charge again without duplicates.
- The new line adopts the reference value, transfer point, and shipment quantity control from the stored **Item Charge**.

### Release, Post, and Reopen

1. **Release:** Release the document via **Release**. If **Transfer Automatically to Document = On Release** is set in the item charge, the **Item Charge (Item)** line is created at the latest now.
2. **Post:** Post the document via **Post**. The quantities of the item charge line are distributed based on **Quantity/Lump Sum to Ship (Sales)** and **Reference Value Document to Ship (Sales)** (in purchase, the corresponding Purchase fields).
3. **Reopen:** Via **Reopen** you reopen the document. The automatically created **Item Charge (Item)** line is removed; on renewed release it is re-created with the then-current setup values.

## Permissions

The module ships the permission set **MuM PKCM All**. It is assignable and defines the permissions for executing the bridge codeunit of this module. Assign this permission set to all users who work with configured items and automatic item charges in sales and purchase documents. It defines that the automatic creation of item charge lines may be executed for these users; the permissions for the actual item charge and document data are controlled via the permission sets of the base modules.

On login, the module additionally runs a **license check**. If the license for this extension is not valid, automatic item charge creation is not available; in that case, contact your administrator.

## Typical Use Cases

### Use Case 1 — Configured sales order with automatic item charge

1. **Trigger:** A customer calls and orders a configurable item; sales support creates a sales order for it.
2. **Entry in BC:** The user creates the **Sales Order**, enters the item line, and opens the configuration via the **Product Configurator** action.
3. **Core flow:** After the configuration is completed, the system enters the **Create Item Charge** flag on the line. On save, Item Charge Management — controlled by this module — automatically creates a line of type **Item Charge (Item)**. The user releases the order via **Release**; the item charge line is taken into account according to the setup.
4. **Completion:** The user posts the order via **Post**. If the configuration must be changed afterward, the user reopens the status via **Reopen**, adjusts the line, and releases again; the item charge line is re-created with the current values.

### Use Case 2 — Purchase order with automatic item charge

1. **Trigger:** For a configured item, additional costs (e.g. freight) arise at the vendor, which are to be represented as an item charge in the order.
2. **Entry in BC:** Purchasing creates a **Purchase Order** for the vendor and enters the item line.
3. **Core flow:** Via the **Product Configurator** action, the line is configured and the **Create Item Charge** flag is set. On save, or at the latest on **Release**, the system automatically creates an **Item Charge (Item)** line. If the framework conditions of the item charge were changed in the meantime, the current setup is applied on deletion and re-creation.
4. **Completion:** The order is posted via **Post**. Via **Reopen** the user can remove the automatic item charge line and have it re-created after adjustment.

## FAQ and Troubleshooting

### 1. What is the purpose of this module at all?
It connects the **Product Configurator** with **Item Charge Management**: if a configuration enters the **Create Item Charge** flag on the document line, this module ensures that the matching **Item Charge (Item)** line is created automatically in the document.

### 2. Where do I set that an item automatically receives an item charge?
In three steps: Create the **Item Charge**, set **Reference Value** and **Transfer Automatically to Document** there (**Yes** or **On Release**), and ensure that the configuration of the item sets the **Create Item Charge** flag.

### 3. Why is no automatic item charge line created?
Check whether the **Create Item Charge** flag is set on the document line. If it is not set, the system treats the line as a normal item line and does not create an item charge. Additionally check whether **Transfer Automatically to Document** in the item charge is set to **Yes** or **On Release**.

### 4. Why do I get an error message when I set "Transfer Automatically to Document" to "Yes"?
The combination **Transfer Automatically to Document = Yes** with **Reference Value = Document** is not permitted and is prevented by the system with an error message. For automatic transfer, choose a different reference value (e.g. **Quantity** or **Lump Sum Partial**).

### 5. What does "On Release" mean compared to "Yes"?
With **Yes**, the item charge line is created already when the item line is created. With **On Release**, it is created only when the document is released via **Release**. In both cases, the system takes the stored parameters into account.

### 6. Why does the item charge line disappear when I reopen the document?
On **Reopen**, the system removes the automatically created **Item Charge (Item)** line. On renewed release, it is re-created with the then-valid setup values — this way, interim changes to the framework conditions are taken into account.

### 7. I changed the quantity of the item line — is the item charge recalculated?
Yes. On every relevant change to the line, this module reports the line as changed, so that Item Charge Management re-evaluates the associated item charge line and re-creates it if needed.

### 8. Are duplicate item charge lines created if I change the line multiple times?
No. The module only re-creates the line when no automatically created item charge line is present anymore. If one already exists, no duplicate is created.

### 9. Can I also add an item charge manually?
Yes. In the item charge, set **Transfer Automatically to Document = Manual** and enable **Selectable in Document Line**. Then the user can manually select and add the item charge via the document line.

### 10. Why does the automatic creation not work at all, even though everything is set up?
The module performs a **license check** on login. If the license for this extension is not valid, automatic item charge creation is not executed. Also check whether the permission set **MuM PKCM All** is assigned, and contact your administrator for license questions.
