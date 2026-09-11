---
title: Anwenderhandbuch m+m Media Storage
---

# m+m Media Storage User Guide

## Introduction

The **m+m Media Storage** app determines **where** the media files (images, PDF
documents) stored in Business Central are actually kept. It is the **background storage
repository** for the m+m **DropZone**: when a user drags a file into a DropZone – for
example on an item card – this creates an entry in the **Media Storage** that this app
manages. Media Storage decides whether the file resides in the database or in the cloud,
and provides the list as well as the download function for these files.

Three storage locations are available for selection (field **Storage Type**):

- **Database** – the file is stored directly in the Business Central database (central
  storage, no further setup required).
- **Azure Blob Storage** – the file is stored decentrally in the Microsoft cloud in a
  dedicated Azure storage account.
- **OneDrive** – the file is stored in OneDrive via Microsoft Graph.

**Target audience:** This guide is aimed primarily at **operational users** who, in their
day-to-day work, store files via the DropZone, manage them in the **Media Storage List**,
and download individual files again. Secondarily, it addresses **administrators** who
configure the storage location and – for cloud usage – the access credentials in the
**Media Storage Setup**.

**Prerequisites:**

- The **m+m Media Storage** app is only usefully deployable together with the m+m
  **DropZone** app; the DropZone creates the entries that Media Storage takes in.
- Media Storage requires the base app **m+m Cloud Base**. After sign-in, the module
  automatically checks the license in cloud environments. If the tenant or user is not
  assigned to the module or a payment is overdue, the user receives a notice; in the case
  of repeated overdue payments, the app can be blocked. In on-premises and sandbox
  environments, this check does not apply.

Brief process overview: **choose Storage Type → (for cloud) enter access credentials and
test the connection → store a file via the DropZone → edit the entry in the Media Storage
List → download the file when needed**.

## Quick Start for Users

The following steps lead to the result in the order enforced by Business Central – first
the setup, then daily usage.

1. **Define the storage location.** Use **Search** to open the **Media Storage Setup** page
   and, in the **Storage Location** area, set the **Storage Type** field to **Database**,
   **Azure Blob Storage**, or **OneDrive**.
2. **For Azure Blob Storage only:** In the **Azure Blob Storage** area, fill in the fields
   **Access Key**, **Storage Account**, and **Storage Container**, then choose the
   **Test Connection** action.
3. **For OneDrive only:** In the **OneDrive** area, fill in the fields **Client ID**,
   **Client Secret**, **Tenant ID**, **Email**, and, if needed, **Delegated permissions**,
   then choose **Test Connection**.
4. **Store a file.** In day-to-day work, drag a file into the m+m DropZone of the relevant
   document or master record (e.g. on the item card). The file is stored immediately in
   Media Storage – depending on the **Storage Type**, in the database, in Azure Blob
   Storage, or in OneDrive.
5. **Find the file again.** Use **Search** to open the **Media Storage List**. There you
   will find the stored file again with **Code**, **Source Type**, and **File name**.
6. **Download the file.** In the **Media Storage Files** file overview, select the entry
   and choose **Download File**.

The Storage Type and the access credentials are a prerequisite for steps 4 to 6; details
are provided in the **Setup** chapter.

## Setup

The entire setup of the module takes place on a single card, the **Media Storage Setup**.
It is a company-wide single record (one record per tenant) and is created automatically
the first time it is opened.

**Entry point:** Use **Search** to open the **Media Storage Setup** page
(category *Administration*). There is no higher-level entry via a master data list; the
DropZone app can pre-populate the setup in the background, but for manual maintenance
**Search** is the intended entry point.

**Who sets it up and when:** The administrator defines the Storage Type **once before the
first file is stored**. As long as no cloud storage is selected, no further entries are
needed. The **Storage Type** chosen here directly controls where each file stored via the
DropZone is written (see the **Media Storage List** and **Typical Use Cases** chapters).

### Storage Location

In this area, the fundamental storage location is chosen. It is the only mandatory value of
the setup and unlocks the further input areas.

| Setup | Explanation |
|---|---|
| **Storage Type** | Determines where each new file is written. **Database:** When selected, the file is stored directly in the Business Central database; no further access credentials are required, and the file is immediately available without external services. **Azure Blob Storage:** When selected, the file is uploaded to the configured Azure storage account when stored, the **On Blob Storage** field is set, and the database-internal image is removed; this relieves the database, but incurs costs on Microsoft's side. **OneDrive:** When selected, the file is stored in OneDrive via Microsoft Graph and the **On OneDrive** field is set; storage takes place in the configured OneDrive account. |

