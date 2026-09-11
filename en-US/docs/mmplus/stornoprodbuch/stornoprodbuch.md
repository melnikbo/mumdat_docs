---
title: Anwenderhandbuch m+m Undoing Production
---

# m+m Undoing Production User Guide

## Introduction

The **m+m Undoing Production** extension provides a convenient way within Microsoft Dynamics 365 Business Central to reverse production postings that have already been posted. Using a single action in the **Production Journal** of a released **Production Order**, you can specifically cancel posted **consumption postings**, posted **output** (finished quantities) and posted **times**. In doing so, the extension does not create a direct posting; instead, it adds corresponding **negative offsetting lines** to the Production Journal, which the user then posts themselves.

**Target audience:** The extension is aimed primarily at **operational users in manufacturing** – workers, production scheduling and reporting stations – who record feedback in day-to-day operations and need to correct erroneous postings. Secondarily, it concerns administrators who install the extension and assign the permission.

**Brief process overview:** For a released production order, the user opens the **Production Journal**, selects the **Cancel Posting** action, decides via options *which* posting types are to be canceled, selects the specific entries to be canceled in the entry lists that then open, and finally posts the Production Journal. The app is intended exclusively for postings that have not yet been finished; it is not intended for feedback that has already been completed (finished).

## Quick Start for Users

The fastest path from an erroneous feedback entry to its correction:

1. Open the relevant **released production order** and, for the desired line, open the **Production Journal**.
2. In the Production Journal, select the **Cancel Posting** action.
3. In the **General** section, set the desired options: **Correct Consumption** and/or **Correct Output**. Below them, as needed, activate **Cancel Quantity** (in the **Consumption** section) as well as **Cancel Quantity** and/or **Cancel Times** (in the **Output** section). Confirm with **OK**.
4. Confirm the prompt stating that all existing journal lines will first be deleted.
5. In the **Item Ledger Entries** and **Capacity Ledger Entries** lists that then open, select the specific entries to be canceled and confirm each with **OK**. You can select individual entries, none, or all lines.
6. Review the negative lines newly inserted into the Production Journal.
7. Select **Post** so that the cancellation postings are actually created.

No additional setup is required to use the extension (see chapter **Setup**). The detailed procedure with all options and prompts is described in the chapter **Cancel Posting – Procedure in the Production Journal**.

## Setup

To use the extension in the web client of Microsoft Dynamics 365 Business Central, **no additional functional setup** is required. There is neither a dedicated setup page nor number series or master data that would need to be maintained before first use. The **Cancel Posting** function is available immediately once the extension is installed and the permission is assigned.

### Installation and Prerequisites

A prerequisite for use is that the **m+m Undoing Production** extension is installed in **Extension Management**. The extension requires the base extension **m+m Cloud Base** from the same manufacturer; this dependency is resolved automatically during installation. When signing in, the extension performs a license check in the background via the payment module of the base extension; no action is required from the user for this.

If the extension is installed and licensed, then the **Cancel Posting** action is available in every **Production Journal** – without any further configuration.

### Permissions

The extension ships its own permission set that unlocks execution of the cancellation function. Assign this permission set to the users who are allowed to reverse production postings.

| Setup | Explanation |
|-------------|-------------|
| Permission set **All permissions** (m+m Undoing Production) | Determines which users are allowed to run the cancellation function. If the set is assigned to a user, then that user can call the **Cancel Posting** action and run the associated correction routine; without this set, the function has no effect for the user. The set determines the permissions for executing the internal correction module and the correction routine. |

Assignment is done via the standard permission management of Business Central (users or permission sets). There are no field-level additional permissions to maintain.

## Cancel Posting – Procedure in the Production Journal

This chapter describes the central and only transactional function of the extension. The function builds on the standard objects of Business Central: entry is made via the **Production Journal** of a released production order, and the selection of the entries to be canceled is made in the standard lists **Item Ledger Entries** and **Capacity Ledger Entries**. The extension does not add any additional fields or columns there; it only adds the **Cancel Posting** action and the associated selection dialog.

### Entry Point

**Entry point:** Open a **released production order**, open the **Production Journal** for the desired production order line, and there select the **Cancel Posting** action. The action is arranged in the ribbon of the Production Journal directly after the standard action for posting and printing.

### Options of the "Cancel Posting" Action

After the action is called, a dialog opens with the following options. All options are toggles (activated/not activated); their explanation describes what happens in the subsequent procedure when they are activated.

