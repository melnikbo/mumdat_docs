---
title: Anwenderhandbuch m+m Test Certificate Mgt. with Additional Lot Info.
---

# User Guide m+m Test Certificate Mgt. with Additional Lot Info.

## Introduction

The **m+m Test Certificate Mgt. with Additional Lot Info.** extension enhances the test certificate functionality of Business Central with additional lot information. It controls **on which lot level** a test certificate is created (test certificate, lot, vendor lot, or lot including source lot), automatically transfers sample values from a vendor lot template to identical samples, and consolidates characteristic values in the document into **minimum, maximum, and average values**. In addition, it defines a dedicated report layout per **standard**.

The extension builds on the modules **m+m Test Certificate Management**, **m+m Additional Lot Information**, and **m+m Cloud Base**. The core functions of the test certificate system (test certificates, samples, test templates, number series, quarantine) come from the base module and are documented there; this guide describes exclusively the fields, pages, and actions that **this** extension adds.

### Target audience

The primary audience is **operational quality assurance users** who record and release samples daily and who create, print, and email test certificates (documents). The secondary audience is **administrators and QA managers** who perform the setup (test certificate creation type, report layout per standard, test group / standard assignment).

### Brief process overview

The administrative path runs from the central **Test Certificate Setup** page (global default of the test certificate creation type and the leading lot), through the **Standard Test Group Assignment** (print value option per test group and standard), to the report assignment per **standard**. The operational path runs from the **sample** (recording the vendor lot information and optionally a template), through the **test certificate** (selecting the samples and consolidating the values), to the **output** via **Print Document** or **Send by Email**.

### Key terms

- **Lot / Lot No.** – the tracked lot of an item.
- **Vendor lot / Vendor Lot No.** – the lot number assigned by the vendor, which can serve as an independent grouping for test certificates.
- **Source lot** – the upstream lot from which the current lot originated.
- **Test certificate / Test Certificate No.** – the test data record for an object (base module).
- **Sample / sample value** – the individual measurement of a characteristic within a test certificate.
- **Test certificate document** – the printable document (page **Test Certificate Report**).
- **Standard** – the standard on which the test certificate is based; controls layout and print value option.
- **Test Certificate Creation Type** – determines the grouping level of the test certificate.

## Quick start for users

The quick start follows the technically enforced order: **first set up, then maintain master data, then work and output.**

**A. Setup (one-time, by administrator/QA):**

1. Open the **Test Certificate Setup** page via **Search**. In the **Certificate** group, set the default for the **Test Certificate Creation Type** and – only for **Vendor Lot Purely** – the **Leading Lot**. If required, enable **Transfer Sample Value from Templ. Vendor Lot No.**.
2. Open the **Standards** list and, per standard, enter **Report ID**, **Report Type**, and **Report Layout Name** (for the action, see the Setup chapter).
3. In the **Standards** list or in the **Test Groups** list, use the **Standard Test Group Assignment** action to open the page of the same name and set the **Print Value Option** per test group and standard.

**B. Master data (ongoing, by QA):**

4. In the **Samples** list or on the sample card, record the vendor lot information. Mark one representative sample per vendor lot with **Is Template Vendor Lot No.** = yes.

**C. Daily work and output (by QA):**

5. Open the **Test Certificate Report**. Check the **Test Certificate Creation Type** that was defaulted from the setup and select the **standard** (**Standard Code**); confirm the prompt *"Should the Lines be updated?"* with Yes.
6. Add the values: via **Select Sample Values** (standard path) or – for a lot- or vendor-lot-based test certificate creation type – via **Select Multiple Samples**.
7. On the **Value Summary** FastTab, check the consolidated values (min./max./average) per characteristic.
8. Output the document: **Print Document** or **Send by Email**.

## Setup

Setup is two-tiered: a global, company-wide setup on the **Test Certificate Setup** page defines defaults that are refined per standard or per test group. All of the following settings are revisited in the **Daily Work** chapter.

### Test Certificate Setup — Certificate group

**Entry point:** Open the **Test Certificate Setup** page via **Search**. It is a company-wide setup page (one record per company); there is no superordinate document.

**Who/when:** The administrator or a QA manager maintains this page **once before the first test certificate is created**. The values set here are adopted as defaults whenever a new **test certificate** is created (see the Daily Work chapter).

The extension adds the following fields to the base setup page (the remaining setup – number series, quarantine, email – belongs to the base module and is maintained there):

