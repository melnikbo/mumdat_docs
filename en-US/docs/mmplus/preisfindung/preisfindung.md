---
title: Anwenderhandbuch m+m Price Calculation
---

# m+m Price Calculation User Guide

## Introduction

The **m+m - Price Calculation** module extends Microsoft Dynamics 365 Business Central with an additional price calculation method that determines sales and purchase prices not per sales or purchase unit, but per a freely definable **Calculation Unit**. Typical use case: an item is sold in "pieces" or "kg", but the price should be stated per liter, per meter, or in a tier such as "100/liter" and automatically converted into the unit price of the document line.

For this purpose, the module provides two master data lists — the **Sales Price Calculation List** and the **Purchase Price Calculation List** — in which, for each combination of customer or vendor, type (Item, item group, G/L account, charge/allowance), unit, and calculation unit, it is defined how the conversion is performed. The additional fields **Calculation Unit**, **Calculation Quantity**, and **Calculation Price** then appear in the sales and purchase documents as well as in the price lists.

**Target audience:** This guide is aimed primarily at **operational users** in Sales and Purchasing who enter document lines and maintain prices every day — they select the appropriate calculation unit in quote, order, purchase order, invoice, and price list and work with the resulting calculation price. **Secondarily**, the guide is relevant to administrators and key users who activate the price calculation method, set up the **Fix Calculation Price**, and maintain the price calculation lists as master data.

**Brief process overview:** First, the administrator activates the **m+m - Price Calculation** method and decides whether the calculation price is fixed. Next, a key user maintains the Sales/Purchase Price Calculation Lists. In day-to-day work, the user selects a calculation unit in the document line; the system determines the matching price calculation, computes the calculation quantity and the calculation price, and writes the converted unit price or direct unit cost back to the line.

## Quick Start for Users

The fastest way to a calculated price — in the order in which the setup requires it:

1. **Setup (one-time, administrator):** Using **Search**, open the **Sales & Receivables Setup** and set the **Price Calculation Method** to **m+m - Price Calculation**. Repeat this for purchasing in the **Purchases & Payables Setup**. For each area, decide whether **Fix Calculation Price** is activated.
2. **Master data (key user):** Using **Search**, open the **Sales Price Calculation List** and create a line for each combination of **Sales Type**, **Type**, **Sales Unit**, **Sales Calculation Unit**, and, if applicable, **Factor**. For purchasing, use the **Purchase Price Calculation List**.
3. **Enter document line (user):** In the **Sales Order** (or quote, invoice, purchase order, etc.), enter a line with an item and **Quantity**.
4. **Select calculation unit:** In the line's **Calculation Unit** field, open the lookup. If there is exactly one matching price calculation, it is applied automatically; if there are several, select the desired one in the **Sales Price Calculation List** that is shown.
5. **Check the result:** The system fills in **Calculation Quantity** and **Calculation Price** and derives from them the **Unit Price** or **Direct Unit Cost** of the line. You can overwrite the **Calculation Price** directly — the unit price is then recalculated in reverse.

This module has **no separate posting or release step**: price calculation acts on the document line; the document is then posted and released as usual via the standard actions of Business Central.

## Setup

Setup takes place in two existing, company-wide standard setup pages of Business Central, each of which this module extends by one field. Both pages are **global single-record pages** (one record per company) and are opened via **Search** — for sales via **Sales & Receivables Setup**, for purchasing via **Purchases & Payables Setup**.

### Activate the Price Calculation Method

**Entry point:** Using **Search**, open the **Sales & Receivables Setup** or the **Purchases & Payables Setup**.

**Process:** The administrator performs this setup once before first use. It determines whether Business Central uses the standard price calculation or the **m+m - Price Calculation** method when determining sales or purchase prices. Only with this method do the calculation fields in documents and price lists become effective; it is the prerequisite for all master data and daily processes in this guide (see **Master Data** and **Daily Work in Documents**).

| Setup | Explanation |
|-------------|-------------|
| **Price Calculation Method** | If **m+m - Price Calculation** is selected here, Business Central determines sales or purchase prices via this module's Sales/Purchase Price Calculation List; the document lines and price list lines then show the fields **Calculation Unit**, **Calculation Quantity**, and **Calculation Price** and convert the price per calculation unit into the unit price. If another value remains set, Business Central uses its standard price calculation and the additional fields have no effect. |

