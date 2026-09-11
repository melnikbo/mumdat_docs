---
title: Anwenderhandbuch m+m Warehouse Job Overview
---

# User Guide m+m Warehouse Job Overview

## Introduction

The **Warehouse Job Overview** consolidates all open warehouse jobs of a company into a single list. Whenever a **Warehouse Receipt**, a **Warehouse Shipment**, a warehouse activity (Pick or Put-Away) or an **Item Reclassification** via an Item Reclassification Journal is created in standard Microsoft Dynamics 365 Business Central, the module automatically creates a line in the Warehouse Job Overview. This gives the user a single place to see which warehouse documents are still open, which remaining quantities exist, and the processing status of each line. Posting of the source documents is triggered and simplified directly from this list.

**Target audience:** The module is aimed primarily at **operational warehouse staff** who pick, put away, process warehouse receipts and warehouse shipments, and post item reclassifications on a daily basis. These users work mainly on the **Warehouse Job Overview** page and on the lines opened from it. Secondarily, the module concerns **administrators and warehouse managers**, who configure the **Warehouse Job Setup**, the **Warehouse Workgroups**, the **Bin Capacity** and the warehouse mask once.

**Process overview:** A source document is created (Sales Order → Warehouse Shipment, Purchase Order → Warehouse Receipt, warehouse activity, Item Reclassification Journal) ⇒ a line in the **Warehouse Job Overview** is created automatically ⇒ the user filters the list (Workgroup, filter template) ⇒ selects a line ⇒ **Start** ⇒ **Partially Finish** or **Finish** ⇒ the source document is posted ⇒ control via the **Event History**.

## Quick Start for Users

The fastest path from an open warehouse document to posting. The setup (steps A–C) is a prerequisite and is usually performed once by the administrator; daily work begins at step 1.

**Prerequisite (administrator, one-time):**

- **A.** Use **Search** to open the **Warehouse Job Setup** and define the global base values (see the *Setup* section).
- **B.** Under **Warehouse Workgroups**, maintain at least one **Workgroup** and activate the required warehouse processes in it (Pick, Put-Away, Warehouse Receipt, Warehouse Shipment, Item Reclassification).
- **C.** Under **Warehouse Job Overview Filter Templates**, create one filter template per work area so that users can quickly restrict the list to their area.

**Daily work (warehouse staff):**

1. Use **Search** to open the **Warehouse Job Overview** page.
2. In the **Filters** area, restrict the list via **Template Filter Code** and/or **Warehouse Group Code Filter**, and if required use **Hide Finished** to hide the completed lines.
3. Select the line (or several lines) to be processed in the **Lines** list.
4. Choose **Start**. The line changes to status **Started**; an entry is recorded in the Event History.
5. After the physical work is completed, choose **Finish** (fully) or **Partially Finish** (remaining quantity stays open). The associated source document is posted in the process.
6. If required, use **Event History** to check the chronological progress of the line.

## Setup

Setup is the foundation of the module. It determines which warehouse documents appear in the Warehouse Job Overview, how posting is carried out, and whether additional functions (Bin Capacity, warehouse mask) are used. Perform the steps in the order given: first the global setup, then the master data of the workgroups, followed by the scoped filter templates and optional functions.

### Warehouse Job Setup

**Entry point:** Use **Search** to open the **Warehouse Job Setup** page (card, one record company-wide). This page is created automatically the first time it is opened.

**Process:** Here the administrator defines the base values valid company-wide once, before the first workgroup is maintained. The fields control the display numbering, the adoption of the complete bin content, and the use of Bin Capacity.

| Setup | Explanation |
|---|---|
| **Global Delimiter** | If you enter a character (default value `%`), the module uses this character as a separator when composing internal identifiers and filters. Change the value only if a stored separator collides with your code values. |
| **Increment Display Order by** | If you enter an increment here (e.g. 10), the system assigns the **Display Order** of new workgroup and view lines automatically at this interval. This makes it possible to insert lines in between later without having to reassign all numbers. |
| **Use Complete Bin Content** | If activated, this default value is copied to the field of the same name when new items are created; the item reclassification then proposes the complete stock of a bin for the movement instead of only the order quantity. Without the flag, only the required quantity is proposed. |
| **Use Bin Capacity** | If activated, the **Bin Capacities** function is enabled: only then can the Bin Capacities page be opened and maximum quantities per bin be maintained. Without the flag, the capacity check is inactive. |

