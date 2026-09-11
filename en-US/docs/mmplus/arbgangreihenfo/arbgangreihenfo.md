---
title: Anwenderhandbuch m+m Routing Sequence
---

# User Guide m+m Routing Sequence

## Introduction

The **m+m Routing Sequence** module manages, for each **Work Center Group**, the
**sequence** in which the operations of released production orders are processed
there. From the operations of the released production orders, a work list
maintained per work center group is created automatically. On the
**Production Planning** page, the user arranges these operations into the
desired processing sequence without changing the routing of the production order
itself.

The module creates **no** documents of its own and does **not** post. It provides
an additional control view: which operation is processed next at a work center
group, and which one follows. The list is maintained automatically by the system;
it grows, shifts, and empties depending on how operations are created, changed, or
completed in the production orders.

**Target audience:** Primarily these are **operational** users in production
control and production planning who define and maintain the processing sequence at
the work center groups on a daily basis. Secondarily, the module concerns
administrators who set up licensing and permissions. A dedicated setup dialog is
not required; after installation, license, and permission, the function is
immediately available.

**Brief process overview:**

1. In a **Released Production Order**, operations are created that refer to a
   **Work Center Group**.
2. For each such operation, the system automatically creates a line in
   **Production Planning** and consecutively assigns the next **sequence** within
   the work center group.
3. The user opens the **Production Planning** page and, if necessary, adjusts the
   **sequence** of individual lines; the system automatically re-sorts the
   remaining lines of the work center group.
4. When an operation is completed, changed, or deleted, the system automatically
   removes or shifts the corresponding line and closes any gaps that arise in the
   sequence.

## Quick Start for Users

The fastest way to a well-maintained processing sequence:

1. **Setup prerequisite:** Make sure the module is licensed and that your user has
   the **Production Planning** permission (see chapter **Setup**). Without a valid
   license and permission, the page cannot be used.
2. **Create operations:** In the **Released Production Order**, create operations
   that refer to a **Work Center Group**. For each of these operations, a line is
   created automatically in Production Planning.
3. **Open the list:** Use **Search** to open the **Production Planning** page. The
   page is a standalone list and is found via the BC search.
4. **Define the sequence:** Select the line to be moved and enter the desired
   position in the **Sequence No.** field. The system automatically shifts the
   lines in between within the work center group and updates the display.
5. **Check:** Verify the sorting: the list is ordered per work center group in
   ascending **Sequence No.** order. Completed operations are no longer included.

A posting or release step is not provided within the module itself; maintaining the
sequence is the only user step. All further changes result automatically from the
work on the production order.

## Setup

The module requires **no** setup page of its own and no number series. The steps
required for operation concern exclusively **licensing** and **permissions**. Both
are performed by the administrator before first use and are a prerequisite for the
daily work on the **Production Planning** page (chapter **Daily Work: Production
Planning**).

### License the Module

**Process intro:** The license check is set up by the administrator and then runs
without any further intervention. It ensures that the module is enabled in the
current company and for the respective user. The check is performed via the base
module **m+m Cloud Base** and is triggered at every sign-in. Without a valid
assignment, the user receives a notice at sign-in, and use of the module may be
restricted.

The license check evaluates a **license type** for each module. Each value results
in a different behavior:

- **Flat-Rate:** When this license type is set, the module is considered enabled
  without any further assignment; no check is performed per company or user.
- **Per Company:** When this license type is set, the current company must be
  assigned to the module; if the assignment is missing, the system reports at
  sign-in that the company is not assigned to the module.
- **Per User:** When this license type is set, the signed-in user must be assigned
  to the module; if the assignment is missing, the system reports that the user is
  not assigned to the module.

**Getting started:** License management is part of the base module **m+m Cloud
Base**; the assignment of companies and users takes place there. No additional page
needs to be set up for this module.

**Enablement steps (in dependency order):**

1. **First**, install the module together with its dependency **m+m Cloud Base**
   in the company. When both apps are installed, the license check can be executed
   at sign-in.
2. **Then**, in the base module, assign the **company** and/or the **users** to the
   module depending on the license type. When the assignment is present, sign-in no
   longer reports a license notice, and the function is ready.
3. **Finally**, the user signs in. When license and assignment are valid, the user
   can open the **Production Planning** page and maintain the sequence (chapter
   **Daily Work: Production Planning**).

