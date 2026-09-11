---
title: Anwenderhandbuch m+m Calculation
---

# User Guide m+m Calculation

## Introduction

The **m+m Calculation** module calculates, within Microsoft Dynamics 365 Business Central, the
**Unit Cost** and the **Sales Price** of an item based on a freely definable
calculation scheme. The basis of every calculation is a **Calculation Template**, which line by
line defines which cost components (material costs, capacity costs, overhead costs,
subcontracting costs, tool costs, surcharges and deductions) are combined in which order.
From the cost values of a simulated production order the module determines the
individual values and consolidates them via **Subtotals** and **Sums** up to the Unit Cost and
Sales Price.

**Target audience:** Primarily **operational users in Sales and Production Planning**
who, in day-to-day business, create, calculate, **certify** and transfer the determined price
into the document out of a **Sales Order**, a **Sales Quote**, a **Sales Invoice** or an
**Opportunity**. The secondary target audience are **administrators and key users**, who set up
the **Calculation Setup**, the **Calculation Templates** and the
**Calculation Template Defaults** once.

**Short process overview:** From the sales document line the user opens a new **Calculation** via
**Line → Functions → Create/Open Calculation**. Based on
**Contact No.** (customer or customer price group) and **Item No.** the system automatically
preselects the appropriate **Calculation Template** via the **Calculation Template Defaults**. The user
maintains values and percentages in the calculation lines, has the values recalculated, **certifies** the
calculation and transfers the **Sales Price** into the document, and the **Unit Cost** into the
item.

The typical entry chain is: **higher-level document (Sales Order/Quote/Invoice)
or Opportunity → Line → Functions → Create/Open Calculation → edit Calculation →
certify → price transfer**.

---

## Quick Start for Users

The steps follow the order of dependencies: first **Setup**, then **Master Data**,
then the daily work on the document.

1. **Check the setup (one-time, administrator).** Open the **Calculation Setup** page via
   **Search** and enter **Calculation Nos.** (number series),
   **Dummy Item No.**, **Dummy Routing No.**, **Template for New Item** as well as
   **Calculation Report**.
2. **Create a Calculation Template (key user).** Open the list
   **Calculation Templates** via **Search**, create a template and define the
   calculation scheme (Field Type, Calculated Value, Formula, Usage Type) in the **Lines**.
3. **Define defaults (optional).** In the **Calculation Setup**, open the page
   **Calculation Template Defaults** via **Default Calc. Templates** and assign a template to
   customer/item combinations.
4. **Start a calculation from the document (user).** In the line of a
   **Sales Order**, **Sales Quote** or **Sales Invoice**, open the action
   **Create/Open Calculation** via **Line → Functions**. The
   **Calculation** opens with pre-filled **Item No.**, **Contact No.** and possibly the **Calculation Template**.
5. **Calculate.** Maintain values/percentages in the lines; the system recalculates the Unit Cost
   and Sales Price continuously. If required, run **Update Unit Cost**.
6. **Certify the calculation.** Choose **Certify Calculation**. The status changes to
   **Certified**; the values become read-only.
7. **Transfer the price.** Transfer the sales price with **Set Sales Price in Documents**
   into the assigned document (with the setup **On Certified** this happens automatically),
   the unit cost with **Update Unit Cost** into the item and, optionally, the
   sales price with **Set Price in Item** into the item card.

---

## Setup

The **Setup** is the prerequisite for every calculation and is performed once by the
administrator. Without **Calculation Nos.**, **Dummy Item No.** and
**Dummy Routing No.** no calculation can be created (when creating a calculation the module
creates, in the background, a **simulated production order** that requires an item number
and a routing).

### Calculation Setup

**Entry:** Open the **Calculation Setup** page via **Search**. This is a
company-wide setup page with exactly one record (type A, no higher-level
document). Here the administrator enters all fundamental defaults for number assignment,
calculation, price transfer and reports, before the first calculation is created. The values set
here subsequently control the **Calculation** (number series, price transfer) and the
**Batch Calculation** (batch template) in the daily workflow.

#### General area

| Setup | Explanation |
|---|---|
| **Calculation Nos.** | Defines the number series from which new calculations receive their **No.**. If entered, the system automatically assigns the next free number when a calculation is created; if the field is empty, no calculation can be created (mandatory check on insert). |
| **Dummy Item No.** | Defines the placeholder item with which the simulated production order is initially created. If set, a calculation can be started even without an already existing target item; without an entry the creation is aborted, because an item number is required for every calculation. |
| **Dummy Routing No.** | Defines the placeholder routing that is assigned to the simulated production order as long as the item does not have its own routing. If set, capacity costs can be determined via the simulated production order. |
| **Template for New Item** | Defines the item template (configuration template) from which the master data of the new item is pre-filled during **Create Item**. If set, the item created from the calculation automatically receives the predefined properties; if no template is entered, the creation is aborted with a message. |
| **Recursive Calculation Update** | Controls whether a change to the unit cost of a calculation that is used as a component in other calculations is passed on to those calculations. For values see the option list below. |
| **Calculate Mat. Overhead Costs on Purch. Items** | Controls whether and when additional material overhead costs are added to purchased components (replenishment method Purchase). For values see the option list below. |
| **Batch Calculation Template** | Defines the calculation template used by the **Batch Calculation** (mass calculation in the **Calculation Batch Journal**). If set, the batch lines are automatically pre-filled with this template when the calculations are collected. |
| **Set Sales Price in Document** | Controls whether the determined sales price is automatically transferred into the assigned sales document. For values see the option list below. |