The value **m+m - Price Calculation** is the method added by this module; the other selectable methods are standard Business Central and are not changed here.

### Set Up Fix Calculation Price

**Entry point:** Using **Search**, open the **Sales & Receivables Setup** or the **Purchases & Payables Setup**. The **Fix Calculation Price** field is located directly after the **Price Calculation Method** field.

**Process:** The administrator sets this flag once per area (Sales, Purchasing). It controls the behavior when a user changes the **Calculation Unit** in a document line (see **Daily Work in Documents**). The setup therefore does not act on the setup page itself, but takes effect later when switching the calculation unit in each sales or purchase line.

| Setup | Explanation |
|-------------|-------------|
| **Fix Calculation Price** | If activated, the previously entered **Calculation Price** of a document line is retained when the user changes the **Calculation Unit** of the line: the remembered calculation price is reapplied to the new calculation unit and the unit price is redetermined from it. If not activated, the calculation price is discarded when the calculation unit is changed and is newly derived from the current unit price of the line. The administrative benefit: with the flag activated, manually specified calculation prices keep their value across a unit change and do not have to be re-entered. |

**Dependency:** Fix Calculation Price is only relevant if the **Price Calculation Method** was previously set to **m+m - Price Calculation**. The flag is maintained separately for Sales and Purchasing.

## Master Data

The actual calculation rules are maintained by a key user in two lists that serve as both master data and maintenance interface: the **Sales Price Calculation List** and the **Purchase Price Calculation List**. Both are opened via **Search**. Without at least one matching line in these lists, neither a calculation unit can be selected nor a calculation price displayed in a document line.

### Sales Price Calculation List

**Entry point:** Using **Search**, open the **Sales Price Calculation List**.

**Process:** The key user maintains this master data before the first price determination in sales and continuously thereafter. Each line defines for which **Sales Type** (reference point customer/customer group), for which **Type** of position (Item, G/L account, charge/allowance, etc.), and for which unit combination a price calculation applies. The lines maintained here are retrieved in day-to-day work via the **Calculation Unit** field of the sales line (see **Daily Work in Documents**) and also serve as the basis for the calculation columns in the sales price lists (see **Calculation in Price Lists**).

| Field | Explanation |
|------|-------------|
| **Sales Type** | Determines the reference point of the calculation. **Customer:** If selected, the line applies to a specific customer; the **Customer No.** field becomes mandatory. **All Customer:** If selected, the line applies across customers and **Customer No.** is omitted. **Customer Price Group:** If selected, the line applies to a price group; the **Customer Price Group** field becomes mandatory. |
| **Customer No.** | If the Sales Type is **Customer**, this field defines the specific customer for whom the calculation applies; only then is the field editable. For other sales types it is cleared when switching. |
| **Customer Price Group** | If the Sales Type is **Customer Price Group**, this field defines the price group whose customers the calculation applies to; only then is the field editable. |
| **Type** | Determines the position type to which the calculation is applied and which position identifier (**No.** or **Item Group**) is mandatory. **Item:** applies to a specific item (**No.** mandatory). **Item Group:** applies to a service item group (**Item Group** mandatory). **All Items:** applies to all items without further identifier. **Charge (Item):** applies to a specific item charge/allowance (**No.** mandatory, **Factor** mandatory). **All Charge (Item):** applies to all item charges/allowances (**Factor** mandatory). **G/L Account:** applies to a specific G/L account (**No.** mandatory, **Factor** mandatory). **All G/L Account:** applies to all G/L accounts (**Factor** mandatory). |
| **Item Group** | If **Type** is set to **Item Group**, this field defines the service item group for which the calculation applies. For other types it is cleared when switching. |
| **No.** | Identifier of the position according to the selected **Type**: for **Item** the item number, for **Charge (Item)** the number of the item charge/allowance, for **G/L Account** the G/L account number. It is cleared when the type is changed if the new type does not require a position number. |
| **Variant Code** | Optionally restricts the calculation to a specific item variant. If the field remains empty, the line applies across variants; if no variant-specific line is found during the lookup in the document line, the variant-neutral line applies. |
| **Sales Unit** | Base unit of measure of the sales line for which the calculation applies (mandatory field). Only if this unit matches the unit of the document line is the line recognized as matching. |
| **Sales Calculation Unit** | Unit in which the price is stated and calculated (mandatory field) — e.g. "L" (liter) if the price is kept per liter although sold in pieces. When the user selects this calculation unit in the document line, the system converts between the sales unit and the calculation unit. |
| **Factor** | Additional divisor for representing tiers such as "100/liter". When set, the calculation quantity is additionally divided by the factor; for **Charge (Item)** and **G/L Account** the factor is mandatory. Setting the factor clears the **Calculation Unit Base** and vice versa: calculation is done either with a factor **or** with a calculation unit base. |
| **Calculation Unit Base** | Base metric to which item- or group-related lines without a factor are converted. When filled, the calculation quantity is determined via the unit-of-measure conversion of this base unit; the field is mandatory as soon as a **Factor** other than 0 is missing and the type is not Charge/G/L Account. Factor and Calculation Unit Base are mutually exclusive. |
| **Default** | If activated, this line is used automatically in the document line as soon as exactly one default line exists for the combination — the user then does not have to select the calculation unit manually. Only **one** default line is permitted per combination of item and customer; when attempting to mark a second one as default, the system reports **"Only one Default allowed for this combination of Item and Customer"** and resets the flag. |

