---
title: Anwenderhandbuch m+m Own Delivery Rating
---

# m+m Own Delivery Rating User Guide

## Introduction

The **Own Delivery Rating** extension lets you systematically monitor your own delivery performance toward your customers and represent it in a traceable rating. It is based on two factors that you can freely activate and weight: the **delivery delay** (deviation of the posting date from the agreed delivery date) and the **return orders** (posted sales return orders). From the **Own Delivery Rating Entries** that are captured automatically with every document posting, the module calculates a score per customer and period and converts it into a **Rating** through a freely defined rating system.

The primary target group is **operational users** who record and post sales orders, warehouse shipments, and sales return orders on a daily basis: they see the **Delivery Status** (On Time, Delay, Too Early) directly in the document line and trigger the data capture by posting. The secondary target group is administrators and analysts who set up the rating system (setup, rating system, delay criteria) and who periodically calculate and post in the worksheet.

Short process overview: In the **Own Delivery Rating Setup**, the administrator defines which factors are included, defines the **Own Delivery Rating System** (point bands) and – when the delivery delay is active – the **Delivery Delay Criteria**. On the **Customer Card**, the administrator flags the customers to be rated. In day-to-day business, entries are created automatically when documents are posted. Periodically, the user calculates and posts the ratings in the **Own Delivery Rating Worksheet**; the results are then available on the Customer Card and in the history lists. Optionally, a **Vendor External Rating** can also be recorded to compare the internal and external views.

## Quick Start for Users

The following procedure leads to the first rating result in the order enforced by the code (setup before use).

1. Open the **Own Delivery Rating Setup** (via **Search**): Under **Factors for Own Delivery Rating Calculation**, activate at least one factor – **Delivery Delays** and/or **Return Orders**. When **Delivery Delays** is active, select a **Delivery Date**; when **Return Orders** is active, enter the **Return Orders Points** (value greater than 0).
2. Use the **Delivery Rating System** action to create the point bands: for each line **Rating Code**, **Description**, **Points From**, **Points To** – gapless and non-overlapping.
3. Only when the delivery delay is active: use the **Delivery Delay Criteria** action to create the delay classes (**Code**, **Days of Delay From**, **Days of Delay To**, **Points**).
4. On the **Customer Card** of the customers to be rated, set the **Included in Rating System** field to **Yes**.
5. Post documents as usual (**Sales Order**, **Warehouse Shipment**, **Sales Return Order**). Posting automatically creates **Own Delivery Rating Entries**.
6. Open the **Own Delivery Rating Worksheet** (via **Search**), optionally set the **Customer Filter** and **Period Filter**.
7. Run the **Calculate Own Delivery Ratings** action: the worksheet is filled with the included customers and determines the **Total Amount of Points** and **Calculated Rating**.
8. Run the **Post** action and confirm the prompt *"Do you want to post the ratings?"* with **Yes**. The ratings are archived per customer as **Own Delivery Rating** and are visible on the Customer Card.

## Setup

The **Own Delivery Rating Setup** is the central, company-wide setup page (one record per company). It is created automatically the first time it is opened. Because the page carries the *Administration* category, it can be found via **Search**; there is no higher-level list page.

**Entry point:** open the **Own Delivery Rating Setup** page via **Search**.

The setup controls the entire module: it defines **which** factors are included in the rating, **which** delivery date is used for the delay calculation, and **how** return orders are scored. From here you reach the two dependent setup pages (rating system, delay criteria) via actions. Only afterward does day-to-day business show the **Delivery Status** and create entries when posting (see **Daily Work** and **Calculating and Posting the Rating**).

### Factors for Own Delivery Rating Calculation

Who sets this up: administrator/key user, once before first use. This page decides whether the module collects data at all and which additional fields appear in the documents.