**Option values:**

- **Recursive Calculation Update**
  - **Never:** The new unit cost is not passed on to higher-level calculations;
    these retain their previous value until they are recalculated manually.
  - **Always:** If the unit cost changes, the system automatically updates, without a prompt,
    all calculations that are under development in which this calculation is used as a component.
  - **Ask:** Before the value is passed on, a prompt appears; the user decides whether the
    dependent calculations are updated.
- **Calculate Mat. Overhead Costs on Purch. Items**
  - **Always:** Material overhead costs are added to purchased components in every calculation
    and shown in **Mat. Overh. Cost Purch. Items**.
  - **Never:** No separate material overhead costs are calculated for purchased items.
  - **When Used:** The surcharge is applied only if the calculation template contains a line with the
    calculated value **Material Overhead Cost Purch. Items**.
- **Set Sales Price in Document**
  - **(blank):** No automatic price transfer takes place; the user transfers the
    sales price manually when required via **Set Sales Price in Documents**.
  - **On Certified:** When the calculation is **Certified**, the sales price is
    automatically written into the lines of the assigned, still open sales documents and is
    fixed afterwards.

#### Printing area

This area links the calculation with the reports to be output. If a report is entered
here, the action **Print** is available in the calculation and in the list **Calculations**.

| Setup | Explanation |
|---|---|
| **Calculation Report** | Defines the report ID with which a calculation is printed. If set, the action **Print** prints exactly this report; if the field is empty, the system reports a missing report when printing. |
| **Report Name** | Displays, for control, the name of the report selected under **Calculation Report** (display only, not editable). |
| **Show Request Page Calculation** | If enabled, the request page (print filter page) opens before the calculation is printed, on which the user can set filters and options; without enabling it, printing takes place directly. |
| **Prod. Order Report** | Defines the report ID of the production order report that is printed in addition to the calculation report for the simulated production order. If set, this report is also output when printing. |
| **Report Name** | Displays, for control, the name of the report selected under **Prod. Order Report** (display only). |
| **Show Request Page Prod. Order** | If enabled, the request page of the production order report appears before it is printed; without enabling it, printing takes place directly. |

**Action in the setup:** Via **Default Calc. Templates** the user opens the page
**Calculation Template Defaults** (see section *Set up Calculation Template Defaults*).

### Permissions

For access to the module the app provides the permission set **MuM CA Permission**. It
defines which actions the users may perform in the calculation objects (create,
modify, certify, delete the calculations, templates and setup). The administrator
assigns this permission set to the relevant users or user groups via the
standard permission management of Business Central.

---

## Master Data

The master data define **how** the calculation is performed (Calculation Templates), **which** template
is automatically proposed (Calculation Template Defaults) and establish the relation to **Item**
and **Opportunity**.

### Calculation Templates

**Entry:** Open the list **Calculation Templates** via **Search** and open a
line to edit the **Calculation Template** card.

The calculation template is the core of the module: in it the key user defines **one** scheme
according to which the system calculates the calculation prices. The administrator/key user maintains the
templates before the first calculation and adjusts them when the calculation scheme changes. The
template is selected in the **Calculation** via the field **Calculation Template** or is
automatically pre-filled via the **Calculation Template Defaults**.

**Procedure:** First you create the template header (Code, Description, base values), then you
enter the template lines from top to bottom in the desired calculation order.

#### Header data of the Calculation Template

| Field | Explanation |
|---|---|
| **Code** | Unique key of the template. If set, the template can be selected in calculations and defaults. |
| **Description** | Meaningful name of the template; simplifies the selection in the calculation and defaults. |
| **Material Overhead Cost % Purch. Items** | Defines the percentage with which material overhead costs are added to purchased components. If set, this value is transferred into the calculation when the template is selected and is used there for calculating the **Mat. Overh. Cost Purch. Items**. |
| **Order Quantity** | Defines the order quantity for which the calculation is performed (minimum value 1). If set, the order quantity is transferred into the calculation when the template is selected; the determined costs are subsequently related to this quantity (per piece). |

#### Lines of the Calculation Template

The **Lines** form the calculation scheme. Processing always takes place **from top to bottom**;
sums and subtotals access the line numbers to be accumulated via the field **Formula**.

