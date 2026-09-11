---
title: Anwenderhandbuch m+m Certificate Of Supply with Report Dispatch
---

# User Guide m+m Certificate Of Supply with Report Dispatch

## Introduction

This module connects the m+m **Certificate of Supply** with the m+m **Report Dispatch**. It ensures that a **Certificate of Supply** and the corresponding **Certificate of Supply reminder** can not only be printed but also sent to the correct recipient via Report Dispatch as an **email** or as a **print attachment**. The module itself has no pages or fields of its own; it operates in the background and enables the sending channel for these two documents.

Functionally, the module handles three tasks automatically during sending: for the selected Certificate of Supply it determines the associated document (the **Sales Shipment**), it determines the appropriate recipient together with the **Language Code** based on the customer or vendor, and it selects the applicable **Document Sending Profile** for the respective document. The user does not have to make this assignment manually.

**Target audience.** The primary target audience is **operational users** in sales and in shipping/export processing who receive, track, print, and send certificates of supply in day-to-day business. The secondary target audience is **administrators and key users** who set up the Certificate of Supply setup and the Document Sending Profiles once.

**Brief process overview.** First, the administrator sets up the **Certificate Of Supply Setup** (number series, due date calculation) and a **Document Sending Profile** per customer or vendor. After that, the user works in the **Certificate Of Supplies** list: they select a record and, via an action, trigger the printing or the emailing of the certificate or the reminder. During emailing, this module steps in and provides the recipient, language, and attachments according to the Document Sending Profile.

## Quick start for users

The fastest route from a configured system to a sent Certificate of Supply. Setup (steps 1–2) is a prerequisite and is performed only once per customer or vendor.

1. **Check setup (once):** Open the **Certificate Of Supply Setup** via **Tell Me** and make sure that a number series is set.
2. **Create Document Sending Profile (once per recipient):** Open the **m+m Document Sending Profiles** page via **Tell Me**, create a line with the **Source Type** Customer or Vendor, the appropriate **Source No.**, the **Type** Email, and the **Document Type** for the Certificate of Supply, and fill in the recipient fields.
3. **Open the list:** Open the **Certificate Of Supplies** list (from the m+m Certificate of Supply module).
4. **Select a record:** Select the line to be sent.
5. **Send:** Choose **Mail Certificate Of Supply** (or **Print Certificate Of Supply** for print only).
6. **Review and send the email:** The recipient and attachments are pre-populated according to the Document Sending Profile; check the recipient, subject, and attachments, and send the email.
7. **Follow up:** If the certificate has not been **received** by the **Due Date**, send a reminder via **Send Reminder via Mail**.

## Setup

Setup is the prerequisite for the entire sending process. It consists of two areas that build on each other: the module-wide **Certificate Of Supply Setup** and — per customer or vendor — the **Document Sending Profile**. Both are maintained by the administrator or key user before first use.

### Certificate Of Supply Setup

**Who and when.** This page is a company-wide setup card and is set up once by the administrator before the first Certificate of Supply is created. **Access:** Open the **Certificate Of Supply Setup** via **Tell Me** (company-wide setup, no parent call path).

| Setup | Explanation |
|---|---|
| **Cert. Of Supply Nos.** | If a number series is set here, then every new Certificate of Supply automatically receives a sequential **No.**; without a number series, certificates of supply cannot be numbered and therefore cannot be uniquely sent and tracked. |
| **Default Due Calc. Cert. Sup.** | If a date formula is set here, then for every new Certificate of Supply the **Due Date** is calculated automatically from the shipment/posting date; if the field is empty, the due date remains open and the reminder-level logic has no reference date. |

### Set up Certificate of Supply dispatch

**Process introduction.** This setup enables email and print dispatch of the Certificate of Supply. It is configured by the administrator or key user, specifically **per customer or vendor** for whom certificates are sent. It is used in day-to-day business in the section **Sending and printing the Certificate of Supply**. Without a matching Document Sending Profile, the email dispatch finds no recipient and cannot be executed.

**Access:** Open the **m+m Document Sending Profiles** page via **Tell Me** and run **Edit List**.

Sequence in order of dependency:

1. **First**, set up the Certificate Of Supply Setup (number series, due date formula) — see above.
2. **Then**, create a line in **m+m Document Sending Profiles** for each customer or vendor: select the **Source Type**, enter the **Source No.**, set **Type** and **Document Type**, and maintain recipients and attachments.
3. **Finally**, in day-to-day business, trigger the dispatch in the **Certificate Of Supplies** list via **Mail Certificate Of Supply**; the module pulls the profile created here automatically.

