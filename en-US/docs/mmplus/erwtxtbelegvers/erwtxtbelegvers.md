---
title: Anwenderhandbuch m+m Ext. Text Module with Report Dispatch
---

# User Guide m+m Ext. Text Module with Report Dispatch

## Introduction

The **m+m Ext. Text Module with Report Dispatch** module connects two existing m+m modules
with each other: the **Ext. Text Module** (placeholder management) and **Report Dispatch**
(email and attachment dispatch). It does not provide any pages of its own, but instead extends the
existing placeholder management with two new **system procedures** — **Attachments** and **Attachment
List** — and ensures that these placeholders are automatically replaced by the names of the actually
attached files when emails are sent through Report Dispatch.

The benefit for the user: When an email is sent through an **m+m Document Send. Profiles**, a
placeholder can be entered in the **Subject** or in the message body that is replaced by the concrete
list of attachments at the moment of sending. This lets the recipient see directly in the email which
files are attached — if required, even as a formatted list with the respective file size.

**Target audience.** The primary audience are **operational users** who send documents by email in
day-to-day business (sales and purchasing clerks who work via **Print/Send**). The secondary audience
are **administrators or key users** who set up the placeholders and the placeholder start/end
characters once.

**Short process overview.** The workflow is divided into three sections that build on each other in
this order:

1. **Setup** — in the **Extended Text Setup** the administrator defines the **Placeholder Start
   Character** and the **Placeholder End Character** and defines a placeholder with the system
   procedure **Attachments** or **Attachment List** in the **Placeholders List**.
2. **Use** — the user inserts this placeholder into the email text (or into a template text that is
   used as the email text) and sends the document through an **m+m Document Send. Profiles** with the
   **Type** **E-Mail**.
3. **Result** — when sending, the module replaces the placeholder with the names of the attachments.

## Quick Start for Users

The quick start describes the shortest path from an empty state to the finished email in which the
attachments are named automatically. The setup is a prerequisite and therefore comes first.

1. **Check the start and end characters.** Open the **Extended Text Setup** page via **Search** and
   make sure that the **Placeholder Start Character** and **Placeholder End Character** are filled
   (e.g. `{` and `}`). Without these two characters no replacement takes place.
2. **Create a placeholder.** In the **Extended Text Setup**, open the **Placeholders List** page via
   the **Placeholders** action. Create a new line, enter a meaningful name in the **Placeholder**
   field (e.g. `Anhaenge`) and select the value **Attachments** or **Attachment List** in the **System
   Procedures** column.
3. **Insert the placeholder into the email text.** Write the placeholder — framed by the start and end
   characters (e.g. `{Anhaenge}`) — into the **Subject** or the message body of the email or into the
   template text being used.
4. **Prepare the document sending profile.** Create a profile with **Type** = **E-Mail** and the
   matching **Document Type** via **Search** in **m+m Document Send. Profiles** (or via the
   customer/vendor card, action **m+m Document Sending Profile**). Use **No. Of Attachments** to store
   the additional files.
5. **Send the document.** Open the document and start **Print/Send**. When the email is created, the
   module replaces the placeholder with the names of the attachments; check the subject and message
   body before sending.

## Setup

The setup is performed in "Microsoft Dynamics 365 Business Central". It consists of two consecutive
steps: defining the placeholder characters on the central setup page and creating the actual
placeholders. Since the module itself does not come with its own setup page, you use the pages of the
Ext. Text Module; the two new values **Attachments** and **Attachment List** appear there
automatically as soon as this module is installed.

### Extended Text Setup

**Process intro.** The **Extended Text Setup** is a company-wide setup (exactly one record per
company). It is maintained once by the administrator before first use. For this module, the fields
**Placeholder Start Character** and **Placeholder End Character** are especially decisive, because they
define at which characters the module recognizes a placeholder in the text. The remaining fields
control the Ext. Text Module as a whole and are described here in full, because the user sees exactly
this one page.

**Entry point:** Open the page via **Search** and the page title **Extended Text Setup** (company-wide
setup without a superordinate list).

