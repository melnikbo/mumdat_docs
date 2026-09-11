---
title: Anwenderhandbuch m+m Wire Rope Configurator
---

# User Manual m+m Wire Rope Configurator

## Introduction

The **m+m Wire Rope Configurator** extends the production objects of Microsoft Dynamics 365 Business Central with a rope configuration. From a rope length in sales, a simulated production order is created together with its **Prod. Order Routing** and its **Prod. Order Components**; the module calculation derives from these the number of coils, the required single strand length, the installation frequency, the remaining meters, and the component quantities to be produced.

For the calculation to take effect, administration sets the **Is Wire Rope** flag on the **routing**, maintains the rope parameters (strands, wires, factors) on the **routing lines** and the **production BOM lines**, and enters the **Setup Length In Meter** and the **Max. Coil Weight** on the **work center**. In day-to-day operations the user records the **Pass Lengths** on the **sales order** and starts the **Prod. Assistant**.

**Target group.** The primary target group are the **operational users** who record rope lengths in the sales order, run the Prod. Assistant, and trigger the rope calculation in the production order. Secondarily, the manual addresses **production preparation and administration**, who set up routings, production BOMs, work centers, and production campaigns as rope.

**Process overview.** The user's path follows this chain: **master data and rope setup** (work center, routing, routing lines, production BOM lines) → **sales order** with recording of the **Pass Lengths** → **Prod. Assistant** creates the simulated production order → **Recalculate Wire Rope** determines the rope values → optional transfer into the source document. In addition, the **production campaign** distributes the **Wire Setup Length** across the contained production orders during release.

## Quick start for users

The quick start lists the minimal steps in dependency order. Setup comes before the daily work, because the rope calculation does not compute without the rope flag and the setup data.

1. **First**, open the **work center** and, on the Scheduling tab, enter the **Setup Length In Meter** and the **Max. Coil Weight** (see *Setup*).
2. **Then**, open the **routing**, set the **Is Wire Rope** flag on the **General** tab, and maintain the rope parameters on the **routing lines** (among others **Amount Of Strands**, **Helixfactor for Rope**, **Safety Factor**, **Target Quantity**) (see *Master data*).
3. On the **production BOM lines**, enter the component parameters (**Amount Of Strands**, **Amount Of Wire**, **Quantity Factor**, **Offcut Factor**, **Helix Factor per Strand**).
4. In the **sales order**, select the relevant line and choose the **Pass Lengths** action from the **Line** menu; for each section, record **Sequence**, **Meter**, and **Number**. The header shows **Order Meter**, **Total Meter**, and **Remaining Meter**.
5. **Finally**, on the same sales order line, choose the **Prod. Assistant** action. The module creates one production order line per pass length, reserves against the sales line, and opens the Prod. Assistant. There, run **Recalculate Wire Rope** so that coils, single strand length, installation frequency, and component quantities are calculated.

> Note: If a sales line has no pass lengths, the system asks **"It does not exist Pass Lengths. Do you want to continue?"**. Confirm only if the order should continue without pass lengths.

## Setup

The setup of the module is spread across a few clearly separated areas: the **setup data on the work center**, the **rope flag of the routing**, and — for campaign-driven production — the **Wire Setup Length of the production campaign**. The rope parameters at routing and BOM level are master data and are described in the chapter *Master data*.

### Setup data on the work center

**Entry point:** Open the relevant **work center** (Work Center Card) and switch to the Scheduling area.

Process intro: These fields are maintained once per work center by **production preparation**, before the first rope order is calculated. The values are the physical basis of the coil and setup length calculation: the **Max. Coil Weight** limits how much rope may be wound per coil, and the **Setup Length In Meter** flows into the routing line as a default value on transfer. The values are later evaluated in the **Prod. Assistant** via **Recalculate Wire Rope**.

| Setup | Explanation |
|-------------|-------------|
| **Setup Length In Meter** | When a value is set, this meter value is automatically defaulted as the **Setup Length In Meter** of the line when a routing line with this work center is created; this means the setup length does not have to be recorded manually per operation and enters the calculation of the quantity to be produced and the component demand consistently. |
| **Max. Coil Weight** | When a weight is set, the rope calculation uses this limit to determine **Number of lengths per coil** and **Amount Of Coils**; if the weight is 0, the Max. Coil Weight of the subsequent work center is used instead, so that the coil calculation does not run empty. A higher limit results in fewer but heavier coils. |

The transfer of the setup length into the routing line happens automatically as soon as a work center is set in the routing line. Further use is described in the section *Recalculate Wire Rope* (chapter *Daily work*).