Note on **Source Type** (enum, value **(blank)**): Media Storage marks each file with a
source type. In this app, only the value **(blank)** is defined initially; the consuming
modules (e.g. the DropZone on items or documents) extend this selection with their own
source types. For the user, this means: the source type indicates the context a file comes
from, and is set automatically when the file is stored.

### Setting up Azure Blob Storage

**Process:** The administrator carries out this setup **before** working with the Storage
Type **Azure Blob Storage** for the first time. It connects Business Central to an Azure
storage account, into which each file stored via the DropZone is subsequently uploaded
automatically (the actual storage takes place in day-to-day work, see **Typical Use
Cases**). The input area is only editable when the **Storage Type** is set to **Azure Blob
Storage**.

| Setup | Explanation |
|---|---|
| **Access Key** | When configured, Business Central authenticates itself at the storage account with this key (shared key); without a valid Access Key, every upload, download, and delete operation fails and the user receives an error message advising them to check the Media Storage Setup. The field is displayed masked. |
| **Storage Account** | When set, this value determines the target storage account in Azure; the input is automatically converted to lowercase and, together with the container, forms the download URL of the file. |
| **Storage Container** | When set, this value defines the container within the storage account in which the files reside; the input is automatically converted to lowercase. If the container is missing, no connection can be established. |

**Steps in dependency order:**

1. **First**, in the **Storage Location** area, set the **Storage Type** to **Azure Blob
   Storage** – this makes the fields in the **Azure Blob Storage** area editable.
2. **Then** enter **Access Key**, **Storage Account**, and **Storage Container** from your
   Azure portal.
3. **Finally**, choose the **Test Connection** action. On success, the system reports
   "Successfully connected to Azure Blob Storage."; otherwise, check the entries and repeat
   the test.

**Operational conclusion:** Once the connection is established, every further file stored
via the DropZone is automatically uploaded to the container (field **On Blob Storage** =
yes). Daily usage is described in the **Media Storage List** chapter and in the *Activate
cloud storage* use case.

**Dependency:** With every connection attempt, **Storage Container**, **Access Key**, and
**Storage Account** are checked; if one of the values is missing, the operation aborts with
a message.

### Setting up OneDrive storage

**Process:** This setup is an independent alternative to Azure Blob Storage and is carried
out by the administrator **before** working with the Storage Type **OneDrive** for the
first time. It configures a registered Azure application (app registration) through which
Business Central accesses OneDrive via OAuth 2.0. The input area is only editable when the
**Storage Type** is set to **OneDrive**.

| Setup | Explanation |
|---|---|
| **Client ID** | When set, this value identifies the registered Azure application with which the access token is requested; without a valid Client ID, no token can be retrieved and uploads to OneDrive fail. |
| **Client Secret** | When configured, this value, together with the Client ID, is used to sign the application in; without a valid Client Secret, the token request fails. The field is displayed masked. |
| **Tenant ID** | When set, this value determines the Azure tenant against which sign-in occurs; the ID is inserted into the login URL through which the access token is obtained. |
| **Email** | When set and **Delegated permissions** is not enabled, the file is uploaded to the OneDrive of the user account specified here (storage path of the specified mailbox). |
| **Delegated permissions** | When enabled, the file is uploaded to the OneDrive of the signed-in user themselves (path ".../me/drive"); when not enabled, the account specified under **Email** is used instead. This is how you control whether storage takes place in your own OneDrive or in a central one. |

**Steps in dependency order:**

1. **First**, in the **Storage Location** area, set the **Storage Type** to **OneDrive** –
   this makes the OneDrive fields editable.
2. **Then** enter **Client ID**, **Client Secret**, and **Tenant ID** from the Azure app
   registration.
3. **Next**, use **Delegated permissions** and, if applicable, **Email** to define which
   OneDrive files are stored in (your own account or a central mailbox).
4. **Finally**, choose the **Test Connection** action. On success, the system reports
   "Successfully connected to Onedrive."; otherwise, check the entries.

**Operational conclusion:** After a successful test, newly stored files are uploaded to
OneDrive (field **On OneDrive** = yes). This setup and the Azure Blob Storage setup are
mutually exclusive, since both are controlled via the same **Storage Type**.

