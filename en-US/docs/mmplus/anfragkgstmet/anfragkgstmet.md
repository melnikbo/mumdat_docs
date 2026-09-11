---
title: Anwenderhandbuch m+m Purchase Quote Manager with Unit Conversion
---

# User Guide m+m Purchase Quote Manager with Unit Conversion

## Introduction

The **m+m Purchase Quote Manager with Unit Conversion** app connects two existing m+m extensions: the **m+m Purchase Quote Manager** (purchase quote and campaign management) and the **m+m Unit Conversion** (conversion between **KG**, **Meter** and **Piece**). The app adds three additional quantity fields to the **Campaign Items** of a purchase quote campaign – **KG**, **Meter** and **Piece** – and automatically keeps these fields in sync with the base quantity.

As soon as a user changes the **Quantity**, the quantities in **KG**, **Meter** or **Piece**, or the **item** in a campaign line, the app recalculates the remaining quantity fields using the conversion factors stored for the item. This lets the buyer, working on a purchase quote campaign for a steel or coil item, see at the same time how much **weight (KG)**, what **length (Meter)** and what **piece count** correspond to a recorded quantity, without having to do the calculation manually.

**Target audience:** This guide is aimed primarily at **operational purchasing users** who record item quantities in purchase quote campaigns every day and prepare quote requests to vendors. **Administrators** and **master data owners** are the secondary audience: they set up the factors required for the conversion on the item, without which the three new fields remain empty.

**Brief process overview:** The administrator maintains the conversion factors **Theoretical KG per Meter** and **Theoretical KG per Piece** on the item one time (in the **m+m Unit Conversion** app). After that, in day-to-day work, the buyer adds the **Campaign Items** of a purchase quote campaign and enters one of the quantities **Quantity**, **KG**, **Meter** or **Piece**; the app calculates the remaining values automatically.

This app is a **bridge app**: it has no setup pages of its own and no list or card pages of its own. Its entire visible functionality consists of the three fields on the **Campaign Items** page of the m+m Purchase Quote Manager. The setup required for it is done entirely in the two dependent modules.

## Quick Start for Users

The fastest path from a configured item to a fully populated purchase quote campaign line with KG, Meter and Piece quantities:

1. **Check the setup (administrator, one time):** Make sure that the factors **Theoretical KG per Meter** and/or **Theoretical KG per Piece** are stored on the item (see the chapter *Setup: Setting up conversion factors on the item*). Without these factors, **KG**, **Meter** and **Piece** remain empty.
2. **Open the purchase quote campaign:** Open the desired campaign of the m+m Purchase Quote Manager and open its **Campaign Items**.
3. **Choose the item:** Enter the **Item No.** in a new line. If the item is set up for unit conversion, the app takes over the item's theoretical factors.
4. **Record one quantity:** Enter **one** of the values **Quantity**, **KG**, **Meter** or **Piece**.
5. **Wait for automatic conversion:** The app fills the other of the three fields **KG**, **Meter** and **Piece** using the item's theoretical factors and updates the **Quantity** in the base unit of measure.
6. **Check and save the line:** Review the calculated values and continue with quote processing in the m+m Purchase Quote Manager.

If **no** conversion factors are set up for the item, the campaign line behaves as in the standard m+m Purchase Quote Manager: no conversion takes place, and the three additional fields remain empty.

## Setup

The **m+m Purchase Quote Manager with Unit Conversion** app comes with **no setup page of its own**. For the automatic conversion to take effect, the two dependent modules must be set up: the **m+m Unit Conversion** (conversion factors on the item and module-wide unit of measure codes) as well as the **m+m Purchase Quote Manager** (purchase quote campaigns). This chapter describes the settings required for the conversion in **dependency order**: first the module-wide unit of measure codes, then the factors per item.

### Activate unit conversion and set up conversion factors on the item

**Who sets this up and when:** This setup is performed by the **administrator** or the **master data owner** – one time module-wide before first use, and thereafter per item for which KG/Meter/Piece are to be used in purchase quote campaigns. The values maintained here are later consumed in day-to-day work on the **Campaign Items** page (see the chapter *Daily Work: Campaign Items with KG, Meter and Piece*).

**Process steps in dependency order:**

1. **First – store module-wide unit of measure codes:** Open the **KG Meter Piece Setup** page of the m+m Unit Conversion. Define which **unit of measure code** in Business Central stands for **KG**, for **Meter** and for **Piece** respectively. Once this assignment is set, the system can recognize which base unit of measure of an item corresponds to which of the three quantities, and perform the conversion at all.
2. **Then – enter theoretical factors per item:** Open the **Item Card** of the item concerned and enter the factors **Theoretical KG per Meter** and/or **Theoretical KG per Piece**. If only **one** of the two factors is set, then only the conversion between those two units of measure is possible; the other unit of measure remains empty in the campaign line. If **both** factors are set, then all three fields KG, Meter and Piece are calculated in the campaign line. If **no** factors are set, then all three fields remain empty in the campaign line and no conversion takes place.
3. **Finally – apply in day-to-day work:** Once the factors are maintained, the conversion takes effect automatically when a buyer records the item in a purchase quote campaign (see *Daily Work: Campaign Items with KG, Meter and Piece*).

