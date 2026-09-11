---
title: Anwenderhandbuch m+m Production Order Assistant with Package Management
---

# User Guide m+m Production Order Assistant with Package Management

## Introduction

The app **m+m Production Order Assistant with Package Management** connects two m+m apps on the **Sales Line**: the **m+m Production Order Assistant** (field **Create Production Order**) and the **m+m Package Management** (field **Package Status**). It ensures that sales lines representing a package are automatically excluded from production order creation.

Without this connection, the production assistant would also try to create a **Production Order** for a package line, even though that line is not an item to be produced but a packaging object. This app prevents that: as soon as a sales line receives the **Package Status** **Package**, the **Create Production Order** flag is cleared on the same line.

The app works **rule-based in the background**. It brings **no pages, actions, setup, or master data tables of its own**. All visible fields belong to the two connected apps and appear where those apps display them — on the sales line in the **Sales Order**.

### Target audience

The primary target audience is **operational users in Sales** who record **Sales Orders** and edit **Sales Lines** every day — especially where the same sales line can act both as a production trigger (**Create Production Order**) and as a package (**Package Status**). The secondary target audience is **administrators** who establish the prerequisites: installing the two base apps and assigning the permissions.

### Short process overview

1. The user creates or changes a **Sales Line** in the **Sales Order**.
2. The **m+m Package Management** determines the **Package Status** for that line (**(blank)**, **Partial**, **Full**, or **Package**).
3. This app checks on every insert and modification of the sales line: if the **Package Status** = **Package**, **Create Production Order** on the line is automatically disabled.
4. When the sales order is **released**, the **m+m Production Order Assistant** creates a **Production Order** only for lines that have **Create Production Order** set — package lines are left out.

## Quick start for users

In day-to-day work the app requires **no operation**. The following steps show how its behavior manifests in the familiar sales order workflow.

1. **Prerequisite (one-time, by the administrator):** The apps **m+m Production Order Assistant** and **m+m Package Management** are installed, and the permission set **MuM PAPM All** is assigned to the affected users (see **Setup**).
2. Open the **Sales Order** and record a **Sales Line** in the **Lines** subpage (field **Type** = **Item**, **No.**, **Quantity**).
3. For items to be produced, set the **Create Production Order** flag on the line.
4. Assign packages as usual via the **m+m Package Management**. If the line thereby receives the **Package Status** **Package**, **Create Production Order** is automatically removed on that line — no intervention is required.
5. In the sales order, choose **Release**. The **m+m Production Order Assistant** creates **Production Orders** only for lines with **Create Production Order** set; package lines are not created as production orders.

## Setup

This app has **no setup page of its own** and **no setup fields of its own**. There is neither a number series nor report or mail parameters in this app. The entire setup consists of two administrative prerequisites and the permission assignment. The functional setup pages reside in the connected apps and are maintained in their guides; the fields essential to the interplay are described here.

### Setting up prerequisites and activation

**Who sets up:** The administrator. **When:** Before first use, before sales lines with packages and production order flags are processed. **Which process is enabled:** The automatic exclusion of package lines from production order creation in the sales order (see **Daily work in the Sales Order**).

The app is a bridge between two apps. It only takes effect when both are present and the triggering fields exist on the sales line. Set up the prerequisites in dependency order:

1. **Install m+m Package Management.** When this app is installed, the field **Package Status** exists on the sales line; only then can a line take on the value **Package** that this bridge evaluates. Without this app there is no **Package Status** and the bridge remains without effect.
2. **Install m+m Production Order Assistant.** When this app is installed, the field **Create Production Order** exists on the sales line; only then does a per-line flag decide whether a **Production Order** is created on release. Without this field there is nothing that the bridge could reset.
3. **Install this app (m+m Production Order Assistant with Package Management).** When both prerequisites are met and this app is installed, the rule becomes active: on every insert or modification of a sales line with **Package Status** = **Package**, **Create Production Order** is disabled.
4. **Configure production order creation in Sales.** In the **Prod. Assistent Setup** page, define how and in which status the **m+m Production Order Assistant** creates production orders on release. This setup controls the downstream step from which the bridge keeps the package lines out.