| Setup | Explanation |
|---|---|
| **Transfer Sample Value from Templ. Vendor Lot No.** | When enabled, upon releasing all samples the sample values of the sample marked as a template are automatically transferred to all open samples with **the same vendor lot**, and those samples are then released; QA thus records the values only once per vendor lot instead of once per sample. Without this flag, the automatic transfer stays off and each sample is recorded individually. |
| **Test Certificate Creation Type** | Defines the default grouping level for new test certificates. If a value is set here, every new **test certificate** adopts this value automatically, and the document lines as well as the output are grouped accordingly (see the value overview below). |
| **Leading Lot** | Defines which lot number is printed on the document as the leading lot. Only editable and effective when **Test Certificate Creation Type** = **Vendor Lot Purely**; otherwise the field is cleared automatically. When **Vendor Lot** is selected, the vendor lot no. appears on the document instead of the internal lot. |

**Values of the Test Certificate Creation Type** (each value determines how the test certificate lines are grouped and how they are summarized on the document):

- **Test Certificate Purely:** The test certificate refers to exactly **one test certificate** (Test Certificate No.); no cross-lot summarization takes place. This is also the enforced setting when the automatic test certificate creation in the base module is active.
- **Lot Purely:** The lines are grouped by **Lot No.**; the certificate summarizes all samples of the same lot. The **Select Multiple Samples** action is available.
- **Vendor Lot Purely:** The lines are grouped by **Vendor Lot No.**; the certificate summarizes all samples of the same vendor lot (even across several internal lots). The **Leading Lot** is effective only for this type. The **Select Multiple Samples** action is available.
- **Lot. incl. Source Lot:** The lines are grouped by the **source lot**; if no source lot exists, the current lot is used. This includes upstream lots in the certificate. The **Select Multiple Samples** action is available.

**Dependency (from the code):** If the automatic creation of the test certificate document is active in the base module, the system forces **Test Certificate Creation Type** to **Test Certificate Purely** and clears the **Leading Lot**. Manually selecting a different test certificate creation type while automatic creation is active is rejected. Conversely, the test certificate creation type can only be changed when automatic creation is disabled.

### Setting up sample value transfer per vendor lot

This process chain links the global setup, the master data maintenance of the samples, and the release in daily operation. It is aimed at the administrator/QA manager and is set up **before** the first release of samples sharing a common vendor lot.

1. **First**, enable the **Transfer Sample Value from Templ. Vendor Lot No.** flag in the **Test Certificate Setup**. When enabled, the automatic transfer is unlocked company-wide.
2. **Then**, in the master data (see the **Samples & lot information** chapter), the QA users maintain exactly **one** sample per vendor lot with **Is Template Vendor Lot No.** = yes. When set, this sample serves as the value template; the system allows only one template per vendor lot.
3. **Finally**, in daily operation the user triggers the release of all samples. If at least one template and at least one open sample with the same vendor lot are present, the system transfers the values and shows the prompt *"Do you want to transfer the Sample Values from the Vendor Lot No. to all samples with the same Vendor Lot No.?"*. If the user confirms, the values are copied and the affected samples are released.

**Validation:** The **Is Template Vendor Lot No.** flag can only be set on a sample with the status *Open*; it requires a filled **Vendor Lot No.**. A second template record for the same vendor lot is rejected with the message *"… can only be set once."*.

The operational conclusion of this chain is described in the **Samples & lot information** chapter and in the use case *Sample value template per vendor lot*.

### Setting up reports and layout per standard

The extension links each **standard** with its own report and report layout. This assignment controls which report is used for **Print Document** and **Send by Email**. The administrator/QA manager is responsible; the setup is done **before** a test certificate for this standard is printed for the first time.

**Entry point:** Open the **Standards** list (standards of the test certificate system). The report fields are maintained there per standard line.

| Field | Explanation |
|---|---|
| **Report ID** | Defines which report is printed for this standard. If a value is set, the output uses exactly this report; when a new standard is created, the default test certificate report is defaulted. If the Report ID is reset to 0, the stored **Report Layout Name** is cleared. |
| **Report Name** | Shows the name of the report selected under **Report ID** (not editable). Serves to verify that the correct report definition is assigned. |
| **Report Type** | Defines which layout type is printed from. If a type is selected, the system checks whether a layout of this type exists for the report and otherwise rejects it with a message (e.g. *"Report '…' has no Word layout."*). For **Custom**, the layout selection opens. |
| **Report Layout Name** | Shows the selected layout (not editable). If **Custom** was selected, the layout confirmed from the layout list is shown here; for built-in layouts, **(Default)** is shown here. |

**Values of the Report Type** (OptionCaption **RDLC,Word,Custom,Excel,External**):

