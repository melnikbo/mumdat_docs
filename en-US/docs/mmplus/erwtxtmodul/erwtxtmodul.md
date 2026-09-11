---
title: Anwenderhandbuch m+m Erweiterte Texte
---

# User Manual m+m Ext. Text Module

## Introduction

The **m+m Ext. Text Module** extends Microsoft Dynamics 365 Business Central with
**extended document texts**: freely designable, multilingual and rule-based text blocks that are
transferred automatically or at the push of a button into sales, purchase, transfer, production,
warehouse and reminder documents. Instead of manually typing standard texts into every document, you
maintain central **templates**, assign them via a **worksheet** to items, customers, vendors,
locations, work centers or machine centers, and use a **print type** to control whether the text
appears on the report, in the **FactBox**, in the **mail** or in the **mail subject**.

**Target audience.** This manual is aimed primarily at **operational users** who process, print and
email documents every day – sales and purchase clerks, planners, warehouse and production staff.
Secondarily it addresses **administrators and key users** who set up the fundamentals in the
**Extended Text Setup**, the **templates**, the **processes** and the **placeholders**.

**Process overview.** The typical path runs in three stages:

1. **Setup** – in the **Extended Text Setup** the administrator defines the number series, language,
   placeholder characters, mail and report behavior and permissions, and defines **processes**,
   **process groups** and **placeholders**.
2. **Master data** – the key user creates **text templates**, assigns them in the **Extended Text
   Assignment Worksheet** to a **type** (e.g. **Item**, **Customer**, **Work Center**) and, where
   required, maintains **translations**.
3. **Daily work** – in the document the user selects the **print type**, opens the document text page
   via the **Extended Document Text** action, has the texts assembled from the templates and adjusts
   them where needed in the **FactBox**.

## Quick start for users

The order follows the dependency in the code: first setup, then master data, then the document.

**A – One-time setup (administrator).**
1. Open the **Extended Text Setup** page via **Search**.
2. Under **Template Nos.** enter a number series and set the **Language Code**,
   **Placeholder Start Character** and **Placeholder End Character**.
3. Use the **Processes** action to define which reports or pages receive texts, and use the
   **Placeholders** action to define the dynamic fields.
4. In the **User Setup**, allow authorized users to use the **Allow Edit Extended Text** field.

**B – Create and assign a template (key user).**
1. Open **Extended Text Templates** and create a **template** via **New**; enter the
   **Template Text**, **Description**, **Print Type** as well as **Starting Date**/**Ending Date**.
2. In the relevant master card (e.g. **Item Card**) open the **Extended Text** action; the
   **Extended Text Assignment Worksheet** appears.
3. Select **Template No.**, **Type**, **Type No.** and, if applicable, **Sub Type**/**Sub Type No.**
   and thereby assign the template to the master data level.

**C – Generate text in the document (user).**
1. Open the **Sales Order** (or the relevant document) and in the header select the **Print Type**;
   for **Report** additionally select the **Sub-Printing Type**.
2. Choose the **Extended Document Text** action (shortcut **Ctrl+Alt+T**). The **Sales Documents
   Extended Text** page opens and assembles the texts from the templates.
3. Choose the **Create Extended Texts for Documents** action and confirm the desired option (current
   document, recreate all preview types, or all texts without overwriting modified texts).
4. Check the text in the **Extended Text Header** or **Extended Text Line** FactBox; adjust it if
   needed via **Edit**.
