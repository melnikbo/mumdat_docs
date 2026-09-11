---
title: Anwenderhandbuch m+m Test Certificate Management
---

# User Guide m+m Test Certificate Management

This guide describes how to operate the **m+m Test Certificate Management** module (test data) in Microsoft Dynamics 365 Business Central. It is intended for users who work day to day with certificates, samples, test reports and the related documents, as well as for key users and administrators who set the module up. All field, page and action names correspond to the English user interface of Business Central.

---

## 1. Introduction

### Purpose of the module

With the **Test Certificate Management** module you record and document quality inspections for items, machine centers and work centers as well as for documents from purchasing, sales, warehousing and production. For each test certificate you create one or more **Samples**, record the **sample values** of the individual test characteristics for each sample, and then release the certificate. From released certificates you generate a printable and sendable **Test Certificate Report**.

Beyond that, the module controls the **Test Status** on the document lines (for example sales, purchase and warehouse documents), blocks inventory when required via a **Quarantine** location, and creates certificates automatically on certain events via **Rules**.

### Target audience

The primary audience is **operational users** in goods receipt, quality assurance, production and sales, who record samples, enter test values, release certificates and print or send test certificate reports on a daily basis. Secondarily, the guide addresses **administrators and key users**, who maintain the **Test Certificate Setup**, the master data (standards, test characteristics, test groups, test templates) and the **Rules**.

### Short process overview

The typical flow in the module runs in the following order:

1. **Setup** – An administrator maintains the number series, the quarantine settings and the report options in the **Test Certificate Setup** and creates the test certificate users and user groups.
2. **Master data** – Key users maintain **Test Certificate Standards**, **Test Certificate Characteristics**, **Test Groups** and **Test Templates** (the templates determine which characteristics a certificate contains).
3. **Rules (optional)** – Via **Rules** you define on which event (for example the release of an order) a certificate is automatically created according to a test template.
4. **Daily work** – The user creates a **Certificate** (manually or automatically), creates **Samples**, records the **sample values** and releases the samples and the certificate.
5. **Output** – From the released certificate a **Test Certificate Report** is produced, which is printed or sent by **email**. Notifications and history lists document the process.

### Navigation and entry point

All test certificate functions are reachable in every role center from the ribbon under the **Test Certificate Management** group. This group contains the **Administration** subgroup (setup and master data), the lists **Test Certificate List**, **Test Certificate Rule List** and **Test Certificate Rule Filter List**, as well as the **Reports And Tasks** group with **Test Cert. Report List**, **Test Cert. Note Entry** and **Test Cert. Notification History**. Administration pages can additionally be found via **Search**; in day-to-day work, however, the path through the **Test Certificate Management** ribbon is the intended entry point.

---

## 2. Quick start for users

The quick start shows the shortest path from the configured system to the finished test certificate report. The setup (step A) is performed once by an administrator before users start working productively.

**A. Setup (one time, administrator).**
1. Open the setup card via **Test Certificate Management → Administration → Test Certificate Setup** and choose **Execute Initial Setup**. This creates the base data of the module.
2. Under **Numbering**, maintain the number series for test templates, certificates, samples and rules.
3. Create the test certificate users under **Test Certificate Management → Test Cert. User** and mark at least one user in the **Test Certificate User Group** as a user with the quality assurance right.

