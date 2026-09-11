---
title: Anwenderhandbuch m+m Item Charge Management
---

# User Guide m+m Item Charge Management

## Introduction

The **m+m Item Charge Management** module extends the item charge processing of Microsoft Dynamics 365 Business Central. It makes it possible to feed **item charges** (freight, packaging flat rates, minimum-quantity surcharges and similar incidental costs) into sales and purchase documents in a rule-based way from master data – automatically on release, manually at the push of a button, or as a pre-filtered selection. This removes the need to repeatedly create item charge lines by hand, and the costs are distributed across the item lines according to stored rules.

**Target audience.** The primary audience is **operational users in sales and purchasing** who process, release and post sales orders, sales invoices, purchase orders and purchase invoices every day. They add item charges in the document lines or have them generated automatically on release. **Administrators and key users** are the secondary audience: they maintain the central **Item Charge Setup**, the individual **Item Charges** and their **Item Charge Assignments**.

**Process overview.** Before item charges take effect in documents, the administrator configures three levels that build on one another: the global **Item Charge Setup**, the individual **Item Charges** (master card with reference value, calculation time and transfer rule) and, per item charge, one or more **Item Charge Assignments** (price and validity per customer/vendor and item). Optionally, **Specific Assignments** restrict an assignment to certain document classes (for example, sales invoice only). In daily work the user selects the **Release**, **Add Item Charge** or **Item Charge Suggestions** action in the document; the module then generates the matching item charge lines and assigns them to the item lines.

The typical entry path is: open **Item Charges** (master card) → action **Item Charge Management → Item Charge Assignments** → maintain assignment; then edit the document line in the **Sales Order** or the **Purchase Order** and feed in the item charge via **Release** or the line actions.

## Quick Start for Users

The quick start describes the shortest route from an empty system to an effective item charge. Setup is a prerequisite and therefore comes first.

1. **One-time setup (administrator):** Open the **Item Charge Setup** via **Search** and define how document charges are distributed and at which delivery time quantity/flat-rate item charges are calculated.
2. **Create an item charge:** Open **Item Charges** via **Search**, create a record, and set **Reference Value**, **Transfer Automatically To Document**, **Selectable For Doc. Line** and **Calculation Time**.
3. **Assign a price:** On the **Item Charges** card, choose the action **Item Charge Management → Item Charge Assignments** and, per customer/vendor (or "All Customer"/"All Vendor"), enter the **Price**, the **Price Type**, the validity period and – if needed – **Minimum Type**, **Minimum Value** and **Fill Difference**.
4. **Apply in the document:** Create a **Sales Order** (or a **Purchase Order**) with an item line.
   - With **Transfer Automatically To Document = By Releasing**, choose **Release** – the item charge is generated as its own line.
   - If needed, add further item charges in the document line via **Line → Functions → Add Item Charge** or **Item Charge Suggestions**.
5. **Ship and post:** Continue processing the document in the Business Central standard way (post the warehouse shipment if applicable) and choose **Post**. Via **Reopen** the system removes automatically generated item charge lines again, so that a fresh release applies the current configuration.

## Setup

Setup is the foundation of the module. It consists of a global setup card, the master cards of the individual item charges (described in the **Master Data** chapter) and the assignment of permissions.

### Item Charge Setup

**Who and when.** This card is maintained by the administrator **once before first use**. It is a company-wide single record (singleton): the record is created automatically the first time it is opened. The values set here act as a default for **every** item charge with reference value **Document**, **Quantity** or **Lump-sum**, and therefore indirectly take effect in all sales and purchase documents.

**Entry:** Open the **Item Charge Setup** via **Search**. It is a global setup page without superordinate master data; opening it via **Search** is the intended route here.

The page is divided into the areas **General**, **Sales** and **Purchase**.

