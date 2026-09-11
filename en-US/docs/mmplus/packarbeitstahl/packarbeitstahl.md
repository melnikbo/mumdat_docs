---
title: Anwenderhandbuch FA-Arbeitsvorrat Stahl
---

# User Guide Production Order Job Overview Steel

This guide describes the extension **m+m Production Order Job Overview Steel with Package Mgt.** The app connects the **Production Order Job Overview** of steel manufacturing with **Package Management**: when finishing or partially finishing a production order, users assign the appropriate **packing materials** to the reported **lots**, build the package structure (packages, partitions, items) and post the reported quantity together with its packing materials in a single step. All designations in this guide correspond to the labels shown in Business Central.

## Introduction

### Purpose of the module

The extension integrates package assignment into the **extended response** of the steel-industry Production Order Job Overview. It ensures that every reported lot of a production order is assigned to a packing material before the operation is posted, and that the resulting package structure is carried forward as a **physical package** into the warehouse and item ledger entries when the last response is posted. In addition, the module consistently converts quantities into **KG**, **meters** and **pieces** (handling quantities), as is customary in steel processing.

### Target audience

The primary audience are **operational users** who report and post at the Production Order Job Overview every day: shop-floor workers and response staff at the workstations, as well as warehouse staff who pack lots and maintain the package structure. The secondary audience are **administrators and key users** who prepare the work center setup and the packing-material master data (chapter *Setup*).

### Short process overview

1. The administrator enables the extended output response per work center and enters the package-based response page via the **Confirmation Page No.**
2. The user opens the **Production Order Job Overview**, filters by **Work Center No.** (and, if applicable, **Machine Center No.**) and selects a started line.
3. Via **Finish partially** or **Finish**, the extended response is started. If the package-based response page is set up, **Document Packages List Prod. Order** opens.
4. The user assigns the **Available Lots** to the packing materials (**Assign Lots.** / **Assign All Lots.**), builds the package structure if needed and confirms with **OK**.
5. When the last response is posted, the packing materials become physical packages, item and warehouse ledger entries are created; optionally the packing materials are automatically assigned to the reserved sales order.

---

## Quick start for users

The following order matches the dependency in the code: first setup, then the list, then the transactional actions.

1. **Check the setup (once, administrator):** In the **Work Center Card**, open the action for the Production Order Job Overview work center setup. In the **Extended Output Response** area, enable the extended output response and, in the field **Confirmation Page No.**, enter the package-based response page (**Document Packages List Prod. Order**). See *Set up package-based extended response*.
2. **Open the Production Order Job Overview:** Open the **Production Order Job Overview** via **Search**. Select the **Work Center No.** (and, if applicable, **Machine Center No.**); the corresponding production orders appear.
3. **Select a line and start the response:** Mark a started line and choose **Finish partially** (partial quantity) or **Finish** (completion of the operation).
4. **Assign lots to packing materials:** In **Document Packages List Prod. Order**, mark the lots in the **Available Lots** area and assign them to the selected packing material via **Assign Lots.**, or use **Assign All Lots.**
5. **Build packing materials if needed:** Create the structure with **Create Package**, **Create Partition** or **Create from Package BOM** and fill it with **Fill Package**.
6. **Confirm:** Close the page with **OK**. If assignments are missing, the system reports this (see FAQ).
7. **Post:** When you **Finish** the last response, the packing materials are posted; item and warehouse ledger entries are created, and the packing materials are carried forward as physical packages.

The quick start names only the shortest path. Triggers, roles and special cases are described in the chapter *Typical use cases*.

---

## Setup

The setup of this module is deliberately lean: the app adds **one** controlling field to the Production Order Job Overview work center setup (**Confirmation Page No.**) that unlocks the entire package-based response. The actual packing-material master data (package codes, number series, package BOMs) is maintained in the **m+m Package Management** app and is a prerequisite; it is named here as a prerequisite and linked to the actions that use it.

### Production Order Job Overview work center setup

