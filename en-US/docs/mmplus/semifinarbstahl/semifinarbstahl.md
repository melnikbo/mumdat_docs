---
title: Anwenderhandbuch m+m Semifinished Items with Prod. Order Job Steel
---

# User Guide m+m Semifinished Items with Prod. Order Job Steel

## Introduction

The app m+m "Semifinished Items with Prod. Order Job Steel" connects two existing m+m extensions for steel production: the semi-finished item logic from m+m "Semifinished Items" and the **Prod. Order Job Overview** from m+m "Production Order Job Overview". It ensures that when the last operation of a semi-finished item is finished, the corresponding job is carried along automatically in the **Prod. Order Job Overview** and – depending on the setting – is reported back either automatically or manually.

To do this, the app adds exactly **one** new value **By Prod. Order Job Overview** to the option **Semi Finished Finish Operation Option** on the operation, and reacts in the background to the reporting events of the semi-finished item module. The app does not bring its own pages or cards; it controls the interaction of the two base modules. All pages and actions mentioned in this guide therefore originate from the supplied base modules, but are described here in full to the extent a user needs for this function.

**Target audience:** This guide is aimed primarily at **operational users** in steel production who start, interrupt, partially finish and finish jobs at the workstation and who report times and quantities. It is also addressed to **administrators and production managers** who set up the work center groups and the last operation for the Prod. Order Job Overview.

**Short process overview:** The administrator flags the last operation of a semi-finished item and selects the reporting method for this operation. During ongoing production, the app starts the job in the Prod. Order Job Overview automatically as soon as the semi-finished item goes into processing. Completion then happens either **automatically when posting the transfer receipt** or **manually by the user in the Prod. Order Job Overview**. Every status change is logged as an event.

## Quick Start for Users

The fastest path from setup to the first feedback posting – in the order enforced by the program (setup first, then daily work):

1. **Setup – flag the operation:** Open the **Prod. Order Routing** of the released production order (in the released production order via **Line → Routing**). On the last operation, set the flag **Semi-Finished Item** and, under **Semi Finished Finish Operation Option**, select the value **By Prod. Order Job Overview**.
2. **Setup – work center group:** Open the relevant **Work Center Group** (Work Center Group Card) and from there the **Prod. Order Job Work Center Setup**. Define the **Time Posting** and the start behavior (see Setup).
3. **Open the Prod. Order Job Overview:** Use **Search** to call up the **Prod. Order Job Overview** and select the **Work Center No.** – optionally also the **Machine Center No.** All associated jobs appear.
4. **Start:** The app starts the job automatically when the semi-finished item goes into processing. If it has not yet started, select the line and the action **Start**.
5. **Partially finish:** For a partial quantity, select the line and the action **Partially Finish**; the status changes to **Partially Finished**.
6. **Finish:** Once the operation is completely done, select **Finish**; the status changes to **Finished**.
7. **Trace:** Use **Event History** to review the logged status changes.

☞ If you instead want fully automatic feedback, in step 1 select the value **When posting the transfer receipt** under **Semi Finished Finish Operation Option**. Then the system performs the partial finish or finish without any manual action (see "How Feedback Works").

## Setup

Setup covers two levels: the **flagging of the last operation** on the production order (controls whether and how the Prod. Order Job Overview is involved) and the **Prod. Order Job Work Center Setup** per work center group (controls start behavior and time posting). The two levels work together; the following H3 "Setting up feedback via the Prod. Order Job Overview" describes the complete chain in dependency order.

### Setting up feedback via the Prod. Order Job Overview

**Who sets up and when:** The administrator or production manager sets up this chain **before the first feedback posting** – the work center group setup once per work center group, the operation flag per production order routing. The setting is applied later in the chapter **Daily Work in the Prod. Order Job Overview**.

**Sequence in dependency order:**

1. **First – flag the semi-finished item:** In the **Prod. Order Routing** of the production order, set the flag **Semi-Finished Item** on the last operation. Only when this flag is set is the selection of the **Semi Finished Finish Operation Option** possible at all; without the flag the option remains locked and the operation is treated like a normal operation without a Prod. Order Job Overview link.
2. **Then – choose the reporting method:** Under **Semi Finished Finish Operation Option**, select the appropriate value. If you select **By Prod. Order Job Overview**, completion happens exclusively manually by the user in the **Prod. Order Job Overview**; if you select **When posting the transfer receipt**, the system partially finishes or finishes the job automatically when the transfer receipt is posted (see "How Feedback Works").
3. **Location check rule:** When setting the option, the system checks that the **location** of the operation differs from the location of the work center group. If both locations are identical, the system cancels the selection with a message; if no location is assigned to the work center group, the option is reset automatically. Therefore, assign the work center group a location that differs from the operation line before you set up feedback via the Prod. Order Job Overview.
4. **Finally – set up the work center group:** In the **Prod. Order Job Work Center Setup**, define the start behavior and the **Time Posting** (fields see next H3). These values determine whether the job must be started explicitly and which times are reported at finish.

