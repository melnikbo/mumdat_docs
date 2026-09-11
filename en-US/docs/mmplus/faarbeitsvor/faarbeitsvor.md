---
title: Anwenderhandbuch m+m Production Order Job Overview
---

# User Guide m+m Production Order Job Overview

This guide describes how to operate the **m+m Production Order Job Overview** app (referred to throughout the user interface as **Prod. Order Job Overview**) in Microsoft Dynamics 365 Business Central. It is aimed at users who work with the job overview every day, as well as key users and administrators who set the app up. All page, field, and action names correspond to the English user interface.

## Introduction

The **Prod. Order Job Overview** app extends production execution with a work-center-based job overview for released production orders. It bundles the open and running operations of a **Work Center** (or a **Machine Center**) into a single work list and lets you control the processing status directly from that list: **Setup Activity**, **Start**, **Interrupt**, **Partially Finish**, **Finish**, and **Set To Open**. Time and quantity postings are made via the posting page, material movements can be prepared as a **Transfer**, and every action is logged in the event history.

**Target audience.** The primary audience is **operational production users** – workers, shift leads, and production planners who start, post, and finish operations. Secondarily, the guide is aimed at key users and administrators who maintain the global **Prod. Order Job Setup** and the **Prod. Order Job Work Center Setup**.

**Typical process flow.** Entry follows a fixed chain: **select a Work Center** (mandatory filter) → optionally narrow by **Machine Center**, **production order**, or **date** → **select a line** → **run a process action** (Setup Activity/Start/Interrupt/Partially Finish/Finish) → for a time or quantity posting, complete the **Prod. Order Job Posting** page. Before first use, administrators maintain the global setup, the work center setup per work center, and the master data **Prod. Order Job Inter. Reasons** and optionally the description schema.

## Quick Start for Users

Order of steps: first the **setup** (performed by the administrator/key user), then the work list, then the process actions.

### Ensure Setup Is in Place (one-time, prerequisite)

1. Using **Search**, open the **Prod. Order Job Setup** page and check the defaults for sequence, refresh after actions, archiving, and the traffic-light colors.
2. Open the **Work Center Card** of the relevant work center and choose the **Prod. Order Job Setup** action to maintain the **Prod. Order Job Work Center Setup** (time posting, setup activity, transfer, sorting).
3. Under **Prod. Order Job Inter. Reasons**, create the interruption reasons you need.

### Open the Job Overview and Process an Operation

1. Using **Search**, open the **Prod. Order Job Overview** page.
2. In the **Work Center No.** field, select the work center you are working for. (The **Work Center Name** is displayed automatically.)
3. Optionally narrow the results further using **Machine Center No.**, **Prod. Order No.**, and **Date**.
4. Run **Update Data** if needed so that the lines are recompiled.
5. Check the selected line (description, **Status**, **Previous Operation Status**, **Operation No.**, quantities).
6. If **Setup Activity** is active for the work center: run the **Setup Activity** action (status **Setup**).
7. Run the **Start** action (status **Started**).
8. If an interruption is required: run the **Interrupt** action and choose an entry from **Prod. Order Job Inter. Reasons** (status **Interrupted**).
9. For a partial quantity: run the **Partially Finish** action (status **Partially Finished**). To complete: run the **Finish** action (status **Finished**).
10. If the action triggers a time or quantity posting, complete the **Prod. Order Job Posting** page with **OK**. If **Time Posting** is set to **None** or **Qty. based exp. Time**, a **Quantity** must be entered.

> Steps 6–10 correspond exactly to the posting and reporting flow (see **Posting and Reporting**) and are repeated in the **Typical Use Cases**.

### Getting Started with the Work Center Lights and History

1. Using **Search**, open the **Work Center Lights** page to see the latest state per work center as a traffic light.
2. From the line in the **Prod. Order Job Overview**, open the **Event History** action to trace postings and interruptions.

## Setup

Setup is the prerequisite for daily work and the most extensive configuration area of the app. It consists of a **global** setup card and a setup maintained **per work center**; several activation chains build on these and are described further below as their own subsections ("Set up …").

### Global Setup (Prod. Order Job Setup)

**Entry:** via **Search** → **Prod. Order Job Setup**. This is a company-wide setup card (one record per company). The card is created automatically the first time it is opened; a record does not need to be created manually. It is configured by the administrator/key user **before** the job overview is first used. The defaults stored here control sequence planning, reloading of the lines after actions (see **Daily Work**), transfer behavior, and the **Work Center Lights**.

**General** section:

