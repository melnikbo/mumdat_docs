---
title: Anwenderhandbuch m+m Digital Metal Code
---

# m+m Digital Metal Code User Manual

## Introduction

The **m+m Digital Metal Code** module (DMC for short) connects Microsoft Dynamics 365 Business Central with an external DMC web service and translates the material classification of the metal trade into usable codes. From the **record properties** of a record maintained in Business Central (material type, item, item variant, lot), the module generates a **DMC Code** (the full code) and an **IDMC Code** (the compact short code), and stores the matching **barcodes** (Code 39 and QR Code) as images for each IDMC.

Conversely, in document lines it is enough to enter an **IDMC Code** for the module to find the matching item, item variant, or lot and fill the line automatically. This way your users work with a single scanned or typed code instead of item numbers.

**Target audience:** The primary audience is the **operational users in day-to-day business** — the people in sales and purchasing who capture document lines and type or scan an IDMC Code, as well as the people in goods receipt and lot management who enrich lots with properties. The secondary audience is **administrators and key users** who configure the module in the Material Property Setup, on the material types, and on the properties.

**Brief process overview:**

1. An administrator activates the DMC connection in the **Material Property Setup** and enters credentials, prefix, and separator.
2. A key user connects each **material type** with a **DMC class** and assigns the DMC identifiers to the **properties** and **property values**.
3. Through the matching actions, **items**, **item variants**, and **lots** receive their IDMC/DMC Code.
4. In day-to-day business, users enter an IDMC Code in **sales** and **purchase lines**; the line is resolved automatically.
5. **Barcodes** are available for every IDMC.

The module requires the base module **Material Properties** (m+m Material Properties). Material type, property, property value, and record property come from this base module; DMC extends these pages with its own fields and actions. Fields that belong exclusively to the base module are described in its own manual; the complete DMC part is documented here.

## Quick Start for Users

The quick start describes the shortest path to a result. The order follows the technical dependency: **first setup, then master data, then daily work**.

### A. One-time setup (administrator)

1. Open the **Material Property Setup** and switch to the **DMC** tab.
2. Enable **DMC Active** and enter **DMC Url**, **DMC User**, and **DMC Password**.
3. Check **DMC Prefix** and **DMC Value Seperator** (defaults `DMC` and `$`).
4. In the **DMC** action group, choose the action **Test Connection**.
5. On the **Matching** tab, enable the flags **DMC Matching** and, as needed, **DMC Item Matching**, **DMC Item Variant Matching**, and **DMC Lot Matching**.

### B. Prepare master data (key user)

6. Open the **Material Type Card** of the material type and, on the **DMC** tab, use **Show DMC Classes** to select the appropriate DMC class; **DMC Class ID** and **DMC Class Identifier** are set.
7. Choose **Suggest DMC Property Matching** and then **Map Missing Mandatory DMC Properties** so that all required properties receive a **DMC Property ID**.

### C. Generate codes (key user)

8. On the **Material Type Card**, choose the action **Match DMC to Item** (and, if needed, **Match DMC to Item Variant**, **Match DMC to Lot No.**). The records receive an **IDMC Code** and a **DMC Code**.

### D. Daily work (sales/purchasing)

9. In the **sales order**, create a new line and enter the scanned or received code in the **IDMC Code** field.
10. Confirm the displayed prompts (e.g. search with mandatory properties only, inventory prompt). The line is filled with the matching **item** or **item variant** and the IDMC Code.

> ☞ The module contains no posting or release run of its own. The actual document posting is performed unchanged through the standard posting actions of Business Central. DMC only acts up to the point of filling the line.

## Setup

Setup is the most extensive configuration part. It covers the central DMC connection, the license quota, the matching options, the user notification, as well as two independent configuration chains (dummy properties and optional group search).

### DMC connection and options (Material Property Setup, DMC tab)

