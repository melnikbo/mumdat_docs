---
title: Anwenderhandbuch m+m Subcontracting Prices
---

# User Guide m+m Subcontracting Prices

## Introduction

The **m+m Subcontracting Prices** app extends manufacturing in Microsoft Dynamics 365 Business Central with a dedicated price list for subcontract work. In this list you store **subcontracting prices** per combination of **Work Center**, **Vendor**, **Standard Task** and **Item**. As soon as a production order with a subcontracted operation is calculated, the module determines the matching price from this list and automatically writes it as the **Direct Unit Cost** into the affected operation line, purchase line or planning line.

**Target audience.** The primary users are **operational roles in manufacturing and purchasing** who work every day with production orders, the **Subcontracting Worksheet** and **purchase orders**, and who need the prices for outsourced subcontract work there. **Secondarily**, the guide addresses **administrators and master data owners** who prepare the work centers and maintain the subcontracting prices.

**Short process overview.** The flow follows a fixed chain:

1. An administrator stores a vendor as subcontractor on the **Work Center Card** and thereby enables the use of specific subcontracting prices.
2. A master data owner maintains the valid prices, minimum prices, minimum quantities and validity periods in the **Subcontracting Prices** list.
3. In daily operations the system calculates the operation price when building up or updating a production order and transfers it into the operation, the Subcontracting Worksheet and the purchase order created from it.

All three steps are described in this guide in this order: first the **Quick Start**, then the **Setup** of the work center, then the **master data maintenance** of the prices, and finally the **daily work** in the production order and purchasing.

---

## Quick Start for Users

The Quick Start describes the shortest path from setup to the automatically set price. Perform the steps in this order; each step requires the previous one.

**A. Setup (one time, by the administrator)**

1. Open the relevant **Work Center** via the search function (**Search**) and choose the **Work Center Card**.
2. In the **Subcontractor No.** field, enter the vendor that performs the subcontract work. With this entry the system automatically sets the **Specific Unit Cost** toggle to active.
3. Verify that **Specific Unit Cost** is enabled. Only then does the price determination of this module apply.

**B. Master data (store prices)**

4. Open the **Subcontracting Prices** list. You reach the list via the search (**Search**) or, more conveniently, via the **Vendor Card** or **Item Card** in the **Related** menu through the **Subcontracting Prices** action.
5. Per line, enter the **Purchase Type**, the **Work Center No.**, the **Reference Type**, if applicable the **Standard Task**, the **Definition Type**, if applicable the **Item**, the **Price**, the **Minimum Quantity**, the **Minimum Price** as well as **Valid From** and **Valid to**.

**C. Daily work (price is set automatically)**

6. Create a **released production order** for the item with a subcontracted operation.
7. Update the order via **Process** > **Refresh Production Order**. When the operations are built up, the system determines the subcontracting price and writes it as **Direct Unit Cost** into the operation line.
8. Open the **routing** of the order (tab **Lines** > **Routing**). The determined price is shown in the operation line; in the **Subcontracting Prices** FactBox you see the underlying valid price lines.
9. From the **Subcontracting Worksheet**, create the **purchase order** via **Process** > **Calculate Subcontracts** and then via **Process** > **Carry Out Action Message**. The subcontracting price is transferred into the purchase line in the process.