| Setup | Explanation |
|---|---|
| Follow Prod. Order Sequence | If enabled, when the lines are collected the operation sequence stored in the production order is taken into account; without the flag, the display follows only the selected **Sort By**. |
| Automatic Sequence adjust | If enabled, when a **Sequence** that is already in use is assigned, the app automatically moves the affected lines back one position so that no duplicate sequence numbers arise; without the flag, the manual assignment stays unchanged. |
| Automatic Sequence on Finish | If enabled, when an operation is **Finished** the remaining open lines are automatically renumbered from 1 upward; without the flag, the existing sequence is retained. |
| Forced Sequence at Routing | If enabled, when you **Start** the app checks whether the previous operation has already been posted; if the posting is missing, the start is prevented with the message "There is no Posting on previous Operation." Without the flag, starting is allowed without this check. |
| Update Prod. Order Job Lines after Job Action | If enabled, the lines are recompiled immediately after a process action so that the user sees the current state; without the flag, the list stays unchanged until the next **Update Data** action. Controls which of the following action fields take effect at all. |
| Update Prod. Order Job Lines for All Actions | If enabled, the lines are reloaded after **every** action; without the flag, the individual action fields below take effect selectively. Editable only when "update after action" is set. |
| Update Prod. Order Job Lines after Setup Action | If enabled, the lines are reloaded specifically after the **Setup Activity** action. |
| Update Prod. Order Job Lines after Run Action | If enabled, the lines are reloaded specifically after the **Start** action. |
| Update Prod. Order Job Lines after Interrupt Action | If enabled, the lines are reloaded specifically after the **Interrupt** action. |
| Update Prod. Order Job Lines after Partially Finish Action | If enabled, the lines are reloaded specifically after the **Partially Finish** action. |
| Update Prod. Order Job Lines after Finish Action | If enabled, the lines are reloaded specifically after the **Finish** action. |
| Update Prod. Order Job Lines after Reopen Action | If enabled, the lines are reloaded specifically after the **Set To Open** action. |
| Set Quantity from Remaining for Transfer | If enabled, when the **transfer lines** are determined the app adopts the component's still-open remaining quantity as the proposed quantity; without the flag, the quantity is initially empty and must be entered manually. |
| Collect Job Line by Query | If enabled, the job overview lines are determined via the internal query of the existing lines (faster compilation); without the flag, collection uses the full iteration method. |
| Archive finished Lines | Defines whether and when finished lines are archived. **Never:** no archiving; finished lines remain in the active lists. **Finished Prod. Order:** as soon as the production order reaches the status "Finished", the associated job overview lines together with their events and transfer lines are moved to the archive (see **History and Archive**). |

**Traffic-Light Add-In** section (controls the **Work Center Lights**):

| Setup | Explanation |
|---|---|
| Refresh Interval (sec) | Defines after how many seconds the **Work Center Lights** page automatically reloads the tiles; a small value keeps the lights more up to date but generates more frequent queries (minimum value 1, default 10). |
| Light 1 | Color value (hex) for the first traffic-light stage. When set, the machine center appears in the monitor in this color as soon as an interrupted operation does **not** release the follow-up process (default Red). |
| Light 2 | Color value (hex) for the second traffic-light stage. When set, the machine center appears in this color when there is no critical run status and only the last production order is displayed (default Yellow). |
| Light 3 | Color value (hex) for the third traffic-light stage. When set, the machine center appears in this color when an operation is actively **Started** (default Green). |

Using the **Interuption Reasons** action, you open the master data list **Prod. Order Job Inter. Reasons** directly from this card (see **Master Data**).

### Work Center Setup (Prod. Order Job Work Center Setup)

**Entry:** Open the **Work Center Card** (or the **Work Centers** list), select the relevant work center, and choose the **Prod. Order Job Setup** action. If no setup yet exists for the work center, the app asks "Setup for Work Center %1 does not exist. Create it?" and creates it upon confirmation. This page is **not** opened via **Search**; it is always bound to a specific work center.

This setup is maintained per work center by the key user and directly controls the behavior of the **Prod. Order Job Overview** and the **Prod. Order Job Posting** page for that work center: which actions are visible, how times are reported, whether material is transferred, and how the list is sorted and filtered.

| Setup | Explanation |
|---|---|
| Work Center Name | Displays the name of the selected work center (display only, read from the master record). |
| Unproductive | If enabled, the work center is flagged as unproductive; this serves to distinguish operations that are used only for reporting or control and do not post a productive quantity. |
| Start Multiple Jobs | If enabled, multiple operations may be in status **Started** at the same time at this work center; without the flag, the app prevents the start of another job as long as a job is still started or interrupted at the same machine center. |
| No Start-Action required | If enabled, a partial finish or finish may be done directly without a prior **Start**; without the flag, the app requires a started job before finishing. Cannot be set as long as **Time Posting** is **Standard**. |
| Sort By | Defines the default sorting of the job overview. **Sequence:** by the assigned work sequence; **Status:** grouped by processing state; **Prod. Item:** by the produced item; **Date:** by start date/time. The user can temporarily override the sorting in the job overview. |
| Time Posting | Controls which time entries can be edited on the **Prod. Order Job Posting** page and how the time is determined. **Standard:** start/end times are used; times are adopted from the event. **None:** the time fields are locked, but a **Quantity** is mandatory. **Expected Time:** setup time and run time are entered directly, date/time stay fixed. **Qty. based exp. Time:** the time is derived from the reported quantity, a **Quantity** is mandatory. **Manual:** setup time and run time are set manually; when "Start Date-Time Editable" is active, the start values can also be adjusted. |
| Post Only Duration | If enabled, the **Prod. Order Job Posting** page is not opened during reporting; the time is posted directly from the event, without detailed entry of start/end time and quantity. Can only be set together with **Time Posting** = **Standard** or **Expected Time**. |
| Setup Activity | If enabled, the **Setup Activity** action is shown in the job overview and a separate setup status change is enabled; without the flag, the separate setup step is omitted. |
| Transfer | If enabled, the **Transfer** action is shown in the job overview, and when you **Interrupt** or on completion the transfer lines are determined; without the flag, no material transfer takes place (see **Set Up Material Transfer**). |
| Start Date-Time Editable | If enabled, the user may change the start date and start time on the **Prod. Order Job Posting** page; without the flag, these fields are locked. |
| Deactivate Direct Search | If enabled, the lines are **not** collected automatically after a work center is selected; the user must deliberately run **Update Data**. Useful with very large job overviews to avoid unnecessary loading operations. |
| Show Sales Order No. | If enabled, the job overview shows the fields related to the sales context (**Sales Order No.**, **Sales Order Line No.**, **Shipping Agent Code**, **Shipping Agent Service Code**); without the flag, these columns stay hidden. |
| Show Times | If enabled, the job overview shows the time fields **Expected Time**, **Posted Time**, **Outstanding Time**, and **Time incl. Setup**; without the flag, these columns stay hidden. |

