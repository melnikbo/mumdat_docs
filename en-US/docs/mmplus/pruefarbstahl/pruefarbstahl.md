---
title: Anwenderhandbuch m+m Test Certificate Mgt. Prod. Order Job Steel
---

# User Guide m+m Test Certificate Mgt. Prod. Order Job Steel

## Introduction

This extension connects the **Ext. Output Response** of the Prod. Order Job in the
steel environment with test certificate management (module **Test Certificate** /
**Test Certificate Setup**). It ensures that matching **Samples** are created in the
associated **Test Certificate** for the **Lots** and **Remaining Lots** of a material
recorded in the output response – either automatically when the lot is created or at
the push of a button by the user.

Functionally, the app closes the gap between two processes: in the **Ext. Output
Response** the user reports the lots that were produced from the **Material**; in
parallel, each relevant lot must be documented for quality. Without this app, the user
would have to create the sample manually in the **Test Certificate** and enter the
**Lot No.** by hand. With the app, the sample is created directly from the reported lot
line and populated with its **Lot No.**

**Target audience.** The primary target audience is **operational users** in production
and quality assurance who work daily with the Prod. Order Job and the **Ext. Output
Response**: they report lots back and document them via samples. The secondary target
audience is **administrators/key users** who perform the one-time **Test Certificate
Setup** (in particular the **Ext. Output Create Sample** toggle).

**Short process overview.**
1. In the **Test Certificate Setup**, the administrator maintains the fundamentals of
   test certificate management (number series, automatic sample creation) and, in the
   **Ext. Output Response** area, activates the **Ext. Output Create Sample** toggle.
2. Prerequisite in the document: the Prod. Order Job line carries a **Test Certificate
   No.** – only then does the relationship between output response and test certificate
   exist.
3. From the **Prod. Order Job**, the user opens the **Ext. Output Response** and reports
   the **Material** and the resulting **Lots** or **Remaining Lots**.
4. A **Sample** is created for a lot line – automatically (when the toggle is active) or
   via the actions **Create Lot Sample** or **Create Remaining Lot Sample**.
5. The user reviews the samples and releases them on the **Test Certificate Card**
   (**Release**); this completion takes place in the base module **Test Certificate**.

## Quick start for users

The quick start describes the shortest path from an empty setup to the first documented
lot. **First** the setup, **then** the daily work.

**A – Setup (one-time, by the administrator)**

1. Open **Test Certificate Setup** (via **Search** → "Test Certificate Setup").
2. Make sure the **Test Certificate Nos.** number series is maintained and that the
   **Automatic Sample Creation** toggle defines the desired degree of automation.
3. In the **Ext. Output Response** area, set the **Ext. Output Create Sample** toggle if
   samples are to be created from reported lots without user intervention.
4. Verify that the relevant Prod. Order Job line carries a **Test Certificate No.** (set
   via the base module between Prod. Order Job and Test Certificate).

**B – Daily work (by the operational user)**

5. Open the **Prod. Order Job** and select the relevant line.
6. Use the **Ext. Output Response** action to open the output response page for the
   **Material**.
7. In the **Lots** subarea, select the reported lot line (**Lot No.** must be set).
8. In the **Test Certificate** action group, choose the **Create Lot Sample** action –
   the app creates the **Sample** in the linked **Test Certificate** and fills its
   **Lot No.** When the **Ext. Output Create Sample** toggle is active, this step is not
   needed; the sample is created automatically.
9. The resulting samples appear in the info boxes **Output Lot Samples** or **Remaining
   Lot Samples** and on the **Test Certificate Card** under **Samples**; there the user
   fills them in and releases them via **Release**.

## Setup

The central setup page of this extension is the **Test Certificate Setup**. The app
extends this page (without creating its own setup page) with the **Ext. Output
Response** area containing the **Ext. Output Create Sample** toggle. Because in Business
Central the user sees **one** coherent page, this chapter documents the entire **Test
Certificate Setup** – base fields and the additional field of this app together.

**Access:** **Search** → "Test Certificate Setup". The **Test Certificate Setup** is a
company-wide setup (one record per company); no higher-level master document exists, so
access via **Search** is correct.