**Action on this page:**

- **Initialize Web Services** — If you run this action, the system publishes the web service required for the warehouse mask (tablet/scanner interface). Run the action before you put the warehouse mask into operation; the system confirms the successful initialization with a message.

Note on permissions: The permission set shipped with the module determines which users are allowed to run the setup, master data and posting functions of the Warehouse Job Overview. Assign this set to all operational warehouse users as well as to the administrators.

### Setting up the Warehouse Job Overview

This core function — collecting, starting and finishing/posting open warehouse documents — requires a multi-stage configuration. Who sets it up: the administrator, before the first productive use. Where it takes effect in day-to-day work: on the **Warehouse Job Overview** page (section *Daily Work on the Warehouse Job Overview*).

1. **First**, define the global base values in the **Warehouse Job Setup** (see above). Once this is done, the default values apply to all downstream steps.
2. **Then**, under **Warehouse Workgroups**, maintain the master data of the workgroups and activate the warehouse processes per group (Pick, Put-Away, Warehouse Receipt, Warehouse Shipment, Item Reclassification). If a warehouse process is activated in a group, the associated source documents appear in the Warehouse Job Overview as soon as the filter is set to this group (see *Master Data → Warehouse Workgroups*).
3. **Next**, create one **Warehouse Job Overview Filter Template** per work area (next section). If a template is stored, the user can restrict the list to their area with one click.
4. **Finally**, the warehouse worker works in day-to-day operations with the actions **Start**, **Partially Finish** and **Finish** (operational execution, see *Daily Work*).

#### Warehouse Job Overview Filter Template

**Entry point:** Use **Search** to open the **Warehouse Job Overview Filter Templates** list and create a template with *New*; the **Whse. Job Fil. Template** card opens.

**Process:** The administrator or key user defines one template per work area (e.g. receiving zone, shipping zone). The warehouse worker later selects this template in the filter area of the Warehouse Job Overview page and immediately sees only the lines relevant to them.

| Field | Explanation |
|---|---|
| **Code** | If you assign a unique code, the template can be selected via **Template Filter Code** in the filter area of the Warehouse Job Overview. |
| **Description** | If you enter a meaningful description, the user immediately recognizes in the selection which work area the template is intended for. |
| **Warehouse Group Filter** | If you store one or more **Workgroups** here, the list shows only lines of these groups when the template is applied. This restricts the view to the responsible warehouse area. |
| **Hide Finished** | If activated, the list hides all already finished lines when the template is applied and shows only the work that is still open. Without the flag, completed lines also remain visible. |

### Setting up Item Reclassification in the Warehouse Job Overview

To handle and post item reclassifications (stock movements between locations/bins) via the Warehouse Job Overview, a dedicated configuration chain is required. Who sets it up: the administrator. Where it takes effect in day-to-day work: via the item reclassification lines in the Warehouse Job Overview (see *Daily Work*) and the Item Reclassification Journal.

1. **First**, use **Search** to open the **Item Journal Templates** and activate the **Warehouse Job Required** field on the desired template. If activated, the system checks that the template has the type **Item Reclassification** and automatically creates a line in the Warehouse Job Overview for each journal line.

   | Field | Explanation |
   |---|---|
   | **Warehouse Job Required** | If activated, all item reclassification lines entered via this journal template are automatically adopted as lines in the Warehouse Job Overview and can be started and finished/posted there. Activation is only permitted if the template has the type **Item Reclassification** (the system enforces this). Without the flag, the item reclassification remains a pure standard journal transaction with no entry in the Warehouse Job Overview. |

   The same field is also available in the **Item Journal Templates** list; the effect is identical.

2. **Then**, in the relevant **Workgroup** (see *Master Data → Warehouse Workgroups*), store the **Item Reclassification** flag as well as the **Journal Template Name** and the **Journal Batch Name**. If these values are set, the system knows into which reclassification journal the movements of the group are posted.
3. **Optionally**, activate the **Use Complete Bin Content** field on the item (see *Master Data → Items*). If activated, the item reclassification proposes the complete bin content of the item for the movement.
4. **Finally**, the user posts the item reclassification line in the Warehouse Job Overview via **Finish** (operational execution, see *Daily Work → Item Reclassification Lines*).