Also present, but hidden in the interface and without effect on the core app: **Initialise Output Quantity** (option values **(blank)** and **Previous Operation**). This field is set up as a non-visible default flag and is not maintained in the standard flow.

**Time Posting locks (validation):** The app enforces consistent settings: **No Start-Action required** is not allowed when **Time Posting = Standard**, and **Post Only Duration** is allowed only when **Time Posting = Standard** or **Expected Time**.

#### Set Up Time Posting and Reporting

**Who/when.** The key user defines, per work center, how times and quantities are reported – **before** the first posting at this machine center. The setting is consumed during daily work when you **Start**/**Partially Finish**/**Finish** and on the **Prod. Order Job Posting** page (see **Posting and Reporting**).

Activation steps in dependency order:

1. Open the **Prod. Order Job Work Center Setup** via the **Work Center Card** → **Prod. Order Job Setup** action.
2. Set **Time Posting** to match the machine center: when **Standard** is chosen, the user works with start/end times; when **None** or **Qty. based exp. Time** is chosen, a **Quantity** must be entered during reporting.
3. Set **Setup Activity** if needed: if enabled, the additional setup step appears in the job overview before starting.
4. Set **Post Only Duration** if needed: if enabled, the posting page is omitted; without the flag, the user confirms every posting via **Prod. Order Job Posting**.
5. Set **Start Date-Time Editable** and **No Start-Action required** as needed, according to how the machine center works.

**Operational completion:** In daily work, **Start** (after a prior **Setup Activity**), **Partially Finish**, and **Finish** trigger the posting; the user completes it via **Prod. Order Job Posting** with **OK** (see **Posting and Reporting**).

#### Set Up Material Transfer

**Who/when.** The key user activates material transfer per work center when components are to be moved between locations/bins at this machine center before or during a posting. The function is applied in daily work via the **Transfer** action and the **Prod. Order Job Tranfer Lines** page (see **Material Transfer**).

1. In the global **Prod. Order Job Setup**, check the **Set Quantity from Remaining for Transfer** flag: if enabled, when the transfer lines are determined the app proposes the component's open remaining quantity as the quantity.
2. In the **Prod. Order Job Work Center Setup**, enable the **Transfer** field: if enabled, the **Transfer** action appears in the job overview, and when you **Interrupt** the transfer lines are collected automatically if they do not yet exist.
3. Make sure the affected items, locations, and bins are maintained in Business Central (a prerequisite for the availability check in the transfer lines).

**Operational completion:** Using the **Transfer** action, the user opens the **Prod. Order Job Tranfer Lines**, checks location, bin, lot no./serial no., and quantity, and completes the material movement with the posting (the transfer is posted on finish, see **Posting and Reporting**).

#### Set Up Sequence Control

**Who/when.** The administrator defines, in the global **Prod. Order Job Setup**, how strictly the operation sequence is specified. This is applied when the lines are collected and sorted and when you **Start**.

1. **Follow Prod. Order Sequence:** if enabled, the app adopts the sequence from the production order; without the flag, the manual **Sequence** per line controls it.
2. **Forced Sequence at Routing:** if enabled, the app prevents the **Start** of an operation as long as the previous operation has no posting.
3. **Automatic Sequence adjust** and **Automatic Sequence on Finish:** if enabled, the app keeps the sequence numbers gapless automatically or renumbers them on finish.

**Operational completion:** In daily work, the user assigns or changes the **Sequence** directly in the line; the configured rules then take effect when sorting, starting, and finishing.

#### Set Up Employee Requirement

**Who/when.** The key user determines, per work center, whether an employee number must be specified when starting. The switch is on the **Work Center Card** (see **Master Data – Work Center**); the effect takes place when you **Start**.