| Setup | Explanation |
|---|---|
| **Delivery Delays** | When set to **Yes**, the module includes delivery delays in the rating: the **Delivery Status** field appears in sales order and warehouse shipment lines, entries of type **Delays** are created when posting, and the **Delivery Date** field and the **Delivery Delay Criteria** become active. Without this flag, no delay is captured and the associated actions/columns remain hidden. |
| **Delivery Date** | Defines against which date the posting date is compared when **no** promised delivery date is stored in the sales line. If you select a value here, it determines the delay calculation for all affected lines. Only visible/relevant when the delivery delay is active (mandatory). See values below. |
| **Return Orders** | When set to **Yes**, an entry of type **Return Order** is created whenever a **Sales Return Order** of a rated customer is posted, and the **Return Orders Points** deducted in the process are included in the rating. Without this flag, return orders remain rating-neutral. |
| **Return Orders Points** | When a value (> 0) is set, it is used as a **deduction** per posted sales return order (in the entry with a negative sign) – regardless of the number of document lines. The value must be greater than 0; otherwise the message *"Return order points value should be greater than 0."* appears. Only visible/relevant when return orders are active. |

**Delivery Date – possible values** (only when the delivery delay is active, used when no promised delivery date is present):

- **Planned Delivery:** the delay is calculated against the planned delivery date of the sales line.
- **Planned Shipment:** the delay is calculated against the planned shipment date.
- **Shipment:** the delay is calculated against the shipment date.
- **Requested Delivery:** the delay is calculated against the requested delivery date.

If a **promised delivery date** is maintained in the sales line, it always takes precedence; the **Delivery Date** setting then does not apply.

**Process steps of the basic setup:** First, activate the desired factors; then – depending on the selection – create the **rating system** and (for the delivery delay) the **delay criteria**; finally, flag the customers on the **Customer Card**. Dependent settings that are not filled in distort the calculation results.

### Setting Up the Delivery Delay Rating

This end-to-end configuration chain activates the rating by delivery performance. It is created by the administrator before first use and is consumed in day-to-day business through the automatic entry capture when posting sales orders and warehouse shipments (see **Daily Work**).

1. In the **Own Delivery Rating Setup**, set the **Delivery Delays** field to **Yes**. When activated, the **Delivery Date** field and the **Delivery Delay Criteria** action are enabled and the **Delivery Status** appears in the document lines.
2. Select the **Delivery Date**. When set, it determines the reference for the delay calculation, provided that no promised delivery date is present in the line.
3. Use the **Delivery Rating System** action to define the point bands (see **Own Rating System**). When created, a **Rating** can be derived from the total amount of points.
4. Use the **Delivery Delay Criteria** action to create the delay classes (see **Delivery Delay Criteria**). When created, each delay span receives its associated points.
5. On the **Customer Card**, set **Included in Rating System** to **Yes** for each customer. When activated, delay entries are captured for this customer when posting.

Operational conclusion of the chain: When posting a sales order or warehouse shipment for a rated customer, an **Own Delivery Rating Entry** (type **Delays**) is created automatically; the evaluation takes place in the **Own Delivery Rating Worksheet**.

#### Own Rating System

**Entry point:** in the **Own Delivery Rating Setup**, choose the **Delivery Rating System** action (the **Own Delivery Rating System** page cannot be found via **Search**).

Who sets this up: administrator/key user, before the first rating. The rating system translates a customer's collected **Total Amount of Points** into a meaningful **Rating**. It applies to both factors jointly and is used by both the delivery delay rating and the return order rating.

| Field | Explanation |
|---|---|
| **Rating Code** | Unique code of the rating (e.g. a grade or level). When set, this code is carried as the result in the rating pages and on the Customer Card. Must not be empty. |
| **Description** | Plain text for the rating. When maintained, it helps the user classify the rating value. |
| **Points From** | Lower limit of the point band. When set, the rating applies from this score. Must not be less than 0 and not greater than **Points To**; otherwise the messages *"Amount of points can not be less than 0."* or *"Minimal rating points value can not be higher than maximum points value."* appear. |
| **Points To** | Upper limit of the point band. When set, the rating applies up to this score. Must be filled (mandatory when creating) and must not be less than **Points From**. |