**Settings for the theoretical factors:**

| Setting | Explanation |
|-------------|-------------|
| Theoretical KG per Meter | Indicates how many KG theoretically correspond to one meter for this item. If set, the app can calculate the associated weight in KG from a recorded Meter quantity (and vice versa); if the factor is empty, the **Meter** field in the campaign line has no relation to the weight and is not populated. |
| Theoretical KG per Piece | Indicates how many KG theoretically correspond to one piece for this item. If set, the app can calculate the associated weight in KG from a recorded piece count (and vice versa); if the factor is empty, the **Piece** field in the campaign line has no weight relation and is not populated. |

**Dependency note:** The app performs a conversion only if the item is set up for it according to the m+m Unit Conversion. If the item is not set up, the app does not intervene and the campaign line behaves as in the standard m+m Purchase Quote Manager. It is therefore mandatory to maintain first the unit of measure codes and then the item factors before the three fields are used in the purchase quote campaign.

## Master Data

The app creates **no master data of its own** and does not extend any master data card with visible fields. It builds entirely on the master data of the dependent modules:

- **Item** (m+m Unit Conversion): carrier of the conversion factors **Theoretical KG per Meter** and **Theoretical KG per Piece** as well as the **Base Unit of Measure**. These factors are the functional basis of every calculation in the purchase quote campaign. Maintenance is described in the chapter *Setup*.
- **Purchase quote campaign and Campaign Items** (m+m Purchase Quote Manager): the campaign bundles the items for which quote requests to vendors are prepared. The app extends the **Campaign Items** with the three quantity fields; the handling is described in the following chapter.

No dedicated master data maintenance screen results from this app.

## Daily Work: Campaign Items with KG, Meter and Piece

The only user interface changed by this app is the **Campaign Items** page of the m+m Purchase Quote Manager. There, the app adds the three fields **KG**, **Meter** and **Piece** in the **General** area. These three fields are controlled by the item's conversion factors described in the chapter *Setup*; without these factors they remain empty.

**Getting started:** Open the desired purchase quote campaign in the m+m Purchase Quote Manager and open its **Campaign Items**. The three fields appear on the same line as the base fields of the campaign line (among others **Item No.**, **Quantity** and **Description**).

### Fields of the campaign line (added by this app)

The following table describes the quantity fields **added** by this app on the **Campaign Items** page. The remaining fields of the line (such as **Item No.**, **Quantity**, **Description**, **Variant Code**) come from the m+m Purchase Quote Manager and retain their standard behavior there; for the conversion, the three following fields as well as **Item No.** and **Quantity** are decisive.

| Field | Explanation |
|------|-------------|
| KG | Weight quantity of the line in kilograms. If you enter a value here, the app recalculates the associated **Meter** and **Piece** using the item's theoretical factors and then adjusts the **Quantity** in the base unit of measure. If the item is not set up for unit conversion, the field remains empty and has no effect. |
| Meter | Length quantity of the line in meters. If you enter a value here, the app recalculates the associated weight in **KG** using the factor **Theoretical KG per Meter** as well as – provided the Piece factor is set – the **Piece**, and adjusts the **Quantity**. If no Meter factor is stored on the item, the field remains empty. |
| Piece | Piece quantity of the line. If you enter a value here, the app recalculates the associated weight in **KG** using the factor **Theoretical KG per Piece** as well as – provided the Meter factor is set – the **Meter**, and adjusts the **Quantity**. If no Piece factor is stored on the item, the field remains empty. |

**Interaction with the base fields:**

- **Item No.:** If you set or change the item in the line and the item is set up for unit conversion, the app takes over the item's theoretical factors, resets the actual factors and calculates KG, Meter and Piece to match the **Quantity** already recorded.
- **Quantity:** If you change the **Quantity** in the base unit of measure, the app recalculates the three fields KG, Meter and Piece from this quantity (provided the item is set up).

### Sequence of the automatic conversion

The conversion runs without an additional button, directly when you leave the changed field. The sequence is always the same:

1. **Trigger:** You change one of the fields **Item No.**, **Quantity**, **KG**, **Meter** or **Piece** in the campaign line.
2. **Check of the setup:** The app checks whether the item is set up for conversion according to the m+m Unit Conversion. If it is not, the app aborts and the line remains unchanged in its standard behavior.
3. **Determine factors:** The app reads the theoretical factors stored on the item (**Theoretical KG per Meter**, **Theoretical KG per Piece**). An actual factor stored on the record takes precedence over the theoretical one; if no actual factor is present, the app uses the theoretical value.
4. **Calculation:** Starting from the changed field, the app calculates the other of the three quantities KG, Meter and Piece.
5. **Adjust quantity:** Finally, the app updates the **Quantity** in the base unit of measure so that the base quantity and the three additional fields remain consistent.

Because the conversion is triggered field-based, it is enough to record **one** of the quantities; the app fills the rest. If you enter several fields one after another, each entry starts a new calculation based on the most recently changed field.

## FAQ and Troubleshooting

