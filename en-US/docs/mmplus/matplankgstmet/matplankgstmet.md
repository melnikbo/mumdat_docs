---
title: Anwenderhandbuch m+m Material Planning with Unit Conversion
---

# User Guide m+m Material Planning with Unit Conversion

## Introduction

The **m+m Material Planning with Unit Conversion** app connects m+m material planning with KG / Meter / Piece unit conversion. It adds four extra columns to the **Material Planning Lines** – **Actual Planning UOM**, **Actual Planning KG**, **Actual Planning Meter** and **Actual Planning Piece** – and automatically calculates these values from the **Actual Planning Quantity** that has already been entered. When the requisition lines are created, the app passes the selected unit of measure to the requisition line.

The app has **no pages, setup pages or reports of its own**. It only extends the material planning lines of the **m+m Material Planning** app and uses the conversion logic and setup of the **m+m Unit Conversion** app. Without these two apps the function cannot be used.

**Target audience.** The primary users are **operational planners and buyers** who set order quantities in material planning every day and pass them into the requisition worksheet. For them it is essential to be able to enter an order quantity in the unit they think in (e.g. meters of a coil) while the system derives the remaining units and the actual order quantity from it. The secondary target group are **administrators and master data owners** who set up the unit codes and the conversion factors per item once.

**Process overview and typical entry point.** The user opens the **Material Planning List**, selects a planning record and opens the **Material Planning** page. There they calculate the planning, which opens the **Material Planning Lines**. In the lines they enter the desired quantity at item level – either as **Actual Planning Quantity** or via one of the unit columns **Actual Planning KG / Meter / Piece** – and then create the **requisition lines**. Prerequisites for the conversion are the one-time setup of the unit codes (**KG Meter Piece Setup**) and the conversion factors on the **Item Card**.

## Quick start for users

The fastest path from setup to a finished requisition. The order follows the technical dependency: first the setup, then the master data, then the daily work.

1. **Set up the unit codes (once, administrator).** Use **Tell Me** to open the **KG Meter Piece Setup** page and enter **KG Unit of Measure Code**, **Meter Unit of Measure Code** and **Piece Unit of Measure Code**. Only then does the system know which units correspond to the base measure KG, Meter or Piece.
2. **Maintain the conversion factors on the item (master data).** Open the **Item Card** of the relevant item and, in the **Factors:** area, enter the values **Theoretical KG per Meter** and/or **Theoretical KG per Piece**. Without these factors the system cannot convert between the units.
3. **Open the planning.** Use **Tell Me** to open the **Material Planning List** and open the **Material Planning** page by selecting a line.
4. **Calculate the planning.** Choose the **Calculate Planning** action. The system fills the **Planning Quantity** and opens the **Material Planning Lines**.
5. **Enter the quantity.** In the planning lines, enter the order quantity at item level – either in **Actual Planning Quantity** or in one of the columns **Actual Planning KG**, **Actual Planning Meter** or **Actual Planning Piece**. If required, change the **Actual Planning UOM**. All values are converted to one another.
6. **Create the requisition.** Choose **Create Requisition Lines**. For every line with a quantity greater than zero a requisition line is created; the **Actual Planning UOM** is taken over as the **Unit of Measure Code**. Use **Show Requisition Lines** to check the result.

## Setup

The app itself does not come with a setup page. The configuration required for the conversion is done entirely in the **m+m Unit Conversion** app and must be completed before it is first used in planning.

### KG Meter Piece Setup

**Process intro.** The administrator defines this company-wide setup once, before the conversion is used in production. It assigns a specific Business Central unit of measure code to each of the three logical reference quantities KG, Meter and Piece. Only this assignment enables material planning to allocate an entered quantity to the correct reference quantity and to convert it. The values set here take effect later in the **Material Planning Lines** (section *Daily work*).

**Entry point:** Use **Tell Me** to open the **KG Meter Piece Setup** page.