| Setup | Explanation |
|-------------|-------------|
| **Template Nos.** | If you store a number series here, then new template texts are automatically assigned a number from this series; without an entry, numbers must be assigned manually. |
| **Language Code** | If you set a language code, then texts are created or preferred in the corresponding language; without an entry, the company's default language applies. |
| **Placeholder Start Character** | Defines the leading character of a placeholder (length 1). If this character is empty, then **no** placeholder replacement takes place — the **Attachments** and **Attachment List** system procedures are then not resolved either. |
| **Placeholder End Character** | Defines the closing character of a placeholder (length 1). If this character is empty, then placeholders are not recognized and not replaced. Only when both the start **and** end characters are filled does the module replace a text of the form start character + placeholder name + end character. |
| **Email Placeholders** | Controls when placeholders in email texts are processed. **(empty):** no automatic email placeholder processing. **Replace Placeholder by Sending:** If set, then placeholders are replaced when the email is sent; the stored text remains unchanged. **Replace by Sending and save:** If set, then the replaced text is additionally saved on the document. |
| **Preferred Email Text** | Determines which text is used as the email text. **Use Email Text:** If set, then the regular email text is used. **Use Factbox Text instead of Email Text:** If set, then the factbox text of the extended texts is used as the email text. |
| **Preview Texts in Source Documents** | If enabled, then the extended texts are already shown as a preview in the source document, so that the user sees the result before posting or dispatch. |
| **extended text factbox texts in report with print subtype empty** | If enabled, then factbox texts are printed in the report even when no print subtype is set; otherwise these texts remain limited to the report without a subtype. |
| **Copy Text** (group **Copy Documents**) | If enabled, then extended texts are copied over into the target document when a document is copied; otherwise the target document starts without these texts. |
| **Assign Ext. Text automatically during posting routines** | If enabled, then extended texts are automatically assigned to the posted document during posting, without the user having to intervene manually. |
| **Transfer routing text to purchase order** | If enabled, then the routing text is transferred to a purchase order when it is created; otherwise the text stays on the source document. |
| **Adopt production order texts on status change** | If enabled, then production order texts are adopted automatically on status change; otherwise they have to be assigned again. |

> Note: The **Background Tasks** group (creating header and line texts in the background for purchasing
> and sales) is hidden in the standard view and is not relevant for the daily handling of this module;
> it is therefore not listed here as a control.

### Setting up a placeholder for attachments

**Process intro.** So that the email shows the attachment names when sent, the administrator has to
create a placeholder and assign it the correct system procedure. Who configures: the administrator or
key user. When: once before first use, after setting the start/end characters. Where it is applied: in
day-to-day business when sending through an **m+m Document Send. Profiles** (see **Daily Work: Sending
Documents by Email**).

Perform the steps in this order:

1. **Ensure the characters.** In the **Extended Text Setup**, check that the **Placeholder Start
   Character** and **Placeholder End Character** are filled. If one of the two characters is empty,
   then the placeholder is not replaced later.
2. **Open the Placeholders List.** In the **Extended Text Setup**, open the **Placeholders List** page
   via the **Placeholders** action.
3. **Create a placeholder.** Create a new line and assign a name in the **Placeholder** field. This
   name is the text that you later write — framed by the start and end characters — into the email
   text.
4. **Choose the system procedure.** Set the **System Procedures** column to **Attachments** (simple
   enumeration of the file names) or to **Attachment List** (formatted list with file size). If you
   choose one of these two system procedures, then the fields for table/field are not needed; the
   module provides the replacement when sending.
5. **Operational conclusion.** Insert the placeholder into the email text and send a document via
   **Print/Send** with a document sending profile of **Type** **E-Mail** — see **Daily Work: Sending
   Documents by Email**.

## Master Data

### Placeholders List

**Process intro.** The **Placeholders List** is the central master record of the Ext. Text Module.
Here the administrator defines which placeholders are permitted in the text and by what they are
replaced. This module extends the selection of the **System Procedures** column with the values
**Attachments** and **Attachment List**. The list is opened via the **Placeholders** action from the
**Extended Text Setup**.

**Entry point:** **Extended Text Setup** → **Placeholders** action → **Placeholders List** page.