**Who/when:** An administrator configures this page **once per company**, before material types, items, and lots are first assigned DMC codes. It is a company-wide setup page (one record per company). **Entry point:** Open the **Material Property Setup** via **Search** (company-wide setup without a parent list) and switch to the **DMC** tab. The values set here control all DMC functions of the material type, item, and lot pages (cross-reference: sections **Master Data** and **Daily Work**).

Fields on the **DMC** tab:

| Setup | Explanation |
|---|---|
| **DMC Active** | When enabled, the DMC web service and all DMC actions of the **DMC** action group are unlocked; if the flag is not set, the connection and code generation remain blocked and the actions cannot be executed. |
| **DMC Url** | When set, the module directs all web service calls (classes, properties, barcodes, IDMC) to this address; without a valid Url, **Test Connection** fails. |
| **DMC User** | When set, the module logs on to the DMC web service with this user; without a user no connection is established. |
| **DMC Password** | When set, this (masked) password is used for logon; it complements the DMC User and is a prerequisite for retrieving classes and codes. |
| **DMC Prefix** | When set (default `DMC`), every generated DMC Code starts with this prefix; when decoding an entered code, the module checks for exactly this prefix — if it does not match, the entry is considered not a valid IDMC. |
| **DMC Value Seperator** | When set (default `$`), this character separates class, property IDs, and values in the DMC Code; without a valid separator, codes can neither be generated nor decoded. |
| **DMC Review Sign** | When set (default `!`), the module appends this character to codes that require review; when reading them in, the module recognizes the character, removes it, and reports "The DMC needs to be reviewed!" — this way codes to be reviewed become visible in the document. If the field is empty, no review flagging takes place. |

Fields of the **DMC License** subgroup:

| Setup | Explanation |
|---|---|
| **DMC Bought Value** | When set, this value defines the purchased quota of DMC retrievals; as this quota is approached, the module warns, and once it is reached it refuses further retrievals with a note to purchase a new license. |
| **DMC Warning Value** | When set, a continue prompt appears before the next retrieval starting from this remaining value; this way users notice a dwindling quota in good time. |
| **DMC Consumption Value** | Shows the quantity of retrievals already consumed; the field is not editable and serves to monitor consumption. |
| **DMC Remaining Value** | Shows the remaining quantity of retrievals; the field is not editable and is derived from the bought minus the consumed value. |

Fields of the **Matching** subgroup:

| Setup | Explanation |
|---|---|
| **DMC Matching** | When enabled, the module determines the matching IDMC/DMC Code from the record properties (the actual matching); if it is not set, all matching actions and the automatic code determination remain ineffective. |
| **DMC Item Matching** | When enabled, an IDMC/DMC is determined for items (when unblocking the item and via **Match DMC to Item**); without this flag, items remain without an automatic code. |
| **DMC Item Variant Matching** | When enabled, matching is also performed for item variants; this flag can only be operated when the item variant feature of the base module is active. Without the flag, variants receive no code. |
| **DMC Lot Matching** | When enabled, an IDMC/DMC is determined for lots (lot no. information); without the flag, lots remain without an automatic code. |
| **DMC Background Matching** | When enabled, the matching runs as a background task instead of in the foreground; the module then requires at least one user with **Notify DMC Warnings** in the User Setup — otherwise enabling it is prevented with an error message. This keeps data entry fluid and ensures that warnings reach the responsible persons by e-mail. |

> ☞ **Search just with required Properties (Background-Matching)** is a further matching flag of the setup table: when enabled, the background matching, in the absence of a full match, continues to search with only the required (mandatory) properties; without the flag, the background matching aborts when there is no full match, without adopting a partial match.

Actions of the **DMC** action group (Actions tab / ribbon):