| Setup | Explanation |
|---|---|
| **KG Unit of Measure Code** | If you enter the unit of measure code for kilograms here, the system recognizes items with this base unit as weight-managed; only then are the KG values converted in the planning lines and filled into **Actual Planning KG**. Without an entry, no KG conversion takes place. |
| **Meter Unit of Measure Code** | If you enter the unit of measure code for meters, the system treats items with this base unit as length-managed and calculates **Actual Planning Meter** from the quantity and the **Theoretical KG per Meter** factor. Without an entry the Meter column remains unconverted. |
| **Piece Unit of Measure Code** | If you enter the unit of measure code for pieces, the system treats items with this base unit as piece-managed and calculates **Actual Planning Piece** via the **Theoretical KG per Piece** factor. Without an entry the Piece conversion is omitted. |

**Dependency note.** The conversion takes effect for an item only if its **Base Unit of Measure** matches one of the three unit of measure codes entered here. If an item's base unit is not assigned to any of these three quantities, the app does not fill the unit columns in the planning lines.

### Setting up unit conversion for material planning

This function – entering order quantities in KG, Meter or Piece and automatically converting them into the planning and order quantity – requires several steps that build on one another across different pages. They are described below in dependency order.

**Process intro.** Responsibility lies with the administrator (global setup) together with the master data owner (item factors). The setup must be completed before the first planning run. The result is applied in the **Material Planning Lines** (section *Daily work*), where the planner uses the converted values.

1. **Assign the unit codes.** First, in the **KG Meter Piece Setup**, enter the **KG / Meter / Piece Unit of Measure Code** (see above). Once this assignment is set, the system recognizes which items can be converted at all.
2. **Maintain the conversion factors per item.** Then, on the **Item Card** in the **Factors:** area, enter the values **Theoretical KG per Meter** and/or **Theoretical KG per Piece** (see chapter *Master data*). If a factor is set, the system can convert between KG and Meter or KG and Piece; if it is missing, the affected conversion has no effect.
3. **Define the quantity behavior per item.** On the Item Card, in the **Qty. Consistency:** area, use the **Qty. Consistency Conf.** field to define whether and how quantities may be adjusted automatically (see *Master data*).
4. **Use the conversion in day-to-day work.** Finally, the planner enters the quantity in one of the unit columns in the **Material Planning Lines** and creates the requisition with **Create Requisition Lines** – this closes the chain (see *Daily work*).

**Operational conclusion.** The configuration chain ends in the **Create Requisition Lines** action in the planning lines: there, the selected **Actual Planning UOM** is taken over as the **Unit of Measure Code** in the requisition line.

## Master data

### Item Card: conversion factors and quantity consistency

**Process intro.** The master data owner maintains these values per item as soon as an item is to be planned by weight, length or piece – ideally when the item is created, at the latest before the first planning. The factors are the calculation basis, without which the unit columns in the **Material Planning Lines** remain empty. They are evaluated in material planning (chapter *Daily work*).

**Entry point:** Open the **Item Card** of the item (open the line from the item list) and switch to the **Factors:** and **Qty. Consistency:** areas.

| Field | Explanation |
|---|---|
| **Theoretical KG per Meter** | If you enter the weight per meter here, the system can calculate the corresponding **Actual Planning KG** in the planning lines from a length entered in **Actual Planning Meter** and vice versa. If the value is zero, the KG/Meter conversion is omitted for this item. |
| **Theoretical KG per Piece** | If you enter the weight per piece, the system converts between **Actual Planning Piece** and **Actual Planning KG**. If the value is zero, the KG/Piece conversion is omitted. |
| **Qty. Consistency Conf.** | Defines how the system adjusts the quantities during a conversion. The effect of each option: see the list below. |

Meaning of the **Qty. Consistency Conf.** values:

- **Always Change Quantity:** If this value is set, the system adjusts the dependent quantities on every conversion without prompting – the planner immediately receives consistent KG, Meter and Piece values.
- **Never Change Quantity:** If this value is set, the system does not change existing quantities automatically; discrepancies between the units remain until the user corrects them.
- **Change Quantity On Confirm:** If this value is set, the system asks before an automatic quantity adjustment and only changes the quantity after confirmation by the user.

**Note on actual factors.** For the conversion the system primarily uses a stored actual factor (**Actual KG per Meter** or **Actual KG per Piece**), provided it is greater than zero for the record; otherwise the theoretical factor from the Item Card applies. In the planning lines these actual and theoretical factors are carried along but shown as non-editable.

## Daily work in the Material Planning Lines

In the **Material Planning Lines** the planner enters the quantity that actually needs to be ordered. Here the app adds the conversion into KG, Meter and Piece. The lines are not opened via **Tell Me**, but from within the planning.

**Controlling setup.** The columns described in this section are controlled by the **KG Meter Piece Setup** (which units count as KG/Meter/Piece) and by the factors on the **Item Card** (conversion factors, quantity consistency). If one of these prerequisites is not met, the unit columns remain without values (see chapters *Setup* and *Master data*).

**Entry point:** Open the **Material Planning** page (from the **Material Planning List**) and choose **Calculate Planning**; the **Material Planning Lines** then open. Alternatively, open the lines via the corresponding action on the Material Planning page.

The app inserts the following columns after **Actual Planning Quantity**:

| Field | Explanation |
|---|---|
| **Actual Planning UOM** | If you choose a unit of the item here, it defines the unit in which the order quantity is managed; the system later passes exactly this unit as the **Unit of Measure Code** to the requisition line. When a new line is created, the item's purchase unit of measure is prefilled. |
| **Actual Planning KG** | If you enter a weight here, the system recalculates **Actual Planning Meter**, **Actual Planning Piece** and the **Actual Planning Quantity** based on the stored factors and thereby determines the actual order quantity. |
| **Actual Planning Meter** | If you enter a length here, the system determines the corresponding KG via **Theoretical KG per Meter** and the **Actual Planning Quantity** via the base unit; this lets the planner think in meters even though the item is managed in, for example, KG. |
| **Actual Planning Piece** | If you enter a number of pieces here, the system converts it via **Theoretical KG per Piece** into KG and into the **Actual Planning Quantity**; the order is thus created from a piece specification. |

**Interaction with the base column.** The app is closely interlocked with the base column **Actual Planning Quantity**: any change to **Actual Planning Quantity**, to one of the three unit quantities, or to the **Actual Planning UOM** triggers a recalculation of the respective other values. What matters for the subsequent order remains the **Actual Planning Quantity** in the selected **Actual Planning UOM**.

**Default prefill on creation.** When a planning line is created automatically, the app sets the **Actual Planning UOM** to the unit stored as the purchase unit of measure on the item. As a result, the requisition is created in the usual purchase unit without any further action.

### Creating the requisition and passing on the unit

From the planning lines the planner creates the requisition lines. This flow corresponds to the material planning standard; the app only intervenes in the unit of measure.

1. Select one or more lines at item level in the **Material Planning Lines**.
2. Enter the order quantity via **Actual Planning Quantity** or one of the unit columns.
3. Choose the **Create Requisition Lines** action. For every line with a quantity greater than zero a requisition line is created; the **Actual Planning UOM** is taken over as the **Unit of Measure Code**.
4. Check the result via **Show Requisition Lines**.

## Typical use cases

### Use case 1: Entering a coil order in meters