**Note on operating mode:** In on-premises environments, the license check is
skipped; the assignment is not required there. In the cloud, the assignment is a
prerequisite for undisturbed operation.

### Assign Permissions

**Process intro:** Permissions are assigned by the administrator before first use.
This determines which users may open Production Planning and change the sequence.
Without this permission, the page is not accessible to the user, and the automatic
maintenance in the background cannot write the planning data.

The module ships with a permission set that covers all objects required for
operation.

| Setup | Explanation |
|-------------|-------------|
| Permission set **Production Planning** | When this permission set is assigned to a user or a user group, that user receives full access (read, insert, modify, delete) to the planning data as well as the execution right on the page and the management logic of the module. The permission set thus determines who may open the **Production Planning** page and maintain the **Sequence No.**, and that the automatic maintenance in the background can create, change, and delete the lines. |

**Enablement steps:**

1. **First**, the administrator opens the permission management of Business
   Central.
2. **Then**, the administrator assigns the permission set **Production Planning**
   to the responsible users or user groups. When the assignment has been made,
   these users can open the page and edit the sequence.
3. **Finally**, the user can begin the daily work (chapter **Daily Work:
   Production Planning**).

## Daily Work: Production Planning

The actual user work takes place on the **Production Planning** page. It shows, per
**Work Center Group**, the operations of the released production orders pending
there in the current processing sequence. The content of the list is a consequence
of the work in the **Released Production Order**: whether a line appears,
disappears, or moves to another work center group is controlled by the user via the
operations in the production order. The **Sequence No.** within a work center group,
on the other hand, is determined by the user directly on this page.

**Getting started:** Open the **Production Planning** page via **Search**. It is a
standalone list; a superordinate document or a setup page as an entry point is not
required.

The page is a pure editing list: new lines can **not** be created manually, and
existing lines can **not** be deleted manually. These changes result exclusively
from the work on the production order. The only editable field is the **Sequence
No.**

### Fields of the List

The list is sorted per **Work Center Group** in ascending **Sequence No.** order.

| Field | Explanation |
|------|-------------|
| **Work Center No.** | When an operation of a released production order refers to a work center group, its number is carried here; it groups the lines and is the reference within which the sequence applies. The field is not editable and is taken by the system from the operation. |
| **Sequence No.** | Determines the processing position of the operation within the work center group. When the user changes this value, the system automatically shifts the lines of the work center group in between and keeps the numbering gapless. This is the only field editable by the user. |
| **Line No.** | Internal, gaplessly assigned ordering number of the record per work center group. When a new line is created, the system assigns the next free Line No.; it serves for unique identification and is not editable. |
| **Item No.** | Shows the item that is produced via the production order at this operation. When the line is created, the system takes the Item No. from the production order line; this way the user recognizes which product is behind the operation. The field is not editable. |
| **Prod. Order No.** | Shows the number of the released production order from which the operation originates. When the line is created, the system takes the Prod. Order No. from the operation; the user uses it to mentally navigate back to the order. The field is not editable. |

The list contains no additional user-defined filter fields beyond the standard BC
list filtering. Filtering is possible via the standard column filters, in
particular by **Work Center No.**, in order to narrow the view to a single work
center group.

### Change the Sequence

Changing the **Sequence No.** is the central user step.

1. In the **Production Planning** list, select the line whose position you want to
   change.
2. Enter the desired target position in the **Sequence No.** field.
3. The system automatically checks and limits the value to the valid range of the
   work center group: if the entered value is below the smallest existing sequence,
   the line is placed at the beginning; if it is above the largest existing
   sequence, at the end.
4. The system shifts the lines of the work center group in between by one position
   and updates the display. If you move a line backward, the skipped lines move
   forward by one position; if you move it forward, the skipped lines move backward
   by one position.

In this way, the numbering within the work center group always remains gapless, and
no two operations occupy the same position.

### Automatic Maintenance of the List (Background Behavior)

The user does not create lines themselves; the system maintains the list based on
the operations in the **Released Production Order**. Only operations of type work
center group are considered. Understanding this behavior makes daily work easier:

- **New operation:** When an operation referring to a work center group is created
  in the released production order, the system creates a new line and appends it
  with the next higher **Sequence No.** to the end of the work center group. Item
  No. and Prod. Order No. are taken from the order in the process.
- **Work center group changed:** When the work center group is changed on an
  existing operation, the system moves the corresponding lines to the new work
  center group, assigns new sequences appended to the end there, and closes the gap
  that arose in the previous work center group.