### Setting up a routing as rope

Process intro: This setup chain prepares an item so that a calculable rope production order arises from its sale. It is run by **production preparation** before the first rope order and processed in this dependency order. The operational closure of this chain — the actual calculation — happens later in day-to-day operations via **Recalculate Wire Rope** (see *Daily work*).

1. **First**, set the **Setup Length In Meter** and the **Max. Coil Weight** on the **work center** (see *Setup data on the work center*). If these values are missing, the coil and setup length calculation cannot deliver meaningful quantities.
2. **Then**, open the **routing** and set the **Is Wire Rope** flag on the **General** tab. When activated, the routing is treated as a rope routing: the routing lines are sorted by the **Wire Rope Sequence**, the rope parameters become mandatory to maintain, and the **Recalculate Wire Rope** action computes for this order. The flag cannot be set while the routing has the Certified status; set it before certification.
3. **Then**, maintain the rope parameters per operation on the **routing lines** (see *Master data → Routing lines*). Without a set **Wire Rope Sequence**, a rope routing line cannot be saved.
4. **Then**, maintain the component parameters on the **production BOM lines** (see *Master data → Production BOM lines*), so that the component quantities can be calculated.
5. **Finally**, the operational closure happens in the sales order: record **Pass Lengths**, start the **Prod. Assistant**, and run **Recalculate Wire Rope** (see *Daily work*).

### Setting up the Wire Setup Length in the production campaign

**Entry point:** Open the relevant **production campaign** (card) and work on the **General** tab as well as in the ribbon.

Process intro: This setup concerns operations that bundle rope production orders in a **production campaign**. It is maintained by production control before the campaign release. The operational closure is the **release of the campaign**: the centrally maintained **Wire Setup Length** is distributed proportionally across the setup lengths of the participating production orders, and the affected orders are recalculated.

| Setup | Explanation |
|-------------|-------------|
| **Is Wire Rope** | When activated, the campaign counts as a rope campaign; the **Wire Setup Length** field becomes editable and the proportional setup length distribution on release becomes effective for this campaign. The flag is set automatically when processing the campaign lines as soon as a rope routing with a setup length is contained; it is not manually editable. All contained production orders must carry the same rope flag, otherwise processing aborts with an error message. |
| **Wire Setup Length** | When a value is set, release distributes this total setup length proportionally across the **Setup Length In Meter** of the operations of all campaign orders and then recalculates these orders; this allows the setup length to be controlled centrally over the entire campaign, instead of maintaining it individually per order. The field is only editable when **Is Wire Rope** is set, and may only be changed in the Open status. |

Numerical steps of setup and closure:

1. **First**, fill the campaign with its rope production orders and process it; the system sets **Is Wire Rope** and sums the setup lengths of the contained rope operations into the **Wire Setup Length**.
2. **Then**, if needed, have the currently summed total setup length of the campaign recalculated via the ribbon action (only possible in the Open status). This action re-reads the setup lengths of the campaign orders and writes them into the **Wire Setup Length**.
3. **Finally**, **release** the campaign. If the new **Wire Setup Length** differs from the previously distributed total, the system distributes the difference proportionally across the setup lengths of the participating operations and recalculates the affected production orders.

## Master data

The rope master data lies in three areas: the **routing** (rope flag), the **routing lines** (rope calculation per operation), and the **production BOM lines** (component parameters). They are maintained by production preparation and directly control what the Prod. Assistant calculates in day-to-day operations.

### Routing — Is Wire Rope flag

**Entry point:** Open **Routings**, select the routing, and work on the **General** tab.

Process intro: The rope flag is the central switch of the module. It decides whether a routing is calculated as rope, and controls the sorting and the maintenance obligations of the routing lines. It is set before certification and evaluated in the sales order as well as in the Prod. Assistant.

| Field | Explanation |
|------|-------------|
| **Is Wire Rope** | When activated, the routing is run as a rope routing: the routing lines are sorted by the **Wire Rope Sequence**, the rope parameters of the lines are checked and become mandatory to maintain, and the **Recalculate Wire Rope** action computes for orders of this routing. Without the flag, the routing remains a standard routing without rope calculation. The flag cannot be set if the routing is already certified. |

### Routing lines — rope parameters per operation

**Entry point:** Open the **routing** and switch to the **Lines** (routing lines).