**Validations (from the program flow):** When creating, **Sales Unit** and **Sales Calculation Unit** are checked; depending on the **Sales Type**, either **Customer No.** or **Customer Price Group** is mandatory; depending on the **Type**, either **No.** or **Item Group** is mandatory. A line cannot be deleted while it is used in a price list line — the system then reports that a dependent price list entry exists.

### Purchase Price Calculation List

**Entry point:** Using **Search**, open the **Purchase Price Calculation List**.

**Process:** Analogous to the sales side, the key user maintains the calculation rules for purchasing here, related to vendors. The lines are retrieved in day-to-day work via the **Calculation Unit** field of the purchase line and supply the calculation columns of the purchase price lists.

| Field | Explanation |
|------|-------------|
| **Purchase Type** | Determines the reference point of the calculation. **Vendor:** If selected, the line applies to a specific vendor; **Vendor No.** becomes mandatory. **All Vendor:** If selected, the line applies across vendors and **Vendor No.** is omitted. |
| **Vendor No.** | If the Purchase Type is **Vendor**, this field defines the specific vendor; only then editable. When switching to another purchase type it is cleared. |
| **Type** | As in the Sales Price Calculation List: **Item** (No. mandatory), **Item Group** (Item Group mandatory), **All Items**, **Charge (Item)** (No. + Factor mandatory), **All Charge (Item)** (Factor mandatory), **G/L Account** (No. + Factor mandatory), **All G/L Account** (Factor mandatory). The selection controls which position identifier must be entered. |
| **Item Group** | Service item group for which the calculation applies when **Type** is set to **Item Group**. |
| **No.** | Position identifier according to **Type**: item number, number of the item charge/allowance, or G/L account number. |
| **Variant Code** | Optional restriction to an item variant; empty = across variants. |
| **Purchase Unit** | Base unit of measure of the purchase line for which the calculation applies (mandatory field). |
| **Purchase Calculation Unit** | Unit in which the purchase price is stated and calculated (mandatory field). |
| **Factor** | Additional divisor for tiers (e.g. "100/liter"); mandatory for **Charge (Item)** and **G/L Account**. Mutually exclusive with **Calculation Unit Base**. |
| **Calculation Unit Base** | Base metric for the conversion without a factor on item/group-related lines; mandatory if no factor is set and the type is not Charge/G/L Account. |
| **Default** | If activated, the line is used automatically in the purchase line, provided exactly one default line exists for the combination. Only one default line is permitted per combination of item and vendor; otherwise the system reports **"Only one Default allowed for this combination of Item and Vendor"**. |

