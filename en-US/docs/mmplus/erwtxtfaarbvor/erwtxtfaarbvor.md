---
title: Anwenderhandbuch m+m Ext. Text Module with Production Order Job Overview
---

# User Guide m+m Ext. Text Module with Production Order Job Overview

## Introduction

The app **m+m Ext. Text Module with Production Order Job Overview** extends Microsoft Dynamics 365 Business Central with additional **FactBoxes** and an action on the **Prod. Order Job Overview** page (German caption *FA-Arbeitsvorrat*). This makes the extended texts of a production order that are stored in the **Ext. Text Module** visible directly at the workstation, without the user having to switch into the production order or into individual documents.

In three FactBoxes the app shows the extended texts of

- the **production order** (header text of the production order),
- the **production order lines** (line text of the production order line), and
- the **operations** (text of the routing line),

each related to the routing line selected in the **Prod. Order Job Overview** for a **released** production order. In addition, the **Extended Production Text** action opens the complete text maintenance for the selected production order.

**Target audience:** Primarily **operational users** in production — machine operators, work scheduling, and production control staff who process operations in the **Prod. Order Job Overview** every day and need to read the stored notes, work instructions, and additional information. Secondarily, this guide is aimed at **administrators** and **key users** who set up the prerequisites in the **Ext. Text Module** and in the **Prod. Order Job Overview** module.

**Short process overview:** A key user maintains the extended texts on the production order (header, line, operation) via the **Ext. Text Module**. The operational user then opens the **Prod. Order Job Overview**, filters on their **work center** or **work center group**, selects a routing line, and reads the texts in the three FactBoxes. When needed, they open the complete text view via **Extended Production Text**.

> This app adds only display and text-viewing functions to the **Prod. Order Job Overview** page. It contains no posting, release, or inventory processes of its own. The texts themselves are captured via the dependent **Ext. Text Module**.

## Quick Start for Users

The fastest way to the extended texts in the **Prod. Order Job Overview**:

1. **Prerequisite (administrator/key user):** The extended texts must exist on the production order. They are captured on the header, line, and operation via the **Ext. Text Module** (see the chapter **Prerequisites and Setup**).
2. **Open the Prod. Order Job Overview:** Use **Search** to open the **Prod. Order Job Overview** page.
3. **Select the work center group:** In the **Work Center Group No.** filter, set the desired work center group.
4. **Select the work center (optional):** Narrow the display with the **Work Center No.** filter to a single work center. This step is optional.
5. **Select a routing line:** In the list, select the routing line you want to process.
6. **Read the texts:** Read the texts matching the selected line in the three FactBoxes **Production Text**, **Production Line Text**, and **Routing Text**.
7. **Complete text view (optional):** Use the **Extended Production Text** action to open the complete text maintenance for the production order.

## Prerequisites and Setup

This app has **no setup pages of its own**. It displays data that originates in two prerequisite modules. Setup is therefore performed in the following order (dependency order):

1. **Provide the Prod. Order Job Overview module** — The **Prod. Order Job Overview** page comes from the **m+m Production Order Job Overview** module. Without this module, the extended page is not available. The administrator ensures that the module is installed and authorized for the affected users. **If** the module is provided, **then** the **Prod. Order Job Overview** page is reachable via **Search** and can be filtered by work center group and work center.
2. **Provide the Ext. Text Module** — The extended texts and the three FactBoxes as well as the complete text view come from the **m+m Ext. Text Module**. **If** this module is provided, **then** text maintenance on the production order and the display of the texts in the FactBoxes are available.
3. **Assign permissions** — The administrator assigns the appropriate permission sets to the users (see **Permissions**).

### Permissions

