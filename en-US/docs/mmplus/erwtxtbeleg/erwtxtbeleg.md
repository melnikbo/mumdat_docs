---
title: Anwenderhandbuch m+m Ext. Text Module with Report Package
---

# User Guide m+m Ext. Text Module with Report Package

## Introduction

This module connects two existing m+m extensions with each other: the **m+m Ext. Text Module** app, in which you maintain extended texts (text templates as well as document- and line-related texts), and the **m+m Report Package**, which prints the m+m reports and documents. The module itself has **no pages, fields, or actions of its own**. Its job is to automatically insert the previously captured extended texts at the correct places in the document when an m+m report is printed.

Specifically, the module ensures that

- extended **header and document texts** (positions **Header text**, **Footer text**, **Before Position**, **After Position**) appear in the report at the respective selected place, and
- extended **line texts** are printed below the associated document line,

and this applies to sales and purchase documents, both open and posted (quote, order, invoice, credit memo, shipment, receipt, return).

**Target audience.** This guide is aimed primarily at **operational users** in sales and purchasing who process documents, store extended texts at the header, footer, before or after a position, and then **print** the m+m document. Secondarily, it addresses **administrators** who perform the one-time setup in the **Extended Text Setup**.

**Short process overview.** First, an administrator defines which text source the line texts are drawn from (setup). Then the user stores the extended texts on the document — per position (Header text, Footer text, Before Position, After Position) and per line. When the m+m report is printed, this module automatically inserts the texts into the document; a separate posting or release step is not required for this.

## Quick Start for Users

Prerequisite: The extended text templates and their assignment to documents are created in the **m+m Ext. Text Module** (see the section *Prerequisites from the m+m Ext. Text Module*).

1. **Check the setup (one-time, by the administration).** Open the **Extended Text Setup** page and decide, via the flag **Extended Text Factbox Texts to Report with Printing Sub Type empty**, which source the **line texts** are taken from into the report (see chapter *Setup*).
2. **Open the document.** Open the relevant sales or purchase document (e.g. a sales invoice or a purchase order).
3. **Store the header/document text.** Using the **Extended Text** action on the document header, capture the text for the desired position — **Header text**, **Footer text**, **Before Position** or **After Position**.
4. **Store the line text (optional).** Capture the associated extended line text for individual document lines.
5. **Print the document.** Trigger the printing of the m+m report (the **Print** or **Reports** action on the document). The module automatically inserts the captured texts at the configured places.

The quick start corresponds to the flow from the chapter *How the texts get into the report*; the sequence (setup → capture text → print) is repeated there and in the *Usage examples* with the same steps.

## Setup

The setup of this module is deliberately lean: the module reads exactly **one** control flag from the central setup card of the **m+m Ext. Text Module**. All other fields on this card control other functions of the text-module app and are documented there; they are mentioned here for orientation so that you can reliably find the one relevant setting.

### Extended Text Setup — the controlling flag

**Who sets it up?** An administrator, **once** before first use (company setup).

**Access:** The **Extended Text Setup** is a company-wide setup card (one record per company). Open the page via the search (**Search**) with the term *Extended Text Setup*. The card serves as the setup point of the m+m Ext. Text Module; there is no higher-level master-data entry point for this singleton setup.

**Which behavior is controlled here?** For this module, only the following flag is relevant. It decides which text source the **line texts** are taken from into the report:

| Setup | Explanation |
|---|---|
| Extended Text Factbox Texts to Report with Printing Sub Type empty | When **enabled**, the texts of **Print Type FactBox** (with an empty Sub-Printing Type) are printed as the line text in the report; this lets the user bring the internally maintained FactBox text onto the document without a separate report template. When **not enabled**, the texts of **Print Type Report** (with an empty Sub-Printing Type) are printed as the line text; in that case only the text explicitly intended for printing takes effect. The flag affects **line texts** only — header, footer, before- and after-position texts on the document header are not affected by it. |

**Process step.** Set the flag according to your text strategy **before** the first document output. Its effect is shown in the chapter *Daily work* when the line texts are printed (cross-reference there).

### Remaining fields of the setup card (orientation)

The **Extended Text Setup** page shows further fields on the *General* tab. These control **other** functions of the m+m Ext. Text Module (text copy, template number series, placeholders, e-mail texts, background processing) and **not** the printing of extended texts on m+m reports. They are described in detail in the m+m Ext. Text Module guide. For quick reference:

| Field | Explanation |
|---|---|
| Template Nos. | When set, BC assigns new text templates from this number series; affects template maintenance, not report printing. |
| Language Code | When set, this language is preset for text maintenance; report printing itself uses the language of the printed document. |
| Copy Text | When enabled, extended texts are carried along when documents are copied; affects the document copy, not this printing process. |
| Overwrite Ext. Text | When set, existing extended texts may be overwritten during transfer; controls the text transfer, not the printing. |

For the printing of extended texts on m+m reports, **none** of these fields is otherwise relevant; only the flag described above remains decisive.

### Setting up document texts for printing

