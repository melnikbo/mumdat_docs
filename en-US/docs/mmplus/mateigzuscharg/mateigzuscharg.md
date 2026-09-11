---
title: Anwenderhandbuch m+m Material Properties with Additional Lot Information
---

# User Guide m+m Material Properties with Additional Lot Information

## Introduction

The app **m+m Material Properties with Additional Lot Information** extends Microsoft Dynamics 365 Business Central with additional lot information at the places where users select lots and assess inventory in day-to-day operations. The app does **not** add its own cards, documents, or reports. It supplements existing pages with origin and vendor details about the lot, and it also controls the order in which lots are proposed in the extended search.

Specifically, the app does three things:

1. It displays additional lot fields in the **Material Balances** and in the **Lot Search Result**: vendor lot, vendor internal lot, acquisition date, purchased vendor, country/region of origin, manufacturer, and the bundle indicator.
2. It supplements the **Purchase Order Lots** page with the Item MatchCode and Lot No. MatchCode columns.
3. It adds the value **FiFo** to the distribution logic of the Material Property Setup. When this value is set, the extended lot search proposes the lots in ascending order by acquisition date (oldest lot first).

**Target audience.** The app is aimed primarily at **operational users** who assign lots to document lines in sales and purchasing, as well as at warehouse staff who assess inventory by lot. Secondarily, it concerns **administrators and key users** who define the extended matchcode search and the distribution logic in the Material Property Setup.

**Prerequisites.** The app requires the base apps **m+m Cloud Base**, **m+m Material Properties**, and **m+m Additional Lot Information**. The lot information itself (vendor lot, manufacturer, country of origin, acquisition date, etc.) is maintained on the **Lot No. Information Card** from **m+m Additional Lot Information**; this app makes these values visible on the pages mentioned and uses them for the ordering.

**Process overview.** The administrator activates the extended matchcode search once and sets the distribution logic. After that, users see the additional lot columns in the Material Balances, in the Lot Search Result, and in the Purchase Order Lots, and, when FiFo is active, receive the lot proposals in the desired order.

## Quick Start for Users

Setup precedes day-to-day operations. Perform the steps in this order.

1. Activate **Use Extended Matchcode Search**. Open the **Material Property Setup** via **Search** and select the **Use Extended Matchcode Search** check box. This flag is the prerequisite for the distribution logic.
2. Set the **Distribution Logic (Split Option)**. In the **Split Option** field, choose the value **FiFo** if the lot search should propose the oldest lot first; leave the value on **Manual** if no automatic ordering is desired.
3. **Check inventory.** Open the **Material Balances** and read the acquisition date, vendor lot, manufacturer, and country/region of origin code of the respective lot in the additional columns.
4. **Select a lot in the document line.** Start the extended search from a sales or purchase line. In the **Lot Search Result**, when FiFo is active, the lots are sorted in ascending order by acquisition date; the additional columns show origin and vendor for the lot.
5. Check the **Purchase Order Lots**. In the **Purchase Order Lots** page, the additional columns **Item MatchCode** and **Lot No. MatchCode** are available.

There is no posting or release step in this app; it provides only additional display fields and the lot ordering.

## Setup

Setup is done centrally on the **Material Property Setup** page. This page is a company-wide setup (one record per company) from the base app **m+m Material Properties**. This app does **not** add its own field to the page; it only extends the **Split Option** field with the value **FiFo**. Documented here are the fields that enable and influence the lot ordering controlled by this app.

**Entry point:** Open the **Material Property Setup** page (company-wide setup) via **Search**.

### Setting up the FiFo lot order

**Who and when.** This setup is performed once by the administrator or key user before first use. The setting then takes effect in daily work in the **Lot Search Result** (see the section **Application in Daily Operations → Lot Search Result**).

**Sequence in dependency order.**

