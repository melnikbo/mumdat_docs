---
title: Anwenderhandbuch m+m Subcontracting Prices with Price Calculation
---

# User Guide m+m Subcontracting Prices with Price Calculation

## Introduction

The m+m "Subcontracting Prices with Price Calculation" app is a connector app for Microsoft Dynamics 365 Business Central. It links the two base apps m+m "Subcontracting Prices" and m+m "Price Calculation" and extends the subcontracting prices by a **Calculation Unit** and a **Calculation Price**. As a result, a stored subcontracting price can be maintained not only per base unit of measure, but additionally per freely chosen calculation unit (for example per 100 pieces, per liter, or per kilogram) and converted automatically.

The business benefit: as soon as a vendor calculates its subcontracting prices in a unit of measure different from the one in which the item is maintained, the app reliably converts the price to the base unit of measure. In the subcontracting documents — in the **Prod. Order Routing** of the released production order, in the **Subcontracting Worksheets**, and in the **Purchase Order** generated from them — the calculation unit and the price per calculation unit are carried along, and the direct unit cost is derived automatically from the subcontracting price that was found.

**Target audience.** This guide is aimed primarily at **operational users** who work with subcontracting on a daily basis: production planning and purchasing, who process released production orders, work through subcontracting worksheets, and generate purchase orders for subcontract work. Secondarily, it addresses **administrators and master data owners** who set up the prerequisites (flag the work center group for subcontracting, maintain subcontracting prices with a calculation unit).

**Brief process overview.** The flow follows this chain: a **Work Center Group** is flagged for subcontracting and assigned to a **Vendor** → a price with a **Calculation Unit** and a **Calculation Price** is stored in the **Subcontracting Prices** → in the **released production order** the user uses this work center group in the **Prod. Order Routing** → the system automatically pulls the matching subcontracting price, transfers the calculation unit and the price per calculation unit, and calculates the direct unit cost → the **Purchase Order** is created from the **Subcontracting Worksheet** with the same values.

**Prerequisite (installation).** As its base installation, this connector app requires the apps m+m "Subcontracting Prices" and m+m "Price Calculation" as well as m+m "Cloud Base". Without these base apps, the fields and processes described here are not available.

## Quick Start for Users

The quick start describes the shortest path from a configured system to an automatically determined subcontracting price. The setup steps deliberately come before the daily work, because without them no price is pulled.

1. **Check the setup (one-time, by the administrator).** Open the **Work Center Group Card** of the relevant work center group, enter the associated **Vendor**, and flag the work center group for subcontracting (activation of the specific unit cost at the work center). When the work center group is flagged in this way, the system does not use the normal purchase price during price determination, but the price stored for this work center group in the subcontracting prices.
2. **Maintain the subcontracting price with a calculation unit.** From the **Vendor Card**, open the **Related** menu item and then **Subcontracting Prices**. Enter a line with **Work Center Group No.**, **Item**, **Unit of Measure**, and **Price**. Additionally select the **Calculation Unit**; the **Calculation Price** is then calculated automatically (see the chapter *Master Data*).
3. **Open the released production order.** Open the **released production order** for the configured item and call the **Routing** action via **Line**. This opens the **Prod. Order Routing**.
4. **Use the work center group.** In the operation line, use the work center group flagged for subcontracting. The system automatically pulls the matching subcontracting price and fills the **Calculation Unit** and **Price per Calculation Unit** fields in the line; the direct unit cost is derived from the price that was found.
5. **Turn subcontracting into a purchase order.** Use the search to open the **Subcontracting Worksheets**. First have the subcontracting demand calculated and then carry out the action message proposed in the worksheet. A **Purchase Order** is created in which the **Calculation Unit** and **Price per Calculation Unit** are taken over from the demand line.

Further steps, all fields, and the conversion logic are described in the following chapters.

## Setup

This app does **not** come with its own setup page. It extends existing pages of the base apps by two fields and derives the price automatically through events. The prerequisites for the automatic subcontracting price are therefore configured in the base apps. For the calculation per calculation unit to take effect, the steps described below must be completed in dependency order.