Process intro: On the routing lines of a rope routing, production preparation stores the geometric and quantity-related key values per operation. These values are the input variables of the rope calculation; several fields already compute dependent values on entry (e.g. **Qty. To Produce**, **Coil Length**, **Total Wire**). For rope routings the lines are sorted by the **Wire Rope Sequence**. Every rope routing line must have a **Wire Rope Sequence**, otherwise it cannot be saved.

| Field | Explanation |
|------|-------------|
| **Wire Rope Sequence** | When set, this value determines the processing and display order of the rope operations; for a rope routing the entry is mandatory, because the lines are sorted by this key and the subsequent operations are derived from it. |
| **Setup Length In Meter** | When set, this meter value enters the **Qty. To Produce** and the **Required Component Setup Length** as a fixed setup share; it is defaulted from the work center's setup length when the work center is set and can be overridden per operation. |
| **Helixfactor for Rope** | When set, this factor multiplies the order length to obtain the required single strand length and the quantity to be produced; it represents the lay elongation of the rope. A higher factor increases the calculated strand length. |
| **Production Quantity Factor** | When set, this factor indicates the ratio of the quantity to be produced to the **Target Quantity**; it is determined automatically from **Qty. To Produce** and **Target Quantity** and serves the back-calculation of the production quantity. |
| **Required Component Setup Length** | When calculated, this field shows the setup length of the components attributable to the operation (Setup Length In Meter multiplied by the number of coils); it makes the setup share of the material demand visible. |
| **Theor. Weight per Coil** | When set, this is the calculated weight of a coil; the coil calculation compares it with the **Max. Coil Weight** of the work center to determine the **Amount Of Coils**. |
| **Amount Of Coils** | When calculated, this field indicates the number of required coils; it results from the theoretical coil weight, the strand count, and the **Max. Coil Weight** and controls the **Coil Length**. |
| **Coil Length** | When calculated, this is the length per coil (**Qty. To Produce** divided by **Amount Of Coils**); it is automatically updated when the quantity or coil count changes. |
| **Amount Of Strands** | When set, this is the number of strands of the rope; it enters the quantity to be produced multiplicatively and — together with **Amount Of Wire Per Strands** — the **Total Wire**. |
| **Amount Of Wire Per Strands** | When set, this value together with **Amount Of Strands** determines the **Total Wire**; it describes the strand structure. |
| **Total Wire** | When calculated, this is the product of **Amount Of Strands** and **Amount Of Wire Per Strands**; the field is not editable and serves as a control value of the wire structure. |
| **Qty. To Produce** | When calculated, this is the rope quantity to be produced per operation; it results from the coil count, **Helixfactor for Rope**, **Target Quantity**, and the setup share and is not directly editable. It is the reference value of the component back-calculation. |
| **Target Quantity** | When set, this is the target quantity of the operation; entering it triggers the recalculation of **Production Quantity Factor** and **Qty. To Produce**. It is the user's controlling quantity target. |
| **Safety Factor** | When set, this factor reduces the permissible load per coil in the calculation of the **Number of lengths per coil**; a higher safety factor leads to shorter coils and thus to more coils and higher process reliability. |

> Calculated fields such as **Qty. To Produce**, **Coil Length**, and **Total Wire** are read-only or are updated automatically; they are documented here so that the user can interpret the displayed values.

### Production BOM lines — component parameters

**Entry point:** Open the **production BOM** and switch to the **Lines**.

Process intro: On the production BOM lines, production preparation describes how a component enters the rope. These values are transferred to the **Prod. Order Components** when the production order is built and there determine, via the rope calculation, the **Quantity per** of the component. The **Quantity Factor** is defaulted from the item's theoretical weight per meter when an item is selected.

| Field | Explanation |
|------|-------------|
| **Amount Of Strands** | When set, this indicates with how many strands the component enters the rope; the value is transferred to the prod. order component and enters the **Strand weight** and the component quantity. |
| **Amount Of Wire** | When set, this describes the wire count of the component; together with the **Quantity Factor** it determines the strand weight of the operation and the calculated component quantity. |
| **Quantity Factor** | When set, this factor weights the component in the quantity calculation; it is defaulted from the item's theoretical weight per meter on item selection, so that the material quantity is consistent without manual entry. |
| **Offcut Factor** | When set, this factor accounts for the material offcut of the component; it increases the calculated material demand according to the expected waste. |
| **Helix Factor per Strand** | When set, this factor represents the lay elongation of the strand and enters the calculated **Quantity per** of the component multiplicatively. A higher factor increases the material demand per meter of rope. |

## Daily work — Sales order, Pass Lengths, and Prod. Assistant