1. **Trigger.** Purchasing reports that an aluminum coil needs to be reordered. The item is managed in KG in the warehouse, but the planner thinks in running meters.
2. **Entry point in BC.** The planner uses **Tell Me** to open the **Material Planning List**, opens the relevant **Material Planning** page and chooses **Calculate Planning**. The **Material Planning Lines** open.
3. **Core flow.** In the item line the planner checks that the **Actual Planning UOM** is set correctly. They enter the required length in **Actual Planning Meter**. The system calculates the **Actual Planning KG**, the **Actual Planning Piece** and the **Actual Planning Quantity** via **Theoretical KG per Meter**. This requires that the Meter unit is set in the **KG Meter Piece Setup** and that the factor is maintained on the **Item Card**.
4. **Conclusion.** The planner chooses **Create Requisition Lines**; the requisition line is created with the inherited **Actual Planning UOM** as the **Unit of Measure Code**. With **Show Requisition Lines** they verify the lines created.

### Use case 2: Regular planning with a prefilled purchase unit

1. **Trigger.** In the weekly planning run, new planning lines are created for several items.
2. **Entry point in BC.** After **Calculate Planning**, the **Material Planning Lines** open with the newly determined items.
3. **Core flow.** For every newly created line the **Actual Planning UOM** is already prefilled with the item's purchase unit of measure. The planner enters the desired quantity in **Actual Planning Quantity**; the unit columns **Actual Planning KG / Meter / Piece** are carried along automatically – as far as factors are available.
4. **Conclusion.** Via **Create Requisition Lines**, all lines with a quantity greater than zero are transferred into requisition lines, each in the prefilled unit.

## FAQ and troubleshooting

### 1. Why do the columns Actual Planning KG / Meter / Piece stay empty?
The conversion only takes effect if the item's **Base Unit of Measure** matches one of the unit of measure codes (KG, Meter or Piece) entered in the **KG Meter Piece Setup**. If the base unit is not assigned to any of these quantities, the app does not fill the columns.

### 2. What happens if no conversion factor is set on the Item Card?
Without **Theoretical KG per Meter** or **Theoretical KG per Piece** the calculation basis is missing. The affected conversion is omitted and the corresponding unit column remains without a value.

### 3. Which unit ends up in the requisition line?
When you run **Create Requisition Lines**, the app takes over the **Actual Planning UOM** of the planning line as the **Unit of Measure Code** of the requisition line. So change the unit already in the planning lines, not only in the requisition afterwards.

### 4. Why is the Actual Planning UOM already filled on creation?
When a planning line is created automatically, the app sets the **Actual Planning UOM** to the unit stored as the purchase unit of measure on the item, so that the requisition is created in the usual purchase unit without any further action.

### 5. How are Actual Planning Quantity and the unit columns related?
All values are coupled: a change to **Actual Planning Quantity** or to **Actual Planning KG / Meter / Piece** or to the **Actual Planning UOM** triggers a recalculation of the respective other values. What matters for the order is the **Actual Planning Quantity** derived from them.

### 6. Can I still enter the quantity the classic way in Actual Planning Quantity?
Yes. You can still enter the quantity in **Actual Planning Quantity** unchanged; the unit columns are then derived from it automatically – as far as factors are available. The app does not force an entry in KG, Meter or Piece.

### 7. Why do quantities sometimes change automatically and sometimes only after a prompt?
This is controlled by the **Qty. Consistency Conf.** field on the Item Card: **Always Change Quantity** adjusts quantities without prompting, **Never Change Quantity** changes nothing automatically, **Change Quantity On Confirm** asks before every adjustment.

### 8. Why can't I edit the Theoretical/Actual KG per Meter fields in the planning lines?
These factors are taken from the master data (item or item tracking information) and are only carried along for traceability. They are not editable in the lines; change the theoretical values on the **Item Card**.

### 9. Which lines does the quantity entry affect?
The order quantity is entered at item or item variant level. Only at this lowest level are the quantities editable; higher levels (material type, property) show cumulated values.

### 10. No requisition lines are created – why is that?
**Create Requisition Lines** only considers lines with an **Actual Planning Quantity** greater than zero. If no quantity has been entered – not even indirectly via a unit column – no requisition line is created.