| Field | Explanation |
|---|---|
| **Line No.** | Defines the position of the line in the scheme and thereby determines the processing order. |
| **Description** | Designation of the line (e.g. "Material Cost", "Administrative Overhead"); appears identically in the calculation. |
| **Field Type** | Determines how the line value is determined. For values see the option list below; the Field Type determines which further fields are editable. |
| **Calculated Value** | Active only with Field Type **Calculated Value**: defines which cost component from the simulated production order is used. For values see the option list below. |
| **Calculation Base** | For percentage lines, refers to the Line No. to whose value the percentage is applied. If set, the system applies the percentage value exactly to this base line. |
| **Formula** | Active only with Field Type **Subtotal** or **Sum**: specifies via line numbers (linked with "+") which lines are accumulated. An invalid formula is rejected with an error message on entry. |
| **Value** | The manually entered amount (for **Manual Value**) or the calculated line value; directly controls the calculation result of the following lines. |
| **Alt. Value 1** … **Alt. Value 4** | Alternative values per line for parallel calculation variants (e.g. different scenarios). If filled, the alternative columns are also calculated in the calculation. |
| **Assigned to Calculated Value** | Assigns a manual line to a cost block so that the sum of the individual costs corresponds to the shown unit cost. For values see the option list below. For the Field Types **Sum**, **Subtotal** and **Calculated Value** an assignment is not permitted (error message). |
| **Fix Value** | If enabled, the entered value is fixed and can no longer be changed in the calculation; without the mark the line remains editable in the calculation. |
| **In Hundred** | If enabled, the percentage is calculated "in the hundred" (Value = Base × Percent/(100−Percent)) instead of "of the hundred"; this allows surcharges on a target price to be determined in reverse. |
| **Usage Type** | Indicates which line delivers the final result. For values see the option list below. If a Usage Type is newly set, the system automatically removes it from the previous line (message), so that **Unit Cost** and **Sales Price** each remain assigned to exactly one line. |

**Option values:**

- **Field Type**
  - **Calculated Value:** The line value is taken from the simulated production order; the
    field **Calculated Value** becomes selectable.
  - **Manual Value:** The user enters the amount directly in the field **Value**.
  - **Manual Percent:** The user enters a percentage; the line value results
    from the **Calculation Base** multiplied by the percentage.
  - **Subtotal:** The value is formed from the lines named in the **Formula**
    (partial sum).
  - **Sum:** The value accumulates the lines named in the **Formula** to a total sum.
  - **Tool Cost per Unit:** The value results from **Tool Cost** divided by
    **Tool Endurance** of the calculation.
- **Calculated Value**
  - **Material Cost:** All costs of the raw, auxiliary and operating materials used.
  - **Mat. Cost Without Scrap:** Pure material costs without the portions caused by scrap.
  - **Material Overhead Cost Purch. Items:** Overhead surcharge on purchased components.
  - **Capacity Cost:** Costs of the production capacity used (operations).
  - **Cap. Overhead Cost:** Capacity overhead costs.
  - **Mfg. Overhead Cost:** Overhead costs of production.
  - **Subcontrd. Cost:** Costs for work steps that are taken over by a vendor.
  - **Routing Scrap:** The scrap portion of the operations entered in the routing.
- **Assigned to Calculated Value**
  - **(blank):** No assignment; the line does not flow into the unit cost control sum.
  - **Material Cost / Capacity Cost / Subcontrd. Cost / Cap. Overhead Cost /
    Mfg. Overhead Cost:** The manual line is allocated to the respective cost block, so that the
    sum of the individual costs matches the shown **Unit Cost**.
- **Usage Type**
  - **Unit Cost:** This line delivers the calculated unit cost and is written into the item
    when it is updated.
  - **Sales Price:** This line delivers the calculated sales price and is transferred into the
    documents or price lists.

The template lines can also be viewed via the standalone overview **Calculation Template Lines**
(drilldown of the template lines).

### Set up Calculation Template Defaults (profile determination)

This dedicated setup ensures that when a calculation is created from a document the
correct calculation template is proposed **automatically**. It is maintained by the key user
after the **Calculation Templates** exist, and it takes effect later in the daily workflow with
**Create/Open Calculation**.

**Entry:** In the **Calculation Setup** open the action
**Default Calc. Templates**. The page **Calculation Template Defaults** opens.

**Process intro:** Via combinations of **Template Type** (customer level) and **Template Subtype**
(item level) the key user assigns a **Calculation Template** to each constellation. When a
calculation is opened, the system determines the most suitable default based on **Contact No.** and
**Item No.**.

