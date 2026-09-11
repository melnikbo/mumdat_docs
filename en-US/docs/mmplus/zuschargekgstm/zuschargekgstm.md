---
title: Anwenderhandbuch m+m Unit Conversion with Additional Lot Information
---

# User Guide m+m Unit Conversion with Additional Lot Information

## Introduction

The app **m+m Unit Conversion with Additional Lot Information** bridges the two modules
**m+m Unit Conversion** and **m+m Additional Lot Information**. It ensures that, during the
**Phys. Inventory Recording**, the additional lot information of an existing lot is automatically transferred to a newly
created lot. As a result, origin and supplementary details (for example, source lot, manufacturer,
inbound date) are preserved when a new lot is created during the inventory recording for quantity-related reasons.

The app itself does not add any pages of its own. Its value materializes at two places provided by the dependent
modules:

- In the **Lot Info. Transfer Setup**, the new **Process** value **Phys. Inventory Recording** becomes available for
  selection. There, the administrator defines **which** fields are transferred from the old lot to the new lot for this
  process.
- In the **Phys. Inventory Recording**, when the action **Cancel and Create Lot** is run, the app transfers the
  configured fields together with the origin details (**Original Item No.**, **Original Variant
  Code**, **Original Lot No.**) to the new **Lot No. Information Card**.

**Target audience.** This guide is primarily aimed at **operational warehouse users** who perform the
**Phys. Inventory Recording** and, in doing so, record, cancel, and create lots. It is secondarily addressed to
**administrators and key users** who configure the **Lot Info. Transfer Setup** once before
first use.

**Prerequisites.** Using this app in the "Microsoft Dynamics 365 Business Central" web client does not require any
separate setup of the app itself. In Extension Management, the app
**m+m Unit Conversion with Additional Lot Information** as well as its base modules **m+m Unit Conversion** and
**m+m Additional Lot Information** must be installed. So that new lots can automatically receive a **Lot No.**,
the item must be assigned a **No. Series** for lots.

**Process overview.** The workflow consists of three steps: The administrator sets up the process
**Phys. Inventory Recording** in the **Lot Info. Transfer Setup**. The user performs the
**Phys. Inventory Recording** and, when required, runs the action **Cancel and Create Lot**.
The user then verifies the result on the **Lot No. Information Card** of the new lot.

## Quick Start for Users

The fastest path from setup to result. The setup is a prerequisite and therefore comes at the
beginning.

1. **Setup (one-time, administrator).** Open the
   **Lot Info. Transfer Setup** via **Search**. Create one or more lines, select the value
   **Phys. Inventory Recording** in the **Process** field, and select in the **Field No.** field the lot fields that
   are to be transferred (for example, a description or a certificate detail). For details, see
   **Setup**.
2. **Open Phys. Inventory Recording.** Open the **Phys. Inventory Recording** via **Search** and select the
   recording line of the affected lot.
3. **Create a new lot.** In the ribbon under **Functions**, choose the action **Cancel and Create
   Lot**. Business Central creates a new **Lot No.** from the item's **No. Series**, transfers
   the configured fields from the old lot to the new lot, and additionally sets the origin fields
   (**Original Item No.**, **Original Variant Code**, **Original Lot No.**).
4. **Verify the result.** The new recording line contains the new **Lot No.** and, in the **Copied From
   Lot No.** field, the source lot; the old line is flagged as **Canceled**. Open the
   **Lot No. Information Card** of the new lot and verify the transferred fields and origin details.
5. **Correction (optional).** If the new lot was created by mistake, choose **Functions → Undo
   Cancel**. The new lot is removed and the original line is reactivated.

## Setup

The central and only setup of this app is performed in the **Lot Info. Transfer Setup**.
This page belongs to the base module **m+m Additional Lot Information**; the present app supplements it with the process
**Phys. Inventory Recording**. Here, the administrator defines which lot fields are transferred from an
existing lot to a newly created lot for a given process.

### Set up field transfer for the Phys. Inventory Recording