5. Print or send the document as usual – the extended text is output according to
   **Print Type**/**Printing Sub Type**.

## Setup

The setup is the densest stage of the module. It comprises the central **Extended Text Setup** card,
the **permissions** in the User Setup, and three self-contained configuration chains: **Set up
processes**, **Set up process groups** and **Set up placeholders**.

### Extended Text Setup

**Process intro.** This card is maintained once per company by the administrator, usually before
first use. It controls the number assignment of templates, the default language, the recognition of
placeholders, the behavior for mail dispatch and report printing, and the automatic text assignment
on posting. **Entry point:** Open the **Extended Text Setup** page via **Search** (global setup, one
record per company; created automatically when opened).

| Setup | Explanation |
|---|---|
| Template Nos. | Number series for new text templates. When set, the template card automatically assigns the next **Template No.** on creation; without an entry the card refuses creation (`TestField "Template Nos."`). |
| Language Code | Default language for generated document texts. When set, it is used as soon as the document itself supplies no language code, and thus determines which **translation** of a template is pulled. |
| Placeholder Start Character | Single character that marks the start of a placeholder. If, for example, "%" is set, the module recognizes everything between the start and end character in the template text as a **placeholder** and replaces it with the field value when the document text is created. |
| Placeholder End Character | Single character that marks the end of a placeholder. When set, together with the start character it delimits the expression to be replaced; without a correct pair the placeholder remains unresolved in the text. |
| Email Placeholders | Controls when placeholders in mail texts are resolved. **Replace Placeholder by Sending:** placeholders are only replaced on dispatch, the stored text stays generic. **Replace by Sending and save:** placeholders are replaced on dispatch and the resolved text is additionally saved. |
| Preferred Email Text | Determines which text is used in the email body. **Use Email Text:** the dedicated mail text is sent. **Use Factbox Text instead of Email Text:** instead, the text maintained in the FactBox is used as the mail body. |
| Preview Texts in Source Documents | When enabled, the document shows additional preview FactBoxes of the target documents (e.g. later posted documents) already in the open document; if the option is empty, only the standard FactBoxes of the current document appear. This option enables the alternative FactBox variants on the sales order. |
| Extended Text Factbox Texts to Report with Printing Sub Type empty | When enabled, FactBox texts without a set **Sub-Printing Type** are not printed on the report; the module points this out when editing ("The extended text will not be printed on the report"). When empty, no such restrictions apply. |
| Copy Text | When enabled, extended texts are also transferred into the target document when a document is copied (copy-document function); if the option is empty, the target document initially remains without extended text. |
| Automatically assign Ext.Text on posting routines | When enabled, on posting the module automatically assigns the matching extended texts so that the posted document (e.g. **Posted Sales Invoice**) already contains the text; without the option, texts must be generated manually. |
| Transfer Rouing Text to Purchase Order | When enabled, the extended text maintained on the operation (routing) is transferred into the purchase document when a purchase order is created; without the option the purchase order text remains empty. |
| Transfer Production Texts on Change Status | When enabled, the extended texts of a production order line are carried over into the new status on a status change (e.g. **Planned** → **Released** → **Finished**); without the option, texts must be recreated in the target status. |

**Background tasks (normally hidden).** The card contains a **Background Tasks** group with the
subgroups **Purchase** and **Sales**, which is hidden by default (`Visible = false`). It controls
whether text generation runs in the background and thus relieves document entry for large documents:

| Setup | Explanation |
|---|---|
| Create Sales Header Text | When enabled, the header text of a sales document is generated as a background task; the document form remains operable in the meantime. |
| Create Sales Line Text | When enabled, the line texts of a sales document are generated in the background. |
| Create Purchase Header Text | When enabled, the header text of a purchase document is generated as a background task. |
| Create Purchase Line Text | When enabled, the line texts of a purchase document are generated in the background. |

From the card you can also reach the follow-up setups via the actions **Create Processes**,
**Processes** and **Placeholders** (see the following sections).

### Set up permissions for text editing

**Process intro.** Who may change extended texts directly in the FactBox of a document is controlled
via the **User Setup**. This authorization is a prerequisite for the **Edit** action in daily work
(see the chapter **Daily work on the document**). **Entry point:** Open the **User Setup** via
**Search** and select the user's line.

1. **First** open the **User Setup** and mark the user line.
2. **Then** set the **Allow Edit Extended Text** field.

| Setup | Explanation |
|---|---|
| Allow Edit Extended Text | Determines the permission for text editing. When set, the user may run the **Edit** action in the **Extended Text Header**/**Extended Text Line** FactBoxes; if the field is empty, the module aborts editing with an error message and the user can only view the text (**Enlarge**). |

**Operational conclusion.** In daily work, the **Edit** action in the text FactBoxes checks this
permission before the editor is opened (cross-reference: **Daily work on the document**).