1. Open the **Work Center Card** and set **Employee No. Required**: if enabled, the app requires a valid **Employee No.** when you **Start**; if it is missing, it aborts with "Employee No. is required for Work Center %1."
2. Make sure the relevant employees are maintained as active employees (without an expired termination date); only such employees can be selected as **Employee No.** in the line.

**Operational completion:** In daily work, the user enters the **Employee No.** directly in the line (only possible while the job is not **Started**); when starting, the app checks the requirement.

## Master Data

The master data of the core app is deliberately kept lean; however, it directly controls daily work.

### Work Center (Employee Requirement)

**Who/when.** The administrator maintains, per work center on the **Work Center Card**, whether an employee requirement applies. The app extends the standard card by exactly one flag; all other fields of the work center card are Business Central standard.

| Field | Explanation |
|---|---|
| Employee No. Required | If enabled, a valid **Employee No.** must be present in the line when you **Start** an operation of this work center; otherwise the start is aborted. Without the flag, specifying the employee is optional. |

The card also contains the **Prod. Order Job Setup** action, which opens the **Prod. Order Job Work Center Setup** (see **Setup**). The value of **Employee No. Required** takes effect in daily work via the check when starting and via the editability of the **Employee No.** field in the line (cross-reference: **Set Up Employee Requirement**).

### Prod. Order Job Inter. Reasons

**Who/when.** The key user maintains the reasons before users interrupt operations. The list is opened from the global **Prod. Order Job Setup** via the **Interuption Reasons** action and is selected in the job overview during the **Interrupt** action. The most important effect lies in the **Next Job Can Start** flag, which controls whether a follow-up step may already begin despite the interruption, and determines the traffic-light color in the **Work Center Lights**.

| Field | Explanation |
|---|---|
| Code | Unique short key of the interruption reason; appears in the line and in the event history. |
| Description | Plain text of the reason; shown to the production employee during selection. |
| Next Job Can Start | If enabled, the next operation may already start despite the interruption, and the machine center appears in the work center lights in the second traffic-light stage (default Yellow); without the flag, the reason blocks the follow-up process, and the monitor shows the first traffic-light stage (default Red). |

**Process steps:** First create a separate **Code** per functional disruption reason, then formulate the **Description** unambiguously, and finally enable **Next Job Can Start** only for reasons that are deliberately released.

### Prod. Order Job Description (Description Schema)

**Who/when.** The key user optionally stores, per work center, a schema from which the app assembles the **Description** of a job overview line. The page is opened from the **Prod. Order Job Work Center Setup** via the **Prod. Order Job Description** action. If no schema is stored, the app forms the description by default from Prod. Order No., Prod. Order Line No., and Operation No.

| Field | Explanation |
|---|---|
| Sequence | Determines the order in which the components are assembled into the description; the lines are processed in ascending order. |
| Prefix | If filled, this text is placed before the field content (e.g. an identifying letter). |
| Field Description | If enabled, the name of the source field is additionally placed before the value (e.g. "Prod. Order No. 100123"); without the flag, only the value appears. |
| Field | Defines which source value is used. Values: **Prod. Order No.**, **Prod. Order Line No.**, **Operation No.**, **Operation Description**, **Prod. Item Description**, **Prod. Item Description 2**. For each value, the corresponding content of the operation or production order is adopted. |
| Suffix | If filled, this text is appended after the field content. |

