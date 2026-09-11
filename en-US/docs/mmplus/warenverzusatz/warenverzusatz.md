---
title: Anwenderhandbuch m+m Goods Receipt with Ext. Production Information
---

# User Guide m+m Goods Receipt with Ext. Production Information

## Introduction

The **m+m Goods Receipt with Ext. Production Information** extension is a bridge component between the m+m **Goods Receipt** and the m+m extension for extended production information. It automatically copies the **Routing No.** from the item or from the item reference onto the line of a Warehouse Receipt document. The user therefore no longer has to enter the Routing No. on the document line by hand.

**Target audience.** The primary audience is **operational users in goods receiving** – that is, employees who record incoming goods and create document lines in **Goods Receipt** every day. Secondarily, the extension concerns administrators and master data owners who maintain the Routing No. at the two data sources (Item Card and Item Reference) and who assign the permissions.

**Short process overview.** In the **Warehouse Receipt**, the user records a document line in the **Finished Material** line area and enters an **Item No.** or an **Item Reference No.** there. As soon as this field is validated, the extension determines the matching **Routing No.** in the background and writes it to the document line:

1. If an **Item Reference No.** is set on the line and the corresponding **Item Reference** carries a Routing No., then that value is used.
2. If no Item Reference No. is set (or the Item Reference carries no Routing No.), then the **Routing No.** is taken from the **Item Card**.

The extension has **no pages, actions or setup fields of its own**. It acts solely as an automation on the existing Warehouse Receipt line. All pages and fields mentioned below belong to **Goods Receipt**, to the extension for production information, or to the standard of Microsoft Dynamics 365 Business Central; this guide describes only the portion that the automation affects.

## Quick Start for Users

The fastest way to the result – the automatically filled **Routing No.** on the Warehouse Receipt line:

1. **Prerequisite (one-time, by the administrator/master data owner):** Store a Routing No. at the data source – either on the **Item Card** in the **Routing No.** field or on the **Item Reference** in the **Routing No.** field (see *Master Data*). Without a maintained Routing No., the field on the line stays empty.
2. Open the **Warehouse Receipt** via the Business Central **Search** (or via **Create Goods Receipt** if you are creating a new document).
3. Switch to the **Finished Material** line area (subpage **Lines**) and create a line.
4. Enter the **Item No.** and confirm the field. If the item carries a Routing No. and no Item Reference No. is set, then the **Routing No.** appears in the line immediately.
5. *Optional:* Instead or in addition, enter an **Item Reference No.** and confirm the field. If the Item Reference carries a Routing No., then it overwrites the previously determined Routing No.
6. Check the **Routing No.** in the line and continue processing the Warehouse Receipt document as usual.

> The order is deliberate: **setup/master data first**, then the document line. If the Routing No. is not maintained at the source, the automation cannot copy anything.

## Setup

The extension brings **no setup page and no setup fields of its own**. The automation is active without configuration after installation. For this extension, "setting up" therefore means: create the **business prerequisites** so that a Routing No. can be copied at all, and assign the **permissions**.

### Permissions

The extension ships an assignable permission set that bundles the execution rights for the two automation codeunits.

| Setup | Explanation |
|---|---|
| Permission set **MuM GRAP All** | Determines which users are allowed to run the extension's automation. If you assign this permission set to a user or a user group, then that user is allowed to use the extension's execution logic; the Routing No. is copied automatically when the Warehouse Receipt line is recorded. Without this permission, the copy operation that runs in the background cannot be executed. The permission set determines only the execution rights of the two automation building blocks and contains no data rights on documents or master data. |

### Setting Up Routing Copy

The automatic copying of the Routing No. onto the Warehouse Receipt line is the only business capability of this extension. It is not activated by a switch, but takes effect through a **chain of prerequisites** across several areas. This chain is set up by the administrator or master data owner **before the first productive use**.

**Who sets it up and when.** Before the first goods receipt, the administrator makes sure that the dependent modules are present and the permissions have been assigned. The master data owner maintains the Routing No. on the items and item references. The result is later applied by the operational user in *Daily Work* (see there).

**Setup steps in dependency order:**