Dependency note: When creating and changing, the system checks that the bands **do not overlap** and connect to each other **gaplessly**; otherwise *"Points values have to be out of existing ranges."* or *"Ratings should be specified sequentially."* appears. If a total amount of points falls outside all bands, the nearest boundary band is used.

#### Delivery Delay Criteria

**Entry point:** in the **Own Delivery Rating Setup**, choose the **Delivery Delay Criteria** action (the **Own Delivery Delay Criteria** page cannot be found via **Search** and is available only when the **Delivery Delays** is active).

Who sets this up: administrator/key user, before first use, as soon as the delivery delay is active. Here you assign a point value to each span of delay days. Based on these criteria, each delay entry created when posting receives its **Rating Points** and its criterion code.

| Field | Explanation |
|---|---|
| **Code** | Unique code of the delay class. When set, this code is carried on the created entry and in the **Delivery Delay Statistics**. Must not be empty. |
| **Description** | Plain text for the delay class. When maintained, it makes classification in analyses easier. |
| **Days of Delay From** | Lower limit of the delay span in days. When set, the class applies from this number of days. Negative values mean "too early", 0 means "on time", positive values mean "delay". Must not be greater than **Days of Delay To**. |
| **Days of Delay To** | Upper limit of the delay span in days. When set, the class applies up to this number of days. Must not be less than **Days of Delay From**; otherwise *"Minimal days of delay value can not be higher than maximum days of delay value."* appears. |
| **Points** | Point value that is credited to or deducted from the customer for entries of this delay class. When set, it is included in the averaging of the delivery delay points (early/on-time deliveries can be scored positively, delays negatively – depending on your point assignment). |

Dependency note: As with the rating system, the day spans must be **non-overlapping** and **gapless** (same check messages). If the calculated delay falls outside all spans, the nearest boundary criterion is used.

### Setting Up the Return Order Rating

This configuration chain activates the second rating factor. It is created by the administrator before first use and is consumed in day-to-day business by posting **Sales Return Orders** of rated customers.

1. In the **Own Delivery Rating Setup**, set the **Return Orders** field to **Yes**. When activated, the **Return Orders Points** field is shown and entries of type **Return Order** are created when posting sales return orders.
2. Enter the **Return Orders Points** (> 0). When set, this amount is deducted from the customer's point account per posted sales return order.
3. Use the **Delivery Rating System** action to create the point bands (shared use with the delivery delay rating, see **Own Rating System**).
4. On the **Customer Card**, set **Included in Rating System** to **Yes** for each customer. When activated, return order entries are captured for this customer.

Operational conclusion of the chain: When posting a sales return order of a rated customer, an **Own Delivery Rating Entry** (type **Return Order**) is created with the negative return order point value; the evaluation takes place in the worksheet.

### Permissions

The module provides an assignable permission set for the own delivery rating (technical identifier `MuM OR Own Deliv Rat`). It determines the permissions for the module tables and pages (read/write rights on setup, rating system, criteria, entries, worksheet, ratings, and vendor external ratings, as well as execute rights on the associated codeunits). Assign it to all users who post documents of rated customers or calculate ratings. A valid license of the base solution **m+m Cloud Base** is a prerequisite for operation; the license check is performed automatically at sign-in.

## Master Data

### Customer Card: Including a Customer in the Rating

**Entry point:** open the customer via the **Customer List** and call up the **Customer Card**; the own delivery rating fields are located in the **Own Delivery Rating** group below the statistics.

Who maintains this: administrator/key user, per customer. The Customer Card is the master data location where you **select** which customers are rated at all – not every customer has to be included in the system. Whether the **Delivery Status** appears in the documents, whether entries are created when posting, and whether the customer is included in the worksheet all depend on this flag.