| Setup | Explanation |
|---|---|
| **Calculation For Ref. Type Document** (General) | If an item charge has the reference value **Document**, then the document amount is distributed across all item lines using this rule. **Volume:** distribution by volume × quantity (total volume) of the lines. **Value:** distribution based on the line amount. **Equal:** proportionally equal by number of lines (for example, 4 lines at 25 % each). **Weight:** distribution based on the net weight of the lines. The selection determines the amount each item line receives from the document charge. |
| **Quantity/Flat-Rate To Ship** (Sales) | Defines the delivery time at which a sales item charge with reference value **Quantity** or **Lump-sum** is calculated. Acts as a default for new sales item charges. Values are listed below. |
| **Reference Value Document To Ship** (Sales) | Defines the delivery time at which a sales item charge with reference value **Document** is calculated. Default for new sales item charges. Values are listed below. |
| **Quantity/Flat-Rate To Receive** (Purchase) | Defines the delivery time at which a purchase item charge with reference value **Quantity** or **Lump-sum** is calculated. Default for new purchase item charges. Values are listed below. |
| **Reference Value Document To Receive** (Purchase) | Defines the delivery time at which a purchase item charge with reference value **Document** is calculated. Default for new purchase item charges. Values are listed below. |

Values for **Quantity/Flat-Rate To Ship** and **To Receive**:
- **Default:** When selected, the system behaves like the Business Central standard; the item charge follows the normal quantity logic.
- **First Shipment (complete)** / **First Receive (complete):** When selected, the item charge is calculated in full at the first delivery.
- **Last Shipment (complete)** / **Last Receive (complete):** When selected, the item charge is calculated at the last delivery; it takes effect as soon as the remaining quantity reaches 0.
- **Every Shipment** / **Every Receive:** When selected, the item charge is calculated proportionally to the quantity delivered in each case.

Values for **Reference Value Document To Ship** and **To Receive**:
- **Default:** When selected, the Business Central standard behavior applies.
- **First Shipment** / **First Receive:** When selected, the document-related item charge is calculated at the first delivery.
- **Last Shipment** / **Last Receive:** When selected, the document-related item charge is calculated at the last delivery, as soon as the remaining quantity reaches 0.

