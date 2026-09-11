---
title: "Anwenderhandbuch m+m Metal & Tolling with Material Properties"
---

# User Guide m+m Metal & Tolling with Material Properties

## Introduction

This guide describes the app **m+m Metal & Tolling with Material Properties**. The app connects two existing m+m modules: the **Material Properties** module (with the **Create Item Template** page) and **Metal & Tolling** (with the metal and tolling master data on the item). It adds exactly one additional flag at a single point — **Tolling** — and uses it to control whether, when an item is created or copied, the complete metal and tolling data of the source item is transferred to the new item or deliberately reset.

**Target audience.** The primary users are **operational users of item management** — people who, in day-to-day work, create new items from a template or copy existing items (for example, master data maintenance, work preparation, and sales and purchase master data). The secondary audience are **administrators and key users** who set up the material types and the associated metal and tolling master data, so that the **Tolling** flag can take effect in a meaningful way at all.

**Brief process overview.** The typical path runs along the following chain: for a **Material Type** you open the associated **Create Item Template**, define there which information areas are transferred when copying, and activate the **Tolling** flag if required. During the subsequent copying of an item, this flag decides whether the metal and tolling data is carried over. This app has no posting of its own, no reports of its own, and no lists of its own; its benefit lies in the correct transfer or clean-up of the tolling data.

## Quick Start for Users

The fastest way to a result (order: setup/template first, then the actual activity):

1. **Check the prerequisite:** The source item already has maintained metal and tolling master data (Metal Account, etc.) from the Metal & Tolling module. Without this master data there is nothing to transfer. See **Prerequisites and Dependent Setup**.
2. **Open the template:** On the **Material Type Card**, for the desired material type, open the action that opens the **Create Item Template** page. When doing so, select the appropriate **Creation Type** (**Base Item** or **Variant Item**).
3. **Define the copy scope:** In the **General** group, enable the areas that are to be copied, and set the **Tolling** flag if the metal and tolling data is to be transferred as well.
4. **Copy the item:** Copy an existing item using the standard function for copying items. The new item is created.
5. **Check the result:** With **Tolling** set, the new item carries the metal and tolling data of the source item; with **Tolling** not set, these fields are empty on the new item.

You will find more context and the real-world triggers under **Typical Use Cases**.

## Prerequisites and Dependent Setup

This app does **not** bring its own setup page, no number series, and no report or mail parameters. It acts exclusively on the already existing **Create Item Template / Copy Item** flow. For the **Tolling** flag to have an effect, the dependent modules must be set up correctly. Administrators or key users perform this setup before first use.

### Setting up Tolling transfer during Copy Item

**Process entry point.** This setup concerns the administrator or key user of the master data. It is to be performed once before first productive use, and for every new material type. The result is later used in day-to-day work in the chapter **Copying Items with Tolling Data**. The chain spans several pages from the dependent modules and ends with the actual user action.

**Numbered setup steps (in dependency order):**

1. **Maintain the metal and tolling master data on the source item.** On the item, store the role and the values for Metal & Tolling (for example, **Metal Account**, **Metal Account 2nd Level**, **Waste Code No.**, **Scrap Item**, **Crude Metal**, **Metal Load Carrier**) as well as the associated subtables via the **Item Metal & Tolling Setup** page. *If this data is present, then a transferable data set exists at all;* if it is missing, the app transfers nothing when copying, because there is no source data.
2. **Provide the material type.** Ensure that the relevant **Material Type** exists in the **Material Types** and is reachable via the **Material Type Card**. *If the material type is maintained, then a template can be opened from it;* without a material type there is no entry point into the template.
3. **Set Tolling in the template.** Via the **Material Type Card**, open the **Create Item Template** page and activate the **Tolling** flag (for details see the chapter **Create Item Template and the Tolling Flag**). *If Tolling is activated in the template, then this flag is automatically carried over into the copy buffer when copying* and controls the transfer of the tolling data there.

**Operational conclusion.** The chain is completed in day-to-day work when the user copies an existing item (see the chapter **Copying Items with Tolling Data**). Only this copy operation triggers the transfer or clean-up of the metal and tolling data.

## Create Item Template and the Tolling Flag

**Process entry point.** The **Create Item Template** page defines which information areas of an item are transferred when copying or when creating from the template. It is not a page that can be found via search; instead, it is opened specifically from the **Material Type Card**.

**Entry point:** On the **Material Type Card**, for the desired material type, open the action that opens the **Create Item Template** page. When it opens — if not already present — a template for the selected **Creation Type** (**Base Item** or **Variant Item**) is automatically created. The template is thus permanently bound to one material type and one creation type.

The app extends this page in the **General** group by exactly one field: the **Tolling** flag. All other fields originate from the base module, but are shown to the user on **one** page and are therefore described in full here.