| Field | Explanation |
|---|---|
| **Included in Rating System** | When set to **Yes**, the customer is included in the own delivery rating: the **Delivery Status** appears in their sales order and warehouse shipment lines, entries are created when posting their documents, and they are considered in the worksheet. With **No**, no more rating data is captured for them and the additional fields/actions remain inactive. |
| **Rating** | Shows the most recently calculated and posted own delivery rating of the customer (not editable). Only visible when the customer is included in the rating system. |
| **Rating Period** | Shows the period of the most recently posted rating (not editable). |
| **Vendor External Rating** | Shows the most recently recorded external rating of the customer (not editable) – to compare the internal view with the external view. |
| **Vendor External Rating Period** | Shows the period of the most recently recorded external rating (not editable). |

The Customer Card also gives you access to the customer's history and comparison pages (actions **Own Delivery Ratings** and **Vendor External Ratings**, both active only when **Included in Rating System = Yes**). These are described under **History and Comparison**. The flag is the shared prerequisite of both setup chains (**Setting Up the Delivery Delay Rating**, **Setting Up the Return Order Rating**).

## Daily Work on Sales Documents

In day-to-day business, users do not need to record anything extra: the own delivery rating is closely tied to sales processing. For rated customers, the module shows the **Delivery Status** in the document lines and automatically creates the **Own Delivery Rating Entries** when posting. Which factors are captured is controlled by the **Own Delivery Rating Setup** (Delivery Delays, Return Orders); who is rated is controlled by the **Customer Card** (Included in Rating System).

### Delivery Status in the Sales Order Line

If the customer is included in the rating system and the **Delivery Delays** is active, the sales order line shows the additional column **Delivery Status**. It is re-determined automatically when opening and when changing the relevant date fields (**Planned Delivery Date**, **Planned Shipment Date**, **Shipment Date**, **Promised Delivery Date**, **Requested Delivery Date**) as well as the **Location Code**.

| Field | Explanation |
|---|---|
| **Delivery Status** | If the posting date is expected to be later than the governing delivery date, the line shows **Delay**; if it is earlier, it shows **Too Early**; if both match, it shows **On Time**. The governing date is the **Promised Delivery Date**, alternatively the **Delivery Date** selected in the setup. If the location requires a warehouse shipment, the field remains empty, because the status is then determined at the warehouse shipment. |

Values of the delivery status:

- **On Time:** the posting date matches the governing delivery date – no delay.
- **Delay:** the posting date is after the governing delivery date – the delivery is late.
- **Too Early:** the posting date is before the governing delivery date – the delivery is made ahead of schedule.

### Delivery Status in the Warehouse Shipment

If the location requires a warehouse shipment, the delivery status remains empty in the sales order line and is instead shown in the **Warehouse Shipment** line (column **Delivery Status**, same values **On Time**, **Delay**, **Too Early**). The governing date here is the **posting date of the warehouse shipment** relative to the governing delivery date of the associated sales order line. If the **Posting Date** is changed in the warehouse shipment header, the display is updated.

### Automatic Capture of Entries When Posting

When posting sales documents of rated customers, the module creates the **Own Delivery Rating Entries** – without any further input:

1. **Posting a sales order** (without a warehouse shipment requirement at the location): if **Delivery Delays = Yes**, the delay is calculated for each sales line and an entry of type **Delays** is written.
2. **Posting a warehouse shipment** (at a location that requires a warehouse shipment): the delay entry is instead created at the warehouse shipment (based on the warehouse shipment posting date). If the associated sales order line is posted afterward, **no** second entry is created – this avoids duplicate capture.
3. **Posting a sales return order**: if **Return Orders = Yes**, an entry of type **Return Order** with the negative **Return Orders Points** is written per document (regardless of the number of lines; the source document line number is always 0 here).

All data captured in this way can be viewed in **Own Delivery Rating Entries** and forms the basis for the calculation in the worksheet.

### Own Delivery Rating Entries

**Entry point:** open the **Own Delivery Rating Entries** page via **Search**; or by drill-down from the worksheet and the Customer Card. The page is not editable and serves to trace the captured data.