### Setting up Bin Capacity

Bin Capacity lets you store maximum quantities per bin. Who sets it up: the administrator. Where it takes effect: with put-away/reclassification proposals that take the bin content into account.

1. **First**, in the **Warehouse Job Setup**, activate the **Use Bin Capacity** field. If activated, the **Bin Capacities** action is enabled; without this flag, the capacity page cannot be opened (the system checks this on opening).
2. **Then**, open the **Location Card** of the relevant location and choose the **Bin Capacities** action there (in the ribbon under *Related/Navigate*). Alternatively, open **Bin Capacities** directly from the **Bins** list or the bin content overview via the action of the same name; the bin is then already prefilled.

**Fields of the Bin Capacities page:**

| Field | Explanation |
|---|---|
| **Location Code** | If you store the location, the capacity line applies to this location. When entering via the Location Card or bin list, the value is already prefilled. |
| **Bin Code** | If you store the bin, the line limits the capacity of this specific bin. |
| **Process Type** | Determines for which movement direction the maximum quantity applies. **All:** capacity applies to inbound and outbound movements. **Inbound:** capacity is only checked on receipts (Put-Away/Warehouse Receipt). **Outbound:** capacity is only checked on issues (Pick/Warehouse Shipment). |
| **Type** | Determines what the capacity refers to (e.g. item- or unit-related). When the Type is changed, the **No.** field is cleared. If the Type is empty, the system reports an error when **No.** is set. |
| **No.** | If you store the value matching the **Type** here (e.g. an item no.), the capacity applies only to this reference. A valid **Type** is a prerequisite. |
| **Unit Of Measure Code** | If you set the unit of measure code, the **Max. Quantity** is interpreted in this unit. |
| **Max. Quantity** | If you enter a maximum quantity, the bin must not exceed this quantity for the specified reference; the module takes the value into account in the capacity-dependent proposals. |

### Setting up the Warehouse Mask

The warehouse mask is the configurable tablet/scanner interface of the module for working directly at the warehouse. It consists of **views** (which fields and actions are shown per process) and the **user/device assignment**. Who sets it up: the administrator. Where it takes effect: on the warehouse worker's mobile device.

1. **First**, run the **Initialize Web Services** action in the **Warehouse Job Setup**. Once this is done, the web service is available through which the mobile interface communicates with Business Central.
2. **Then**, under **Warehouse Mask Views**, define one **Warehouse Mask View** per process type.
3. **Finally**, under **User Device Setup**, assign the users or devices.

#### Warehouse Mask View

**Entry point:** Use **Search** to open the **Warehouse Mask Views** list and open a line; the **Warehouse Mask View** card appears.

The card is divided into several areas that are visible depending on the **Type** of the view. Each area is its own subpage with its own lines.

**General:**

| Field | Explanation |
|---|---|
| **Type** | Determines which warehouse process the view applies to and which areas are shown. **Transfer:** view for stock movements. **Warehouse Activity:** view for Pick/Put-Away (additionally shows the Warehouse Receipt and Warehouse Shipment areas). **Warehouse Receipt / Warehouse Shipment:** view for the respective document. **Qty. Transfer / Qty. Warehouse Activity / Qty. Warehouse Receipt / Qty. Warehouse Shipment:** views in which the worker enters only quantities on the device. Only for the quantity- and activity-related types is the **Input Enabled** column in the lines relevant. |
| **Description** | If you enter a description, the administrator recognizes in the overview what the view is used for. |

**Areas (subpages) of the view:** **Header Information**, **Line Information** as well as – for the **Warehouse Activity** type – **Warehouse Receipt** and **Warehouse Shipment**. Each area contains the same fields for field control.

**Lines of the areas (Warehouse Mask View Line):**

| Field | Explanation |
|---|---|
| **Field No.** | If you choose the field number, the associated data field is shown in this area of the mask. |
| **Field Name** | Shows the name of the selected field for control. |
| **Display Order** | If you assign an order, the fields appear on the device in this sort order. The default value is derived from the **Increment Display Order by** of the setup. |
| **Input Enabled** | If activated, the worker is allowed to change the field on the device (only visible for quantity/activity-related view types). Without the flag, the field is only displayed. |
| **Switch editability** | If activated, the editability of the field can be switched situationally on the device; in this case the system asks before a partial quantity is entered. Only relevant if **Input Enabled** is set. |