For extended texts to actually appear on an m+m document, a multi-stage preparation is required. This chain is described here in dependency order; the actual capture of the templates takes place in the m+m Ext. Text Module, while this module handles the printing.

**Process entry.** Configuration is done by administration or key users **before** the first document with an extended text is printed. The result is used in *Daily work* during document printing.

**Setup steps (in dependency order):**

1. **Create text templates.** In the m+m Ext. Text Module, create the **Extended Text Template** (the **Extended Text Template** page/template card). When a template is created with **Print Type Report**, it can be printed on documents; with **Print Type FactBox** it serves internal display, and with **Print Type Mail** it serves e-mail dispatch.
2. **Choose the Sub-Printing Type (only for Print Type Report).** When the Print Type is **Report**, use the **Sub-Printing Type** to determine at which place in the report the text appears (see the value overview below). If the Sub-Printing Type remains **(empty)**, it is a **line text**.
3. **Assign the template to the document/process.** Assign the template to the desired document or position via the **Assignment Worksheet**. When the assignment is set, the text is available during document printing.
4. **Define the line-text source (optional).** In the **Extended Text Setup**, set the flag **Extended Text Factbox Texts to Report with Printing Sub Type empty** according to your strategy (see above). When enabled, the FactBox text is printed as the line text; otherwise the report text.

**Operational conclusion.** The user opens the document, captures the position texts via the **Extended Text** action, and prints the m+m report (chapter *Daily work*). This closes the chain.

### Sub-Printing Type — value overview (position in the report)

The **Sub-Printing Type** is subordinate to the **Print Type** and can only be used with Print Type **Report**. It defines the printing place of the text. All values provided by the system:

| Sub-Printing Type | Explanation |
|---|---|
| Header | When selected, the text is printed in the **header area** of the report (document position **Header text**). |
| Footer | When selected, the text is printed in the **footer area** of the report (document position **Footer text**). |
| Before Position | When selected, the text is printed **before** the respective document position. |
| After Position | When selected, the text is printed **after** the respective document position. |
| (empty) | When no Sub-Printing Type is set, the text is treated as a **line text** and printed below the associated document line; the source (FactBox or Report) is controlled by the flag in the Extended Text Setup. |

### Print Type — value overview

The **Print Type** of a text template determines what the text is used for. Values provided by the system:

| Print Type | Explanation |
|---|---|
| Report | When selected, the text is intended for **printing on documents** and is taken over into the m+m report by this module. Only with this Print Type is a **Sub-Printing Type** possible. |
| FactBox | When selected, the text serves the **internal display** in the FactBox on the document and is normally not printed. It is only taken over into the report as a **line text** when the flag **Extended Text Factbox Texts to Report with Printing Sub Type empty** is enabled in the Extended Text Setup. |
| Mail | When selected, the text is intended for **e-mail dispatch**; it is not printed into the report by this module. |

## Daily Work on the Document

This section assumes the setup from the chapter *Setup*. In particular, the flag **Extended Text Factbox Texts to Report with Printing Sub Type empty** in the **Extended Text Setup** controls which source **line texts** are printed from (cross-reference: chapter *Setup*).

### Capturing extended texts on the document header

1. Open the sales or purchase document (open or — for a reprint — the posted document).
2. Open the text capture on the document header via the **Extended Text** action.
3. Select the desired **position** and capture the text:
   - **Header text** — appears in the header area of the report.
   - **Footer text** — appears in the footer area of the report.
   - **Before Position** — appears before the positions.
   - **After Position** — appears after the positions.
4. Format the text in the editor if needed. Paragraphs (breaks between paragraphs) are automatically converted into line breaks when printing, so that the text wraps cleanly in the report.

### Capturing extended line texts

1. In the document, select the relevant **line**.
2. Capture the line-related text via **Extended Text**.
3. The line text is output below the document line when printing. Whether the **FactBox** or the **Report** text is drawn in the process depends on the setup flag (see Setup).

### Printing a document with extended texts

1. On the document, trigger the printing of the m+m report (the **Print** or **Reports** / **m+m Report Package** action).
2. The module reads — matching the language of the document — the captured extended texts and inserts them into the report: header, footer, before- and after-position texts at their respective places, line texts below the positions.
3. Images stored in the texts are also output at the respective place.

For **posted** documents (e.g. posted sales invoice, shipment, receipt, credit memo, return), the extended texts saved at the time of posting are printed; reprinting a posted document therefore shows the texts saved there.

## How the Texts Get Into the Report

For a better understanding of the interrelations — fully derived from the behavior of the module:

- **Header/document texts.** When building the report data, the Report Package queries the text module for each printing position (Header text, Footer text, Before Position, After Position) for the matching extended text of the document. The module supplies this text and writes it into the report line buffer.
- **Line texts.** For each document line, the module supplies the extended line text. Which template source is read (Print Type **FactBox** or **Report**, each with an empty Sub-Printing Type) is decided by the setup flag.
- **Open vs. posted documents.** For open documents, the texts come from the document-related text tables; for posted documents, from the posted text tables. This keeps the printout consistent with the posting status on repeat prints.
- **Language.** The texts are read in the language of the printed document, so that foreign-language documents print the appropriate text versions.