**B. Master data (key user).**
4. Maintain **Test Certificate Standards**, **Test Cert. Characteristics** and **Test Groups**.
5. Create a **Test Template**, transfer the characteristics of a test group with **Transfer Test Group**, set **Valid From**/**Valid To** and activate the template with **Activate Templates**.

**C. Daily work (user).**
6. Create a **Certificate** – either automatically via an active **Rule**, or manually via the action **Create Item Test Certificate** on the item card or **Open Test Certificate Samples** on a document line, or directly via **Test Certificate List → New** and selection of a test template.
7. On the **Test Certificate Card**, choose the action **New Sample** (one sample) or **Create Multiple Samples** (several samples).
8. Open the **Test Cert. Sample Card**, use **Get Serial/Lot No. from Document** to retrieve the lot no./serial no. and record the **sample values** for each test characteristic in the value grid.
9. On the sample, choose **Release** (or **Release All Samples** in the sample list). The sample receives the status **Released**.
10. On the **Test Certificate Card**, choose **Release**. If open samples still exist, Business Central reports that all samples must be released first. After release – depending on the setup – a **Test Certificate Report** is created automatically.
11. Open the **Test Certificate Report**, choose **Select Sample Values** if required, and then **Print Report** or **Send Email**.

If a certificate is changed again, set it back to **Open** with **Reopen** (with the corresponding setup, only possible for a user with the quality assurance right).

---

## 3. Permissions and test certificate users

The module distinguishes users by a **quality assurance right**. Many controlling actions (activating rules, editing templates and mail templates, reprinting or deleting test certificate reports, posting blocked quarantine inventory, reopening certificates) are reserved exclusively for users with this right. Therefore create the test certificate users and user groups before users start working productively.

### 3.1 Test Certificate Users

**Entry point:** Open the **Test Certificate User** list via **Test Certificate Management → Test Cert. User**.

Who maintains this: the administrator, before first use. Every user who is to receive notifications or is recorded as an inspector is entered here.

| Field | Explanation |
|---|---|
| User ID | If you select a Business Central user here, then this user is recorded as a test certificate user and can receive notifications as well as be used as a recipient or inspector in rules and test certificate reports. |
| Notification Method | Defines by which channel the user is informed about test certificate events. **Email:** The user receives an email (via the Notification Email report). **Note:** The user receives an internal Business Central notification as a note entry. |

Via the action **Notification Schedule** you open, for a selected user, the associated **Notification Schedule** (see chapter 9), in which you define the frequency and time of the notifications.

### 3.2 Test Certificate User Groups and quality assurance right

**Entry point:** Open the **Test Certificate User Group List** via **Test Certificate Management → Test Cert. User Group** and open a group by its line to reach the card.

Process: The administrator groups the test certificate users and determines, per group member, whether it holds the quality assurance right. The right determines the permissions for all controlling actions of the module.

| Field | Explanation |
|---|---|
| Code | Unique code of the test certificate user group. When you create a group, you can subsequently assign members to it and, via the test group assignment, control which test groups the members see. |
| Description | Plain-text label of the group for selection in lists. |

On the card you maintain the members in the **Test Certificate User Group Member** subform:

| Field | Explanation |
|---|---|
| User ID | Assigns a test certificate user to the group. When a user is a member, then the group assigns test group views and – if the flag is set – quality assurance rights to that user. |
| Quality Assurance | If this flag is set, then the user may perform the controlling actions of the module: activate/deactivate/copy rules, edit test templates and mail templates, maintain user groups, delete already printed test certificate reports, and perform postings on quarantine locations and bins. If the flag is not set for any member, the module treats the group as freely editable and, when the group is created, automatically adds at least one user with the quality assurance right, so that a responsible person always exists. |

Note on permissions: The module ships with the permission set **MuM TC Permission**, which covers the data access rights to the test certificate objects. The quality assurance right from the user group additionally controls – independently of the permission set – the business actions named above.

---

## 4. Setup

The **Test Certificate Setup** is the central, company-wide setup card of the module (one record per company). It is the most extensive configuration object and should be fully maintained before users start working.

**Entry point:** **Test Certificate Management → Administration → Test Certificate Setup**. The card can additionally be found via **Search**. The fields can only be edited by users with the quality assurance right.

Before first use, run the action **Execute Initial Setup**; it creates the necessary base data of the module. With **Setup Quarantine Bins** the quarantine bins are created and the bins are then displayed.

### 4.1 General settings

These settings control the fundamental behavior of certificates and samples in day-to-day work.

| Setup | Explanation |
|---|---|
| Certificate Can Be Re-Opened Only by QA User | If enabled, then an already released certificate can only be reopened via **Reopen** by a user with the quality assurance right; other users receive an error message. This keeps the release controlled. |
| Ignore Rule When Creating Test Certificate Manually | If enabled, then the rules are not applied when a certificate is created manually; the user selects the template and assignment themselves. Without the flag, the rule specifications also apply for manual creation. |
| Automatic Sample Creation | If enabled, then the module automatically creates the intended number of samples when a certificate is created, so that the user can start entering values directly. |
| Warn Before Changing Production Order Status | If enabled, then Business Central warns before the status of a production order for which a certificate exists is changed – so that no certificate references are lost unnoticed. |
| Caption Default Value 1 | Defines the column heading under which the first default value of a test characteristic is shown in templates, certificates and samples. If you store a text here, then it appears everywhere instead of the standard label "Default Value 1". |
| Caption Default Value 2 | Defines, analogously, the column heading for the second default value. |
| Block Lot No. | If enabled, then the lot belonging to a certificate is blocked in inventory as long as the certificate is not released; the lot can then be used further only after a successful inspection. |
| Allow Reopen Processed Samples | If enabled, then a sample already marked as "processed" may be reopened. Without the flag, reopening processed samples is blocked and Business Central reports this on the attempt. |
| Processed Sample Editable | If enabled, then the fields of a sample marked as processed remain editable. Without the flag, the module blocks processed samples against changes and sets the processed flag automatically on release or reopening. |
| Update Activate Flag Job Queue | If enabled, then the time-controlled activation/deactivation of test templates and rules is updated via the job queue, instead of only when the lists are opened. This keeps validity periods up to date even without opening them manually. |

### 4.2 Quarantine Setup

Quarantine blocks inspected but not yet released inventory. You need a quarantine location or bin as well as – depending on warehouse complexity – the posting and bin type settings. This configuration takes effect in day-to-day work in chapter 8 (document integration and warehouse).

**Entry point for creating the bins:** action **Setup Quarantine Bins** on this card.

| Setup | Explanation |
|---|---|
| Quarantine Location | If you store a location, then inspected inventory is transferred there and blocked for further use until the certificate is released. Only locations without directed put-away and pick and without mandatory bins can be selected. |
| Quarantine Bin Code | Defines the specific bin within the quarantine location to which blocked inventory is posted. |

**Posting.** These options control whether and how inventory is automatically posted to quarantine.

| Setup | Explanation |
|---|---|
| Automatically Post Item to Quarantine | If enabled, then the module automatically posts the inventory to be inspected to the quarantine bin as soon as the certificate is created; the user does not need to trigger the block manually. |
| Ask Before Post to Quarantine | If enabled, then a confirmation prompt appears before the automatic quarantine posting, so that the user can confirm the transfer. |
| Block Posting Quarantine Lines | If enabled, then document lines with quarantine inventory cannot be posted normally as long as the certificate is not released – the inventory is thereby protected against accidental use. |
| Enable Quarantine Warning Before Validating Sample Value | If enabled, then Business Central points out, before confirming a sample value, that the inventory is in quarantine, so that the inspector takes the block into account. |

**Advanced Warehousing.** These codes are needed when the quarantine location is operated with directed put-away and pick (zones and bin types).

| Setup | Explanation |
|---|---|
| Quarantine Zone Code | Defines the zone in which the quarantine bins of a location with directed put-away and pick are located. |
| Quarantine Bin Type Code | Determines the general bin type used when the quarantine bins are created. |
| Quarantine Bin Type Receive | Determines the bin type used for the goods receipt into quarantine. |
| Quarantine Bin Type Ship | Determines the bin type for the goods shipment out of quarantine. |
| Quarantine Bin Type Put Away | Determines the bin type for the put-away into quarantine. |
| Quarantine Bin Type Pick | Determines the bin type for the pick out of quarantine. |

### 4.3 Numbering

Without number series, templates, certificates, samples and rules cannot be created. Create the series before first use.

| Setup | Explanation |
|---|---|
| Test Certificate Template Nos. | If you store a number series here, then new test templates automatically receive a consecutive number from this series. |
| Test Certificate Nos. | Determines the number series for new certificates. Without this series no certificate can be created (Business Central checks the field on creation). |
| Sample No. Series | Determines the number series for new samples. |
| Test Certificate Rule Nos. | Determines the number series for new rules. |

### 4.4 Report

These settings control the layout and the automatic creation of the test certificate report (see chapter 9).

| Setup | Explanation |
|---|---|
| Test Certificate Report Nos. | Determines the number series for new test certificate reports. |
| Logo Position on Documents | Defines where the company logo appears on the printed test certificate report. **No Logo:** without logo. **Left / Center / Right:** The logo is output at the selected position in the document header. |
| Picture Reference Symbol | Defines the character with which the report refers to a stored picture of a test characteristic. If you set a symbol here, then it appears at the value positions with media reference. |
| Automatically Create Test Certificate Report Document | If enabled, then the module automatically creates the associated test certificate report on release of a certificate; without the flag the user creates the test certificate report manually. |

### 4.5 Job queue (scheduling)

| Setup | Explanation |
|---|---|
| Restart Job Queue On Error | If enabled, then the module automatically restarts a failed job queue entry of the rule-based processing after the set wait time. On activation, the wait time is preset to 60 minutes if it is still 0. |
| Restart Job Queue After No. Of Minutes | Defines the wait time (in minutes) until the automatic restart. The field can only be edited if restart on error is enabled. |

---

## 5. Master data

The master data defines **what** is inspected. It is maintained by key users with the quality assurance right. Order in practice: first **Test Certificate Standards**, **Test Cert. Characteristics** and, if applicable, **Lookups**, then **Test Groups** (bundles of characteristics), and finally **Test Templates** (the concrete composition that a certificate receives). The test template is the link to daily work (chapter 7) and to the rules (chapter 6).

### 5.1 Test Certificate Standards

**Entry point:** **Test Certificate Management → Administration → Test Certificate Standards**.

Process: The key user maintains the test standards, which are later assigned to a test template via the **Standard Assignment** and shown on the test certificate report.

| Field | Explanation |
|---|---|
| Code | Unique code of the standard. When you create a standard, then it is available for selection in test templates and certificates and can be printed on the test certificate report. |
| Description | Plain-text label of the standard. Via the action **Translation** you store language-dependent labels, so that the test certificate report can be output in the language of the recipient. |

### 5.2 Test Certificate Characteristics

**Entry point:** **Test Certificate Management → Administration → Test Cert. Characteristics**.

Process: A **Test Certificate Characteristic** is a single attribute that is later evaluated in a sample (for example a measured value). The key user creates the characteristics; via test groups and test templates they flow into the certificates.

| Field | Explanation |
|---|---|
| No. | Consecutive number of the test characteristic. |
| Description | Label of the characteristic; it must not be empty and appears as the line label in templates, certificates and samples. Via the action **Translation** you maintain language-dependent labels. |
| Data Type | Defines which kind of value is recorded for this characteristic. **Text:** free text. **Integer:** integer value. **Decimal:** decimal number (numeric check). **Media:** a picture/media object. If values already exist for this characteristic, the data type can no longer be changed. |
| Reference-Type | Determines whether the input value is checked against a stored value list. **(blank):** free entry according to the data type. **Table:** The value must be a valid entry from a lookup. |
| Reference-Value | For Reference-Type **Table**, refers to the associated lookup (see 5.3). If you choose a lookup here, then only the values defined there are permitted during value entry. |
| Media | Holds a default picture for the characteristic. Via **Import Media** you load a picture, via **Show Media** you open it. |
| Media Exists | Indicates whether a picture is stored for the characteristic. |

### 5.3 Lookups for test characteristics

**Entry point:** **Test Certificate Management → Administration → Test Certificate Lookup Types**. You open the associated values via the action **Value** in the line.

Process: A lookup is a closed value list that is assigned to a test characteristic with Reference-Type **Table**. This ensures that inspectors only record permitted values.

| Field | Explanation |
|---|---|
| Code | Unique code of the lookup type. When you create a lookup type, then it can serve as the reference value of a test characteristic. |
| Description | Label of the lookup type. |

For each lookup type you maintain the permitted values (page **Test Certificate Lookup Values**):

| Field | Explanation |
|---|---|
| Lookup Value | A permitted value of the lookup type. If you store values, then the inspector can only choose from this list during value entry. |
| Description | Explanation of the value. Via the action **Translation** you store language-dependent labels. |

### 5.4 Test Groups

**Entry point:** **Test Certificate Management → Administration → Test Certificate Test Groups**. You open the assigned characteristics via the action **Characteristic Assignment**.

Process: A **Test Group** bundles several test characteristics and determines their print form. Test groups are subsequently transferred into test templates (see 5.5) and at the same time control which test groups a user may see via their user group.

| Field | Explanation |
|---|---|
| Code | Unique code of the test group. When you create a test group, then it can be assigned to a test template and assigned to its members via the user group. A code that is already used in certificate or template lines cannot be deleted. |
| Description | Label of the test group. Via the action **Translation** you maintain language-dependent labels. |
| Print Style | Defines how the characteristics of the group appear on the test certificate report. **(blank):** no special print form. **Lines:** one line per characteristic. **Columns:** the characteristics side by side in columns. **Text Block:** a coherent text block (content from the Text Block Text field). |
| Text Block Text | For Print Style **Text Block**, holds the text to be output. |

Via **Copy Characteristics from** you transfer the characteristic assignment of an existing test group into the current one, in order to build up comparable groups quickly.

### 5.5 Test Templates

**Entry point:** **Test Certificate Management → Administration → Test Cert. Template List** (list); opening a line leads to the **Test Cert. Template Card**.

Process: The **Test Template** is the concrete composition of test groups and characteristics with their default values that a certificate receives. Templates are **versioned** and time-controlled via **Valid From**/**Valid To**. A certificate, an item or a rule always refers to a template; daily work (chapter 7) and the rules (chapter 6) consume the template.