**Process steps:** First create a line with a **Sequence** per desired component, then choose the **Field** (and set **Field Description** if needed), and finally add **Prefix**/**Suffix**. The result then appears in the job overview in the **Description** column of the affected work center.

## Daily Work in the Prod. Order Job Overview

The **Prod. Order Job Overview** page is the central work list. Its behavior is controlled by the **Prod. Order Job Work Center Setup** (visibility of **Setup Activity**, **Transfer**, time fields, and sales fields, default sorting, time posting) and by the global **Prod. Order Job Setup** (sequence, refresh after actions). Without selecting a **Work Center**, the app cannot collect any lines.

### Filters

The filter area above the line list determines which operations are compiled and displayed.

| Filter field | Explanation |
|---|---|
| Work Center No. | Mandatory filter. When set, the app collects the open and running operations of this work center; without a value, the message "No Work Center selected." appears and no lines are loaded. |
| Work Center Name | When a work center is selected, its name is displayed automatically (display only). |
| Machine Center No. | When set, the lines are additionally narrowed to this machine center. |
| Machine Center Name | When a machine center is selected, its name is displayed (display only). |
| Prod. Order No. | When set, only lines of the specified released production order are displayed. |
| Date | When set, the lines are narrowed by the operation's start date. |
| Sort By | When set, the value overrides the default sorting from the work center setup (**Sequence**, **Status**, **Prod. Item**, **Date**). |
| Hide Finished | When enabled, lines with **Status = Finished** are hidden (active by default when the page is opened). |
| Hide Open | When enabled, lines with **Status = Open** are hidden. |
| Postings in Previous Operation | When enabled, only lines whose previous operation already has a posting are displayed; without the flag, lines without a posting in the previous operation are also shown. |

**Parent-before-child.** In daily work, always select the **Work Center No.** **first** and only **afterward** – optionally – the **Machine Center No.**. The machine center is not mandatory.

### Reading the Line List

The lines contain considerably more than the operation and quantity. Central columns:

| Field | Explanation |
|---|---|
| Description / Description 2 | Assembled name of the operation (see description schema) or additional line. |
| Sequence | Work sequence in the job overview; the internal blank value 999999 is hidden. A change sets the job to **Planned** and – depending on the setup – automatically adjusts the other sequences. |
| Status | Processing state of the operation (see status values below). |
| Previous Operation Status | Shows the posting state of the previous operation. **No Posting:** the previous operation has not yet been posted; **Posting exist:** a posting already exists; **Finished:** the previous operation is completed; **1st Operation:** there is no previous operation. |
| Operation No. | Operation from the routing of the production order. |
| Employee No. | Assigned person; editable only while the job is not **Started**. With an employee requirement (see master data), mandatory when starting. |
| Machine Center No. | Assigned machine center; a change sets the job to **Planned**. |
| Interr. Reason Code / Interr. Reason Description | For interrupted lines, the chosen reason and its description. |
| Start Date / Start Time | Planned or reported start of the operation. |
| Finished Quantity | Sum of the quantities already posted (calculated from the events). |
| Prod. Quantity | Production quantity of the production order (display only). |
| Unit of Measure Code | Unit of measure of the production item. |

Via **Show Times** (setup), **Expected Time**, **Posted Time**, **Outstanding Time**, and **Time incl. Setup** additionally appear; via **Show Sales Order No.**, the sales fields **Sales Order No.**, **Sales Order Line No.**, **Shipping Agent Code**, and **Shipping Agent Service Code**. Further optional columns that are hidden by default are the production order header data (**Prod. Order Status**, **Prod. Order No.**, **Prod. Order Line No.**, **Prod. Item No.**, **Prod. Variant Code**, **Prod. Item Description**/**2**, **Last Operation**) as well as the previous/next operation fields (**Prev. Operation Type/No./Desc.**, **Next Operation Type/No./Desc.**).

**Status values (Status column):**

- **Open:** operation compiled, not yet planned or started – no time or quantity posting.
- **Planned:** assigned to a person, a machine center, or a sequence, but not yet in progress.
- **Setup:** the setup step is running (only when the setup activity is active); the subsequent processing can be started.
- **Started:** processing is running; follow-up postings are possible; another start at the same machine center is blocked unless "Start Multiple Jobs" is set.
- **Interrupted:** processing is paused with a stored interruption reason; a completion is not possible until it is resumed or finished.
- **Partially Finished:** a partial quantity has been reported; the operation remains open for further processing.
- **Finished:** operation completed; no further quantity or time changes; optionally archived.

### Process Actions

The actions in the menu bar (**Process** area) control the status change and, if needed, trigger postings:

- **Setup Activity:** Visible only when the setup activity is active for the work center. Sets the operation to **Setup**.
- **Start:** Sets the operation to **Started**. With **Forced Sequence at Routing** active, the app checks whether the previous operation has been posted; with an employee requirement, the **Employee No.** is checked; when a machine center with machine centers is used, the **Machine Center No.** must be specified.
- **Interrupt:** With transfer active, first opens the collection of the transfer lines, requires the selection of an **interruption reason**, and sets the operation to **Interrupted**; the employee number is removed in the process.
- **Partially Finish:** Reports a partial quantity (status **Partially Finished**); the operation remains editable.
- **Finish:** Completes the operation functionally (status **Finished**). Changes from **Open**/**Planned** (without "No Start-Action required"), **Interrupted**, or **Partially Finished** are confirmed with a "Continue Process?" prompt.
- **Transfer:** Visible only with transfer active. Opens the **Prod. Order Job Tranfer Lines** of the selected operation.
- **Set To Open:** After the prompt "Set prod. order job line to status "Open"?", resets the operation to **Open**.
- **Show Document:** Opens the underlying production order in accordance with its status (simulated, planned, firm planned, released, or finished).
- **Event History:** Opens the history of the selected operation (**Prod. Order Job Events**).
- **Update Data:** Recompiles the lines and applies the default sorting.

**Status rules (excerpt).** A **Started** job cannot be started again ("Job already started."); an **Interrupted** job cannot be finished without being resumed; an already **Finished** job triggers the message "Job already finished." when you try to finish it again. Without "No Start-Action required", finishing from **Open**/**Planned** is only possible after confirming "Job not started! Continue Process?".

### FactBox Previous & Next Operation

To the right of the line list, the FactBox **Prev. & Next Operation** shows the immediately preceding and following step for the selected record. It helps decide whether an operation may already be started or whether follow-up processes need to be prepared.

| Field | Explanation |
|---|---|
| Prev. Operation Desc. | Short text of the immediately preceding operation. |
| Next Operation Desc. | Short text of the immediately following operation. |

## Posting and Reporting