**Who and when.** This setup is performed by the **administrator** or a **key user** once before first
use. It controls which details are automatically carried over during daily work in the **Phys. Inventory Recording**
(see **Daily Work on the Phys. Inventory Recording**).

**Entry point:** Open the **Lot Info. Transfer Setup** via **Search**. The page is a
list page and is not opened via a superordinate card or list.

The page contains the following fields per line:

| Field | Explanation |
|---|---|
| **Process** | Defines the business transaction for which the field transfer applies. If you select **Phys. Inventory Recording**, the line takes effect for the action **Cancel and Create Lot** in the Phys. Inventory Recording; if you select **Production Order**, the line takes effect when posting an output entry of a production order (a process of the base module). Exactly one line is possible per process and field. |
| **Field No.** | Defines which field of the **Lot No. Information** is transferred. If you select a field via the drill-down, this field is copied from the source lot to the target lot when the new lot is created; without a line for this field, the field remains empty on the new lot. The normal (non-system) fields of the Lot No. Information can be selected. |
| **Field Name** | Displays the technical field name for the selected field. The field is filled automatically and serves for unambiguous assignment; no entry is required. |
| **Field Caption** | Displays the caption of the selected field as the user sees it on the **Lot No. Information Card**. The field is filled automatically and makes it easier to find the configured fields again. |

**Process — meaning per value (complete):**

- **Production Order:** The line applies to lot propagation in the production order (handover of the
  source lot to the finished product). This value is used by the base module and is listed here only for the
  sake of completeness.
- **Phys. Inventory Recording:** The line applies to the Phys. Inventory Recording. When a user runs the action
  **Cancel and Create Lot** there, exactly the fields configured for this process are transferred to
  the new lot. This value is added by the present app.

**Setup sequence (in order of dependency):**

1. **First**, open the **Lot Info. Transfer Setup** via **Search**.
2. **Then**, create one line per field to be transferred and set the value
   **Phys. Inventory Recording** in the **Process** field.
3. **Then**, in the **Field No.** field, select the desired field of the **Lot No. Information**
   via the drill-down. Repeat this for every field that is to be carried over.
4. **Finally**, make sure the affected item is assigned a **No. Series** for lots so that the new **Lot No.**
   can be assigned automatically. The configured field transfer is then triggered in daily operation by the action
   **Cancel and Create Lot** (see
   **Daily Work on the Phys. Inventory Recording**).

☞ If you do not create a line for a field, that field is **not** copied from the
source lot when the new lot is created. The origin fields (**Original Item No.**, **Original Variant Code**,
**Original Lot No.**), on the other hand, are **always** set, regardless of the setup (see
**Master Data: Lot No. Information Card**).

## Master Data: Lot No. Information Card

The **Lot No. Information Card** is the central master card of a lot. This app does not maintain any master data of
its own, but it writes the origin and supplementary details it takes over from the source lot onto the card of the
**newly created** lot. The user reads these values from the card.

**Who and when.** The values are created **automatically** at the moment of the action **Cancel and Create Lot**
in the **Phys. Inventory Recording**. Manual maintenance is not required for the origin fields; they are
not editable on the card.

**Where visible.** Open the **Lot No. Information Card** of the new lot (from the item's lot tracking
or from the Lot No. Information). There, among other things, you will find the following fields that this app
populates:

| Field | Explanation |
|---|---|
| **Original Item No.** | When a new lot is created via **Cancel and Create Lot**, the item no. of the source lot is entered here; this makes it traceable which item the lot originated from. The field is not editable. |
| **Original Variant Code** | If the source lot has a variant code, it is transferred to the new lot; this preserves the variant assignment. |
| **Original Lot No.** | When a new lot is created, the **Lot No.** of the source lot (origin lot) is entered here; the origin of the lot is thus documented seamlessly. |
| **Inbound Date** | If the inbound date of the source lot is maintained, it is transferred to the new lot; this preserves the temporal classification of the stock. |
| **Bundle** | If the source lot is flagged as **Bundle**, this flag is transferred to the new lot; the new lot is thereby treated the same as the source lot. |
| **Manufacturer Code** | The manufacturer code of the source lot is transferred to the new lot; the manufacturer assignment is preserved. |
| **Country/Reg. Of Orig. Code** | The country or region of origin of the source lot is transferred to the new lot; the origin detail remains available for evidence. |
| **Purchase Document No.** | If the source lot is assigned to a purchase document, the purchase document no. is transferred to the new lot; the reference to the goods receipt is retained. |
| **Purchased from Vendor No.** | The purchasing vendor of the source lot is transferred to the new lot; the vendor assignment is preserved. |
| **Vendor Lot No.** | The vendor lot no. of the source lot is transferred to the new lot; the external lot reference remains traceable. |
| **Vendor Internal Lot No.** | The vendor's internal lot no. is transferred to the new lot; this external reference is also preserved. |

☞ In addition to these permanently transferred fields, **all** fields you have configured in the
**Lot Info. Transfer Setup** for the process **Phys. Inventory Recording** are transferred.

## Daily Work on the Phys. Inventory Recording

In the **Phys. Inventory Recording**, users record the actually available stock. If a counted
quantity of a lot cannot be posted consistently, the affected lot is canceled and a new
lot is created. It is precisely at this moment that this app's field transfer takes effect (for the setup, see
**Set up field transfer for the Phys. Inventory Recording**).

**Entry point:** Open the **Phys. Inventory Recording** via **Search** and select the recording line. The
actions of this function are located in the ribbon in the **Functions** group.

The following actions are available on the recording lines:

| Action | Explanation |
|---|---|
| **Create Lot No.** | When you choose this action, an additional recording line is created with a new **Lot No.** drawn from the item's **No. Series**. This is an empty new lot; **no** fields are taken over from an existing lot. |
| **Cancel and Create Lot** | When you choose this action for the marked lines, a new **Lot No.** is generated per line, the configured fields as well as the origin fields are transferred from the previous lot to the new lot, the new line receives the source lot in the **Copied From Lot No.** field, and the previous line is flagged as **Canceled** with quantity 0. This action triggers the field transfer of this app. |
| **Undo Cancel** | When you choose this action for canceled lines, the previously created new lot is removed again and the original line is reactivated (the **Canceled** flag is reset). This is how you correct a new lot created by mistake. |

**Sequence when creating a new lot (order derived from the code):**

1. You select the recording line in the **Phys. Inventory Recording**.
2. You choose **Functions → Cancel and Create Lot**. The action can only be run if the item
   is not set to **Qty. Consistency** = *Always Change Quantity* (see the note below).
3. Business Central draws a new **Lot No.** from the item's **No. Series**.
4. The fields configured for the process **Phys. Inventory Recording** are transferred from the source lot to the new
   lot.
5. The origin fields (**Original Item No.**, **Original Variant Code**, **Original
   Lot No.**) as well as inbound date, bundle, manufacturer code, country/region of origin code, purchase details, vendor
   and vendor lot details are set on the new lot.
6. The new recording line carries the new **Lot No.** and **Copied From Lot No.**; the old line is
   **Canceled**. You verify the result on the **Lot No. Information Card** of the new lot.

☞ **Interlock Qty. Consistency:** If the item is set so that the quantity is always changed directly
(**Qty. Consistency** = *Always Change Quantity*), the action **Cancel and Create Lot** is disabled.
In this case, no new lot is created and no field transfer takes place.

## Typical Use Cases

### Use Case 1: Stock correction with a new lot during the inventory count

**Trigger.** During the inventory count, a warehouse employee determines that the counted quantity of a lot does not
match the expected stock and that the lot therefore cannot be posted unchanged.

**Entry point in BC.** The employee opens the **Phys. Inventory Recording** via **Search** and selects the
recording line of the affected lot.