**Header of the test template:**

| Field | Explanation |
|---|---|
| No. | Number of the test template from the number series. Several versions share the same No. and are distinguished by the version code. |
| Version Code | Code of the template version. If you keep several versions, then the active version is always the one whose validity period includes the work date. |
| Description | Label of the template. |
| Creation Date | Creation date of the version (set automatically). |
| Valid From | Start of the validity period (mandatory field). If the work date falls within the period, then the version can be activated. |
| Valid To | End of the validity period (mandatory field). The module prevents overlapping validity periods of several versions of the same template and reports a date that lies before "Valid From". |
| Active | Indicates whether the version is active. When a version becomes active, then other versions of the same No. are deactivated and the linked rules adopt the validity period. If the template becomes inactive, the module deactivates the associated rule and notes this in its description. |
| Sample Data Filling | Defines how new samples are prefilled with values (adoption of the default values or of the most recently recorded sample values). |
| Show Standard Values | If enabled, then the default values (Default Value 1/2) are shown as separate columns in the value grid of the sample, so that the inspector sees the target value. |
| Number of Samples | Defines how many samples are created by default when a certificate is created. |

**Lines of the test template** (subform **Test Certificate Template SubPage**):

| Field | Explanation |
|---|---|
| Test Group Code | Assigns the line to a test group. |
| Characteristic No. | Refers to the test characteristic within the test group. |
| Test Group Description | Label of the test group (display). |
| Character Description | Label of the test characteristic (display). |
| Default Value 1 | Target or default value 1 of the characteristic. If you set a default value, then it is prefilled during sample creation; for Reference-Type Table it is checked against the lookup, for numeric data type it is evaluated as a number. The column heading corresponds to the caption from the setup (4.1). |
| Default Value 2 | Target value 2 of the characteristic (for example upper limit value), analogous to Default Value 1. |
| Data Type | Shows the data type of the characteristic (Text, Integer, Decimal, Media). |
| Print | If enabled, then the line is printed on the test certificate report. |
| Test | If enabled, then the line is transferred when a certificate is created from the template. Only lines with the flag set flow into the certificate. |