### Test Connection

The **Test Connection** action is only active when **Azure Blob Storage** or **OneDrive**
is selected as the **Storage Type**. Using the configured access credentials, it checks
whether a connection to the respective service can be established, and outputs a success or
error message without changing any data. For the Storage Type **Database**, no test is
required, since there is no external connection.

## Media Storage List

The **Media Storage List** is the central overview of all files stored in Media Storage. It
shows entries stored both in the database and in the cloud, and serves the user for viewing
and managing the files.

**Entry point:** Use **Search** to open the **Media Storage List**. It is also configured
as a jump-off point from Media Storage.

The entries are created automatically when a user drags a file into the DropZone of a
document or master record. When a user – as in the example of item "EK1701595" – stores an
image in the DropZone, they subsequently find this image again in the Media Storage List.

| Field | Explanation |
|---|---|
| **Entry No.** | Sequential number of the file within the same source context. Assigned automatically when the file is stored (the first file for a source receives 1, each further one the next number) and is not editable. |
| **Code** | Assigns the file to its source object; taken over from the DropZone when the file is stored. Based on the Code, the user recognizes which record the file belongs to. |
| **Source Type** | Indicates which module or context the file comes from. In this app, only the value **(blank)** is defined; consuming modules add further source types. Set when the file is stored. |
| **File name** | The original name of the stored file (technical field *Description*). Serves the user for identifying the file in the list and download. |
| **Picture** | Preview or content of the file, as long as it resides in the database. When stored in Azure Blob Storage, this field is cleared after the upload, since the file then resides externally. |
| **Is Title Image** | When enabled, this file is considered the title image of the source. The **first** file stored for a source is automatically set as the title image; this way the consuming module knows which image to preferentially display. |
| **Position** | Sort order of the file within the source. Controls the order in which the files are displayed. |
| **On Blob Storage** | When enabled (yes), the file resides in Azure Blob Storage and not in the database; the download then takes place directly from the cloud. The field is set automatically on a successful upload and is not editable. |
| **On OneDrive** | When enabled (yes), the file resides in OneDrive. The field is set on the OneDrive upload and is not editable. |

**Deleting:** If the user deletes an entry in the Media Storage List, the associated file is
automatically removed at the respective storage location as well – for **On Blob Storage** =
yes from Azure Blob Storage, otherwise from the internal media storage of the database. Thus,
no orphaned file remains.

**Source fields (technical background):** In addition to the visible columns, Media Storage
maintains additional source information per file – **Source Subtype**, **Source No.**, and
**Source Line No.** – with which a file is uniquely assigned to a document, a line, or a
master record. The DropZone sets these values automatically when the file is stored; the
user does not need to maintain them. For cloud storage, the system additionally stores
**External Picture Url Reference**, **Blob Storage File Name**, and **Blob Storage
Reference** for locating the file again.

## Media Storage Files and Download File

The **Media Storage Files** file overview is an embedded subpart (FactBox) that, alongside
the DropZone, lists the files stored for a record. It shows the **File name** per line and
provides the **Download File** action.

| Field | Explanation |
|---|---|
| **File name** | Name of the stored file; identifies the entry to be downloaded. |

**Download File action:** Select the desired line and choose **Download File**. The system
delivers the file from the correct storage location: if the file resides in Azure Blob
Storage (**On Blob Storage** = yes), it is read directly from the cloud; otherwise, it is
provided from the database. The user then receives the file as a download; PDF files are
named accordingly.

## Permissions