**Operational completion of the chain:** In day-to-day work the rule requires no separate action. It is executed automatically every time the user inserts or changes a sales line with **Package Status** = **Package** in the sales order (see **Daily work in the Sales Order**).

### Setting up permissions

**Who sets up:** The administrator. **When:** After installation, before use. **Purpose:** The permission set determines which users may run the objects provided by this app.

Assign users the permission set that ships with the app. The set **MuM PAPM All** defines the execution rights for the two processing objects of this app.

| Setup | Explanation |
|-------------|-------------|
| Permission set **MuM PAPM All** | When this set is assigned to a user or a role, then that user may run this app's background processing; without the assignment the automatic rule does not take effect for that user, because the associated objects may not be run. The set is assignable and comprises exclusively the two processing codeunits of this app. |

The app contains no further permission-relevant setup fields. The permissions on **Sales Line**, **Package Status**, and **Create Production Order** themselves are controlled via the base app and the two connected apps.

## Daily work in the Sales Order

This app acts exclusively on the **Sales Line** in the **Sales Order**. It does not present a page of its own; the two relevant fields are displayed by the connected apps in the **Lines** subpage of the sales order. Controlling preconditions reside in the setup of the connected apps: the field **Package Status** is derived by the **m+m Package Management** from the package assignment, and the field **Create Production Order** and the creation of production orders are controlled via the **Prod. Assistent Setup** (see **Setting up prerequisites and activation**).

**Entry point:** Open the desired **Sales Order** via the **Release** action or via the **Sales Orders** list and work in the **Lines** subpage.

### Fields on the Sales Line

The following fields control the interplay. Both appear on the same sales line.

| Field | Explanation |
|------|-------------|
| **Create Production Order** | When this flag is set on a sales line, then the **m+m Production Order Assistant** creates a **Production Order** for that line when the sales order is released. If it is not set, no production order is created for that line. This app automatically resets the flag as soon as the line carries the **Package Status** **Package**. |
| **Package Status** | When this field carries a value on a sales line, then it indicates to what extent packages are assigned to the line. The field is not directly editable; the **m+m Package Management** sets the value automatically from the package assignment. Once the value reaches **Package**, this app disables the **Create Production Order** flag on the same line. |
| **Package Reference No.** | When a reference is entered here, then the **m+m Package Management** links the sales line to the corresponding package document; the assignment is checked on entry and via the lookup. The field belongs to the **m+m Package Management** and influences which **Package Status** the line receives. |

The values of the field **Type** and the further standard fields of the sales line (**No.**, **Description**, **Quantity**) belong to the standard Business Central sales line and are only mentioned here to the extent needed for the workflow: a **Production Order** is created by the **m+m Production Order Assistant** only for lines with **Type** = **Item** and **Create Production Order** set.

### Meaning of the values in the Package Status field

The field **Package Status** is an option field of the **m+m Package Management**. What matters for this app is that only the value **Package** triggers the automatic disabling of **Create Production Order**. All values:

- **(blank):** No packages are assigned to the line. The line is **not** changed by this app; a set **Create Production Order** is retained.
- **Partial:** Packages are assigned to the line only for part of the quantity. The line does not count as a pure package line; this app does **not** change **Create Production Order**.
- **Full:** Packages are assigned to the line for the entire quantity, but it remains an item line. This app does **not** change **Create Production Order**.
- **Package:** The line itself represents a package. In this case, this app sets the **Create Production Order** flag to **No** on insert and modification of the line, so that no production order is created for that line.

### Posting or release workflow

The production order is not created by this app, but by the **m+m Production Order Assistant** when the sales order is released. This app intervenes on the sales line in a purely preparatory way. The workflow in interplay:

1. Select the line in the **Sales Order** (**Lines** subpage).
2. Assign packages via the **m+m Package Management** or enter a **Package Reference No.**. If the line thereby becomes a package line, it receives the **Package Status** **Package**.
3. On insert and modification of the line, this app sets the **Create Production Order** flag automatically to **No** when **Package Status** = **Package**.
4. Choose the **Release** action in the sales order.
5. The **m+m Production Order Assistant** creates a **Production Order** for all lines with **Create Production Order** set. Package lines are excluded by step 3.