**Process steps to set up a test template:**
1. First create the template header with **No.**, **Version Code**, **Valid From**/**Valid To**.
2. Then transfer the characteristics of a test group into the template lines with **Transfer Test Group** and adjust the **default values**.
3. Via **Standard Assignment** you assign the standards to be printed to the template (field **Print Sign Area** per assignment).
4. Finally activate the version via **Activate Templates** (in the template list). Only an active template can be used by certificates and rules.

Via **Comment** you store header and line comments for the template.

### 5.6 Test Certificate Mail Templates

**Entry point:** **Test Certificate Management → Test Cert. Mail Tmpl. List** (list); opening a line leads to the **Test Cert. Mail Template Card**.

Process: A **Mail Template** defines the subject and text of the email that is sent on a test certificate response (rule response). The text contains placeholders that are filled with the concrete test and document data on sending. Mail templates are created per test certificate response and category and are consumed in the rule/notification process (chapters 6/9).

| Field | Explanation |
|---|---|
| Subject Code | Refers to the test certificate response for which the mail template applies. When you choose the code, then category, description and subject are adopted. |
| Subject Text | Subject line of the email, with optional placeholders. |
| Category | Test certificate category for which the template applies (display). |
| Description | Label of the mail template (display). |

In the **Test Cert. Mail Template** subform you record the text lines with placeholders (**Line Text** and **Value 1** through **Value 10**). The permitted placeholders are managed in the **Test Cert. Mail Template Value List** and are replaced on sending, for example by certificate number, document number, user, object, lot, quantity.

### 5.7 Test certificate system tables (reference)

The following pages contain reference data that controls the rule processing (chapter 6). They are largely predefined by the app and only supplemented when needed.

- **Test Cert. Category** – business areas (for example purchasing, sales, item) under which events, responses and rules are grouped. Fields: **Code** and **Description**.
- **Test Cert. Entity** – assigns a table/table pair (with an optional related table) to a test certificate category. This lets the module recognize the responsible category from a document. Fields include: **Table ID**, **Related Table ID**, **Category**.
- **Test Certificate Events** – trigger points ("When") at which rules are processed (field **When** per event).
- **Test Certificate Responses** – reactions ("Then") that a rule executes, for example create certificate, block item, notify user (field **Then** per response).
- **Test Cert. Attribute** – defines a **Special Attribute**, i.e. a field reference reachable via a related table (for example the customer on the production order) that serves as an additional rule criterion. Fields include: **Table ID**, **Field ID**, **Attribute Table ID**, **Special Attribute**.

---

## 6. Rules and automatic certificate creation

Rules create certificates automatically as soon as a certain event occurs in Business Central (for example the release of an order, validation of a sample value, a time-controlled run). A rule connects three building blocks: a **Test Cert. Category** (business area), a **Test Template** (what is inspected) as well as **Rule Filters** (which records the rule applies to) and **Event Responses** (on which event which reaction occurs).

### 6.1 Rule master data and rule processing

Processing runs as follows: when an event occurs, the module determines the category via the **Test Cert. Entity**, collects all active rules for the event and category, retains in priority order only the rules whose **Rule Filters** all apply, and executes the stored **Event Responses** per rule – the response then, for example, creates the certificate.

**Entry point:** **Test Certificate Management → Test Certificate Rule List** (list); opening a line leads to the rule card **Test Cert. Rule**. The card can only be edited while the rule is inactive and the user holds the quality assurance right.

| Field | Explanation |
|---|---|
| Category | Assigns the rule to a business area. If you change the category, then the existing rule filters and event responses of the rule are removed, as they are category-specific. |
| No. | Number of the rule from the number series. |
| Active | Indicates whether the rule is effective. Only active rules are executed on an event. |
| Priority | Defines the order in which competing rules are evaluated. |
| Description | Label of the rule. |
| Test Cetificate Template No. | Refers to the test template according to which the certificate is created. If you choose a template, then Valid From/To are adopted; an inactive template is rejected. |
| Test Certificate Template Version Code | Version of the assigned test template. |
| Valid From / Valid To | Validity period of the rule (adopted from the template). |
| Rule Type | Defines how the rule triggers. **Standard:** The rule takes effect on every matching event. **Interval:** The rule takes effect only when a counter or an accumulated quantity reaches a threshold (interval control via the rule filters). |
| Last Run Date / Execution Interval / Run Per Item Quantity | Visible only for time-controlled rules: they control the next run via the job queue and the quantity accumulated per object. |

**Rule Filters** (subform): Each filter line checks a field of a document, a line or a related table.

| Field | Explanation |
|---|---|
| Table ID / Table Name | Defines the table to be checked. |
| Field ID / Field Caption | Defines the field to be checked. |
| Field Filter | Defines the value/filter that must apply for the rule to take effect. **If set, then** the rule is only applied to records that satisfy this filter. |
| Field Type | Shows the type of the field value: **Other**, **Boolean** or **Option** – the filter is interpreted accordingly. |
| Related Table ID / Related Table Caption | For filters via a related table (special attribute), refers to it. |
| Count Interval / Execution Interval / Interval Field / Interval counter | Only for Rule Type **Interval**: they define whether the trigger is by count (counter) or by accumulated field quantity and at which threshold. Via **Edit Interval Counter** you reset the counter. |

**Event Response** (subform): connects, per line, an **Event** with a **Response** of the same category; via **Notify User** an additional notification is triggered.

Actions on the rule: **Activate Rule** (sets Active; requires a valid, active template and prompts on an empty time interval), **Deactivate Rule**, and in the rule list **Copy Rule** (duplicates the rule together with filters and event responses).

### 6.2 Setting up automatic certificate creation

This dedicated setup connects master data and rule up to the automatic certificate in the daily flow. It is configured by an administrator/key user with the quality assurance right before automatic creation is first used; it takes effect in daily work on the documents (chapters 7/8).

1. **First**, ensure that an **active test template** exists (chapter 5.5): template with a valid period and **Activate Templates**. *If no active template exists, then the rule cannot be activated.*
2. **Then** check the **Test Cert. Category** and the **Test Cert. Entity** (chapter 5.7): the entity assigns the relevant table to the category. *If the assignment is missing, then the module recognizes no category from the document and the rule does not take effect.*
3. **Then** create the **Test Cert. Rule** via **Test Certificate Rule List → New**, choose category and Test Certificate Template No. and set the **Priority**.
4. **Then** record the **Rule Filters** (which records) and the **Event Response** (which event triggers which response, for example "Create Test Certificate"). *If a filter does not apply, then the rule is skipped for that record.*
5. **Finally**, choose **Activate Rule**. From now on, Business Central automatically creates a certificate according to the template on the matching event. The user then finds the certificate via the **Test Status** of the document line or via **Test Certificate List** (chapters 7/8).

### 6.3 Setup wizard for rules

The **Test Certificate Rule Setup Wizard** guides an administrator step by step through the preparation of the rules. Via the steps **Category → Entity → Attribute → Event → Response**, the wizard opens the associated setup page in each case (action **Open …**), so that the base data is present before a rule is created. With **Back**, **Next** and **Finish** you navigate through the wizard.

---

## 7. Daily work: certificate, samples and sample values

This chapter describes the core of daily work: creating a certificate, creating samples, recording the sample values and the release.

Daily work is controlled by the **Test Certificate Setup** (chapter 4: automatic sample creation, quarantine, lot blocking, processed samples) as well as by the **Test Templates** (chapter 5.5: which characteristics and default values, number of samples). Certificates can additionally arise automatically through **Rules** (chapter 6).

### 7.1 The Test Certificate Card

**Entry point:** **Test Certificate Management → Test Certificate List** opens the **Test Certificate List**; via a line you reach the **Test Certificate Card**. Alternatively, the card is opened directly when a certificate is created (actions in 7.4) or via the detail information of a document line (chapter 8).

**General:**

| Field | Explanation |
|---|---|
| No. | Number of the certificate from the number series (not editable). |
| Status | **Open:** The certificate is in progress; lines and samples can be changed. **Released:** The certificate is completed; the lines are locked and the test certificate report can be created. |
| Different to Default Value Exists | If this (highlighted) flag is set, then at least one recorded sample value deviates from the default value of the template – an indication for the quality assessment. |
| Description | Free-text label of the certificate. |
| Creation Date | Creation date (set automatically). |
| Test Certificate Standard | Assigns a standard to the certificate (selection from **Test Certificate Standards**); it is shown on the test certificate report. |
| Document Type | Defines what the certificate refers to. Available are the document-related types (Purchase Order, Sales Order, Warehouse Receipt, Warehouse Shipment, Warehouse Put-away/Pick, Production Order, Item Journal) as well as the object-related case (blank). If you change the document type, then the dependent reference fields are reset (only permitted as long as no sample exists). |

Depending on the document type, the card shows additional groups whose fields relate exclusively to the selected reference (for clarity, only the matching group is visible in each case):

- **Location** (for object-related certificates, document type blank): **Location Code** of the object to be inspected.
- **Template:** **Test Cetificate Template No.** (mandatory; the selection transfers version, number of samples and sample data filling) and **Test Certificate Template Version Code**.
- **Sample Process:** **Number of Samples**.
- **Object:** **Object Type** – **(blank)**, **Item**, **Machine Center** or **Work Center** –, **Object No.**, **Variant Code** and the descriptions. The object type determines which master data is inspected.
- **Document** or **Source** (for document-related certificates): **Document No.**, **Document Line No.**, **Source Type** (**(blank)**, **Customer**, **Vendor**), **Source No.** and **Source Name**, as well as, for Item Journal, the journal fields.
- **Production Order** (for document type Production Order): **Prod. Order Status**, **Prod. Order No.** and **Prod. Order Line Type** – **(blank)**, **Production Order Line**, **Production Order Component** or **Production Order Routing Line** – with the respective matching reference fields.

**Lines (subform Test Certificate SubPage):** The certificate lines arise from the template and contain, per test characteristic, **Test Group Code**, **Characteristic No.**, descriptions, **Data Type**, **Default Value 1/2** and the **Print** flag.

**FactBoxes** on the right: **Test Certificate Sample FactBox** and **Test Certificate Sample Value FactBox** (overview of the samples and values), the header and line comments as well as the **Test Certificate Report List** for the certificate.

**Actions of the Test Certificate Card:** **Test Certificate Sample FactBox** (opens the sample list), **New Sample**, **Create Multiple Samples**, **Release**, **Reopen**, **Update Test Certificate Lines** (transfers the lines again from the template), **Open Source Document** (jumps to the source document or object) and **Comment**.

### 7.2 The Test Cert. Sample Card and value entry

**Entry point:** action **Test Certificate Sample FactBox** or **New Sample** on the Test Certificate Card; alternatively **Open Test Certificate Samples** on a document line (chapter 8). From the sample list, a line opens the **Test Cert. Sample Card**.

**General (Test Cert. Sample Card):**

| Field | Explanation |
|---|---|
| Processed | If set, then the sample counts as completed; its fields are – depending on the setup "Processed Sample Editable" – locked against changes. |
| Sample No. | Number of the sample from the number series (not editable for a processed sample). |
| Status | **Open:** value entry possible. **Released:** values locked; the certificate can only be released once all samples are released. |
| Description | Free-text label of the sample. |
| Creation Date | Creation date. |
| Document Type | Reference of the sample (display). |
| Sample Difference To Default | Indicates whether a sample value deviates from the default value. |
| Print Sample | If enabled, then the values of this sample are included in the test certificate report. |
| Key Value | If enabled, then the lines of this sample are treated as key values and are given priority when the test certificate report is created. |
| Quarantine | If enabled, then the associated inventory is marked as quarantine; the flag is transferred to samples with the same lot/serial no. |
| Test Cetificate Template No. | Refers to the underlying test template (jump to the template via detail information). |

**Item Tracking:** In the group for item tracking you record **Item No.**, **Variant Code**, **Serial No.** and **Lot No.**. Via **Get Serial/Lot No. from Document** you adopt the values present in the source document; the associated quantity and the tracking description are determined automatically.

**Value entry (subform Test Cert. Sample SubPage):** Here you enter the measured value for each test characteristic.

| Field | Explanation |
|---|---|
| Test Group Code | Test group of the line (display). |
| Characteristic No. | Test characteristic of the line (display). |
| Character Description | Label of the test characteristic. |
| Data Type | Data type of the characteristic (Text, Integer, Decimal, Media). |
| Sample Value | The recorded measured value. If you enter a value, then it is checked against the data type or the lookup and – on deviation from the default value – marked as a deviation. |
| Default Value 1 / Default Value 2 | Target values from the template; only visible if **Show Standard Values** is enabled in the template. |
| Sample Difference To Default | Indicates whether the recorded value deviates from the default value. |
| Key Value | Marks the line as a key value. |
| Media Exists | Indicates whether a picture is stored for the characteristic; via **Import Media**/**Show Media** you manage the picture. |
| Processed | Indicates whether the line is processed (display). |