The documents for which this module enables dispatch are the **Certificate of Supply** and the **Certificate of Supply reminder**. Set the **Document Type** in the profile to the respective Certificate of Supply document accordingly, so that the correct profile is pulled.

#### Fields of the m+m Document Sending Profiles page

The following table documents all fields of the Document Sending Profile line. For the Certificate of Supply, the key fields are above all **Source Type**, **Source No.**, **Type**, **Document Type**, and the recipient and attachment fields.

| Setup | Explanation |
|---|---|
| **Source Type** | Determines the group of business partners the profile applies to. **General:** The profile applies independently of a specific partner. **Customer:** If chosen, then the profile applies to a single customer and the **Source No.** must be specified. **Vendor:** If chosen, then the profile applies to a single vendor and the **Source No.** must be specified. A separate line must be created for each customer or vendor. |
| **Source No.** | If Customer or Vendor is chosen as the source type, then the number entered here determines the specific business partner for whom the profile is pulled during dispatch; the selection automatically fills the **Source Name**. |
| **Source Name** | Shows the name of the selected customer or vendor so that the line can be uniquely identified without a lookup. |
| **Reference Type** | Optional refinement of the scope. **(empty):** If empty, then the profile applies without an additional reference. **Deliverer:** If chosen, then the profile is additionally related to a deliverer and the **Reference No.** must be specified. |
| **Reference No.** | If a reference type is set, then this number specifies the reference (e.g. the deliverer) to which the profile is additionally narrowed. |
| **Type** | Controls the sending channel. **Email:** If chosen, then the document is sent as an email. **Print:** If chosen, then the document is printed. **Print & E-Mail:** If chosen, then printing and email dispatch occur together. |
| **Document Type** | Determines the document for which the profile applies. For this module, the document type must be set to the Certificate of Supply document so that exactly this profile is pulled when sending from the **Certificate Of Supplies** list. |
| **Responsibility Code** | If a code is set, then all contacts of this responsibility are pre-populated as **To** recipients; this allows a group of people to be addressed without maintaining individual addresses. |
| **Responsibility Description** | Shows the description of the selected responsibility code. |
| **CC** | If a responsibility is set here, then its contacts are pre-populated as **CC** recipients of the email. |
| **BCC** | If a responsibility is set here, then its contacts are pre-populated as **BCC** recipients of the email. |
| **Additional To** | If addresses are stored here, then these are additionally transferred into the **To** field; this allows recipients to be addressed who are not maintained as a contact of the customer or vendor. |
| **Additional CC** | Like **Additional To**, but the addresses are transferred into the **CC** field. |
| **Additional BCC** | Like **Additional To**, but the addresses are transferred into the **BCC** field. |
| **No. Of Attachments** | Shows the number of additional attachments stored. If you click in the field, then the attachment list opens, in which additional documents or files are selected for dispatch; the actual document is always attached and is not counted here. |
| **Additional To Default** | Controls which recipients are pre-populated in the **To** field. **Standard:** If chosen, then only the addresses from the Document Sending Profile are set. **Yes:** If chosen, then the addresses from the profile plus those from the BC standard logic are set. **Question:** If chosen, then a dialog prompts during dispatch; confirming acts like **Yes**, declining acts like **Standard**. **Just Standard:** If chosen, then only the addresses of the BC standard logic are set. The setting affects only the **To** field, not CC and BCC. |
| **ZIP Option** | Controls the bundling of attachments. **None:** If chosen, then no ZIP folder is created. **All:** If chosen, then all documents and files are packed into a ZIP folder. **Just Attachments:** If chosen, then only the additional files (not the document itself) are packed into a ZIP folder. |
| **Max. MB** | If a value is set here, then an email whose attachments exceed this limit is automatically split into several numbered partial emails; if a single file already exceeds the limit, then an error message appears. This prevents emails from remaining undeliverable due to attachments that are too large. |
| **Additional To** / **Additional CC** / **Additional BCC** (display) | The three display fields summarize the additional addresses stored per distribution field and make them directly visible in the list. |

**Dependency note.** During email dispatch, the module selects the profile by priority based on Source Type, Source No., and Document Type (in the background via Report Dispatch). If a profile with the matching Document Type is missing for the customer or vendor, the email dispatch finds no recipient. The **Language Code** for the email is drawn automatically from the customer or vendor.

## Sending and printing the Certificate of Supply

This section describes day-to-day business. It assumes the profiles created in the **Setup** chapter (cross-reference: **Set up Certificate of Supply dispatch**).