The calculation quantity and the calculation price arise only in the document line or price list line — the price calculation lists define the rules exclusively.

### Explanation of the Calculation Steps

So that the master data is maintained correctly, here is the calculation path applied by the system (from the program flow), using the sales example; for purchasing it applies analogously with Direct Unit Cost instead of Unit Price:

- **Calculation quantity without factor:** The **Quantity** of the line (converted to base units) is divided by the quantity per unit of measure of the **Sales Calculation Unit** or the **Calculation Unit Base**. Example: a quantity of 10 with a conversion of 100 per unit results in a calculation quantity of 0.1.
- **Calculation price:** It is determined by multiplying the unit price by the quantity and dividing by the calculation quantity. Example: a unit price of 500 and a quantity of 10 result, with a calculation quantity of 0.1, in a calculation price of (500 × 10) / 0.1 = 50,000 per calculation unit.
- **Calculation quantity with factor:** If a **Factor** is set, the previously determined calculation quantity is additionally divided by the factor. Example: 0.1 divided by a factor of 100 results in a final calculation quantity of 0.001.
- **Reverse calculation:** If the user overwrites the **Calculation Price** directly, the **Unit Price** is conversely redetermined from the calculation price and the calculation quantity.

## Calculation in Price Lists

In addition to direct entry in documents, the price calculation can already be stored in the **price lists**. This module extends the lines of the sales and purchase price lists with calculation columns and hides the standard fields **Work Type Code**, **Minimum Quantity**, and (in sales) **Cost Factor**, since they are not combined with the calculation.

**Entry point:** Open the desired **price list** and work in the **Lines**. The calculation columns are available both in the editable price list lines and in the overview of the price list lines.

**Process:** The key user maintains the calculation once in the price list; the lines then take effect automatically when a document is priced via the standard price calculation using such a price list line. Here, too, the activated **m+m - Price Calculation** method is a prerequisite (see **Setup**).

| Field | Explanation |
|------|-------------|
| **Sales Type** / **Purchase Type** | Determines the reference point of the calculation line (Customer/All Customer/Customer Price Group or Vendor/All Vendor). When set, the system searches for the matching Sales/Purchase Price Calculation based on this reference point. |
| **Customer No.** / **Vendor No.** | Specific customer or vendor if the Sales/Purchase Type is set to **Customer** or **Vendor**. When the type is changed, the field is cleared. |
| **Customer Name** / **Vendor Name** | Display field: shows the name of the customer or vendor stored in the line for verification; not editable. |
| **Customer Price Group** | Price group if the Sales Type is set to **Customer Price Group**. |
| **Item Group** | Restricts the calculation line to a service item group. |
| **Calculation Unit** | Unit in which the price of the price list line is calculated. Via the lookup (drill-down) in the field, the system searches for matching price calculations; if none exists, it reports **"There are no Sales Price Calculations that match current line."** (or the purchase variant). After selection, the reference to the price calculation is set and the price is derived from it. |
| **Calculation Price** | Price per calculation unit for the price list line. When filled, the **Unit Price** or the **Direct Unit Cost** of the price list line is converted from it; conversely, when the unit price is changed, the calculation price is updated. |
| **Price Calc.** | Internal reference of the price list line to the Sales/Purchase Price Calculation used; set through the selection of the calculation unit and used for traceability. |

The calculation unit can only be selected and a price only displayed if a setup for the combination exists in the Sales/Purchase Price Calculation List.

## Daily Work in Documents

In day-to-day work, the module extends the lines of the sales and purchase documents with the fields **Calculation Unit**, **Calculation Quantity**, and **Calculation Price**. On the sales side, this affects quote, order, invoice, credit memo, return order, and blanket order; on the purchase side, request for quote, purchase order, invoice, credit memo, return order, and blanket order. All calculation fields are on the **line** (not in the header) and are available only when the **m+m - Price Calculation** method is activated (see **Setup**).

### Select Calculation Unit and Determine Price