### Setting up the calculation unit for subcontracting prices

**Process introduction.** This setup is performed by the **administrator** or a master data owner **before first use**. It activates the central capability of this app: maintaining and automatically converting a subcontracting price per calculation unit. The configured values are later used by the operational users in the chapter *Daily Work in the Prod. Order Routing*. The steps build on one another — first the work center group, then the subcontracting price, and finally the effect in the document.

**Numbered setup steps (in dependency order):**

1. **Flag the work center group for subcontracting.** Open the **Work Center Group Card**, enter the associated **Vendor**, and flag the work center group for subcontracting (specific unit cost at the work center). When the work center group is flagged in this way, the system does not use the standard purchase price for this work center group during price determination, but exclusively the prices stored in the subcontracting prices — without this flag the subcontracting price is not taken into account and the calculation unit of this app does not take effect.
2. **Prepare the calculation unit in the purchase price calculation.** The selectable calculation units come from the **Purchase Price Calculation** of the m+m "Price Calculation" app (the purchase price calculation table per vendor and item). When a **Purchase Calculation Unit** is set up there for the combination of vendor and item, it is available for selection in the subcontracting prices; without this entry, no valid selection is possible in the **Calculation Unit** field.
3. **Enter the subcontracting price with a calculation unit and calculation price.** Open the subcontracting prices via **Vendor Card → Related → Subcontracting Prices** and enter a price line (see the field table in the chapter *Master Data*). When you select a **Calculation Unit** and a **Price** is set, the system calculates the **Calculation Price** automatically; conversely, when you change the **Calculation Price**, the **Price** per base unit of measure is adjusted automatically.

**Operational conclusion.** The setup takes effect in daily operations when the user uses the corresponding work center group in the **Prod. Order Routing** of the released production order (see the chapter *Daily Work in the Prod. Order Routing*). From that point on, the system automatically pulls the matching subcontracting price including the calculation unit and calculates the direct unit cost.

## Master Data

The subcontracting prices are the central master data of this app. They are provided by the base app m+m "Subcontracting Prices"; this connector app extends them by the **Calculation Unit** and **Calculation Price** fields, as well as by the automatic conversion between **Price** and **Calculation Price**.

### Subcontracting Prices

**Process introduction.** The subcontracting prices are maintained by the **master data owner** per vendor. They define which price applies to the combination of work center group, standard task code, item, and quantity. The easiest access is via **Vendor Card → Related → Subcontracting Prices**. The values maintained here control the later automatic price determination in the Prod. Order Routing and in the subcontracting worksheet (see the chapters *Daily Work* and *Automatic Price Derivation*).

**Field table (base fields of the base app and additional fields of this app on the same page):**