**Who sets it up and when:** The administrator or key user sets up the work center setup once per work center before the first response. The setup controls which response page the operational users see in the chapter *Daily work*.

**Entry point:** In the **Work Center Card** (standard BC work center master data), open the associated action for the Production Order Job Overview work center setup (object: `Prod. Order Job Work Center Setup`). If no setup exists yet for this work center, the system offers to create it and then opens the card. The setup page is not reachable via **Search**; it is called exclusively from the Work Center Card.

The setup page is a shared surface from the base module, the steel module and this extension. The user sees one page; therefore the following table documents the entire relevant page and highlights the field added by this app.

| Setup | Explanation |
|-------------|-------------|
| **General work center fields** (Work center name, "Unproductive", "Start Multiple Jobs", "No Start-Action required", "Sort By", "Time Posting", "Post Only Duration", "Setup Activity", "Transfer", "Start Date-Time Editable", "Deactivate Direct Search POJ", "Show Sales Order No.", "Show Times") | When these fields are set, they determine the general behavior of the Production Order Job Overview for this work center (display, sorting, time recording, direct search). They come from the base module Production Order Job Overview and do not directly affect package assignment; they are grouped here because only the following fields control the packing-material behavior. |
| **Extended Output Response** (extended output response active) | When enabled, the work center uses the extended output response instead of the simple quantity response; only then can a package-based response page be entered. Without this flag, the field **Confirmation Page No.** has no effect. (Field from the steel base module.) |
| **Ext. O. R. Tr. Qty.** (quantity-based extended response) | When enabled, the extended response works purely quantity-based. For the package-based response, this flag must be **disabled** — otherwise the system refuses to set the **Confirmation Page No.** (check in the code). |
| **Hide Posting Page** (hide posting page) | When enabled, the system skips the interactive response page when posting and posts directly; the user then no longer confirms any package assignment in the posting step. Without the flag, the response page opens before posting. (Field from the steel base module; controls the posting flow, see *Posting and subsequent documents*.) |
| **Confirmation Page No.** | When the page **Document Packages List Prod. Order** is entered here, finishing/partially finishing at the Production Order Job Overview opens the package-based response: the user assigns lots to packing materials before posting. If the field remains empty or points to the material-based standard response page, the classic response runs without package assignment. When set, the system checks that **Extended Output Response** is active and **Ext. O. R. Tr. Qty.** is disabled. (Field of this extension.) |
| **Material and scrap fields** (Material-oriented, Response without material, Post material consumption, scrap location/bin, etc.) | When set, these steel base fields control the material consumption and scrap posting of the operation. They affect package assignment only indirectly (e.g. whether **Show Consumption** is visible in the response) and are grouped here; their full explanation is contained in the guide of the steel Production Order Job Overview. |

#### Set up package-based extended response

This capability requires several configuration steps in dependency order. Who sets it up: administrator/key user, before the first response, per work center. Where it takes effect: in the chapter *Daily work* on **Finish**/**Finish partially**.

1. **Provide packing-material master data (prerequisite):** In **m+m Package Management**, make sure that package codes, the associated **number series** for package numbers and — if used — **package BOMs** exist. If these are missing, the user cannot create packing materials later (the system reports, for example, that no number series is set).
2. **Enable the extended output response:** In the work center setup, enable **Extended Output Response**. When enabled, the work center switches from the simple quantity response to the extended response; only then is step 4 possible.
3. **Exclude quantity mode:** Make sure that **Ext. O. R. Tr. Qty.** is disabled. If this flag remained set, the system would reject the Confirmation Page No. and the package-based response would not be possible.
4. **Set the Confirmation Page No.:** In the field **Confirmation Page No.**, enter the page **Document Packages List Prod. Order**. When set, finishing/partially finishing at the Production Order Job Overview opens exactly this page and the user assigns lots to packing materials.
5. **Optionally control the posting page:** Enable **Hide Posting Page** if no interactive response page should appear when posting; the user then confirms packing materials already in the response step and not again when posting.

**Operational completion:** The user later triggers the chain via **Finish**/**Finish partially** at the Production Order Job Overview (see *Daily work → Document Packages List Prod. Order*).