1. **Provide the dependent modules.** If the extension is installed, then the prerequisite modules **m+m Cloud Base**, **m+m Goods Receipt** and **m+m Ext. Production Information** must also be installed and licensed; only then do the Warehouse Receipt line with the **Routing No.** field and the **Routing No.** field on the Item Reference – which the automation accesses – exist. The extension also checks the license automatically at login.
2. **Assign permissions.** If you assign the **MuM GRAP All** permission set to the affected users, then they are allowed to run the copy operation (see *Permissions*).
3. **Maintain the data source (master data).** If you store a **Routing No.** on the **Item Card** and/or on the **Item Reference**, then a value is available for the automation to copy (see *Master Data*). Without a maintained Routing No., the line stays empty – this is not an error, but the expected behaviour.
4. **Operational completion of the chain.** When the user confirms the **Item No.** or the **Item Reference No.** in the Warehouse Receipt line, then the automation copies the matching Routing No. into the **Routing No.** field of the line (see *Daily Work*).

This way the chain interlocks: module and permission prerequisite → maintained master data → user action on the document line.

## Master Data

The Routing No. that is copied onto the Warehouse Receipt line comes from **one of two** master data sources. Both are maintained by the master data owner before the Warehouse Receipt lines are recorded. The automation evaluates them with a clear priority: **Item Reference before Item.**

### Routing No. on the Item Card

**Process.** For each production item, the master data owner stores the default routing on the **Item Card**. This value serves as a **fallback**: it is copied when the line carries no Item Reference No. or the Item Reference carries no routing of its own. The value is applied in *Daily Work* when the Item No. is confirmed.

**Entry point:** Open the item list via **Search**, open the **Item Card** of the item concerned and maintain the **Routing No.** field.

| Field | Explanation |
|---|---|
| **Routing No.** (Item Card) | If you store a routing here, then exactly this Routing No. is copied onto the Warehouse Receipt line as soon as the user confirms the Item No. and no (routing-carrying) Item Reference No. is on the line. If the field is empty, then the Routing No. on the line stays empty and must be entered manually if needed. |

### Routing No. on the Item Reference

**Process.** For customer-specific cases, the master data owner maintains the **Routing No.** directly on the **Item Reference** (a field from the extension for production information). This value takes **precedence** over the routing of the Item Card. It is applied in *Daily Work* when the Item Reference No. is confirmed.

**Entry point:** Open the **Item Card**, call up the associated **Item References** and maintain the **Routing No.** field there.

| Field | Explanation |
|---|---|
| **Routing No.** (Item Reference) | If you store a routing on an Item Reference, then the automation copies this Routing No. onto the Warehouse Receipt line with priority, as soon as the user confirms the matching Item Reference No. The default routing of the Item Card is not used in this case. If the field is empty, then the automation falls back to the routing of the Item Card. |
| **Reference Type** (prerequisite) | The Routing No. can only be maintained on the Item Reference **if** the **Reference Type** has the value **Customer**. If you try to enter the Routing No. for a different Reference Type, then Business Central prevents the entry with a field validation. In practice this means: customer-specific routings via the Item Reference are intended exclusively for **customer-related** references. |

> **Priority rule (important for maintenance):** If both the Item Reference and the Item Card carry a routing, then the **Item Reference** wins. Maintain the Item Card as the general default and the Item Reference only where a customer requires a deviating routing.

## Daily Work on the Warehouse Receipt Line

Daily work takes place in the **Warehouse Receipt** document. The area relevant to this extension is the **Finished Material** line area (subpage **Lines**). This section is controlled by the master data from the previous chapter: the **Routing No.** on the **Item Card** and on the **Item Reference** determine which value is written automatically into the line. Therefore create this master data before recording the document (cross-reference: *Master Data*, *Setting Up Routing Copy*).

**Entry point:** Open the **Warehouse Receipt** via **Search** or via **Create Goods Receipt** and switch to the **Finished Material** line area.

On the line, the following fields are decisive for the automation (further columns of the Warehouse Receipt line belong to Goods Receipt and are described there):

| Field | Explanation |
|---|---|
| **Item No.** | If you enter and confirm the Item No. and the line carries **no** Item Reference No., then the automation copies the **Routing No.** from the Item Card of this item (provided it is maintained there). If the item carries no routing, then the field stays empty. |
| **Item Reference No.** | If you enter and confirm an Item Reference No. and the corresponding Item Reference carries a **Routing No.**, then this is copied into the line with priority. If the Item Reference carries no routing, then the automation falls back to the Routing No. of the Item Card. |
| **Routing No.** | Target field of the automation. If one of the two sources supplies a routing, then the Routing No. is present in the line after confirmation without any further entry. The value is set through the regular field validation, so that dependent checks of the line are triggered. You can overwrite the value manually if needed. |
| **Description**, **Quantity**, **Unit of Measure Code**, **Location Code** | Usual line fields of the Warehouse Receipt (no influence from the automation). You record them as usual; they are mentioned here only as context of the line. |

