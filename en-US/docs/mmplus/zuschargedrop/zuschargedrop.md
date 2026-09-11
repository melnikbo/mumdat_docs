---
title: Anwenderhandbuch m+m Additional Lot Information with Dropzone
---

# User Guide m+m Additional Lot Information with Dropzone

## Introduction

The **m+m Additional Lot Information with Dropzone** extension connects three m+m modules within Microsoft Dynamics 365 Business Central: **m+m Additional Lot Information**, **m+m Dropzone** and **m+m Media Storage**. It ensures that documents and images stored against a lot via **DropZone** automatically travel along with a lot derived from it.

The business background: In **m+m Additional Lot Information**, a lot can reference an **original lot** (fields **Original Item No.**, **Original Lot No.** and **Original Variant Code** on the **Lot No. Information Card**). When a user creates such a derived lot or changes its original-lot details, this extension transfers the **attachments** stored via DropZone on the original lot to the new lot — controlled by a single toggle in the **Media Storage Setup**.

**Target audience:** Primarily **operational users** in warehouse, quality and logistics who create lots or maintain lot information in day-to-day work and want to see the associated documents on the derived lot immediately. **Secondarily**, the **Setup** chapter is aimed at administrators or key users who enable the function once, company-wide.

**Short process overview:**

1. The administrator activates the **Transfer Attachments from the Original Lot** toggle in the **Media Storage Setup**.
2. A user maintains the **Original Lot No.** (and **Original Item No.**) on a lot.
3. When the lot is saved, the extension automatically copies all DropZone attachments of the original lot to the derived lot, unless they already exist there.

This extension has **no** document of its own, no posting and no manual button for the transfer — the process runs **automatically** in the background as soon as the toggle is set.

## Quick Start for Users

The fastest route to a result consists of a one-time setup and the ongoing maintenance of the original-lot details.

1. **First — enable the function (one-time, administrator):** Use **Search** to open the **Media Storage Setup** and, in the **Dropzone** area, activate the **Transfer Attachments from the Original Lot** toggle. If this toggle is not set, no transfer takes place.
2. **Then — record the original lot (user):** Open the **Lot No. Information Card** of the derived lot and enter the **Original Item No.** and the **Original Lot No.** (and, if applicable, the **Original Variant Code**).
3. **Result:** When saving, the **attachments** stored via **DropZone** on the original lot are automatically transferred to the derived lot and appear there in the DropZone fact box.

> Prerequisite: Attachments must already have been stored on the original lot via the DropZone, and the **Media Storage** must be set up — as is usual for the DropZone (see **Setup**).

## Setup

The entire setup of this extension takes place on **one** page: the **Media Storage Setup**. This page belongs to the **m+m Media Storage** module; the present extension adds the **Dropzone** area with a single toggle to it. Because Business Central shows the user **one** cohesive page, this guide documents the **complete** page — the Media Storage base fields and this extension's additional field together.

**Getting there:** Use **Search** to open the **Media Storage Setup**. It is a company-wide setup page (one record per company); it is created automatically the first time it is opened.

### Configuring attachment transfer

**Who and when:** This setup is performed once by an **administrator** or **key user** before first use. It controls the entire module behavior and is used in day-to-day work by users on the **Lot No. Information Card** (see **Master Data** and **Automatic Process**).

**Sequence (in order of dependency):**

1. **First — define the storage location:** In the **Storage Type** field, choose where the **Media Storage** stores the files (**Database**, **Azure Blob Storage** or **OneDrive**). This setting is the foundation that allows DropZone attachments to be stored at all and later copied. Depending on your selection, fill in the associated connection fields (see field table) and check the connection with **Test Connection**.
2. **Then — enable the transfer:** In the **Dropzone** area, activate the **Transfer Attachments from the Original Lot** toggle. Only then is the automatic copying of attachments armed.
3. **Finally — operational completion in day-to-day work:** The chain is completed without any further button: as soon as a user maintains and saves the **Original Lot No.** and **Original Item No.** on a lot, the attachments are transferred automatically (see **Automatic Process**).

**Field table – Media Storage Setup (Storage Location, Azure Blob Storage, OneDrive, Dropzone areas):**