The app ships the permission set **All Ext. Text Module with Production Order Job Overview permissions** (the app's internal permission set). It defines which actions users may perform within the scope of this app; it comprises only the execution permission for this app's internal processing. **If** the permission set is assigned to a user, **then** that user can use the FactBoxes provided by the app and the **Extended Production Text** action. The permissions to read and maintain the actual texts, and to open the **Prod. Order Job Overview**, additionally derive from the prerequisite modules **Ext. Text Module** and **Prod. Order Job Overview**.

> **Note on text maintenance:** *Capturing* the extended texts on the production order is part of the **Ext. Text Module**. This guide describes **how** and **where** these texts are displayed and opened in the **Prod. Order Job Overview**. For the detailed setup of the Ext. Text Module (e.g. text templates, language versions, print and report parameters), refer to the guide for the **Ext. Text Module**.

## The Prod. Order Job Overview as Entry Point

The **Prod. Order Job Overview** is the central working page in which this app operates. The user opens the page via **Search** and narrows it down using the header filters before selecting a routing line.

### Entry and Filters

**Entry:** Open the **Prod. Order Job Overview** page via **Search**.

The page is organized by two related filter levels. Set the **work center group** first and then, if needed, narrow down to a single **work center**.

| Filter Field | Explanation |
| --- | --- |
| **Work Center Group No.** | When set, the displayed routing lines are filtered to the selected work center group; the user sees only the operations within their area of responsibility. This is the superordinate filter and is set first. |
| **Work Center No.** | When set, the lines are additionally narrowed down to a single work center within the work center group. This filter is optional and is set after the work center group; without an entry, all work centers of the selected group remain visible. |

After filtering, the user selects the routing line to be processed. All FactBoxes added by this app and the **Extended Production Text** action always relate to the currently selected line.

## FactBoxes with Extended Texts

This app adds three FactBoxes to the **Prod. Order Job Overview**. All three relate to **released** production orders and update their content automatically as soon as the user selects a different routing line. The FactBoxes show the texts in display mode **FactBox** (print type of the display) — the same texts can additionally be intended for **Report** in the Ext. Text Module.

### FactBox "Production Text"

**Process context:** This FactBox shows the extended **header text** of the released production order. It is maintained by the key user on the production order header and serves the operational user as order-related overall information (e.g. cross-operation production notes).

The FactBox is bound to the header data of the production order. The decisive fields are:

| Field | Explanation |
| --- | --- |
| **Production Text** | Displays the extended header text of the production order. If a released production order with a stored header text exists for the selected line, then this text appears here; without a stored text, the FactBox remains empty. |
| **Prod. Order No.** | Determines for which production order the header text is loaded. When the user selects a line, then the production order number of the line is used to select the header text. |

**Relation to the selected line:** The production order for the **Prod. Order No.** of the currently selected routing line is always loaded; the document status is fixed to **Released**.

### FactBox "Production Line Text"

**Process context:** This FactBox shows the extended **line text** of the production order line. It supplements the header text with line-specific notes (e.g. about the specific item to be produced).

| Field | Explanation |
| --- | --- |
| **Production Line Text** | Displays the extended text of the production order line. If a production line with a stored text exists for the selected routing line, then it appears here; otherwise the FactBox remains empty. |
| **Prod. Order No.** | Together with the line number, determines which production line is loaded. |
| **Prod. Order Line No.** | Determines the specific production line within the production order. When the user selects a line, then the matching line text is determined via Prod. Order No. and Prod. Order Line No. |

**Relation to the selected line:** The text is determined via the **Prod. Order No.** and **Prod. Order Line No.** of the selected routing line; the document status is fixed to **Released**.

### FactBox "Routing Text"

**Process context:** This FactBox shows the extended text of the **operation** (routing line) and is therefore the most important FactBox for daily processing: it provides the specific work instruction for the selected operation. The FactBox is rebuilt on every line change and narrowed down exactly to the selected operation.

| Field | Explanation |
| --- | --- |
| **Routing Text** | Displays the extended text of the routing line. If a routing text is stored for the selected line, then it appears here; otherwise the FactBox remains empty. |

The routing text is narrowed down automatically via several criteria of the selected line:

| Field | Explanation |
| --- | --- |
| **Prod. Order No.** | When set, the routing text is narrowed down to the production order of the selected line. |
| **Line No.** | When set, it is narrowed down to the corresponding production line or routing reference line. |
| **Operation No.** | When set, it is narrowed down to exactly the selected operation; this way the user sees only the text for the work step they are currently working on. |
| **Routing No.** | When set, the text is assigned to the correct routing of the production order. |
| **Center No.** | When set, the text is assigned to the capacity (work center or work center group) of the operation, so that the display matches the center that actually performs the work. |

**Relation to the selected line:** The routing text is determined via the routing line of the production order and narrowed down to the **Prod. Order No.**, **Line No.**, **Operation No.**, **Routing No.**, and **Center No.** of the selected line. The document status (**Prod. Order Status**) of the selected line is passed to the FactBox so that the text is loaded for the correct status.

## Action "Extended Production Text"

In addition to the FactBoxes, the app provides the **Extended Production Text** action. It is pinned in the ribbon of the **Prod. Order Job Overview** (Process category) and opens the complete text maintenance of the Ext. Text Module for the production order of the selected line.

**Use the Extended Production Text action to open the complete text view** of the production order. The following applies:

- The production order for the **Prod. Order No.** of the selected line is used.
- The document status is fixed to **Released**; the action therefore opens the texts of the released production order.

While the FactBoxes display the texts compactly at the edge, the action offers the complete view of the document texts of the production order and is suitable for reading longer texts or for users who need more context than the FactBox shows.

### Status Values of the Document Type

The underlying text assignment of the Ext. Text Module distinguishes several document types of a production order. This app consistently uses the value **Released**. The complete value set of the document type is:

- **Simulated:** Texts of a simulated production order. **Not** used by this app — the FactBoxes and action do not access simulated orders.
- **Planned:** Texts of a planned production order. **Not** used by this app.
- **Firm Planned:** Texts of a firm planned production order. **Not** used by this app.
- **Released:** Texts of the released production order. **This value is used by the app:** the FactBoxes and the **Extended Production Text** action access released production orders exclusively, because only these are processed in the **Prod. Order Job Overview**.
- **Finished:** Texts of a finished production order. **Not** used by this app.

### Display Mode (Print Type of the Display)

The FactBoxes of this app run in display mode **FactBox**. The corresponding value set in the Ext. Text Module is:

- **FactBox:** The text is displayed as a FactBox next to the list. **This mode is used by the three FactBoxes of this app.**
- **Report:** The text is intended for output in a report. Not relevant for the display in the **Prod. Order Job Overview** by this app; the report output of the texts is controlled by the Ext. Text Module.

## Typical Use Cases

The following scenarios show how operational users use the FactBoxes and the action provided by this app in their daily routine. All screens, filters, and actions described are available in the **Prod. Order Job Overview** and in the associated FactBoxes.

### Scenario 1: Read the Work Instruction at the Workstation

1. **Trigger:** A machine operator starts their shift and wants to know which special aspects apply to the upcoming operations.
2. **Entry in BC:** The operator opens the **Prod. Order Job Overview** via **Search** and sets their work center group in the **Work Center Group No.** filter; if needed, they narrow down to their work center with **Work Center No.**
3. **Core flow:** They select the first routing line to be processed. In the **Routing Text** FactBox they read the specific work instruction for the selected operation. In the **Production Line Text** FactBox they see line-specific notes about the item, and in the **Production Text** FactBox they see cross-operation notes about the entire production order.
4. **Completion:** When switching to the next line, all three FactBoxes update automatically. No further steps are required in this app; the processing of the operations themselves is performed via the functions of the **Prod. Order Job Overview** module.

### Scenario 2: View the Complete Production Text

1. **Trigger:** The text in the **Production Text** FactBox is extensive, and the user wants to read the complete header text of the production order.
2. **Entry in BC:** In the **Prod. Order Job Overview**, the user selects a routing line of the production order concerned.
3. **Core flow:** In the ribbon they choose the pinned **Extended Production Text** action. The complete text view of the released production order for the **Prod. Order No.** of the selected line opens.
4. **Completion:** The user reads the complete text and closes the view again. Changes to the texts themselves are made via the text maintenance of the Ext. Text Module.

### Scenario 3: Check Why No Texts Appear

1. **Trigger:** A user reports that the FactBoxes remain empty.
2. **Entry in BC:** In the **Prod. Order Job Overview**, the key user selects the same routing line.
3. **Core flow:** They check whether the associated production order is **released** (only released orders are displayed) and whether any texts are stored at all on the header, line, or operation in the Ext. Text Module.
4. **Completion:** If the texts are missing, they are added via the text maintenance of the Ext. Text Module; afterwards they appear automatically in the FactBoxes when the line is selected again.

## FAQ and Troubleshooting

### 1. Why do I not see any extended texts in the Prod. Order Job Overview?

The FactBoxes access **released** production orders exclusively and display only texts that have been stored in the Ext. Text Module on the header, line, or operation. If no released order exists for the selected line, or no texts are maintained, then the FactBoxes remain empty.

### 2. Where do I maintain the texts that appear in the FactBoxes?

The texts are not captured in this app but via the prerequisite **Ext. Text Module** on the production order (header, line, operation). This app merely displays these texts in the **Prod. Order Job Overview**.

### 3. What does the "Production Text" FactBox show compared to "Production Line Text"?

**Production Text** shows the header text of the entire production order (cross-order). **Production Line Text** shows the text of the individual production order line (item- or line-specific). Both relate to the **Prod. Order No.** of the selected line.

### 4. Why does the routing text change when I select a different line?

The **Routing Text** FactBox is rebuilt on every line change and narrowed down exactly via the **Prod. Order No.**, **Line No.**, **Operation No.**, **Routing No.**, and **Center No.** of the selected line. This way you always see only the text for the operation you are currently working on.

### 5. How do I open the complete text view?

In the **Prod. Order Job Overview**, select a routing line and choose the **Extended Production Text** action in the ribbon. The complete text view of the released production order for the **Prod. Order No.** of the selected line opens.

### 6. Why does the action open only released orders?

The **Prod. Order Job Overview** serves the processing of released production orders. The **Extended Production Text** action is therefore fixed to the document type **Released** and does not access simulated, planned, firm planned, or finished orders.

### 7. How do I make sure I see only the operations for my work center?

In the **Prod. Order Job Overview**, first set the **Work Center Group No.** filter and then, optionally, **Work Center No.** The FactBoxes and the action then relate to the line you select within this filtering.

### 8. Do I always have to set the Work Center No. filter?

No. The **Work Center No.** filter is optional. Without an entry you see all work centers of the selected **work center group**; with an entry you narrow down to a single work center.

### 9. Which permissions do I need for this app?

For the functions of this app, the permission set **All Ext. Text Module with Production Order Job Overview permissions** is required. In addition, you need the permissions of the prerequisite modules **Prod. Order Job Overview** (to open the page) and **Ext. Text Module** (to read and maintain the texts).

### 10. Is the text updated automatically, or do I have to reload it?

The FactBoxes update automatically as soon as you select a different routing line. Manual reloading is not required. When new texts are maintained in the Ext. Text Module, they appear when the line is selected again.