The value grid shows only the test groups for which the signed-in user is authorized via their test certificate user group. Thus inspectors see only the characteristics relevant to them.

**Actions of the Test Cert. Sample Card:** **Release**, **Reopen** (not possible as long as the certificate is released) and **Get Serial/Lot No. from Document**.

### 7.3 Release of samples and certificate

The closing process follows a fixed order (for details see also the quick start, chapter 2):

1. Record **sample values** for each sample in the value grid.
2. On each sample, choose **Release** (or, in the sample list, **Release All Samples**). The sample receives the status **Released**; depending on the setup it is at the same time marked as processed.
3. On the **Test Certificate Card**, choose **Release**. If open samples still exist, Business Central first requires their release. Then the certificate receives the status **Released**, the samples are set to processed and – with the setup **Automatically Create Test Certificate Report Document** enabled – the test certificate report is created.
4. If required, **Reopen** on the certificate (with the setup **Certificate Can Be Re-Opened Only by QA User**, only by a user with the quality assurance right). Reopening resets the **Test Status** of the document line.

### 7.4 Creating a certificate – entry points

A certificate arises in one of the following ways:

- **From the master data:** On the **Item Card** or in the item list, the action **Create Item Test Certificate**; on the work center or machine center card, **Create Work Center Test Certificate** or **Create Machine Center Test Certificate**. You choose a test template; the Test Certificate Card then opens.
- **From a document:** On a document line, the action **Open Test Certificate Samples** or **Create Test Certificate** (see chapter 8).
- **Directly:** Via **Test Certificate List → New**, selection of the test template and entry of the reference (object/document).
- **Automatically:** Via an active **Rule** on the matching event (chapter 6).