| Setup | Explanation |
|---|---|
| **Storage Type** | Determines where the Media Storage — and thus the DropZone attachments — is stored. The selection controls which connection fields below it are active. **Database:** When selected, attachments are stored directly in the Business Central database; no external connection data is required. **Azure Blob Storage:** When selected, attachments are stored in an Azure storage; the fields **Access Key**, **Storage Account** and **Storage Container** become editable and must be filled. **OneDrive:** When selected, attachments are stored in OneDrive; the OneDrive fields (**Client ID**, **Client Secret**, **Tenant ID**, **Onedrive Email**, **Delegated permissions**) become editable. |
| **Access Key** | If the Storage Type is **Azure Blob Storage**, enter the storage account's access key here; without a valid key, **Test Connection** fails and no attachments can be stored or copied. (Masked as a password field.) |
| **Storage Account** | If the Storage Type is **Azure Blob Storage**, specify the name of the Azure storage account here; it determines which account the files reside in. |
| **Storage Container** | If the Storage Type is **Azure Blob Storage**, specify the container in which the files are stored within the storage account here. |
| **Client ID** | If the Storage Type is **OneDrive**, enter the client ID of the registered Azure app here; it enables Business Central to sign in to OneDrive. Without this value, OneDrive storage is not possible. |
| **Client Secret** | If the Storage Type is **OneDrive**, enter the associated client secret of the Azure app here; together with the Client ID it authenticates the access. (Masked as a password field.) |
| **Tenant ID** | If the Storage Type is **OneDrive**, specify the directory/tenant ID here; it determines which Azure AD tenant the sign-in takes place in. |
| **Onedrive Email** | If the Storage Type is **OneDrive**, enter the OneDrive mailbox or user here, in whose storage the files are saved. |
| **Delegated permissions** | If the Storage Type is **OneDrive**, this field controls whether access uses delegated permissions (on behalf of a signed-in user); with it you determine the permission model of the OneDrive connection. |
| **Transfer Attachments from the Original Lot** | The central toggle of this extension. **When enabled**, Business Central automatically copies all DropZone attachments of the original lot to the derived lot whenever a lot with a recorded original lot is created or changed. **When not enabled**, lot maintenance remains unchanged; no attachments are transferred and the user would have to store documents on the new lot manually via DropZone. |

**Action on this page:**

- **Test Connection** – checks the connection to the external storage. **If** the Storage Type is **Azure Blob Storage** or **OneDrive**, run this action after filling in the connection fields to ensure that attachments can actually be stored and later copied. With the Storage Type **Database**, the action is not required.

**Validation/dependency:** The transfer only takes effect if (a) the **Transfer Attachments from the Original Lot** toggle is active **and** (b) both **Original Item No.** and **Original Lot No.** are filled on the derived lot. If one of these entries is missing, the copy does not occur (see **Automatic Process**). Cross-reference: maintaining the original-lot details is described under **Master Data**.

## Master Data

This extension does **not** provide any master data pages of its own. It relies on the **Lot No. Information** from the **m+m Additional Lot Information** module and on the **attachments** stored via **DropZone**. Both are prerequisites for the automatic transfer and are described here only as far as is necessary to use this extension.

### Maintaining the original lot on the Lot No. Information Card

**Who and when:** Users in warehouse/quality maintain these details as soon as it is established from which original lot a lot was derived. The details come from the **m+m Additional Lot Information** module and are the triggers for this extension's attachment transfer.

**Relevant fields (Lot No. Information Card):**

| Field | Explanation |
|---|---|
| **Original Item No.** | References the item number of the original lot. **When filled** (together with the Original Lot No.), this field jointly identifies the original lot from which the attachments are copied. |
| **Original Lot No.** | References the lot number of the original lot. **When filled**, the extension looks up its DropZone attachments and transfers them to the current lot. If the field is empty, no transfer takes place. |
| **Original Variant Code** | Additionally narrows the original lot down to a specific variant. **When filled**, the original lot is determined exactly by item, variant and lot number; for variant-tracked items this prevents a mix-up. |

**Process step:** Open the **Lot No. Information Card** of the derived lot, enter the **Original Item No.** first and then the **Original Lot No.**, and save. The prerequisite is that the toggle from the **Setup** chapter is set (cross-reference: **Configuring attachment transfer**).

### DropZone attachments on the lot

The **DropZone** is shown as a separate fact box on the **Lot No. Information Card**. Users store documents there via drag and drop; the files are stored in the **Media Storage** (source: Lot No. Information). For this extension, these attachments are the **source stock**: exactly the attachments stored on the original lot are copied to the derived lot. A separate setup of the DropZone is not required; only the **Media Storage Setup** is decisive (see **Setup**).

## Automatic Process (transferring the attachments)

This extension does **not** provide the user with a button for transferring. The transfer takes place **automatically**, triggered by saving a lot.

**Process in detail (derived from the code):**