If an action (**Start** after a prior **Setup Activity**, **Partially Finish**, **Finish**, or **Interrupt**) triggers a time or quantity posting, the app opens the **Prod. Order Job Posting** page as a modal dialog – provided **Post Only Duration** is not set in the work center setup. The app checks temporal consistency in the process: the **Start Date** must not be after the **Ending Date**, and for the same date the **Start Time** must not be after the **Ending Time**. Which fields are editable depends on the **Time Posting** of the work center (see **Set Up Time Posting and Reporting**).

**Posting Period** section:

| Field | Explanation |
|---|---|
| Start Date | Start of the operation; editable only when "Start Date-Time Editable" is set. |
| Start Time | Start time; editable only with "Start Date-Time Editable". |
| Ending Date | Completion date; with **Standard** time posting from the event, otherwise locked. |
| Ending Time | Completion time; editability analogous to Ending Date. |
| Setup Time | Setup time; editable with **Expected Time** and **Manual** time posting. |
| Run Time | Run time; editable with **Expected Time** and **Manual** time posting. |

**Quantities** section:

| Field | Explanation |
|---|---|
| Quantity | Reported quantity of the operation. With **None** and **Qty. based exp. Time** time posting, the entry is mandatory; if no quantity is detected on closing, "No Quantity set." appears and the posting is not completed. |
| Posted Quantity | Total quantity already posted for the operation (display only). |

**Location** section (relevant especially for the **last operation**):

| Field | Explanation |
|---|---|
| Location | Target location of the posting; editable only at the last operation. |
| Bin Code | Target bin of the posting; editable only at the last operation. |

**Information** section (display only, for cross-checking): **Prod. Order No.**, **Item No.**, **Variant Code**, **Description**, **Description 2**. Using the **Item Tracking Lines** action, you open item tracking for tracking-relevant items; afterward, the reported **Quantity** is reconciled with the captured quantity.

**Effect of the time posting (summary):**

1. **Standard:** start/end times are used per the setup; times come from the event.
2. **None:** time fields locked; **Quantity** mandatory.
3. **Expected Time:** **Setup Time** and **Run Time** are entered directly, date/time fixed.
4. **Qty. based exp. Time:** the time is derived from the quantity; **Quantity** mandatory.
5. **Manual:** **Setup Time** and **Run Time** manual; with "Start Date-Time Editable", start values can be adjusted as well.

### Posting Flow (Order of Steps)

The reporting flow follows a fixed sequence of steps that is repeated in **Quick Start** and in the **Typical Use Cases**:

1. Select a line in the **Prod. Order Job Overview**.
2. Optionally **Setup Activity** (status **Setup**).
3. **Start** (status **Started**). With forced sequence active, the posting of the previous operation is checked.
4. On a triggered posting and with **Post Only Duration** disabled: fill in the **Prod. Order Job Posting** page and close it with **OK**.
5. **Partially Finish** (partial quantity) and/or **Finish** (completion).
6. When finishing with **Transfer** active and a prior status of **Started**, the material transfer is posted first, then the reported quantity and time.
7. The app posts the output/capacity journal; **capacity ledger entries**, **item ledger entries**, and – with a transfer – **warehouse entries** arise. The event is marked as **Posted**.

**Hidden posting page (Post Only Duration).** If **Post Only Duration** is active, the **Prod. Order Job Posting** page is skipped; triggered by the same actions (Start/Partially Finish/Finish), the app posts the time directly from the event values. The user still confirms the action itself; a quantity or time correction in the dialog is omitted.

**Partial quantities.** Partial postings are permitted: via **Partially Finish**, a partial quantity can be reported repeatedly without completing the operation. A full quantity balance is not required for completion.

### Reporting Without Start (Special Case)

If **No Start-Action required** is set in the work center setup, a partial finish or finish can be done directly without starting first. The app then posts the reported quantity on completion.

## Material Transfer