| Field | Explanation |
|---|---|
| Purchase Type | When "All Vendors" is selected, the price line applies to all vendors; when "Vendor" is selected, it applies only to the vendor specified in the line. This selection directly controls which price lines the system takes into account during the automatic determination in the Prod. Order Routing. |
| Vendor No. | When a vendor is entered, the price line is bound to exactly this subcontractor; the system only pulls it if the work center group is assigned to the same vendor. |
| Vendor Name | Is filled automatically after selecting the Vendor No. and serves for unambiguous assignment in the list; manual maintenance is not required. |
| Work Center Group No. | Binds the price line to a work center group. When this work center group is used in the Prod. Order Routing, exactly this price line is used for price determination. |
| Reference Type | When "All Standard Task Codes" is selected, the line applies to every operation; when "Standard Task Code" is selected, it applies only to the code specified in the line. This lets you control whether the price applies as a flat rate or per specific operation. |
| Standard Task Code | When a standard task code is entered, the line is only pulled for operations with exactly this code; this allows different subcontracting operations to be priced differently. |
| Definition Type | When "All Items" is selected, the price applies regardless of item; when "Item" is selected, it applies only to the item specified in the line. This lets you separate general from item-specific subcontracting prices. |
| Item | When an item is entered, the price line applies only to production orders for this item; empty, in combination with "All Items", means the price applies to every item. |
| Unit of Measure | Defines the base unit of measure to which the **Price** field refers. This unit of measure is the reference point for the later conversion into the calculation unit. |
| Minimum Amount | When the amount calculated from Price × Quantity falls below the minimum amount, the minimum amount is applied as a flat rate. This ensures that small quantities are never billed below an agreed base amount. Per work center group and standard task code, the minimum amount can only be assigned once. |
| Minimum Quantity | Defines the minimum quantity from which the price of this line applies. When you create several lines with different minimum quantities per work center group and standard task code, they form a price scale from which the system selects the matching price for the production quantity. |
| Price | Defines the price per **Unit of Measure** for the combination of work center group, standard task code, and quantity. When you change the price and a calculation unit is set, the system automatically recalculates the **Calculation Price**. |
| Starting Date | When a date is set, the price line applies only from this date; during determination, the system only takes into account lines whose validity includes the work date. |
| Ending Date | When a date is set, the price line loses its validity afterward; expired lines are no longer pulled during the automatic determination. |
| Calculation Unit | Defines which item unit of measure is used for calculating the price. When you select a calculation unit, the system automatically calculates the **Calculation Price** from the **Price** and the quantity ratios of the units of measure, and carries both values into the subcontracting documents. The selection is made from the purchase price calculation of the m+m "Price Calculation" app for the vendor and item. |
| Calculation Price | Shows the price per **Calculation Unit**. When you change this value manually, the system automatically recalculates the **Price** per base unit of measure, so that both price figures always remain consistent. |

**Conversion logic (validation note).** The conversion between **Price** and **Calculation Price** is performed via the "quantity per unit of measure" ratio of the two item units of measure involved (unit of measure and calculation unit). If no item unit of measure is stored for one of the two units, the conversion is skipped and the calculation price remains 0. It is also a prerequisite that a calculation unit is set up in the purchase price calculation for the combination of vendor and item.

### Subcontracting Prices FactBox

**Process introduction.** For a quick visual check, the base app provides a FactBox in the Prod. Order Routing with the stored subcontracting prices. This connector app extends the FactBox by the **Calculation Unit**, so that the user already recognizes in the operation line which calculation unit the displayed price refers to.

| Field | Explanation |
|---|---|
| Calculation Unit | Shows in the FactBox the item unit of measure to which the calculation price of the displayed subcontracting price line refers. When the user reads the FactBox, they recognize — without switching to the subcontracting prices — in which calculation unit the price was calculated. |

## Daily Work in the Prod. Order Routing

Daily work builds on the values maintained in *Setup* and *Master Data*: as soon as the work center group is flagged for subcontracting and a subcontracting price with a calculation unit exists, the system fills the additional fields automatically. Here the user maintains no prices, but uses the prepared work center group and checks the result.

### Prod. Order Routing (operation lines)

**Entry:** Open the **released production order** and call the **Prod. Order Routing** via **Line → Routing**.

When the user uses the work center group flagged for subcontracting in the operation line, the system automatically determines the matching subcontracting price and fills the following fields:

| Field | Explanation |
|---|---|
| Calculation Unit | Shows the calculation unit taken over from the subcontracting price that was found. When the system finds a matching price, it enters the calculatory unit here, so that the origin of the price per calculation unit remains traceable. |
| Price per Calculation Unit | Shows the price calculated per calculation unit from the subcontracting price that was found. From this value and the production quantity, the system derives the direct unit cost of the operation line; this amount feeds into the calculation of the production order. |

**Note on the automatic determination.** The system only takes into account operations of type Work Center Group whose work center group is flagged for subcontracting (specific unit cost at the work center). From all valid price lines (validity period includes the work date, minimum quantity less than or equal to the production quantity), the system selects the cheapest and takes the **Minimum Amount** into account as a lower limit. For details see the chapter *Automatic Price Derivation*.