- **Operation completed:** When the routing status of the operation switches to
  **Finished**, the system removes the corresponding line from Production Planning
  and closes the gap in the sequence of the work center group.
- **Operation deleted:** When an operation is deleted, the system removes the
  corresponding line and likewise closes the gap in the sequence.

In all cases, the sequence per work center group remains gapless and consistent
without the user having to intervene manually.

## FAQ and Troubleshooting

### 1. Why can I not create a new line in Production Planning?

The page does not allow manual insertion. Lines are created exclusively
automatically as soon as an operation referring to a **Work Center Group** is
created in the **Released Production Order**. Create the operation in the production
order; the matching line then appears by itself.

### 2. Why can I not delete a line?

Deletion is locked on the page. A line disappears only when the corresponding
operation is completed or deleted in the production order. This way the planning
always stays in line with the operations actually present.

### 3. Which fields can I actually edit?

Only the **Sequence No.** field. All other fields — **Work Center No.**, **Line
No.**, **Item No.**, and **Prod. Order No.** — are filled by the system and are not
editable.

### 4. What happens if I enter a very high or very low sequence?

The system automatically limits the value to the valid range of the work center
group. A value below the smallest existing sequence places the line at the
beginning, a value above the largest existing sequence at the end. Invalid
positions outside the list cannot arise this way.

### 5. Why do other lines also shift when I change a sequence?

Because the sequence within a work center group must remain gapless. When you set a
line to another position, the lines in between automatically move by one position
so that no double allocation and no gap arise.

### 6. Why does an operation not appear in Production Planning?

Only operations that refer to a **Work Center Group** are considered. Operations of
another kind are not taken into Production Planning. Check the operation in question
in the production order.

### 7. Why has a previously visible operation suddenly disappeared from the list?

This happens when the routing status of the operation was set to **Finished** or
the operation was deleted. In both cases, the system removes the line and closes the
gap in the sequence.

### 8. What happens to the sequence when I switch an operation to another work center group?

The system removes the line from the previous work center group, closes the gap
there, and re-creates it in the new work center group with a **Sequence No.**
appended to the end. A position previously set in the old work center group is lost
in the process.

### 9. Why do I receive a license notice at sign-in, and what does it mean?

The module checks the license at every sign-in via the base module **m+m Cloud
Base**. A notice appears when the company or the user is not assigned to the module
or a payment is outstanding. Have the assignment checked and completed by the
administrator in the base module.

### 10. Why can a user not open the Production Planning page?

As a rule, the permission is missing. Assign the permission set **Production
Planning** to the user. Without this permission, the page is not accessible, and the
automatic maintenance in the background cannot write any lines.

## Typical Use Cases

### Use Case 1: Reorder the Sequence at a Work Center Group

**Trigger:** A production foreman reports by phone that an urgent order is to be
prioritized at a work center group.

**Entry in BC:** The planner opens the **Production Planning** page via **Search**
and filters on the relevant **Work Center No.** using the column filter in order to
see only its operations.

**Core flow:**

1. In the filtered list, the planner finds the line of the operation to be
   prioritized (orientation via **Item No.** and **Prod. Order No.**).
2. In the **Sequence No.** field, the planner enters the desired front position.
3. The system limits the value to the valid range, automatically shifts the lines
   in between backward, and updates the display.

**Conclusion:** The work center group now shows the new processing sequence; the
prioritized operation is at the desired position, all others remain sorted in
gaplessly. A posting step is not required.

### Use Case 2: A New Production Order Queues Up Automatically

**Trigger:** Production control releases a further production order due to a new
demand notification.

**Entry in BC:** The clerk works in the **Released Production Order** and creates
the operations of the order; each operation refers to a **Work Center Group**.

**Core flow:**

1. As each operation is created, the system automatically creates a line in
   **Production Planning** and appends it with the next **Sequence No.** to the end
   of the respective work center group; **Item No.** and **Prod. Order No.** are
   taken from the order.
2. The planner opens **Production Planning** via **Search** and checks at which
   position the new operations have been queued.
3. If necessary, the planner adjusts individual **Sequence No.** values in order to
   move the new order forward or backward; the system re-sorts automatically.

**Conclusion:** The new order is integrated into the processing sequence of the
affected work center groups without manual line creation. When its operations are
later completed, the system removes the corresponding lines automatically.