**Core flow.**
1. The employee selects the recording line.
2. They choose **Functions → Cancel and Create Lot**.
3. Business Central assigns a new **Lot No.** from the item's **No. Series**.
4. The configured fields (process **Phys. Inventory Recording**) are transferred from the old lot to the new lot.
5. The origin fields **Original Item No.**, **Original Variant Code**, and **Original
   Lot No.** are set; the old line is marked as **Canceled**, the new line carries **Copied From
   Lot No.**

**Conclusion.** The employee opens the **Lot No. Information Card** of the new lot and confirms that the
origin and supplementary details were taken over correctly. The origin of the new lot is thereby documented
seamlessly.

### Use Case 2: Initial configuration by the administrator

**Trigger.** Before the first inventory count with this module, it is to be defined which lot details are
automatically carried over on a new creation.

**Entry point in BC.** The administrator opens the **Lot Info. Transfer Setup** via **Search**.

**Core flow.**
1. The administrator creates one line per field to be transferred.
2. In the **Process** field, they select **Phys. Inventory Recording**.
3. In the **Field No.** field, they select the relevant fields of the **Lot No. Information** via the drill-down;
   **Field Name** and **Field Caption** are displayed automatically.
4. They make sure the affected items are assigned a **No. Series** for lots.

**Conclusion.** From now on, at every action **Cancel and Create Lot** in the
**Phys. Inventory Recording**, the configured fields are transferred automatically. The setup is used in daily
operation by the users (see **Daily Work on the Phys. Inventory Recording**).

## FAQ and Troubleshooting

### Why are two processes available for selection in the Lot Info. Transfer Setup?
The **Process** field is an option field with the values **Production Order** and **Phys. Inventory Recording**. The
value **Production Order** comes from the base module and controls lot propagation in the production order; the
value **Phys. Inventory Recording** is added by this app and controls the field transfer in the inventory count. For
the present app, you set up lines with the process **Phys. Inventory Recording**.

### Why are not all fields taken over from the old lot for the new lot?
Only the fields for which a line with the process **Phys. Inventory Recording** exists in the
**Lot Info. Transfer Setup** are taken over. If a line for a field is missing, this field remains empty on the
new lot. Add the missing line in the setup.

### What happens if I have not created a line for a field in the setup?
The field in question is not copied from the source lot when the new lot is created. The
origin fields **Original Item No.**, **Original Variant Code**, and **Original Lot No.**
are, however, always set regardless of the setup.

### Why is the action "Cancel and Create Lot" grayed out?
The action is only active if the item is not set to **Qty. Consistency** = *Always Change Quantity*.
With this setting, the quantity is changed directly instead of creating a new lot; that is why the action is
disabled.

### Why do I not receive a Lot No. when creating the new lot?
A new **Lot No.** is drawn automatically from the **No. Series** for lots assigned to the item.
If this assignment is missing on the item, no new lot can be created. Assign the item a No. Series
for lots.

### How do "Create Lot No." and "Cancel and Create Lot" differ?
**Create Lot No.** creates an additional, empty recording line with a new **Lot No.**, without taking over fields from
an existing lot. **Cancel and Create Lot** cancels the previous line, creates a
new lot, and transfers the configured fields as well as the origin details from the old lot.

### How do I recognize which lot a new lot originated from?
On the recording line, the **Copied From Lot No.** field shows the source lot. On the
**Lot No. Information Card** of the new lot, the source lot is additionally shown in the **Original
Lot No.** field.

### Can I remove a new lot created by mistake?
Yes. In the **Phys. Inventory Recording**, select the canceled line and then **Functions → Undo
Cancel**. The new lot is removed and the original line is reactivated.

### Are the origin fields on the Lot No. Information Card populated automatically?
Yes. The fields **Original Item No.**, **Original Variant Code**, and **Original Lot No.**
are set automatically from the source lot when the new lot is created and are not
editable on the card.

### Do I have to set up this app separately?
Using this app in the "Microsoft Dynamics 365 Business Central" web client does not require any separate setup of the
app. It is sufficient that the app and its base modules are installed and that the desired fields for the process
**Phys. Inventory Recording** are stored in the
**Lot Info. Transfer Setup**.