#### Set up package-reference-based package creation

This second capability makes it possible to automatically generate the package structure from a **Package Reference No.** stored on the production order, instead of building it manually. Who sets it up: administrator/key user together with those responsible for packaging specifications; where it takes effect: in the **Extended Response Material** via the action **Create from Package Reference**.

1. **Maintain package references (prerequisite):** In **m+m Package Management**, create the package references (packaging specifications) that are to serve as a template. When present, the user can select them on the production order.
2. **Store the reference on the document:** In the **Extended Response Material**, the user selects the appropriate reference in the field **Package Reference No.** When set, the system checks the reference against the production order line and adopts it as the default.
3. **Generate the structure:** Via **Create from Package Reference**, the system builds the package structure according to the reference and distributes the reported lot quantities across the packing materials. If packing materials already exist, the system asks for safety whether it should continue.

Both setup paths overlap on the response page: if the Confirmation Page No. is set to **Document Packages List Prod. Order**, both the manual lot assignment and — with a maintained reference — the reference-based generation are available.

### Permissions

The app ships the permission set **MuM PSP Permission**. It defines which actions users may perform in the package response and posting objects of this extension. Assign it to the roles that report and post at the Production Order Job Overview, in addition to the permissions of the base and package modules.

---

## Master data and lists

This module maintains no master data cards of its own (package codes and package BOMs reside in m+m Package Management). However, it extends two central lists with quantity and reference information and provides the Production Order Job Overview list as the entry point.

### Production Order Job Overview (entry list)

The **Production Order Job Overview** is the overview of all production orders per work center and the starting point of daily work. It is opened via **Search**. This extension does not add any columns to the list, but hooks into the actions **Finish** and **Finish partially** (see *Daily work*).

#### Filters

The list is filtered via the header fields. The entry is **work-center-oriented**: first the work center, then optionally the machine center.

| Filter field | Explanation |
|------------|-------------|
| **Work Center No.** | When set, the lines are filtered to the production orders of this work center; this is the first, leading filter. |
| **Machine Center No.** | When set, the lines are additionally restricted to this machine center. Optional — with pure work-center control, the field remains empty. |
| **Prod. Order No.** | When set, filtering is applied to a specific released production order. |
| **Date** | When set, the lines are filtered by date. |
| **Sort By** | When set, it determines the sort order of the lines. |
| **Hide finished** | When enabled, already finished lines are hidden, so that only open work appears. |
| **Hide open** | When enabled, open lines are hidden (e.g. to check responses already completed). |
| **Postings in previous operation** | When enabled, only lines are shown for which the previous operation already has postings. |

### Extended Package Documents List (extended columns)

This extension adds the industry-typical handling quantities to the document package list of Package Management. This way, per package line, the user sees not only the piece quantity but also KG and meters.

| Field | Explanation |
|------|-------------|
| **Qty. To Handle KG** | When a value is present, it shows the quantity assigned to this package line in kilograms; it is carried forward during lot assignment from the conversion (KG per meter/piece). |
| **Qty. To Handle Meter** | When a value is present, it shows the assigned quantity in meters; for length material the leading control quantity of the assignment. |
| **Qty. To Handle Piece** | When a value is present, it shows the assigned piece count; for piece-based material the leading control quantity. |

### Physical Packages (extended columns and reference)

After posting, document packages become **physical packages**. This extension adds handling quantities and a reference back to the Production Order Job Overview to the list of physical packages.

| Field | Explanation |
|------|-------------|
| **Qty. To Handle KG** | When a value is present, it shows the quantity contained in the physical package in kilograms; it is adopted from the document package during posting. |
| **Qty. To Handle Meter** | When a value is present, it shows the contained quantity in meters. |
| **Qty. To Handle Piece** | When a value is present, it shows the contained piece count. |
| **No. Of Prod. Order Job Relations** | When the value is greater than zero, there are still unposted document packages (WIP) for this package group. Calling the field opens the **WIP Prod. Document Packages** list with exactly these open document packages. |