| Action | Explanation |
|---|---|
| **Test Connection** | Checks the stored credentials against the DMC web service; the action is also available as a promoted action and should be run after every change to the connection data. |
| **Show DMC Classes** | Retrieves the classes from the web service and displays them in the **DMC Buffer** for viewing; provides an overview of the available classes. |
| **Init Material Types from DMC Classes** | Creates material types from the DMC classes; the action is hidden by default and intended for the initial setup of large class inventories. |
| **Get IDMC from Hash** | Opens an input dialog for a hash value and determines the IDMC and DMC from it for verification; available only when matching is active. |
| **Suggest for all Materials** | Suggests the property matching for all material types; available only when matching is active. |
| **Suggest for all Property Values** | Suggests the value assignment (Value ID) for all properties; available only when matching is active. |
| **Suggest for Material Type and Property in Background** | Schedules the combined suggestion run as a background task (job queue); available only when matching is active. |
| **Init IDMC Matching** | Starts the IDMC determination; via a selection dialog you choose **Run directly** or **Run in background**. Available only when matching is active. |
| **Sync DMC Fields to Record Properties** | Transfers the DMC Property ID and DMC Category from the material type assignment to all derived record properties of the items, variants, and lots; available only when matching is active. |
| **IDMC Dummy Properties** | Opens the setup of the properties that may be replaced by dummy values during matching (see **Set up DMC dummy properties**). |

### User notification (User Setup)

**Who/when:** An administrator defines which persons are informed of DMC warnings from the background matching. **Entry point:** Open the **User Setup** via **Search** (company-wide standard setup) and complete the field below for each user line.

| Setup | Explanation |
|---|---|
| **Notify DMC Warnings** | When enabled, this user receives a notification by e-mail (subject "DMC Error!") when the background matching fails; if not a single user has this flag set for **DMC Background Matching**, the module refuses to enable background matching. |

### Set up DMC matching

**Process entry:** This chain connects master data, global setup, and the operational code generation. An administrator and a key user set it up together **before the first code generation**. The setup is consumed in the section **Daily Work** (IDMC entry in the document) and by the matching actions of the material type.

**Numbered steps in dependency order:**

1. **Connect material type with DMC class (master data):** On the **Material Type Card**, set the **DMC Class ID** and the **DMC Class Identifier** via **Show DMC Classes**. When these values are set, the module knows the target class; without them, all matching actions of the material type are locked.
2. **Flag properties (master data):** Using **Suggest DMC Property Matching** and **Map Missing Mandatory DMC Properties**, assign each property a **DMC Property ID** and a **DMC Category** (Mandatory/Optional). When a property is flagged as **Mandatory**, it is included in the DMC Code without exception; properties flagged as **Optional** only complement the code when they have a value.
3. **Assign property values (master data):** In the **property values**, assign the **DMC Value ID** via **Suggest DMC Property Value Matching**. When a Value ID is set, the module uses the encoded value instead of the plain text during matching.
4. **Enable matching globally (global setup):** In the **Material Property Setup**, set **DMC Active** and **DMC Matching** as well as the desired levels **DMC Item Matching**, **DMC Item Variant Matching**, **DMC Lot Matching**. When a level is not enabled, matching remains ineffective for that record type.
5. **(Optional) Background matching (global + user-specific setup):** Enable **DMC Background Matching** and, beforehand, set **Notify DMC Warnings** for at least one user. When enabled, the code determination runs asynchronously and errors are sent by e-mail to the flagged users.
6. **Operational completion:** Generate the codes via **Match DMC to Item** / **Match DMC to Item Variant** / **Match DMC to Lot No.** on the Material Type Card, or have the codes determined automatically in day-to-day business when unblocking the item or when entering the IDMC in the document (cross-reference: **Daily Work**).

### Set up DMC dummy properties

**Process entry:** If the matching finds no hit for a property combination, the module can replace certain properties with a **dummy value** and search again. A key user configures which properties are permitted as dummies per material type. The setup takes effect automatically during matching (see **Daily Work**); the result is recognizable by the **IDMC is Dummy** flag.

**Numbered steps:**

1. **Entry:** On the **Material Type Card**, open the action **IDMC Dummy Properties** (alternatively the same action in the Material Property Setup). The page is filtered to the selected material type.
2. **Define properties:** For each line, capture the property that may be replaced.