Via the **Translations** action, you store language-dependent captions per field line or action; via the **Actions** area, you define which buttons (e.g. Finish, Close) are available on the device.

#### User Device Setup

**Entry point:** Use **Search** to open the **User Device Setup** list. Via the **User Device** card view, you maintain the details of an entry.

**Process:** The administrator assigns each warehouse user or each device a filter template and a language and activates the access. The user set up in this way sees exactly the selection of Warehouse Job Overview lines intended for them on the device.

| Setup | Explanation |
|---|---|
| **Type** | Determines whether the entry concerns a **User** or a **Device**. **User:** The **Code** refers to a Business Central user name. **Device:** The entry applies to a device regardless of the logged-in user. |
| **Code** | If you store the code, the assignment applies to this user or this device. For the **User** type, the user table is referenced. |
| **Language Code** | If you store a language, the warehouse mask appears on the device in this language. |
| **State** | Determines whether the access is active. **Enabled:** The user/device can use the warehouse mask. **Disabled:** The access is blocked; the mask cannot be used for this entry. |

In the **User Filter Lines** subarea (workspace lines), you store per entry the filters to be displayed with **Description** and **Display Order**, so that the user finds their work areas on the device in the desired order.

## Master Data

### Warehouse Workgroups

**Entry point:** The **Warehouse Workgroups** form the central master data table of the module. Open the **Warehouse Workgroups** list and open a line to edit the **Workgroup** card; the workgroup is also opened as a lookup and drill-down page wherever a workgroup is referenced (e.g. in the **Warehouse Group Filter** of the filter template).

**Process:** The administrator creates one workgroup per organizational warehouse area and thereby determines **which warehouse processes** appear in this group in the Warehouse Job Overview. The group is then used in the filter templates and in the filter area of the Warehouse Job Overview list to control the users' view.

| Field | Explanation |
|---|---|
| **Code** | If you assign a unique code, the group can be referenced in filter templates and in the **Warehouse Group Code Filter**. |
| **Description** | If you enter a description, the group is clearly identifiable in selection lists. |
| **Put-Away** | If activated, put-away warehouse activities (with warehouse logistics) of this group appear in the Warehouse Job Overview. When assigning locations, only locations that require put-away are accepted. |
| **Pick** | If activated, pick warehouse activities (with warehouse logistics) of this group appear in the Warehouse Job Overview; the location assignment is restricted to locations with pick requirement. |
| **Invt Put-Away** | If activated, inventory put-aways (Invt. Put-away, without advanced warehouse logistics) of this group are taken into account. |
| **Invt Pick** | If activated, inventory picks (Invt. Pick, without advanced warehouse logistics) of this group are taken into account. |
| **Warehouse Receipt** | If activated, open warehouse receipts of the assigned locations appear in the Warehouse Job Overview and can be posted from there. |
| **Warehouse Shipment** | If activated, open warehouse shipments of the assigned locations appear in the Warehouse Job Overview and can be posted from there. |
| **Item Reclassification** | If activated, item reclassifications of this group are managed in the Warehouse Job Overview. Only with this flag are the **Journal Template Name** and **Journal Batch Name** fields editable; when it is reset, both are cleared. Setting the **Bin Usage** to **From** or **To** makes item reclassification mandatorily active (the system checks this). |
| **Bin Usage** | Controls how bins of the group are used in item reclassification. **All:** no restriction. **From:** bins serve as the source. **To:** bins serve as the destination. The values **From** and **To** require **Item Reclassification** to be active. |
| **Journal Template Name** | If you store the reclassification journal template, the item reclassifications of the group are posted into this template. Only templates of the type **Item Reclassification** with **Warehouse Job Required** can be selected. Editable only when **Item Reclassification** is active. |
| **Journal Batch Name** | If you store the specific journal batch, the item reclassifications are written into this batch of the selected template. Editable only when **Item Reclassification** is active. |