**Who sets it up and when.** The **Test Certificate Setup** is performed once before the
first productive use by an administrator or key user of quality assurance and adjusted
afterwards only when processes change. The toggle decisive for this app, **Ext. Output
Create Sample**, directly controls whether samples are created automatically during the
**daily work** (chapter *Daily work at the Prod. Order Job*).

### Test Certificate Setup – "Ext. Output Response" area (this app)

This area is added by the present extension.

| Setup | Explanation |
|-------------|-------------|
| **Ext. Output Create Sample** | When activated, the system automatically creates a **Sample** in the associated **Test Certificate** when a lot or remaining lot line is created or changed in the **Ext. Output Response**, and adopts the **Lot No.** of the line. The user then no longer has to trigger the **Create Lot Sample** / **Create Remaining Lot Sample** actions manually. If the toggle is not set, samples are created only on an explicit click by the user. Prerequisite in both cases: the Prod. Order Job line carries a **Test Certificate No.** and the lot line carries a **Lot No.** |

### Test Certificate Setup – base areas

The following areas belong to test certificate management and appear on the same page.
They are documented here as well so that the user can set up the entire page without an
additional manual. For the present app, the fields **Automatic Sample Creation** and
**Test Certificate Nos.** are especially relevant.

**"General" area**

| Setup | Explanation |
|-------------|-------------|
| **Automatic Sample Creation** | When activated, the system already creates samples in the quantity specified by the template when a **Test Certificate** is created; the user does not have to create the samples individually. This base setting works together with **Ext. Output Create Sample**: if the latter is set, the automatically created samples are additionally filled with the **Lot No.** from the output response. |
| **Certificate Can Be Re-Opened Only by QA User** | When activated, only users flagged as quality assurance may re-open an already completed **Test Certificate**; other users then cannot undo the completion. |
| **Ignore Rule When Creating Test Certificate Manually** | When activated, the system skips the automatic rule population as soon as a test certificate is created manually (from operation or component); the user then receives an empty test certificate instead of a rule-based, pre-filled one. |
| **Warn Before Changing Production Order Status** | When activated, the system warns before a status change of the production order if test certificates with a test status other than "Passed" are still open; the user can thus react before advancing. |
| **Caption Default Value 1** | Defines the freely selectable label of the first default value column; the entered label then appears in test certificates and in the test certificate report. |
| **Caption Default Value 2** | Defines the label of the second default value column; acts analogously to Default Value 1 on test certificates and printout. |
| **Block Lot No.** | When activated, the system automatically blocks a newly created **Lot No.** until the associated test certificate delivers a positive result; unchecked lots can thus not be reused untested. |
| **Transfer Sample Values from Vendor Lot Template** | When activated, the system adopts existing sample values from the vendor lot template into the new sample; the user is spared re-entering already known values. |

**"Quarantine Setup" area**

| Setup | Explanation |
|-------------|-------------|
| **Quarantine Location** | Defines the location to which items are transferred when quarantine is triggered; without an entry no quarantine posting can occur. |
| **Quarantine Bin Code** | Determines the bin within the quarantine location to which quarantined items are posted. |

**"Posting" area**

| Setup | Explanation |
|-------------|-------------|
| **Automatically Post Item to Quarantine** | When activated, the system opens the transfer journal with a proposed line that the user can post directly when "move item to quarantine" is triggered. |
| **Ask Before Post to Quarantine** | When activated, the system prompts the user before moving to quarantine; without the toggle, posting occurs without a query. |
| **Block Posting Quarantine Lines** | When activated, the system blocks the generated quarantine posting lines against further changes. |
| **Enable Quarantine Warning Before Validating Sample Value** | When activated, the system notifies the user that the test status of the origin line changes to "Quarantine" before the default value is validated. |

**"Warehouse" area**

