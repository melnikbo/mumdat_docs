---
title: Anwenderhandbuch m+m Production Campaign with Rework
---

# User Guide m+m Production Campaign with Rework

## Introduction

The **m+m Production Campaign with Rework** module connects the production campaign with the rework logic of Business Central. It adds the action **Rework** to the **Production Campaign** page: users select the affected campaign lines and trigger a rework operation from them. Depending on the selected **Rework Process**, the affected quantity is either transferred into a new **Production Order** (process **To Production**) or treated as scrap (process **To Junk**). If the same production order quantity is split across several campaigns or operations, the module additionally requires a manual distribution of the quantity reduction in the **Update Campaign Lines** wizard.

The extension has **no setup page of its own** and no separate overview list. It builds entirely on three base apps: the production campaign (campaigns, campaign lines, linked production orders), the rework logic (number series, production status, defect types and defect reasons, junk location), and the Cloud Base license check.

### Target audience

The primary target audience is **operational users in production control** – production scheduling, production planning, and shop floor control – who work with the production campaign in their day-to-day business and handle quality and scrap cases there. Administrators and key users are the secondary target audience: in **Manufacturing Setup** they configure the number series and the production status for rework, and on the **Location Card** they enable junk locations.

### Process overview

Check prerequisites (campaign, campaign line, linked production order) → mark line(s) → action **Rework** → fill in the **Rework Dialog** (defect type, defect reason, quantity, and for junk additionally the junk location) → for split quantities, fill in the **Update Campaign Lines** wizard → **Finish**. The module posts the rework directly and automatically adjusts the campaign and production order quantities.

## Quick start for users

The fastest path from a quality or scrap case to a posted rework. The setup (see the **Setup** chapter) must have been carried out once by an administrator before the first operation can be posted.

1. **Prerequisite (one-time, administrator):** In **Manufacturing Setup**, the **Production Status**, **To Junk Nos.**, and **To Production Nos.** are maintained; for junk, at least one location with **Allow Junk** exists.
2. Open the **Production Campaign** page and select the affected campaign. In the header, the **Rework** indicator shows whether a rework reference already exists for this campaign.
3. Switch to the campaign lines and mark the affected line (or several lines).
4. In the lines, choose the action **Rework**. The **Rework Dialog** opens.
5. For each line, enter at least **Rework Defect Type Code**, **Rework Defect Reason Code**, and **Quantity**. The **Rework Process** is derived automatically from the defect type:
   - For **To Production**, you can optionally specify an **Alternate Routing**.
   - For **To Junk**, you additionally fill in the **Junk Location Code** and – for locations that require bins – the **Junk Bin Code**.
6. Close the dialog with **OK**. The module checks all mandatory fields and quantities.
7. If the **Update Campaign Lines** wizard appears, enter the future remaining quantity for each affected line in **New Quantity**, until the total **Lowered Quantity** matches the **Needed Quantity to Lower**. Close the wizard with **Finish**.
8. The module posts the rework directly: it reduces the affected campaign and production order quantities, marks the source line as **Reworked**, and for **To Production** creates a new **Production Order** for the rework quantity.

## Setup

This extension comes with **no setup page of its own**. All prerequisites are maintained on existing standard or base-module pages. An administrator sets them up once before the first rework operation can be posted from a production campaign. If these values are not maintained, no document number can be assigned when saving a rework line, and the operation aborts with an error message.

### Setting up Manufacturing Setup for rework

**Process entry:** The administrator defines these values before first use. They control which production order status and which number series the rework uses to generate its documents. The **Rework Dialog** (chapter **Daily work**) accesses these values on every posting.

**Entry point:** **Manufacturing Setup** is a company-wide setup page (one record per company). Open it via **Search** and enter **Manufacturing Setup**.