**Dependency (check in code):** When saving, the system checks that for **Bin Usage** = From/To the **Item Reclassification** flag is set, and that when item reclassification is inactive the two journal fields are empty. In the **Warehouse Workgroup Lines** subarea, assign the specific locations and bins; the locations allowed there depend on the warehouse processes activated in the group.

#### Warehouse Workgroup Lines

In the **Warehouse Workgroup Lines** subarea of the workgroup, you store for which locations and bins the group applies.

| Field | Explanation |
|---|---|
| **Location Code** | If you choose a location, the group applies to this location. The selection is restricted to locations whose logistics flags match the processes activated in the group (e.g. pick requirement when Pick is active). |
| **Bin Code** | If you choose a bin, the group is additionally narrowed to this bin. |
| **Description** | Automatically shows the description of the selected bin so that the assignment is unambiguous. |

### Item: Use Complete Bin Content

**Entry point:** Use **Items** to open the **Item Card** and switch to the **Warehouse** FastTab.

**Process:** The administrator or planner decides per item whether the complete bin content should be moved during item reclassifications. The default value comes from the **Warehouse Job Setup** and is adopted when new items are created; it can be overridden per item.

| Field | Explanation |
|---|---|
| **Use Complete Bin Content** | If activated, the item reclassification proposes for this item the complete stock present at the bin for the movement, instead of only the quantity required for the order. This is useful when a bin is to be completely cleared. Without the flag, only the required quantity is proposed. |

This flag works together with the *Item Reclassification in the Warehouse Job Overview* setup (see there).

## Daily Work on the Warehouse Job Overview

The **Warehouse Job Overview** page is the central workplace of the operational warehouse staff. It shows all open warehouse documents as lines and provides the actions to start, partially finish, finish, reopen, as well as access to the Event History. Which lines appear is controlled by the administrator via the **Warehouse Workgroups** and the **Warehouse Job Setup** (see *Setup*).

**Entry point:** Use **Search** to open the **Warehouse Job Overview** page.

### Filters

The filter area at the top of the page restricts the displayed lines. Since the number of hits drops significantly with active filter templates and workgroups, every user should first set their area here.

| Filter field | Explanation |
|---|---|
| **Template Filter Code** | If set, the lines are filtered by the selected **Warehouse Job Overview Filter Template**; the workgroups stored in the template and the **Hide Finished** setting are adopted. |
| **Warehouse Group Code Filter** | If set, only lines of the specified **Workgroups** are shown. Via the lookup, the filter expression can conveniently be assembled from the existing groups; the system checks the validity of the entered filter. |
| **Hide Finished** | If set, all lines with status **Finished** are hidden and only the work that is still open is shown. Without the flag, finished lines remain visible (e.g. for review). |

### Lines and Columns

The **Lines** list shows one line per open warehouse document. The lines are sorted by **Shipment Date**; finished lines are visually offset, and the status is additionally highlighted in color.

| Field | Explanation |
|---|---|
| **Job Description** | Shows the identifier of the source document (document no. and line no.) so that the user can uniquely assign the line to a document. |
| **Status** | Shows the processing state of the line. **Open:** line created, not yet started — only **Start** is possible. **Planned:** flagged state (highlighted in color), no processing yet. **Started:** processing is running — **Partially Finish** and **Finish** are possible. **Interrupted:** processing paused (highlighted in color as critical). **Partially Finished:** part has been posted, a remaining quantity stays open — can be **started** again. **Finished:** line fully posted/completed — displayed offset; can be reopened if required via **Reopen**. |
| **Shipment Date** | Shows the delivery/due date of the source document; controls the sorting and urgency of processing. |
| **Source ID** | Shows the document number of the source document (Warehouse Shipment, Warehouse Receipt, warehouse activity or journal template). |
| **Location Code** | Shows the location at which the movement takes place. |
| **Bin Code** | Shows the source bin of the movement. |
| **New Location Code** | Shows the destination location for item reclassifications. |
| **New Bin Code** | Shows the destination bin for item reclassifications. |
| **Customer Name** | Shows the name of the customer for warehouse shipments from sales orders. |
| **Sales Order No.** | Shows the underlying sales order number for warehouse shipments. |
| **Item No.** | Shows the item to be moved. |
| **Item Description** | Shows the description of the item. |
| **Item Description 2** | Shows the second description line of the item. |
| **Quantity** | Shows the (open) quantity of the line to be processed. |