| Setup | Explanation |
|-------------|-------------|
| **Quarantine Zone Code** | Defines the warehouse zone for quarantine stock in warehouses with directed put-away and pick. |
| **Quarantine Bin Type Code** | Determines the bin type for quarantine in directed put-away and pick. |
| **Quarantine Bin Type Receive** | Defines the bin type for goods receipt into quarantine. |
| **Quarantine Bin Type Ship** | Defines the bin type for goods shipment out of quarantine. |
| **Quarantine Bin Type Put Away** | Defines the bin type for put-away into quarantine. |
| **Quarantine Bin Type Pick** | Defines the bin type for picking out of quarantine. |

**"Numbering" area**

| Setup | Explanation |
|-------------|-------------|
| **Test Certificate Template Nos.** | Determines the number series for test certificate templates; without a series, no test certificate templates can be created consecutively. |
| **Test Certificate Nos.** | Determines the number series for **Test Certificates**. It must be set so that a test certificate with a **Test Certificate No.** can be created – and so that the samples created from the output response can be assigned to a test certificate at all. |
| **Test Certificate Sample Nos.** | Determines the number series for the individual **Samples** within a test certificate. |
| **Test Certificate Rule Nos.** | Determines the number series for test certificate rules. |

**"Report" area**

| Setup | Explanation |
|-------------|-------------|
| **Test Certificate Report Nos.** | Determines the number series for test certificate report documents. |
| **Logo Position on Documents** | Defines at which position the logo appears on the test certificate report. |
| **Picture Reference Symbol** | Defines a symbol (up to 5 characters) that indicates in the report that pictures are stored for a sample value; the default value is "*". |
| **Automatically Create Test Certificate Report Document** | When activated, the system creates the test certificate report document automatically as soon as the prerequisites are met. |

**"Job Queue" area**

| Setup | Explanation |
|-------------|-------------|
| **Restart Job Queue On Error** | When activated, the system automatically restarts the associated job queue after an error. |
| **Restart Job Queue After No. Of Minutes** | Defines the wait time until the restart in minutes (e.g. 60 = one hour; 1440 = one day). |

### Setting up automatic sample creation from the Ext. Output Response

This extension provides exactly one capability that brings several pages together: the
**automatic creation of samples** from reported lots. The administrator sets it up in
the order given below; the benefit arises in the **daily work** (chapter *Daily work at
the Prod. Order Job*).

**Process intro.** The capability is configured by the administrator/key user of quality
assurance, once before the first output response. It takes effect as soon as the
operational user reports lots back in the **Ext. Output Response**.

**Access:** **Search** → "Test Certificate Setup".

**Setup steps in dependency order:**

1. **Ensure a Test Certificate No. on the Prod. Order Job line (prerequisite).** If the
   Prod. Order Job line carries a **Test Certificate No.**, the relationship between
   output response and test certificate exists; without this number, no sample is
   created (processing aborts without a message). The **Test Certificate No.** is set
   via the base module between Prod. Order Job and Test Certificate.
2. **Maintain the Test Certificate Nos. number series.** If the **Test Certificate
   Nos.** number series is set in the **Test Certificate Setup**, a test certificate
   with a **Test Certificate No.** can be created at all, to which the samples are
   assigned; if it is missing, the assignment fails.
3. **Release automatic sample creation.** If the base toggle **Automatic Sample
   Creation** is activated, the system creates samples for the test certificate in the
   specified quantity; the lot assignment of this app builds on these samples.
4. **Activate Ext. Output Create Sample (this app).** If the **Ext. Output Create
   Sample** toggle is set in the **Ext. Output Response** area, the system creates the
   sample automatically when the lot or remaining lot line is created/changed and fills
   its **Lot No.** – the user no longer has to trigger any action.

**Operational conclusion.** In daily work, the samples are now created automatically
when the lots are reported. If the **Ext. Output Create Sample** toggle is deliberately
not set, the user triggers the creation manually via **Create Lot Sample** or **Create
Remaining Lot Sample** (see chapter *Daily work at the Prod. Order Job*). The samples
are then completed on the **Test Certificate Card** via **Release**.

## Daily work at the Prod. Order Job