---

## 8. Document integration, test status, quarantine and warehouse

The module extends the standard documents of Business Central with a **Test Status** and with actions with which you open, for a document line, the associated certificate or its samples or create a certificate. Affected are, in particular, the sales order and purchase order lines, the warehouse documents (warehouse receipt, warehouse shipment, pick, put-away, including warehouse/inventory variants), the production documents (**Production Order Routing**, **Production Order Component**, released/finished production order lines) as well as the journals (item journal, consumption, output and production journal) and the item tracking lines.

### 8.1 The test status on document lines

On the named document lines, the module adds the **Test Status** column. It is highlighted with color and is not directly editable; it is set by the associated certificate.

| Value | Explanation |
|---|---|
| **(blank)** | No certificate exists for the line; there is no inspection obligation or it has not yet been triggered. |
| **Test** | An open certificate exists for the line; the certificate is created but not yet released. |
| **Passed** | The associated certificate has been released and the line is inspected/released. |
| **Blocked** | The line is blocked; further processing is not permitted until the certificate is completed. |
| **Quarantine** | The inventory of the line is in quarantine (blocked inspection inventory). |

Note: On **Production Order Routing Lines**, the test status does not have the **Quarantine** value; there only **(blank)**, **Test**, **Passed** and **Blocked** are possible.