The module includes the permission set **m+m Media Storage** (internal identifier "All
permissions"). It defines which actions a user may perform in Media Storage, and bundles the
read, write, modify, and delete rights on the **Media Storage** and **Media Storage Setup**
tables as well as the execution rights on the associated pages and processing logic. Assign
this permission set to all users who are to store files, manage them in the Media Storage
List, or download them; without these permissions, Media Storage remains unusable for the
user.

## FAQ and Troubleshooting

### 1. Where do I define whether my files are stored in the database or in the cloud?
In the **Media Storage Setup** via the **Storage Type** field in the **Storage Location**
area. The storage chosen there applies to all files stored anew afterward.

### 2. Why is the "Azure Blob Storage" (or "OneDrive") area greyed out?
The respective area is only editable when the **Storage Type** is set to the same value.
First set the Storage Type to **Azure Blob Storage** or **OneDrive**, then the associated
fields are unlocked.

### 3. Why can I not select the "Test Connection" action?
The action is only active when **Azure Blob Storage** or **OneDrive** is selected as the
**Storage Type**. For the **Database** storage, the test does not apply, since there is no
external connection.

### 4. What happens if the connection to Azure fails when storing?
The upload is aborted and the message appears stating that the file could not be uploaded
and that the Media Storage Setup should be checked. Check **Access Key**, **Storage
Account**, and **Storage Container** and test the connection again.

### 5. Why is the "Picture" field empty for some entries, even though a file exists?
When stored in **Azure Blob Storage**, the file is removed from the database after the
upload and the **Picture** field is cleared (field **On Blob Storage** = yes). The file is
not lost – it resides in the cloud and is loaded directly from there on **Download File**.

### 6. How does a file get into Media Storage in the first place?
Not by manual creation: the user drags a file into the m+m **DropZone** of a document or
master record. From this, the system automatically creates an entry in Media Storage with
**Code**, **Source Type**, **File name**, and content.

### 7. Why is my first stored file automatically marked as the title image?
If no title image yet exists for a source, the system automatically sets **Is Title Image** =
yes on the first file. This way, a preferred image is immediately available to the consuming
module. Further files do not receive this marking automatically.

### 8. What happens to the file when I delete an entry from the Media Storage List?
The file is deleted at the respective storage location as well – from **Azure Blob Storage**
if **On Blob Storage** is set, otherwise from the internal media storage of the database. No
orphaned file remains.

### 9. Does the "Delegated permissions" option determine which OneDrive the file is stored in?
Yes. If **Delegated permissions** is enabled, the file lands in the OneDrive of the
signed-in user. If the option is not enabled, the account configured under **Email** is
used.

### 10. After sign-in I receive a license or payment notice – what does that mean?
Media Storage checks the license in cloud environments via the base app **m+m Cloud Base**.
If the tenant or user is not assigned to the module or a payment is overdue, a notice
appears; in the case of repeated overdue payments, the app can be blocked. Contact your
administrator or Markmann + Müller for clarification. In on-premises and sandbox
environments, this check does not apply.

## Typical Use Cases

### Use Case 1: Store a product image for an item

**Trigger:** A colleague sends a product photo for an item by email and asks for it to be
stored in the system.

**Entry point in BC:** The user opens the relevant item; on the card, the m+m DropZone along
with the **Media Storage Files** FactBox is available.

**Core flow:** The user drags the image file into the DropZone. The system automatically
creates a Media Storage entry: **Code** and **Source Type** are taken over from the item
context, **File name** is set from the file name, and – since it is the first file for this
item – **Is Title Image** = yes is set. Depending on the configured **Storage Type**, the
file now resides in the database, in Azure Blob Storage, or in OneDrive. In the **Media
Storage List** (via **Search**), the user subsequently finds the image again.

**Conclusion:** If needed, the user downloads the file again via the **Media Storage Files**
FactBox and the **Download File** action.

### Use Case 2: Activate cloud storage via Azure Blob Storage

**Trigger:** The database is to be relieved; the administrator decides to store all files in
Azure going forward.

**Entry point in BC:** The administrator uses **Search** to open the **Media Storage Setup**.

**Core flow (order mandatory):**
1. In the **Storage Location** area, set the **Storage Type** to **Azure Blob Storage**.
2. In the **Azure Blob Storage** area, enter the fields **Access Key**, **Storage Account**,
   and **Storage Container** from the Azure portal.
3. Choose the **Test Connection** action and wait for the success message.

**Conclusion:** From now on, every file stored via the DropZone is automatically uploaded to
the container; in the **Media Storage List**, these entries have **On Blob Storage** = yes,
and the **Picture** field is cleared. The download continues to take place via **Download
File**, now directly from the cloud.

### Use Case 3: Remove a file that is no longer needed

**Trigger:** A document is outdated and should disappear from the system.

**Entry point in BC:** The user uses **Search** to open the **Media Storage List** and
searches for the entry based on **Code** and **File name**.

**Core flow:** The user selects the entry and deletes it. The system removes the file at the
storage location at the same time: for **On Blob Storage** = yes from Azure Blob Storage,
otherwise from the database.

**Conclusion:** The entry disappears from the Media Storage List; no orphaned file remains at
the storage location. If a copy is still needed beforehand, the user downloads the file first
via **Download File**.