---

## Daily work at the Production Order Job Overview

Daily work is controlled by the work center setup (chapter *Setup*): only if **Extended Output Response** is active there and the **Confirmation Page No.** points to **Document Packages List Prod. Order** do the package pages described here appear. Otherwise the classic material-based response runs.

### Extended Response Material (document line)

The **Extended Response Material** is the central response page per production order line. It comes from the steel base module (header area with posting dates/times, material lines with quantities in quantity/KG/meter/piece, remaining and posted quantities, as well as the subpages **Lots** and **Remaining Lots**). This extension adds to the header, one action and one FactBox.

**Elements added by the module:**

| Field / Action | Explanation |
|---------------|-------------|
| **Package Reference No.** (header) | When set, the selected packaging specification is checked against the production order line and adopted as the default for package creation; if a reference was already selected on the production order or sales order, it appears prefilled here. Without a reference, the user builds the packing materials manually. |
| **Output Package Assignment** (action) | Opens the page **Document Package** for the current line. There the user assigns the packing materials to the reported lots and builds the package structure. The action is only active for an editable (started) response. |
| **Create from Package Reference** (action) | When a **Package Reference No.** is maintained, the action generates the package structure automatically according to the reference and distributes the lot quantities across it. If packing materials already exist, the confirmation **"Packages have already been created. Are you sure you want to continue?"** appears first. |
| **Document Package Structure** (FactBox) | Shows, for the current line, the built package structure of the production document, so that the user can check the assignment without switching pages. |

If the user changes the **Quantity** on this page, the module immediately checks whether the package quantity and response quantity still match and points out deviations (see *Posting and subsequent documents*).

### Document Packages List Prod. Order (response page with lot assignment)