## Prerequisites from the m+m Ext. Text Module

For this module to be able to print texts, the texts must already exist in the **m+m Ext. Text Module**. Relevant master data there (only referenced in this module, not maintained by it):

- **Extended Text Template** (template card): with **Template No.**, **Template Text**, **Print Type**, **Start Date**, **End Date**, **Assignment Worksheet** and — for Print Type Report — **Sub-Printing Type**.
- **Assignment Worksheet**: links the template with documents or positions and the desired process.

The complete maintenance of this master data is described in the m+m Ext. Text Module guide. For report printing, it is enough to know that a template with **Print Type Report** and a matching **Sub-Printing Type** must exist and be assigned to the document.

## FAQ and Troubleshooting

### 1. Why does my extended text not appear on the report?

Check the **Print Type** of the template: only texts of Print Type **Report** are printed regularly. A text of Print Type **FactBox** appears as a line text only when the flag **Extended Text Factbox Texts to Report with Printing Sub Type empty** is enabled in the **Extended Text Setup**. Texts of Print Type **Mail** are not printed.

### 2. What exactly does the flag "Extended Text Factbox Texts to Report with Printing Sub Type empty" do?

It controls the source of the **line texts**: when enabled, the **FactBox** text (with an empty Sub-Printing Type) is printed; when disabled, the **Report** text (with an empty Sub-Printing Type). The flag has no effect on header, footer, before- and after-position texts.

### 3. How do I get a text to appear in the letterhead of the document?

Capture the text at the position **Header text** (or create the template with Print Type **Report** and Sub-Printing Type **Header**). For the footer area, use **Footer text** or Sub-Printing Type **Footer**.

### 4. How do I place a note directly below a specific document line?

Capture a **line text** on the relevant line (a template without a Sub-Printing Type, i.e. **(empty)**). The text is printed below the position.

### 5. What is the difference between "Before Position" and "After Position"?

**Before Position** prints the text above the respective document position, **After Position** below it. Both belong to the header/document texts on the document header and are evaluated per position.

### 6. Why are my paragraphs wrapped differently in the report than in the editor?

When printing, the module automatically converts paragraph breaks into single line breaks. As a result, the text is displayed compactly in the report and without empty paragraphs.

### 7. Can I print images in the extended texts?

Yes. If an extended text contains an image, it is taken over into the report at the same place as the text and printed along with it.

### 8. Why do the German texts not appear on the foreign-language document?

The texts are read in the **language of the document**. Store the translation of the text template in the required language; without a matching language version, the module finds no text for that language.

### 9. I changed the template — why does the posted document show the old text?

For **posted** documents, the texts saved at the time of posting are printed. Changes to the template do not apply retroactively to posted documents.

### 10. Do I have to post or release anything after capturing the texts so that they are printed?

No. The module takes effect only when the m+m report is **printed**. An additional posting or release step is not necessary; it is enough to capture the texts and print the document.

## Typical Use Cases

### Use Case 1: Fixed header text on every sales invoice

**Trigger.** Marketing asks for a uniform introductory text to be printed in the header area on every sales invoice.

**Entry in BC.** The administration creates an **Extended Text Template** with **Print Type Report** and **Sub-Printing Type Header** in the m+m Ext. Text Module and assigns it to the sales invoices. Alternatively, the user captures a **Header text** on the individual document via **Extended Text**.

**Core flow.**
1. Open the sales invoice.
2. Capture the **Header text** via **Extended Text** or use the assigned template.
3. **Print** the invoice via the m+m report output.

**Conclusion.** The header text appears in the header area of the printed invoice. For posted invoices, the header text saved at the time of posting is printed.

### Use Case 2: Position-related note below an order line

**Trigger.** A clerk must print a note (e.g. a care instruction) for a specific item directly below the position.

**Entry in BC.** Open the sales order, select the relevant **line**.

**Core flow.**
1. Capture the **line text** for the selected line via **Extended Text** (a template without a Sub-Printing Type, i.e. **(empty)**).
2. Check that the line-text source is set up correctly: with the flag **Extended Text Factbox Texts to Report with Printing Sub Type empty** enabled, the FactBox text is printed, otherwise the Report text (cross-reference: *Setup*).
3. **Print** the order via the m+m report.

**Conclusion.** The note appears immediately below the relevant order line.

### Use Case 3: Footer text to the vendor on the purchase order

**Trigger.** Purchasing wants to print supplementary terms to the vendor in the footer area on every order.

**Entry in BC.** Open the purchase order.

**Core flow.**
1. Capture the text at the position **Footer text** on the document header via **Extended Text**.
2. **Print** the order via the m+m report output.

**Conclusion.** The footer text appears in the footer area of the printed order; likewise on the associated posted purchase documents (receipt, purchase invoice, credit memo, return), provided it was captured there.