| Field | Explanation |
|---|---|
| **Material Type Code** | When set, the dummy property applies to this material type; only material types with a DMC Class ID can be selected. |
| **Material Type Description** | Shows the description of the selected material type (display only). |
| **Property Code** | When set, this property may be replaced by a dummy value during IDMC matching; only properties of the material type with an assigned DMC Property ID can be selected. |
| **Property Name** | Shows the name of the selected property (display only). |

3. **Operational completion:** During automatic matching, the module first attempts the hit with real values; if this fails, it searches again with the stored dummy properties. If an IDMC is found this way, the module sets the **IDMC is Dummy** flag on the record (cross-reference: **Master Data – Item/Lot**).

### Set up DMC optional group search

**Process entry:** Optional properties can be bundled into **search groups** so that matching also succeeds when not all optional values are present. A key user defines the groups per material type. The groups are used when determining the hash value (see **Daily Work**).

**Numbered steps:**

1. **Entry:** On the **Material Type Card**, open the action **DMC Optional Group Search**. The **DMC Opt. Search Groups** page is filtered to the material type and sorted by Material Type Code and Group No.
2. **Form groups:** Enter a group number for each optional property.

| Field | Explanation |
|---|---|
| **Material Type Code** | When set, the group line belongs to this material type; only material types with a DMC Class ID can be selected. |
| **Material Type Description** | Shows the description of the material type (display only). |
| **Property Code** | When set, this (optional or uncategorized) property is included in the search group; only properties of the material type with an assigned DMC Property ID can be selected. |
| **Property Name** | Shows the name of the property (display only). |
| **Group No.** | When set, this number groups several properties into one search group; if the matching finds no full match, it tries the groups in order until a hash value is found. |

3. **Operational completion:** During matching, the module builds a filter from the mandatory properties plus one group at a time and retrieves the hash value; the first matching group delivers the IDMC.

### Permissions

The module ships with the permission set **MuM DM All**. This determines the permissions for all DMC objects and defines which actions users may perform in the module. Assign it to the persons who set up or use DMC. In addition, the module checks the app license via the stored billing module on logon; if no valid license is present, the DMC functions are not available.

## Master Data

The master data is the basis of every code generation. DMC extends the cards and overviews of the Material Properties base module as well as the standard item and lot pages with its fields and actions.

### Material Type (Material Type Card)

**Process entry:** The material type is the central classification level. A key user connects it with a DMC class and maintains the assignment of the properties here; all code generation for items, variants, and lots of this material type depends on it. **Entry point:** Open the material type from the material type overview of the base module and call up the **Material Type Card**; the DMC fields are on the **DMC** tab.

| Field | Explanation |
|---|---|
| **DMC Class ID** | When set, the material type is connected with this DMC class of the web service; only then can the matching actions be operated and codes generated. |
| **DMC Class Identifier** | When set, this field contains the textual identifier of the class; it is written into the DMC Code and used when decoding a code to determine the material type. |
| **Last Automatch** | Shows the time of the last automatic matching; serves to monitor when codes were last determined for this material type. |

Actions of the Material Type Card (**DMC** action group):

| Action | Explanation |
|---|---|
| **Get DMC Properties** | Retrieves the properties of the connected class and displays them in the **DMC Buffer**. |
| **Suggest DMC Property Matching** | Suggests the assignment of the class properties to the properties of the material type; available only when a DMC Class ID is set. |
| **Map Missing Mandatory DMC Properties** | Assigns the still-missing mandatory class properties to the material type; available only when a DMC Class ID is set. |
| **DMC Optional Group Search** | Opens the **DMC Opt. Search Groups** for this material type (see **Set up DMC optional group search**). |
| **IDMC Dummy Properties** | Opens the **IDMC Dummy Properties** for this material type (see **Set up DMC dummy properties**). |
| **Match DMC to Item** | Determines the matching IDMC/DMC for all items of this material type without an IDMC Code; available only when a DMC Class ID is set. |
| **Match DMC to Item Variant** | Determines the IDMC/DMC for the item variants of this material type; available only when a DMC Class ID is set. |
| **Match DMC to Lot No.** | Determines the IDMC/DMC for the lots of this material type; available only when a DMC Class ID is set. |