### Subcontracting Worksheets

**Entry:** Use the search to open the **Subcontracting Worksheets**.

The subcontracting worksheets transfer the subcontracting demand of a production order into a purchase order. This connector app extends the lines by the same calculation fields as the Prod. Order Routing, so that the calculation unit is retained consistently all the way into the purchase order.

| Field | Explanation |
|---|---|
| Calculation Unit | Shows the calculation unit derived from the subcontracting price for the demand line. When a purchase order is later generated from this line, the calculation unit is taken over unchanged into the purchase line. |
| Price per Calculation Unit | Shows the price calculated per calculation unit for the demand line. From it, the direct unit cost of the later purchase line is derived, so that the calculation remains consistent from planning through to the purchase order. |

**Process steps up to the purchase order:**

1. Open the **Subcontracting Worksheets** via the search.
2. Have the subcontracting demand to be processed calculated; the system fills the demand lines and, in doing so, determines the **Calculation Unit** and **Price per Calculation Unit** via the subcontracting prices.
3. If required, set a filter on the record to be processed and carry out the proposed action message. A **Purchase Order** is created; the record then disappears from the worksheet.
4. In the new **Purchase Order**, the **Calculation Unit** and **Price per Calculation Unit** are taken over from the demand line; the direct unit cost results from the subcontracting price that was found divided by the quantity.

## Automatic Price Derivation

This chapter describes the core logic of the app, so that users can follow the automatic behavior and classify deviations. The user does not trigger this logic via a dedicated button; it takes effect automatically as soon as a subcontracting price is required.

**Price determination (finding the subcontracting price).** For an operation of type Work Center Group, the system first checks whether the work center group is flagged for subcontracting (specific unit cost at the work center). Then all lines from the subcontracting prices are collected that match the work center group, whose validity period includes the work date, and whose **Minimum Quantity** does not exceed the production quantity. In doing so, the combinations of **Purchase Type** (All Vendors / Vendor) and **Reference Type** (All Standard Task Codes / Standard Task Code) are taken into account, so that both general and specific price lines are included. From the matching lines, the system selects the cheapest; if the amount calculated from Price × Quantity falls below the **Minimum Amount**, the minimum amount is applied.

**Effect in the documents.** The price that was found takes effect in three places:

- In the **Prod. Order Routing**, the system sets the **Calculation Unit**, **Price per Calculation Unit**, and the direct unit cost (price found divided by the production quantity) in the operation line.
- In the **Purchase Order** created from the subcontracting worksheet, the calculation unit and price per calculation unit are taken over, and the direct unit cost is derived from the price found divided by the order quantity.
- In the **demand line** of the subcontracting worksheet, the same values are set, so that they are passed on unchanged when the purchase order is created.

**Reciprocal conversion Price ⇄ Calculation Price.** In the subcontracting prices, **Price** (per base unit of measure) and **Calculation Price** (per calculation unit) are linked to each other via the quantity ratio of the item units of measure. When the user changes the **Price** or the **Calculation Unit**, the calculation price is recalculated; when they change the **Calculation Price**, the price per base unit of measure is calculated back. In this way, both price figures always remain free of contradiction.

## FAQ and Troubleshooting

### 1. Why does the calculation price in the subcontracting prices stay at 0?

Because no item unit of measure is stored for the **Unit of Measure** or the **Calculation Unit**. The conversion uses the "quantity per unit of measure" ratio of both units of measure; if one of them is missing, the calculation aborts and the calculation price remains 0. Maintain both item units of measure on the item.

### 2. Why can I not select a unit in the Calculation Unit field?

Because no calculation unit is set up for the combination of **Vendor** and **Item** in the purchase price calculation of the m+m "Price Calculation" app. The selection list draws its values from this purchase price calculation; without a matching entry, no selection is possible.

### 3. Why is no subcontracting price pulled in the Prod. Order Routing?

