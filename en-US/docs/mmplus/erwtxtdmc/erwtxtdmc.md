---
title: Anwenderhandbuch m+m Ext. Text Module with Digital Metal Code
---

# User Guide m+m Ext. Text Module with Digital Metal Code

## Introduction

The **m+m Ext. Text Module with Digital Metal Code** module extends the base *m+m Ext. Text Module* with two additional **System Procedures** that let you embed **IDMC barcodes** directly into extended texts. When a document is printed or sent, a **placeholder** in an extended text is replaced not by a plain field value but by a **barcode image**: either a **QR Code** (two-dimensional matrix code) or a **Code 39** (linear barcode). The barcode is based on the **IDMC Code** that the *m+m Digital Metal Code* module maintains on the item, item variant, lot, or the related document lines.

The process is deliberately lean: you create a placeholder in the base module, select **IDMC QR-Code** or **IDMC Code39** as the **System Procedures** value, and set **Width** and **Resize %** if required. During printing, the module first looks for a barcode image already stored for the IDMC Code; if none exists, it regenerates the barcode via the barcode service. This way the matching, scannable code automatically appears at the placeholder position on your documents, in your reports, and in email texts.

**Target audience:** This guide is aimed primarily at **operational users in day-to-day business** who use extended texts on sales and purchase documents and need a barcode there. It also addresses **administrators and key users** who maintain the **placeholders** and the **Extended Text Setup** of the base module and who ensure that the items, variants, or lots carry an **IDMC Code**.

**Short process overview:**

1. An administrator ensures in the **Extended Text Setup** that a **Placeholder Start Character** and a **Placeholder End Character** are defined (a prerequisite for placeholders to be processed at all).
2. A key user creates a new placeholder in the **Placeholders** list, selects the target table and the value **IDMC QR-Code** or **IDMC Code39** as the **System Procedures**, and sets **Width** and/or **Resize %**.
3. The placeholder is inserted into the extended text module between the start and end characters.
4. A prerequisite is that the corresponding record has an **IDMC Code** (from the *m+m Digital Metal Code* module).
5. When printing or sending by email, the module replaces the placeholder with the barcode image — either from the cache or newly generated.

> ☞ This module contains **no** posting, release, or report run of its own. It only inserts barcode images into existing extended texts; the actual document processing remains unchanged and standard.

## Quick Start for Users

The quick start describes the shortest path to a result. The order follows the technical dependency: **setup first, then placeholders, then daily work**.

### A. One-time prerequisite (administrator)

1. Use **Search** to open the **Extended Text Setup**.
2. Verify that a **Placeholder Start Character** and a **Placeholder End Character** are defined. Without both characters the base module does not process any placeholders, and no barcode is inserted.

### B. Create a barcode placeholder (key user)

3. In the **Extended Text Setup**, use the **Placeholders** action to open the list of placeholders.
4. Create a new **placeholder** and assign a unique placeholder code.
5. Select the **Table ID** of the target table (e.g. Sales Line) and — if the target field is needed — the **Field No.**
6. Set the **System Procedures** field to **IDMC QR-Code** (two-dimensional code) or **IDMC Code39** (linear barcode).
7. For **IDMC QR-Code**, enter the desired **Width** and, if required, the **Resize %**.

### C. Use the placeholder in text and print (user)

8. Insert the placeholder code — enclosed by the start and end characters — at the desired position in the extended text module.
9. Ensure that the record (item, variant, lot, or document line) carries an **IDMC Code**.
10. Print or send the document as usual. The barcode image automatically appears at the placeholder position.

> ☞ If a barcode image is already stored for the IDMC Code, the module uses it; otherwise it regenerates the barcode during printing (regeneration only in the cloud/SaaS environment).

## Setup

The setup of this module is deliberately minimal: the module ships with **no setup page of its own**. All settings are made on two pages of the base module — the **Extended Text Setup** (global prerequisite) and the **Placeholders** list (the actual configuration of the barcode placeholder). Together these two pages control whether and how the barcode appears at the placeholder position.

### Prerequisite: placeholder characters in the Extended Text Setup

**Who/when:** An administrator makes this setting **once per company** before placeholders are used for the first time. It is a company-wide setup with exactly one record per company. **Entry point:** Use **Search** to open the **Extended Text Setup**. The characters set here are a prerequisite for placeholder processing — and thus for this module's barcode replacement — to start at all (cross-reference: section **Daily Work**).