> ☞ The matching actions require that **DMC Matching** and the respective level (item/variant/lot) are enabled in the **Material Property Setup**; otherwise the run aborts with a field check note.

### Property (Property Card)

**Process entry:** Each property receives a DMC identifier so that its value can flow into the code. A key user maintains the identifier as soon as the property is assigned to a material type with a DMC class. **Entry point:** Open the **Property Card** from the property overview of the base module.

| Field | Explanation |
|---|---|
| **DMC Property ID** | When set, the value of this property is included in the DMC Code under this identifier; without an identifier, the property cannot be matched. |
| **Last Automatch** | Shows the time of the last automatic value assignment. |

Actions of the Property Card:

| Action | Explanation |
|---|---|
| **Get DMC Property Values** | Retrieves the possible values of the property from the DMC class; available only when a DMC Property ID is set. |
| **Suggest DMC Property Value Matching** | Suggests the matching DMC Value ID per property value; available only when a DMC Property ID is set. |

### Property Values

**Process entry:** For properties with a fixed value table, a key user assigns each value a DMC value identifier so that the encoded value instead of the plain text is written into the code. **Entry point:** Open the property values from the **Property Card**.

| Field | Explanation |
|---|---|
| **DMC Value ID** | When set, the matching uses the encoded value identifier for this property value; without a Value ID, the plain-text value is used in the filter. |

Action: **Suggest DMC Property Value Matching** — suggests the DMC Value IDs for the values of the selected property and updates the lines.

### Record Properties

**Process entry:** The **record properties** are the concrete property lines of a record (material type, item, variant, lot). Here DMC adds the code-forming identifiers that are taken over from the material type assignment. A key user checks these values; as a rule they are set from the material type via **Sync DMC Fields to Record Properties**. **Entry point:** Open the record properties via the property capture of the respective record.

| Field | Explanation |
|---|---|
| **DMC Property ID** | When set, the value of this record property is included in the DMC Code under this identifier. |
| **DMC Category** | Defines how the property enters the code. **(empty):** no DMC assignment, the property does not flow into the code. **Optional:** the property is only included when it has a value, and can be omitted in the group search. **Mandatory:** the property is required and must match during matching. |

### Item and Item Variant (Item Card, Item Variant Card)

**Process entry:** On the item and the item variant, DMC stores the generated codes and controls the review sign. A key user maintains or checks these fields; the codes are created automatically when the item is unblocked or via the matching actions of the material type. **Entry point:** Open the **Item Card** from the **Item List** or the **Item Variant Card** from the **Item Variants**.

| Field | Explanation |
|---|---|
| **IDMC Code** | When set, this short code is assigned to the record; it is used in document lines for automatic resolution and is the basis for barcode generation. A duplicated IDMC on an item or variant is prevented on saving with an error. |
| **DMC Code** | When set, the record contains the full DMC Code; it is determined from the record properties or from the web service. |
| **Use DMC Review Sign** | When enabled, the module appends the review sign stored in the setup to the generated IDMC/DMC; this way lines with this code are later recognized as requiring review. Without the flag, the code remains without the additional character. |
| **IDMC is Dummy** | When set, the IDMC was found only with the help of configured dummy values (see **Set up DMC dummy properties**); this signals that the code does not stem from real values but from substitute ones. |

> ☞ On the **Item Card**, the **IDMC Barcodes** factbox shows the barcode image belonging to the IDMC Code (see **Barcodes**). The **Item Variant Card** carries the same four DMC fields as the Item Card.

### Lot (Lot No. Information Card)