### Creation Type

The **Creation Type** is preset when the template is opened from the **Material Type Card** and determines for which item type the template applies. It is an option field with the following values:

- **Base Item:** The template applies to the creation of a base item. In this case, the **Variant Items** group with the **Copy Variant Items** field is additionally visible.
- **Variant Item:** The template applies to the creation of a variant item. The **Variant Items** group is not shown in this case.

### Fields of the "General" group

The area flags define which information of the source item is carried over when copying. If a flag is activated, the relevant area is transferred; if it is not activated, the area remains empty on the new item, or is set to the default values.

| Field | Explanation |
|---|---|
| **General Item Information** | If activated, the general header data of the item (description and further base data) is transferred to the new item; without activation, the new item starts without this base data. |
| **Units of measure** | If activated, the units of measure of the source item are copied along, so that the new item can be used immediately with the same units (for example, base and sales units). |
| **Dimensions** | If activated, the new item adopts the dimension values of the source item; later posting to cost centers/cost objects therefore takes place without a new assignment. |
| **Picture** | If activated, the stored item picture is copied along; without activation, the new item remains without a picture. |
| **Comments** | If activated, the comments of the source item are transferred. |
| **Planning** | If activated, the planning/replenishment parameters of the source item are copied along, so that the procurement logic takes effect directly for the new item. |
| **Tolling** | If activated, the complete metal and tolling data of the source item is transferred to the new item when copying (Metal Account and further header fields as well as the subtables such as Item Metal Values, Item Reductions, and Metal Account Allocations). If the flag is **not** activated, the metal and tolling header fields on the new item (**Metal Account**, **Metal Account 2nd Level**, **Waste Code No.**, **Scrap Item**, **Crude Metal**, **Metal Load Carrier**) are deliberately reset — the new item therefore starts without a tolling reference. This is the only field added by this app. |

### Fields of the "Sales" group

| Field | Explanation |
|---|---|
| **Sales Prices** | If activated, the sales prices of the source item are copied along; the new item is thus immediately calculated as ready for sale. |
| **Sales Line Disc.** | If activated, the sales line discounts are transferred, so that existing discount tiers continue to apply for the new item. |

### Fields of the "Purchase" group

| Field | Explanation |
|---|---|
| **Purchase Prices** | If activated, the purchase prices of the source item are transferred; the procurement of the new item is thus valued. |
| **Purchase Line Disc.** | If activated, the purchase line discounts are copied along. |

### Fields of the "Service" group

| Field | Explanation |
|---|---|
| **Troubleshooting** | If activated, the troubleshooting of the source item is transferred. |
| **Resource Skills** | If activated, the resource skills are copied along. |

### Fields of the "Extended" group

| Field | Explanation |
|---|---|
| **Item Variants** | If activated, the item variants of the source item are transferred. |
| **Translations** | If activated, the item translations are copied along, so that foreign-language descriptions are retained. |
| **Extended Texts** | If activated, the extended texts of the source item are transferred. |
| **BOM Components** | If activated, the BOM components are copied along. |
| **Item Vendors** | If activated, the assigned item vendors are transferred. |
| **Attributes** | If activated, the item attributes are copied along. |
| **Item References** | If activated, the item references (for example, references to vendor or customer numbers) are transferred. |
| **Stockkeeping Units** | If activated, the stockkeeping units of the source item are copied along, so that warehouse-specific settings are retained. |

### Fields of the "Variant Items" group (only for Creation Type Base Item)

| Field | Explanation |
|---|---|
| **Copy Variant Items** | If activated, the associated variant items are also copied along when creating a base item. The group is only visible if the **Creation Type** is set to **Base Item**. |

### Fields of the "Options" group

| Field | Explanation |
|---|---|
| **Unblock New Item** | If activated, the newly created item is automatically unblocked after copying (the **Blocked** flag is removed) and is immediately usable. If the option is not activated, the new item initially remains blocked and must be released manually before use. |

**Validation/dependency.** The **Tolling** flag only takes effect in a meaningful way if the source item actually has metal and tolling data (see **Prerequisites and Dependent Setup**). The transfer or clean-up takes place automatically during the copy operation; a separate confirmation is not required.

## Copying Items with Tolling Data (Daily Work)

**Control by upstream pages.** This daily flow is controlled by two upstream points: by the **metal and tolling master data** on the source item (maintained via **Item Metal & Tolling Setup**) and by the **Tolling** flag in the **Create Item Template**. Both determine whether and which tolling data reaches the new item.

This is how the copy operation runs:

1. Open an existing item, or select it in the item list.
2. Start the standard function for copying items. The copy scope depends on the flags set in the template, including **Tolling**.
3. Business Central creates the new item.
4. **If Tolling is activated**, the app additionally transfers the metal and tolling data of the source item: the header fields on the item as well as the associated records from **Item Metal & Tolling Setup**, the **Item Metal Values**, the **Item Reductions**, the Metal Account Allocations, and the Hedging Balances.
5. **If Tolling is not activated**, the app resets the metal and tolling header fields on the new item (**Metal Account**, **Metal Account 2nd Level**, **Waste Code No.**, **Scrap Item**, **Crude Metal**, **Metal Load Carrier**). The new item is thus without a tolling reference.

**Note.** The app transfers only those subtables that actually have records on the source item. If an area is empty, it is skipped. No posting and no release takes place; the operation is complete once the new item has been created.

## Permissions

The permission set **MuM MTMP Permissions** is delivered for using the app. This set is assignable and determines the permissions for executing the app logic: it defines which actions users can perform in the context of the tolling transfer, by covering the execution rights for the app's two codeunits (copy logic and event logic). The permissions for the actual metal, tolling, and item data are controlled via the permission sets of the base and dependent modules.

## FAQ and Troubleshooting

### 1. Why can't I find the "Create Item Template" page via search?
The page is deliberately not findable via search. It is opened exclusively from the **Material Type Card** via the associated action, because a template is always bound to a specific **Material Type** and **Creation Type**.

### 2. Where do I activate that the tolling data is copied along?
In the **Create Item Template**, in the **General** group, via the **Tolling** flag. This flag is automatically taken into account when copying.

### 3. What happens if "Tolling" is not set?
The new item is created, but its metal and tolling header fields (**Metal Account**, **Metal Account 2nd Level**, **Waste Code No.**, **Scrap Item**, **Crude Metal**, **Metal Load Carrier**) are reset. The item then has no tolling reference.

### 4. Which data exactly is transferred when "Tolling" is active?
The header fields on the item as well as the records from **Item Metal & Tolling Setup**, the **Item Metal Values**, the **Item Reductions**, the Metal Account Allocations, and the Hedging Balances of the source item.

### 5. Why were no subtables copied even though "Tolling" was active?
The app transfers only subtables that actually contain records on the source item. If, for example, no Item Reductions are maintained on the source item, there is nothing to transfer.

### 6. Must the source item have specific master data for "Tolling" to take effect?
Yes. The source item must have the metal and tolling master data (for example, **Metal Account**). Without this data, nothing can be transferred when **Tolling** is active.

### 7. Why is the new item blocked after copying?
Whether the new item is unblocked is controlled by the **Unblock New Item** flag in the template. If it is not activated, the new item initially remains **Blocked** and must be released manually.

### 8. When is the "Variant Items" group visible?
Only if the **Creation Type** of the template is set to **Base Item**. For **Variant Item**, this group is hidden.

### 9. Does the app create its own postings, reports, or documents?
No. The app only extends the copy behavior with the tolling data. There is no posting of its own, no report of its own, and no document of its own.

### 10. Can I set the behavior differently per material type?
Yes. Since the template is bound to **Material Type** and **Creation Type**, you can set the **Tolling** flag differently per material type and per creation type (base item or variant item).

## Typical Use Cases

### Use Case 1: Creating a new tolling item from a template

**Trigger.** A colleague from work preparation reports by phone that, for an existing material type, a further item variation is needed which is to carry the same metal and tolling conditions as an existing item.

**Entry point in BC.** You open the **Material Type Card** for the relevant material type and invoke the action that opens the **Create Item Template** page for the **Creation Type Base Item**.

**Core flow.** In the **General** group you activate the required areas and set the **Tolling** flag. You then copy the existing tolling item using the standard function for copying items. When the new item is created, the app transfers the metal and tolling data of the source item in full, including the subtables such as Item Metal Values and Item Reductions.

**Conclusion.** The new item carries the same tolling conditions as the source item. If **Unblock New Item** is set in the template, it is immediately usable; otherwise, you release it manually.

### Use Case 2: Duplicating an item without a tolling reference

**Trigger.** By email, the task arrives to duplicate an existing item as a pure trade or standard item — explicitly **without** the metal and tolling binding of the original.

**Entry point in BC.** For the appropriate material type, you open the **Create Item Template** and make sure that the **Tolling** flag is **not** set.

**Core flow.** You copy the source item using the standard function for copying items. Since **Tolling** is not set, the app resets the metal and tolling header fields on the new item (**Metal Account**, **Metal Account 2nd Level**, **Waste Code No.**, **Scrap Item**, **Crude Metal**, **Metal Load Carrier**).

**Conclusion.** The new item is created without a tolling reference and can be used further as a standalone standard item.
