---
title: Anwenderhandbuch m+m Supplier Declaration
---

# User Guide m+m Supplier Declaration

## Introduction

The **m+m Supplier Declaration** module manages **supplier declarations** (supplier's declarations of the preferential origin status) in Microsoft Dynamics 365 Business Central. It covers both **single** and **long-term supplier declarations**, each split by **Purchase** and **Sales**, and links them to lots, countries and documents.

**Target audience.** The primary users are **operational clerks in purchasing and sales** as well as in customs/preference processing: they create declarations, confirm countries, release declarations and work with the resulting status information when posting sales shipments and purchase receipts. **Administrators and key users** set up the module (setup, number series, reports, master data) — they are the secondary audience.

**Short process overview.** The typical path through the module:

1. The administrator activates the **supplier declaration functions** and defines number series, reports and the control behaviour during posting (setup).
2. In the master data part, it is defined **for which customers/vendors and which material types/items** a supplier declaration is required, and which **countries/regions** as well as **country/region groups** are relevant for the declaration.
3. The user creates a declaration from one of the four lists, maintains **Country/Region** and **Country/Region Group**, checks validity (**Check countries**) and releases the declaration (**Release**).
4. When posting sales shipments or purchase receipts, the module automatically links lots and documents to the matching declarations and can create and release single declarations.
5. Via the **Lot No. Information Card**, the **Material Balances** and the lot tracing, you can at any time verify whether a supplier declaration exists for a lot.

The typical entry point is: **Search** -> one of the four declaration lists -> select a line -> open the card -> run actions.

## Quick start for users

The fastest way from setup to a released declaration. The order follows the dependency in the code (first setup, then master data, then day-to-day business).

1. **Check setup.** Open the **Supplier Declaration Setup** page via **Search** and activate **Suppl. Decl. Functions active**. Without this flag all module functions are inactive (see Setup).
2. Define **number series and reports** on the same page (one number series per area and type; one report ID per area and type).
3. **Define master data.** On the **Countries/Regions** page, mark the countries relevant for the declaration via **For Supplier Declaration**. If required, maintain **country/region groups** and their **assignments**. Set the **Supplier Declaration required** flag on the **Customer Card** or **Vendor Card** and use **Supplier Declaration for Types** to maintain for which material types/items a declaration is needed.
4. **Create declaration.** Open, for example, **Long-Term Supplier Declarations Purchase** via **Search**, create a line with *New* (Area and Type are set automatically) and select the vendor. Maintain **Valid From/Valid To** and the included items/material types (tab **Supplier Declaration Included**).
5. **Maintain countries.** On the subpages **Supplier Declaration Country/Region** and **Supplier Declaration Country/Region Group**, confirm the promised countries via **Confirmed**. Use **Insert valid countries** to fill in the relevant countries automatically.
6. **Check validity.** Choose **Check countries**. If all confirmed countries/groups lie within the validity period, the **Validity Status** is set to *Checked*.
7. **Release.** Choose **Release**. The status changes to *Released*; the lots are transferred to the Lot No. Supplier Declaration. Use **Reopen** to return to *Open*, use **Cancel** to cancel the declaration.

When posting sales shipments and purchase receipts, the linking runs automatically — depending on the setup (see **Document Integration**).

## Setup

The setup is the most extensive configuration part of the module. It controls whether the module is active, which number series and reports are used, and how the module behaves during posting.

### Set up Supplier Declaration (central setup page)

**Entry point:** Open the **Supplier Declaration Setup** page via **Search**. It is a company-wide setup page (exactly one record per company); it is created automatically on first opening.

**Process.** The administrator configures this page **before first use** of the module. It activates the module, defines the number ranges, assigns the print/send reports and determines the behaviour during posting, which later takes effect in day-to-day business (Document Integration).

**General tab**

| Setup | Explanation |
|---|---|
| **Suppl. Decl. Functions active** | When activated, all functions of the module are effective: creating and releasing declarations, checks during posting and setting the status fields in document lines. If the flag is not set, all module routines exit immediately, so day-to-day business runs in the standard way without supplier declaration. |
| **Event Publisher activated** | When activated, the module additionally reacts to the insertion/modification of item ledger entries and to the validation of sales/purchase lines: when the origin is moved to a new lot (via the additional lot information), the supplier declaration is transferred to the new lot, and when a document line is entered, **Supplier Declaration required** is determined automatically. Without this flag these automatic determinations do not occur. |

**Supplier Declaration tab**

| Setup | Explanation |
|---|---|
| **Insert Default Country/Region Codes** | When activated, all countries marked as **For Supplier Declaration** are pre-filled automatically as Country/Region lines when a declaration is created; the user then only needs to confirm them instead of entering them one by one. |
| **Insert all Countty/Region Groups** | When activated, all existing country/region groups are additionally pre-filled as group lines when a declaration is created; without the flag the user maintains the groups manually. |
| **Delete Not Relevant Country/Region Codes** | When activated, the module removes all unconfirmed Country/Region lines from the declaration on release; the released declaration then contains only the countries that were actually promised. Without the flag, unconfirmed lines are also retained. |

**Sales tab**

| Setup | Explanation |
|---|---|
| **Create Suppl. Decl. on Sales Ship. Post.** | When activated, the module automatically creates a single supplier declaration including country, document and lots when posting a sales shipment for lines that require a declaration and for which none yet exists. Without the flag, no new declaration is created during posting. |
| **Release Suppl. Decl. on Sales Ship. Post.** | When activated, the single declaration just created automatically is released immediately after posting (status *Released*). Without the flag it remains in status *Open* for manual review. Takes effect only together with *Create Suppl. Decl. on Sales Ship. Post.*. |
| **Check for Missing Suppl. Decl. on Sales Inv. Posting** | Controls the posting block for the sales invoice. **(empty):** no check. **Warning:** if a line requires a declaration when posting a sales invoice but the associated shipment does not have one, a notice appears and posting continues. **Error:** in the same situation, posting is cancelled with an error message until a declaration exists. |
| **Print/Send Sales Suppl. Decl. With** | Controls the check when printing/sending a sales supplier declaration. **(empty):** no check. **Warning:** missing prerequisites are reported as a notice. **Error:** the operation is cancelled if prerequisites are missing. |

> Note: The **Purchase** tab does not contain its own fields in this version; the purchase-side control is handled via the number series, report and General settings.

**No. Series tab**

| Setup | Explanation |
|---|---|
| **Purch. Supplier Declaration Nos.** | When set, the module assigns the number from this series when creating a **single** purchase declaration. If the series is set to manual numbers, the user can also enter the number themselves; otherwise each new declaration automatically receives the next available number. |
| **Purch. Long-Term Supplier Declaration Nos.** | When set, this series provides the numbers for **long-term** purchase declarations. |
| **Sales Supplier Declaration Nos.** | When set, this series provides the numbers for **single sales** declarations. |
| **Sales Long-Term Supplier Declaration Nos.** | When set, this series provides the numbers for **long-term sales** declarations. |

Without the respective matching number series, creating a declaration is cancelled with a test field message — maintaining all four series is therefore a prerequisite for day-to-day business.

**Reports tab**

| Setup | Explanation |
|---|---|
| **Sales Supplier Declaration Report-ID** (Purchase) | When set, the print/send action for single purchase declarations uses this report. Without an entry, no printout is available. |
| **Purch. Long-Term Supplier Declaration Report-ID** | When set, this report is printed/sent for long-term purchase declarations. |
| **Sales Supplier Declaration Report-ID** (Sales) | When set, this report is used for single sales declarations (action **Print** on the declaration). |
| **Sales Long-Term Supplier Declaration Report-ID** (Sales) | When set, this report is used for long-term sales declarations. |

The report IDs reference report objects; maintaining them assigns the matching print form to the respective area/type. The actual report layouts are provided outside this module.

> A further control field of the setup table, **Missing Pre Mat. Suppl. Decl. in Mat. Selection** (option values **(empty)**, **Warning**, **Error**), controls the message for a missing material prerequisite in the material selection: **(empty)** = no check, **Warning** = notice, **Error** = cancellation. It is not shown on the standard setup page and is only relevant for special cases of the material selection.

### Set up permissions

The permission set **MuM SDMuM All** (caption **All permissions**) bundles the table and object rights of the module. Assign it to the users who are allowed to work with supplier declarations. The permission set determines the permissions for all module tables and pages and defines which actions the users can perform in the module; without an assignment, the module pages are not operable for the user.

### Set up Supplier Declaration during posting (process chain)

This setup chain connects the global setup, master data and the operational action during posting. It is configured by the administrator before the first shipment and takes effect in day-to-day business during posting (cross-reference: **Document Integration**).

1. **First,** on the **Supplier Declaration Setup** page, set the **Suppl. Decl. Functions active** flag. When activated, the posting checks become effective at all.
2. **Then** set **Event Publisher activated** so that the **Supplier Declaration required** field is determined automatically when document lines are entered.
3. **Next,** in the master data, define for which customers/vendors (**Supplier Declaration required**) and which material types/items (**Supplier Declaration for Types**) a declaration is needed (see Master data).
4. **Then** choose the sales behaviour: **Create Suppl. Decl. on Sales Ship. Post.** and optionally **... release**; additionally set **Check for Missing Suppl. Decl. on Sales Inv. Posting** to **Warning** or **Error**.
5. **In the daily routine,** the user posts the sales shipment/purchase receipt; the module links documents and lots, creates or releases single declarations and checks the sales invoice according to the chosen level.

## Master data

The master data defines **when** a supplier declaration is required and **which countries** qualify as origin.

### Mark Countries/Regions for the supplier declaration

**Entry point:** Open the standard **Countries/Regions** page via **Search**. The module adds four fields to the list.

**Process.** The key user marks, before the first declaration, which countries are relevant as origin. This marking controls which countries are pre-filled automatically when a declaration is created via **Insert Default Country/Region Codes** (cross-reference: Setup) and can be confirmed as a Country/Region line in the declaration.

| Field | Explanation |
|---|---|
| **For Supplier Declaration** | When activated, this country/region is considered declaration-relevant: it is taken over into new declarations as a Country/Region line and can be confirmed there. Without the flag, the country does not appear in the automatic pre-fill. |
| **Free Text** | When filled, an explanatory text is available for this country, which can be taken over into the declaration line. |
| **Valid From** | When set, the declaration relevance of the country only applies from this date. |
| **Valid To** | When set, the declaration relevance of the country ends with this date. |

### Set up Supplier Declaration for Types per customer/vendor

**Entry point (Sales):** In the **Customer Card**, open the action **Supplier Declaration for Types**; alternatively, in the **Customer List**, the action **Supplier Declaration Material Types**. **Entry point (Purchase):** In the **Vendor Card**, open the action **Supplier Declaration for Types**. The page is additionally reachable via **Search** as the list **Contact Supplier Declaration for Types**.

**Process.** The key user maintains, per customer/vendor, for which material type, which item/variant or which tariff number a supplier declaration is required. First set the **Supplier Declaration required** field on the customer/vendor card (open the detail page via the lookup of the same field). The entries are evaluated when a document line is entered: if the line matches an entry, **Supplier Declaration required** is set in the document line (cross-reference: Document Integration).

| Field | Explanation |
|---|---|
| **Vendor No./Customer No.** | Assigns the entry to the business partner for which the declaration is required. |
| **Type** | Determines the reference point of the rule. **Material Type:** the material type of the item counts; the **Material Type** field becomes editable. **Item/Variant:** the specific item and, if applicable, the variant count; the fields **Item No.** and **Variant Code** become editable. **Tariff No.:** the tariff number of the item counts. |
| **Material Type** | If Type = Material Type: the material type for which a declaration is required. Editable only for this type. |
| **Item No.** | If Type = Item/Variant: the item for which a declaration is required. Editable only for this type. |
| **Variant Code** | If Type = Item/Variant: the variant of the item. Editable only for this type. |
| **Tariff No.** | If Type = Tariff No.: the tariff number for which a declaration is required. |
| **Description** | Designation of the material type/item for orientation. |
| **Description 2** | Additional designation for orientation. |

The associated fields on the customer/vendor:

| Field | Explanation |
|---|---|
| **Supplier Declaration required** (Customer/Vendor Card) | When activated, the module evaluates the entries under *Supplier Declaration for Types* for this business partner. If not set, no declaration obligation is determined for its document lines. |
| **No. of Single Supplier Declarations** / **No. of Long-Term Supplier Declarations** | Show, per business partner, how many single or long-term declarations exist; serve as a quick overview in the card and FactBox. |

### Set up country/region groups and assignments

**Entry point:** The **Country/Region Group** and its **assignments** are maintained from within the declaration or via the associated lists; the group is also available in the declaration subpages as type **Country/Region Group**.

**Process.** Several countries that are promised together (for example a cumulation zone) are combined into a group. In the declaration, the group can then be confirmed instead of many individual countries; during the validity check the module verifies that all countries of the group lie within the validity period.

**Country/Region Group**

| Field | Explanation |
|---|---|
| **Code** | Unique identifier of the group. |
| **Name** | Designation of the group. |
| **Valid From** / **Valid To** | When set, the group is valid only in this period; outside it, it is reported as invalid during the validity check. |
| **Countries/Regions** | Shows the number or the assigned countries of the group. |

**Country/Region Assignment** (which countries belong to the group)

| Field | Explanation |
|---|---|
| **Country/Region Code** | A country/region assigned to the group. |
| **Name** | Designation of the country. |
| **Free Text** | Explanatory text for the assignment. |
| **Valid From** / **Valid To** | When set, the assignment of the country to the group is valid only in this period. If an assignment is outside the declaration period, the validity check fails. |

### Approvals

The master data list **Approval** manages approval codes (**Code**, **Description**) that can be assigned to a declaration via the **Approval-Code** field; the **Approval Description** is then looked up. It serves the internal marking of released or approved declarations.

## Daily work: create and release a supplier declaration

The declaration is the central document of the module. There are four entry lists that differ only in **Area** (Purchase/Sales) and **Type** (single/long-term); the underlying card is structured identically.

### Entry point and lists

**Entry point:** Open one of the four lists via **Search**:

- **Single Supplier Declarations Purchase**
- **Long-Term Supplier Declarations Purchase**
- **Single Supplier Declarations Sales** (single, sales)
- **Long-Term Supplier Declarations Sales**

Each list is pre-filtered to its area and type; when a new line is created, **Area** and **Type** are pre-filled automatically. The list is not editable; selecting a line opens the associated card.

Columns of the list (excerpt, identical table model as the card): **No.**, **Area**, **Type**, **Customer/Vendor No.**, **Customer/Vendor Name**, **Cust./Vend. Country/Reg. Code**, **Status**, **Valid From/Valid To** (long-term only), **Cumulative**, **Cancellation Date**, **Incomplete**, **Created by/at**, **Modified by/at**, **Cumulative Countries/Regions**.

### Header data of the Supplier Declaration Card

**Entry point:** Select a line in the list; the **Supplier Declaration Card** opens. On creation, the number is assigned from the matching number series.

| Field | Explanation |
|---|---|
| **No.** | Unique number of the declaration from the number series. Renaming is not allowed. |
| **Area** | **Purchase** or **Sales**. As long as no customer/vendor is set, the area can be chosen; after that it is fixed. Controls whether the declaration runs against vendors or customers. |
| **Type** | **Single Supplier Declaration** or **Long-term Supplier Declaration**. On switching, already entered countries are deleted and the validity status is reset to *Check necessary*, because the check logic differs. |
| **Customer/Vendor No.** | Business partner of the declaration. On entry, the module checks that the partner is not blocked and that its country is an EU member; otherwise the entry is cancelled. Name, address, post code, city and country/region code are taken over automatically. |
| **Customer/Vendor Name**, **Name 2**, **Address**, **Address 2**, **Post Code**, **City** | Address of the business partner; pre-filled from the master record, can be overwritten if required. |
| **Cust./Vend. Country/Reg. Code** | Country/region of the business partner. On change, the EU membership is checked again; a non-EU country is rejected. |
| **Status** | Life cycle of the declaration (not directly editable). **Open:** in progress; changes allowed. **Released:** released; the lots are transferred, changes to the header are blocked. **Cancelled:** cancelled; the assigned lot declarations were removed and the cancellation date set. |
| **First Release Date** | Date of the first release (automatically on the first **Release**). |
| **Actual Release Date** | Date of a renewed release after reopening. |
| **Valid From** / **Valid To** | Validity period (especially for long-term declarations). On entry, it is checked that *from* is not after *to*; every change resets the validity status to *Check necessary*. |
| **Validity Status** | Result of the country check (not editable). **Check necessary:** check is pending; a release is not possible. **Checked:** all confirmed countries/groups lie within the validity period. **Checked+Changed:** previously checked, then changed. **Manual checked:** set manually as checked by the user. **Check again:** a previously checked declaration was changed and must be checked again. |
| **Incomplete** | When set, the module marks the declaration as not yet complete (not editable). |
| **Cumulative** | When activated, cumulative countries/regions are additionally taken into account; the flag is set automatically as soon as cumulative countries are entered. Without cumulative countries, a release with *Cumulative* activated is not possible. |
| **Cumulative Countries/Regions** | Number of cumulative countries; the lookup opens the maintenance page **Supplier Declaration Cumulative Country/Region**. |
| **Cancellation Date** | Date of the cancellation (for status *Cancelled*). |
| **Created by/at**, **Modified by/at** | Log fields; maintained automatically. |
| **Approval-Code** / **Approval Description** | Optional approval reference from the master data list **Approval**. |

> Note on distinguishing the cards: The **Supplier Declaration Card** (long-term) additionally shows the tabs **Supplier Declaration Included** and **Supplier Declaration Exceptions** as well as the validity status. The **single** sales/purchase pages do not show these tabs, but do show the same header and country areas.

### Worksheet areas of the declaration

The card combines several subpages. Each area maintains a part of the declaration.

#### Supplier Declaration Country/Region

Maintains the individual promised countries.

| Field | Explanation |
|---|---|
| **Code** | Country/region that is promised in the declaration. On entry, it is checked whether the country lies within the valid range. |
| **Name** | Designation of the country. |
| **Free Text** | Explanatory text for the country line. |
| **Confirmed** | When activated, the country is considered promised and is taken over into the released declaration. If the country belongs to a group, the module asks whether the entire group should be confirmed. A country that is contained in a group cannot be set to "unconfirmed" individually. |
| **In Country/Region Group** | Shows whether the country is part of a group. |
| **Country/Region Group** | Group to which the country is assigned. |
| **Valid From** / **Valid To** | Optional validity period of the country line; must lie within the declaration period, otherwise the check reports the country as invalid. |

#### Supplier Declaration Country/Region Group

Maintains the groups confirmed in the declaration.

| Field | Explanation |
|---|---|
| **Code** | Confirmed country/region group. |
| **Name** | Designation of the group. |
| **Confirmed** | When activated, the associated countries of the group are also kept as confirmed for long-term declarations; the module verifies that the period is set and valid. |
| **Valid From** / **Valid To** | Optional validity period of the group line. |

#### Supplier Declaration Included (long-term only)

Defines **which** items/material types/tariff numbers are covered by the long-term declaration. During posting, this list is used to check whether a document line is covered by an existing long-term declaration (cross-reference: Document Integration).

| Field | Explanation |
|---|---|
| **Type** | **Item**, **Material Type** or **Tariff No.**. Depending on the selection, the associated fields become editable; on switching, the remaining fields are cleared. |
| **Tariff No.** | If Type = Tariff No.: the covered tariff number. |
| **Item No.** / **Variant Code** | If Type = Item: the covered item and, if applicable, the variant. |
| **Matchcode** | Search aid for quick item determination. |
| **Material Type Code** | If Type = Material Type: the covered material type. |
| **Description** / **Description 2** / **Cross-Reference No.** | Descriptive fields; derived from the item (not editable). |

#### Supplier Declaration Exceptions (long-term only)

Defines exceptions that, despite a match in "included", are **not** covered by the long-term declaration (in which case a single declaration is required).

| Field | Explanation |
|---|---|
| **Type** | **Material Type**, **Item**, **Item Variant** or **Characteristic**. The respective matching fields become editable. |
| **Material Type Code** | If Type = Material Type: excepted material type. |
| **Item No.** / **Variant Code** | If Type = Item/Item Variant: excepted item or variant. |
| **Matchcode** | Search aid. |
| **Characteristic No.** / **Characteristic Value Filter** / **Characteristic Description** | If Type = Characteristic: exception based on a material characteristic and its value filter. |
| **Description** / **Description 2** / **Cross-Reference No.** | Descriptive fields. |

#### Assigned documents

Shows and maintains the documents linked to the declaration.

| Field | Explanation |
|---|---|
| **Document Type** | **(empty)**, **Purch. Order**, **Purch. Receipt**, **Purch. Invoice**, **Sales Order**, **Sales Shipment** or **Sales Invoice**. Determines from which document type the assignment originates; on selection, the customer/vendor no. is looked up. |
| **Document No.** | Number of the assigned document. |
| **Document Line No.** | Line number of the assigned document. |

> A subsequent change of assigned documents is blocked; if required, delete the line and insert a new one.

#### FactBoxes of the card

- **Suppl. Decl. Lot No.** (FactBox): shows the lots belonging to the declaration, per lot.
- **DropZone** (FactBox): attachments to the declaration by drag-and-drop (via the m+m DropZone module; **Supplier Declaration** is registered as the source).

### Actions of the declaration (release and validity flow)

The following steps reflect the checked flow. They appear — depending on the card — in the groups **Release** and **Further Actions**.

1. **Insert valid countries** — fills the Country/Region lines (and, for long-term declarations, the groups) automatically from the countries marked as declaration-relevant. If countries are already entered, a confirmation is requested before the rebuild.
2. **Cumulation Country/Region** — opens **Supplier Declaration Cumulative Country/Region** to maintain cumulative countries; then sets the **Cumulative** flag if cumulative countries exist.
3. **Update Countries with Cumulation** — updates the countries of all lots of the declaration based on the lot origin and the groups.
4. **Check countries** — checks whether all confirmed countries, groups and group countries lie within the validity period. Success: **Validity Status** = *Checked*. Otherwise, a previously checked status is set to *Check again*. Without an entered period, a notice appears that no check was performed.
5. **Set manual Validity** / **Reset Validity** — sets the validity status manually to *Manual checked* or resets it to *Check necessary*.
6. **Release** — releases the declaration: if the validity status is still *Check necessary*, the release is refused with a notice. Otherwise, non-relevant countries are removed, the mandatory check is run, the release date is set, an entry is written per lot in **Lot No. Supplier Declaration**, and the **Status** is set to *Released*.
7. **Reopen** — resets a released declaration to *Open* and removes the lot declaration entries.
8. **Cancel** — cancels the declaration (status *Cancelled*), removes the lot declaration entries and sets the cancellation date.
9. **Add Document** / **Add Sales Shipment** / **Add Purchase Receipt** — assigns posted sales shipment or purchase receipt lines to the declaration (selection via **Posted Sales Shipment Lines** or **Posted Purchase Receipt Lines**) and takes over the associated lots.
10. **Print** — prints/sends the declaration via the report defined in the setup.

## 8D report and email

This module contains no 8D report and no module-specific email function. The only output channel is the configurable **report** for the supplier declaration (action **Print**), whose report ID is defined per area/type in the setup. Printing/sending can be safeguarded via **Print/Send Sales Suppl. Decl. With** (Warning/Error). The module does not keep its own send logging.

## Document Integration (sales and purchase documents)

The module extends the standard documents with status fields and intervenes during release and posting. Prerequisites are the setup (**Suppl. Decl. Functions active**, **Event Publisher activated**) and the master data (**Supplier Declaration required**, **Supplier Declaration for Types**) — see **Setup** and **Master data**.

### Additional fields in the document lines

The fields appear in the lines of **Sales Order** and **Purchase Order** (as well as in quote, blanket and posted document subpages in the same form):

| Field | Explanation |
|---|---|
| **Supplier Declaration required** | When set, the line requires a supplier declaration. The module determines the flag when **Item No.** or **Variant Code** is entered, from the business partner (**Supplier Declaration required**) and the **Supplier Declaration for Types** entries. |
| **Sales Suppl. Decl. Status** / **Purch. Suppl. Decl. Status** (document status) | Determined on release of the document: **(empty):** not yet determined. **Long-term Supplier Declaration exists:** a valid, released long-term declaration covers the line. **Single Supplier Declaration needed:** no long-term declaration covers the line; a single one is needed. |
| **Purchase Suppl. Decl. Status** (inventory reference, sales line, not editable) | Result of the inventory check of the existing lots: **(empty):** not determined. **Single Supplier Declaration possible:** all open lots have a purchase declaration. **Single Supplier Declaration not possible:** no lot has a declaration. (Intermediate level "restricted possible": only part of the lots has a declaration.) The status is highlighted in colour (favourable/ambiguous/unfavourable). |

### Status on release of the document

When a **Sales Order** or a **Purchase Order** is released, the module checks, per declaration-required line, whether a valid, released long-term declaration includes the item/variant (via **Supplier Declaration Included**) and no **exception** applies. The result is the document status described above. Additionally, for sales lines, it is checked against the open item ledger entries whether the existing lots have a purchase declaration.

### During posting

1. **Post sales shipment.** For declaration-required shipment lines without an existing declaration, a single sales declaration including country, assigned document and lots is created — if **Create Suppl. Decl. on Sales Ship. Post.** is active; if **Release Suppl. Decl. on Sales Ship. Post.** is active, it is released immediately. If a long-term declaration covers the line, only the document is assigned instead.
2. **Post purchase receipt.** For declaration-required order lines, the posted purchase receipt is assigned to a matching, valid, released long-term purchase declaration and the lots are transferred.
3. **Post sales invoice.** If **Check for Missing Suppl. Decl. on Sales Inv. Posting** is set to **Warning** or **Error** and the declaration of the associated shipment is missing for a declaration-required line, a notice appears or posting is cancelled.

### Follow-up document lines: create single declaration

In the **Posted Sales Shipment Lines** and **Posted Purchase Receipt Lines**, the action **Create Single Supplier Declaration** is available. With it, the user subsequently creates a single supplier declaration from a posted line if none was created during posting.

## Lot tracing, history and evidence

Whether a lot has a supplier declaration can be verified in several places.

### Lot No. Information Card

The module adds two fields to the **Lot No. Information Card**:

| Field | Explanation |
|---|---|
| **Purchase Supplier Declaration Exists** (Purchase) | When set, a purchase supplier declaration exists for this lot. Via lookup, the module opens the associated declaration (with exactly one hit the **Supplier Declaration Card**, otherwise the lot tracing). |
| **Purchase Supplier Declaration Exists** (Sales) | When set, a sales supplier declaration exists for this lot; lookup as above for the sales area. |

### Material Balances

In the **Material Balances** (m+m Material Properties), the module adds the field **Purchase Supplier Declaration Exists** per lot line. When set, the lot has a purchase declaration; via lookup the user goes directly to the declaration or to the lot tracing.

### Lot tracing of the supplier declaration

The tracing page (called, among others, via the lookups of the lot fields) shows the origin/usage chain of the lots with reference to the supplier declaration.

**Filters**

| Filter field | Explanation |
|---|---|
| **Item Filter** | When set, the tracing lines are restricted to this item. An item filter is required for the tracing. |
| **Variant Filter** | When set, restriction to a variant. |
| **Lot No. Filter** | When set, restriction to a lot. |
| **Serial No. Filter** | When set, restriction to a serial number. |
| **Trace Method** | Determines the direction of the tracing. **Origin -> Usage:** from the source to the usage. **Usage -> Origin:** from the usage to the source. |
| **Show Components** | **No:** no components. **Item-tracked Only:** only lot-/serial-tracked components. **All:** all components. |

Actions of the tracing: **Trace** (run tracing), **Set Filters with Line Values**, **Trace Opposite - from Line**, **Next/Previous Trace Result**, **Show Document**, **Item/Card/Ledger Entries**, **Print** as well as the jump to the history **Go to Already-Traced History**.

### Lot Supplier Declaration

On release, entries are created in **Lot No. Supplier Declaration** per lot (fields include **Lot No.**, **Item No.**, **Variant Code**, **Area**, **Type**, **Supplier Declaration No.**, **Vendor Lot No.**). This table is the evidence basis for which lot was promised in which declaration; manual changes are blocked here and must be made in the declaration.

## FAQ and troubleshooting

### Why can I not release a declaration even though countries are confirmed?
If the **Validity Status** is still *Check necessary*, **Release** refuses the operation with a notice. First run **Check countries** (or **Set manual Validity**) so that the status changes to *Checked* or *Manual checked*.

### Why does the system report that the country is not an EU member?
When setting **Customer/Vendor No.** or **Cust./Vend. Country/Reg. Code**, the module checks the EU membership of the country. If the EU country code is not maintained on the country/region, the insertion is cancelled. Maintain the EU country code on the country or choose an EU business partner.

### Why are my entries in the declaration not saved?
Changes are only allowed in **Status** *Open*. A released or cancelled declaration is blocked against changes. First reset it via **Reopen**.

### Why does a document line require a supplier declaration?
The **Supplier Declaration required** field is set when **Supplier Declaration required** is active on the business partner and the line matches an entry under **Supplier Declaration for Types** (by item/variant, material type or tariff number). Additionally, **Event Publisher activated** in the setup is a prerequisite.

### What does the document status "Single Supplier Declaration needed" mean?
There is no valid, released **long-term** declaration that covers the item/variant via **Supplier Declaration Included** (or an **exception** applies). For this line, a **single** declaration must be created.

### What happens automatically when posting a sales shipment?
For declaration-required lines without coverage, the module creates — if **Create Suppl. Decl. on Sales Ship. Post.** is active — a single declaration with country, assigned document and lots and releases it immediately if **Release Suppl. Decl. on Sales Ship. Post.** is active. Otherwise, only the document is assigned to an existing long-term declaration.

### Why is my sales invoice rejected during posting?
If **Check for Missing Suppl. Decl. on Sales Inv. Posting** is set to **Error** and the underlying sales shipment does not have a declaration for a declaration-required line, posting is cancelled. Create the missing declaration or set the check to **Warning**.

### Why can I not release "Cumulative"?
If **Cumulative** is set but no cumulative countries were assigned, the release is not possible. Maintain the cumulative countries via **Cumulation Country/Region** or deactivate **Cumulative**.

### Why does the question about the whole group appear when confirming a country?
If the confirmed country belongs to a group, the module asks whether the entire group should be confirmed. If you confirm, all countries of the group are kept as confirmed; an individual country of a group cannot be set to "unconfirmed" separately.

### How do I find out whether a lot already has a supplier declaration?
Open the **Lot No. Information Card** or the **Material Balances** and check the **Purchase Supplier Declaration Exists** field. Via lookup you go to the declaration or to the lot tracing.

## Typical use cases

### Record a long-term supplier declaration of a supplier
**Trigger:** A supplier sends a long-term supplier declaration for several items by email.
**Entry point in BC:** Via **Search** -> **Long-Term Supplier Declarations Purchase** -> *New* (Area Purchase, Type long-term are pre-filled) -> card.
**Core flow:** Select the vendor (address is taken over, EU check runs). Enter **Valid From/Valid To**. In the tab **Supplier Declaration Included**, enter the covered items/material types/tariff numbers, and maintain exceptions if required. Use **Insert valid countries** to pre-fill the countries and promise them in **Supplier Declaration Country/Region** via **Confirmed**; confirm groups if applicable. **Check countries** -> Validity Status *Checked*. **Release** -> Status *Released*.
**Conclusion:** Optionally **Print** for the evidence; the declaration will cover matching purchase and sales lines going forward.

### Single sales supplier declaration for a shipment
**Trigger:** A customer requests a supplier declaration for an already posted shipment.
**Entry point in BC:** Via **Search** -> **Single Supplier Declarations Sales** -> *New* -> card (Area Sales, Type single pre-filled).
**Core flow:** Select the customer. Via **Add Document**, assign the relevant lines from **Posted Sales Shipment Lines** (the module takes over the lots). Confirm Country/Region, **Release**.
**Conclusion:** **Print** for the customer evidence. Alternatively, this declaration is already created **automatically during posting** of the sales shipment with an active setup and is released immediately if applicable.

### Posting check in day-to-day business
**Trigger:** A clerk posts a sales invoice for a shipment with declaration-required items.
**Entry point in BC:** Standard sales invoice; no separate module page needed.
**Core flow:** During posting, the module checks, according to **Check for Missing Suppl. Decl. on Sales Inv. Posting**, whether the shipment of the declaration-required lines has a declaration. With **Warning**, a notice appears and posting continues; with **Error** it is cancelled.
**Conclusion:** If a declaration is missing, the user creates it via **Create Single Supplier Declaration** in the posted shipment lines and posts again.