With **Transfer** active (see **Set Up Material Transfer**), the user prepares the movement of the components via the **Transfer** action or when you **Interrupt**. The **Prod. Order Job Tranfer Lines** page lists one line per component with a source and target location. The lines are editable as long as the operation is in status **Setup** or **Started** (or in **Open**/**Planned** when "No Start-Action required" is set).

| Field | Explanation |
|---|---|
| Item No. | Item to be transferred; defaulted from the production order component. |
| Lot No. | If the item is lot-tracked, the lot is captured here; it can be selected from inventory via the assist button. |
| Serial No. | For serial-number-tracked items, the serial number to be moved. |
| Description | Name of the component (display only, read from the component). |
| Remaining Quantity | Open quantity calculated from the component quantity less transfers already captured and posted; changes when the **Quantity** of a line is adjusted. |
| Quantity | Quantity to be moved; a change updates the remaining quantities of all associated lines. |
| Posted Quantity | Transfer quantity already posted (display only). |
| Unit of Measure Code | Unit of measure of the component (display only). |
| From Location Code / From Bin Code | Source location and source bin; the bin selection takes lot/serial number and available inventory into account. |
| Available | If green, the required quantity is available at the source location; if red, the inventory is insufficient for the captured quantity. |
| To Location Code / To Bin Code | Target location and target bin of the movement. |

**Actions:** **Split Line** creates a new line from an existing one, in order to split the same component across multiple lots, serial numbers, or bins. **Bin Contents** opens the bin content for the item for inventory control. The FactBoxes **From Location - Bin Content** and **To Location - Bin Content** show the lot inventories per bin for the source and target location.

The prepared transfers are posted together with the reporting when the started operation is **Finished** (see **Posting Flow**, step 6/7).

## Work Center Lights and Event History

### Work Center Lights

**Entry:** via **Search** → **Work Center Lights**. The page shows one traffic-light tile per work center and reads for it the most recently changed job overview line of the group. The light follows that line's status and – on interruption – the **Next Job Can Start** flag of the reason:

1. Light 3 (default Green): an operation is actively **Started**; the Prod. Order No. and **Finished Quantity** are displayed.
2. Light 1 (default Red): the last operation is **Interrupted** and the reason does **not** release the follow-up process; the **Interr. Reason Code** is displayed.
3. Light 2 (default Yellow): no critical run status; the last production order is displayed.

Clicking the values of a tile opens the associated **Released Prod. Order** directly. The **Refresh Interval (sec)** from the global setup controls the automatic reload.

### Event History (Prod. Order Job Events)

**Entry:** from the **Prod. Order Job Overview** via the **Event History** action (or from the **Prod. Order Job Overview** list via **Event History** per production order). The read-only list documents every action on a job overview line and serves for traceability.

| Field | Explanation |
|---|---|
| Created By | User ID of the person who triggered the action. |
| Date / Time | Date and time of the event. |
| Status | Status documented by the event (Setup/Started/Interrupted/Partially Finished/Finished). |
| Interr. Reason Code / Interr. Reason Description | For interruptions, the chosen reason and its description. |
| Quantity | Posted or reported quantity of this event. |
| Run Time / Setup Time | Posted run time or setup time of the event. |
| Machine Center No. / Work Center No. | Assigned machine center or work center. |

Hidden but available for detailed review: **Date-Time Modified**, **Posted** (whether postings have already arisen from the event), **Time Posting**, the pre-start timestamps, and the "modified" flags of the times. Using the **Item Ledger Entries**, **Warehouse Entries**, and **Capacity Ledger Entries** actions, you open the entries that arose from the event for follow-up tracing. For this, the app links each entry to the triggering event via the event relation (field **Prod. Order Job Event** in the extended entry and journal tables).

## Blocking a Production Order for the Job Overview

Using the extended field **Blocked for Prod. Order Job** on the production order, a job can be excluded from compilation in the job overview.

| Field | Explanation |
|---|---|
| Blocked for Prod. Order Job | If enabled, the operations of this production order are **not** included in the **Prod. Order Job Overview**; without the flag, the job appears normally in the work list. |

The app prevents this flag from being set as long as at least one job overview line for the production order still has the status **Started** or **Interrupted**; in that case "At least one line in Prod. Order Job has status "%1"!" appears.

## Employee No. in Journals and Entries

For tracing who created a posting, the app adds the **Employee No.** field in the associated journals and entries:

| Field | Explanation |
|---|---|
| Employee No. (in the output journal and production journal) | When set, the reporting person is carried in the posting line; only valid, active employees are allowed, otherwise "This personnel number does not exist." appears. |
| Employee No. (in the capacity ledger entries) | Shows which person reported the posted capacity (display only, adopted from the posting). |

## History and Archive

If archiving is set to **Finished Prod. Order** in the global **Prod. Order Job Setup** and a production order reaches the status "Finished", the app moves the associated job overview lines together with their events and transfer lines to the archive. The **Archived Prod. Order Job Line** page then serves as proof of completed operations.

| Field | Explanation |
|---|---|
| Prod. Order Status / Prod. Order No. / Prod. Order Line No. | Reference to the archived production order. |
| Status | Archived work status. |
| Operation No. / Work Center No. / Machine Center No. | Operation, work center, and machine center of the operation. |
| Interr. Reason Code / Interr. Reason Description | Stored interruption reason. |
| Start Date / Start Time | Start of the archived operation. |
| Sequence | Sequence in the job overview. |
| Prod. Quantity / Finished Quantity | Original production quantity and finished-reported quantity. |
| Employee No. | Person involved. |

For detailed review, the **Archived Prod. Order Job Event** and **Arch. Prod. Order Job Tranfer Lines** pages are additionally available; they correspond in content to the active lists but serve only for tracing. Use these pages to clarify who started, interrupted, or finished an operation, which quantities and times were posted, and which material transfer was prepared or posted before the reporting.

## Permissions

The app ships a permission set **MuM PJ Permission**. It determines the permissions for the app's objects and defines which actions users may perform in the job overview and in its setup. Assign this set to the roles that work with the job overview or administer it.

## FAQ and Troubleshooting

### Why don't I see any lines after opening the job overview?
Without a **Work Center No.**, the app cannot collect any lines (message "No Work Center selected."). Select a work center first. If **Deactivate Direct Search** is active in the work center setup, additionally run **Update Data**.

### Why aren't the Setup Activity or Transfer actions visible?
Both actions depend on the work center setup: **Setup Activity** is shown by the **Setup Activity** field, **Transfer** by the **Transfer** field. If the respective flag is not set, the action stays hidden.

### Why does the posting page require a quantity?
With **Time Posting = None** or **Qty. based exp. Time**, the app checks when closing the **Prod. Order Job Posting** page that a reporting quantity has been entered. If it is missing, "No Quantity set." appears and the posting is not completed.

### Why can't I start an operation even though the job is selected?
With **Forced Sequence at Routing** active, the app prevents the start as long as the previous operation has no posting ("There is no Posting on previous Operation."). Post the previous operation first. If **Employee No. Required** is also set, a valid **Employee No.** must be present in the line beforehand.

### Why can't a second job be started at the same machine center?
If **Start Multiple Jobs** is not set in the work center setup, the app blocks the start of another job as long as a job is still **Started** or **Interrupted** at the same machine center. Finish or interrupt the running job, or enable the flag.

### Why can't I finish an interrupted job directly?
An **Interrupted** job must first be resumed with confirmation; only after the prompt "Job interrupted! Continue Process?" is completion possible. Likewise, an already finished job reports "Job already finished.".

### Why can't I block the production order for the job overview?
The app blocks setting **Blocked for Prod. Order Job** when at least one job overview line for the job still has the status **Started** or **Interrupted**. Finish these lines first.

### Why does the work center lights show red?
The first traffic-light stage (default Red) appears when the last relevant operation is **Interrupted** and the associated interruption reason does not release **Next Job Can Start**. If needed, choose a reason with the release flag set, or end the interruption.

### Why does the remaining quantity in the transfer lines stay at zero or change immediately?
The app recalculates the **Remaining Quantity** from the component quantity less transfers already captured and posted. As soon as you change the **Quantity** of a line, the remaining quantities of all associated lines are updated. If **Set Quantity from Remaining for Transfer** is additionally active, the open remaining quantity is proposed automatically as the quantity.

### Why is the employee number in a line no longer editable?
The **Employee No.** is editable only while the job is not **Started**. After the start, the field is locked; when you **Interrupt**, the employee number is removed again and can then be set anew.

## Typical Use Cases

### Shift Start at a Work Center

**Trigger.** The early shift begins, and the shift lead wants to see which operations are due at a work center today.

**Entry in BC.** The user opens the **Prod. Order Job Overview** page via **Search** and selects the appropriate **Work Center No.**.

**Core flow.**
1. Set the filter for **Work Center No.** and optionally **Date**; add **Machine Center No.** if needed.
2. **Update Data** so that the current lines are collected.
3. Sort by **Sequence** or **Date**.
4. In the line, check **Status**, **Previous Operation Status**, **Operation No.**, **Prod. Order No.**, and **Finished Quantity**.
5. Take the first released operation into work with **Start** (status **Started**).

**Completion.** For queries, the user opens the released production order directly with **Show Document**.

### Machine Disruption with Interruption and Material Decision

**Trigger.** A disruption occurs during processing; the employee must stop the operation and secure material for the next step.

**Entry in BC.** The user is already working in the **Prod. Order Job Overview** on the line of the running operation (status **Started**).

**Core flow.**
1. In the line, check that **Status** = **Started**.
2. Run the **Interrupt** action.
3. With **Transfer** active, the transfer lines are collected or opened automatically.
4. Choose an entry from **Prod. Order Job Inter. Reasons** (status changes to **Interrupted**).
5. In the **Prod. Order Job Tranfer Lines**, check **From Location Code**, **From Bin Code**, **Lot No.**, and **Quantity**; the **Available** field must be green.
6. If needed, prepare multiple lots or bins with **Split Line**.

**Completion.** The operation remains visible in the **Event History**. In the **Work Center Lights**, the display switches to the first (Red) or second (Yellow) traffic-light stage depending on the interruption reason.

### Partial Reporting and Completion of an Operation

**Trigger.** Initially only part of the quantity was produced; the reporting should already take place in the system, and the operation completed later.

**Entry in BC.** The user is working in the **Prod. Order Job Overview** on the started line.

**Core flow.**
1. Select the line with **Status = Started**.
2. Run the **Partially Finish** action (status **Partially Finished**).
3. On the **Prod. Order Job Posting** page, capture the **Quantity** (and, depending on **Time Posting**, the times) and close with **OK**; with **Time Posting = None**/**Qty. based exp. Time**, the **Quantity** is mandatory.
4. Later, complete the remaining operation with **Finish** (status **Finished**); again close the **Prod. Order Job Posting** with **OK**.
5. If it is the **last operation**, set **Location** and **Bin Code** in the **Location** section of the posting page for the put-away.

**Completion.** The posted quantities and times appear in the **Event History**; via **Capacity Ledger Entries**, **Item Ledger Entries**, and if applicable **Warehouse Entries**, the resulting entries can be reviewed.
