---
title: Anwenderhandbuch m+m PDF Merge
---

# User Guide m+m PDF Merge

## Introduction

The **m+m PDF Merge** app extends the m+m **DropZone** within Microsoft
Dynamics 365 Business Central with the ability to merge several PDF documents that have been
placed in the DropZone into a single new PDF document. You can then download the merged
document directly or save it back into the DropZone as a new document. Optionally, you can
additionally include standard reports from Business Central in the merge.

Because the app is part of the m+m DropZone, it is available everywhere the DropZone can be
accessed as well — that is, on master data and document pages where the DropZone is shown as
a FactBox. The app does not require any dedicated setup or master data maintenance.

**Target audience:** The app is aimed primarily at **operational users** who, in day-to-day
work, place documents on documents and master data and want to combine them into a single
shared PDF document (e.g. an order confirmation and a drawing in one document).
Administrators are affected only insofar as they assign the required permissions (see
**Prerequisites and Permissions**).

**Brief process overview:**

1. In the DropZone of a page, select the desired PDF files.
2. From the assist-edit menu of the DropZone, choose the action **PDF Merge and View**
   or **PDF Merge and Download**.
3. When viewing, the **PDF Editor** opens; here you can optionally add further reports
   and store the result in the DropZone via **Save as New Report**.
4. The merged document appears in the DropZone or is downloaded as a file.

## Quick Start for Users

Prerequisite: the DropZone of the current page contains **at least two PDF files**.

1. Open the page (master record or document) on which the DropZone is displayed as a
   FactBox. Below the DropZone area you see the placed files with their
   **File name**.
2. Select the files to be merged. To do so, use the standard function **Select More** in the
   assist-edit menu and select the desired lines.
3. Open the assist-edit menu again and choose **PDF Merge and View**. The **PDF Editor**
   opens with the preview of the merged document.
4. *(Optional)* In the PDF Editor, use **Add Report** or **Add multiple reports**
   to add additional standard reports (see **Including Reports in the Merge**).
5. Choose **Save as New Report**, enter a **File name** in the **Report File Name Input**,
   and confirm with **OK**. The merged PDF is stored in the DropZone.

If you only need the document without saving it in the DropZone, in step 3 choose
**PDF Merge and Download** instead. The merged document is then downloaded directly as a file
in your browser, without the PDF Editor being opened.

## Prerequisites and Permissions

This app deliberately contains **no** setup pages, number series, or master data tables of
its own. It relies entirely on the existing functions of the m+m DropZone. Before users can
use the merge, the following prerequisites must be met.

**Dependent modules (prerequisites):** m+m PDF Merge requires the m+m **DropZone**, the
m+m **Media Storage** (where the placed documents are stored), as well as
m+m **Cloud Base**. When these modules are installed and licensed, the app's actions
appear automatically in the DropZone FactBox — a separate activation is not
required.

**Placing documents:** For a merge to be possible, PDF files must already be placed in the
DropZone. Placing is done via the standard function of the DropZone (drag and drop documents
into the DropZone area); the placed files are stored in the Media Storage and listed below
the DropZone with their **File name**. m+m PDF Merge processes only files with the extension
`.pdf`; other file types in the DropZone are skipped during the merge.

**Permissions:** For use, the app ships the permission set
**All permissions** (m+m PDF Merge). This set includes the execution rights for the app's
pages and its processing codeunit. Assign the permission set to the user groups whose members
are allowed to run the merge. The set determines which users can open the app pages (PDF
Editor, Report Lookup, Report File Name Input) and run the merge; rights to the documents
themselves that go beyond this (placing, downloading, deleting) are controlled via the
permissions of the DropZone or the Media Storage.

## Working with PDF Merge in the DropZone

The entire process starts in the **DropZone** FactBox of any page. The app extends this
FactBox with a PDF preview as well as two actions in the FactBox's processing menu.

**Actions in the DropZone FactBox:**

| Action | Explanation |
|---|---|
| **PDF Merge and View** | When you choose this action for the selected files, all selected PDF files are merged into one document and the **PDF Editor** opens as a dialog. There you see the preview of the result and can add further reports as well as save the document. If no selected PDF files exist, the message "You need to select at least one PDF." appears. |
| **PDF Merge and Download** | When you choose this action, the selected PDF files are merged in the background and the result is immediately downloaded as a file, without the PDF Editor being opened. Use this action when you only need the merged document outside of Business Central and do **not** want to place it in the DropZone. |
| **Download file** | Standard action of the DropZone: when you select a single file and choose this action, the selected file is downloaded unchanged. This action does not perform a merge. |