| Setup | Explanation |
|---|---|
| **Placeholder Start Character** | When set, the base module recognizes the start of a placeholder in the extended text from this character on; if the character is empty, no placeholder — and therefore no barcode — is processed, and the text remains unchanged. |
| **Placeholder End Character** | When set, this character marks the end of the placeholder; only with a valid start **and** end character does the module replace the enclosed code with the barcode image. If either is missing, no replacement takes place. |
| **Template Nos.** | When set, the base module draws the numbers of new text templates from this number series; this affects the creation of text modules in which you later insert the barcode placeholder. |
| **Preview Texts in Source Documents** | When enabled, the base module already displays the extended texts in the source document as a preview; this lets you see before printing where the barcode placeholder takes effect. |

> ☞ The other fields of the **Extended Text Setup** (e.g. automatic text assignment on posting, email placeholders, background text generation) belong to the feature set of the base module *m+m Ext. Text Module* and have **no** influence on this module's barcode generation. They are configured where the base module describes them.

### Set up a barcode placeholder

**Process entry point:** This is the module's central configuration. For each barcode application, a key user creates a **placeholder** and links it to barcode generation via the **System Procedures**. The setup takes effect later in **Daily Work**, as soon as an extended text containing this placeholder is printed or sent. **Entry point:** In the **Extended Text Setup**, use the **Placeholders** action; the **Placeholders** list opens.

The following table describes the placeholder fields that are relevant to barcode generation. The module adds no new fields to them; it merely extends the selection in the **System Procedures** field.

| Field | Explanation |
|---|---|
| **Placeholder** | When set, this is the unique code you insert between the start and end characters in the extended text; the barcode image later appears exactly at this position. Without a placeholder code the record cannot be saved. |
| **Table ID** | When set, the placeholder binds to this target table (e.g. Sales Line, Purchase Line, Item); from it the module reads, during printing, the record whose IDMC Code supplies the barcode. Only the tables released by the base module are allowed. |
| **Table Name** | Displays the name of the selected table (display only); it helps verify that the correct target table was chosen. |
| **Field No.** | When set, the placeholder refers to this field of the target table; for the barcode system procedures this is the starting value from which the module determines the corresponding IDMC field. |
| **Field Name** | Displays the caption of the selected field (display only). |
| **System Procedures** | Controls what the placeholder is replaced with. For this module you select **IDMC QR-Code** or **IDMC Code39** — the placeholder is then replaced with the respective barcode image (the individual values are explained below). |
| **Free Text** | When set, the base module replaces the placeholder with this fixed text; setting a free text clears the table and field reference. For barcode placeholders this field stays empty, because the value comes from the record. |
| **Related Table** | Shows the linked table the placeholder additionally refers to (determined automatically when the Field No. is set, display only). |
| **Related Table Field** | When set, the base module reads the value from this field of the related table; relevant when the IDMC is not directly in the target table but in a linked table. |
| **Related Field Name** | Displays the caption of the related field (display only). |
| **Print Type** | When set to **Report**, the placeholder is available for printing in a report; this determines the output channel in which the barcode appears. |
| **Width** | When set, the module generates the **IDMC QR-Code** with this width; the width controls the edge length of the QR image in the document. If left empty, the barcode service's default size is used. |
| **Resize %** | When set (permitted range −99 to 99), the module scales the generated barcode image by this percentage: a positive value enlarges the image, a negative value shrinks it; at 0 the original size is kept. This lets you fit the barcode to the available space in the document without regenerating the code. |
| **Height** | When set, the image is brought to this height; together with **Width**, the height determines how the barcode is displayed. A change triggers a rescaling of the image. |
| **Picture / Picture Name** | Contains a manually stored image and its name; for the barcode system procedures this image storage usually stays empty, because the barcode image comes from the IDMC cache or is newly generated. |

#### Values of the System Procedures field (task-relevant option values)

The **System Procedures** field is a selection field with a fixed set of values. The base module supplies the first values; this module adds the two IDMC values. Meaning of each value:

- **(blank):** No system procedure is executed; the placeholder — if filled — is replaced via free text or field reference, and **no** barcode is produced.
- **User ID:** The placeholder is replaced with the user ID (base function, no barcode).
- **Today:** The placeholder is replaced with the current date (base function, no barcode).
- **Work Date:** The placeholder is replaced with the work date set in Business Central (base function, no barcode).
- **Current Time:** The placeholder is replaced with the current time (base function, no barcode).
- **IDMC QR-Code:** When selected, the module determines the field with the IDMC Code for the record, looks for a stored **QR Code** image, and places it at the placeholder position; if none exists, it regenerates the QR Code via the barcode service (with the configured **Width**) and embeds it as an image.
- **IDMC Code39:** When selected, the module proceeds in the same way but generates a linear **Code 39** barcode; if no stored image is available, the Code 39 is newly generated and inserted as a barcode.

> ☞ The two values **IDMC QR-Code** and **IDMC Code39** appear in the selection field with this spelling regardless of language, because they are fixed product identifiers.

#### Process steps: set up a barcode placeholder completely

1. **First**, in the **Extended Text Setup**, check or set the **Placeholder Start Character** and **Placeholder End Character** — without these characters no placeholder takes effect.
2. **Then**, use the **Placeholders** action to create a new placeholder, assign a placeholder code, and select the **Table ID** (and, if applicable, **Field No.**) of the target table.
3. **Next**, set the **System Procedures** field to **IDMC QR-Code** or **IDMC Code39** and — for QR — enter the **Width** and, if required, the **Resize %**.
4. **Finally**, insert the placeholder code, enclosed by the start and end characters, into the extended text module (cross-reference: **Daily Work**).

**Prerequisite/dependency:** The barcode is only generated if the record of the target table has a field whose name ends with **IDMC Code** and that is filled. This field comes from the *m+m Digital Metal Code* module (see **Daily Work** and **Prerequisite IDMC Code**). If the IDMC field is empty, the placeholder position remains without a barcode.

## Daily Work

In day-to-day business this module involves no page and no action of its own. It works **in the background** when a document is printed or sent by email, as soon as an extended text contains a barcode placeholder. For the user, the process stays the familiar one: enter the document, assign the extended text, print or send.

**Relation to setup:** For a barcode to appear at the placeholder position, three conditions must be met — they are set or assumed in **Setup**:

1. In the **Extended Text Setup**, the **Placeholder Start Character** and **Placeholder End Character** are defined.
2. In the **Placeholders** list there is a placeholder with **System Procedures** = **IDMC QR-Code** or **IDMC Code39** that is used in the text module.
3. The printed record has a filled **IDMC Code** (from *m+m Digital Metal Code*).

### Prerequisite IDMC Code

The barcode always represents an **IDMC Code**. The *m+m Digital Metal Code* module maintains this code on the item, the item variant, the lot, and on the related sales and purchase document lines. During printing, this module automatically finds the field on the target table whose caption ends with **IDMC Code** and uses its content as the barcode content.

- If the IDMC field is **empty**, the placeholder position remains without a barcode (the document is still printed in full).
- If the IDMC field is **filled**, the module first checks the barcode cache **IDMC Barcode** (a table of the *m+m Digital Metal Code* module).

### Sequence of the barcode replacement (derived from the code)

1. During printing, the base module processes the extended text and encounters a placeholder with **System Procedures** = **IDMC QR-Code** or **IDMC Code39**.
2. This module determines the field on the target table whose name ends with **IDMC Code** and reads its value.
3. It looks in the **IDMC Barcode** cache for an image matching the key of **IDMC Code** and **Barcode Type** (**QR Code** or **Code 39**).
4. **If an image exists**, it is placed at the placeholder position — first scaled according to **Resize %** if required.
5. **If no image exists**, the module regenerates the barcode: the **QR Code** with the configured **Width**, the **Code 39** as a linear barcode. Regeneration takes place via the barcode service and is reserved for the cloud/SaaS environment.
6. The generated or read barcode image replaces the placeholder in the output text.

### The barcode cache: IDMC Barcode

For each **IDMC Code**, the *m+m Digital Metal Code* module stores exactly one image per **Barcode Type**. The **IDMC Barcodes** page displays these images. For this module the cache is the preferred source, because the stored image can be used without another service call.

| Field | Explanation |
|---|---|
| **IDMC Code** | The code the barcode belongs to; it links the printed record with the stored barcode image. |
| **Barcode Type** | Type of barcode. **Code 39:** a linear barcode — used when the placeholder is set to **IDMC Code39**. **QR Code:** a two-dimensional matrix code — used when the placeholder is set to **IDMC QR-Code**. Per IDMC Code, exactly one image is kept per barcode type. |
| **Picture** | The stored barcode image; this module embeds it unchanged (or scaled according to **Resize %**) into the extended text. |