| Field | Explanation |
|---|---|
| **Template Type** | Defines the customer level of the default. For values see the option list below. If switched to **All Customers**, the system automatically removes a customer number that may have been entered. |
| **Customer No.** | For **Customer**, defines the customer number, or for **Customer Price Group** the group code. If set, the default applies only to this customer or this price group; with a different Template Type, an entry is not permitted. |
| **Template Subtype** | Defines the item level of the default. For values see the option list below. If switched to **All Items**, the system automatically removes an item number that may have been entered. |
| **Item No.** | For **Item**, defines the item number for which the default applies. An entry is only permitted if the Template Subtype is **Item**. |
| **Calculation Template** | Defines the calculation template that is automatically proposed for the selected combination. |

**Option values:**

- **Template Type**
  - **All Customers:** The default applies across customers as a fallback rule.
  - **Customer:** The default applies to exactly one customer (in **Customer No.**).
  - **Customer Price Group:** The default applies to all customers of a price group.
- **Template Subtype**
  - **All Items:** The default applies to all items of the selected customer range.
  - **Item:** The default applies to exactly one item (in **Item No.**).

**Numbered determination (procedure per the code):** When a calculation is created from a document
the system searches for the template in the following order:

1. **First** it is checked whether a default with **Template Type = Customer** and the **Customer No.**
   of the document exists.
2. **Next**, if not found, the **Customer Price Group** of the customer is used
   (**Template Type = Customer Price Group**).
3. **Finally**, if still not found, the fallback rule
   **Template Type = All Customers** applies.
4. Within the found customer level, if an **Item No.** is present the default
   for **Item** is used first, and otherwise for **All Items**.

The **Calculation Template** determined in this way is transferred into the calculation; the user can
still change it manually. These defaults save time in the daily workflow and increase reliability,
because the calculation scheme does not have to be selected anew for every calculation (relation to the
section *Daily Work: Calculation*).

### Set up sales price transfer

This setup connects the **Calculation Setup** with the daily workflow on the document. It
defines whether and when the calculated sales price reaches the sales document.

1. **First** the administrator sets the field **Set Sales Price in Document** to
   **On Certified** in the **Calculation Setup** if the price transfer is to take place
   automatically (with **(blank)** it remains manual).
2. **Next**, when the calculation is created from the document, a **document assignment** is created
   automatically (see *Document Assignment*), which links the calculation and the sales document line.
3. **Operational conclusion:** When **Certifying**, the system writes the **Sales Price** into
   the lines of the assigned, still **open** sales documents. Alternatively, the user triggers the
   transfer at any time manually via **Set Sales Price in Documents** (see *Daily
   Work*).

### Item relation (master data on the item)

The module extends the **Item Card** with the field **Calculation Unit Cost**. The value is
maintained when a certified calculation writes the unit cost into the item via **Update Unit Cost**.
If filled, the field documents the unit cost of the item last transferred from a
calculation; the administrator does not have to maintain it manually. Thus it is at any time
traceable at the item which calculated unit cost was last valid.

### Opportunity (master data relation)

On the **Opportunity** (Opportunity Card) the module adds the field **Calculation Item No.**
as well as the action **Create/Open Calculation**.

| Field | Explanation |
|---|---|
| **Calculation Item No.** | Defines the item for which the calculation is to be performed out of the opportunity. If set, the action **Create/Open Calculation** uses this item as the target item of the new calculation. |

The sales representative maintains the **Calculation Item No.** in the quotation phase. Via
**Line/Action → Functions → Create/Open Calculation** they start the calculation directly from
the opportunity; a **document assignment** with source "Opportunity" is created automatically
(relation to the section *Daily Work*).

---

## Daily Work: Calculation

The actual calculation is created in day-to-day business, usually triggered from a sales document.
The defaults used originate from the **Calculation Setup** (number series,
price transfer, reports) and from the **Master Data** (Calculation Template, template defaults) —
see chapters *Setup* and *Master Data*.

### Entry via the sales document

**Entry (type C – action on the document line):** In the line of a **Sales Order**,
**Sales Quote**, a **Sales Invoice** or a blanket sales order, open the group
**Line → Functions** and choose **Create/Open Calculation**. If a calculation already exists for
the line, its latest version is opened; otherwise the system creates a new
**Calculation** with a consecutive **No.**, transfers **Item No.** and **Contact No.** from the
document and preselects the appropriate **Calculation Template** via the **Calculation Template Defaults**.

Alternatively, the user starts the calculation from an **Opportunity** via the
action **Create/Open Calculation** there (see *Opportunity*).

### Calculation – Card

The **Calculation** page is the main document of the module. It is divided into the areas
**General**, the lines (**Lines**), **Advanced**, **Contact**, **Values**, **Info** and
**Post Calculation**. All fields are editable only in the status **Under Development**.

#### General area