| Field | Explanation |
|------|-------------|
| **Correct Consumption** (section **General**) | If activated, then the posted **consumption postings** of the components are offered for cancellation in the subsequent procedure. Only with this option does the lower **Consumption** section become effective. If the option is deactivated again, then the **Cancel Quantity** option below it is automatically reset. |
| **Correct Output** (section **General**) | If activated, then the posted **output** of the finished item (reported quantities and/or times) is offered for cancellation in the subsequent procedure. Only with this option do the options in the **Output** section become effective. If the option is deactivated again, then the **Cancel Quantity** and **Cancel Times** options are automatically reset. |
| **Cancel Quantity** (section **Consumption**) | If activated, then the posted **consumption quantities** are canceled by an offsetting posting; the system opens the list of the production order's consumption item ledger entries for selection. The option can only be edited if **Correct Consumption** was activated beforehand. |
| **Cancel Quantity** (section **Output**) | If activated, then the posted **output quantities** (reported finished quantities) are canceled by an offsetting posting; the system opens the list of the production order's open output item ledger entries for selection. The option can only be edited if **Correct Output** was activated beforehand. |
| **Cancel Times** (section **Output**) | If activated, then the posted **setup, run and stop times** of the output are canceled by an offsetting posting; the system opens the list of the production order's **Capacity Ledger Entries** for selection. The option can only be edited if **Correct Output** was activated beforehand. |

If neither **Correct Consumption** nor **Correct Output** is set in the dialog – or if a higher-level option is set but none of the subordinate quantity/time options are set – then the correction routine aborts without any change. Therefore, select at least one higher-level option **and** the associated quantity or time option.

### Procedure After Confirming with OK

After confirming the dialog with **OK**, the correction routine runs through the following steps:

1. **Empty the journal:** First – after a prompt – all existing lines of the current Production Journal are deleted, as are the reservations belonging to this journal. As a result, cancellation starts with an empty journal.
2. **Prompts per option:** For each option that is set, a prompt appears:
   - when quantity cancellation of the consumption posting is activated: *"Do you want to select the Consumption Quantity for correction?"*
   - when quantity cancellation of the output is activated: *"Do you want to select the output quantities which should be canceled?"*
   - when time cancellation is activated: *"Do you want to select the Output Time for correction?"*
3. **Entry selection:** Once you confirm a prompt, the associated standard list opens in selection mode:
   - **Output – Quantity:** the **Item Ledger Entries** list, filtered to the production order's open output entries (entry type Output).
   - **Times:** the production order's **Capacity Ledger Entries** list (only entries with a quantity other than zero).
   - **Consumption posting – Quantity:** the **Item Ledger Entries** list, filtered to the production order's consumption entries (entry type Consumption).
   Mark the entries to be canceled and confirm with **OK**. You can mark individual entries, none, or all entries.
4. **Reservation check (output quantity only):** If **reservations** to dependent documents still exist for the selected output entries, then the prompt *"Reservations exists. Do you want to continue? The Reservations will be deleted."* appears. If confirmed, then the reservations in question are removed; if declined, then the selection remains unchanged and nothing is canceled.
5. **Create offsetting lines:** In accordance with the selection, the system inserts new lines with **negative values** into the Production Journal (negative output quantity, negative consumption, or negative setup/run/stop times). Lot and serial numbers of the original entries are transferred via reservation entries in the process; lines for operations that have already been finished are internally marked as done.
6. **Post:** The offsetting lines created are initially only proposals. Select **Post** in the Production Journal so that the actual cancellation postings are created and the entries are corrected.

### Effects of the Cancellation

- **Item Ledger Entries:** For canceled consumption and output quantities, offsetting item ledger entries with the opposite sign are created upon posting. For items tracked by lot or serial number, the reversal is linked via item tracking to the original **Lot No.** or **Serial No.**
- **Capacity Ledger Entries:** For canceled times, capacity ledger entries with negative **Setup Time**, **Run Time** and stop time values are created, so that the reported times of the production order are relieved.
- **Reservations:** Existing reservations for the affected output entries are – after confirmation – removed so that the reversal can be carried out.

## FAQ and Troubleshooting

### Why is the "Cancel Posting" action only available in the Production Journal?
The extension adds this action exclusively to the **Production Journal**, because the cancellation runs as a negative offsetting posting precisely via this journal. You therefore always reach the action via a released production order and its Production Journal, not via the search function.