| Field | Explanation |
|---|---|
| **Customer No.** | Customer to which the entry belongs. |
| **Document Type** | Source document type of the entry. See values below. |
| **Document No.** | Number of the source document (sales order, warehouse shipment, or sales return order). |
| **Source Doc. Line No.** | Line of the source document. For sales order/warehouse shipment, filled per line; for sales return order, always 0, because it is calculated per document. |
| **Posting Date** | Posting date of the source document. |
| **Rating Criteria Type** | Type of the rating criterion. See values below. |
| **Delay Days** | Number of delay days (only for type **Delays**): negative value = too early, 0 = on time, positive value = delay. |
| **Rating Points** | Points added or deducted during the calculation. |
| **Entry No.** | Consecutive, unique entry number (technical sorting, hidden by default). |

**Document Type – possible values:**

- **(blank):** no source type set (technical initial value; not used for created entries).
- **Sales Order:** the entry originates from a posted sales order.
- **Sales Return Order:** the entry originates from a posted sales return order.
- **Warehouse Shipment:** the entry originates from a posted warehouse shipment.

**Rating Criteria Type – possible values:**

- **Delays:** the entry rates a delivery delay; **Delay Days** and the delay class (**Delivery Delay**) are filled.
- **Return Order:** the entry rates a sales return order; the **Rating Points** contain the negative return order deduction.

## Calculating and Posting the Rating

The periodic rating is performed in the **Own Delivery Rating Worksheet**. It reads the **Own Delivery Rating Entries**, condenses them per customer and period into a **Total Amount of Points**, derives the **Calculated Rating** from it, and archives the results as **Own Delivery Rating** when posting. Which factors are included and which columns are visible depends on the **Own Delivery Rating Setup**.

**Entry point:** open the **Own Delivery Rating Worksheet** page via **Search**.

### Filters

Before the calculation, you limit the included customers and the evaluation period.

| Filter field | Explanation |
|---|---|
| **Customer Filter** | When set, only the selected customers that are included in the rating system are taken into the worksheet. Via the AssistEdit button (three dots), customers can be selected from the customer list (only rated customers). Without a customer filter, all included customers are included in the calculation. |
| **Period Filter** | When set, only entries with a posting date in this period are included in the averaging and summation as well as in the factbox. The period also determines the **Rating Period From/To** of the posted rating. |

### Worksheet Lines

| Field | Explanation |
|---|---|
| **Customer No.** | Customer of the worksheet line (only rated customers can be selected). |
| **Customer Name** | Name of the customer (adopted automatically). |
| **Latest Rating** | Most recently posted rating of the customer (not editable) – to compare with the new result. |
| **Calculated Rating** | Rating newly determined for the selected period (not editable); set by **Calculate Own Delivery Ratings**. |
| **Avg. Points (Delivery Delays)** | Average of the rating points from delay entries in the period. Only visible when **Delivery Delays = Yes**. Via drill-down, the underlying entries can be displayed. |
| **Sum Points (Return Orders)** | Sum of the rating points from return order entries in the period (always a negative value). Only visible when **Return Orders = Yes**. Via drill-down, the underlying entries can be displayed. |
| **Total Amount of Points** | Result of **Avg. Points (Delivery Delays) + Sum Points (Return Orders)** (each summand only for an active factor). From this value, the **Calculated Rating** is determined via the rating system. |

### Factbox "Delivery Delay Statistics"

To the right of the worksheet lines, the **Delivery Delay Statistics** factbox shows, for the selected customer, how their delay entries are distributed across the criteria in the selected period.

| Field | Explanation |
|---|---|
| **Delivery Delay** | Delay class (code from **Delivery Delay Criteria**). |
| **Number of Entries** | Number of delay entries of this class in the period. Via drill-down, the associated **Own Delivery Rating Entries** are displayed. |

### Posting Procedure

The calculation and posting procedure corresponds to the Quick Start and is expanded on here (Quick Start steps 6–8 mirror this numbering):