1. **Trigger:** A **Lot No. Information** record is **created** or **changed** (e.g. when the original-lot details are entered). Both events trigger the check.
2. **Check original-lot reference:** The extension checks whether both **Original Item No.** and **Original Lot No.** are filled on the lot. If one entry is empty, the operation ends without any action.
3. **Check toggle:** It checks whether the **Transfer Attachments from the Original Lot** toggle is active in the **Media Storage Setup**. If it is not set, the operation ends.
4. **Determine the original lot:** Using **Original Item No.**, **Original Variant Code** and **Original Lot No.**, the matching Lot No. Information record is searched for. If **Item No.** or **Lot No.** is missing there, the operation ends.
5. **Copy attachments:** All **Media Storage** entries of the original lot (source Lot No. Information) are iterated over. For each entry it is checked whether an attachment with **the same description** already exists on the target lot. Only if not, the attachment — including the stored **image**/file — is copied to the target lot and created with a new running number.

**What the user sees:** After saving, the copied documents appear in the DropZone fact box of the derived lot and can be opened or downloaded there as usual. Existing attachments with the same name are not created twice.

## Permissions

The extension delivers the **"All Permissions"** permission set (object name **MuM ALDZ Permission**). It defines which actions a user may perform within this extension, and includes the execution rights for the two internal codeunits (management and event processing). Because the transfer runs automatically when the lot is saved, users additionally need the usual rights to the **Lot No. Information** and the **Media Storage**. Assign the permission set to the users or user groups that work with lot information and DropZone attachments.

## Typical Use Cases

The following scenarios are derived from the actual behavior verified in the code.

### Use case 1 – Derived lot receives the documents of the original lot

1. **Trigger:** In the warehouse, a new, derived lot is created from an existing lot (e.g. by repackaging or splitting). Test documents and images for the original lot already exist in the DropZone.
2. **Entry point in BC:** The user opens the **Lot No. Information Card** of the new lot.
3. **Core process:** They enter the **Original Item No.** and the **Original Lot No.** (for variant-tracked items also the **Original Variant Code**) and save. The prerequisite is that the administrator has previously activated **Transfer Attachments from the Original Lot** in the **Media Storage Setup**.
4. **Completion:** Business Central automatically copies all DropZone attachments of the original lot to the new lot. The user finds them immediately in the DropZone fact box of the derived lot — without having to upload the files again.

### Use case 2 – Original lot is added afterwards

1. **Trigger:** A lot has already been created, but the associated original lot only becomes known later.
2. **Entry point in BC:** The user opens the **Lot No. Information Card** of the affected lot again.
3. **Core process:** They add the **Original Lot No.** and **Original Item No.** and save the change. Because changing the lot also triggers the transfer, no further step is required.
4. **Completion:** The attachments of the original lot are transferred afterwards. Existing attachments with the same name remain unchanged and are not created twice.

## FAQ and Troubleshooting

### 1. Why are no attachments transferred to the new lot?
First check whether the **Transfer Attachments from the Original Lot** toggle is activated in the **Media Storage Setup**. Without this toggle, no transfer takes place.

### 2. Which details must I maintain on the lot for the transfer to take effect?
**Both** fields **Original Item No.** and **Original Lot No.** must be filled. If one of the two entries is missing, the copy does not occur.

### 3. Do I have to start the transfer manually?
No. There is no button. The transfer runs automatically when the Lot No. Information is **created** or **changed**.

### 4. Can I also trigger the transfer afterwards?
Yes. Open the **Lot No. Information Card**, add or change the original-lot details and save. Changing the lot also initiates the transfer.

### 5. Are attachments created twice if I save the lot multiple times?
No. Before copying, it is checked whether an attachment with **the same description** already exists on the target lot. Only missing attachments are added.

### 6. Where do the transferred documents come from?
From the **Media Storage** entries of the original lot, i.e. from the attachments stored via **DropZone** on the original lot (source Lot No. Information).

### 7. Why do I find no attachments to transfer on the original lot?
Documents must previously have been stored on the original lot via the **DropZone**. If the original lot has no attachments, there is nothing to copy.

### 8. Which Storage Type should I choose in the Media Storage Setup?
Choose **Database** to store directly in Business Central, **Azure Blob Storage** or **OneDrive** for external storage. For the external variants, fill in the associated connection fields and check the connection with **Test Connection**.

### 9. What happens if the original lot does not lead to a valid Lot No. Information?
If the original lot cannot be uniquely determined by item and lot number, or the lot number is missing there, the operation ends without a copy and without an error message.

### 10. Which permissions do the users need?
Assign the delivered **"All Permissions"** permission set (MuM ALDZ Permission). In addition, users need the usual rights to the **Lot No. Information** and the **Media Storage**, since the transfer takes place when the lot is saved.