| Field | Explanation |
|---|---|
| **No.** | Consecutive calculation number from the number series. Editable only in the status **Under Development**; via the assist edit a linked number series can be selected. |
| **Version** | Shows the version number of the calculation. With **Create New Version** a higher version is created; older certified versions can be set to **Closed**. |
| **Valid from** / **Valid to** | Define the validity period of the calculation. If set, they control, during **Update Sales Price List**, the period of the sales price lines to be updated. |
| **Description** | Free-text description of the calculation; is pre-filled, if applicable, from the item description when the **Item No.** is set. |
| **Project** | Free-text field for the assignment of a project. Can also be changed in the status **Certified**. |
| **Quote** | Free-text field for the assignment of a quote. Can also be changed in the status **Certified**. |
| **Calculation Template** | Defines the calculation scheme. When changed, existing calculation lines are deleted after a prompt and recreated from the new template; afterwards the values are recalculated. |
| **Item No.** | Defines the item to be calculated. If set (and not equal to the dummy item), **Item Created** is activated, the routing and production BOM of the item are transferred into the simulated production order and the lines are calculated. |
| **Multilevel Calculation** | If enabled, the system first calculates the standard unit cost of the item (multilevel via the BOM) and uses it as the material cost of the calculation; without the mark the material costs are taken directly from the simulated production order. |
| **Item Created** | Indicates whether a real item has already been created from the calculation (display only). |
| **Status** | Controls the life cycle of the calculation. For values see the option list below. Setting it directly to **Certified** via the field is blocked; the action **Certify Calculation** must be used for this. |

**Option values – Status:**

- **Under Development:** The calculation is being edited; all values are editable, it can be
  recalculated.
- **Certified:** The calculation is released and read-only; prices can no longer be
  changed. Only in this status are **Create Item**, **Update Unit Cost**
  and **Update Sales Price List** possible.
- **Closed:** The calculation is closed and is only kept for historical purposes.

#### Lines area (calculation scheme)

The lines correspond to the scheme of the selected calculation template and are processed **from top to
bottom**. Depending on the **Field Type**, only the appropriate value or
percentage fields are editable; **Sums** and **Subtotals** are calculated by the system and displayed in bold.

| Field | Explanation |
|---|---|
| **Description** | Designation of the line from the template; sum/subtotal lines are highlighted. |
| **Field Type** | Shows the type of the line taken from the template (see option values in the section *Calculation Templates*). |
| **Calculated Value** | For calculated lines, shows the cost component used. |
| **Percent** | Editable for **Manual Percent**: the percentage that is applied to the calculation base. A change triggers the recalculation of the following lines. |
| **Value** | Editable for **Manual Value**, or the calculated line value; controls the result of the following lines. |
| **Alt. Percent 1** … **Alt. Percent 4** | Alternative percentages for the parallel calculation variants (editable only for percentage lines). |
| **Alt. Value 1** … **Alt. Value 4** | Alternative values of the parallel calculation variants (editable only for value lines). |

If values or percentages are set as **fixed** (template mark **Fix Value**), the
corresponding fields are locked in the calculation.

#### Advanced area

| Field | Explanation |
|---|---|
| **Routing No.** | Defines the routing from which capacity costs and routing scrap are determined. When changed, the simulated production order is rebuilt and recalculated. |
| **Production BOM No.** | Defines the production BOM from which the material components and costs originate. When changed, components and costs are re-determined. |
| **Order Quantity** | Defines the order quantity (minimum value 1) to which the costs are related. When changed, the simulated production order and the lines are recalculated (costs per piece). |
| **Material Overhead Cost % Purch. Items** | Defines the percentage for material overhead costs on purchased components; controls the amount of the **Mat. Overh. Cost Purch. Items**. |
| **Tool Cost** | Defines the total tool costs; together with the **Tool Endurance** the value of a line of type **Tool Cost per Unit** results. A change forces a recalculation. |
| **Tool Endurance** | Defines over how many units the tool costs are distributed (Tool Cost ÷ Endurance = Tool Cost per Unit). |
| **Internal Comment** | Free text for internal notes; can also be changed in the status **Certified**. |

#### Contact area

| Field | Explanation |
|---|---|
| **Contact Type** | Defines against which master data the **Contact No.** is checked. Values: **Customer** (check/source from the customer overview) or **Contact** (from the contact overview). On switching, an existing contact number is reset. |
| **Contact No.** | Defines the customer or contact of the calculation. For **Customer**, the entry triggers the automatic determination of the calculation template via the defaults (see *Set up Calculation Template Defaults*). |
| **Reference No.** | Free-text field for an external reference; can also be changed in the status **Certified**. |
| **Reference Date** | Date of the external reference; can also be changed in the status **Certified**. |

**Option values – Contact Type:** **Customer:** Contact No. is selected from the customer overview and
triggers the template determination. **Contact:** Contact No. is selected from the contact overview.

#### Values area

All value fields are result fields (display only) and are updated at every recalculation.