| Setup | Explanation |
|---|---|
| **Production Status** | When set, a production order newly created for **To Production** is created with exactly this status (e.g. planned, firm planned, or released). Without a status set, saving the rework line aborts, because the module does not know the target status of the new order. |
| **To Junk Nos.** | When set, the module automatically assigns a document number from this series when saving a rework line with the process **To Junk**. If the series is missing, no junk operation can be saved. |
| **To Production Nos.** | When set, the module automatically assigns a document number from this series when saving a rework line with the process **To Production**. If the series is missing, no to-production rework operation can be saved. |

> Note: The production status is additionally used when reading the target status for the new production order. It is therefore always required for the **To Production** process, regardless of whether a junk or a to-production operation is posted in the specific case.

### Enabling junk storage (location and bin)

**Process entry:** So that the **To Junk** process can offer a location in the **Rework Dialog**, the administrator must explicitly enable the relevant location (and, where bins are mandatory, also the bins) for the junk process. Without this enablement, the location does not appear in the **Junk Location Code** selection, and a junk operation cannot be completed.

**Entry point:** Open the **Locations** (overview), select the desired location, and open the **Location Card**. For locations that require bins, additionally open the associated **Bins**.

| Setup | Explanation |
|---|---|
| **Allow Junk** (location) | When enabled, this location can be selected in the **Junk Location Code** field. Without the enablement, the location is not available for junk, and the user cannot save the junk operation. |
| **Allow Junk** (bin) | When enabled, this bin can be selected in the **Junk Bin Code** field. If the selected location requires bins, an enabled bin is mandatory so that the dialog can be closed. |

### Permissions

The extension delivers the permission set **MuM PCRW All** ("All permissions"). It defines which actions users are allowed to perform in the rework of the production campaign: read and write access to the rework line as well as running the associated codeunits and pages (Rework Dialog and the **Update Campaign Lines** wizard). Assign this permission set to the users who are to post rework from production campaigns; without these permissions, the **Rework** action has no effect.

## Daily work in the production campaign

All daily work of this extension takes place on the existing **Production Campaign** page. The extension does not change the basic logic of the campaign but adds an indicator in the header and an action in the lines. The actual entry then takes place in the **Rework Dialog**.

The prerequisite is that the campaign line is already linked to a production order. When the action starts, the module reads the line, the associated production order, the operation, and the available campaign quantity. Therefore, before starting, check at least: campaign no., production order status, production order no., operation, and the current campaign quantity of the line.

### Indicator in the campaign header

The extension adds a single field to the header of the **Production Campaign**.

| Field | Explanation |
|---|---|
| **Rework** | When set, at least one posted rework operation with a campaign reference already exists for this campaign. The field is calculated automatically and is not editable; it serves as a quick visual check of whether the campaign has already been reworked. If it is empty, no rework with a campaign connection has yet been posted for this campaign. |

### Rework action in the campaign lines

In the campaign lines, the extension adds the **Rework** action. It is the only user-driven action of this module in the daily workflow.

Use the **Rework** action to open the **Rework Dialog**: mark one or more campaign lines and choose **Rework**. The module then creates a temporary rework line for each marked line and automatically transfers the item, variant, unit, description, available quantity, and the origin (campaign no. and line no.) into the dialog. Only after confirming the dialog do real rework documents result from this, which are posted immediately.

### The Rework Dialog

The **Rework Dialog** is the central entry screen of the rework. When opened, the **Production Rework Type** is set to **Item** by default, and the system shows a note: if the rework is run as **To Junk** from a production campaign, the module does **not** automatically move the item to the junk location. Instead, the quantity of the production order line is reduced and the operation is logged in the rework logic.

The dialog is divided into three areas: the header area **General**, the **Origin Document Information** area, and the line area **Lines**.

#### Header and origin fields (General, Origin Document Information)