1. Activate **Use Extended Matchcode Search**. When this flag is set, the extended matchcode and lot search is enabled overall and the dependent fields (including **Split Option**) become editable. Without this flag, the distribution logic cannot be changed: with every change to the Split Option, the system checks that the extended matchcode search is active and otherwise rejects the entry.
2. Set the **Split Option** to **FiFo**. When the Split Option is set to **FiFo**, the extended lot search automatically sorts the result list in the **Lot Search Result** in ascending order by **Acquisition Date**, so that the oldest lot is proposed and assigned first. If the value remains on **Manual**, the user determines the order themselves and no automatic sorting by acquisition date is performed by this app.
3. **Operational completion.** The chain closes in the document line: as soon as a user starts the extended search from a sales or purchase line, the configured Split Option takes effect and arranges the lots in the **Lot Search Result** accordingly.

**Relevant setup fields**

| Setup | Explanation |
|---|---|
| Use Extended Matchcode Search | When activated, the extended matchcode and lot search is switched on and follow-up settings such as **Split Option**, **Lot Search**, **Item Search**, **In Order**, and **Show All** become editable. If the flag is not set, these settings are locked and the FiFo order provided by this app does not take effect. |
| Split Option | Controls the order in which lots are proposed in the extended search. **Manual:** No automatic sorting is performed by this app; the user selects the lot freely. **FiFo:** The result list is sorted in ascending order by acquisition date; the lot received first (oldest) is at the top and is assigned first. Changing this field requires the **Use Extended Matchcode Search** flag to be activated. |
| Lot Search | When activated, the extended search includes lots as a search result, so that the **Lot Search Result** is populated at all. Without this flag, the search returns no lot lines and this app's FiFo order is moot. |
| Item Search | When activated, the extended search returns items as a search result; in combination with the lot search, this determines which kind of hit the user receives in the line. |
| In Order | When activated, the search additionally includes lots that have not yet been received and are on order (without an acquisition date). With the **FiFo** Split Option active, this app separates the on-order lots from those already received based on the acquisition date, so that the sorting remains unambiguous. |
| Show All | When activated, the search shows all hits without restriction to item or lot search; the flag is mutually exclusive with the lot search and is therefore only relevant when a pure lot search is not desired. |

Additional fields on the **Material Property Setup** page belong to the base scope of the app **m+m Material Properties** and do not control the behavior of this extension; they are therefore not covered here.

### Permissions

The app ships an internal permission set that only grants the processing necessary for the lot ordering. It defines the permissions for this extension's internal processing and specifies which technical actions may be performed in the background; a standalone functional scope assigned to the user is not associated with it. The actual lot and inventory permissions result from the base apps and the Business Central standard.

## Application in Daily Operations

The app takes effect on three existing pages. All fields are display fields about the lot; they are maintained on the **Lot No. Information Card** (from **m+m Additional Lot Information**) and made visible here.

### Material Balances

The **Material Balances** show the inventory per lot. This app supplements the list with origin and vendor details about the respective lot, so that the user can assess the lot without switching to the Lot No. Information Card.

**Entry point:** Open the **Material Balances** from the item or inventory overview.

#### Additional lot columns

| Field | Explanation |
|---|---|
| Vendor Lot No. | Shows the lot number assigned by the vendor. When filled, the user immediately recognizes in inventory under which lot number the vendor tracked the goods, without opening the Lot No. Information Card. |
| Vendor Internal Lot No. | Shows the vendor's internal lot identifier. When filled, the lot can be uniquely assigned to the vendor lot even when the external numbering differs. |
| Acquisition Date | Shows the date of lot receipt. When filled, the user can assess the age of the lot; this date is at the same time the sorting criterion of the FiFo order in the extended search. |
| Purchased From Vendor No. | Shows the vendor number from which the lot was purchased. When filled, the source of the lot is directly evident in inventory. |
| Purchased From Vendor Name | Shows the name of the purchasing vendor for the lot origin. The value is derived from the vendor and serves for quick plain-text assignment without number resolution. |
| Country/Reg. Of Orig. Code | Shows the country or region of origin of the lot. When filled, the user can check origin requirements already in inventory. |
| Manufacturer Code | Shows the manufacturer of the lot as a code. When filled, the manufacturer of the lot is immediately recognizable. |
| Manufacturer Name | Shows the manufacturer name in plain text. This column is hidden by default and can be shown via personalization if needed; it supplements the Manufacturer Code with the readable description. |
| Bundle | Marks the lot as a bundle. When set, the user knows that this is a bundled goods unit, which must be taken into account during withdrawal and picking. |