| Field | Explanation |
|---|---|
| **Material Cost** | Determined material cost per piece from the simulated production order. |
| **Mat. Cost Without Scrap** | Material cost without the portion caused by scrap. |
| **Mat. Overh. Cost Purch. Items** | Material overhead costs added to purchased components (depending on setup and template percentage). |
| **Capacity Cost** | Costs of the production capacity used, from the operations. |
| **Cap. Overhead Cost** | Capacity overhead costs. |
| **Mfg. Overhead Cost** | Production overhead costs. |
| **Subcontrd. Cost** | Costs of subcontracted work steps. |
| **Routing Scrap** | Cost portion of the scrap entered in the routing. |
| **Unit Cost** | Calculated unit cost (from the line with Usage Type **Unit Cost**); is written into the item when it is updated. |
| **Sales Price** | Calculated sales price (from the line with Usage Type **Sales Price**); is transferred into documents or price lists. |
| **Margin %** | Relative margin in percent between unit cost and sales price. |

#### Info area

| Field | Explanation |
|---|---|
| **Sim. Prod. Order** | Shows the number of the simulated production order kept in the background, from which the costs are determined (display only). |
| **Last Calculation Date** | Point in time of the last calculation (display only). |
| **Last Calculated By** | User of the last calculation (display only). |
| **Batch Calculation** | Indicates whether the calculation was created/updated within a **Batch Calculation** (display only). |

#### Post Calculation area

The **Post Calculation** compares the calculated values against the actual costs of a
**completed (finished) production order**. The user selects the
production order and the order line; the system determines the actual costs and writes them into
the post calculation fields.

| Field | Explanation |
|---|---|
| **Post Calc. Prod. Order** | Defines the completed production order against which the post calculation is performed. |
| **Post Calc. Prod. Order Line** | Defines the order line; on setting it, the system triggers the post calculation. If the item number of the line does not match the calculation, an error message appears. |
| **Post Calc. Material Cost** | Actual material cost per manufactured unit. |
| **Post Calc. Mat. Cost Without Scrap** | Actual material cost without scrap portion. |
| **Post Calc. Mat. Overh. Cost Purch. Items** | Actual material overhead costs for purchased components. |
| **Post Calc. Capacity Cost** | Actual capacity costs. |
| **Post Calc. Cap. Overhead Cost** | Actual capacity overhead costs. |
| **Post Calc. Mfg. Overhead Cost** | Actual production overhead costs. |
| **Post Calc. Subcontrd. Cost** | Actual subcontracting costs. |
| **Post Calc. Routing Scrap** | Actual routing scrap (from the capacity ledger entries). |

### Actions of the Calculation

The following actions are available in the calculation (the order corresponds to the
typical workflow).

| Action | Explanation |
|---|---|
| **Versions** | Opens the list of all versions of the calculation. |
| **Components** | Opens the page **Calculation Components** with the material components of the simulated production order (reservation, item availability, item substitution, and more). |
| **Routing Lines** | Opens the operations of the simulated production order; after editing, replanning and recalculation take place. |
| **Certify Calculation** | Sets the status to **Certified** and locks the values (see *Posting or Release Workflow*). |
| **Edit** | Opens the page **Calculation Edit**, on which the permitted fields (Description, Project, Quote, Reference, Internal Comment) can be changed even for certified calculations. |
| **Close Calculation** | Sets a certified calculation to **Closed**. |
| **Copy Calculation** | Copies an existing calculation into a new calculation (selection from the overview). |
| **Create New Version** | Creates a new version of the current calculation. |
| **Create Item** | Creates a new item from a certified calculation (see *Create Item*). |
| **Set Price in Item** | Writes the calculated **Sales Price** into the field **Unit Price** of the item card. |
| **Update Unit Cost** | Writes the calculated **Unit Cost** into the item and the associated stockkeeping data. |
| **Update Sales Price List** | Transfers the calculated **Sales Price** into the appropriate sales price lines (price list) within the validity period. |
| **Document Assignment** | Opens the **Calculation Doc. Assignments** with the linked documents. |
| **Set Sales Price in Documents** | Transfers the calculated **Sales Price** into the lines of the assigned, still open sales documents. |
| **Print** | Prints the **Calculation Report** entered in the setup (and, optionally, the **Prod. Order Report**). |

### Posting or Release Workflow (Certifying)

The module knows no document or inventory posting. The release and completion step is
**Certifying**, which locks the calculation and – depending on the setup – transfers the sales price into
the documents. The workflow (derived from the code):

1. Select a line in **Calculations** or open the calculation from the document.
2. Maintain values/lines and, if applicable, **Update Unit Cost**, until the calculation is
   calculated.
3. Choose **Certify Calculation**. Checks: the status must be **Under Development**, the
   calculation must be calculated, and there must be no components of type **Calculation**
   present (otherwise abort with a message). If further certified versions exist,
   the system asks whether these should be set to **Closed**.
4. If **Set Sales Price in Document = On Certified** is set in the setup, the system transfers
   the sales price automatically into the open assigned sales documents
   (hidden background process, no window).
5. After certification, depending on the need, **Set Price in Item**, **Update Unit Cost**,
   **Update Sales Price List**, **Set Sales Price in Documents** or
   **Create Item** are possible.