| Field | Explanation |
|---|---|
| **Description** | Description of the affected item or operation. Display only; taken from the campaign line. |
| **Variant Code** | Variant of the item. Display only; comes from the linked production order line. |
| **Unit Of Measure Code** | Unit of measure used. Display only; comes from the production order line and determines the conversion to the base quantity. |
| **Origin Process** | Display only. Shows which process the rework originates from. When entered from the production campaign, this shows **In Production**. Further values of the underlying rework logic are **In Sales** and **After Production**. |
| **Origin Document Type** | Display only. Identifies the origin of the record. For campaign rework this shows **Production Campaign**; the underlying logic additionally knows **Sales** and **Production**. |
| **Origin Document No.** | Display only. Number of the origin document – here the campaign no. of the marked line. |

On the meaning of the option values in the header area:

- **Origin Process** – **In Production:** The rework originates from an ongoing production operation; this is the case when entering via the production campaign. **In Sales:** The rework would have been triggered from sales. **After Production:** The rework relates to goods already reported as finished.
- **Origin Document Type** – **Production Campaign:** value added by this extension; identifies rework with a campaign reference and controls that the campaign-specific posting logic applies. **Sales** / **Production:** origin from the sales or production context of the base logic.

#### Line fields (Lines)

In the **Lines** area, you enter one line per operation to be reworked. Mandatory fields are marked and are checked when the dialog is closed.

| Field | Explanation |
|---|---|
| **Origin Line No.** | Display only. Refers to the original campaign line from which the rework quantity originates. |
| **Item No.** | Display only. Affected item of the campaign line. |
| **Rework Defect Type Code** | Mandatory field. When you choose a defect type from the maintained rework types, the module automatically transfers the **Rework Process** stored in the defect type (To Junk or To Production) into the line and thereby controls which further fields become mandatory. |
| **Rework Defect Type Description** | Display only. Plain text for the selected defect type; calculated when the defect type is set. |
| **Rework Defect Reason Code** | Mandatory field. When you choose a defect reason from the maintained reasons, the operation is assigned to this reason; without a reason, the dialog cannot be closed. |
| **Rework Defect Reason Description** | Display only. Plain text for the selected defect reason; calculated when the reason is set. |
| **Rework Process** | Display only, derived from the defect type. Determines the entire further flow (see option values below). |
| **Rework Cause** | Indicates who or what triggered the rework. When you set the originator here, you document responsibility for reporting (see option values below). |
| **Production Rework Type** | Display only. When opened from the campaign, always **Item**. The underlying logic additionally knows **Component**; in this entry point it stays with the item reference, so that the rework acts on the production item. |
| **Junk Location Code** | Editable only for the process **To Junk** and then a mandatory field. When you choose a location enabled for junk, it is stored for the rework data; if the location changes, a previously selected bin is reset. |
| **Junk Bin Code** | Editable only for the process **To Junk**. If the selected junk location requires bins, this field becomes mandatory; only a bin enabled for junk on the selected location is allowed. |
| **Quantity** | Mandatory field. When you enter the quantity to be reworked, the module calculates the base quantity from it. The quantity must not be less than 0 and not greater than the remaining allowed maximum quantity of the line; otherwise an error appears. |
| **Quantity (Base)** | Base quantity of the operation. Editable only when the unit factor is greater than 1; otherwise it is calculated automatically from **Quantity**. |
| **Alternate Routing** | Editable only for the process **To Production**. When you specify a certified routing here, the newly created rework production order receives this routing instead of the routing data of the source order. For **To Junk**, the value is automatically cleared. |

Option values in the line area:

- **Rework Process** – **To Junk:** **No** new production order is created. The module reduces the connected campaign and production quantities and logs the operation; **Junk Location Code** (and, if applicable, **Junk Bin Code**) are mandatory, **Alternate Routing** is cleared. **To Production:** The module creates a new production order with the rework quantity; **Alternate Routing** can optionally be selected, the junk location fields are cleared.
- **Rework Cause** – **Internal:** The defect was caused internally. **Customer:** The originator is the customer. **Supplier:** The originator is the vendor. The value serves for reporting and the assignment of responsibility.
- **Production Rework Type** – **Item:** The rework relates to the production item itself (standard in this entry point). **Component:** A component-related case possible in the base logic; it is not set from the campaign.