> The complete field description of the setup can be found under [Setup](#setup), the price maintenance under [Master Data: Maintaining Subcontracting Prices](#master-data-maintaining-subcontracting-prices).

---

## Setup

The setup of this module consists of **one** mandatory configuration: linking a **Work Center** with a subcontractor and enabling the specific unit cost. Only this setting unlocks the entire price determination of the module. The price lines themselves are master data and are described in the chapter [Master Data](#master-data-maintaining-subcontracting-prices).

### Setting Up Subcontracting Prices per Work Center

**Process introduction.** This setup is performed by the **administrator** or the manufacturing owner **before first use** for each subcontracted work center. It defines for which work centers subcontracting prices are drawn at all. The setting is evaluated later in the [daily work on the production order](#daily-work-on-the-production-order): only for work centers with the **Specific Unit Cost** enabled does the module replace the regular purchase price with the stored subcontracting price.

**Entry point:** Via the search (**Search**), open the **Work Centers**, choose the relevant line and open the **Work Center Card**. The relevant fields are located in the posting and cost data area of the card.

| Setup | Explanation |
|-------------|-------------|
| **Subcontractor No.** | If you enter a vendor here, you mark the work center as subcontracted and at the same time automatically set the **Specific Unit Cost** toggle to active. As a result, operations of this work center are procured through a purchase order from this vendor, and the price determination of this module is switched on for this work center. |
| **Specific Unit Cost** | When enabled, the system does **not** use the regular purchase or unit cost during order calculation, but rather the price stored for this work center in the **Subcontracting Prices**. If the toggle is not set, the standard unit cost remains effective and the module does not intervene. The toggle is automatically enabled when a **Subcontractor No.** is entered, but it can be checked and adjusted by the administrator. |

**Process steps (dependency order):**

1. **First** enter the **Subcontractor No.** This automatically sets the **Specific Unit Cost** toggle.
2. **Then** verify that **Specific Unit Cost** is enabled. Without this toggle, the module does not draw a subcontracting price in daily work.
3. **Finally** maintain the price lines for this work center in the **Subcontracting Prices** list (see [Master Data](#master-data-maintaining-subcontracting-prices)).

**Dependency / validation.** The price determination applies exclusively to operations of type **Work Center** and only if the work center carries **Specific Unit Cost** = active. The subcontractor stored on the work center is used as the vendor during price determination; if the vendor or the toggle is missing, the regular price remains in place.

---

## Master Data: Maintaining Subcontracting Prices

The **Subcontracting Prices** list is the central master data object of this module. Here master data owners define which price applies for which combination of work center, vendor, Standard Task and item, in what quantity and in what period.

**Process introduction.** The prices are maintained by the **master data owner** or purchaser **after** the setup of the work center and **before** the first production order with subcontract work. The maintained lines are evaluated in daily work as soon as a production order is calculated or a Subcontracting Worksheet or a purchase order is created.

### Navigation to the Subcontracting Prices List

You reach the **Subcontracting Prices** list in three ways:

- Via the search (**Search**) directly as the list page **Subcontracting Prices**.
- Via the **Vendor Card**: menu **Related** > **Subcontracting Prices**. The list is then pre-filtered to the opened vendor.
- Via the **Item Card**: menu **Related** > **Subcontracting Prices**. The list is then pre-filtered to the opened item.

Navigation via the **Vendor Card** or **Item Card** is recommended for daily maintenance, because the list is already narrowed down to the relevant record.

### Fields of the Subcontracting Prices List

Enter the following fields per price line. The editability of individual fields is controlled by the system through the respective type (see option values below): if you set a type to "All …", the associated detail field is locked and cleared.

| Field | Explanation |
|------|-------------|
| **Purchase Type** | Defines for which procurement reference the line applies. For **Vendor**, the price applies only to the vendor named in **Vendor No.**; for **All Vendors**, it applies across vendors. If you choose **All Vendors**, **Vendor No.** is locked and cleared. |
| **Vendor No.** | The vendor for which the price applies. Editable only when **Purchase Type** = **Vendor**, and then checked against the vendor master data. If you enter a value here despite **All Vendors**, the system aborts with the message "%1 must be blank." |
| **Vendor Name** | Displays the name of the vendor stored in **Vendor No.** (display only, read from the vendor master data). |
| **Work Center No.** | The work center for which the price applies. If **Purchase Type** = **Vendor** is set, only work centers whose subcontractor corresponds to the chosen vendor can be selected; otherwise all work centers can be selected. This field links the price line to the operation in the production order. |
| **Work Center Name** | Displays the name of the work center stored in **Work Center No.** (display only). |
| **Reference Type** | Defines whether the price applies to a specific Standard Task or to any Standard Task. For **Standard Task**, the price applies only to the named code; for **All Standard Tasks**, it applies across vendors and work centers independently of the code. If you choose **All Standard Tasks**, **Standard Task** is locked and cleared. |
| **Standard Task** | The Standard Task (the activity/operation type) for which the price applies. Editable only when **Reference Type** = **Standard Task**, and checked against the Standard Tasks. An entry with **All Standard Tasks** leads to the error message "%1 must be blank." |
| **Definition Type** | Defines whether the price applies to a specific item or to any item. For **Item**, the price applies only to the named item; for **All Items**, across items. If you choose **All Items**, **Item** is locked and cleared. |
| **Item** | The item for which the price applies. Editable only when **Definition Type** = **Item**, and checked against the item master data. An entry with **All Items** leads to the error message "%1 must be blank." |
| **Unit** | The unit of measure to which the price refers. Checked against the units and serves as the reference basis of the price entry. |
| **Minimum Price** | When set, this amount applies as a lower limit: if the line amount calculated from **Price** × quantity falls below the minimum price, the system uses the minimum price as a flat rate. This ensures that a subcontract job does not go below a base amount. The minimum price may be assigned per work center and Standard Task **only once**; a second minimum price for the same combination is rejected with the message "For this Combination of Work Center and Standard Task, there is already a Minimum Price." |
| **Minimum Quantity** | When set, the price of this line applies only from the specified quantity onward. Across multiple lines with different minimum quantities you build **price tiers**: during calculation, only lines whose minimum quantity is less than or equal to the order quantity are considered. The minimum quantity may be assigned multiple times per combination. |
| **Price** | The price per **Unit** for the combination of work center, Standard Task and quantity. From this price the system calculates the line amount and, from it, the **Direct Unit Cost** of the operation or purchase line. |
| **Valid From** | When set, the price applies only from this date onward. During calculation, only lines whose **Valid From** is blank or less than/equal to the work date are considered. |
| **Valid to** | When set, the price applies only up to this date. During calculation, only lines whose **Valid to** is blank or greater than/equal to the work date are considered. This lets you plan price changes in advance. |

#### Option Values in Detail

**Purchase Type**

- **Vendor:** The line applies exclusively to the vendor named in **Vendor No.**. The **Vendor No.** field is editable and must be filled.
- **All Vendors:** The line applies to every vendor. **Vendor No.** is locked and cleared; a manually entered vendor is rejected.
- **Vendor Group:** Intended value for bundling several vendors into a group. In the current price determination, the option values **Vendor** and **All Vendors** are evaluated when selecting the valid lines; document the planned use of **Vendor Group** with your consultant.

**Reference Type**

- **Standard Task:** The line applies only to the named Standard Task. **Standard Task** is editable and must be filled.
- **All Standard Tasks:** The line applies to every Standard Task. **Standard Task** is locked and cleared.

**Definition Type**

- **Item:** The line applies only to the named item. **Item** is editable and must be filled.
- **All Items:** The line applies to every item. **Item** is locked and cleared.

**Process steps for a price tier (example):**

1. **First** create a line with **Minimum Quantity** 0 (or blank) and the base price.
2. **Then** create additional lines with increasing **Minimum Quantity** and the respective tiered **Price**.
3. **Optionally** store a **Minimum Price** as a base amount in **one** line per combination of work center and Standard Task.
4. **Finally** narrow the period via **Valid From** / **Valid to** if prices are meant to apply for a limited time.

**Dependency / validation.** The **Minimum Price** is unique per work center and Standard Task. For a second minimum price for the same combination, the system aborts. The determination of the applicable price in daily work is described under [Price Determination](#price-determination-logic).

---

## Daily Work on the Production Order

This chapter describes how and when the subcontracting price is drawn in ongoing operations. All described automatisms require that the work center carries the **Specific Unit Cost** toggle per [Setup](#setup) and that valid [Subcontracting Prices](#master-data-maintaining-subcontracting-prices) are maintained for the combination.

**Relation to the setup.** The daily price determination is controlled by two upstream configurations: by the **Specific Unit Cost** toggle and the subcontractor on the **Work Center Card** (setup) as well as by the lines in the **Subcontracting Prices** list (master data). If one of these prerequisites is missing, the regular price remains in place.

### Price in the Operation of the Production Order

The module sets the **Direct Unit Cost** of the subcontracted operation automatically at several points:

1. **When building up the operations** (action **Process** > **Refresh Production Order**): as soon as an operation is added to the production order, the system determines the subcontracting price and enters the **Direct Unit Cost**.
2. **When changing the operation line:** if you change the **Work Center No.** or the **Standard Task** of an operation line in the **routing**, the system recalculates the price immediately.
3. **When converting planning suggestions** into a production order, the price is likewise set when the operation line is created.

**Entry point:** Open the **released production order** and, within it, the **Lines** > **Routing** tab. The affected operation line shows the determined price in the **Direct Unit Cost** field.

### Subcontracting Prices FactBox

On the **Routing** (Prod. Order Routing), **Subcontracting Worksheet** and **Purchase Order** pages, the module shows the **Subcontracting Prices** FactBox. For the currently selected line, it shows the applicable, **currently valid** price lines (filtered to **Valid From** ≤ work date and **Valid to** ≥ work date). This lets users check directly on the document which stored prices feed the calculation.

| Field (FactBox) | Explanation |
|--------------------|-------------|
| **Work Center Name** | Shows the work center of the respective valid price line. |
| **Standard Task** | Shows the Standard Task of the valid price line. |
| **Minimum Price** | Shows the stored base amount of the line. |
| **Minimum Quantity** | Shows the quantity threshold of the price tier. |
| **Price** | Shows the price stored per unit. |
| **Valid From** / **Valid to** | Shows the validity period of the displayed price line. |

The FactBox is not editable; it serves control purposes only. The **Vendor No.** is not shown as a column in the FactBox, because the reference is already given through work center and document.

### Purchase Order from the Subcontracting Worksheet

The regular path for procuring the subcontract work leads through the **Subcontracting Worksheet**:

1. Via the search (**Search**), open the **Subcontracting Worksheet**.
2. Choose **Process** > **Calculate Subcontracts** to display the open subcontract jobs. In doing so, the subcontracting price is transferred into the planning line.
3. If applicable, set a filter on the lines to be processed and choose **Process** > **Carry Out Action Message**. The system creates the **purchase order** from it; the processed line disappears from the worksheet.
4. Open the created **purchase order**. In the purchase line, the **Direct Unit Cost** taken from the subcontracting prices is shown.

### Recalculating the Price in the Purchase Order

On the **purchase order lines**, the **Calculate Subcontracting Prices** action is additionally available. It recalculates the price of the selected purchase line based on the currently valid subcontracting prices and the associated production order operation.

**Entry point:** Open the **purchase order**, select the relevant purchase line in the lines and, via **Functions**, choose the **Calculate Subcontracting Prices** action.

Use this action when quantity, operation or price tier have changed after the order was created and you want to align the **Direct Unit Cost** with the current subcontracting price. The prerequisite is that the purchase line is assigned via production order, routing and operation to a calculable operation, and that the quantity is greater than zero.

<a id="price-determination-logic"></a>
### Price Determination – How the System Determines the Price

At each calculation the module selects the applicable prices from the maintained lines and determines the governing price from them:

1. **Precondition:** The operation is of type **Work Center** and the work center carries **Specific Unit Cost** = active. Otherwise the module does not intervene.
2. **Base filter:** Only price lines are considered whose **Work Center No.** matches, whose **Item** is blank or equals the order item, whose validity period includes the work date, and whose **Minimum Quantity** is less than or equal to the order quantity.
3. **Combinations:** From these lines the system considers four option combinations — **All Vendors + All Standard Tasks**, **Vendor (subcontractor) + All Standard Tasks**, **Vendor (subcontractor) + Standard Task**, and **All Vendors + Standard Task**.
4. **Amount determination per line:** For each considered line the following applies: line amount = **Price** × order quantity. If the line amount is above the **Minimum Price**, the line amount is used, otherwise the **Minimum Price**.
5. **Best value:** From all amounts determined this way, the system chooses the **lowest** amount. This amount divided by the quantity yields the **Direct Unit Cost** of the line.

Depending on the trigger, the determined price is written into the **operation line**, the **purchase line** or the **planning line**; when converting from the worksheet into the order, the calculated price is additionally written back into the operation of the production order.

---

## FAQ and Troubleshooting

### 1. Why is no subcontracting price transferred into the operation?

First check the **Work Center Card**: without the **Specific Unit Cost** toggle enabled, the price determination does not apply. The toggle is set automatically as soon as a **Subcontractor No.** is entered. In addition, the operation must be of type **Work Center**.

### 2. Why does the price stay zero even though a matching price line exists?

The price determination only considers lines whose **Minimum Quantity** is less than or equal to the order quantity and whose validity period (**Valid From** / **Valid to**) includes the work date. If the order quantity is smaller than every stored **Minimum Quantity**, or the work date lies outside the validity, the line is ignored. Even with an order quantity of zero, no calculation takes place.

### 3. Why does the system report "For this Combination of Work Center and Standard Task, there is already a Minimum Price."?

The **Minimum Price** may be assigned only **once** per combination of **Work Center No.** and **Standard Task**. For the same combination, a line with a minimum price greater than zero already exists. Use the existing line or set the duplicate minimum price to zero.

### 4. Why can I not fill in the Vendor No.?

The **Vendor No.** is editable only when **Purchase Type** = **Vendor**. With **All Vendors**, the system locks and clears the field. A vendor entered anyway is rejected with "%1 must be blank." The same principle applies to **Standard Task** for **Reference Type** and **Item** for **Definition Type**.

### 5. How do I represent quantity discounts for subcontract work?

Create several price lines with the same work center and increasing **Minimum Quantity** and store the tiered **Price** per line. During calculation, all lines up to the order quantity are considered; the system chooses the cheapest governing amount from them.

### 6. How does the minimum price affect small quantities?

If the line amount calculated from **Price** × order quantity is below the **Minimum Price**, the system charges the minimum price as a flat rate. For very small quantities, therefore, not the proportional amount but the base amount is applied.

### 7. Where do I see which prices are currently being used?

In the **Subcontracting Prices** FactBox on the **routing**, in the **Subcontracting Worksheet** and in the **purchase order**. It shows the currently valid price lines for the selected line, filtered to the work date.

### 8. Why does the price in the purchase order differ from the operation?

After the order was created, quantity or operation may have changed. In the purchase order lines, use the **Calculate Subcontracting Prices** action via **Functions** to determine the **Direct Unit Cost** anew based on the currently valid subcontracting prices.

### 9. Does a price line without a vendor apply to every supplier?

Yes. With **Purchase Type** = **All Vendors** and **Reference Type** = **All Standard Tasks**, the line acts as a general basis. More specific lines (with vendor or Standard Task) are additionally considered; in the end, the cheapest determined amount governs.

### 10. Do I have to enter the price manually into the order?

No. The regular path creates the **purchase order** via the **Subcontracting Worksheet** (**Process** > **Calculate Subcontracts**, then **Process** > **Carry Out Action Message**); the price is transferred automatically. Manual rework is only needed for subsequent changes via **Calculate Subcontracting Prices**.

---

## Typical Use Cases

The following scenarios show the flow from the perspective of the operational users. Every page and action addressed is described in the previous chapters.

### Scenario 1: New Subcontracting Price for a Subcontractor

**Trigger.** A new subcontractor takes over the coating of a component; purchasing has negotiated a tiered price and received confirmation by email.

**Entry into BC.** The administrator opens the **Work Centers** via the search (**Search**), chooses the "Coating" work center and, within it, the **Work Center Card**.

**Core flow.**
1. The administrator enters the new vendor in the **Subcontractor No.** field; **Specific Unit Cost** is automatically enabled.
2. The master data owner opens the **Subcontracting Prices** via the **Vendor Card** in the **Related** menu.
3. He creates a first line with **Purchase Type** = **Vendor**, the work center, **Reference Type** = **All Standard Tasks**, **Definition Type** = **All Items**, **Minimum Quantity** 0 and the base price.
4. For the higher tier he creates a second line with a larger **Minimum Quantity** and a lower **Price**, and stores a **Minimum Price** as a base amount in one line.

**Conclusion.** The prices are effective immediately and are drawn automatically from the next production order onward.

### Scenario 2: Production Order with Subcontract Work Through to the Purchase Order

**Trigger.** Manufacturing control releases a production order for a component whose routing contains a subcontracted operation.

**Entry into BC.** The manufacturing planner opens the **released production order**.

**Core flow.**
1. He updates the order via **Process** > **Refresh Production Order**; the system enters the **Direct Unit Cost** into the subcontracted operation.
2. Via the **Lines** > **Routing** tab he checks the determined price and reviews the underlying lines in the **Subcontracting Prices** FactBox.
3. In the **Subcontracting Worksheet** he calls **Process** > **Calculate Subcontracts** and then **Process** > **Carry Out Action Message**.

**Conclusion.** The system creates the **purchase order** with the transferred subcontracting price; the processed line disappears from the worksheet. For subsequent quantity changes, the purchaser aligns the price via **Functions** > **Calculate Subcontracting Prices** in the purchase order lines.

### Scenario 3: Time-Limited Special Price

**Trigger.** A subcontractor grants a reduced price for one quarter.

**Entry into BC.** The master data owner opens the **Subcontracting Prices** via the **Item Card** in the **Related** menu.

**Core flow.**
1. He creates a price line for the affected combination and enters the reduced **Price**.
2. Via **Valid From** and **Valid to** he narrows the period to the quarter.

**Conclusion.** Within the period the system draws the special price; afterward the regular price lines automatically apply again, because expired lines are skipped during calculation.