These chapters describe the operational core of the module. The actions used here presuppose the rope data described in the chapters *Setup* and *Master data*: the routing must carry **Is Wire Rope**, the routing and BOM parameters must be maintained, and the work center must contain **Setup Length In Meter** and **Max. Coil Weight**. If these are missing, **Recalculate Wire Rope** does not deliver meaningful quantities.

### Entry via the sales order

**Entry point:** Open the **sales order**, select the order line, and use the **Pass Lengths** and **Prod. Assistant** actions in the line menu **Line**.

Both actions are anchored on the sales order line. The **Pass Lengths** action is only active as long as the line has an open remaining quantity. The **Pass Lengths** page is not reachable via **Search**; it opens exclusively from this line action.

### Recording Pass Lengths

Process intro: In the **Pass Lengths** entry, the user breaks the order length down into individual rope sections. Each section carries a **Sequence**, a length in **Meter**, and a **Number** (number of identical sections). The header of the page continuously reflects how much of the order length is already planned.

| Field | Explanation |
|------|-------------|
| **Order Meter** | Shows the total meters of the source document line; serves as the target value against which the recorded pass lengths are reconciled. The field is not editable. |
| **Total Meter** | Shows the sum of **Meter** × **Number** across all recorded pass lengths; increases with each recorded line and represents the length already planned. |
| **Remaining Meter** | Shows the difference **Order Meter** − **Total Meter**; if the value is 0, the order length is fully broken down into pass lengths. A positive value means length not yet planned, a negative value means over-planning. |
| **Sequence** | When set, this value determines the sequence of the pass length; a drilldown on this field opens — if a production order has already been created — the Prod. Assistant for the associated order line and marks the pass length after processing as **Assistant Prepared**. |
| **Meter** | When set, this is the length of a section; on entry the line is saved and **Total Meter**/**Remaining Meter** are recalculated. |
| **Number** | When set, this is the number of equally long sections; together with **Meter** it results in the **Total Meter** of the line. |
| **Assistant Prepared** | Indicates whether the pass length has already been processed via the Prod. Assistant; the field is set by the system and is only visible in the guided assistant view. |

When closing the entry, the system checks open items:

- If the guided view is confirmed with OK and there are still unprocessed pass lengths, **"It exists not prepared Pass Length Lines. Do you want to continue?"** appears.
- If the sum of the pass lengths differs from the **Order Meter**, the system offers to update the source document: **"The Remaining Quantity is different from the Source Document Quantity. … Do you want to update the Source Document?"**. Confirm if the sales line should be adjusted to the actually planned length.

A safeguard takes effect when changing the sales quantity: if the sum of the pass lengths exceeds the quantity of the sales line, the system reports **"The Pass Length cannot be greater then the Quantity … . Please Update the Pass Length before."**. In this case, adjust the pass lengths first.

### Starting the Prod. Assistant

Process intro: The **Prod. Assistant** action transfers the pass lengths into a simulated production order. The user starts it on the sales order line; the module creates one production order line per pass length with total meters greater than 0, reserves the created quantity against the sales line, and then opens the Prod. Assistant for further processing.

Flow on start:

1. Select the **sales order line** and choose **Prod. Assistant**.
2. If no pass lengths exist, the system asks **"It does not exist Pass Lengths. Do you want to continue?"**; on confirmation the standard Prod. Assistant is called without pass lengths.
3. Otherwise the module creates the simulated production order and one production order line per pass length, transfers **Confection Meter** and **Pass Length Sequence**, and reserves against the sales line.
4. The **Prod. Assistant** opens. If it is cancelled without transfer, the created simulated production order is deleted again.

In the Prod. Assistant, the **Confection Meter** field is available; it holds the length to be confectioned for the rope section and is the reference value of the rope calculation. Via the assistant action, the **Pass Lengths** can be called again; the sorting of the embedded routing follows the rope flag of the chosen routing.

### Recalculate Wire Rope

Process intro: **Recalculate Wire Rope** is the central calculation action of the module. It is available in the **Prod. Assistant**, on the **Prod. Order Routing** (operations of the production order), and on the **Prod. Order Components**, and computes across the entire operation chain.

Flow:

1. Open the Prod. Assistant or the **Prod. Order Routing** of the rope production order.
2. Choose **Recalculate Wire Rope**. If no pass lengths are defined, the system reports **"No Pass Length defined. Do you want to continue?"**.
3. The module checks that the routing carries **Is Wire Rope** and calculates per operation: **Total meters per strand for total order length from production**, **Required single strand length for specified rope length (without setup length)**, **Number of lengths per coil** (limited by **Max. Coil Weight** and **Safety Factor**), **Installation frequency 1 (setup frequency)**, **Total number of coils**, **Remaining meters**, as well as the **Qty. To Produce** and **Qty. To Produce (Component)**; afterwards the **Quantity per** of the prod. order components is updated.

The results appear on the **Prod. Order Routing** in the following fields. They are predominantly calculation results and are overwritten on recalculation.

| Field | Explanation |
|------|-------------|
| **Total meters per strand for total order length from production** | Shows the strand meters required over the order length; input variable for **Number of lengths per coil** and **Remaining meters**. |
| **Required single strand length for specified rope length (without setup length)** | Shows the single strand length required for a rope length without a setup share; it scales with **Helixfactor for Rope** and **Confection Meter**. |
| **Number of lengths per coil** | Shows how many single lengths fit on one coil; limited by **Max. Coil Weight**, **Strand weight**, and **Safety Factor**, at least 1. |
| **Installation frequency 1 (setup frequency)** | Shows how often the operation is set up or installed until the remaining meters are used up; together with the coil count it controls the total number of coils. |
| **Total number of coils** | Shows the total number of coils (Amount Of Coils × installation frequency); reference value of the setup share in the quantity to be produced. |
| **Remaining meters** | Shows the meters remaining after distribution across whole coils; the calculation repeats until this value is 0 or less. |
| **Strand weight** | Shows the weight of the strand determined from **Amount Of Wire** and **Quantity Factor** of the components; it enters the coil calculation. |

On the **Prod. Order Components**, the same component parameters as on the production BOM lines are available (**Amount Of Strands**, **Amount Of Wire**, **Quantity Factor**, **Offcut Factor**, **Helix Factor per Strand**); the **Recalculate Wire Rope** action is available here as well and updates the **Quantity per** of the components.

## Production campaign and Wire Setup Length

When several rope production orders are controlled together, the **production campaign** bundles them and distributes the setup length. The setup of the campaign fields is described in the chapter *Setup → Setting up the Wire Setup Length in the production campaign*; here the operational context is given.

On the **release** of the campaign, the module checks whether the campaign carries **Is Wire Rope** and distributes the centrally maintained **Wire Setup Length** proportionally across the **Setup Length In Meter** of the operations of all campaign orders. Afterwards the affected production orders are recalculated via the same logic as **Recalculate Wire Rope**. If the campaign lines contain rope and non-rope routings mixed, processing aborts with a message that names the affected production order and the differing rope flags; in this case, ensure that all campaign orders are uniformly flagged as rope.

In the campaign overview, the **Is Wire Rope** flag is visible per campaign, so that rope campaigns are recognizable without opening the card.

## Overview lists

### Prod. BOM Line List (overview)

**Entry point:** This standalone list is reachable via **Search** (**Prod. BOM Line List**).

Process intro: The list shows production BOM lines with their rope parameters in a flat overview and serves to control the maintained component values across multiple BOMs. It is to be understood as read-only; the values are maintained on the production BOM itself.

In addition to the standard columns of the production BOM line (among others **Number**, **Quantity**, **Length**), the rope parameters of the component are visible:

| Field | Explanation |
|------|-------------|
| **Amount Of Strands** | Shows the strand count of the component per line; for control of the rope parameters across multiple BOMs. |
| **Amount Of Wire** | Shows the wire count of the component per line. |
| **Quantity Factor** | Shows the quantity factor of the component; conspicuous values indicate a missing item default. |
| **Offcut Factor** | Shows the offcut factor of the component. |
| **Helix Factor per Strand** | Shows the helix factor of the strand of the component. |

### Confection Meter on the production order lines

On the line overviews of the simulated, planned, firm planned, and released production orders, the module adds the **Confection Meter** column in each case. It shows the length to be confectioned for the rope section of the respective production order line and is transferred from the pass length on creation. The column is identical on all four order status levels and serves the quick control of the planned rope length per line.

## Permissions

The module delivers its own assignable permission set for the wire rope configurator. It bundles the objects of the module: the pass length table with read, insert, modify, and delete rights as well as the execution rights of the module codeunits and pages. The permission set defines which actions users may perform in the wire rope configurator. Assign it to the users who are to record pass lengths, use the Prod. Assistant, and run the rope calculation.

## FAQ and Troubleshooting

### 1. Why does "Recalculate Wire Rope" not calculate any values?
The underlying **routing** must carry the **Is Wire Rope** flag. If it is not set, the action aborts because it explicitly checks that the routing is flagged as rope. Set the flag before certification of the routing.

### 2. What happens if no pass lengths are recorded for a sales line?
When starting the **Prod. Assistant**, **"It does not exist Pass Lengths. Do you want to continue?"** appears. If you confirm, the standard Prod. Assistant runs without pass lengths; if you cancel, first record the pass lengths via the **Pass Lengths** action.

### 3. Why does the system report that the pass length is greater than the quantity?
If the quantity of the sales line is changed and the sum of the pass lengths exceeds the new quantity, **"The Pass Length cannot be greater then the Quantity … . Please Update the Pass Length before."** appears. First reduce the pass lengths to the new order quantity.

### 4. How do I ensure that the sales order carries the actually planned length?
When closing the **Pass Lengths** entry with differing **Remaining Meter**, the system asks **"… Do you want to update the Source Document?"**. If you confirm, the module adjusts the meter and quantity values of the sales line to the sum of the pass lengths.

### 5. Why is a pass length marked as "Assistant Prepared"?
When a pass length is led into the Prod. Assistant via the drilldown of the **Sequence** and processed there, the module sets the **Assistant Prepared** flag. When closing the guided view, the system warns if there are still unprocessed pass lengths.

### 6. Where does the setup length in the routing line come from?
It is defaulted from the **Setup Length In Meter** field of the work center when the **work center** is set in the routing line. For machine center assignments, the value of the associated work center is used. You can override the value per operation.

### 7. How does the "Max. Coil Weight" influence the result?
The **Max. Coil Weight** of the work center limits how much rope is permissible per coil. The calculation derives from it **Number of lengths per coil** and **Amount Of Coils**. If the weight at the subsequent work center is 0, the weight of the current work center is used instead, so that the coil calculation does not fail.

### 8. What role does the safety factor play?
The **Safety Factor** reduces the calculated permissible load per coil. A higher value leads to shorter coils, thus to more coils and a higher setup frequency — it increases process reliability at the cost of setup effort.

### 9. Why does the campaign processing abort with a rope message?
If a production campaign contains production orders with different rope flags, the module reports the affected production order and the differing values and aborts. Ensure that all orders of a rope campaign are run uniformly as rope.

### 10. How is the Wire Setup Length distributed across a campaign?
On the **release** of a campaign with **Is Wire Rope**, the module distributes the centrally maintained **Wire Setup Length** proportionally across the **Setup Length In Meter** of the operations of all campaign orders and recalculates the affected orders. Change the **Wire Setup Length** only in the Open status.

## Typical use cases

### Use case 1 — Rope order from a customer order

**Trigger.** A customer orders by phone a wire rope of a specific total length, which is to be produced in several sections.

**Entry in BC.** The user creates the **sales order**, selects the order line, and chooses the **Pass Lengths** action from the **Line** menu.

**Core flow.**
1. In the **Pass Lengths** entry, the user records **Sequence**, **Meter**, and **Number** per section and checks against **Order Meter**, **Total Meter**, and **Remaining Meter** that the order length is fully broken down.
2. On the same sales order line, they choose **Prod. Assistant**. The module creates the simulated production order with one line per pass length, transfers the **Confection Meter**, and reserves against the sales line.
3. In the Prod. Assistant, they run **Recalculate Wire Rope**; the module calculates **Number of lengths per coil**, **Total number of coils**, **Required single strand length**, **Installation frequency 1 (setup frequency)**, **Remaining meters**, and the component quantities.

**Closure.** If the planned length differs from the **Order Meter**, the user confirms, on closing, the prompt to update the source document, so that the sales line carries the actually planned length.

### Use case 2 — Controlling the setup length via a production campaign

**Trigger.** Production control bundles several rope production orders in a **production campaign** in order to plan the setup length jointly.

**Entry in BC.** The user opens the **production campaign** (card) and works on the **General** tab.

**Core flow.**
1. After processing the campaign lines, the **Is Wire Rope** flag is set; the sum of the setup lengths of the contained rope operations appears in the **Wire Setup Length**.
2. If needed, the user has the current total setup length recalculated via the ribbon action (only in the Open status).
3. They **release** the campaign. The module distributes the **Wire Setup Length** proportionally across the **Setup Length In Meter** of the operations and recalculates the affected production orders.

**Closure.** If all campaign orders are uniformly flagged as rope, the distribution is complete; otherwise the abort message points to the differing production order and the user unifies the rope flags.