**Flow of the automation (derived from the code):**

1. You confirm the **Item No.** on the line → if no Item Reference No. is set, the **Routing No.** is copied from the Item Card (only if it is not empty there).
2. You confirm the **Item Reference No.** on the line → if the Item Reference carries a **Routing No.**, it is copied; otherwise the Routing No. of the Item Card is copied.

The extension provides **no buttons of its own**; there is no separate action to trigger the copy. It happens solely through the field confirmation.

## Typical Use Cases

The following flows show the two realistic triggers for the automation. All fields and pages mentioned are backed by the code of the extension and the dependent modules.

### Use Case 1 – Routing from the Item

**Trigger.** Finished material arrives in goods receiving for which a default routing is stored on the item; a customer-specific reference is not involved.

**Entry point in BC.** The user opens the **Warehouse Receipt** via **Search** and switches to the **Finished Material** line area.

**Core flow.**
1. The user creates a line and enters the **Item No.**
2. On confirmation, the automation checks: no **Item Reference No.** set → it reads the **Routing No.** from the **Item Card**.
3. If a routing is stored there, then the **Routing No.** appears in the line immediately.

**Completion.** The user completes the line (Quantity, Location Code) and continues processing the Warehouse Receipt document in the usual process. Manual entry of the Routing No. is no longer needed.

### Use Case 2 – Routing from the Item Reference (customer-specific)

**Trigger.** A deviating routing applies for a specific customer. This is stored as **Routing No.** on the **Item Reference** (Reference Type **Customer**).

**Entry point in BC.** The user opens the **Warehouse Receipt** via **Search** and switches to the **Finished Material** line area.

**Core flow.**
1. The user enters the **Item Reference No.** on the line and confirms it.
2. The automation reads the **Routing No.** from the Item Reference and writes it into the line – **with priority** over any routing of the Item Card.
3. If, by way of exception, the Item Reference carries no routing, then the automation copies the **Routing No.** from the Item Card instead.

**Completion.** The user checks the copied **Routing No.** and continues processing the document. This way, the customer-specific goods receipt automatically gets the correct routing.

## FAQ and Troubleshooting

### 1. Why does the Routing No. appear automatically on my Warehouse Receipt line?
Because the extension copies the matching **Routing No.** from the item or the item reference when you confirm the **Item No.** or the **Item Reference No.** That is the entire purpose of the extension.

### 2. Where does the copied Routing No. come from – from the item or from the item reference?
If the line carries an **Item Reference No.** and this reference carries a routing, then the value comes from the **Item Reference**. Otherwise it comes from the **Routing No.** of the **Item Card**.

### 3. What happens if both the item and the item reference have a routing?
Then the **Item Reference** wins. Its routing is copied with priority; the routing of the Item Card is not used in this case.

### 4. Why does the Routing No. field on the line stay empty?
Because no routing is maintained at either source: the **Item Card** carries no **Routing No.**, and no (routing-carrying) **Item Reference No.** is set. Maintain the Routing No. at the desired source, then it is copied on the next confirmation.

### 5. Why can't I save the Routing No. on the Item Reference?
Because the **Reference Type** is not **Customer**. The Routing No. on the Item Reference is intended only for customer-related references; for a different Reference Type, a field validation prevents the entry.

### 6. Do I have to press a button for the Routing No. to be copied?
No. There is **no** dedicated action. The copy runs automatically when the **Item No.** or the **Item Reference No.** is confirmed on the line.

### 7. What happens if I change the Item No. after an Item Reference No. is set?
As long as an **Item Reference No.** is on the line, the automation does **not** copy the routing of the Item Card when the Item No. is confirmed. The path via the Item Card takes effect only when no Item Reference No. is set.

### 8. Can I overwrite the automatically set Routing No.?
Yes. The Routing No. is a regular field of the Warehouse Receipt line. You can change the copied value manually; the extension sets it only at the moment of the field confirmation.

### 9. Why am I checked for a license at login?
The extension performs a **license check** via the m+m payment module at login. If the license is valid, then you notice nothing of it; the check ensures that the automation is allowed to run.

### 10. I maintained the Routing No. on the item, yet the line stays empty – what's the reason?
Check three points: (a) Is there an **Item Reference No.** without a routing of its own on the line? Then the item routing should take effect – is the Item Card really filled? (b) Was the **Item No.** **confirmed** again after maintenance? The copy happens only on field confirmation. (c) Does the user have the **MuM GRAP All** permission set? Without the execution right, the automation cannot run.