**Fields and areas of the FactBox:**

| Field / Area | Explanation |
|---|---|
| **File name** | Shows the name of the file for each placed document. Based on the `.pdf` extension, the app recognizes which files can be merged. Via this list field you select the files for the merge. |
| DropZone area | The drop area of the DropZone. When you place a document here by drag and drop, it is stored in the Media Storage and then shown in the file list; only afterwards is it available for the merge. |
| PDF preview | Once a merge has taken place, this area displays the generated PDF document. As long as no merge exists, the area remains empty. |

After selecting **PDF Merge and View**, the **PDF Editor** opens. In
this dialog the following areas and actions are available to you.

**Areas and fields in the PDF Editor:**

| Field / Area | Explanation |
|---|---|
| **PDF** (preview) | Shows the currently merged document. Every further file included or report added is appended to the existing document and the preview is then rebuilt. |
| **Error** (message area) | This area is shown only when a problem occurs during the merge. When a file cannot be processed (e.g. an encrypted PDF), the message "There was an error while combining the pdfs. Please check the document." appears here — in this case, check the affected file and start the process again. |

**Actions in the PDF Editor:**

| Action | Explanation |
|---|---|
| **Add Report** | When you choose this action, the **Report Lookup** opens. After selecting **one** report, its request page is shown; the printed report is then appended as a PDF to the merged document. |
| **Add multiple reports** | When you choose this action, the **Report Lookup** also opens, but here you can select **several** reports at once. For each selected report a request page is processed and the result is appended to the document. |
| **Save as New Report** | When you choose this action, the merged PDF currently shown in the preview is saved. Beforehand, you are asked for a **File name** in the **Report File Name Input**. After confirmation, the document is stored as a new entry in the Media Storage of the current DropZone and appears in the DropZone's file list once the PDF Editor is closed. |

### Including Reports in the Merge

In addition to the PDF files placed in the DropZone, you can include **standard reports**
from Business Central in the merged document in the PDF Editor. This
is helpful when a current document (e.g. an order confirmation) is to be output together with
already placed documents in a single PDF.

Proceed as follows:

1. Open the PDF Editor via **PDF Merge and View**.
2. Choose **Add Report** (one report) or **Add multiple reports**
   (several reports). The **Report Lookup** opens.
3. In the Report Lookup, select the desired report(s) and confirm the
   selection.
4. Fill in the displayed request page for each report. The report is
   then generated as a PDF and appended to the merged document; the preview is
   updated.

The **Report Lookup** shows the selectable reports in a list. Only
reports that can actually be output are offered (pure processing reports
without output are hidden).

**Columns in the Report Lookup:**

| Field | Explanation |
|---|---|
| **ID** | Shows the object number of the report. Based on this number the report is called during the merge. |
| **Name** | Shows the internal name of the report object and helps with unambiguous assignment when several reports have similar designations. |
| **Caption** | Shows the descriptive caption of the report, as it also appears with normal report output. Use this column to find the functionally appropriate report. |

### Saving the Merged PDF

If you want to keep the merged document permanently in the DropZone, save
it as a new report. This step completes the merge process.

1. In the PDF Editor, choose **Save as New Report**.
2. The **Report File Name Input** opens. In the **File name** field, enter the
   desired name for the merged document (without extension — the extension `.pdf` is
   added automatically).
3. Confirm with **OK**.

**Field in the Report File Name Input:**

| Field | Explanation |
|---|---|
| **File name** | When you enter a name here and confirm with **OK**, the merged PDF is saved under this name (extended with `.pdf`) in the Media Storage of the current DropZone. If you leave the field empty and confirm without input, the message "You need to specifiy file name." appears and nothing is saved. |

After saving, the new document appears in the DropZone's file list once you
have closed the PDF Editor. If no cover image has been set for the DropZone yet,
the saved document is automatically marked as the cover image (**Is Image Title**).

> **Technical note (combine mode):** Internally, the app distinguishes when
> merging where a document originates from. The mode **(empty)** means that no
> automatic merge is triggered and the existing files are appended.
> With the mode **Print Report**, a Business Central report is output and the result
> is appended (this mode applies to **Add Report** / **Add multiple reports**).
> With the mode **URL**, a document is loaded via an address and appended. This
> distinction is controlled by the app automatically; you do not have to select the mode manually.