**Operational completion of the chain:** After this setup, the app starts the affected job in the Prod. Order Job Overview automatically as soon as the semi-finished item goes into processing; the user then completes it via the actions **Partially Finish** and **Finish** in the **Prod. Order Job Overview** (see chapter **Daily Work in the Prod. Order Job Overview**).

**Field | Explanation** (last operation in the **Prod. Order Routing**):

| Field | Explanation |
|------|-------------|
| **Semi-Finished Item** | When enabled, this operation is treated as the last operation of a semi-finished item and the app includes it in the Prod. Order Job Overview; only then can the **Semi Finished Finish Operation Option** be set. Without the flag the operation remains without a Prod. Order Job Overview link. |
| **Semi Finished Finish Operation Option** | Determines how the last operation is reported back. **(blank):** The base module's standard behavior applies without automatic Prod. Order Job Overview feedback. **When posting the transfer receipt:** When the transfer receipt is posted, the system automatically partially finishes or finishes the associated job in the Prod. Order Job Overview – without any user action. **By Prod. Order Job Overview:** The system does not report back automatically; the user finishes the job manually in the Prod. Order Job Overview via **Partially Finish**/**Finish**. This app adds exactly this value. |

☞ The option can only be selected if **Semi-Finished Item** has been enabled beforehand.

### Prod. Order Job Work Center Setup

**Who sets up and when:** The administrator sets up the **Prod. Order Job Work Center Setup** page per work center group **once before the first feedback**. It controls how jobs of this work center group can be started and reported in the **Prod. Order Job Overview** and how times are posted at finish – that is, exactly the behavior the user encounters in **Daily Work in the Prod. Order Job Overview**.

**Entry point:** In the **Work Center Group** (Work Center Group Card), open the line or card of the desired work center group and from there select the call to the **Prod. Order Job Work Center Setup**. This page is deliberately not reachable via **Search**; it is always opened from the work center group.

**Setup | Explanation** (tab "General"):

| Setup | Explanation |
|-------------|-------------|
| **Work Center Name** | Shows the name of the work center group to which this setup applies; taken from the work center group and used for the unambiguous assignment of the setup values. |
| **Unproductive** | When enabled, the work center group is considered unproductive; its times do not flow into the evaluation as productive production time, so that feedback cleanly separates value-adding and non-value-adding time. |
| **Start Multiple Jobs** | When enabled, the user can start several jobs of this work center group at the same time in the Prod. Order Job Overview; without the flag only one actively started job is allowed at a time, which prevents mispostings during parallel work. |
| **No Start-Action required** | When enabled, the user can partially finish or finish a job directly without starting it first; this speeds up feedback at workstations without separate start-time capture. This flag cannot be combined with the **Standard** time posting. |
| **Sorting** | Sets the default sorting of the job lines in the Prod. Order Job Overview; a suitable sorting reduces the search effort at the workstation. |
| **Time Posting** | Determines which times are posted to the capacity ledger entries at finish. **Standard:** The actually reported start/end times are posted. **None:** No time is posted; only the status is updated. **Expected Time:** Instead of actual times, the setup and run time stored in the routing are posted. **Qty. based exp. Time:** The expected time is distributed according to the reported quantity. **Manual:** The user enters the times themselves. This field thus directly controls how precisely and how effortlessly feedback is performed. |
| **Only Report Time** | When enabled, only the time – but no finished quantity – is posted at finish; useful at pure time workstations. Permitted only with time posting **Standard** or **Expected Time** – with other time posting methods the system rejects the flag. |
| **Setup Activity** | When enabled, a separate setup phase is maintained for this work center group; the user can first set the job to **Setup** before starting, so that setup and run time are captured separately. |
| **Start Date-Time Editable** | When enabled, the user may adjust the start date and time afterward when reporting; this allows correct retroactive entry when feedback is given at a different time from the actual processing. |
| **Default Finished Quantity** | Controls the default of the finished quantity at finish. **(blank):** No default. **Previous Operation:** The quantity is taken from the previous operation, which avoids typing effort and transfer errors for pass-through quantities. (Field hidden by default; show it via page personalization if needed.) |
| **Deactivate Direct Search** | When enabled, the direct jump into the Prod. Order Job Overview is suppressed for this work center group; the user then calls up the view exclusively via the regular path, which prevents operating errors in environments with fixed workstation control. |
| **Show Sales Order No.** | When enabled, the Prod. Order Job Overview shows the associated sales order number; the user thus directly recognizes which customer order they are reporting for. |
| **Show Times** | When enabled, the time fields are shown in the Prod. Order Job Overview; without the flag the view remains reduced to status and quantity. |