**Relationship to daily work.** These defaults take effect as soon as the **Reference Value** is set on an item charge card (see Master Data): for reference value **Document** the system adopts the values **Reference Value Document To Ship/To Receive**, for reference value **Quantity**/**Lump-sum** the values **Quantity/Flat-Rate To Ship/To Receive**. The delivery time later decides, during posting, which quantity share of the item charge takes effect.

### Setting up permissions

**Who and when.** Before first use, the administrator assigns the module's permission set to users. The permission set **"All permissions"** (the module's internal permission set) defines which actions users may perform on the item charge data: it grants full access (read, insert, modify, delete) to the tables **Item Charge Assignment**, **Specific Assignments**, **Item Charge Setup**, **Item Charge Translation** as well as the associated pages and processing codeunits. Without this permission set, users can neither view nor maintain the item charge master data and cannot run the document actions. Assign the set to the relevant user groups via the standard Business Central permission management.

## Master Data

The entire automation is built on the master data. It comprises the **Item Charges** (the actual item charge types), their **Item Charge Assignments** (prices and validities), the optional **Specific Assignments** (document-class control) and the **Translations**.

### Item Charges (master card)

**Who and when.** Key users or the administrator maintain the item charge types before they are fed into documents. Each record describes exactly one item charge type (for example "Freight", "Minimum-quantity surcharge") and controls **how** and **when** it reaches documents.

**Entry:** Open **Item Charges** via **Search**. This page is the central master list; it extends the standard Business Central page with the following fields and with the **Item Charge Management** action group.

| Field | Explanation |
|---|---|
| **No.** | Unique number of the item charge; serves as a reference in assignments and document lines. |
| **Description** | Meaningful name of the item charge; appears as the text of the generated document line. |
| **Gen. Prod. Posting Group** | If set, it links the postings of the item charge to the appropriate G/L account via the posting matrix; without a correct group, posting the item charge line fails. |
| **VAT Prod. Posting Group** | If set, it controls the VAT of the item charge line via the VAT posting matrix; determines the tax amount shown. |
| **Reference Value** | Determines what the item charge relates to and thereby controls all subsequent processing. Values are listed below. |
| **Selectable For Doc. Line** | When enabled, the user can select this item charge manually in the document line via **Add Item Charge**; if the flag is not set, the item charge does not appear in the selection list. |
| **Transfer Automatically To Document** | Controls whether and when the item charge reaches the document without any user action. Values are listed below. |
| **Unit Of Measure Code** | If set, the generated item charge line is created with this unit of measure; without an entry, the line uses no separate unit of measure. |
| **Calculation Time** | Defines which date the price calculation of the item charge uses at invoice creation. Values are listed below. The default is **Order Date**. |
| **Reference Value Document To Receive** | If the reference value is **Document**, this value determines the delivery time in purchasing; it is defaulted from the setup and is editable only for reference value **Document**. |
| **Quantity/Flat-Rate To Receive** | If the reference value is **Quantity**/**Lump-sum**, this value determines the delivery time in purchasing; defaulted from the setup. |
| **Reference Value Document To Ship** | As above, but for sales and editable only for reference value **Document**. |
| **Quantity/Flat-Rate To Ship** | As above, but for sales and editable only for reference value **Quantity**/**Lump-sum**. |
| **Search Description** | If set, the user finds the item charge via this text, even if the number is unknown. |

Values for **Reference Value**:
- **(empty):** The Business Central standard applies; the item charge is not fed in by the module.
- **Lump-sum Partial:** Line-related with quantity = 1; the item charge relates proportionally to the individual item line.
- **Document:** The item charge relates to all lines of the document (quantity = 1) and is distributed according to the **Calculation For Ref. Type Document** rule.
- **Quantity:** Line-related with quantity = quantity of the item line; the item charge scales with the item quantity.
- **Lump-sum Total:** Lump-sum related to the entire line amount.

Values for **Transfer Automatically To Document**:
- **(empty):** No automatic transfer; the item charge is only available for manual selection (provided **Selectable For Doc. Line** is set).
- **Yes:** When selected, the system creates the item charge line automatically as soon as the item line is inserted and validated. This value cannot be combined with reference value **Document** (the system rejects the combination with an error message).
- **Manual:** When selected, the transfer is left to the user; they add the line via **Add Item Charge** or **Item Charge Suggestions**.
- **By Releasing:** When selected, the system generates the item charge line automatically as soon as the user **releases** the document; on **Reopen** it is removed again.

Values for **Calculation Time**:
- **(empty):** No separate time is stored.
- **Work Date:** Price calculation at invoice creation uses the work date.
- **Posting Date:** Price calculation uses the posting date.
- **Order Date:** Price calculation uses the order date (default).
- **Shipment Date/Expected Receipt Date:** Price calculation uses the shipment date or expected receipt date.

**Actions of the "Item Charge Management" action group:**
- **Item Charge Assignments** – opens the **Item Charge Assignment** filtered to the current item charge (see below).
- **Translation** – opens the **Item Charge Translations** (see below).

#### Setting up an item charge

**Process.** This chain makes an item charge effective in documents. The administrator configures it once per item charge type; the sales and purchasing departments use the result later in daily work (see chapter **Daily Work**).

1. **Check the global setup:** In the **Item Charge Setup**, define the distribution rule and the delivery times. When these values are set, they are defaulted automatically on every new item charge card.
2. **Create the item charge card:** On **Item Charges**, enter the **Reference Value**. If you choose **Document**, the setup's distribution rule controls the split across the lines; if you choose **Quantity**/**Lump-sum**, the item charge scales with the line.
3. **Define the transfer behavior:** Set **Transfer Automatically To Document** (Yes / Manual / By Releasing) and – for manual selection – **Selectable For Doc. Line**. When **By Releasing** is set, the document line is created only on release.
4. **Assign a price:** Switch via **Item Charge Management → Item Charge Assignments** and store the price per customer/vendor (next section).
5. **Operational conclusion:** In daily work the user accesses the configured chain via **Release** or **Add Item Charge**/**Item Charge Suggestions** (see **Daily Work in Sales**).

### Item Charge Assignment (price table)

**Who and when.** The key user maintains the **Item Charge Assignments** for each item charge before the item charge takes effect price-wise in documents. Here, prices and validities are defined per customer or vendor and per item.

**Entry:** Open the **Item Charges** card and choose the action **Item Charge Management → Item Charge Assignments**. The list opens filtered to the selected item charge (**No.**).

| Field | Explanation |
|---|---|
| **No.** | Refers to the item charge to which the assignment belongs. |
| **Reference Type** | Defines the group of business partners for which the assignment applies, and controls the selection of the **Reference No.**. Values are listed below. |
| **Reference No.** | If the reference type is **Customer** or **Vendor**, this field specifies the concrete customer or vendor; with **All Customer**/**All Vendor** it remains empty (the system rejects an entry there). |
| **Type** | Defines whether the assignment applies to a specific item or to all items, and controls the **Code** field. Values are listed below. |
| **Code** | If the type is **Item**, this field contains the item number; with **All Items** it remains empty. |
| **Price** | If set, this value forms the price of the item charge; the interpretation depends on the **Price Type**. |
| **Price Type** | Determines how the **Price** is interpreted. **Total:** fixed amount. **Percentage:** percentage value that, depending on the reference value, is applied to the document amount, line amount or unit price. |
| **Starting Date** | If set, the assignment applies from this date; empty means no lower limit. |
| **Ending Date** | If set, the assignment applies up to this date; the starting date may not be later than the ending date (the system rejects this). |
| **Minimum Type** | Defines against which reference value the **Minimum Value** is checked. Values are listed below. |
| **Minimum Value** | If set, the item charge only takes effect as long as the respective amount (line or document) falls below the minimum value; requires a **Minimum Type**. |
| **Fill Difference** | When enabled, the item charge fills the amount up to the **Minimum Value** instead of adding a fixed amount; permitted only with reference value **Document** and minimum type **Line Amount** or **Document Amount**. |
| **Specific Assignments** | If set to **Specific Selection**, the assignment is additionally restricted to certain document classes via the **Specific Assignments** (see next section); with **(empty)** the assignment applies to quote and order without further restriction. |
| **Count of Specific Assignments** | Shows how many **Specific Assignments** are stored for this line (filtered by the set **Specific Assignment Filter**). Clicking the number opens the filtered list of specific assignments directly. |