- **RDLC:** Uses the report's built-in RDLC layout; the layout selection is cleared. If no RDLC layout exists, the selection is rejected.
- **Word:** Uses the built-in Word layout; selection analogous to RDLC.
- **Custom:** Opens the **Report Layouts** list to select a specific layout; the name and the application ID of the layout are adopted. If nothing is selected, *"No report layout was selected."* appears.
- **Excel:** Uses an Excel layout; if none exists, it is rejected.
- **External:** Uses an external layout; if none exists, it is rejected.

Two further fields on this line are hidden from users and are summarized here: the technical **Report Layout App ID** (internal, not visible) and the **Custom Report Layout Code** (deprecated, automatically migrated to the new **Report Layout Name** during an upgrade). Neither requires manual maintenance.

### Setting up the Standard Test Group Assignment

The **Standard Test Group Assignment** defines, per combination of **test group** and **standard**, how the values of that test group are printed on the document (individually or consolidated). It is the prerequisite for the consolidated min./max./average values in the test certificate. The QA manager is responsible; the assignment is maintained as soon as new standards or test groups are in use.

**Entry point:** Open the **Standards** list and, in the standard's line, choose the **Standard Test Group Assignment** action (the page is prefiltered on the **Standard Code**). Alternatively, open the **Test Groups** list and choose the same **Standard Test Group Assignment** action there (prefiltered on the group code). Both paths open the same **Standard Test Group Assignment** page.

| Field | Explanation |
|---|---|
| **Group Code** | Refers to the test group for which the rule applies. When set, the **Group Name** is pulled in automatically; only values from the existing test groups are allowed. |
| **Group Name** | Shows the description of the test group (not editable); serves to uniquely identify the group. |
| **Standard Code** | Refers to the standard for which the rule applies. When set, the **Standard Description** is pulled in; only existing standards are allowed. |
| **Standard Description** | Shows the description of the standard (not editable). |
| **Print Value Option** | Defines how the values of this test group appear on the document under this standard (see values below). When an option other than **Standard** is selected, the system calculates additional key figures and displays them in the **Value Summary**. |

**Values of the Print Value Option:**

- **Standard:** The individual sample values are printed; no additional consolidation.
- **Min./Max. Value:** In addition, the smallest and the largest value per characteristic are calculated and printed.
- **Average Value:** In addition, the average per characteristic is calculated and printed.
- **Min./Max. Value and Average Value:** Minimum, maximum, and average value per characteristic are calculated and printed.

**Validation / dependency:** If a test group or a standard for which assignments still exist is deleted, the system prevents the deletion with the message *"The Table … has entries. Delete them before."*. For characteristics of the value type *Text* or *Media*, **Standard** is always used, since no key figures can be calculated for them.

## Master data

### Standard Test Group Assignment (master list)

The **Standard Test Group Assignment** page is at the same time the master list of the rules from the previous section. It shows per line **Group Code**, **Group Name**, **Standard Code**, **Standard Description**, and **Print Value Option** (for field meanings, see above). Through it, QA users get an overall view of which test groups are printed consolidated under which standards. The values flow directly into document creation: when the **Standard Code** is set in the test certificate, the lines are given the respective **Print Value Option** based on this assignment.

### Samples & lot information

The extension enhances the samples with vendor lot information. These entries control whether a sample serves as a value template and with which lot it appears on the document. The QA users are responsible; maintenance is ongoing during sample recording.

**Entry point:** Open the **Samples** list and, from it, the associated sample card. The following fields appear in the lot/sample area of the card; in the **Samples** list, **Vendor Lot No.** and **Is Template Vendor Lot No.** are additionally shown as columns.

| Field | Explanation |
|---|---|
| **Vendor Lot No.** | Shows the lot number assigned to the vendor for the sample (derived from the lot information, not editable). When filled, the sample can be used for a vendor-lot-purely summarization and is a prerequisite for marking it as a template. |
| **Is Template Vendor Lot No.** | When enabled, this sample serves as a **value template** for all open samples with the same vendor lot; upon releasing all samples, their values are adopted (see *Setting up sample value transfer per vendor lot*). Can be set only in the status *Open* and only with a filled Vendor Lot No.; only one template per vendor lot is allowed. |
| **Vendor Internal Lot No.** | Shows the vendor's internal lot number (derived from the lot information, not editable). Serves for traceability when the vendor and one's own system use different lot numbers. |
| **Original Lot No.** | Shows the upstream lot from which the current lot originated (derived from the lot information, not editable). Used with the **Lot. incl. Source Lot** test certificate creation type to group the document lines. |

**Sample value entry (base field of the test certificate):** The extension enhances the base field **sample value entry** with three additional methods that define from which existing sample missing values are automatically adopted when no matching sample is available:

- **Original Lot Same Certificate:** An already recorded sample **of the same test certificate** with the source lot is used.
- **Original Lot Same Template:** A sample for the source lot is used whose test certificate uses **the same test template and template version**.
- **Original Lot Overall (Last Sample):** The most recent existing sample for the source lot is used, regardless of test certificate or template.

In all three cases a **source lot** must be stored; if it is missing, the method does not apply.

## Daily work: creating a test certificate

The central document of this extension is the **test certificate**. This section assumes that the defaults described in the **Setup** chapter are maintained: the **Test Certificate Creation Type** and **Leading Lot** in the **Test Certificate Setup**, the report layout in the **Standards** list, and the **Print Value Option** in the **Standard Test Group Assignment**.

### Test certificate header

When a new test certificate is created, the system automatically adopts the **Test Certificate Creation Type** and the **Leading Lot** from the **Test Certificate Setup** into the document header. The extension adds the following fields to the header:

| Field | Explanation |
|---|---|
| **Test Certificate Creation Type** | Determines the grouping level for this document (Test Certificate Purely, Lot Purely, Vendor Lot Purely, Lot. incl. Source Lot; for meanings see the Setup chapter). When the value is changed, the system enables or disables the **Select Multiple Samples** action accordingly. For a value other than **Vendor Lot Purely**, the **Leading Lot** is cleared automatically. |
| **Leading Lot** | Determines which lot is printed on the document as the leading lot. Effective only for **Vendor Lot Purely**; when **Vendor Lot** is selected, the vendor lot no. appears on the document as the leading lot. |

### Selecting values

Two actions are available for filling the document lines:

- **Select Sample Values** (base action): Opens the sample value selection for the test certificate currently set in the header. This path is used for **Test Certificate Purely**.
- **Select Multiple Samples** (action of this extension): Active only when the **Test Certificate Creation Type** is **Lot Purely**, **Lot. incl. Source Lot**, or **Vendor Lot Purely**. Use the **Select Multiple Samples** action to open the appropriate selection list:
  - for **Lot Purely** and **Lot. incl. Source Lot**, the **Lot No. Information List** (for "incl. source lot", the chained source lots are additionally included),
  - for **Vendor Lot Purely**, the **Vendor Lot No. List**.

  After selection, the system adopts all samples (sample values) of the selected lot or vendor lot into the document lines and then recalculates the consolidated values.

**Setting the standard:** On the **Standard** FastTab, set the **Standard Code**. If lines already exist, the prompt *"Should the Lines be updated?"* appears. Upon confirmation, each line receives the **Print Value Option** stored in the **Standard Test Group Assignment**; for text/media characteristics it remains **Standard**.

### Value Summary

The extension displays the **Value Summary** FastTab in the test certificate (not editable). It shows the key figures per characteristic calculated from the document lines:

| Field | Explanation |
|---|---|
| **Print Key** | Combines the lines into a grouping unit (depending on the test certificate creation type: Test Certificate No., Lot No., source lot, or vendor lot). Serves as the sorting attribute of the consolidation. |
| **Group Name** | Shows the test group of the key figure. |
| **Characteristic Description** | Shows the characteristic to which the key figure applies. |
| **Value Option** | Indicates which key figure it is: **Min.**, **Max.**, or **Average**. |
| **Value** | Shows the calculated key figure (minimum, maximum, or average rounded to three decimal places). |

The consolidation is recalculated automatically as soon as document lines are added or deleted or the **Standard Code** is changed. Which key figures actually appear depends on the **Print Value Option** of the respective test group (see Standard Test Group Assignment).

## Output: printing and sending

After the document lines are filled and the values are consolidated, the test certificate is output. The output uses the report set up per **standard** and the configured layout (chapter *Setting up reports and layout per standard*).

1. **Print Document:** Generates the printout. If a dedicated report is assigned to the standard, it is used; otherwise the default test certificate report. Without a stored standard, no output takes place.
2. **Send by Email:** Generates the test certificate as a PDF and hands it over to the document's email dispatch.

**Printing the values:** For test groups with a **Print Value Option** other than **Standard**, the **Min.**, **Max.**, and/or **Average** columns from the **Value Summary** are printed instead of, or in addition to, the individual values. With the leading lot **Vendor Lot**, the vendor lot no. appears as the leading lot indication on the document.

## FAQ and troubleshooting

### Why can't I change the test certificate creation type?
If the automatic creation of the test certificate document is active in the base module, the system forces **Test Certificate Purely** and clears the **Leading Lot**. First disable the automatic creation to be able to select a different test certificate creation type.