If the **Confirmation Page No.** is set up accordingly, **Finish**/**Finish partially** at the Production Order Job Overview opens the page **Document Packages List Prod. Order**. It is a composite page with two areas. The header contains the field **Package Reference No.** (prefilled as above).

#### "Package list" area

Shows the package structure of the document as a tree (packages, partitions, items). Important columns:

| Field | Explanation |
|------|-------------|
| **Package No.** / **Package Code** | Identify the individual package or its package type. |
| **Line Type** | Determines the type of line in the tree. **Package:** a package as a container. **Partition:** a subdivision within a package. **Item:** a packed item (lot) within a package or a partition. |
| **Level** / **Package Parent No.** | Represent the nesting of the tree; the parent number refers to the enclosing package. |
| **Document Line No.** | When set, links the item line to the response/document line; for lines generated from lots not editable. |
| **Qty. To Handle / KG / Meter / Piece** | The quantity assigned to the package; for length/weight material KG/meters lead, for piece material the piece count. |
| **Remaining physical quantity** / **Physical quantity** / **Document quantity** | Show the open physical quantity, the quantity already recorded physically and the document quantity to check the assignment. |
| **From Available Lots** | When enabled, the line was generated from lot assignment; such lines are protected against manual quantity changes. |
| **Do not consume package** | When enabled, this packing material is not posted as consumed during posting (e.g. reusable containers). |

Actions in the Package list area: **Create Package**, **Create Partition**, **Create from Package BOM**, **Fill Package**, **Select Package**, **Select Package Item**, **Delete Package Group** as well as **Move Up/Move Down/Move Left/Move Right** to move lines in the tree.

#### "Available Lots" area

Shows the reported lots that are not yet fully packed. Here the user enters the quantities to be packed.

| Field | Explanation |
|------|-------------|
| **Item No.** / **Variant Code** / **Lot No.** / **Serial No.** | Identify the available lot. |
| **Location Code** / **Bin Code** | Origin location/bin of the lot; controls which packing material it may be assigned to (location/bin must match). |
| **Total Quantity / KG / Meter / Piece** | The total available lot quantity in the four sizes (not editable). |
| **Quantity to Pack / KG / Meter / Piece** | The quantity the user currently wants to pack. When a value is entered, the module converts the remaining sizes; the value must not exceed the not-yet-packed remaining quantity, otherwise the message **"… must be less or equal than …"** appears. |
| **Quantity Packed / KG / Meter / Piece** | The quantity already packed (sum of the assigned package lines). |
| **Completely Packed** | When enabled, the lot is fully assigned to a package; only then can the operation be finished. |

**Actions (ribbon):**

| Action | Explanation |
|--------|-------------|
| **Assign Lots.** | Assigns the lots marked in the Available Lots area to the **one** package marked in the Package list area (only one package may be marked, otherwise message **"Only one package can be selected."**). The assigned quantity is created as an item line under the package. |
| **Assign All Lots.** | Assigns all matching available lots to the marked package, without the user having to mark each lot individually. |
| **Remove Lots. From Packing Material** | Removes item lines previously generated from lots that are not yet posted back out of the packing materials, so that the lots can be assigned again. |
| **Show Consumption** | Shows the material consumption for the extended output response. Visible only when the work center posts material consumption. |

Confirming with **OK** adopts the assignment; **Cancel** discards it.

### Document Package (package worksheet)

The action **Output Package Assignment** in the Extended Response Material opens the worksheet **Document Package**. It serves to build the package structure for exactly one response line and shows at the top the key figure **Qty. pending to Adjust** (open quantity still to be distributed). As long as this value would be less than zero, the page cannot be closed (message **"Qty. pending to adjust is less than zero…"**).

The lines form the same package tree as above (Line Type Package/Partition/Item, Level, Description, quantity, Location/Bin, Physical, handling quantities KG/Meter/Piece). Technical columns (Entry No., Sequence, Level, partition details, source record) are hidden by default.

**Actions:**

| Action | Explanation |
|--------|-------------|
| **Create Package** | Opens the *Create Package* dialog for creating one or more packages. |
| **Create from Package BOM** | Generates the package structure from a stored package BOM of Package Management. |
| **Fill Package** | Fills an existing package with the reported items/lots (dialog *Fill Package Document*). |
| **Select Package** | Adopts an existing physical package as a template into the document. |
| **Delete Package Group** | Deletes the marked package group after the confirmation **"Do you want to delete selected Package Groups?"**. |
| **Move Up / Move Down / Move Left / Move Right** | Move a line in the tree: Move Left/Move Right change the nesting level, Move Up/Move Down the order. |

### Package creation dialogs

Three dialogs support the building of the structure:

#### Create Package

| Field | Explanation |
|------|-------------|
| **Package Code** | When chosen, for exactly one package the next **Package No.** is automatically proposed from the number series and Description/Description 2 are adopted from the package code. |
| **Package No.** | The unique number of the package to be created; for multiple packages the system assigns it automatically. |
| **Description** / **Description 2** | Are adopted from the package code and serve for identification. |
| **Location Code** / **Bin Code** | Determine where the packing material is managed; for bin-mandatory locations the bin is mandatory. |
| **Number of Packages** | When greater than one, the system creates multiple packing materials of the same kind with automatically assigned numbers. |
| **Create Package Inside Another Package** | When enabled, the new packing material is created inside an existing package; the fields **To Package No.** / **To Package Code** define the target. |

#### Create Partition

| Field | Explanation |
|------|-------------|
| **Package Code** (partition) | When chosen, partition type and description are adopted from the selected partition code. |
| **Partition Type** | Shows the partition type derived from the code (not editable). |
| **Description** | Identifies the partition. |
| **To Package No.** | The package in which the partition is created. If it is empty, the system reports on closing **"Can not create package inside package with empty Package No."**. |

#### Fill Package Document

| Field | Explanation |
|------|-------------|
| **To Package No.** / **To Package Code** | Determine the target package into which the marked items/lots are filled. |
| **Lines (item, lot, quantity, KG/Meter/Piece, Location/Bin)** | Show the fillable response lines; the handling quantities KG/Meter/Piece can be adjusted before filling. |

### WIP Prod. Document Packages and Select Package

- **WIP Prod. Document Packages** (via **Search** or from the key figure **No. Of Prod. Order Job Relations** of the physical packages): shows all not-yet-posted document packages as a tree, so that the user recognizes open packing work.
- **Select Package** (via **Search** or from the action **Select Package**): lists the physical packages per location/bin. Via **Select Package Group** the user marks an entire package group for adoption.

---

## Posting and subsequent documents

The posting flow is hard-wired in the code and ties into the response. The following order applies to the package-based response (Confirmation Page No. = **Document Packages List Prod. Order**):

1. On the **Production Order Job Overview**, mark a started line.
2. Choose **Finish partially** (partial quantity) or **Finish** (completion).
3. **Document Packages List Prod. Order** opens; assign lots to packing materials (**Assign Lots.** / **Assign All Lots.**), add to the structure if needed, confirm with **OK**.
4. On **Finish**, the system checks that **all** available lots are completely packed. If a lot is not **Completely Packed**, it aborts with **"Packing material has not been assigned to all lots."**.
5. Afterwards the system checks whether the package quantity and reported quantity match:
   - On the **last operation** and **Finish**, a deviation is not permitted: **"The mismatch between package item quantity and the output quantity must be fixed before finishing last operation of the production order"**.
   - Otherwise the confirmation **"There is a mismatch between package item quantity and the output quantity. Do you want to finish the job?"** appears, or the offer to adjust the packing materials (**"There is a mismatch between package item quantity and the output quantity. Do you want to adjust packages?"**), which opens the document package list.
6. The module transfers the assigned packing materials into the document package structure of the production order line.
7. If **Hide Posting Page** is set, the interactive response page is skipped when posting; the system posts directly.
8. When posting the **output of the last operation**, the document packages become **physical packages**: item and (for bin-mandatory locations) warehouse ledger entries are created, the lines are marked as **Ledger Posted** and **Warehouse Posted** and flagged as **Posted From Prod. Order Job. Overview**.
9. If automatic sales assignment is active in Package Management and the posted quantity is reserved for a sales order line, the resulting packing materials are automatically assigned to this sales line.

**Partial quantities:** **Finish partially** is explicitly permitted; the module transfers the packing materials even for a partial response. A requirement to "only close on complete quantity balance" exists **only** for the last operation on full **Finish** (step 5). For earlier operations, the user can confirm the deviation and continue.

---

## History, archive and tracking

- **WIP Prod. Document Packages:** Open, not-yet-posted document packages per production order; serves to track open packing work before posting.
- **Physical Packages:** Packages created after posting with handling quantities KG/Meter/Piece; via **No. Of Prod. Order Job Relations** it is possible to jump back to still-open document packages.
- **Archive (Arch Document Packages List Prod. Order):** When a production order is archived, the module transfers the package structure into the archived response views. This keeps it traceable which lots were reported in which packing materials. The archived views are not editable.

---

## Typical use cases

The following scenarios show the flow starting from realistic triggers. All named pages and actions are stored in the code.

### Scenario 1 — Pack and report steel lengths from production

1. **Trigger:** A worker reports at the workstation that a started production order for bar steel is ready to be reported.
2. **Entry in BC:** The reporter opens the **Production Order Job Overview** via **Search**, selects the **Work Center No.** and marks the started line.
3. **Core flow:** He chooses **Finish**. Since the **Confirmation Page No.** is set to **Document Packages List Prod. Order** for the work center, this page opens. In the **Available Lots** area he enters, per lot, the **Quantity to Pack** (or **… Meter/KG**), marks the target package in the **Package list** area and chooses **Assign Lots.** If a container is still missing, he creates it via **Create Package**. Once all lots are **Completely Packed**, he confirms with **OK**.
4. **Completion:** When posting, the system checks the complete assignment and the quantity match, carries the packing materials forward as physical packages and creates item and warehouse ledger entries. The posted lines appear as **Posted From Prod. Order Job. Overview**.

### Scenario 2 — Packing according to packaging specification (package reference)

1. **Trigger:** A fixed packaging specification applies to a customer order; sales has stored a package reference on the production order.
2. **Entry in BC:** The reporter opens the **Production Order Job Overview**, selects the line and starts the response; alternatively he works in the **Extended Response Material**.
3. **Core flow:** In the field **Package Reference No.**, the prefilled reference appears. He chooses **Create from Package Reference**; the system builds the package structure according to the reference and distributes the lot quantities. If there are lots without an assigned quantity, the system asks **"There are some lots without Quantity To Assign. Do you want to continue?"**. After confirmation it reports **"Documents Packages created successfully."**.
4. **Completion:** He finishes the operation; posting proceeds as in Scenario 1. If automatic sales assignment is active and the posted quantity is reserved, the system assigns the packing materials directly to the sales order.

### Scenario 3 — Partial response with later remainder packing

1. **Trigger:** Only part of the lot is packed; the remainder follows in a later shift.
2. **Entry in BC:** The reporter opens the **Production Order Job Overview** and marks the started line.
3. **Core flow:** He chooses **Finish partially**, enters in **Document Packages List Prod. Order** only the already-packed **Quantity to Pack**, assigns it via **Assign Lots.** and confirms with **OK**. Since this is not the last operation or is a partial quantity, a complete quantity balance is not enforced; a remaining quantity stays open.
4. **Completion:** In a later shift he opens the line again, packs the remainder and **finishes** the operation. Only then does the system require the complete assignment of all lots.

---

## FAQ and troubleshooting

### Why does no package page open on Finish, but the normal response instead?
Because in the work center setup the **Confirmation Page No.** is not set to **Document Packages List Prod. Order** or **Extended Output Response** was not enabled. Without this setup, the classic, material-based response runs.

### Why can the Confirmation Page No. not be set?
On setting, the system requires that **Extended Output Response** is active and **Ext. O. R. Tr. Qty.** is disabled. If quantity mode (Ext. O. R. Tr. Qty.) is active, the input is rejected. First enable the extended output response and disable quantity mode.

### What happens if not all lots are assigned a packing material?
On **Finish**, the system aborts with **"Packing material has not been assigned to all lots."**. Assign the open lots in the **Available Lots** area until the flag **Completely Packed** is set everywhere.

### Why does the system report "Only one package can be selected."?
**Assign Lots.** always assigns lots to exactly **one** package. Mark only a single package in the **Package list** area and trigger the action again.

### What does the deviation message on the last operation mean?
If package quantity and reported quantity do not match on the last operation, the system requires the correction before completion: **"The mismatch between package item quantity and the output quantity must be fixed before finishing last operation of the production order"**. Adjust the quantities to be packed or the packing materials until the quantities match.

### Can I report an operation partially?
Yes. Via **Finish partially** you report a partial quantity; the module transfers the assigned packing materials even for a partial response. The complete quantity balance is only enforced on **Finish** of the last operation.

### Why can I not close the "Document Package" page?
When the quantity still to be adjusted would be less than zero, the system reports **"Qty. pending to adjust is less than zero. Please adjust the quantities before closing the page."**. Correct the item quantities in the structure so that the pending quantity is not negative.

### Why can I not change the quantity of a line generated from lots?
Lines with the flag **From Available Lots** are created from lot assignment and are protected against manual quantity changes. Use **Remove Lots. From Packing Material** and reassign the lot with the desired quantity.

### Why does "Create Package" fail with a number-series hint?
No package number series is stored for the selected **Package Code**, or the central series in Package Management is missing. Store the number series in m+m Package Management.

### Where do I see what is already posted and what is still open?
Open, not-yet-posted document packages are shown by the **WIP Prod. Document Packages** list (also reachable via the key figure **No. Of Prod. Order Job Relations** at the physical packages). Posted packing materials appear as **physical packages** and carry, on the document line, the flags **Ledger Posted** / **Warehouse Posted** as well as **Posted From Prod. Order Job. Overview**.
