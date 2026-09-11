---
title: Anwenderhandbuch m+m Goods Receipt with Dropzone
---

# User Guide m+m Goods Receipt with Dropzone

## Introduction

The m+m extension **Goods Receipt with Dropzone** adds a **document storage area directly on the warehouse receipt document** to goods reception in "Microsoft Dynamics 365 Business Central". Users can attach files (delivery notes, certificates, photos, PDFs) to the **Warehouse Receipt** via drag and drop, or capture an **image** directly through the device camera. When the warehouse receipt is processed, these documents are automatically transferred to the resulting **processed goods receipt** (source type **Processed Whse Receipt**), so that the documentation remains permanently linked to the transaction.

**Target audience:** Primarily the **operational users in goods receipt and warehouse processing** who record, release, and process warehouse receipts on a daily basis and keep documents or photos attached to the transaction. Secondarily, the extension concerns administrators, who only need to ensure the dependent apps are installed — no functional setup is required.

**Brief process overview:** The extension adds the **DropZone** FactBox to both the **Warehouse Receipt** view and the processed goods receipt view. On the warehouse receipt, the **Take Picture** action is additionally available. When the user attaches files on the warehouse receipt and then processes the document through the standard functions of the Goods Receipt module (**Release**, **Process**), the attached documents automatically move along to the processed goods receipt. If a still-open warehouse receipt is deleted, the associated documents are removed as well.

> This extension builds on the m+m apps **m+m Goods Receipt** (Goods Receipt), **m+m Dropzone**, **m+m Media Storage**, and **m+m Cloud Base**. The actual warehouse receipt documents, their header and line fields, as well as the actions **Release**, **Notify**, and **Process** originate from the Goods Receipt module; this guide describes the functions added by the DropZone extension and their place in the process.

## Quick Start for Users

The fastest path from the warehouse receipt to a documented, processed goods receipt:

1. **Open the warehouse receipt.** In the Goods Receipt module, select the desired line in the list of warehouse receipts and open the **Warehouse Receipt** view.
2. **Attach documents.** Drag the desired files from Windows Explorer into the **DropZone** FactBox while holding down the mouse button, and release them there (drag and drop). The file is saved and listed below the drop area under **File name**.
3. **Optional: Take a picture.** Use the **Take Picture** action to create a photo of the goods directly through the device camera. The photo is automatically stored as a document on the warehouse receipt.
4. **Release.** Trigger the **Release** action to release the warehouse receipt (status **In Process** / released).
5. **Process.** Start processing the warehouse receipt via the **Process** category. This creates the **processed goods receipt** (Processed Whse Receipt).
6. **Check the result.** Open the processed goods receipt: in its **DropZone** FactBox you will find the same documents again — they were transferred automatically.

**No separate setup** is required for use (see the following chapter).

## Setup

**No functional setup** is required for the **Goods Receipt with Dropzone** extension. There are no dedicated setup pages, no number series, and no parameters to maintain. The function is available directly on the warehouse receipt and on the processed goods receipt as soon as the required apps are installed.

**Prerequisites (to be ensured by the administrator):**

| Setup | Explanation |
|---|---|
| App **m+m Goods Receipt with Dropzone** installed | When the extension is installed in Extension Management, the **DropZone** FactBox and the **Take Picture** action appear on the warehouse receipt, as does the **DropZone** FactBox on the processed goods receipt; without the installation, these functions are not available. |
| Dependent app **m+m Goods Receipt** installed | When the Goods Receipt module is present, the **Warehouse Receipt** and **Processed Whse Receipt** documents exist, which the DropZone docks onto; if it is missing, there are no target documents for the document storage. |
| Dependent app **m+m Dropzone** installed | When the Dropzone base is present, storage via drag and drop works, including the list (**File name**) and the **Download File** action; without it, the drop area is missing. |
| Dependent app **m+m Media Storage** installed | When media storage is present, the attached files and captured images are permanently held in the database (or in the configured storage) and can be retrieved later; without it, no documents can be saved. |

> Note: Where and how the media storage is physically stored (e.g. database or Azure storage) is governed by the **m+m Media Storage** app through its own setup. No additional settings specific to this extension need to be made there for the DropZone on the warehouse receipt.

## Daily Work on the Warehouse Receipt

The actual work takes place on two documents of the Goods Receipt module: on the **Warehouse Receipt** (open warehouse receipt document) and on the **processed goods receipt** (Processed Whse Receipt). Both receive the **DropZone** FactBox through this extension; the warehouse receipt additionally receives the **Take Picture** action.