The daily work takes place in the **Ext. Output Response** of the Prod. Order Job. This
output response page and its subareas belong to the steel base module; the present app
extends it with the **Test Certificate No.** column, with info boxes containing samples,
and with the **Test Certificate** action group.

**Controlling setup (bridge to the setup).** The behavior of this chapter is controlled
in the **Test Certificate Setup**: the **Ext. Output Create Sample** toggle decides
whether samples are created automatically upon output response; the **Test Certificate
Nos.** number series and **Automatic Sample Creation** determine whether and how the
test certificate together with its samples is created. For details, see chapter *Setup*
→ *Setting up automatic sample creation from the Ext. Output Response*.

**Access:** In the **Prod. Order Job**, open the relevant line and choose the **Ext.
Output Response** action. The output response page for the **Material** opens with the
subareas **Lots** and **Remaining Lots**.

### Ext. Output Response – "Test Certificate No." column

On the three output response areas (**Material**, **Lots**, **Remaining Lots**), the app
adds one read-only column each.

| Field | Explanation |
|------|-------------|
| **Test Certificate No.** | Shows which **Test Certificate** the line is assigned to via the Prod. Order Job line. The value is calculated from the **Test Certificate No.** of the associated Prod. Order Job line and is not editable. If a number is shown here, the relationship to the test certificate exists and samples can be created for the line; if the column is empty, the assignment is missing and the sample creation actions remain ineffective. |

### Ext. Output Response – "Test Certificate" action group

The app adds the **Test Certificate** action group with two actions to the material
output response area.

| Action | Effect |
|--------|---------|
| **Create Lot Sample** | Creates a **Sample** in the linked **Test Certificate** for the lot line currently selected in the **Lots** subarea and fills its **Lot No.** with the **Lot No.** of the line. Prerequisite: the lot line carries a **Lot No.** and the Prod. Order Job line carries a **Test Certificate No.**; otherwise nothing happens. |
| **Create Remaining Lot Sample** | Creates a **Sample** in the linked **Test Certificate** for the remaining lot line currently selected in the **Remaining Lots** subarea and fills its **Lot No.** with the **Lot No.** of the remaining lot line. Prerequisites as for **Create Lot Sample**. |

**Procedure.** Use the **Ext. Output Response** action to open the output response page,
select the desired line in the **Lots** (or **Remaining Lots**) subarea, and choose the
appropriate action in the **Test Certificate** group. The app creates the sample and
stamps in the **Lot No.** You then review and document the sample on the **Test
Certificate Card** (invoked via the **Test Certificate No.** column or the base module
**Test Certificate**) and release it via **Release**.

### Ext. Output Response – info boxes

The app shows three info boxes with the existing samples on the material output response
area. They serve to check whether samples already exist for a lot.

| Info box | Explanation |
|---------|-------------|
| **All Material Lot Samples** | Shows all samples for the **Lot No.** of the current material – independent of a specific test certificate. This lets the user recognize whether samples for this lot were already created elsewhere. |
| **Output Lot Samples** | Shows the samples that belong to the **Lot No.** of the selected lot line and to the assigned **Test Certificate**. Updates as soon as a sample is created via **Create Lot Sample** or automatically. |
| **Remaining Lot Samples** | Shows the samples that belong to the **Lot No.** of the selected remaining lot line and to the assigned **Test Certificate**. Updates analogously with **Create Remaining Lot Sample**. |

### Completing the test certificate (outlook into the base module)

Filling in the sample values, releasing the individual samples and the test certificate,
and printing or sending a test certificate report take place in the base module **Test
Certificate** (Test Certificate Card, **Samples**, **Release**). This extension creates
and links the samples; further processing uses the functions there. To do this, open the
**Test Certificate Card** via the calculated **Test Certificate No.** or by searching for
the test certificate.

## FAQ and troubleshooting

### 1. Why is no sample created when I report a lot?
Samples are created automatically only if the **Ext. Output Create Sample** toggle is set
in the **Ext. Output Response** area of the **Test Certificate Setup**. Without the
toggle, you must trigger the **Create Lot Sample** action manually.