#### Filter

The **Material Balances** can be restricted by location. The filter belongs to the base page and remains effective even with the additional lot columns.

| Filter field | Explanation |
|---|---|
| Location Code | When set, the inventory lines are filtered by the specified location, so that only lots of this location are shown with their origin details. |

### Lot Search Result

The **Lot Search Result** is the result list of the extended lot search. It is not opened via **Search**; instead, it appears when the user starts the extended search from a sales or purchase line. This app supplements the result list with the same origin columns as in the Material Balances and controls — depending on the Split Option — the order of the hits.

**Entry point:** Start the extended matchcode/lot search from the document line; the **Lot Search Result** opens with the lots found.

**Order.** If the **Split Option** is set to **FiFo**, the app sorts the hits when the page is opened, when the records are built, and before quantity assignment in ascending order by **Acquisition Date**, so that the oldest lot is at the top. If the Split Option is set to **Manual**, the standard order is retained.

#### Additional lot columns

| Field | Explanation |
|---|---|
| Acquisition Date | Shows the acquisition date of the lot. When filled, the user recognizes the lot age immediately in the result list; when FiFo is active, this date determines the sorting. |
| Vendor Lot No. | Shows the vendor lot number for the hit line. When filled, the search proposal can be assigned to a vendor lot. |
| Vendor Internal Lot No. | Shows the vendor's internal lot identifier for the hit line. When filled, the lot is unambiguous even when the external number differs. |
| Manufacturer Code | Shows the manufacturer of the lot as a code, so that the origin can already be taken into account during selection. |
| Manufacturer Name | Shows the manufacturer name in plain text for the hit line. |
| Country/Reg. Of Orig. Code | Shows the country/region of origin of the proposed lot, so that origin requirements can be checked before assignment. |
| Bundle | Marks the proposed lot as a bundle; when set, the packaging unit must be taken into account during selection. |
| Purchased from Vendor No. | Shows the vendor number of the source for the hit line. |
| Purchased From Vendor Name | Shows the name of the purchasing vendor in plain text for the hit line. |

In addition to these extra columns, the Lot Search Result contains the standard fields of the base search, including **Item No.**, **Lot No.**, **Available Quantity**, and the document details **Purchase Order No.** and **Purchase Order Line No.** The additional origin columns of this app are read-only.

### Purchase Order Lots

The **Purchase Order Lots** page presents the lots of a purchase order. This app supplements it with two matchcode columns, so that item and lot can be assigned based on their matchcode.

**Entry point:** Open the **Purchase Order Lots** from the lot or item tracking context of the purchase order.

#### Additional columns

| Field | Explanation |
|---|---|
| Item MatchCode | Shows the matchcode of the item for the lot line. When filled, the user can assign the line based on the item matchcode, without comparing the full item number. The value is derived from the item and is read-only. |
| Lot No. MatchCode | Shows the matchcode of the lot for the line. When filled, the lot can be identified via its matchcode; the value is derived from the lot no. information and is read-only. |

The remaining columns of the page — including **Purchase Order No.**, **Item No.**, item description, **Lot No.**, vendor lot, and **Quantity**, as well as the indicator for the selected line — belong to the base page from **m+m Additional Lot Information**.

## FAQ and Troubleshooting

### 1. Why can't the Split Option be changed?
Changing the **Split Option** requires the **Use Extended Matchcode Search** flag to be activated. As long as this flag is not set, the system rejects the entry in the Split Option field. First activate the extended matchcode search.