**Access.** Open the **Certificate Of Supplies** list (from the m+m Certificate of Supply module). Each line is a Certificate of Supply for a Sales Shipment.

### Fields of the Certificate Of Supplies list

The most important fields for dispatch and tracking:

| Field | Explanation |
|---|---|
| **Document Type** | Source document type of the certificate. **Sales Shipment:** Certificate for a posted sales shipment (the case supported by this module). **Service Shipment:** Certificate for a service shipment. **Return Shipment:** Certificate for a return shipment. |
| **Document No.** | If set, then the number refers to the underlying shipment document; through it the module determines the associated document record during dispatch. |
| **Status** | Shows the processing state of the certificate (Not Applicable, Required, Received, Not Received). The status is controlled by the actions **Received Certificate of Supply** and **Undo Received Certificate of Supply** as well as by the due date/reminder logic, and is read-only. |
| **No.** | Sequential number from the number series of the Certificate Of Supply Setup; uniquely identifies the certificate. |
| **Printed** | If set, then the certificate has already been printed; used to verify whether the proof reached the recipient. |
| **Customer/Vendor No.** | Number of the business partner; through it the module pulls the appropriate Document Sending Profile and the language code during email dispatch. |
| **Customer/Vendor Name** | Name of the business partner for quick identification of the line. |
| **Delivery Term Code** | Delivery term of the underlying shipment; a functional component of the proof. |
| **Shipment/Posting Date** | Date of the shipment/posting; the starting point for the due date calculation. |
| **Due Date** | Date by which the certificate should be received; calculated from the shipment/posting date and the default due date formula. After it has passed, a **Reminder** is indicated. |
| **Reminder Level** | Shows how often a reminder has already been sent; controls escalation via the reminder actions. |
| **Vehicle Registration No.** | Registration or tax number of the transport vehicle; a functional proof field. |
| **Certification No.** | If set, then this number bundles several combined certificates; the basis for collective printing and collective reminder. |
| **Certification Date** / **Received Date** / **Goods Receipt Date** | Date information for the certificate, the confirmed receipt, and the goods receipt; they document the chronological sequence of the proof. |
| **Invoice No.** / **Shipment/Posting Date** | Reference to the associated invoice and the document date. |
| **Type** | Indicates whether it is a **Customer** or a **Vendor**; determines whether a customer or vendor profile is pulled during dispatch. |
| Address fields **Ship-to Name/Address/City/Post Code/Country**, **Bill-to Name/Address/City/Post Code/Country**, contact and code | These read-only address fields reflect the ship-to and bill-to address from the underlying document and appear on the printed proof. They are grouped together here because they serve only for display and are not controlled by this module. |

### Actions for sending and printing

The following list actions trigger printing or dispatch. Email dispatch uses m+m Report Dispatch; this module provides the recipient, language, and attachments in the process.

| Action | Explanation |
|---|---|
| **Print Certificate Of Supply** | Prints the certificate of the selected line. Afterwards sets the **Printed** field. |
| **Mail Certificate Of Supply** | Sends the certificate of the selected line as an email via Report Dispatch; recipient, language, and attachments are pre-populated from the Document Sending Profile of the customer or vendor. |
| **Combine Certificate Of Supply** | Combines several selected certificates under a common **Certification No.** so that they can be printed or sent in a bundle. |
| **Batch Print Certificate of Supply** | Prints all certificates combined under one **Certification No.** in a single operation. |
| **Mail Combine Certificate Of Supply** | Sends the combined certificates of one **Certification No.** in a single email. |
| **Reminder** | Prints a Certificate of Supply reminder for the overdue selected lines and increases the reminder level. |
| **Send Reminder via Mail** | Sends the Certificate of Supply reminder as an email via Report Dispatch. |
| **Combine Reminder** | Prints a combined reminder across several certificates. |
| **Mail Combine Reminder** | Sends the combined reminder as an email. |
| **Received Certificate of Supply** | Marks the certificate as received and sets the associated status; the **Received Date** is set. Afterwards, no reminder is needed. |
| **Undo Received Certificate of Supply** | Undoes the "received" mark; incorrectly confirmed lines are returned to tracking. |

### Sequence during email dispatch

When you choose **Mail Certificate Of Supply**, the following chain runs in the background:

1. The module determines the associated document (the **Sales Shipment**) for the attachment for the Certificate of Supply.
2. Based on **Type** (Customer/Vendor) and **Customer/Vendor No.**, the appropriate **Document Sending Profile** is selected by priority.
3. Recipients (**To**, **CC**, **BCC**, additional recipients) and the **Language Code** are pre-populated from the profile and the business partner.
4. Report Dispatch creates the email with the attachments according to the profile (**No. Of Attachments**, **ZIP Option**, **Max. MB**).
5. Before sending, you can review and, if necessary, adjust the recipient, subject, message text, and attachments; then you send the email.