### 2. Why does nothing happen when I choose "Create Lot Sample"?
The action aborts without a message if the lot line has no **Lot No.** or the associated
Prod. Order Job line carries no **Test Certificate No.** Check these two values first.

### 3. Why is the "Test Certificate No." column in the output response empty?
The **Test Certificate No.** is calculated from the **Test Certificate No.** of the Prod.
Order Job line. If no test certificate is assigned to the line, the column remains empty
and no samples can be created.

### 4. Can I change the "Test Certificate No." in the output response?
No. The column is read-only because it is a value calculated from the Prod. Order Job
line. You change the assignment via the Test Certificate No. of the line in the base
module.

### 5. What is the difference between "Create Lot Sample" and "Create Remaining Lot Sample"?
**Create Lot Sample** creates a sample for the selected line in the **Lots** subarea,
**Create Remaining Lot Sample** for the selected line in the **Remaining Lots** subarea
(remaining lot = leftover remaining quantity of a lot).

### 6. What number does the new sample get?
The sample is assigned to the **Test Certificate** that is determined via the **Test
Certificate No.** of the line; the sample number comes from the sample number series
maintained in the **Test Certificate Setup**. The **Lot No.** of the output response line
is adopted into the sample.

### 7. Why are several samples created instead of one?
The app calls the standard sample creation of the test certificate. How many samples are
created is determined by the test certificate template or the **Automatic Sample
Creation** setting. The app then fills the most recently created sample with the **Lot
No.**

### 8. Must the test certificate already exist before I report back?
The Prod. Order Job line must carry a **Test Certificate No.** The actual test
certificate and its samples are created when the action is triggered or during automatic
creation via the standard function of the test certificate.

### 9. I don't see the new sample immediately – why is that?
The samples appear in the info boxes **Output Lot Samples** / **Remaining Lot Samples**
and on the **Test Certificate Card** under **Samples**. Check whether you have selected
the correct lot line, since the info boxes filter by **Lot No.** and **Test
Certificate**.

### 10. Where do I release the sample and print the test certificate report?
Releasing the samples and the test certificate (**Release**) and printing/sending the
test certificate report take place on the **Test Certificate Card** of the base module
**Test Certificate**. This extension only creates the samples and links them to the lot.

## Typical use cases

### Use case 1 – Documenting a lot after the output response (manual)

**Trigger.** A production employee has produced a steel lot and reported it back in the
Prod. Order Job; quality assurance is to document the lot.

**Access in BC.** The user opens the **Prod. Order Job**, selects the line, and chooses
the **Ext. Output Response** action. The output response page for the **Material** opens
with the subareas **Lots** and **Remaining Lots**.

**Core procedure.**
1. In the **Lots** subarea, select the reported line with a set **Lot No.**
2. In the **Test Certificate** action group, choose the **Create Lot Sample** action.
3. The app creates a **Sample** in the **Test Certificate** determined via **Test
   Certificate No.** and adopts the **Lot No.**
4. The new sample appears in the **Output Lot Samples** info box.

**Conclusion.** The user opens the **Test Certificate Card**, fills in the sample values,
and releases the sample and the test certificate via **Release**. Printing or sending the
test certificate report takes place in the base module **Test Certificate**.

### Use case 2 – End-to-end automatic sample creation

**Trigger.** Quality assurance wants a sample to be created for every reported lot
without an additional click.

**Access in BC.** One-time setup via **Search** → "Test Certificate Setup".

**Core procedure.**
1. In the **Test Certificate Setup**, ensure the **Test Certificate Nos.** number series
   and **Automatic Sample Creation**.
2. In the **Ext. Output Response** area, set the **Ext. Output Create Sample** toggle.
3. From now on, the system automatically creates a **Sample** when a lot or remaining lot
   line is created or changed in the **Ext. Output Response** and fills the **Lot No.** –
   without triggering the actions manually.
4. The operational user reports back as usual in the **Prod. Order Job** via **Ext.
   Output Response**; the samples appear automatically in **Output Lot Samples** or
   **Remaining Lot Samples**.

**Conclusion.** The automatically created samples are reviewed on the **Test Certificate
Card** and released via **Release**.