Via the detail information on the **Test Status** column you jump directly to the associated **Test Certificate Card**.

### 8.2 Actions on the document line

Per document, the following actions are available in the line group:

- **Open Test Certificate Samples** – opens, for the document line, the associated sample (for one sample the **Test Cert. Sample Card**, for several the sample list). Available on, among others, sales and purchase lines, warehouse lines, production lines and journal lines.
- **Create Test Certificate** / **Create Item Test Certificate** / **New Test Report** – creates a certificate or a test certificate report for the line (available on, among others, **Production Order Routing**, **Production Order Component**, item/consumption/output journal as well as finished/released production order lines).
- **Open Test Certificate** – on the **Lot No. Information Card**, opens the certificate belonging to the lot.

### 8.3 Quarantine and inventory blocking

If a **Quarantine Location** or bin is stored in the **Test Certificate Setup** and the automatic quarantine posting is enabled, then inventory to be inspected is automatically posted to the quarantine bin and blocked there until the certificate is released. Optionally a confirmation prompt precedes it (**Ask Before Post to Quarantine**), and document lines with quarantine inventory can be blocked (**Block Posting Quarantine Lines**).

In addition, a posting block applies: if a warehouse or sales document contains a line that concerns the **Quarantine Location** or a bin marked as quarantine, then the document can only be posted by a user with the quality assurance right; other users receive an error message. This prevents blocked inspection inventory from leaving the warehouse uncontrolled.

You create the quarantine bins via the action **Setup Quarantine Bins** in the setup; the affected bins are then displayed.

---

## 9. Test certificate report, print and email

From a released certificate the **Test Certificate Report** is produced – the printable and sendable proof of the inspection results.

**Entry point:** **Test Certificate Management → Reports And Tasks → Test Cert. Report List** opens the **Test Certificate Report List**; a line opens the **Test Certificate Report**. With the setup **Automatically Create Test Certificate Report Document** enabled, the test certificate report is already created when the certificate is released.

### 9.1 The test certificate report

The test certificate report header adopts the data of the certificate (source, document, object, standard, quantity). Key fields:

| Field | Explanation |
|---|---|
| No. | Number of the test certificate report from the number series. |
| Description | Free-text label; used as the message text in the email dispatch. |
| Test Certificate No. | Refers to the underlying certificate. If you set the certificate, then the report lines are adopted from the key sample values and the header data (source, object, document, standard) are filled. |
| Test Certificate Creation Date | Creation date of the underlying certificate (display). |
| Quality Assurance Users | Lists the test certificate users with the quality assurance right who belong to the printed test groups; they appear in the signature area of the report. |
| Test Certificate User | The test certificate user responsible for the report. |
| Print Counter | Counts the printouts of the report. An already printed report can only be deleted by a user with the quality assurance right. |

In the groups **Object**, **Source/Document** and **Standard**, the associated data (object type/no., document type/no., source type, standard) is mirrored read-only. The report lines (subform **Test Certificate Report SubPage**) contain, per value, the test characteristic, the **Sample Value**, the **Print Style** (Lines/Columns/Text Block) as well as lot no./serial no.

### 9.2 Printing and sending

On the test certificate report the following are available:

- **Select Sample Values** – opens the sample values and adopts the selected values as report lines.
- **Print Report** – produces the printed test certificate report (report) with the company logo (position according to the setup), header data and the results in the respective print style as well as stored pictures; the print counter is incremented.
- **Send Email** – produces the test certificate report as a PDF and opens an email to the stored address of the signed-in user with the PDF as an attachment (subject = Test Certificate No., text = Description).

### 9.3 Notifications and mail templates

Test certificate responses from rules can notify users. Per test certificate user, the **Notification Method** (Email or Note) determines how they are informed. The **Notification Schedule** defines the frequency.

**Entry point Notification Schedule:** action **Notification Schedule** on the **Test Certificate User** list (per user).

| Field | Explanation |
|---|---|
| Recurrence | Defines when accumulated notifications are sent. **Instantly:** immediately. **Daily / Weekly / Monthly:** bundled at the set point in time. |
| Time | Time of dispatch (except for Instantly). |
| Daily Frequency | **Weekday:** only on weekdays. **Daily:** on all days. |
| Monday … Sunday | For weekly recurrence: the weekdays of dispatch. |
| Date of Month / Monthly Notification Date | For monthly recurrence: **First Workday**, **Last Workday** or **Custom** (then a concrete day in the "Date of Month" field). |

The text of the email is produced from a **Test Cert. Mail Template** (chapter 5.6), whose placeholders are replaced by the concrete test and document data. Internal notifications appear as **Test Cert. Note Entry**.

---

## 10. History and traceability

The module documents its activities in several lists, which you reach under **Test Certificate Management → Reports And Tasks** or **→ Administration**:

- **Test Certificate List** – all certificates with status; entry point to the Test Certificate Card and starting point for evaluations. Via **Delete Selected** you remove marked certificates (together with the associated samples and comments).
- **Test Certificate Report List** – all created test certificate reports with Test Certificate No., description and **Print Counter**.
- **Test Cert. Note Entry** – the notifications created per recipient with type (**New Record**, **Approval**, **Overdue**), triggering record, target page and error message.
- **Test Cert. Notification History** – the notifications actually sent, with recipient, email address, send time as well as subject and text.
- **Test Certificate Rule Filter List** – an overview of all rule filters across all rules, each with an indication of whether the associated rule is active.