### 1. Why do the KG, Meter and Piece fields in the campaign line remain empty?
Because the item is not set up for unit conversion. The app only performs a calculation if the m+m Unit Conversion factors are stored on the item. Check the values **Theoretical KG per Meter** and **Theoretical KG per Piece** on the **Item Card**.

### 2. Why is only one of the three additional quantities filled and the others remain empty?
Because only **one** of the two factors is set on the item. If only **Theoretical KG per Meter** is stored, the app can only convert between KG and Meter; the **Piece** field remains empty. If only **Theoretical KG per Piece** is stored, the reverse applies. For all three fields, both factors must be maintained.

### 3. What happens if I change the quantity in the base unit of measure?
The app recalculates the values for **KG**, **Meter** and **Piece** from the new **Quantity** using the item's theoretical factors, provided the item is set up. This keeps the base quantity and the additional quantities consistent.

### 4. What happens if I enter a KG value directly?
The app calculates back from the entered **KG** value to **Meter** and **Piece** and then adjusts the **Quantity** in the base unit of measure. This lets you record a line in a weight-oriented way as well, without first knowing the piece count.

### 5. Do I have to press a button to start the conversion?
No. The conversion is performed automatically when you leave the changed field (**Item No.**, **Quantity**, **KG**, **Meter** or **Piece**). This app has no action or dialog of its own.

### 6. Which field takes precedence when several quantity fields contain values?
The **most recently changed** field is always decisive. The app calculates the remaining quantities from this field. If you enter values one after another, each new entry overwrites the previously calculated values.

### 7. Why do calculated values occasionally differ slightly from a manual calculation?
The app uses the theoretical factors stored on the item and the rounding rules and rounding precisions set in the m+m Unit Conversion. Small deviations from an unrounded manual calculation result from these rounding settings.

### 8. Why do I not see fields for the theoretical or actual KG factors in the campaign line?
These factor fields are maintained at the data level but are **not** shown in the campaign line. On the **Campaign Items** page, the app displays only the three quantity fields **KG**, **Meter** and **Piece**. You maintain the factors on the **Item Card**.

### 9. Does the conversion also apply to items without a KG relation?
No. For items without stored KG factors, the app does not intervene. Such items behave unchanged in the purchase quote campaign, as in the standard m+m Purchase Quote Manager.

### 10. What should I do if nothing is calculated at first after installation?
Check in this order: first, whether the unit of measure codes for KG, Meter and Piece are set in the **KG Meter Piece Setup**; second, whether the theoretical factors are stored on the item concerned; third, whether the recorded item really is this set-up item. Only when the unit of measure codes and item factors are present does the app fill the three quantity fields.

## Typical Use Cases

The following scenarios show the use of the app in the context of purchase quote processing. Each screen and each quantity comes from the **Campaign Items** page of the m+m Purchase Quote Manager; the calculation is performed using the factors of the m+m Unit Conversion.

### Use Case 1: Record a quote request for coil material by weight

1. **Trigger:** A supplier reports available coil quantities for a steel item by phone. The buyer is to prepare a purchase quote campaign for this and record the quantities in a weight-oriented way.
2. **Getting started in BC:** The buyer opens the relevant purchase quote campaign in the m+m Purchase Quote Manager and opens the **Campaign Items**.
3. **Core sequence:** In a new line, they enter the **Item No.** of the coil item; the app takes over the item's theoretical factors. Then they record the weight named by the supplier in the **KG** field. From this the app calculates the associated **Meter** and **Piece** and adjusts the **Quantity** in the base unit of measure.
4. **Completion:** The buyer checks the calculated values and continues quote processing in the m+m Purchase Quote Manager. No posting or document of its own results from this app.

### Use Case 2: Report a requirement in pieces, determine the weight automatically

1. **Trigger:** A requirement for a certain **piece count** of a long-product item comes in by email from production. However, the weight is needed for the quote request to the vendor.
2. **Getting started in BC:** The buyer opens the matching purchase quote campaign and its **Campaign Items**.
3. **Core sequence:** They record the **Item No.** and enter the reported piece count in the **Piece** field. Using the factor **Theoretical KG per Piece**, the app calculates the weight in **KG** and – provided the Meter factor is maintained on the item – the **Meter**; the **Quantity** in the base unit of measure is also updated.
4. **Completion:** The buyer uses the calculated KG values for further quote and price clarification in the m+m Purchase Quote Manager.

### Use Case 3: Clarify a missing conversion on a line

1. **Trigger:** A buyer notices that for a newly recorded item the **KG**, **Meter** and **Piece** fields remain empty, even though they have entered a quantity.
2. **Getting started in BC:** They stay on the **Campaign Items** at first and then open the **Item Card** of the item concerned.
3. **Core sequence:** On the Item Card they find that the factors **Theoretical KG per Meter** and **Theoretical KG per Piece** are not maintained. The master data owner adds the factors; in addition, it is checked whether the unit of measure codes are set in the **KG Meter Piece Setup** (see the chapter *Setup*).
4. **Completion:** Back on the **Campaign Items**, the buyer records the quantity again; the app now fills the three quantity fields correctly.