The following header fields of the **Warehouse Receipt** originate from the Goods Receipt module and serve here only for orientation as to which transaction the documents are attached to:

| Field | Explanation |
|---|---|
| **No.** | Unique document number of the warehouse receipt; the DropZone assigns all attached documents to exactly this number. |
| **Location Code** | Location for which the goods are received; controls the further warehouse logic of the base module. |
| **Receipt Date** | Date of the goods receipt; documents when the goods were received. |
| **Sell-to Customer No.** / **Sell-to Customer Name** | Customer, provided the receipt is linked to a sales transaction; relevant for follow-up steps such as **Create Sales Order**. |
| **Posting Date** | Date with which the processing is posted. |
| **Status** | Processing state of the document; **In Process** indicates a released document that has not yet been completed. |

### DropZone FactBox

The **DropZone** FactBox is the central storage area for documents on the warehouse receipt. It is displayed at the top of the FactBoxes on both the warehouse receipt and the processed goods receipt, and is always linked to the document number (**No.**) of the current document.

**How to attach a document:** Open Windows Explorer, select the desired file, and drag it into the **DropZone** area while holding down the mouse button. Release the file there. The document is saved and displayed in the list below the drop area.

| Field / Action | Explanation |
|---|---|
| **DropZone** (drop area) | When you drag and drop a file into this area, it is saved and permanently assigned to the current warehouse receipt (via its **No.** and the source type **Whse Receipt**); the file is thereby available on the document again at any time. |
| **File name** | Displays the name of the attached file per line; select a line to run the action for exactly that document. |
| **Download File** | When you select a line and run this action, the associated file is downloaded to your device; this is how you retrieve a previously attached document (e.g. the delivery note) again. |

> The attached documents can be displayed in the DropZone and downloaded again. Documents that are no longer needed can be removed again from the open document; when the open warehouse receipt is deleted, the associated documents are automatically deleted along with it (see **Processing and Posting Flow**).

### "Take Picture" Action

On the **Warehouse Receipt**, the promoted **Take Picture** action is available in the **Process** ribbon category.

| Action | Explanation |
|---|---|
| **Take Picture** | When you run this action, the device's camera function opens; after capturing, the photo is automatically saved as a document on the current warehouse receipt and appears in the list (**File name**) of the **DropZone** FactBox. This is how you document, for example, the condition of the delivered goods without a separate upload. |

**Flow in detail:** After triggering the action, you capture the image in the camera dialog and confirm it. The system automatically assigns a file name composed of the document number and a sequential number (example: `WA00012_3.jpg`) and stores the image as a further document on the warehouse receipt. This action is particularly suited for capture via tablet or smartphone in the web client.

### Processing and Posting Flow

The document storage follows the processing path of the Goods Receipt module. The extension intervenes automatically here — it has no posting action of its own, but reacts to the processing of the base module:

1. **Open the warehouse receipt** and attach documents or photos to the **DropZone** (actions **Take Picture**, drag and drop).
2. **Release** (action **Release**): The document is released and prepared for further processing.
3. **Process** (category **Process**): The warehouse receipt is processed via the processing functions of the base module; this creates the **processed goods receipt** (Processed Whse Receipt).
4. **Automatic document transfer:** At the moment the processed goods receipt is created or updated, the extension transfers all documents attached in the DropZone of the open warehouse receipt (source type **Whse Receipt**) to the processed goods receipt (source type **Processed Whse Receipt**). The assignment is made via the **Source Document No.** of the posted document.
5. **Result on the processed goods receipt:** Open the processed goods receipt; in its **DropZone** FactBox the same documents are visible and retrievable via **Download File**. The header fields **Processed by User ID** and **Processed at** document who processed the receipt and when; the **Reversed** field marks correction documents.
6. **Deleting an open warehouse receipt:** If a still-open warehouse receipt is deleted, the extension automatically removes the associated attached documents (source type **Whse Receipt**), so that no orphaned documents remain.

> There is no requirement that all documents must be attached before processing is allowed — the document storage is independent of the posting status. Documents that have already been attached remain on the processed goods receipt after processing.

## Source Types of Document Storage

The extension distinguishes which document type a document is attached to. To do this, it extends the source type of the media storage by two values. Each attached document carries exactly one of these source types:

| Value | Explanation |
|---|---|
| **Whse Receipt** | When a document carries this source type, it is assigned to an **open warehouse receipt**. Such documents are transferred to the processed goods receipt during processing and are removed when the open warehouse receipt is deleted. |
| **Processed Whse Receipt** | When a document carries this source type, it is assigned to the **processed goods receipt**. These documents are created automatically during processing from the documents of source type **Whse Receipt** and remain permanently on the posted document. |

> These source types control the automatic assignment in the background; the user does not select them manually. They explain why a document attached to the warehouse receipt reappears on the processed goods receipt after processing.

## Typical Use Cases

### Attach a delivery note at goods receipt

**Trigger:** A paper delivery note arrives with the goods and is to be stored digitally on the transaction.

**Entry point in BC:** The user opens the relevant **Warehouse Receipt** in the Goods Receipt module.

**Core flow:** The delivery note is scanned and the file is dragged into the **DropZone** FactBox via drag and drop. It appears immediately under **File name**. The user then releases the warehouse receipt via **Release** and starts the **Process**.

**Completion:** On the automatically created **processed goods receipt**, the delivery note is still present in the DropZone and can be called up at any time via **Download File**.

### Take a photo of the goods directly at goods receipt

**Trigger:** During unloading, transport damage is noticed that is to be recorded photographically.

**Entry point in BC:** On a tablet or smartphone, the user opens the **Warehouse Receipt** of the transaction in the web client.

**Core flow:** Via the promoted **Take Picture** action, the user opens the camera, takes a photo of the damaged goods, and confirms it. The image is automatically saved as a document and appears in the DropZone under **File name**. If needed, further photos are added.

**Completion:** After **Release** and **Process**, the photos are on the processed goods receipt and are available for later complaint or inspection processes.

### Documents move automatically to the posted document

**Trigger:** A colleague has already attached certificates and photos to the warehouse receipt; the transaction is now to be completed.

**Entry point in BC:** The user opens the prepared **Warehouse Receipt**.

**Core flow:** The user checks the documents listed in the DropZone, releases the document via **Release**, and triggers the **Process**. No manual copying of the documents is necessary.

**Completion:** The extension transfers all documents automatically to the **processed goods receipt** (source type **Processed Whse Receipt**). The user opens the posted document and finds the same documentation there again — linked via the **Source Document No.**

## FAQ and Troubleshooting

### 1. Why do I not see a DropZone on the warehouse receipt?
The FactBox appears only if the app **m+m Goods Receipt with Dropzone** and its dependent apps (**m+m Dropzone**, **m+m Media Storage**, **m+m Goods Receipt**) are installed. Also check whether the FactBoxes are shown in the page's side pane.

### 2. How do I add a document?
Drag the file from Windows Explorer into the **DropZone** area while holding down the mouse button and release it. Alternatively, on the warehouse receipt use the **Take Picture** action to capture a photo via the camera.

### 3. What happens to my documents when I process the warehouse receipt?
During processing, the **processed goods receipt** is created. All documents attached to the warehouse receipt are automatically transferred to this posted document and remain there.

### 4. Do I have to transfer the documents manually after processing?
No. The transfer happens automatically as soon as the processed goods receipt is created or updated. Manual copying is not intended.

### 5. Why can I no longer find an attached document after deleting the warehouse receipt?
If a still-**open** warehouse receipt is deleted, the extension automatically removes the files attached to this document, so that no orphaned documents remain. After processing, the documents are on the processed goods receipt and are not affected by the deletion of the open warehouse receipt.

### 6. How do I retrieve an attached document again?
In the DropZone, select the desired line (**File name**) and run the **Download File** action. The file is downloaded to your device.

### 7. Where do I find the photos created with "Take Picture" again?
The captured photos appear immediately in the **DropZone** FactBox of the warehouse receipt (list **File name**) and are transferred to the processed goods receipt during processing.

### 8. Do I have to set anything up first before I can attach documents?
No. No functional setup is required for this extension. It is sufficient that the app and its dependent apps are installed.

### 9. Can I attach multiple documents to one warehouse receipt?
Yes. You can attach any number of files and take multiple photos; each document is kept as its own line with its own **File name**.

### 10. Why does the system distinguish between "Whse Receipt" and "Processed Whse Receipt"?
These two source types indicate whether a document is attached to an **open** warehouse receipt (**Whse Receipt**) or to the **processed** goods receipt (**Processed Whse Receipt**). The distinction controls the automatic transfer during processing and the cleanup when open documents are deleted.