#### Checks when closing the dialog

When closing with **OK**, the module checks each line in a fixed order and prevents closing until all entries are complete and plausible:

1. **Rework Defect Type Code** must be filled.
2. **Rework Defect Reason Code** must be filled.
3. **Item No.** must be present.
4. **Quantity** must be filled.
5. For the process **To Junk**, a **Junk Location Code** must be present.
6. If the junk location requires bins, the **Junk Bin Code** must additionally be filled.
7. If several lines work with the same assigned item ledger entry, their total quantity must not exceed the remaining quantity of the entry; otherwise the system requests that you delete the line and reassign the entry.

If you cancel the dialog, all temporary lines are discarded and no rework is posted.

## Update Campaign Lines (wizard)

The **Update Campaign Lines** wizard is not a separate menu entry but opens automatically during posting, when the rework quantity cannot be deducted from the marked campaign line alone.

### When the wizard appears

The module searches for additional campaign lines that belong to the same production order line and the same routing. If the same production quantity affects several campaign lines of the same operation and the remaining quantity is not sufficient for the rework, the reduction must be distributed manually across the affected lines. In this case the wizard opens. If no manual distribution is needed, it is skipped and the rework is posted directly.

### Flow in the wizard

The wizard guides you through the distribution in three steps. Navigation is done via **Back**, **Next**, and **Finish**.

1. **Introduction page** with the note that the quantity of associated campaigns must be lowered manually.
2. **Line view** with all affected campaign lines for distribution.
3. **Completion page:** With **Finish**, the values are saved and the rework is then posted directly.

### Fields in the line view

The line view shows the affected campaign lines in a dense table. Only the **New Quantity** column is editable; all other columns serve for control. The two total fields above the table control the completion:

| Field | Explanation |
|---|---|
| **Needed Quantity to Lower** | Display only. Target sum by which all affected lines together must be reduced. The wizard can only be finished when this value is reached exactly. |
| **Lowered Quantity** (header) | Display only. Sums the reductions already entered across all affected lines. The value is evaluated by color: matching when it exactly matches the needed quantity, deviating when under- or over-covered. |
| **New Quantity** | The only editable column. When you enter the future remaining quantity of a line here, the module calculates the associated **Lowered Quantity** and updates the total sum. The value must not be less than 0 and not greater than the previous campaign quantity; otherwise an error appears. |
| **Lowered Quantity** (line) | Display only. Automatically calculated reduction of the individual line (previous campaign quantity minus **New Quantity**). |
| **Campaign No.** | Display only. Affected campaign. |
| **Prod. Order Status**, **Prod. Order No.**, **Prod. Order Line No.** | Display only. Linked production order with status and line. |
| **Routing / operation reference** | Display only. Shows the assigned routing and operation of the line, so that the distribution can be assigned to the correct operation. |
| **Item No.**, **Item Description** | Display only. Item and description of the line. |
| **Campaign Quantity** and **Production Order Quantity** | Display only. Previous quantity of the campaign line as well as the total quantity of the associated production order as a comparison base. |
| **Further control columns** (Type, No., Description, Work Center, Starting Date/Time, Setup Time, Run Time, Wait Time, Move Time) | Display only. Key figures taken from the campaign line for orientation during distribution. |

Completion is only possible when the sum of all **Lowered Quantities** matches the **Needed Quantity to Lower** exactly. If the sum is too small or too large, the system shows a message and does not complete the operation.

## Effect of posting

After closing the dialog or finishing the wizard, the module posts the rework directly. The effect depends on the **Rework Process**.

### Rework to production

For the process **To Production**, the module performs the following steps:

1. The original campaign line and the linked production order line are read.
2. If necessary, additional campaign lines are manually reduced via the **Update Campaign Lines** wizard.
3. A new **Production Order** is created with the rework quantity and the **Production Status** stored in **Manufacturing Setup**.
4. The new production order line receives the same base data as the original line; the finished quantity is set to 0.
5. If an **Alternate Routing** is specified, its routing is used for the new order and built up from the certified routing lines. Otherwise the routing data from the existing production order is taken over.
6. The quantities of the affected campaign lines and of the original production order line are reduced by the rework quantity.
7. The original campaign line is additionally marked as **Reworked**.

### Rework to junk

For the process **To Junk**, **no** new production order is created. The module reduces the connected campaign and production quantities and logs the operation via the rework logic. As announced in the dialog note, when entering from the production campaign there is **no** automatic transfer of the material to a junk location. The junk location is needed for the completeness of the rework data; the actual effect consists of the quantity reduction and the logging.

### Automatic quantity adjustment

After successful posting, the extension adjusts the quantities systematically:

| Step | Explanation |
|---|---|
| Manually reduced secondary lines | Lines from the wizard are set to their **New Quantity**. If this results in a quantity of 0 or less, the line is deleted. |
| Further lines of the same campaign | Affected related campaign lines are reduced by the rework quantity; at a quantity of 0 or less, the line is deleted. |
| Original campaign line | Is reduced by the rework quantity and marked with the **Reworked** indicator; at a quantity of 0 or less, the line is deleted. |
| Production order line | Its base quantity is reduced by the rework quantity. |
| Linked campaign lines of the production order | Receive the updated production order quantity as the new reference quantity. |

## History and tracking

The extension has **no history list of its own** and no separate report. The tracking of a rework operation is done via the existing places:

| Area | Explanation |
|---|---|
| **Production Campaign** | The header indicator **Rework** shows that at least one rework operation has been connected with the campaign; the reduced quantities and the line indicator **Reworked** document the affected lines. |
| **Rework document of the base logic** | On posting, the module stores the connection between the rework operation and the production campaign (connection type and connection no. = campaign no.). Through this, the rework logic recognizes the campaign-related origin. |
| **Production Order** | For rework **To Production**, the newly created production order represents the rework quantity and can be traced via the assigned origin. |

## Typical use cases

The following scenarios show the flow based on realistic triggers. All screens and actions are substantiated in the code of the extension.

### Rework due to an internal production defect

**Trigger:** In ongoing production, an employee reports a quality problem on an item; the affected quantity is to run through production again.

**Entry in BC:** Production control opens the **Production Campaign** page, jumps into the affected campaign, and switches to the lines.

**Core flow:** The user marks the affected campaign line and chooses **Rework**. In the **Rework Dialog** they set **Rework Defect Type Code** (with process **To Production**) and **Rework Defect Reason Code**, leave the **Rework Process** at **To Production**, enter the **Quantity**, and specify an **Alternate Routing** if needed. As **Rework Cause** they select **Internal**. When closing with **OK**, the module checks the mandatory fields. If the same production quantity is split across several campaigns, **Update Campaign Lines** opens; there the user enters the **New Quantity** for each line, until the **Lowered Quantity** matches the **Needed Quantity to Lower**, and chooses **Finish**.

**Completion:** The system creates a new **Production Order** for the rework quantity, reduces the original campaign and production quantity, and marks the source line as **Reworked**. The campaign's header indicator **Rework** is now set.

### Posting scrap in a production campaign

**Trigger:** Part of the planned quantity is unusable and cannot be reworked; it is to be treated as scrap.

**Entry in BC:** The user opens the affected **Production Campaign** and selects the appropriate line in the lines.

**Core flow:** Via **Rework**, the **Rework Dialog** opens. The user chooses a **Rework Defect Type Code** whose stored **Rework Process** is **To Junk**, along with the defect reason. They fill in **Junk Location Code** and – for a location that requires bins – **Junk Bin Code** as well as the **Quantity**. The note when opening reminds that no automatic transfer to the junk location takes place from the campaign. If the operation affects several related campaign lines, the user distributes the reduction in the **Update Campaign Lines** wizard.