☞ The combination rules (e.g. **No Start-Action required** not with **Time Posting Standard**, **Only Report Time** only with **Standard**/**Expected Time**) are checked by the system when saving; an invalid combination is rejected with a field message.

## How Feedback Works

This app does not change any page visibly; instead it reacts to the reporting events of the semi-finished item module. Depending on the selected **Semi Finished Finish Operation Option**, two flows result. Both are co-controlled by the **Prod. Order Job Work Center Setup** (start behavior, time posting).

### Automatic feedback – When posting the transfer receipt

If the option **When posting the transfer receipt** is selected on the last operation, feedback runs without any user intervention:

1. The user posts the **transfer receipt** of the semi-finished item.
2. The system determines the associated **Prod. Order Job Line**. If no started line exists yet, the job is first started automatically.
3. If the operation is still **in progress**, the job is set to **Partially Finished**; if it is fully completed, to **Finished**.
4. The status change is logged as an event (see **Event Log**).

☞ With this option, no action is required in the Prod. Order Job Overview; the user can only trace the result there.

### Manual feedback – By Prod. Order Job Overview

If the option **By Prod. Order Job Overview** provided by this app is selected, the system does **not** report back automatically:

1. When the semi-finished item goes into processing, the app **starts** the associated job in the Prod. Order Job Overview automatically, provided it is not yet **Started**. The user therefore finds it already as a running job.
2. When posting the transfer receipt, the system **deliberately does nothing** – it leaves partial finishing and finishing to the user.
3. The user reports the progress themselves in the **Prod. Order Job Overview** via the actions **Partially Finish** and **Finish** (see **Daily Work in the Prod. Order Job Overview**).

☞ Always choose **By Prod. Order Job Overview** when the operator at the workstation should decide the reporting time and the partial quantities themselves – for example when the transfer receipt and the actual completion occur at different times.

## Daily Work in the Prod. Order Job Overview

The **Prod. Order Job Overview** is the central working view of the operational user. It is controlled by the settings of the **Prod. Order Job Work Center Setup** (start behavior, time posting, displayed columns – see Setup).

**Entry point:** Call up the **Prod. Order Job Overview** via **Search**. First select the **Work Center No.** (higher-level area); optionally narrow it down additionally via the **Machine Center No.** All jobs of the selected work center group appear.

**Actions on the ribbon:**

| Action | Explanation |
|--------|-------------|
| **Setup** | Sets the selected job to the status **Setup**; usable when the setup activity is set up for the work center group, in order to capture setup time separately before processing. |
| **Start** | Sets the job to **Started** and begins time capture. With the option **By Prod. Order Job Overview**, this step is usually already performed automatically as soon as the semi-finished item goes into processing. |
| **Interrupt** | Sets the job to **Interrupted**. The system requires the selection of an **Interr. Reason Code**; without a reason the action is canceled. This keeps every pause traceably justified. |
| **Partially Finish** | Reports back a partial quantity and sets the job to **Partially Finished**; the job remains open for further reporting. Partial quantities are explicitly permitted – you do not have to wait until the quantity is balanced. |
| **Finish** | Completes the job and sets it to **Finished**; depending on the **Time Posting**, times and, if applicable, the finished quantity are posted. |
| **Reopen** | Resets an already reported job back to **Open** to allow a correction. |
| **Transfer** | Opens the associated transfer lines of the job, provided that transfer is active for the work center group. |
| **Show Document** | Opens the associated production order (simulated, planned, firm planned, released or finished depending on the status) for review. |
| **Update Data** | Reloads the job list and reapplies sorting and display options. |
| **Event History** | Opens the event list of the selected job (see **Event Log**). |

**Status values of the job line:**

| Status | Meaning |
|--------|-----------|
| **Open** | Job created, not yet started – no time or quantity feedback. |
| **Planned** | Job is scheduled but not yet in progress. |
| **Started** | Processing is running; follow-up reports (Interrupt, Partially Finish, Finish) are possible. |
| **Setup** | Setup phase is running; the setup time is captured separately before the job is started. |
| **Interrupted** | Processing paused with a stored reason; completion is only possible after starting again. |
| **Partially Finished** | A partial quantity has been reported; the job remains open for further reporting. |
| **Finished** | Job completed; no further quantity or time changes are intended. |

☞ This app acts primarily on the status changes **Started**, **Partially Finished** and **Finished** of the semi-finished item operations; the remaining status values belong to the general behavior of the Prod. Order Job Overview.

## Event Log

Every status change triggered by this app (Start, Partially Finish, Finish) is stored as an **event** on the Prod. Order Job Line. This makes it possible to trace seamlessly when and by whom the last operation was reported.

**Entry point:** In the **Prod. Order Job Overview**, select the job line and choose **Event History**. The **Prod. Order Job Events** for the selected line open.

For each event, the reached **Status**, **Prod. Order No.**, **Operation No.**, **Work Center No.**, **Machine Center No.**, the adopted **Time Posting**, date and time, and the creating user are recorded, among other things. In the case of an **interruption**, the **Interr. Reason Code** is additionally logged, and in the case of a transition out of setup, the previous start time as well.

☞ The event log is a pure audit view; it is written automatically and requires no manual maintenance.

## Typical Use Cases

The following usage examples show the two verified feedback paths in context. All pages and actions mentioned correspond to the verified program behavior.

### Use Case 1 – Automatic feedback at the transfer receipt

**Trigger:** At goods receipt, a semi-finished item from the upstream production stage is transferred and the **transfer receipt** is posted. The last operation is set up with the option **When posting the transfer receipt**.

**Entry point in BC:** The warehouse employee posts the transfer receipt as usual; opening the Prod. Order Job Overview is not required.

**Core flow:**
1. When the transfer receipt is posted, the system determines the associated **Prod. Order Job Line**.
2. If no started line exists yet, the job is started automatically.
3. If the operation is still in progress, the system sets the job to **Partially Finished**; if it is fully done, to **Finished**.
4. The status change is logged as an event.

**Completion:** The production manager later opens the **Prod. Order Job Overview** via **Search**, filters the **Work Center No.** and checks via **Event History** that the job was partially finished or finished correctly.

### Use Case 2 – Manual reporting via the Prod. Order Job Overview

**Trigger:** An operator at the last processing station should report the production progress themselves and in partial quantities, because the transfer receipt and the actual completion occur at different times. The last operation is set up with the option **By Prod. Order Job Overview**.

**Entry point in BC:** The operator opens the **Prod. Order Job Overview** via **Search** and selects the **Work Center No.** – if needed also the **Machine Center No.**

**Core flow:**
1. The job is already **Started**, because the app started it automatically when the semi-finished item went into processing. Otherwise the operator chooses **Start**.
2. For a produced partial quantity, the operator chooses **Partially Finish**; the status changes to **Partially Finished** and the job remains open.
3. If the work has to be paused, the operator chooses **Interrupt** and specifies an **Interr. Reason Code**; the status becomes **Interrupted**.
4. Once the operation is completely done, the operator chooses **Finish**; depending on the **Time Posting**, times and, if applicable, quantity are posted and the status becomes **Finished**.

**Completion:** Via **Event History**, the operator reviews the logged reports; via **Show Document** they can open the associated production order if needed.

## FAQ and Troubleshooting

### Why does the option "By Prod. Order Job Overview" not appear on the last operation?
The **Semi Finished Finish Operation Option** can only be selected once the flag **Semi-Finished Item** is enabled on the same operation. Set the flag first; then the option becomes available.

### Why is a location message shown when setting the option?
The system requires that the **location** of the operation differs from the location of the work center group. If both are the same, the selection is canceled with a message. Assign the work center group a different location.

### Why does nothing happen in the Prod. Order Job Overview after posting the transfer receipt?
This is intended with the option **By Prod. Order Job Overview**: the system then deliberately does not report back automatically. Completion is done manually via **Partially Finish**/**Finish**. For automatic feedback, choose **When posting the transfer receipt**.

### Why is my job already "Started" although I did nothing?
With the option **By Prod. Order Job Overview**, the app starts the job automatically as soon as the semi-finished item goes into processing – provided it is not yet **Started**. You can proceed directly with **Partially Finish** or **Finish**.

### Why does "Interrupt" require an additional entry?
For **Interrupt**, an **Interr. Reason Code** is mandatory. If no reason is selected, the action is canceled and the status remains unchanged. This way every pause is documented with a justification.

### Why can I not enable "Only Report Time"?
**Only Report Time** is permitted only with the time posting **Standard** or **Expected Time**. With other time posting methods the system rejects the flag with a field message. First set the appropriate **Time Posting**.

### Why can I not finish a job directly without starting it?
Directly partially finishing/finishing without starting first is only possible if **No Start-Action required** is enabled in the work center group setup. This flag cannot be combined with the **Standard** time posting.

### Do I have to fully complete a job or may I report partial quantities?
Partial quantities are explicitly permitted. Via **Partially Finish** you set the job to **Partially Finished**; it remains open for further reporting. Waiting for the complete quantity balance is not required.

### Where can I see when and how an operation was reported?
Select the job line in the **Prod. Order Job Overview** and choose **Event History**. In the **Prod. Order Job Events** you will find status, date, time, user, work center group/machine center and – for interruptions – the interruption reason code.

### Why are different times posted at finish than were actually worked?
This depends on the **Time Posting** of the work center group: with **Expected Time** or **Qty. based exp. Time**, not the actual times but the expected times stored in the routing or distributed by quantity are posted. For actual times, choose **Standard** or **Manual**.