**Process entry:** On the lot, DMC stores the lot-specific codes; they are created during lot matching or by entering an IDMC Code on the Lot No. Information Card. **Entry point:** Open the **Lot No. Information Card** from the **Lot No. Information List**.

| Field | Explanation |
|---|---|
| **IDMC Code** | When you enter an IDMC Code here, the module determines the associated property values from the web service, checks the material type of the item, and writes the values into the record properties of the lot (only as long as no open item ledger entry locks the lot); the description is completed and the barcodes are generated. |
| **DMC Code** | When set, the lot contains the full DMC Code. |
| **Use DMC Review Sign** | When enabled, the generated code of the lot receives the review sign (see Setup). |
| **IDMC is Dummy** | When set, the IDMC of the lot was determined via dummy values. |

> ☞ A lot property cannot be set as a pure sales property; the module prevents this with a note. Likewise, a property not flagged as a lot property cannot be changed from within the lot.

## Overview and List Pages

For quick orientation, DMC extends the most important overviews with columns. The extension adds **columns** only; it introduces no additional filter fields into the request area of the lists.

### Item List, Item Variants, Lot No. Information List

Each of these overviews additionally shows the same four columns:

| Field | Explanation |
|---|---|
| **IDMC Code** | Shows the assigned short code per line; updates as soon as a matching or a manual entry sets the code. |
| **DMC Code** | Shows the full code per line. |
| **Use DMC Review Sign** | Indicates whether the review sign is appended to the code for this record. |
| **IDMC is Dummy** | Indicates whether the IDMC was found via dummy values. |

### IDMC List

The **IDMC List** is a technical overview of the determined IDMC buffer entries with the columns **Hash Value**, **Name**, **Item No.**, **Variant Code**, **Lot No.**, and **Related Record ID**. It cannot be found via **Search** (internal diagnostic view) and serves to check the assignments.

## Daily Work

In day-to-day business, DMC mainly touches the **document lines** of sales and purchasing as well as the determination dialogs. The module has no posting or release run of its own; it fills the line and then hands over to the standard processing.

**Relation to setup:** For the IDMC entry to work, **DMC Active** and **DMC Matching** must be set in the **Material Property Setup**, the material type must have a **DMC Class ID**, and the properties/values must carry their **DMC Property ID** or **DMC Value ID** (cross-reference: **Setup – Set up DMC matching**).

### Sales Lines (Sales Order, Sales Quote, Blanket Order)

DMC extends the lines of the **sales order**, the **sales quote**, and the **blanket order** with:

| Field | Explanation |
|---|---|
| **IDMC Code** | When you enter an IDMC Code in an open, not-yet-shipped line, the module searches in order for matching lots with inventory, then item variants and items, and sets **Type**, **No.**, and, if applicable, **Variant Code** automatically. If there are multiple hits, the item or variant selection opens for adoption. |
| **DMC Review Required** | When set, the entered code ended in the review sign; the module removes the character, flags the line as requiring review, and reports "The DMC needs to be reviewed!". |

Flow of the IDMC entry in the sales line (derived from the code):