1. Open the **Own Delivery Rating Worksheet**.
2. Set the **Customer Filter** and/or **Period Filter** (optional; without a customer filter, all included customers are taken into the calculation).
3. Run the **Calculate Own Delivery Ratings** action: if there are no lines yet, all included customers are inserted; afterward, the **Total Amount of Points** and **Calculated Rating** are determined for each line.
4. Run the **Post** action. The prompt *"Do you want to post the ratings?"* appears. With **Yes**, an **Own Delivery Rating** record (rating period from/to, rating) is archived for each line that has entries in the period, and the worksheet line is removed. Lines without entries in the period are not posted and are logged with *"There is nothing to post for %1 Customer."*. After successful posting, *"Own Delivery ratings are posted."* appears.

There is no intermediate posting document and no partial posting: posting transfers all existing worksheet lines directly into the rating archive. A customer cannot be rated more than once for an identical period.

## History and Comparison

The posted ratings and the captured raw data are permanently available for traceability; in addition, external ratings can be recorded for comparison.

### Own Delivery Ratings (Posted Ratings)

**Entry point:** on the **Customer Card** of a rated customer, choose the **Own Delivery Ratings** action (active only when **Included in Rating System = Yes**).

| Field | Explanation |
|---|---|
| **Rating Period From** | Start of the period for which the rating was posted. |
| **Rating Period To** | End of the period for which the rating was posted. |
| **Rating** | The own delivery rating determined for this period. |

Via the **Own Delivery Rating Entries** action, you jump from a rating to the underlying entries of the respective period (active only when records exist).

### Vendor External Ratings

**Entry point:** on the **Customer Card** of a rated customer, choose the **Vendor External Ratings** action (active only when **Included in Rating System = Yes**).

Here you record externally determined ratings of the same customer in order to compare the internally calculated own delivery rating with the external view. The fields correspond to those of the posted ratings.

| Field | Explanation |
|---|---|
| **Rating Period From** | Start of the period of the external rating. |
| **Rating Period To** | End of the period of the external rating. |
| **Rating** | Externally assigned rating (rating code from your own rating system). |

The most recently recorded external rating additionally appears on the Customer Card in the **Vendor External Rating** and **Vendor External Rating Period** fields.

## FAQ and Troubleshooting

### Why does no Delivery Status appear in the sales order line?

The **Delivery Status** is only shown when the customer has **Included in Rating System = Yes** on the Customer Card **and** the **Delivery Delays** is active in the **Own Delivery Rating Setup**. If the location of the line additionally requires a warehouse shipment, the field remains empty in the order line – the status then appears in the warehouse shipment line.

### Why are no Own Delivery Rating Entries created when posting?

Entries are only created for customers with **Included in Rating System = Yes** and only for active factors: delay entries require **Delivery Delays = Yes**, return order entries require **Return Orders = Yes**. If neither factor is active or the customer is not included, the posting remains rating-neutral.

### Why is a delay entry not created at the sales order but only at the warehouse shipment?

If the location of the sales line requires a warehouse shipment, the module skips the capture at order posting and creates the entry when posting the warehouse shipment (with the warehouse shipment posting date). This prevents a duplicate capture when the order line is posted afterward.

### Which date is used for the delay calculation?

The **Promised Delivery Date** of the sales line takes precedence. If it is empty, the module uses the date selected in the **Own Delivery Rating Setup** under **Delivery Date**: **Planned Delivery**, **Planned Shipment**, **Shipment**, or **Requested Delivery**. The delay is the difference between the posting date and this date.

### What do negative delay days mean?

The **Delay Days** result from the posting date minus the governing delivery date. A **negative** value means "too early", **0** means "on time", a **positive** value means "delay". Via the **Delivery Delay Criteria**, you assign points to each span.

### Why can the rating system not be saved ("ranges" / "sequentially")?

The point bands in the **Own Delivery Rating System** must be non-overlapping and gapless. If bands overlap, *"Points values have to be out of existing ranges."* appears; if a gap arises, *"Ratings should be specified sequentially."* appears. Adjust **Points From/To** so that the bands connect directly to each other.