6. With **Close Calculation** the certified calculation is set to **Closed**.

### Create Item

From a **certified** calculation the user creates a real item together with its routing and
production BOM via **Create Item**. The dialog **Create Item** opens.

| Field | Explanation |
|---|---|
| **No.** | Number of the new item; via the assist edit a number series can be drawn. Locked if the item already exists. |
| **Description** / **Description 2** | Designation of the new item; is pre-filled from the calculation if the entry is empty. |
| **Create Item** (mark) | If enabled, a new item is created from the **Item Template**; if the item already exists, the mark is locked and the note **Item always created** appears. |
| **Item Template** | Defines the item template (configuration template) from which the master data is taken. Without a template, the creation is aborted with a message. |
| **Create Routing** (mark) | If enabled, a routing is created from the operations of the simulated production order; if the item already has a routing, the mark is locked (**Routing always created**). |
| **Create Prod. BOM** (mark) | If enabled, a production BOM is created from the components of the simulated production order; if one already exists, the mark is locked (**Prod. BOM always created**). |

After confirming with **OK** the system creates the item, transfers the unit cost and
replaces – if the calculation is used as a component in other calculations – the
calculation component there with the new item.

---

## Batch Calculation

The **Batch Calculation** serves the mass determination or update of unit costs via
the **Calculation Batch Journal**. It falls back on the **Batch Calculation Template**
entered in the **Calculation Setup**.

**Entry:** Open the **Calculation Batch Journal** (task page) via **Search**. The
journal is filtered per user.

**Procedure:**

1. **Collecting Calculations** — collects the items to be calculated into batch lines (including
   BOM level and relations).
2. Per line, choose the **Action** (see option values) and, if applicable, set **New Calculation Template**,
   **New Order Quantity** and further defaults.
3. **Check Line** — rechecks a line that is in error; via **Show Errors** and
   **Show Relations** details can be viewed.
4. **Calculate/Set Unit Cost** — performs the calculations for the batch lines and
   sets the unit costs.

Important fields of the batch line:

| Field | Explanation |
|---|---|
| **Error** | Indicates whether the line contains an error; an Action other than **None** is only permitted for an error-free line. |
| **Action** | Defines what is to happen with the line. For values see the option list below. |
| **Item No.** | The item to be calculated (display). |
| **Actual Calculation No.** / **Actual Calculation Version** | Refer to the currently valid calculation of the item. |
| **Calculation Template** / **New Calculation Template** | Previous template, or the template to be used for the new calculation. |
| **New Calculation No.** / **New Calculation Version** | Result of the batch processing. |
| **Unit Price** / **New Unit Price** / **Unit Price Difference** | Old and new unit cost as well as their difference. |
| **Has Relations** | Indicates whether the item is used as a component in other calculations. |

**Option values – Action:**

- **None:** The line is not processed.
- **New Version:** A new version of the existing calculation is created for the item.
- **New Calculation:** A completely new calculation is created for the item.

Via **Show Errors** the page **Calculation Batch Errors** opens with the respective
**Error Type**:

- **No BOM / No Routing:** No production BOM or
  routing is assigned to the item.
- **No Cert. BOM / No Cert. Routing:** No certified
  production BOM or certified routing exists.
- **Unit Cost Mismatch:** The sum of the individual costs does not correspond to the unit cost.
- **Unit Cost 0:** The determined unit cost is 0.
- **Costing Method (Item Ledger Entries):** The costing method is not "Standard" and
  item ledger entries exist.
- **Costing Method (Purchase Orders):** The costing method is not "Standard" and
  open purchase orders exist.

Via **Show Relations** the page **Calculation Batch Relations** opens the lines in
which the item is used as a component.

---

## Document Assignment

The **Calculation Doc. Assignments** link a calculation with the documents from which it
was created, or for which the price is to be set. They are created automatically during
**Create/Open Calculation** and are the basis for **Set Sales Price in Documents**.

**Entry:** In the calculation via the action **Document Assignment**.

| Field | Explanation |
|---|---|
| **Document** | Shows the designation of the assigned document (display). |
| **Document Type** | Shows the type of the assigned document (display). |
| **Document No.** | Number of the assigned document. |
| **Document Line No.** | Line number of the assigned document line. |
| **Assignment Date** | Date of the assignment. |
| **Expired** | If set, the assignment is no longer taken into account in the price transfer. |
| **Primary Source** | Indicates the original source line of the calculation. |

Actions: **Show Document** opens the assigned document; via **Functions** further document lines can be
linked manually with the calculation using **Sales Quote Line Assignment** or
**Sales Order Line Assignment**.

---

## Report and Outputs

Via the action **Print** (in the **Calculation** and in the list **Calculations**) the
**Calculation Report** entered in the **Calculation Setup** is output. If, in addition, a
**Prod. Order Report** is entered, this is also printed for the simulated production order. Via
the setup marks **Show Request Page Calculation** and **Show Request Page Prod. Order**
the administrator controls whether the respective request page appears before printing. The
calculation report contains the calculation lines and – via the option **Print Comments** –
optionally the entered comments.