In this workflow, this app shows **no message** and **no confirmation dialog**; the disabling of **Create Production Order** happens unnoticed in the background. Whether the production order creation on release occurs with or without a prompt, and in which status the production order is created, is controlled by the **Prod. Assistent Setup** of the **m+m Production Order Assistant**.

## Typical use cases

The following scenarios show how the app takes effect in the familiar sales workflow. All steps refer to standard Business Central pages and the fields of the connected apps.

### Sales order with production item and package

**Trigger:** A customer orders an item to be produced by phone; in addition, packaging is to be recorded as a separate line item.

**Entry in BC:** The user opens the **Sales Orders** list, creates a new **Sales Order**, and switches to the **Lines** subpage.

**Core workflow:**
1. The user records the first line with the **Item** to be produced (**Type** = **Item**, **No.**, **Quantity**) and sets **Create Production Order**.
2. They record a second line for the packaging and assign packages to it via the **m+m Package Management**; this line thereby receives the **Package Status** **Package**.
3. When saving this second line, this app automatically removes any **Create Production Order** that may have been set on the package line.
4. The user chooses **Release**.

**Completion:** The **m+m Production Order Assistant** creates a **Production Order** exclusively for the item line. No production order is created for the package line.

### Subsequent package assignment on a line that is already flagged

**Trigger:** A sales line was initially intended as a production item with **Create Production Order**; afterwards the line is classified as a package via package assignment.

**Entry in BC:** The user opens the affected **Sales Order** from the **Sales Orders** list and the **Lines** subpage.

**Core workflow:**
1. On the line, **Create Production Order** is already set.
2. The user assigns packages via the **m+m Package Management** or enters the **Package Reference No.**; the line switches to **Package Status** **Package**.
3. Because the line is changed when saving, this app's rule takes effect: **Create Production Order** is set to **No**.

**Completion:** On the later **Release**, no **Production Order** is created for this line anymore, even though the flag was originally set.

## FAQ and troubleshooting

### 1. Why is no production order created for a sales line?

Check the **Package Status** of the line. If it shows **Package**, this app has automatically disabled the **Create Production Order** flag; by design, no **Production Order** is created for package lines.

### 2. Why can the Create Production Order flag not be set permanently on a package line?

As soon as the line is inserted or changed with **Package Status** = **Package**, this app sets **Create Production Order** back to **No**. This is intentional: a package line should not trigger a production order.

### 3. What happens if a line has the Package Status Full or Partial?

In these cases, this app's rule does **not** take effect. Only the value **Package** triggers the disabling of **Create Production Order**. With **Full** or **Partial**, a set **Create Production Order** is retained.

### 4. Do I have to operate the app in daily work?

No. The app has no page and no action of its own. On every insert and modification of a sales line, it automatically checks the **Package Status**.

### 5. Why do I not see a setup page of the app's own?

The app deliberately brings no setup. It controls itself entirely via the **Package Status** of the sales line. Configuration is done exclusively in the connected apps (**m+m Package Management** and **m+m Production Order Assistant**).

### 6. When exactly is Create Production Order reset?

On **inserting** a new sales line and on **modifying** an existing sales line — in each case precisely when the **Package Status** of the line has the value **Package**.

### 7. Can I disable the automatic reset for individual lines?

No. The rule applies uniformly to all sales lines with **Package Status** = **Package**. A line-by-line exception is not provided.

### 8. Why does nothing happen even though I have assigned packages?

Check whether the line has actually reached the **Package Status** **Package**. With only partial assignment it shows **Partial** or **Full**, and the rule does not take effect. The **Package Status** is derived by the **m+m Package Management** from the assignment.

### 9. Which permission is required for the app?

Assign users the permission set **MuM PAPM All**. Without this permission, this app's processing may not be run, and the rule does not take effect for the affected user.

### 10. Does the app work without the two connected apps?

No. Without **m+m Package Management** there is no **Package Status**, and without **m+m Production Order Assistant** there is no **Create Production Order** field. Both apps are prerequisites; only with them does the bridge become effective.