| Field | Explanation |
|------|-------------|
| **Placeholder** | The name of the placeholder. If you write this name — framed by the start and end characters — into a text, then the module replaces the character string with the determined value. The name is a mandatory field. |
| **System Procedures** | Determines by what the placeholder is replaced. Values: **(empty):** no system procedure — the replacement is governed by table/field or free text. **User ID:** If chosen, then the placeholder is replaced by the user ID of the logged-in user. **Today Date:** If chosen, then the current date is inserted. **Work Date:** If chosen, then the work date set in BC is inserted. **Current Time:** If chosen, then the current time is inserted. **Attachments:** If chosen, then the placeholder is replaced by the comma-separated names of all attachments when the email is sent. **Attachment List:** If chosen, then the placeholder is replaced by a formatted list of the attachments in which the size in MB is additionally shown for each file. |
| **Table ID** | If no system procedure is chosen, then this field determines the source table from which the replacement value is read. It is not needed for the **Attachments** and **Attachment List** system procedures. |
| **Table Name** | Shows the name of the table chosen via **Table ID** (not editable). |
| **Field No.** | If no system procedure is chosen, then this field determines the field number in the source table whose value is inserted. |
| **Field Name** | Shows the name of the field chosen via **Field No.** (not editable). |
| **Related Table** | If a system procedure other than (empty) is chosen, then a linked table whose value is used instead can be specified here. |
| **Related Table Field** | Determines the field number in the related table whose value is inserted. |
| **Related Field Name** | Shows the name of the related field (not editable). |
| **Free Text** | If you enter a text here, then the placeholder is replaced by this fixed text; the entries for table, field and picture are reset in the process. |
| **Picture** | If you store a picture, then the placeholder is replaced by this picture (e.g. for reports). |
| **Resize %** | If you set a percentage value, then the stored picture is scaled proportionally (value range −99 to 99). |
| **Height** | If you set a value, then the picture is scaled to the specified height. |
| **Width** | If you set a value, then the picture is scaled to the specified width. |
| **Picture** (factbox) | Shows a preview of the picture stored for the placeholder in the factbox. |

> For this module, only the values **Attachments** and **Attachment List** of the **System Procedures**
> column are relevant. For these two values, the module provides the replacement text itself when
> sending; the fields for table, field, free text and picture remain empty.

## Daily Work: Sending Documents by Email

**Setup reference (bridge paragraph).** The daily workflow is controlled by two setup areas: by the
**Extended Text Setup** and the **Placeholders List** (which placeholder exists and that the start/end
characters are set) as well as by the **m+m Document Send. Profiles** of Report Dispatch (whether
sending happens by **E-Mail** at all and whether and how it is **zipped**). Once the setup has been
performed as described under **Setup** and **Master Data**, in day-to-day business the user only has
to insert the placeholder into the text and send the document.

**Workflow.** The module does not intervene in the interface as a button, but works automatically at
the moment of email dispatch. The workflow is:

1. The user opens the document (e.g. a **Sales Order** or a posted document) and starts the dispatch
   via **Print/Send**. A matching **m+m Document Send. Profiles** with the **Type** **E-Mail** or
   **Print & E-Mail** is a prerequisite.
2. Report Dispatch creates the email, attaches the document and additional files and — depending on
   the **ZIP Option** (**All**, **Just Attachments** or without ZIP) — forms a ZIP folder if
   applicable.
3. Immediately before sending, this module processes the email subject and the message body: It
   collects the names of all attachments. If it is a ZIP attachment, the names of the files **inside**
   the ZIP folder are additionally determined.
4. Every placeholder with the system procedure **Attachments** is replaced by the comma-separated list
   of file names. Every placeholder with the system procedure **Attachment List** is replaced by an
   HTML enumeration in which the size in MB — rounded to two decimal places — is shown in brackets for
   each file, provided it is larger than 0 MB.
5. Report Dispatch sends the email with the subject and message body prepared in this way. Before
   sending, the user can still check and manually adjust the recipients, **Subject**, message body and
   attachments.

> Prerequisite for the replacement: In the **Extended Text Setup**, the **Placeholder Start Character**
> and **Placeholder End Character** must be filled. If they are empty, Report Dispatch sends the email
> unchanged — the placeholder would remain as text.

### Attachments and Attachment List compared

Both system procedures refer to the same attachments, but differ in the presentation in the email
text:

| System procedure | Result in the text |
|----------------|------------------|
| **Attachments** | A single-line, comma-separated enumeration of the file names (e.g. `Angebot.pdf, AGB.pdf`). Suitable for the **Subject** or a short sentence in the message body. |
| **Attachment List** | A formatted enumeration (HTML list). For each file larger than 0 MB the size in MB is additionally shown (e.g. `AGB.pdf (0.12 MB)`); files without a determinable size appear without an MB indication. Suitable for the message body when the recipient should see the attachments listed clearly. |

## Typical Use Cases

### Use case 1: Naming attachments in the email text