Values for **Reference Type**:
- **All Customer:** The assignment applies to all customers; the reference no. remains empty.
- **Customer:** The assignment applies to the customer specified in **Reference No.**.
- **All Vendor:** The assignment applies to all vendors; the reference no. remains empty.
- **Vendor:** The assignment applies to the vendor specified in **Reference No.**.

Values for **Type**:
- **All Items:** The assignment applies to all items; **Code** remains empty.
- **Item:** The assignment applies to the item specified in **Code**.

Values for **Minimum Type**:
- **(empty):** No minimum check; the item charge takes effect regardless of the amount.
- **Line Amount:** The minimum value is checked against the amount of the individual item line.
- **Document Amount:** The minimum value is checked against the total amount of the document.

**Determination logic.** When applying, the module searches for the matching assignment in this order: first **Item + Customer/Vendor**, then **All Items + Customer/Vendor**, then **Item + All Customer/All Vendor**, finally **All Items + All Customer/All Vendor**. In addition, the **Calculation Time** must fall within the validity period (starting/ending date). This makes it possible to combine general and specially negotiated conditions.

#### Filter

The **Item Charge Assignment** list provides a document-class filter that controls the count field.

| Filter field | Explanation |
|---|---|
| **Specific Assignment Filter** | If set (Sales Quote & Sales Order / Sales Invoice / Purchase Quote & Purchase Order / Purchase Invoice), the **Count of Specific Assignments** field counts only the specific assignments of this document class; without a filter, the count refers to all specific assignments stored for the line. |

### Specific Assignments

**Who and when.** The key user restricts an item charge assignment to certain document classes when an item charge should take effect only in specific documents (for example, only in the sales invoice). This function addresses cases in which the sales price is not fixed until late – for instance through calculation in the invoice.