## Typical Use Cases (Usage Examples)

### Sending an order confirmation and a drawing as one PDF to a customer

**Trigger:** A customer asks by e-mail for the order confirmation together with the
technical drawing — ideally in a single PDF document.

**Entry in BC:** Open the relevant document (or the master record) on which the
**DropZone** is shown as a FactBox. Both the order confirmation and the
drawing are already there as PDF files.

**Core process:**

1. In the DropZone, select the two PDF files (via **Select More**).
2. In the assist-edit menu, choose **PDF Merge and View**. The **PDF Editor**
   opens and shows both documents one after another in a single PDF.
3. Check the preview. If everything is correct, choose **Save as New Report**.
4. Enter a meaningful **File name** in the **Report File Name Input** and
   confirm with **OK**.

**Completion:** The merged document is now available as a new file in the DropZone and
can be downloaded from there with **Download file** and sent to the customer.

### Bundling several standard reports and placed documents into one document

**Trigger:** For an internal compilation, several Business Central reports are to be
bundled together with already placed PDF files into one document.

**Entry in BC:** Open the page with the **DropZone** in which the prepared
PDF files are located.

**Core process:**

1. Select the existing PDF files and choose **PDF Merge and View**.
2. In the **PDF Editor**, choose the action **Add multiple reports**.
3. In the **Report Lookup**, select the required reports and confirm the
   selection.
4. Go through the request page for each report. The reports are appended one after another to the
   document; the preview is updated each time.
5. Choose **Save as New Report**, enter a **File name**, and confirm
   with **OK**.

**Completion:** The bundled document is ready in the DropZone. If it is only needed
temporarily, in step 1 you can alternatively choose **PDF Merge and Download**
and skip the saving.

## FAQ and Troubleshooting

### 1. Why don't the merge actions appear?

The actions **PDF Merge and View** and **PDF Merge and Download**
belong to the **DropZone** FactBox. They appear only on pages on which the DropZone is
shown, and only when the m+m PDF Merge app together with the dependent modules (DropZone,
Media Storage, m+m Cloud Base) is installed and licensed and the permission set
has been assigned.

### 2. What happens if I have not selected a file?

If you run **PDF Merge and View** or **PDF Merge and Download**
without a selected PDF file, the message "You need to select at least one
PDF." appears. No document is created. Select at least one
PDF file and repeat the process.

### 3. Why are some files not taken into account during the merge?

The app processes only files with the extension `.pdf`. Other file types (e.g.
images or Office documents) in the DropZone are skipped during the merge. Check
whether the desired file is actually a PDF document.

### 4. What does the message "There was an error while combining the pdfs" mean?

This message appears in the **Error** area of the PDF Editor when one of the files could not
be merged — often with **encrypted** PDF documents or with
corrupted files. Remove the affected file from the selection or place an
unencrypted version in the DropZone and start the process again.

### 5. How do I save the result permanently in Business Central?

Open the result via **PDF Merge and View** and, in the PDF
Editor, choose **Save as New Report**. After entering a **File name** and confirming with
**OK**, the merged PDF is stored in the Media Storage of the current DropZone.

### 6. Why do I have to enter a file name?

The file name is required so that the document can be saved unambiguously. If you leave
the **File name** field empty, the message "You need to specifiy file name."
appears and nothing is saved. The extension `.pdf` is added automatically.

### 7. How do "view" and "download" differ?

With **PDF Merge and View**, the **PDF Editor** opens with the preview; there
you can add reports and save the result in the DropZone. With **PDF
Merge and Download**, the result is downloaded immediately as a file without an editor
and is **not** saved in the DropZone.

### 8. Where do I find the merged document after saving?

The saved document appears in the DropZone's file list once you have closed the PDF
Editor. From there you can download it like any other placed file via
**Download file**.

### 9. Can I include reports in addition to the DropZone files?

Yes. Open the PDF Editor via **PDF Merge and View** and choose
**Add Report** (one report) or **Add multiple reports** (several reports).
The selection is made in the **Report Lookup**; for each report you go through a request page.

### 10. Why is my saved document marked as the cover image?

If **no** cover image has been set for the current DropZone yet, the app marks
the document just saved automatically as the cover image (**Is Image Title**). If a cover
image already exists, it remains unchanged and the new document is placed without
a cover-image marking.