---

## FAQ and Troubleshooting

### Why can no calculation be created?
Without an entered **Calculation Nos.** (number series) as well as **Dummy Item No.** and
**Dummy Routing No.** in the **Calculation Setup**, the creation is aborted, because the module
creates a simulated production order with item and routing in the background. Maintain
these fields first.

### Why is no calculation template proposed when opening from the document?
The automatic pre-fill only takes effect if a suitable combination of **Template Type**
(Customer, Customer Price Group or All Customers) and **Template Subtype** (Item or All Items)
with a **Calculation Template** is entered in the **Calculation Template Defaults**.
If a default is missing, select the template in the calculation manually.

### What happens if I change the calculation template in an existing calculation?
The system points out that the existing calculation lines are deleted, and, after
confirmation, recreates the lines from the new template. Confirm only if you want to discard the
previous scheme.

### Why can I not certify the calculation?
Certifying requires that the status is **Under Development** and that the calculation
has been calculated. If the simulated production order contains components of type **Calculation**,
the system aborts the certification; resolve these components first (e.g. via
**Create Item**).

### Why does the system report that the sum does not correspond to the unit cost?
When updating the unit cost, the system checks whether the sum of the individual costs (including
the lines assigned via **Assigned to Calculated Value**) corresponds to the shown **Unit Cost**.
If it deviates, correct the assignment of the manual lines in the
calculation template.

### Why is the unit cost 0 and the update fails?
If the calculated **Unit Cost** is 0, **Update Unit Cost** aborts with a message.
Check whether operations and components are present and whether the line with Usage Type
**Unit Cost** is filled correctly.

### How is the sales price set automatically into the sales order?
Set the field **Set Sales Price in Document** in the **Calculation Setup** to
**On Certified**. When certifying, the system writes the sales price into the lines of the
assigned, still open sales documents. Alternatively, use **Set Sales Price in
Documents** at any time.

### Why is the price not updated in an already released/posted document?
The sales price is only transferred into assigned sales documents whose status is **open**.
If the document is no longer open, the price remains unchanged.

### What does "Multilevel Calculation" do?
With **Multilevel Calculation** enabled, the system first calculates the multilevel
standard unit cost of the item via the BOM and uses it as the basis of the
material costs. Without the mark, the material costs originate directly from the simulated
production order.

### Can I delete the simulated production order?
No. The simulated production order cannot be deleted as long as its basis is a
calculation. Instead, delete the calculation; the associated simulated
production order is removed with it. A certified calculation cannot be deleted.

---

## Typical Use Cases

### 1. Calculation from the Sales Order

**Trigger:** A customer requests an item to be manufactured; Sales has already entered a
sales order with item and quantity and needs a reliable sales price.

**Entry in BC:** The user opens the **Sales Order**, marks the line and chooses
**Line → Functions → Create/Open Calculation**. A new **Calculation** opens with
pre-filled **Item No.**, **Contact No.** (customer of the order) and – if a default
exists – a pre-filled **Calculation Template**.

**Core procedure:**
1. If required, adjust **Calculation Template**, **Order Quantity** and **Tool Cost**.
2. In the **Lines** maintain the manual values/percentages; the system calculates the unit cost and
   sales price continuously.
3. **Certify Calculation**.
4. **Set Sales Price in Documents** (or – with the setup **On Certified** – automatically)
   transfers the sales price into the order line.

**Conclusion:** The sales order contains the calculated sales price; via **Print** the
calculation report can be output.

### 2. Calculation from the Sales Invoice (price only in the invoice)

**Trigger:** The sales price is to be set definitively only in the sales invoice, because it
results from the calculation.

**Entry in BC:** In the line of the **Sales Invoice** the user chooses
**Line → Functions → Create/Open Calculation**.

**Core procedure:**
1. Maintain the calculation and have it calculated.
2. **Certify Calculation**.
3. **Set Sales Price in Documents** transfers the calculated sales price into the open
   invoice line.

**Conclusion:** The sales invoice carries the calculated sales price; the **Document Assignment**
documents the link between the calculation and the invoice line.

### 3. Mass update via the Batch Calculation

**Trigger:** After changed material or capacity costs, the unit costs of several
manufactured items are to be re-determined.

**Entry in BC:** The user opens the **Calculation Batch Journal** via **Search**.

**Core procedure:**
1. **Collecting Calculations** fills the batch lines.
2. Per line, set the **Action** (**New Version** or **New Calculation**) and the **New
   Calculation Template**.
3. Clear errors via **Check Line**, **Show Errors** and **Show Relations**.
4. **Calculate/Set Unit Cost** performs the calculations and updates the
   unit costs.

**Conclusion:** The new unit costs are on the items; the column
**Unit Price Difference** documents the change per line.