Via the detail information of the test status column on the document lines (chapter 8) and via **Open Source Document** on the Test Certificate Card you navigate between certificate, report and source document.

---

## 11. FAQ and troubleshooting

### 1. Why can't my certificate be released?
Because at least one sample still has the status **Open**. When releasing the certificate, Business Central reports that all existing samples must be released first. Release the samples individually via **Release** or collectively via **Release All Samples** and then repeat the release of the certificate.

### 2. Why can't I reopen a released certificate?
If the option **Certificate Can Be Re-Opened Only by QA User** is enabled in the **Test Certificate Setup**, only a user with the quality assurance right may perform the action **Reopen**. Have the right assigned to you in a test certificate user group or ask a QA user.

### 3. Why can't I post a warehouse receipt/sale?
Because a document line concerns the **Quarantine Location** or a bin marked as quarantine. Such documents may only be posted by users with the quality assurance right. Complete the certificate or have a QA user post it.

### 4. Why is no certificate created automatically, even though a rule exists?
Check three points: The **Rule** must be **active**, the assigned **Test Template** must be active and within the validity period, and the **Rule Filters** must apply to the specific record. If a filter does not apply or the template is inactive, the module skips the rule.

### 5. Why can't a rule be activated?
Because no valid, active **Test Template** is assigned to it. Assign an active template (validity period includes the work date, **Activate Templates** executed). For time-controlled rules with an empty execution time interval, an additional prompt appears.

### 6. Why can I no longer change the data type or reference type in a test characteristic?
Because values or usages already exist for the test characteristic. If characteristics/values already exist, changes to the data type and reference type are blocked, in order to keep existing inspection results consistent.

### 7. Why don't I see all test groups in the sample value grid?
Because the grid only shows the test groups for which you are authorized via your **Test Certificate User Group**. If a group is missing, have yourself authorized via the test group assignment of your user group.

### 8. Why can I no longer edit or reopen a processed sample?
If the setup **Processed Sample Editable** is disabled, the module blocks processed samples against changes. Reopening a processed sample additionally requires the setup **Allow Reopen Processed Samples**.

### 9. Why does my Test Certificate Card say "Different to Default Value Exists"?
Because at least one recorded **Sample Value** deviates from the **default value** of the test template. Check the affected values in the value grid; the deviation is an indication for the quality assessment, not a technical error.

### 10. Why can't I delete an already printed test certificate report?
Because a test certificate report with a **Print Counter** greater than zero may only be deleted by a user with the quality assurance right. This keeps it traceable which reports have already been issued.

---

## 12. Typical use cases

The following examples show the flow from a real trigger through to completion. All pages and actions correspond to the actual behavior of the module.

### 12.1 Goods receipt with inspection (vendor lot)

**Trigger:** A delivery arrives; a goods receipt inspection is required for a purchase order before the inventory may be used freely.

**Entry point in BC:** The user opens the **Warehouse Receipt** for the order. In the warehouse receipt line, the **Test Status** column shows the value **Test** (the certificate was created by a rule) or the user chooses **Open Test Certificate Samples** in the line. Via the detail information of the test status column, they reach the **Test Certificate Card**.

**Core flow:**
1. On the **Test Certificate Card**, check the document data (document type Warehouse Receipt, source type **Vendor**, object Item).
2. Choose **New Sample**; on the **Test Cert. Sample Card**, adopt the **Lot No.** via **Get Serial/Lot No. from Document**.
3. In the value grid, record the **sample values** for each test characteristic.
4. **Release** the sample, then on the Test Certificate Card **Release**.

**Completion:** After release, the **Test Status** of the warehouse receipt line is **Passed**; the quarantine inventory is unblocked if applicable. With the setup enabled, a **Test Certificate Report** is created automatically, which can be output via **Print Report**.

### 12.2 Sales order with test certificate report printout

**Trigger:** A customer requires a test certificate report for the delivery.

**Entry point in BC:** The user opens the **Sales Order**. In the sales line there is the **Test Status** column; via **Open Test Certificate Samples** in the line they open the associated sample or certificate.

**Core flow:**
1. On the **Test Certificate Card**, create the samples (**New Sample** / **Create Multiple Samples**) and record the **sample values**.
2. **Release** the samples and **Release** the certificate.
3. Open the created **Test Certificate Report** (**Test Certificate Management → Reports And Tasks → Test Cert. Report List**), and **Select Sample Values** if required.

**Completion:** Via **Print Report** the test certificate report is printed; via **Send Email** it is sent as a PDF to the customer or the clerk.

### 12.3 Automatic certificate creation via rule

**Trigger:** The quality manager wants a certificate to be created automatically on a certain event (for example the release of a document).

**Entry point in BC:** The administrator opens **Test Certificate Rule List** and creates a **Test Cert. Rule**.

**Core flow:**
1. Choose category and **Test Cetificate Template No.** (active template), set the **Priority**.
2. Record the **Rule Filters** (which records are affected).
3. In the **Event Response**, connect the event with the response "Create Test Certificate", and set **Notify User** if applicable.
4. **Activate Rule**.

**Completion:** When the event occurs, Business Central automatically creates the certificate; the user finds it via the **Test Status** of the document line or under **Test Certificate List** and processes it as in chapter 7.

### 12.4 Certificate for an item from the master data

**Trigger:** A quality inspection is to be performed for a specific lot of an item, without a document being present.

**Entry point in BC:** The user opens the **Item Card** of the item concerned and chooses **Create Item Test Certificate**.

**Core flow:**
1. In the selection dialog, choose the appropriate **Test Template**; the **Test Certificate Card** opens with object type **Item**.
2. Create a **New Sample**, record **Lot No.**/**Serial No.** and enter the **sample values**.
3. **Release** the sample and the certificate.

**Completion:** The certificate is **Released**; if required, proof is printed or sent via the **Test Certificate Report**. The certificate is then traceable in the **Test Certificate List** and in the history.