### 2. What does the value FiFo do in the Split Option?
When **FiFo** is set, the extended lot search sorts the result list in the **Lot Search Result** in ascending order by **Acquisition Date**. The lot received first (oldest) is at the top and is proposed first. With **Manual**, this automatic sorting does not apply.

### 3. Why aren't the lots sorted despite FiFo?
The sorting only takes effect when the Split Option is actually set to **FiFo** and the extended lot search is active (**Use Extended Matchcode Search** and **Lot Search**). If the Split Option is set to **Manual**, the standard order is retained.

### 4. Why don't I see the Manufacturer Name column in the Material Balances?
The **Manufacturer Name** column is hidden by default in the Material Balances. Show it via the page personalization if needed. The associated **Manufacturer Code** is visible by default.

### 5. Where do the additional lot details come from?
All origin and vendor details (vendor lot, vendor internal lot, acquisition date, purchased vendor, country/region of origin, manufacturer, bundle) are maintained on the **Lot No. Information Card** from **m+m Additional Lot Information**. This app displays them on the pages mentioned but does not change them.

### 6. Can I edit the additional lot columns?
No. The origin columns supplemented by this app in the **Material Balances** and in the **Lot Search Result**, as well as the matchcode columns in the **Purchase Order Lots**, are read-only. Make changes on the Lot No. Information Card.

### 7. What does the Bundle indicator mean?
**Bundle** marks the lot as a bundled goods unit. When the flag is set, the lot is tracked as a bundle; take this into account during withdrawal and picking.

### 8. What are the Item MatchCode and Lot No. MatchCode in the Purchase Order Lots for?
Both columns make assignment easier: the **Item MatchCode** comes from the item, the **Lot No. MatchCode** from the lot no. information. Using the matchcode, items and lots can be identified faster than via the full numbers. Both values are read-only.

### 9. Why do the German field labels differ between the pages?
The same lot detail can carry a slightly different label depending on the underlying page: in the **Lot Search Result** the vendor lot is called **Lieferantencharge** (Vendor Lot No.), while in the material search of the **Material Balances** it is called **Lieferanten-Chargennr.** (Vendor Lot No.). In terms of content, this is the same origin detail about the lot.

### 10. Do I need to consider anything for lots that are on order?
When the **In Order** setting is active, the search also includes lots that have not yet been received, without an acquisition date. When **FiFo** is active, the app separates these from the lots already received based on the acquisition date, so that the order remains unambiguous.

## Typical Use Cases

### Use case 1: Assigning the oldest lot in the sales line

1. **Trigger.** A customer orders goods by phone that are to be delivered according to the "oldest lot first" principle.
2. **Entry point in BC.** The user opens the sales order, enters the line with item and quantity, and starts the extended matchcode/lot search from the line.
3. **Core flow.** The **Lot Search Result** opens. Since the **Split Option** is set to **FiFo**, the lots are sorted in ascending order by **Acquisition Date**; the oldest lot is at the top. The user additionally checks **Vendor Lot No.**, **Manufacturer Code**, and **Country/Reg. Of Orig. Code** directly in the result list and assigns the quantity to the topmost lot.
4. **Completion.** Business Central transfers the assigned lot into the item tracking of the line. This app does not create its own posting step; the further document flow follows the standard.

### Use case 2: Assigning the lots of a purchase order via matchcode

1. **Trigger.** At goods receipt, several lots for a purchase order are present that are to be reconciled based on their matchcode.
2. **Entry point in BC.** The user opens the **Purchase Order Lots** page from the lot or item tracking context of the purchase order.
3. **Core flow.** In the list, each lot line shows the standard details (**Purchase Order No.**, **Item No.**, **Lot No.**, **Quantity**) as well as the columns **Item MatchCode** and **Lot No. MatchCode** supplemented by this app. Using the Lot No. MatchCode, the user assigns the received lot to the correct order line.
4. **Completion.** The assignment takes place within the standard item tracking. This app provides the additional matchcode columns for it; there is no separate posting or completion step.