### What happens if I do not set any option in the dialog?
If you set neither **Correct Consumption** nor **Correct Output** – or a higher-level option without an associated quantity/time option – then the correction routine aborts without any change. No lines are created and nothing is posted.

### Why are all existing journal lines deleted first?
The correction routine requires an empty Production Journal in order to hold only the cancellation offsetting lines. Therefore, after a prompt, all existing lines of the journal and the associated reservations are first removed. Please record any still-needed, unposted lines only after the cancellation.

### Why does the cancellation only create proposal lines and not post immediately?
The extension deliberately creates only **negative offsetting lines**. This lets you review the proposed reversal before posting and, if necessary, discard it. Only with **Post** do the actual cancellation postings arise.

### Why does the message about reservations to dependent documents appear?
If selected output entries are still reserved for dependent documents, then this reservation must be resolved first. The prompt *"Reservations exists. Do you want to continue? …"* gives you control: if you confirm, then the reservations are deleted and the cancellation continues; if you decline, then everything remains unchanged.

### Can I cancel individual entries specifically?
Yes. In the opened **Item Ledger Entries** or **Capacity Ledger Entries** lists, you select exactly the entries that are to be reversed. You can mark individual, several, or all entries; unmarked entries remain unchanged.

### Why don't I find all entries when canceling the output quantity?
For cancellation of the output quantity, the system offers only **open** output entries of the production order. Entries that have already been applied or closed are not available for selection, because they can no longer be reversed.

### Are lot and serial numbers taken into account during the reversal?
Yes. If the original entries are tracked by lot or serial number, then the extension transfers the **Lot No.** or **Serial No.** into the offsetting lines via item tracking and links the reversal to the original entry.

### Why are separate options offered for quantity and times?
Output contains both reported quantities (via item ledger entries) and reported times (via capacity ledger entries). With **Cancel Quantity** you reverse the reported finished quantity; with **Cancel Times** you reverse the reported setup, run and stop times. This allows quantity and time corrections to be carried out independently of each other.

### Can I cancel production order lines that have already been finished?
The extension is intended for reversing feedback that has not yet been finished. For the cancellation, the associated released production order line is used; the correction routine is not intended for fully completed (finished) feedback.

## Typical Use Cases

### Use Case 1: Correcting an Incorrectly Reported Output Quantity

**Trigger:** A worker reports to production scheduling by phone that, for a released production order, they accidentally reported an output quantity that was too high and already posted it.

**Entry in BC:** Production scheduling opens the relevant **released production order**, opens the **Production Journal** for the production order line, and selects the **Cancel Posting** action.

**Core procedure:**
1. In the **General** section, **Correct Output** is activated; in the **Output** section, **Cancel Quantity** is set. Confirm with **OK**.
2. The prompt to empty the journal is confirmed.
3. In response to the prompt *"Do you want to select the output quantities which should be canceled?"*, the **Item Ledger Entries** list opens with the order's open output entries. The incorrectly posted position is marked and confirmed with **OK**.
4. If a reservation still exists for the entry, the reservation prompt is confirmed.
5. The system inserts a negative output line into the Production Journal.

**Conclusion:** Production scheduling reviews the inserted offsetting line and selects **Post**. The excessive output quantity is thereby reversed via an offsetting item ledger entry; the correct quantity can then be reported again.

### Use Case 2: Reversing an Order's Consumption and Times Together

**Trigger:** By e-mail, production engineering reports that, for a production order, component consumption and run times were posted with the wrong date and are to be fully reversed before being reported correctly again.

**Entry in BC:** The clerk opens the **released production order**, opens the **Production Journal**, and selects **Cancel Posting**.

**Core procedure:**
1. In the **General** section, **Correct Consumption** and **Correct Output** are activated.
2. In the **Consumption** section, **Cancel Quantity** is set; in the **Output** section, **Cancel Quantity** and **Cancel Times** are set. Confirm with **OK**.
3. The prompt to empty the journal is confirmed.
4. One after another, the prompts for output quantities, output times and consumption quantities appear. For each confirmed prompt, the appropriate list opens – **Item Ledger Entries** for quantities, **Capacity Ledger Entries** for times – in which the relevant entries are marked and taken over with **OK**.
5. Any reservations for the output entries are resolved after a prompt.
6. For all selections, the system inserts negative offsetting lines (consumption, output quantity, times) into the Production Journal.

**Conclusion:** The clerk reviews the offsetting lines and selects **Post**. The order's consumption, output quantity and times are thereby reversed via offsetting item and capacity ledger entries; the feedback can then be recorded again with the correct date.