### Why am I not allowed to enter negative or excessively large point limits?

In the rating system, **Points From** must not be less than 0 (*"Amount of points can not be less than 0."*) and not greater than **Points To** (*"Minimal rating points value can not be higher than maximum points value."*). **Points To** is also a mandatory entry when creating. These rules ensure a consistent assignment of the total amount of points.

### Why does posting report "There is nothing to post for … Customer"?

A worksheet line is only posted when **Own Delivery Rating Entries** actually exist for the customer within the selected **Period Filter**. If entries are missing (e.g. wrong period or no posted documents), the line is skipped and the note is logged. Check the period and the existing entries.

### Why can I not post a second rating for the same period?

The key of the posted **Own Delivery Rating** consists of the customer and the rating period. A customer can therefore not be rated more than once for an identical period. Select a different period or clean up the existing rating.

### Why are the columns "Avg. Points (Delivery Delays)" or "Sum Points (Return Orders)" not visible?

These columns and their contribution to the **Total Amount of Points** depend on the setup factors: the delay column appears only when **Delivery Delays = Yes**, the return order column only when **Return Orders = Yes**. Activate the respective factor in the **Own Delivery Rating Setup**.

## Typical Use Cases

The following scenarios show realistic triggers and the chronological procedure in Business Central. All steps are covered by the module logic.

### Scenario 1: Quarterly Rating of a Customer

**Trigger:** At the end of the quarter, the delivery performance toward a key customer is to be evaluated and documented.

**Entry point in BC:** Open the **Own Delivery Rating Worksheet** via **Search**.

**Core procedure:**
1. Set the **Customer Filter** to the customer in question and the **Period Filter** to the quarter.
2. Run the **Calculate Own Delivery Ratings** action. The worksheet shows **Avg. Points (Delivery Delays)**, **Sum Points (Return Orders)**, **Total Amount of Points**, and **Calculated Rating**; the **Delivery Delay Statistics** factbox breaks down the delay classes (drill-down via **Number of Entries**).
3. Run the **Post** action and confirm *"Do you want to post the ratings?"* with **Yes**.

**Conclusion:** The rating appears under **Own Delivery Ratings** and on the **Customer Card** (fields **Rating**, **Rating Period**).

### Scenario 2: Late Warehouse Shipment in Location-Managed Processing

**Trigger:** Logistics reports that a delivery to a rated customer left the warehouse only after the promised date.

**Entry point in BC:** Open the customer's **Sales Order**; because the location requires a warehouse shipment, the **Delivery Status** in the order line is empty and is carried in the **Warehouse Shipment**.

**Core procedure:**
1. In the **Warehouse Shipment**, check the line: the **Delivery Status** shows **Delay** when the warehouse shipment posting date is after the governing delivery date.
2. Post the warehouse shipment. In the process, an **Own Delivery Rating Entry** of type **Delays** is created automatically with the determined **Delay Days** and the points of the matching delay class.

**Conclusion:** The entry is visible in **Own Delivery Rating Entries** and flows into the next quarterly calculation. A later posting of the associated order line does not create a second entry.

### Scenario 3: Return Order of a Rated Customer

**Trigger:** A customer reports faulty goods; a sales return order is recorded.

**Entry point in BC:** Record and post the customer's **Sales Return Order** (prerequisite: **Return Orders = Yes** and **Return Orders Points** maintained).

**Core procedure:**
1. Post the sales return order. Exactly one **Own Delivery Rating Entry** of type **Return Order** with the negative **Return Orders Points** is created – regardless of the number of lines.
2. At the next calculation in the worksheet, this entry reduces the customer's **Total Amount of Points** via **Sum Points (Return Orders)**.

**Conclusion:** The worsened rating is archived at the next **Post** and is traceable on the Customer Card; via drill-down in the worksheet, the triggering return order entry can be displayed.