### Set up processes

**Process intro.** A **process** connects a **print type** with a specific output object – a
**report** or a **page** – and thereby defines for which output a text is intended. Processes are
maintained by the administrator before templates are assigned, and are selected in the **Extended
Text Assignment Worksheet**. **Entry point:** In the **Extended Text Setup** open the **Processes**
action; alternatively reachable via **Search** → **Extended Text Processes**.

1. **First** choose the **Create Processes** action in the **Extended Text Setup** to create the
   standard processes.
2. **Then** in **Extended Text Processes** add **Code**, **Print Type**, **Object Type** and
   **Object No.** per line.
3. **Finally** assign the process to a template in the worksheet (cross-reference: **Master data
   → Assignment**).

| Field | Explanation |
|---|---|
| Code | Unique key of the process (number series via **No. Series**). When set, the assignment references exactly this process. |
| Print Type | Determines the output kind. **FactBox:** text appears in the document's FactBox. **Report:** text is printed on the assigned report. **Mail:** text forms the email body. **Mail Subject:** text forms the subject of the email. |
| Description | Plain-text designation of the process for orientation in the list. |
| Object Type | Defines what the process refers to. **Report:** a Report object. **Page:** a Page object. For **Page**, only the print types **FactBox** or **Mail** are allowed; otherwise the module reports "Only FactBox or Mail is allowed as a print type if Object Type is Page." |
| Object No. | Number of the report or page. When set, the lookup checks whether the object is available; unknown objects are rejected with a message. |
| Object Name | Shows the name for the selected object number (not editable, serves for control). |
| Process Assignements | Shows in how many assignments this process is already used. |

Via the **Process Report Assignement** action (active only for **Print Type** = **Report**) you
check which reports the process is assigned to.

### Set up process groups

**Process intro.** A **process group** bundles several process objects under a common **Process Print
Type**, so that a template applies to several output objects in one step. Process groups are a
self-contained configuration chain alongside the individual processes and are selected in the
worksheet via the **Process Group** field. **Entry point:** Open the **Extended Text Process Group
List** via **Search** and, within it, the **Extended Text Process Group Card**.

1. **First** create a group in the **Extended Text Process Group List** with **Code**,
   **Description** and **Process Print Type**.
2. **Then** enter the associated process objects in the **Extended Text Process Group Lines**.
3. **Finally** select the process group for a template in the worksheet.

| Field | Explanation |
|---|---|
| Code | Unique key of the process group. When set, the assignment references this group. |
| Description | Plain-text designation of the group. |
| Process Print Type | Common output kind of all group lines (**FactBox**, **Report**, **Mail**, **Mail Subject**). If lines already exist, the print type can no longer be changed; the module reports "Cannot change Process Print Type because there are existing lines for this Process Group." |