1. Enter the document line with **Type**, **No.**, and **Quantity** as usual.
2. **Automatic application:** If exactly one matching line marked as **Default** exists in the Sales/Purchase Price Calculation List, the system fills in the **Calculation Unit** automatically as soon as the line is evaluated.
3. **Manual selection:** Otherwise, open the lookup in the **Calculation Unit** field. If there are several matching price calculations, the system shows the **Sales Price Calculation List** (or **Purchase Price Calculation List**) for selection; with exactly one line, it is applied directly. If the system finds no matching line, the message **"There are no Sales Price Calculations that match current line."** appears.
4. The system then fills in **Calculation Quantity** and **Calculation Price** and converts the **Unit Price** or the **Direct Unit Cost** of the line.
5. **Override calculation price:** You can enter the **Calculation Price** directly (this requires a filled calculation unit, otherwise the system reports **"Enter a Calculation Unit to be able to fill in the Calculation Price field."**). The unit price is then redetermined in reverse from your calculation price.

**Interaction with Fix Calculation Price:** If you change the **Calculation Unit** of a line again, the behavior depends on the setup flag **Fix Calculation Price** (see **Setup**): if it is activated, the previously entered calculation price is remembered and applied to the new calculation unit; if it is not activated, the calculation price is discarded and newly derived from the current unit price.

| Field (document line) | Explanation |
|-------------------|-------------|
| **Calculation Unit** | Unit in which the price of this line is calculated. Via the lookup, you select the applicable price calculation; the change resets **Calculation Quantity** and **Calculation Price** and redetermines them. Changing is only possible while the document has the status **Open**. |
| **Calculation Quantity** | Quantity in the calculation unit, determined from the document quantity and the conversion; display field, not directly editable. It is the reference value for the calculation price. |
| **Calculation Price** | Price per calculation unit. When you enter it, the unit price of the line is recalculated from it; it is only editable if a calculation unit is set, and only when the document status is **Open**. |

### Item Tracking and Recalculation

When you open and close the **Item Tracking Lines** in sales or purchase order lines, the module then automatically updates the calculation quantity and the price of the line so that the price calculation matches the tracked quantity. No additional step is required by the user.

## Archive and Posted Documents

The calculation fields are archived and posted together with the document and are available for tracing — however, **read-only**, since no prices can be changed on an archived or posted document.

- **Archived documents:** In the archived sales and purchase orders as well as quotes, the lines show **Calculation Unit**, **Calculation Quantity**, and **Calculation Price** in the state in which the document was archived.
- **Posted documents:** In the posted sales and purchase invoices as well as credit memos, the lines likewise show **Calculation Unit**, **Calculation Quantity**, and **Calculation Price** — as a record of how the document was calculated at the time of posting.

## Permissions

For use of the module, the application provides the permission set **MuM Price Calc. Per**. It defines which actions users may perform in price calculation: it grants read and write access (view, create, modify, delete) to the tables of the **Sales Price Calculation** and **Purchase Price Calculation** as well as execution rights on the associated processing objects and the two price calculation lists. The administrator assigns this permission set to the users who are to maintain price calculation lists or work with the calculation fields in documents.

## FAQ and Troubleshooting

### 1. Why do the Calculation Unit and Calculation Price fields not appear in my document lines?
The additional fields take effect only if the **Price Calculation Method** is set to **m+m - Price Calculation** in the **Sales & Receivables Setup** or **Purchases & Payables Setup**. Without this method, Business Central uses the standard price calculation and the calculation has no effect.

### 2. Why does the system report "There are no Sales Price Calculations that match current line"?
For the combination of customer/customer group, type, item/G/L account, unit, and, if applicable, variant, there is no matching line in the **Sales Price Calculation List**. Create a corresponding line there or extend an existing one via **All Customer** or **All Items** so that the lookup finds a match.

### 3. Why can I not enter the Calculation Price?
The **Calculation Price** can only be filled if a **Calculation Unit** was selected beforehand. Otherwise the system reports **"Enter a Calculation Unit to be able to fill in the Calculation Price field."** Select the calculation unit first.

### 4. Why does the unit price change when I overwrite the Calculation Price?
This is intentional: the **Unit Price** or the **Direct Unit Cost** is back-calculated from the calculation price and the calculation quantity. This lets you work with the price per calculation unit without having to convert the unit price manually.