1. Open the **sales order** and create a new line.
2. Enter the scanned or received code in the **IDMC Code** field (the line must be open and not yet shipped).
3. If the module finds **lots with inventory** for the IDMC, the line is filled with their item/variant.
4. If it finds no lot with inventory, it checks lots without inventory, then unique item variants, then items; in case of ambiguity, the **item variant** or **item selection** appears.
5. If no assignment leads to the target, the module decomposes the DMC (or retrieves it via the web service) and starts the property search. In the absence of a full match, the prompt **"No match found for all. Search just with required?"** appears.
6. If the found inventory is insufficient or not at the location, the prompt **"Not found enough quantity or on location. Continue?"** appears; on confirmation, the search is repeated without a warehouse/quantity filter.
7. The line is filled with **item**/**variant** and the IDMC Code; the actual posting is then performed via the standard actions of Business Central.

### Purchase Lines (Purchase Order, Purchase Quote, Blanket Purchase Order)

DMC extends the lines of the **purchase order**, the **purchase quote**, and the **blanket purchase order** with the same two fields **IDMC Code** and **DMC Review Required**. When you select an **item** (field **No.**) or a **Variant Code** in a purchase line, the module automatically takes over the **IDMC Code** and the **DMC Review Required** flag from the item or the variant. This way the code is already visible on the line at procurement.

### Determination and Selection Dialogs

When retrieving and adopting classes, properties, and values, several dialog pages open:

#### DMC Buffer

The **DMC Buffer** shows classes, properties, values, and translations as an expandable tree (indented by level, color-graded). It serves the selection and adoption of the desired lines.

| Field | Explanation |
|---|---|
| **Selected** | Indicates whether the line is marked (display only). |
| **Name** | Designation of the class, property, or value. |
| **Value** | The associated value. |
| **Type** | Type of the line in the tree. **(empty):** no assignment. **Class:** a DMC class. **Class Group / Class Substance Group:** groupings of the class. **Class Property:** a property of the class. **Property Value:** a possible value. **Class Translation / Class Property Translation / Property Value Translation:** language translations of the respective level. |
| **Language** | Language identifier on translation lines. |
| **Property Category** | Category of the property (Mandatory/Optional). |
| **Related Record** | Shows the already linked Business Central record; via **Edit** you jump into the associated record property page. |

Actions of the DMC Buffer:

| Action | Explanation |
|---|---|
| **Get Properties** | Loads the properties of the marked class. |
| **Create from Selection** | Creates or changes the material type, properties, values, or translations in Business Central from the marked lines; afterwards, proposed changes are shown in **Changed Values** for confirmation. |
| **Select Lines** | Marks the current selection (shortcut Ctrl+1). |
| **Remove Selections** | Removes the marking (Ctrl+2). |
| **Show All Lines** | Shows all lines (Ctrl+3). |
| **Show Selected Lines** | Shows only marked lines (Ctrl+4). |

#### DMC Suggestion

The **DMC Suggestion** lists the assignments suggested by the web service (Property ID, Value ID, Name, Property Code/Name, and **Match Counter**). Based on the Match Counter you can tell how reliable a suggestion is before you adopt it.

#### Changed Values

After **Create from Selection**, the **Changed Values** page shows the pending changes with **Old Value**, **New Value**, **Source Table**, and **Source Record**. Via the **Change Option**, you decide per line:

| Field | Explanation |
|---|---|
| **Change Option** | **(empty):** the change is not adopted. **Accept:** the new value is written into the source record when leaving the page. |

## Barcodes

For every **IDMC Code**, the module automatically creates barcode images as soon as the code is generated or completed. The **IDMC Barcodes** page and the factbox of the same name on the Item Card display the images.

| Field | Explanation |
|---|---|
| **IDMC Code** | The code the barcode belongs to. |
| **Barcode Type** | Type of the barcode. **Code 39:** a linear barcode. **QR Code:** a two-dimensional matrix code. For every IDMC, exactly one image is generated per barcode type. |
| **Image** | The rendered barcode image (delivered by the web service and stored as an image). |

## Posted Documents and History

The IDMC flagging is retained through posting. DMC extends the lines of the **posted** sales and purchase documents — posted sales shipment, invoice, and credit memo, posted purchase receipt, posted purchase invoice and credit memo, posted sales and purchase returns — as well as the document archives with the columns **IDMC Code** and **DMC Review Required** (display only). This way it is also traceable afterwards which code a line was captured with and whether it required review.

## FAQ and Troubleshooting

### 1. Why are the DMC actions on the Material Property Setup grayed out?

The **DMC** action group can only be operated when the **DMC Active** flag is set. Enable the flag and enter Url, User, and Password.

### 2. Why does entering a code report "The input is not a valid IDMC"?

The entered code does not start with the **DMC Prefix** stored in the setup, or could not be resolved by the web service. Check the prefix and separator in the **Material Property Setup**.

### 3. What happens when the matching finds no full match?

The module asks "No match found for all. Search just with required?". Confirm to continue searching with the required properties; alternatively, set up **DMC dummy properties** or a **DMC optional group search**.

### 4. Why can't DMC Background Matching be enabled?

For background matching, at least one user in the **User Setup** must carry the **Notify DMC Warnings** flag. Without such a user, the module prevents enabling it with a note.

### 5. Why does an item not receive an IDMC/DMC Code?

Check whether **DMC Matching** and the appropriate level (**DMC Item Matching**) are set, whether the material type has a **DMC Class ID**, and whether the required properties have a **DMC Property ID** and a value.

### 6. What does the "IDMC is Dummy" flag on the record mean?

The IDMC was found not with the real values but via configured **dummy properties**. The code is thus a substitute hit; check the values if the assignment has to be unambiguous.

### 7. Why does the note "The DMC needs to be reviewed!" appear?

The entered or generated code ended in the **DMC Review Sign**. The module removes the character and marks the line with **DMC Review Required**. Check the affected line.

### 8. Why does the system report "There is one Entry with the same IDMC"?

An IDMC Code may be assigned only once per item or item variant. The module prevents duplicates on saving. Find the already existing record and clean up the duplicate assignment.

### 9. Why can't a lot property be changed or set as a sales property?

A property not flagged as a lot property cannot be changed from within the lot, and a lot property cannot be set as a pure sales property. Adjust the flags of the property in the material type assignment.

### 10. Why does the module refuse further retrievals ("You have not got any dmc license")?

The **DMC Bought Value** is used up (**DMC Remaining Value** = 0). Increase the quota or acquire a new license; via **DMC Warning Value** you can be warned in good time before it is used up.

## Typical Use Cases

The following scenarios are derived from the verified behavior of the module.

### Use Case 1: Connect a new material type with a DMC class and code the items

- **Trigger:** The metal data service has a new material class; a key user is to assign DMC codes to the associated items.
- **Entry in BC:** Open the material type from the material type overview → **Material Type Card**, **DMC** tab.
- **Core flow:** Choose the class via **Show DMC Classes** (**DMC Class ID**/**Identifier** are set) → **Suggest DMC Property Matching** → **Map Missing Mandatory DMC Properties** → assign the **DMC Value ID** in the **property values** via **Suggest DMC Property Value Matching** → **Match DMC to Item**. The items receive an **IDMC Code** and a **DMC Code**.
- **Completion:** On the **Item Card**, the **IDMC Barcodes** factbox shows the generated barcode; in the **Item List**, the new code columns are filled.

### Use Case 2: Enrich a lot in goods receipt via IDMC

- **Trigger:** An IDMC (label/scan) is available for an incoming lot; the lot properties are to be set automatically.
- **Entry in BC:** Open the **Lot No. Information Card** of the lot.
- **Core flow:** Enter the code in the **IDMC Code** field. The module retrieves the DMC from the web service, checks the material type of the item, writes the values into the **record properties** of the lot (as long as no open item ledger entry locks the lot), and completes the description.
- **Completion:** The lot carries an **IDMC Code**/**DMC Code**; the barcodes are ready. If the material type of the item differs from the class of the code, the process aborts with a note.

### Use Case 3: Fill a sales line via a scanned IDMC

- **Trigger:** A customer transmits an IDMC/barcode instead of an item number.
- **Entry in BC:** Open the **sales order**, new line.
- **Core flow:** Enter the code in the **IDMC Code** field. The module first searches for lots with inventory, then variants and items; in case of ambiguity, the selection page appears. Prompts about mandatory properties and inventory/location are displayed as needed. If the code ends in the review sign, the line is marked as **DMC Review Required**.
- **Completion:** The line is filled with **item**/**variant** and **IDMC Code**; the posting is performed via the standard actions of Business Central.