Depending on the source type, the page displays a matching detail area below the list — e.g. the warehouse shipment lines, the warehouse receipt lines, the pick/put-away lines, or, for item reclassifications, the **Item Reclassification Lines** (Item Reclassification Journal). This way the user sees the details of the source document directly in the same view.

### Actions and Posting Flow

The following actions are available in the ribbon; they are active or inactive depending on the status of the selected line.

| Action | Explanation |
|---|---|
| **Start** | If you start a line with status **Open** (or again after Partially Finish/Finish), the line changes to status **Started** and an entry is written in the **Event History**. Only afterwards are Partially Finish and Finish possible. For lines without a valid source, the action is not available. |
| **Partially Finish** | If you partially finish a started line, the system sets the status to **Partially Finished**, writes an event entry and posts the processed partial quantity of the source document. The remaining quantity stays open and can be started again later. |
| **Finish** | If you finish a started line, the system sets the status to **Finished**, writes an event entry and posts the source document. In case of a remaining quantity, the system additionally marks the document as fully completed, so that no further delivery/receipt is expected. |
| **Reopen** | If you reopen a line that has not yet been finished, its status is reset to **Open**. This makes it possible to defer a line that was started by mistake. |
| **Event History** | If you choose this action, the **Whse. Job Event Lines** page opens with the chronological progress of the selected line. |

**Posting flow (step by step):**

1. Select a line on the **Warehouse Job Overview**.
2. **Start** — status changes to **Started**, an event entry is created.
3. Perform the physical warehouse work (pick, put away, receive/issue goods, reclassify).
4. **Partially Finish** (remaining quantity stays open) **or** **Finish** (fully).
5. The module posts the matching source document automatically: the warehouse shipment via the warehouse shipment posting run, the warehouse receipt via the warehouse receipt posting run, the pick/put-away via the warehouse activity registration, the item reclassification via the item reclassification posting.
6. Check the result via **Event History**.

**Automatic completion from the document:** If a source document is posted or registered directly in standard (Warehouse Shipment, Warehouse Receipt, warehouse activity or reclassification journal), the module automatically sets the associated Warehouse Job Overview line to **Finished**, without posting again. This keeps the Warehouse Job Overview up to date even when posting was done outside the list.

### Item Reclassification Lines

For lines with the source **Item Reclassification** (Item Reclassification Journal), the **Item Reclassification Lines** area is displayed below the list. There you see the journal lines with source and destination bin. Via the associated actions, you reach the **Bin Contents**, the **Dimensions** and the **Item Tracking Lines** of the line. Completion is done via **Finish** as with all other source types; the item reclassification is then posted in the stored journal batch (prerequisite: New Bin Code is filled).

## History and Tracking

Every status change of a Warehouse Job Overview line (Start, Partially Finish, Finish) is logged. This makes it possible to trace when and by whom a line was processed.

**Entry point:** On the **Warehouse Job Overview** page, select the desired line and choose the **Event History** action. The **Whse. Job Event Lines** page opens.

| Field | Explanation |
|---|---|
| **Status** | Shows which status the line changed to with this event (e.g. Started, Partially Finished, Finished). |
| **Date** | Shows the date of the status change. |
| **Time** | Shows the time of the status change. |
| **Quantity** | Shows the quantity relevant at the time of the event. |
| **Location Code** | Shows the location of the processed line. |
| **Bin Code** | Shows the bin of the processed line. |

For each event, the system additionally stores the creating user as well as the previous start date, so that the processing duration per line can be traced.

## Typical Use Cases

The following scenarios show typical triggers and the complete flow in Business Central. All pages and actions are present in the module and behave as described.

### Picking a Warehouse Shipment for a Sales Order

- **Trigger:** A released sales order is ready to ship; a warehouse shipment was created from it.
- **Entry point in BC:** The warehouse worker uses **Search** to open the **Warehouse Job Overview** page. In the **Filters** area, they select their shipping filter template via **Template Filter Code**; the list shows only the warehouse shipments of their **Workgroup**.
- **Core flow:** They select the line (source Warehouse Shipment, Customer Name and Sales Order No. visible) and choose **Start** — the status changes to **Started**. After picking, they choose **Finish**. The module posts the warehouse shipment. If only a partial quantity is ready to ship, they choose **Partially Finish** instead; the remaining quantity stays as an open line.
- **Completion:** Via **Event History** they verify that the line was set to **Finished** with date and time.