- **Trigger.** A clerk sends an order confirmation to which, in addition to the document, the general
  terms and conditions are attached as an additional file. The recipient should already see in the
  email text which files are attached.
- **Preparation (one-time).** In the **Extended Text Setup**, the **Placeholder Start Character** and
  **Placeholder End Character** are set. In the **Placeholders List** a placeholder exists (e.g.
  `Anhaenge`) with **System Procedures** = **Attachments**. The placeholder `{Anhaenge}` is in the
  message body or in the template text being used.
- **Entry point in BC.** The clerk opens the **Sales Order** and chooses **Print/Send**. The
  associated **m+m Document Send. Profiles** has the **Type** **E-Mail** and the matching **Document
  Type**; the additional file is stored via **No. Of Attachments**.
- **Core workflow.** When the email is created, the module replaces `{Anhaenge}` with the file names of
  the attachments (document and additional file). The clerk checks the subject and message body.
- **Conclusion.** The email is sent; the message body names the attached files by name.

### Use case 2: Attachment list with size indication for ZIP dispatch

- **Trigger.** For a customer, several files are regularly sent bundled together. So that the email
  does not become too large, the attachments should be sent as a ZIP folder, and the recipient should
  see in the text what they are receiving.
- **Preparation (one-time).** In the **Placeholders List** a placeholder exists (e.g. `Anhangsliste`)
  with **System Procedures** = **Attachment List**. The placeholder is in the message body. The **m+m
  Document Send. Profiles** has **Type** = **E-Mail** and **ZIP Option** = **All**; optionally, **Max.
  MB** limits the total size.
- **Entry point in BC.** The user opens the document and starts **Print/Send**.
- **Core workflow.** Report Dispatch packs the attachments into a ZIP folder according to the **ZIP
  Option**. The module reads the names of the files inside the ZIP folder and replaces the placeholder
  with a formatted list in which the size in MB is shown for each file larger than 0 MB.
- **Conclusion.** The email is sent with the ZIP attachment and the readable attachment list in the
  message body.

## FAQ and Troubleshooting

### Why is my placeholder not replaced in the email text?

Most likely the placeholder characters are missing. In the **Extended Text Setup**, check whether the
**Placeholder Start Character** and **Placeholder End Character** are filled. If one of the two
characters is empty, the module does not process any placeholder and the text remains unchanged.

### How do I have to write the placeholder in the text?

Write the name assigned in the **Placeholders List** and frame it exactly with the **Placeholder Start
Character** and the **Placeholder End Character** (e.g. `{Anhaenge}`). Only this exact character string
is recognized and replaced.

### What is the difference between Attachments and Attachment List?

**Attachments** replaces the placeholder with a single-line, comma-separated enumeration of the file
names. **Attachment List** replaces it with a formatted enumeration in which the size in MB is
additionally shown for each file larger than 0 MB.

### Why is there no MB indication for some files in the Attachment List?

The size is only shown if it is larger than 0 MB. If the determined size is 0 (or not available), the
**Attachment List** lists the file only with the name and without a size indication.

### Does the replacement also work in the subject of the email?

Yes. The module processes both the **Subject** and the message body. For the subject, the system
procedure **Attachments** (compact enumeration) is more suitable than the **Attachment List**, which is
intended for the body.

### Are the files inside a ZIP folder listed as well?

Yes. If an attachment is a ZIP folder, the module reads the names of the files it contains and includes
these in the replacement. This way the recipient sees the individual files and not just the name of the
ZIP folder.

### Do I have to press a special button of the module to send?

No. The module works automatically at the moment of email dispatch through Report Dispatch. You send
the document as usual via **Print/Send** with an **m+m Document Send. Profiles** of the **Type**
**E-Mail**; the replacement happens in the background.

### Why does nothing happen even though I have created a placeholder?

The replacement only takes effect for **email dispatch**. If the **Type** of the document sending
profile is set to **Print**, no email is created and the placeholder is not processed. Choose **E-Mail**
or **Print & E-Mail**.

### Where do I define which additional files are attached at all?

The attachments themselves are not defined in this module, but in the **m+m Document Send. Profiles**
via **No. Of Attachments**. The module afterwards only names the files that Report Dispatch has actually
attached to the email.

### Can I still check the replaced text before sending?

Yes. Before sending, you can check and, if required, manually adjust the recipients, **Subject**,
message body and attachments in the email. At this point the placeholders have already been replaced by
the attachment names.
