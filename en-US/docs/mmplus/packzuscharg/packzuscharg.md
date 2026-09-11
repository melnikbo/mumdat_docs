---
title: Anwenderhandbuch m+m Additional Lot Information with Package Management
---

# User Guide m+m Additional Lot Information with Package Management

## Introduction

The **m+m Additional Lot Information with Package Management** app connects two existing m+m apps with one another: **m+m Additional Lot Information** and **m+m Package Management**. It ensures that the **Vendor Lot No.** stored for a lot becomes directly visible in the **Physical Packages** overview.

From a business perspective, the app solves a simple but important task in goods receipt and logistics: anyone working with a physical package sees at a glance which **Vendor Lot No.** is assigned to the lot it contains – without having to open the item's lot number information separately. To do this, the app adds exactly one additional, read-only field to the **Physical Packages** overview and automatically reads its value from the lot.

**Target audience:** This guide is aimed primarily at **operational users** in goods receipt, warehouse, and logistics who work with physical packages and lots every day and who need the Vendor Lot No. while processing them. Secondarily, it concerns users who, as part of lot maintenance, record the **Vendor Lot No.** on the **Lot No. Information** so that this value later appears in the package overview.

**Brief process overview:**

1. During goods receipt or lot maintenance, the **Vendor Lot No.** is stored on the lot's **Lot No. Information** (this value originates from the m+m Additional Lot Information app).
2. In the **Physical Packages** overview, the app automatically displays this value per line in the new **Vendor Lot No.** column – matching the line's Item No., Variant Code, and Lot No.

**Prerequisites:** The app is an extension (bridge) and requires the installed base apps **m+m Package Management** (provides the **Physical Packages** page), **m+m Additional Lot Information** (provides the **Vendor Lot No.** on the lot), and **m+m Cloud Base**. Without these apps there is neither the overview to be displayed nor the value to be read. A valid **license** is also required for use: the app automatically checks the license when the user signs in; if no valid license is present, the additional column is not available. Complete lot and package maintenance is described in the guides for the two base apps; this guide is limited to the additional function that this app contributes.

## Quick Start for Users

The fastest way to the result – seeing a package's Vendor Lot No.:

1. **Store the Vendor Lot No. on the lot (prerequisite).** Open the **Lot No. Information** of the relevant lot (via the item card or the item's item tracking) and enter the vendor's lot number in the **Vendor Lot No.** field. This step is only necessary as long as the value has not yet been maintained.
2. **Open the overview.** Using the **Search** in Microsoft Dynamics 365 Business Central, open the **Physical Packages** view.
3. **Find the line.** Search for or sort to the desired package line (e.g. by **Item No.**, **Lot No.**, or **Package No.**).
4. **Read the Vendor Lot No.** In the **Vendor Lot No.** column, the value stored for the lot is displayed automatically. The field is read-only; a change is made exclusively via the **Lot No. Information** (see step 1).

> Note: This app does not add any actions or postings of its own. All actions of the **Physical Packages** overview (e.g. **Fill Package**, **Move Item**) come from the m+m Package Management base app and are documented there.

## Data Source and Prerequisites

The app only displays the **Vendor Lot No.** – it does not create or store it itself. The value is created elsewhere and read from there. For the column to be filled, two prerequisites must be met: the lot must carry a **Vendor Lot No.**, and the app license must be valid.

### Origin of the value: Lot No. Information

The **Vendor Lot No.** is maintained on the **Lot No. Information** of the respective lot. This field is provided by the **m+m Additional Lot Information** app. Whoever maintains the lots (typically in goods receipt or in quality assurance) enters the lot number assigned by the vendor there. Only then can the package overview display this value.

The following applies when recording or changing the **Vendor Lot No.** on the lot:

- If a value is entered, it is stored as the vendor lot for the lot and is subsequently available to all evaluating views – including the **Physical Packages** overview.
- If the **Vendor Lot No.** is changed afterwards and item ledger entries already exist for this lot, a confirmation prompt appears. If the user confirms, the changed vendor lot number is applied consistently to the affected entries; if the user declines, the previous value is retained. This keeps the traceability of the vendor lot ensured across all postings.

Further details belonging to the lot from m+m Additional Lot Information (for context only, to show where the Vendor Lot No. sits):

| Field | Explanation |
|-------|-------------|
| **Vendor Lot No.** | If the vendor's lot number is stored here, then exactly this value is displayed in the **Physical Packages** overview in the column of the same name; without an entry, the column there remains empty. |
| **Vendor Internal Lot No.** | If set, the lot number used internally by the vendor is available for queries and evaluations; it supplements the official Vendor Lot No. but is not shown in the package overview by this app. |
| **Country/Reg. Of Orig. Code** | If maintained, the origin of the lot is documented; relevant for proofs of origin, not part of this app's package display. |
| **Manufacturer Code** | If set, the manufacturer of the lot is stored; used for traceability, independent of the package display. |
| **Bundle** | If enabled, the lot is marked as a bundle; controls evaluations in m+m Additional Lot Information, not the display of this bridge app. |

### License Prerequisite

The app checks the license automatically when the user signs in. If the app is installed and licensed, then the additional **Vendor Lot No.** column is available in the **Physical Packages** overview. If no valid license is present, then the additional function is not activated. No manual setup steps are required for this check; the user does not need to configure anything.

## The "Physical Packages" List

The **Physical Packages** overview can be reached via the **Search** in Microsoft Dynamics 365 Business Central. It comes from the m+m Package Management app and lists the currently existing physical packages per line (packages, contained items, and partitions). New lines are not created directly here; maintenance is done via the base app's actions. This app adds exactly one read-only column to the list: **Vendor Lot No.**

### Columns of the Overview

The following table describes the columns visible in the overview (the base app columns and the column added by this app together, since the user sees a single list):

| Field | Explanation |
|-------|-------------|
| **Package No.** | Shows the number of the physical package; this is how the user identifies the specific package in the list. |
| **Package Code** | Shows the code of the underlying package definition; this is how the user recognizes the type of package. |
| **Reserved** | Shows the reserved quantity for this line; if the value is greater than zero, then the inventory is already assigned to a process and is not freely available. |
| **Item No.** | Shows the item contained in the package; together with Variant Code and Lot No., this value determines which **Vendor Lot No.** is displayed. |
| **Variant Code** | Shows the item variant of the line; it is used in determining the Vendor Lot No. |
| **Serial No.** | Shows the serial number, provided the item is serial-number tracked. |
| **Lot No.** | Shows the lot number of the contained item; via this Lot No. (together with Item No. and Variant Code) the **Vendor Lot No.** is determined from the Lot No. Information. |
| **Line Type** | Indicates what content the line describes. See the explanation of the values immediately below this table. |
| **Partition Type** | Indicates the orientation of a partition. See the explanation of the values below this table. |
| **Partition Code** | Shows the code of the partition; relevant when the line describes a partition. |
| **Package Group No.** | Shows the number of the package group the line belongs to; this is how the user recognizes packages that belong together. |
| **Package Group Code No.** | Shows the group code of the package group; used to assign several packages to one group. |
| **Entry No.** | Shows the internal sequential number of the entry; used for the unique technical identification of the line. |
| **Sorting No.** | Controls the display order; this keeps the tree view of the packages stably sorted. |
| **Sequence Line No.** | Shows the line number within the sort order; supplements the Sorting No. for a unique order. |
| **Level** | Shows the level of the line in the package structure; this is how the user recognizes the nesting (e.g. package over partition over item). |
| **Package Parent Code No.** | Shows the parent group code of the line; assigns the line to its higher-level package structure. |
| **Package Parent No.** | Shows the parent package; this makes the parent-child relationship in the structure traceable. |
| **Description** | Shows the name of the package or item of the line. |
| **Description 2** | Shows a supplementary name, if maintained. |
| **Quantity** | Shows the quantity of the line's content; this is how the user sees how much is contained in the package. |
| **Location Code** | Shows the location of the package; this makes the physical location recognizable. |
| **Bin Code** | Shows the bin within the location; supplements the location with the exact storage position. |
| **SSCC Code** | Shows the SSCC (Serial Shipping Container Code) of the package, if assigned; used for shipment and consignment identification. |
| **Vendor Lot No.** *(added by this app)* | If a Vendor Lot No. is stored on the **Lot No. Information** for the line's lot (Item No. + Variant Code + Lot No.), then this column automatically displays exactly this value. This way the user sees the vendor lot directly on the package, without opening the Lot No. Information separately. The field is read-only and is continuously calculated from the lot; a change is made exclusively on the **Lot No. Information**. |

**Values of the Line Type field** (indicates what the line represents – all possible values):

- **(blank):** Line without a specific classification – the line is not assigned to any of the following types.
- **Package:** The line describes the package itself (the outer package).
- **Item:** The line describes an item contained in the package; the **Vendor Lot No.** is only functionally relevant for these lines, because Item No. and Lot No. are present here.
- **Partition:** The line describes a partition within the package.

**Values of the Partition Type field** (only relevant for lines with Line Type Partition – all possible values):

- **Horizontal:** The partition is arranged horizontally.
- **Vertical:** The partition is arranged vertically.

### Actions of the Overview (Context)

The **Physical Packages** overview provides actions of the m+m Package Management base app, including **Fill Package**, **Create Package**, **Create from Package BOM**, **Create Partition**, **Package References**, **Move Package to Another Package**, **Change Package Group Location/Bin**, **Move Item**, and **Delete Package Group**. These actions are **not** changed or extended by this app; their operation is described in the m+m Package Management guide. No dedicated actions are required for the additional **Vendor Lot No.** column – the value is displayed automatically.

## FAQ and Troubleshooting

### Why don't I see a "Vendor Lot No." column in "Physical Packages"?
The column is only provided if the app is installed and licensed. Check whether the **m+m Additional Lot Information with Package Management** app is active. The column may also simply be hidden by personalization; show it again via **Personalize**.

### Why is the "Vendor Lot No." column empty for a line?
The app only displays the value if a **Vendor Lot No.** is maintained for the line's lot. If the entry is missing on the **Lot No. Information** (combination of Item No., Variant Code, and Lot No.), then the column remains empty. Add the value on the Lot No. Information.

### Why can't I change the "Vendor Lot No." in the package overview?
The field is deliberately read-only, because it only displays the value from the lot. The Vendor Lot No. is maintained exclusively on the **Lot No. Information**; the overview takes the value from there automatically.

### Where do I maintain the "Vendor Lot No." correctly?
On the **Lot No. Information** of the relevant lot, in the **Vendor Lot No.** field. You reach this via the item or its item tracking. After saving, the value automatically appears in the package overview.

### What happens if I change the "Vendor Lot No." afterwards, even though postings have already been made?
If item ledger entries already exist for the lot, a confirmation prompt appears when you make the change. If you confirm, the new value is applied consistently to the affected entries; if you cancel, the previous value remains. This preserves traceability.

### Why does the displayed "Vendor Lot No." differ from the expected lot?
The assignment is made via the **Item No.**, **Variant Code**, and **Lot No.** of the package line. If one of these values does not match the maintained lot, then a different value or no value is displayed. Check the three key fields of the line against the Lot No. Information.

### Do I have to set anything up for this app?
No. The app has no setup page of its own and no flags. The only prerequisites are the installed base apps, a valid license, and a maintained Vendor Lot No. on the lot.

### Which permissions do I need?
You need the permissions that also apply to the **Physical Packages** overview (m+m Package Management) and to the **Lot No. Information** (m+m Additional Lot Information). The additional column itself does not require any separate authorization beyond the license check.

### Why is the column not available immediately after installation?
The license is checked at **sign-in**. Sign in again after the installation so that the check runs anew and the additional column is activated.

### Does this app change anything about the postings or actions of the packages?
No. The app only adds a read-only display column. It does not change any postings, any actions (e.g. **Fill Package**, **Move Item**), or any quantities. All of these functions remain unchanged as part of the m+m Package Management base app.

## Typical Use Cases

The following scenarios show realistic triggers and the chronological flow in Business Central. All the pages, fields, and behaviors mentioned are defined in the code of the apps involved.

### Use Case 1: Record the vendor lot at goods receipt and make it visible on the package

**Trigger:** A delivery arrives; the vendor's lot number is printed on the containers. It is to be stored in Business Central so that it is later visible on the package.

**Entry in BC:** For the relevant item, the user opens the **Lot No. Information** of the newly received lot (via the item's item tracking).

**Core flow:**
1. In the **Vendor Lot No.** field, the user enters the lot number assigned by the vendor.
2. On saving, the value is stored for the lot and is available to evaluating views.
3. The user then opens the **Physical Packages** overview via the **Search**.
4. In the line of the corresponding package (matching **Item No.**, **Variant Code**, and **Lot No.**), the value now appears automatically in the **Vendor Lot No.** column.

**Conclusion:** The vendor lot is visible on the package; opening the Lot No. Information separately is no longer necessary for daily package work.

### Use Case 2: Look up the vendor lot during package processing

**Trigger:** An employee in warehouse/logistics is processing a package and has to state the **Vendor Lot No.** of the contained lot to a customer or to quality assurance.

**Entry in BC:** The user opens the **Physical Packages** view via the **Search**.

**Core flow:**
1. The user filters or sorts the list by **Package No.**, **Item No.**, or **Lot No.** to find the correct line.
2. In the **Vendor Lot No.** column, they read the value stored for the lot directly.
3. If the column is empty, the user recognizes that the Vendor Lot No. has not yet been maintained on the lot (see Use Case 1).

**Conclusion:** The required information is available immediately in the package overview; the information can be provided without switching to other views.

### Use Case 3: Correct an incorrectly recorded vendor lot

**Trigger:** It is noticed that an incorrect **Vendor Lot No.** has been stored for a lot, even though postings (item ledger entries) already exist for this lot.

**Entry in BC:** The user opens the **Lot No. Information** of the affected lot.

**Core flow:**
1. In the **Vendor Lot No.** field, the user changes the value to the correct vendor lot.
2. Because item ledger entries already exist for the lot, a confirmation prompt appears asking whether the change should be applied to the existing entries.
3. If the user confirms, the corrected Vendor Lot No. is applied consistently to the affected entries; if the user declines, the original value remains.
4. After the update, the **Physical Packages** overview automatically shows the corrected value in the **Vendor Lot No.** column.

**Conclusion:** The vendor lot is correct across all postings and correctly visible on the package; traceability is preserved.