Per group line (**Extended Text Process Group Line**), **Process**, **Process Group Code**,
**Process Object Type** (**Report**/**Page**), **Process Object ID** and **Process Object Name** are
maintained; they assign the individual output objects to the group.

### Set up placeholders

**Process intro.** **Placeholders** make template texts dynamic: when a document text is created, the
module replaces a placeholder with a field value, a linked table value, a system value (e.g.
**Today Date**) or a picture. Placeholders are defined by the administrator before template
maintenance and are used in the template texts between the **Placeholder Start Character** and
**Placeholder End Character**. **Entry point:** In the **Extended Text Setup** open the
**Placeholders** action; alternatively via **Search** → **Placeholders List**.

| Field | Explanation |
|---|---|
| Placeholders | The text you use in the template text. When set, every occurrence between the start and end character is replaced when the document text is created. |
| System Procedures | Defines that a system value is inserted instead of a field value. **(empty):** no system value, the field/table assignment applies. **Today Date:** current date. **Current Time:** current time. **Work Date:** BC work date. **User ID:** logged-in user. |
| Table Id | Table from which the field value originates (editable when no **System Procedure** is selected). |
| Table Name | Shows the name for the **Table Id** (control). |
| Field No. | Field number within the table whose value is inserted. |
| Field Name | Shows the name for the **Field No.** (control). |
| Related Table | For linked values: the table that is referred on to (editable when a **System Procedure** is selected). |
| Related Table Field | Field number in the related table whose value is pulled. |
| Related Field Name | Shows the name for the related table field. |
| Free Text | Fixed text that is inserted (editable when no **System Procedure** is selected). When filled, the placeholder is replaced by this constant text. |
| Picture | Picture that the placeholder inserts (for print type **Report**). |
| Resize % | When set, the picture is scaled by a percentage before output. |
| Height / Width | Target height or width of the inserted picture. |

For each picture placeholder, the **Picture** FactBox shows the stored picture; via the picture page
you can **Import**, **Export**, **Delete** the picture or **Reload Picture as Original**.

## Master data

Master data maintenance comprises the **text templates**, their **assignment** via the worksheet, as
well as the **translations**. All master-data-related cards (Item, Customer, Vendor, Item Variants,
Item References, Serial and Lot No. Information Card, Work Center, Machine Center) integrate the same
entry point **Extended Text** and lead into the **Extended Text Assignment Worksheet**.

### Text templates

**Process intro.** A **template** is the reusable text block. The key user maintains templates before
assignment; each template carries a **print type** and a temporal validity. **Entry point:** Open
the **Extended Text Templates** via **Search** and, via a line within it, the **Extended Text
Template Card**. When opened, the list shows only templates whose **Starting Date**/**Ending Date**
includes the current date.

| Field | Explanation |
|---|---|
| Template No. | Unique number of the template. If **Template Nos.** is set in the setup, the number is assigned automatically on creation. |
| Template Text | Short designation/heading of the template. |
| Description | Explanatory designation for orientation in the list and the assignment. |
| Print Type | Determines the output kind of the template. **FactBox:** display in the document FactBox. **Report:** print on the report (additionally shows **Sub-Printing Type**). **Mail:** email body. **Mail Subject:** email subject. |
| Starting Date | Start of validity. When set, the template appears in the list only from this date; must not be greater than the **Ending Date**. |
| Ending Date | End of validity. When set, the template is hidden from the following day; must not be less than the **Starting Date**. |
| Assignment Worksheet | When enabled, the template is offered for assignment in the **Extended Text Assignment Worksheet**. |
| Translation Exists | Shows whether **translations** in other languages are already maintained for this template. |
| Sub-Printing Type | Visible only for **Print Type** = **Report**. Defines the print position: **Header**, **Footer**, **Before Position**, **After Position**. |
| Legacy Data | Marks templates carried over from legacy stock (not editable); serves to distinguish migrated data. |

Via the **Copy Template** action you create a new template from an existing one; via **Translation**
you reach the language maintenance. The template text itself is maintained in the **Template Text**
FactBox in the **Text Editor**.

### Assignment in the Extended Text Assignment Worksheet

**Process intro.** The worksheet is the central place where templates are bound to master data. The
key user calls it from the relevant master card via the **Extended Text** action; the assignment
decides which template is later pulled into which document (cross-reference: **Daily work on the
document**). **Entry point:** In the **Item Card** (or **Customer Card**, **Vendor Card**, **Work
Center Card**, **Machine Center Card** …) open the **Extended Text** action.

| Field | Explanation |
|---|---|
| Template No. | The **template** to be assigned. When set, its text is pulled for a matching document. |
| Print Type | Output kind of the assignment; editable when **Template No.** is empty. **FactBox**/**Report**/**Mail**/**Mail Subject** as with the template. If a process is set, the print type must match the process print type; before a change, the **Process** field must be cleared. |
| Type | Master data level of the assignment. **All Customers/Customer/Customer Group**, **All Vendors/Vendor/Vendor Group**, **Location/All Locations**, **Routings/All Routings**. Defines for which document origin the template applies. |
| Type No. | Concrete key for the **Type** (e.g. customer no.). Empty for "All …"; for a wrong combination the module reports "Field … is not allowed with choosen type!". |
| Sub Type | Finer item/capacity level: **All Items/Item/Item Category**, **Work Center/All Work Center**, **Machine Center/All Machine Center**, **Ship-to Code**. **Ship-to Code** is allowed only when a secondary print type is set. |
| Sub Type No. | Concrete key for the **Sub Type** (e.g. item no., item category code). |
| Process Group | Optional binding to a **process group**; the lookup filters by the matching **Process Print Type**. |
| Process | Optional binding to an individual **process**; the lookup filters by the print type of the assignment. You must choose **Process Group** or **Process**, otherwise the module reports "You have to choose … OR … if you want to assign process!". |
| Process Object Name | Shows the name of the selected process object (not editable, control). |
| Legacy Data | Marks migrated assignments (not editable). |

In the worksheet you see the **Texts** (template text) and **Translation Texts** FactBoxes. Actions:
**Show related lines** (shows the associated combined lines), **Template Card**, **Translation**,
**Placeholders** as well as the batch functions under **Import/Export** and **Update** (see the
chapter **Import/Export and mass update**).

### Translations

**Process intro.** For each template you can maintain language-dependent versions. The key user calls
the translation from the template card, the template list or the worksheet; when the document text is
created, the module pulls the version matching the document's language code or the default language
from the setup. **Entry point:** In the **Extended Text Template Card** open the **Translation**
action; the **Extended Text Translations** page appears.

| Field | Explanation |
|---|---|
| Language Code | Language of the translation. When set, this version text is pulled as soon as the document carries this language code. |
| Description | Header/short text of the translated version. |
| Language Name | Shows the plain name for the **Language Code** (control). |

The actual translation text is entered in the **Texts** FactBox in the **Text Editor**.

## Daily work on the document

On the open document (described representatively on the **Sales Order**), the module adds two control
fields, several text FactBoxes and the **Extended Document Text** action in the header. The texts
visible here come from the **templates** and **assignments** (chapter **Master data**); whether and
where they are printed or mailed is determined by **Print Type**/**Printing Sub Type**.

**Setup reference.** Which templates apply is controlled by the administrator via **Extended Text
Setup** (language, placeholders, auto-assignment on posting, preview behavior) and via the
**assignment** in the worksheet; the editing rights come from the **User Setup**
(**Allow Edit Extended Text**).

### Header fields Print Type and Sub-Printing Type

| Field | Explanation |
|---|---|
| Print Type | Output kind of the extended text for this document. **FactBox:** on-screen display only. **Report:** print on the document. **Mail:** email body. **Mail Subject:** email subject. A change immediately updates the text FactBoxes. |
| Sub-Printing Type | Visible only for **Print Type** = **Report**. Determines the print position: **Header**, **Footer**, **Before Position**, **After Position**. |

On posted and further documents, the corresponding header field is called **Printing Sub Type** (same
values); it documents the print position used at posting.

### Extended Text Header and Extended Text Line (FactBox)

The **Extended Text Header** FactBox shows the header text, **Extended Text Line** the line text for
the marked document line. Both offer the same actions:

- **Edit** (Ctrl+Shift+H): Opens the **Text Editor** for changing. The module first checks the
  permission (**Allow Edit Extended Text**); if it is missing, an error message appears and the text
  remains unchanged.
- **Update**: Confirm the **"Do you want to update document texts from Templates"** dialog to
  reassemble the text from the current templates. If a template was changed after text creation
  (**Template Updated**), a notification points this out.
- **Enlarge**: Opens the text read-only in a large view.

### Extended Document Text action

The **Extended Document Text** action (Ctrl+Alt+T) opens the **Sales Documents Extended Text** page.
When opened, it automatically assembles the texts of all relevant follow-up and preview document
types (e.g. **Order** → **Posted Sales Invoice**, **Posted Sales Shipment**, **Released**,
**Warehouse Shipment**).

| Field | Explanation |
|---|---|
| Print Type | Output kind for the preview; controls which text version is shown in the FactBoxes. |
| Sub-Printing Type | Visible only for **Print Type** = **Report**; print position of the preview. |
| Document Type | Target document kind of the respective line (e.g. **Order**, **Posted Sales Invoice**). If the **Document Type** matches the **Source Document Type**, the line is highlighted. |
| No. | Document number for the respective document type. |

In the **Lines** subform you see the line-related texts. Via the **Create Extended Texts for
Documents** action you choose one of the options via a selection dialog: create/update extended text
only for the current document and type, recreate all preview document types, or update all texts
without overwriting already modified texts.

## Further document areas

The pattern of header fields (**Print Type**/**Printing Sub Type**), text FactBoxes and the
**Extended Document Text** action repeats in further document areas. The underlying templates and
assignments are the same (chapter **Master data**); only the document kind changes.

- **Purchase.** Order, Quote, Blanket Order, Return Order, Purchase Invoice and Credit Memo carry the
  **Extended Document Text** action and open **Purchase Documents Extended Text**. Via the
  **Transfer Rouing Text to Purchase Order** setting, the routing text can flow automatically into
  the purchase order.
- **Transfer.** The **Transfer Order** opens **Transfer Documents Extended Text**; posted documents
  are called **Posted Transfer Shipment** and **Posted Transfer Receipt**.
- **Production.** Production orders in the statuses **Simulated**, **Planned**, **Firm Planned**,
  **Released** and **Finished** open **Production Extended Text**. When the **Transfer Production
  Texts on Change Status** setting is active, the texts are carried over on a status change;
  production orders created from a sales order take over the line texts.
- **Warehouse.** Warehouse Receipt, Warehouse Shipment, **Warehouse Pick** and **Warehouse Put-away**
  as well as their registered and posted documents carry the text FactBoxes and the header fields
  **Print Type**/**Printing Sub Type**.
- **Reminders.** Reminder and **Issued Reminder** carry **Print Type**/**Printing Sub Type** and the
  text actions; the text can be printed as a **Report** or sent via **Mail**.
- **Archive and posted documents.** Archived documents (e.g. archived sales order) and posted
  documents (e.g. **Posted Sales Invoice**, **Posted Sales Shipment**) show the extended text valid
  at the time of posting or archiving read-only in the FactBoxes as well as via the actions
  **Extended Text**, **Factbox**, **Report** and **Mail**.

## Output: Report, Mail and FactBox

Whether and how an extended text is output is decided by the **Print Type** of the template or the
document:

- **FactBox:** The text appears exclusively on screen in the document's text FactBoxes.
- **Report:** The text is printed on the report; the position is controlled by the **Sub-Printing
  Type** (**Header**, **Footer**, **Before Position**, **After Position**). If the setup option
  **Extended Text Factbox Texts to Report with Printing Sub Type empty** is active, FactBox texts
  without a secondary print type are not printed.
- **Mail:** The text forms the email body; **Mail Subject** supplies the subject. Via **Preferred
  Email Text** you define whether your own mail text or the FactBox text is used, and via **Email
  Placeholders** when placeholders are replaced on dispatch.

On posted documents, the actions **Extended Text**, **Factbox**, **Report** and **Mail** are
available for this; the subgroups **Header**, **Footer**, **Before position**, **After position** and
**Default** select the print position.

## Import/Export and mass update

From the **Extended Text Assignment Worksheet**, batch functions are available:

- **Export Excel Template** / **Import Excel Template**: Export or re-import the template structure as
  an Excel file.
- **Export Excel Ext. Text**: Export the filtered assignments as Excel data.
- **Delete Legacy Ext. Text**: Remove legacy texts marked as **Legacy Data**.
- **Update All Document Texts**: Triggers the recalculation of all document texts in the background
  (confirmation "Task has been run successfully in background!").
- **Update Notifications in All Document**: Checks in the background whether templates were changed
  after text creation and generates corresponding notifications.

## FAQ and Troubleshooting

### 1. Why can't I create a new template?
Because no **Template Nos.** is stored in the **Extended Text Setup**. The template card checks this
field and refuses creation without a number series. Enter a number series.

### 2. Why is my template text not replaced in the document (placeholder remains)?
The placeholder is only replaced if it stands exactly between the **Placeholder Start Character** and
**Placeholder End Character** and is defined in the **Placeholders List**. Check the spelling and the
set start/end characters in the setup.

### 3. Why am I not allowed to edit the text in the FactBox?
The **Edit** action requires the **Allow Edit Extended Text** field to be set in the **User Setup**.
Without this permission an error message appears; you can only view the text via **Enlarge**.

### 4. Why can't I choose print type "Report" for object type "Page"?
For a **process** with **Object Type** = **Page**, only the print types **FactBox** or **Mail** are
allowed. The module reports "Only FactBox or Mail is allowed as a print type if Object Type is Page."
For report printing choose **Object Type** = **Report**.

### 5. Why can the Process Print Type of a process group no longer be changed?
As soon as the process group contains **lines**, the **Process Print Type** is locked so that the
lines stay consistent. Delete the lines first, or create a new group.

### 6. Why does an assignment not appear even though I chose a process?
You must set either **Process Group** or **Process**. If both are missing, the module reports "You
have to choose … OR … if you want to assign process!" and the assignment is incomplete.

### 7. Why is the extended text not transferred into the posted document after posting?
The automatic transfer is controlled by the **Automatically assign Ext.Text on posting routines**
setting. If it is empty, you must generate the texts for the posted document manually via **Create
Extended Texts for Documents**.

### 8. Why does a "Template Updated" notification appear on the document?
Because the underlying template was changed after text creation (**Template Updated** field). Choose
**Update** in the FactBox and confirm the dialog to re-pull the document text from the template.

### 9. Why is a FactBox text not printed on the report?
If the setup option **Extended Text Factbox Texts to Report with Printing Sub Type empty** is active,
FactBox texts without a set **Sub-Printing Type** are not printed. Set a secondary print type or
disable the option.

### 10. Why don't I see a template in the list even though it exists?
When opened, the **Extended Text Templates** shows only templates whose **Starting Date**/**Ending
Date** includes today's date. If today's date lies outside the validity, the template is hidden.

## Typical use cases

### Usage example 1: Printing a standard condition on a sales order

**Trigger.** A customer orders by phone; the sales clerk is to add a fixed delivery condition as a
footer text on the report of the order.

**Entry point in BC.** The user opens the **Sales Order** and marks the document.

**Core flow.**
1. In the header, the user sets **Print Type** = **Report** and **Sub-Printing Type** = **Footer**.
2. He chooses the **Extended Document Text** action (Ctrl+Alt+T); the **Sales Documents Extended
   Text** page opens and assembles the texts automatically.
3. He chooses **Create Extended Texts for Documents** and confirms the "current document and type"
   option.
4. In the **Extended Text Header** FactBox he checks the text; if something is missing, he adds it
   via **Edit** (permission required).

**Conclusion.** The document is printed as usual; the extended text appears as a **Footer** on the
report. The assigned template comes from the **Extended Text Assignment Worksheet**.

### Usage example 2: Maintaining a recurring item text centrally

**Trigger.** For an item group, a maintenance note is to automatically appear in every sales document
from now on.

**Entry point in BC.** The key user opens the **Extended Text Templates** and creates a new
**template** with **Print Type** = **Report**.

**Core flow.**
1. In the template card he enters the note in the **Text Editor** and sets **Starting Date**/**Ending
   Date**.
2. He opens the **Item Card** of an affected item and chooses the **Extended Text** action.
3. In the **Extended Text Assignment Worksheet** he sets **Template No.**, **Type** = **Item** (or
   **Item Category** for the whole group) and **Sub Type**/**Sub Type No.**.
4. Via **Show related lines** he checks the combined result.

**Conclusion.** From now on, every matching sales document automatically pulls the note into the line
texts; the user no longer has to enter anything manually.

### Usage example 3: Foreign-language version for export customers

**Trigger.** An export customer receives documents in another language; the existing German template
text is to be translated.

**Entry point in BC.** The key user opens the **Extended Text Template Card** of the affected
template.

**Core flow.**
1. He chooses the **Translation** action; the **Extended Text Translations** page appears.
2. He creates a line with the matching **Language Code** and enters the translated text in the
   **Text Editor**.
3. The template's **Translation Exists** field now shows the existing translation.

**Conclusion.** If the document carries the corresponding language code – or if it is stored as the
**Language Code** in the **Extended Text Setup** – the module automatically pulls the translated
version when the document text is created.