## Permissions

The permission set **MuM CSRD All** is available for the module. It defines the permissions for executing the module-internal logic that enables dispatch of the Certificate of Supply via Report Dispatch. Assign this permission set to all users who are to send or print certificates of supply. In addition, users need the permissions of the m+m Certificate of Supply and m+m Report Dispatch modules for the pages and Document Sending Profiles located there.

## FAQ and troubleshooting

### Why is no recipient suggested during email dispatch?
Because no **Document Sending Profile** with a matching **Document Type** has been created for the relevant customer or vendor. The module selects the profile by Source Type, Source No., and Document Type; without a matching line it finds no recipient. Create the profile in **m+m Document Sending Profiles**.

### What happens if I choose the "print" action instead of "mail"?
Then the Certificate of Supply is only printed and the **Printed** field is set. Report Dispatch and this module's recipient determination are not activated in that case.

### In which language is the email created?
In the recipient's language: the module draws the **Language Code** automatically from the customer or vendor of the Certificate of Supply.

### Why can't I create a collective profile for "all customers"?
Because a separate profile line is required per customer or vendor. Choose Customer or Vendor as the **Source Type** and enter the specific **Source No.**; a profile "for all customers" is not provided.

### How do I ensure that additional documents are sent as well?
Via the **No. Of Attachments** field in the Document Sending Profile. Click in the field and store the additional documents or files there; the actual proof is attached anyway.

### What does the "Additional To Default" setting do?
It controls only the **To** field: **Standard** uses only the profile addresses, **Just Standard** only the BC standard addresses, **Yes** both together, and **Question** prompts during dispatch. The setting has no effect on CC and BCC.

### Why is my email split into several parts?
Because the total of the attachments exceeds the **Max. MB** value. Report Dispatch then splits the email into numbered partial emails. If a single file already exceeds the limit, an error message appears.

### When does a reminder become due?
When the **Due Date** has been exceeded and the certificate has not yet been marked as **received**. The due date results from the shipment/posting date and the **Default Due Calc. Cert. Sup.** from the Certificate Of Supply Setup.

### How do I combine several certificates for one recipient?
Select the lines and choose **Combine Certificate Of Supply**. The certificates receive a common **Certification No.** and can then be sent in a bundle via **Batch Print Certificate of Supply** or **Mail Combine Certificate Of Supply**.

### I accidentally marked a certificate as received – how do I correct that?
Choose **Undo Received Certificate of Supply**. The mark is removed and the line returns to tracking.

## Typical use cases

### Use case 1: Sending a Certificate of Supply to a customer by email

**Trigger.** A shipment to a customer in another EU country has been posted; the tax proof (Certificate of Supply) is to be delivered to the customer by email.

**Access in BC.** The administrator has previously created a line in **m+m Document Sending Profiles** with **Source Type** Customer, the customer's **Source No.**, **Type** Email, and the matching **Document Type**. The user opens the **Certificate Of Supplies** list.

**Core sequence.**
1. The user selects the line with the **Document Type** Sales Shipment and the matching **Customer/Vendor No.**.
2. They choose **Mail Certificate Of Supply**.
3. The module determines the associated Sales Shipment, pulls the customer's Document Sending Profile, and pre-populates the recipient and **Language Code**.
4. The user checks the recipient, subject, and attachments, and sends the email.

**Conclusion.** As soon as the customer confirms the proof, the user marks the line via **Received Certificate of Supply**; the **Received Date** is set and a reminder is not needed.

### Use case 2: Reminding of an overdue certificate

**Trigger.** The **Due Date** of a Certificate of Supply has been exceeded and the **Status** still indicates that the proof has not been received.

**Access in BC.** The user opens the **Certificate Of Supplies** list and filters or sorts by **Due Date** and **Reminder Level**.

**Core sequence.**
1. The user selects the overdue line.
2. They choose **Send Reminder via Mail** (or **Reminder** for print only).
3. The module sends the **Certificate of Supply reminder** via Report Dispatch to the recipient from the Document Sending Profile; the **Reminder Level** is increased.

**Conclusion.** If the proof then arrives, the user marks the line via **Received Certificate of Supply**. For several overdue certificates of the same recipient, a bundled reminder can be sent beforehand via **Combine Certificate Of Supply** and **Mail Combine Reminder**.