### Why is the Leading Lot field grayed out?
The **Leading Lot** is editable only for the **Vendor Lot Purely** test certificate creation type. For any other type, the field is locked and cleared automatically.

### Why is the "Select Multiple Samples" action disabled?
The action is active only when the **Test Certificate Creation Type** is **Lot Purely**, **Lot. incl. Source Lot**, or **Vendor Lot Purely**. For **Test Certificate Purely**, use **Select Sample Values** instead.

### Why aren't the sample values transferred on release?
The automatic transfer requires three conditions: the **Transfer Sample Value from Templ. Vendor Lot No.** flag in the **Test Certificate Setup** is active, a sample with **Is Template Vendor Lot No.** = yes and a filled **Vendor Lot No.** exists, and there are open samples with the same vendor lot.

### Why do I get the message "… can only be set once."?
Only **one** template is allowed per vendor lot. A sample with **Is Template Vendor Lot No.** = yes and the same vendor lot no. already exists. First remove the existing marking.

### Why can't I set "Is Template Vendor Lot No."?
The flag can be set only in the status *Open* and only with a filled **Vendor Lot No.**. Check the status of the sample and whether a vendor lot is stored.

### Why don't any min./max. or average values appear on the document?
These key figures appear only when, in the **Standard Test Group Assignment**, a **Print Value Option** other than **Standard** is set for the relevant test group and standard. For characteristics of type *Text* or *Media*, it always remains **Standard**.

### Why can't a test group or standard be deleted?
If entries still exist in the **Standard Test Group Assignment**, the system prevents the deletion with *"The Table … has entries. Delete them before."*. First remove the associated assignments.

### Why does the system report "Report '…' has no Word layout." (or similar)?
The selected **Report Type** expects a layout of this type, which does not exist for the report stored under **Report ID**. Select a matching report type or store the corresponding layout.

### Why is no document generated on print?
The output requires a set **standard** (Standard Code) as well as existing document lines. Without a standard or without lines, **Print Document** or **Send by Email** aborts without output.

## Typical use cases

### 1. One test certificate per vendor lot across several internal lots

**Trigger:** A customer requests a test certificate that refers to the **vendor lot**, even though the goods have been split across several internal lots in one's own warehouse.

**Entry point in BC:** The QA user opens the **Test Certificate Report**. The default **Test Certificate Creation Type** = **Vendor Lot Purely** comes from the **Test Certificate Setup**; if it is not set there, the user selects it in the header and sets the **Leading Lot** = **Vendor Lot**.

**Core process:** Via **Select Multiple Samples**, the user opens the **Vendor Lot No. List** and selects the relevant vendor lot. The system adopts all associated samples – across all internal lots – into the document lines. The user then sets the **Standard Code** and confirms *"Should the Lines be updated?"*; the lines receive the **Print Value Option** from the **Standard Test Group Assignment**. In the **Value Summary**, the user checks the consolidated values.

**Conclusion:** The user outputs the document via **Print Document**; on the document, the vendor lot no. appears as the leading lot.

### 2. Sample value template per vendor lot

**Trigger:** For one vendor lot, several goods receipts (internal lots) arrive; according to the vendor certificate the values are identical and should not be recorded multiple times.

**Entry point in BC:** The QA user opens the **Samples** list and the associated sample card. A prerequisite is the active **Transfer Sample Value from Templ. Vendor Lot No.** flag in the **Test Certificate Setup**.

**Core process:** The user records the values on **one** sample with a filled **Vendor Lot No.** and sets **Is Template Vendor Lot No.** = yes there (possible only in the status *Open*). The user then triggers the release of all samples. The system shows the prompt *"Do you want to transfer the Sample Values from the Vendor Lot No. to all samples with the same Vendor Lot No.?"*.

**Conclusion:** After confirmation, the system transfers the values to all open samples with the same vendor lot and releases them. The samples are thus fully ready for test certificate creation.

### 3. Consolidated key figures per standard in the test certificate

**Trigger:** A test certificate should not show all individual values per characteristic, but rather **minimum, maximum, and average**, as required by the applicable standard.

**Entry point in BC:** The QA manager opens the page of the same name via the **Standard Test Group Assignment** action (from the **Standards** or **Test Groups** list).

**Core process:** For the relevant test group and standard, the manager sets the **Print Value Option** = **Min./Max. Value and Average Value**. The user then creates the **test certificate**, fills the lines (via **Select Sample Values** or **Select Multiple Samples**), and sets the **Standard Code**; the lines automatically receive the print value option. The calculated key figures appear in the **Value Summary**.

**Conclusion:** The document is output via **Print Document** or **Send by Email**; for the affected test groups, the **Min.**, **Max.**, and **Average** columns are printed.