### 5. Why is the Calculation Price sometimes kept and sometimes not when the Calculation Unit is changed?
This is controlled by the setup flag **Fix Calculation Price**. If it is activated, the previous calculation price is applied to the new calculation unit; if it is deactivated, it is discarded and newly derived from the current unit price.

### 6. Why can a line in the price calculation list not be deleted?
A price calculation line cannot be deleted while it is used in a **price list line**. The system points out the dependent price list entry. Remove or change the relevant price list line first.

### 7. Why does the system report "Only one Default allowed for this combination of Item and Customer"?
Per combination of sales type, customer, type, item/group, variant, and unit, only **one** line may be marked as **Default**, so that the automatic application is unambiguous. The flag is reset automatically on a second default. In purchasing, this applies to the combination of item and vendor.

### 8. What is the Factor for, and why may I not set Factor and Calculation Unit Base together?
The **Factor** represents tiers such as "100/liter" by additionally dividing the calculation quantity by it. **Calculation Unit Base** instead defines a base unit of measure for the conversion. The two paths are mutually exclusive: setting the factor clears the Calculation Unit Base and vice versa.

### 9. Why is a list shown when there are several matching calculations?
If there is more than one matching price calculation, the system cannot decide on its own and shows the **Sales**/**Purchase Price Calculation List** for selection. Mark the desired line as **Default** if it should be applied automatically in the future.

### 10. Why do calculation fields change after I have opened the Item Tracking Lines?
After editing the **Item Tracking Lines**, the module recalculates the calculation quantity and the price of the line automatically so that the price calculation matches the tracked quantity. This is an intended reconciliation and requires no further step.

## Typical Use Cases

### Use Case 1: Sale with a price per liter although sold in pieces

**Trigger:** A customer orders 10 containers of an item by phone; the item is managed internally in pieces but calculated per liter.

**Entry in BC:** The user opens the **Sales Order** and enters the item with **Quantity** 10 in the **Lines**.

**Core flow:** If a Sales Price Calculation marked as **Default** exists, the system fills in the **Calculation Unit** (e.g. "L") automatically. Otherwise the user opens the lookup in the **Calculation Unit** field and selects the matching line from the **Sales Price Calculation List** that is shown. The system determines the **Calculation Quantity** via the unit-of-measure conversion and sets the **Calculation Price** per liter; the **Unit Price** of the line is derived from it. The user can adjust the calculation price per liter directly — the unit price is then recalculated.

**Completion:** The order is then processed further and posted as usual via the standard actions of Business Central; the calculation fields appear read-only in the posted invoice.

### Use Case 2: Set the sales price only in the invoice

**Trigger:** The final sales price is not established until invoicing and should not be fixed in the order yet.

**Entry in BC:** The user opens the **Sales Invoice** and works in the **Lines**.

**Core flow:** In the invoice line, the user selects the applicable price calculation in the **Calculation Unit** field and enters the **Calculation Price** per calculation unit. The system computes the **Unit Price** of the line from it. If **Fix Calculation Price** is activated in the **Sales & Receivables Setup**, a calculation price once entered is retained even if the calculation unit is later changed again.

**Completion:** The invoice is posted via the standard actions; **Calculation Unit**, **Calculation Quantity**, and **Calculation Price** are documented with the posted invoice.

### Use Case 3: Purchase price in a "100/liter" tier

**Trigger:** A vendor quotes its price per 100 liters, while the item is ordered in a different unit.

**Entry in BC:** The key user stores a line in the **Purchase Price Calculation List** with **Purchase Type** = **Vendor**, the matching **Purchase Unit**, the **Purchase Calculation Unit**, and a **Factor** of 100 (in combination with the **Calculation Unit Base** "L"). The buyer then opens the **Purchase Order**.

**Core flow:** In the order line, the buyer selects the **Calculation Unit**; the system additionally divides the calculation quantity by the factor of 100 and thus determines the price per 100 liters. The **Direct Unit Cost** of the line arises from **Calculation Price** and **Calculation Quantity**.

**Completion:** The order is processed further via the standard actions of Business Central; the calculation fields are available in posted and archived purchase documents for traceability.