### Posting an Internal Item Reclassification Between Bins

- **Trigger:** Stock is to be moved from one bin to another; the movement was entered in an Item Reclassification Journal (journal template with **Warehouse Job Required**).
- **Entry point in BC:** For each journal line, a line has automatically been created in the **Warehouse Job Overview**. The worker filters the list to the item reclassification **Workgroup**.
- **Core flow:** They select the item reclassification line; in the displayed **Item Reclassification Lines** area they see the source and **New Bin Code**. They choose **Start**, perform the item reclassification physically and choose **Finish**. The module posts the item reclassification into the **journal batch** stored in the workgroup.
- **Completion:** The line is at **Finished**; the stock is posted to the new bin.

### Completing a Warehouse Receipt for a Purchase Order

- **Trigger:** A warehouse receipt document was created for a purchase order; the goods have arrived.
- **Entry point in BC:** The warehouse receipt line appears automatically in the **Warehouse Job Overview**. The worker filters to their warehouse receipt **Workgroup**.
- **Core flow:** They select the line, choose **Start**, check the goods and choose **Finish**; the module posts the warehouse receipt. Alternatively, the document can also be posted directly in standard — then the module automatically sets the Warehouse Job Overview line to **Finished**.
- **Completion:** Control via **Event History**.

## FAQ and Troubleshooting

### Why does my warehouse document not appear in the Warehouse Job Overview?

A line is only created if the source process is activated in a **Workgroup** and the affected location is assigned to that group. Check in the **Warehouse Workgroups** whether, for example, **Warehouse Receipt**, **Warehouse Shipment**, **Pick** or **Item Reclassification** is set and whether the location was stored in the **Warehouse Workgroup Lines**.

### Why is the Start action greyed out?

**Start** is only available for lines with status **Open**, **Partially Finished** or **Finished** and a valid source. For a line that is already started, **Partially Finish** or **Finish** is active instead. Lines without a valid source type cannot be started.

### What is the difference between Partially Finish and Finish?

**Finish** posts the source document fully and sets the line to **Finished**. **Partially Finish** posts only the processed partial quantity and sets the status to **Partially Finished**; the remaining quantity is retained as open work and can be started again. An open remaining quantity is explicitly permitted — you do not have to wait for the full settlement.

### What happens if I finish a line that is only partially delivered?

If the quantity to be posted is smaller than the document quantity and you choose **Finish**, the module additionally marks the source document as fully completed. As a result, no further delivery or receipt is expected for the remaining quantity.

### Why can I not fill in the journal fields in the workgroup?

The **Journal Template Name** and the **Journal Batch Name** are only editable if the **Item Reclassification** flag is active in the workgroup. First activate **Item Reclassification**; if you deactivate it again, both fields are cleared automatically.

### Why can the journal template not be selected?

Only Item Journal Templates of the type **Item Reclassification** where the **Warehouse Job Required** field is activated can be selected. First set this flag in the **Item Journal Templates**; the system enforces the **Item Reclassification** type in the process.

### Why can I not open the Bin Capacities page?

Bin Capacity is only available if the **Use Bin Capacity** field is activated in the **Warehouse Job Setup**. Without this flag, the system reports an error on opening. Activate the setup and then open **Bin Capacities** via the Location Card or the bin list.

### How do I change the order of the lines in the warehouse mask?

In the **Warehouse Workgroup Lines** or in the **Warehouse Mask View Line**, assign a **Display Order**. The default interval is derived from the **Increment Display Order by** of the setup. An already assigned display order must not occur twice within the same group — otherwise the system reports an error.

### Why does the warehouse mask not work on the device?

The warehouse mask requires a published web service. Run the **Initialize Web Services** action in the **Warehouse Job Setup** and make sure that the relevant entry under **User Device Setup** has the status **Enabled**.

### Can I undo a line that was finished by mistake?

As long as the line is not already finished, **Reopen** resets the status to **Open**. A line already posted via **Finish** is completed; if it was finished automatically from the document, control corrections via the standard document process of the source document.