**Entry:** Open the relevant line in the **Item Charge Assignment** list, set **Specific Assignments** to **Specific Selection** and then choose the **Specific Assignments** action, or click the number in the **Count of Specific Assignments** column. The **Specific Assignments** page can only be reached this way (no access via **Search**).

| Field | Explanation |
|---|---|
| **Specific Assignment** | Defines in which document class the superordinate assignment may take effect. Values are listed below. The remaining columns (No., Reference Type, Reference No., Type, Code, Starting/Ending Date) are read-only and are adopted from the selected assignment line. |

Values for **Specific Assignment**:
- **Sales Quote & Sales Order:** If stored, the item charge takes effect in the sales quote and the sales order.
- **Sales Invoice:** If stored, the item charge takes effect in the sales invoice.
- **Purchase Quote & Purchase Order:** If stored, the item charge takes effect in the purchase quote and purchase order.
- **Purchase Invoice:** If stored, the item charge takes effect in the purchase invoice.

#### Setting up a specific assignment

**Process.** This chain unlocks document-class-specific control. It is the module's second, independent configuration chain alongside the general item charge setup.

1. **Prepare the assignment:** In the **Item Charge Assignment**, create the desired line (price, reference type, validity).
2. **Activate the specific assignment:** In the line, set the **Specific Assignments** field to **Specific Selection**. When activated, the **Specific Assignments** button becomes effective and the line is then controlled only via the stored document classes.
3. **Store the document classes:** Open the list via **Specific Assignments** and enter one record per document class (Sales Quote & Sales Order, Sales Invoice, Purchase Quote & Purchase Order, Purchase Invoice). When a document class is stored, the item charge takes effect exactly there.
4. **Check in the document:** Via the **Specific Assignment Filter** and the **Count of Specific Assignments** column you check for which document class entries exist.
5. **Operational conclusion:** In the sales invoice or purchase invoice the user adds the item charges controlled in this way via **Add Item Charge** / **Item Charge Suggestions** (see **Daily Work**). Without a matching specific assignment, the item charge does not appear in invoices.

### Translations

**Who and when.** The key user maintains translations of the item charge description when documents are generated in multiple languages.

**Entry:** Open the **Item Charges** card and choose **Item Charge Management → Translation**. The **Item Charge Translations** list can only be reached via this action.

| Field | Explanation |
|---|---|
| **Language Code** | If set, the translation applies to this language code; when printing the document, the system selects the description matching the document language. |
| **Description** | Translated text of the item charge, shown instead of the standard description. |

## Daily Work in Sales

**Relationship to setup.** The actions visible in sales are controlled by the master data: **Item Charges** (Reference Value, Transfer Automatically To Document, Selectable For Doc. Line, Calculation Time), **Item Charge Assignment** (Price, Minimum Value, Fill Difference) and – where maintained – **Specific Assignments** (document class). Changes to these conditions take effect immediately in the next documents.

The module extends the line ribbons of the following sales documents with the **Add Item Charge** and **Item Charge Suggestions** actions (each under **Line → Functions**):

- Sales Quote
- Sales Order
- Sales Invoice

In addition, the module hooks into the standard release of the **Sales Order** (and further sales documents including the blanket order).

### Actions in the sales document line

- **Add Item Charge** (keyboard shortcut Alt+Z): Opens the list of **Item Charges**, filtered to the item charges selectable in the document. The prerequisite is that the item charge has **Selectable For Doc. Line** set; the active line must be of type **Item**. After selecting with **OK**, the system creates the matching item charge lines and assigns them to the item line. In the sales invoice, additionally only item charges with a matching **Specific Assignment** (Sales Invoice) are selectable.
- **Item Charge Suggestions**: Determines, for the marked item line(s), the matching manual item charges according to master data and adds them if not already present. Assignments that already exist are not created twice.

### Automatic item charge on release (posting flow)

The posting flow in sales follows the Business Central standard; the module merely adds the automatic item charge line:

1. Open the **Sales Order** and enter the item line (type **Item**, quantity).
2. Optionally, in the line, add **Item Charge Suggestions** or **Add Item Charge** via **Line → Functions**.
3. Choose **Release**. If the associated item charge has **Transfer Automatically To Document = By Releasing**, the system now generates the item charge line and assigns it to the item line. Item charges with **= Yes** are created already when the item line is entered.
4. If needed, choose **Reopen** – automatically generated item charge lines (By Releasing) are removed, so that a fresh release applies the current configuration.
5. Continue processing the document (post the warehouse shipment if applicable) and choose **Post**. On posting, the item charge is assigned to the respective delivered quantity according to **Quantity/Flat-Rate To Ship** or **Reference Value Document To Ship**.

**Document chain.** If a sales order is created from a quote with item charges, the item charges are carried over as well; the same applies when creating a sales invoice from an order. An item charge with **By Releasing** is not created again if an assignment already exists for the item line.

**Document charge with Fill Difference.** If a document charge is set to **Fill Difference**, the line charge is first assigned to the item lines and then the document charge is distributed as the last line after all item and item charge lines. The already existing line and document line amount thereby reduces the document amount to be filled up, so that the configured total amount (minimum value) is reached exactly.

## Daily Work in Purchasing

**Relationship to setup.** Analogous to sales, **Item Charges**, **Item Charge Assignment** and **Specific Assignments** control the behavior; in purchasing the purchase variants of the delivery times apply (**Quantity/Flat-Rate To Receive**, **Reference Value Document To Receive**) as well as the reference type **Vendor**/**All Vendor**.

The module extends the line ribbons of the following purchase documents with **Add Item Charge** and **Item Charge Suggestions**:

- Purchase Quote
- Purchase Order
- Purchase Invoice

In addition, the module hooks into the release of the **Purchase Order** (and the blanket purchase order document).

### Actions in the purchase document line and posting flow

- **Add Item Charge** and **Item Charge Suggestions** work as in sales: manual or pre-filtered selection of the item charges matching the master data; prerequisite **Selectable For Doc. Line** and line type **Item**.
- **Release** of the purchase order automatically generates the item charge lines for all item charges with **Transfer Automatically To Document = By Releasing**; **Reopen** removes them again. If the conditions were changed in the meantime, the current configuration is applied on the next release.
- **Post** assigns the item charge to the receipt or invoice quantity according to the purchase delivery times.

**History and archive.** When documents are archived, the document line archives adopt the control fields of the item charge (among others **Autom. Created Charge**, **Charge Ref. Value**, **Minimum Type**), so that archived documents retain the original item charge logic in a traceable way. The module does not provide a separate history list; tracking is done via the standard document archives and the value entries of Business Central.

## FAQ and Troubleshooting

### 1. Why does my item charge not appear automatically in the document?
On the **Item Charges** card, check the **Transfer Automatically To Document** field. Only with **Yes** (when the item line is entered) or **By Releasing** (on release) is the line created automatically. With **Manual** or **(empty)** you must add the item charge via **Add Item Charge**.

### 2. Why can I not select an item charge via "Add Item Charge"?
The selection shows only item charges for which **Selectable For Doc. Line** is enabled. If the flag is not set, the system hides the item charge in the selection list. In addition, the active document line must be of type **Item**.

### 3. Why does the system report an error when I combine "Transfer Automatically To Document = Yes" with reference value "Document"?
This combination is not permitted. A document charge (**Reference Value = Document**) cannot be formed already when the item line is entered (**Yes**), because it relates to all lines. Choose **By Releasing** or **Manual** instead.

### 4. What is "Fill Difference" used for?
When **Fill Difference** is enabled, the item charge fills the document or line amount up to the **Minimum Value** instead of adding a fixed amount. This is only possible with reference value **Document** and minimum type **Line Amount** or **Document Amount** and is used to reach minimum amounts.

### 5. Why does an item charge take effect in the sales invoice but not in the order (or vice versa)?
The **Specific Assignments** setting is responsible. If it is set to **Specific Selection**, the item charge takes effect only in the document classes stored under **Specific Assignments** (for example, only **Sales Invoice**). Without a matching entry, the item charge does not appear in the relevant document class.

### 6. How do I check for which documents an assignment applies?
Open the **Item Charge Assignment**, set the **Specific Assignment Filter** to the desired document class and read off the **Count of Specific Assignments** column. Clicking the number opens the filtered list of **Specific Assignments**.

### 7. Why does my automatic item charge line disappear on Reopen?
Item charges with **By Releasing** are coupled to the release. On **Reopen**, the system removes the automatically generated lines again, so that a fresh release applies the configuration then valid (for example, changed prices). Lines that have already been shipped or invoiced are retained.

### 8. Which assignment is chosen when several match?
The module searches in a fixed order: **Item + Customer/Vendor**, then **All Items + Customer/Vendor**, then **Item + All Customer/All Vendor**, finally **All Items + All Customer/All Vendor**. In addition, the **Calculation Time** must fall within the validity period (starting/ending date). Thus more specific conditions take precedence.

### 9. Why does the calculated amount differ between the order and the invoice?
The **Calculation Time** defines which date the price calculation uses (work, posting, order or shipment date). With **Price Type = Percentage**, the amount also depends on the reference value (document amount, line amount or unit price), which can change between documents.

### 10. Why is the item charge posted only proportionally?
The decisive settings are **Quantity/Flat-Rate To Ship/To Receive** or **Reference Value Document To Ship/To Receive**. With **Every Shipment/Every Receive** the item charge is calculated proportionally to the delivered quantity; with **First/Last Shipment (complete)** or **First/Last Receive (complete)** it is calculated fully at the first or last delivery. The full amount therefore arises only once the decisive delivery has been posted.

## Typical Use Cases

### Use Case 1 – Freight flat rate automatically on order release

**Trigger.** Sales enters a standard order; according to the terms agreement, a freight flat rate is incurred per order that must not be forgotten.

**Entry in BC.** The administrator has created the "Freight" item charge on **Item Charges** with **Reference Value = Lump-sum Total** and **Transfer Automatically To Document = By Releasing** and stored a price for the customer via **Item Charge Management → Item Charge Assignments**.

**Core flow.**
1. The user opens the **Sales Order** and enters the item line.
2. The user chooses **Release**.
3. The system automatically generates the "Freight" item charge line and assigns it to the item line.

**Conclusion.** The order is processed further in the standard way and **posted**. If the user chooses **Reopen**, the freight line is removed and re-created on the next release.

### Use Case 2 – Minimum-quantity surcharge only in the sales invoice (Specific Assignment)

**Trigger.** The sales price is not fixed until the sales invoice (calculation). A minimum-quantity surcharge should fill the remaining amounts up to a minimum value – but only in the invoice, not in the quote or order.

**Entry in BC.** The key user maintains a line in the **Item Charge Assignment** with **Minimum Type = Document Amount**, **Minimum Value** and **Fill Difference = active**, sets **Specific Assignments** to **Specific Selection** and stores the document class **Sales Invoice** under **Specific Assignments**.

**Core flow.**
1. The user creates the **Sales Invoice** (if applicable, via delivery lines from a posted warehouse shipment).
2. In the invoice line the user chooses **Line → Functions → Item Charge Suggestions** or **Add Item Charge**.
3. The system offers the surcharge, because a **Specific Assignment** for **Sales Invoice** exists, and fills the document amount up to the **Minimum Value**.

**Conclusion.** The user chooses **Release** and **Post**; the filled item charge line appears in the posted sales invoice.

### Use Case 3 – Adding additional costs manually in a purchase order

**Trigger.** A supplier announces a one-time packaging surcharge by phone, which should be taken into account in the current purchase order.

**Entry in BC.** The item charge is created on **Item Charges** with **Selectable For Doc. Line = active** and an **Item Charge Assignment** for the vendor.

**Core flow.**
1. The user opens the **Purchase Order** and marks the item line (type **Item**).
2. The user chooses **Line → Functions → Add Item Charge** (Alt+Z).
3. In the **Item Charges** list the user selects the packaging surcharge and confirms with **OK**; the system creates the item charge line and assigns it to the item line.

**Conclusion.** The purchase order is **released** and, after receipt, **posted**; the manually added item charge is assigned according to the purchase delivery times.