**Completion:** The module reduces the campaign and production quantities and logs the junk operation in the rework logic. No new production order is created, and no inventory receipt is posted in the junk location.

### Rework across several split campaign lines

**Trigger:** A production quantity was split across several campaigns or operations; the rework affects the common origin.

**Entry in BC:** Entry via **Production Campaign**, then switch to the lines and start **Rework**.

**Core flow:** In the **Rework Dialog**, the user enters the rework quantity. The module recognizes that the remaining quantity of the marked line is not sufficient and that additional campaign lines of the same production order must be lowered manually, and opens **Update Campaign Lines**. The user checks the campaign no., production order reference, operation, and previous campaign quantity for each line and enters the future remaining quantity in **New Quantity**.

**Completion:** Only when the **Lowered Quantity** matches the **Needed Quantity to Lower** exactly can the operation be finished with **Finish** and the rework be posted. Lines whose quantity thereby drops to 0 are deleted.

## FAQ and troubleshooting

### 1. Why can the Rework Dialog not be closed?

The dialog checks the mandatory fields strictly. Usually the **Rework Defect Type Code**, **Rework Defect Reason Code**, **Item No.**, or **Quantity** are missing; for the process **To Junk**, additionally the **Junk Location Code** or – for a location that requires bins – the **Junk Bin Code**. Complete the relevant line.

### 2. Why is the Alternate Routing field not editable?

The **Alternate Routing** is only enabled for the process **To Production**. For **To Junk**, the value is automatically cleared, because no production order and thus no routing is created.

### 3. Why is no inventory receipt created in the junk location for junk?

The dialog explicitly points this out when opening: when entering from the production campaign, the junk process performs **no** automatic transfer to a junk location. Instead, the module reduces production and campaign quantities and logs the operation in the rework logic. The **Junk Location Code** is only needed for the completeness of the rework data.

### 4. Why does the Update Campaign Lines wizard not always appear?

The wizard opens only when the same production order quantity is split across several campaign lines or operations and the rework quantity cannot be deducted from the marked line alone. If no manual distribution is needed, the rework is posted directly.

### 5. Why can I not simply enter an arbitrary New Quantity in the wizard?

The **New Quantity** must not be less than 0 and not greater than the previous campaign quantity of the line. In addition, the sum of all **Lowered Quantities** must match the **Needed Quantity to Lower** exactly. Only then can **Finish** be run.

### 6. Why does the system report that the lowered quantity is not correct?

When finishing, the module compares the sum of the lowered quantities with the needed quantity to lower. If the sum deviates (under- or over-coverage), a message appears with both values, and the operation is not completed. Adjust the **New Quantity** in the affected lines until the header display **Lowered Quantity** is evaluated as matching.

### 7. Why was a campaign line deleted after posting?

If the remaining campaign quantity of a line drops to 0 or below due to the rework, the module automatically deletes this line. This applies to both the source line and related lines of the same production structure.

### 8. Why can I not rework a larger quantity than displayed?

The **Quantity** per line is limited to the remaining allowed maximum quantity, which is derived from the campaign line. In addition, when closing, the module checks whether the total quantity of all lines with the same assigned item ledger entry does not exceed its remaining quantity. If it does, delete the relevant line and reassign the entry to obtain the available quantity.

### 9. Why can no rework line be created when saving?

When saving, the module assigns a document number from the appropriate number series and reads the production status from **Manufacturing Setup**. If the **Production Status**, the **To Junk Nos.** (for junk), or the **To Production Nos.** (for production) are missing, the operation aborts with an error message. Add the missing values in Manufacturing Setup.

### 10. How do I recognize that a campaign has already been reworked?

The header field **Rework** of the production campaign is set as soon as at least one rework operation with a campaign reference has been posted. At line level, the affected line is marked with **Reworked** and reduced in its quantity.