Because the relevant **Work Center Group** is not flagged for subcontracting (specific unit cost at the work center not set). Without this flag, the system uses the standard purchase price and ignores the subcontracting prices. Flag the work center group accordingly on the work center group card.

### 4. What happens if the production quantity is smaller than every minimum quantity?

Then the system finds no matching price scale and determines no subcontracting price for this line. Create a price line with a **Minimum Quantity** that is less than or equal to the planned production quantity.

### 5. Why is a higher amount applied than Price × Quantity?

Because the calculated amount falls below the stored **Minimum Amount**. In this case, the system applies the minimum amount as a flat rate, so that small quantities are not billed below the agreed base amount.

### 6. By what criterion does the system select from several valid price lines?

The system collects all matching lines (Purchase Type, Reference Type, validity, minimum quantity) and selects the **cheapest** from them. The minimum amount is then taken into account as a lower limit.

### 7. Why does the price also change when I change the calculation price?

Because **Price** and **Calculation Price** are firmly coupled via the quantity ratio of the units of measure. A change to the calculation price automatically recalculates the price per base unit of measure, so that both values remain consistent. This is intentional.

### 8. Are the calculation unit and price per calculation unit taken over into the purchase order?

Yes. When the order is generated from the subcontracting worksheet, the system transfers the **Calculation Unit** and **Price per Calculation Unit** from the demand line unchanged into the purchase line; the direct unit cost is derived from the price found divided by the order quantity.

### 9. Why does the FactBox show a different calculation unit than expected?

Because the FactBox shows the calculation unit of the subcontracting price line that was actually pulled. When several price scales exist, a line other than the assumed one may be the cheapest. Check the price lines in the subcontracting prices for the relevant work center group.

### 10. Do I have to enter the prices manually during daily work?

No. During daily work, you only use the prepared work center group; the system fills the **Calculation Unit**, **Price per Calculation Unit**, and the direct unit cost automatically. The prices are maintained once in the subcontracting prices.

## Typical Use Cases

### Use Case 1: Store a new subcontracting price per calculation unit and use it in the production order

**Trigger.** A subcontractor reports a new framework price by phone for a subcontracting operation, which it calculates per 100 pieces, while the item is maintained in the system in pieces.

**Entry in BC.** The master data owner opens the **Vendor Card** of the subcontractor and calls the subcontracting prices via **Related → Subcontracting Prices**.

**Core flow.** They enter a price line with **Work Center Group No.**, **Item**, **Unit of Measure** (pieces), and **Price**. As the **Calculation Unit**, they select the 100-pieces unit; the system then automatically calculates the **Calculation Price**. If required, they create further lines with different **Minimum Quantity** to represent a price scale, and store a **Minimum Amount** as a base amount. The prerequisite is that the work center group is assigned to the vendor on the **Work Center Group Card** and flagged for subcontracting (specific unit cost at the work center; see the chapter *Setup*).

**Conclusion.** Afterward, production planning opens the **released production order**, calls the **Prod. Order Routing** via **Line → Routing**, and uses the work center group. The system fills the **Calculation Unit** and **Price per Calculation Unit** and derives the direct unit cost. In the FactBox, the subcontracting price used can be checked.

### Use Case 2: Turn subcontracting into a purchase order via the worksheet

**Trigger.** For a released production order, a subcontracting step is due, for which a purchase order is to be generated at the subcontractor.

**Entry in BC.** Purchasing uses the search to open the **Subcontracting Worksheets**.

**Core flow.** By calculating the subcontracting demand, the system displays the subcontracting to be processed. In the demand lines, the **Calculation Unit** and **Price per Calculation Unit** are already filled from the previously found subcontracting price. The user sets a filter on the desired record if required.

**Conclusion.** By carrying out the proposed action message, the system generates the **Purchase Order**; the processed record disappears from the worksheet. In the order, the **Calculation Unit** and **Price per Calculation Unit** are taken over from the demand line, and the direct unit cost results from the price found divided by the order quantity. Thus, the subcontracting is ordered with the correctly converted price.