## Typical Use Cases

The following scenarios are derived from the module's verified behavior.

### Use case 1: QR Code on the order confirmation

- **Trigger:** A customer requires a scannable QR Code per line item on the printed order confirmation so that their goods receipt can uniquely identify the goods.
- **Entry point in BC:** Use **Search** to open the **Extended Text Setup** and make sure that the **Placeholder Start Character** and **Placeholder End Character** are set. Then use the **Placeholders** action to open the placeholder list.
- **Core process:** Create a placeholder, select the Sales Line as the **Table ID**, and set **System Procedures** = **IDMC QR-Code**. Enter the desired **Width** and adjust the display via **Resize %** if required. Insert the placeholder code into the extended text module of the order confirmation. Enter the sales order as usual; the line items already carry their **IDMC Code**.
- **Completion:** During printing, the module replaces the placeholder with the QR image from the **IDMC Barcode** cache. The document is printed via the standard function or sent as an email.

### Use case 2: Code 39 barcode for a freshly coded item

- **Trigger:** A newly created item has just received its **IDMC Code**; **no** barcode image is stored for this code yet, but the document should immediately show a linear barcode.
- **Entry point in BC:** In the **Extended Text Setup**, use the **Placeholders** action to open the placeholder list.
- **Core process:** Use a placeholder with **System Procedures** = **IDMC Code39** in the extended text of the relevant document. During printing, the module finds no image in the cache and regenerates the **Code 39** via the barcode service.
- **Completion:** The newly generated barcode appears at the placeholder position. (Regeneration is reserved for the cloud/SaaS environment; see FAQ.)

## FAQ and Troubleshooting

### 1. Why does nothing — no barcode — appear at the placeholder position?

The record's corresponding **IDMC Code** field is empty. The module recognizes the placeholder but finds no code content and leaves the position without a barcode. Provide the item, variant, lot, or document line with an IDMC Code beforehand (*m+m Digital Metal Code* module).

### 2. Why is the placeholder not replaced in the text at all?

The **Placeholder Start Character** or the **Placeholder End Character** is missing in the **Extended Text Setup**. Without both characters the base module does not process any placeholders, and no barcode is inserted. Define both characters.

### 3. When does the module use a stored image and when does it regenerate?

First the module looks in the **IDMC Barcode** cache for an image matching the **IDMC Code** and the **Barcode Type** (**QR Code** or **Code 39**). If an image exists, it is used; if it is missing, the barcode is regenerated via the barcode service.

### 4. Why is no barcode regenerated in my local installation?

**Regeneration** of a barcode via the barcode service takes place only in the cloud/SaaS environment. If no cached image is available, the position remains without a newly generated code in an on-premises installation. In this case, make sure a barcode image is already stored for the IDMC Code.

### 5. What is the difference between IDMC QR-Code and IDMC Code39?

**IDMC QR-Code** generates a two-dimensional **QR Code** (compact, holds a lot of content, scannable by camera) and takes the configured **Width** into account. **IDMC Code39** generates a linear **Code 39** barcode (classic barcode scanner). For each application you choose the appropriate value in the **System Procedures** field.

### 6. How do I set the size of the barcode?

For **IDMC QR-Code** you control the edge length via the **Width**. In addition, **Resize %** scales the finished image: positive values enlarge, negative values shrink it (permitted range −99 to 99); at 0 the original size is kept. This lets you fit the barcode to the available space in the document.

### 7. Which table must I bind the placeholder to?

In the **Table ID**, select the table from which, during printing, the record with the IDMC Code originates (e.g. Sales Line or Purchase Line). Only the tables released by the base module for placeholders are allowed; the base module rejects an invalid table with a message.

### 8. Do I have to fill in the Free Text field?

No. For barcode placeholders, **Free Text** stays empty, because the code content is read from the record. Setting a free text would remove the table and field reference and replace the placeholder with fixed text instead of the barcode.

### 9. Where can I see the existing barcode images?

On the **IDMC Barcodes** page of the *m+m Digital Metal Code* module. There, for each **IDMC Code** and per **Barcode Type**, the stored **Picture** is kept that this module embeds into the extended texts.

### 10. Why does the module not work even though everything is set up?

At sign-in, the module checks the license. If a valid license for the extension is missing, the barcode system procedures are not available. In this case, contact your administrator or m+m to clarify the licensing.
