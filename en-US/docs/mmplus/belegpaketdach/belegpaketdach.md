---
title: Anwenderhandbuch m+m Report Package DACH
---

# User Guide m+m Report Package DACH

## Introduction

The **m+m Report Package DACH** app extends the document and reporting capabilities of Microsoft Dynamics 365 Business Central with an additional, DACH-specific document: the printed **Delivery Reminder** to your vendors. It builds on the **m+m Report Package** base module and closes the gap left in that base module's standard scope — namely a ready-made purchase report for the **Issued Delivery Reminder**.

Specifically, the app delivers two things:

1. The **Purchase - Report DACH** report (report ID **5613062**), which can be used to print an issued delivery reminder to the vendor or send it by e-mail.
2. Three additional code fields on the header of the Delivery Reminder and the Issued Delivery Reminder — **Purchaser Code**, **Clerk Code** and **Field Worker Code** — with which you specify which internal person appears as the contact person on the printed document.

**Target audience.** This guide is primarily aimed at **operational users in Purchasing** who process, issue and send delivery reminders to vendors. For them, the daily routine is extended by the three code fields on the document header and by printing the DACH report. Secondarily addressed are **administrators and key users** who perform the one-time report selection and report setup so that printing is available at all.

**Scope of the app.** The app extends only the document handling around the delivery reminder. It contains no setup pages of its own, no master data cards and no inventory or posting logic. The layout of the documents (header, footer, logo position and further print options) is maintained centrally in the base module via the **Report Setup** page; the assignment of the report ID is done in **Report Selection – Comfort Purch.**

## Quick Start for Users

The shortest path from an overdue purchase order to a printed reminder to the vendor:

1. **Check setup (one-time, by administrator).** Make sure that report ID **5613062** is entered in **Report Selection – Comfort Purch.** for the DACH purchase area. Without this assignment, the **Purchase - Report DACH** printout is not available. Layout options (e.g. logo position, footer) are maintained in the **Report Setup**.
2. **Open the delivery reminder.** Open the **Delivery Reminders** list and select the relevant **Delivery Reminder** (or create a new one).
3. **Set the contact person (optional).** On the document header, open the **m+m Belegpaket** FastTab and, if required, enter the **Purchaser Code**, **Clerk Code** and **Field Worker Code**.
4. **Issue.** Issue the delivery reminder using the standard action. This turns the Delivery Reminder into an **Issued Delivery Reminder**.
5. **Print or send.** Open the **Issued Delivery Reminder** and print or send it with the **Purchase - Report DACH** layout. The entered **Purchaser Code** determines the contact person in the document header.

The order is deliberate: the setup (step 1) is a prerequisite before the printout in step 5 can succeed.

## Prerequisites and Setup

For the DACH printout of a delivery reminder to work, two central setup pages of the base module are relevant. Both are company-wide setups (one record per company) and are maintained by the administrator or key user. This app itself brings no setup fields of its own; it **uses** the base module's setup and merely provides the additional report ID **5613062**.

### Setting Up Report Provisioning

**Who and when.** This setup is performed once by the administrator before first use. Only afterward can users print an issued delivery reminder in the DACH layout in the daily routine (see **Codes on the Document Header** and **Purchase - Report DACH**).

**Sequence in dependency order:**

1. **Open Report Setup.** Use **Search** to open the **Report Setup** page (m+m Report Package base module). Here you define the company-wide layout options for all m+m documents — such as logo position, footer contents, whether the document number appears as a barcode and whether lot/serial numbers are printed. If you set these options, they also affect the printout of the delivery reminder; without maintenance, the base module's default settings apply.
2. **Open Report Selection – Comfort Purch.** Use **Search** to open the **Report Selection – Comfort Purch.** page. Enter report ID **5613062** for the DACH purchase area. If this ID is set, the DACH layout **Purchase - Report DACH** is used when printing an issued delivery reminder; if the assignment is missing, the document cannot be printed in this layout.
3. **Maintain codes on the document header (optional, in the daily routine).** The last step lies with the operational user: they enter the desired contact-person codes on the delivery reminder (see the next chapter). This closes the chain from setup to use.

**Completing the chain.** The operational action that makes this setup usable is the **printing** or **e-mail dispatch** of the issued delivery reminder in the **Purchase - Report DACH** chapter.

### Permissions

The app ships with the assignable permission set **MuM RPD All**. It determines the permissions for the objects provided by this app and defines which actions users may perform with them: run the **Purchase - Report DACH** report, run the preparatory data-management report and use the associated processing logic.

| Setup | Explanation |
|---|---|
| Permission set **MuM RPD All** | If this permission set is assigned to a user or user group, they may run and print the DACH delivery reminder. Without the assignment, the report objects provided by this app are not available to the user, and the **Purchase - Report DACH** printout cannot be started. |

## Codes on the Document Header

The app adds the **m+m Belegpaket** FastTab with three code fields to the header of the **Delivery Reminder** and — identically — to the header of the **Issued Delivery Reminder**. Through these fields you control which internal person appears as the contact person in the header of the printed document.

**Who and when.** These fields are maintained by the operational user in Purchasing while processing the delivery reminder — before issuing, so that the details are carried over to the issued document and printed with it. All three fields refer to the **Salespeople/Purchasers** table; only codes created there can be selected.

**Getting started:** Open the **Delivery Reminders** list, open the desired **Delivery Reminder** and switch to the **m+m Belegpaket** FastTab on the document header. After issuing, you find the same fields again on the **Issued Delivery Reminder**.

| Field | Explanation |
|---|---|
| **Purchaser Code** | If you set a code from **Salespeople/Purchasers** here, then exactly this purchaser is carried over to the document header as the contact person when the issued delivery reminder is printed: name, direct phone number and contact e-mail are pulled from the record and printed in the header area (**Contact Person:**, **Phone Extension:**, **Contact (E-mail):**). Without an entry, this contact-person block remains empty on the document. |
| **Clerk Code** | If you enter a code from **Salespeople/Purchasers** here, you document the responsible internal clerk on the document header. The value is retained when issuing and is available on the issued delivery reminder for internal tracking. |
| **Field Worker Code** | If you enter a code from **Salespeople/Purchasers** here, you assign the document to the responsible field worker. The value is carried over to the issued delivery reminder and serves the internal allocation of the transaction. |

**Interaction with the printout.** Of the three fields, the **Purchaser Code** directly controls the contact-person block of the printout (see the **Purchase - Report DACH** chapter). **Clerk Code** and **Field Worker Code** serve internal allocation and tracking. When issuing, the values are transferred from the delivery reminder to the issued delivery reminder, so that the historical, issued document carries the same details.

## Purchase - Report DACH

The **Purchase - Report DACH** (report ID 5613062) is the printable layout of the issued delivery reminder to the vendor. It is not started via **Search**; instead, it is automatically used as the layout when printing or e-mailing an **Issued Delivery Reminder**, as soon as the report ID is entered in **Report Selection – Comfort Purch.** (see **Setting Up Report Provisioning**).

**Getting started:** Open the **Issued Delivery Reminders** list, select the document and start the print or e-mail dispatch. If no selection is set, only the previously marked documents are printed.

### Content of the Document Header

In the header, the report assembles the details customary for a vendor delivery reminder. They originate from the issued delivery reminder, from the vendor master and — for the contact person — from the record selected via **Purchaser Code**.

| Field on the document | Explanation |
|---|---|
| **Y/Vendor No.:** | The number under which you are managed at the vendor (from the vendor master). Only printed when entered. |
| **Document Date:** | The document date of the issued delivery reminder, formatted according to language. |
| **Posting Date:** | The posting date of the issued delivery reminder. |
| **Your VAT No.:** | The VAT registration number of the vendor, if available. |
| **Our Vendor No.:** | Your own account number at the vendor (from the vendor master). |
| **Your Reference:** | The reference from the document. If the "Change Your Reference to Your Sign" option is active in the Report Setup, the label **Your Sign:** appears instead. |
| **Reminder Level:** | The reminder level of the issued delivery reminder. |
| **Contact Person:** | The name of the purchaser selected via **Purchaser Code**. Only filled when a purchaser code is set. |
| **Phone Extension:** | The phone number of this purchaser. |
| **Contact (E-mail):** | The e-mail address of this purchaser. |
| **No.** (or barcode) | The document number of the issued delivery reminder. If "Document No. as Barcode" is active in the Report Setup, the number is displayed as a barcode; otherwise as text under the label **No.** |

### Content of the Document Lines

In the lines, the report lists the reminded positions of the underlying issued delivery reminder. For each overdue position, the following columns, among others, are printed:

| Column | Explanation |
|---|---|
| **Pos.** | The consecutive position number of the reminded line. |
| **No.** | The document number the reminder line refers to (e.g. the purchase order number). |
| **Description** | The description of the reminded position; additional description lines and text modules are printed as well. |
| **Quantity** | The ordered or reminded quantity. |
| **Unit** | The unit of measure of the position. |
| **Rem. Qty** | The quantity of the purchase order line still open. |
| **Level** | The reminder level of the respective position. |
| **Delivery Date** | The delivery date relevant for the reminder. Depending on the line's setting, the requested, the promised or the expected receipt date is used. |

If a position is overdue, the report adds a note **due since … days**. In addition — where present in the purchase order — your reference, the vendor order number and the vendor shipment number are printed as explanatory lines. Beginning and ending texts of the reminder method (**Delivery Reminder Term:**) are also carried over.

### Request Page of the Report

When the report is called manually, three options are available in the **General** area:

| Setup | Explanation |
|---|---|
| **No. Of Copies** | If you enter a value greater than 0 here, then in addition to the original a corresponding number of copies marked as **COPY** are printed; at 0, only the original is output. |
| **Show internal Information** | If activated, additional internal details (e.g. dimension and VAT details) are printed as well; if the option is not set, the document is limited to the details intended for the vendor. |
| **Log Interactions** | If activated, the printout is logged as a contact interaction; without the option, no logging of the transaction takes place. |

## Typical Use Cases

### Case 1 – Remind an overdue delivery and send the DACH document

1. **Trigger.** A purchase order is overdue; Purchasing decides to remind the vendor in writing.
2. **Entry in BC.** Open the **Delivery Reminders** list and open or create the relevant **Delivery Reminder**.
3. **Core process.** Switch to the **m+m Belegpaket** FastTab on the document header and set the **Purchaser Code** to the responsible purchaser; if required, add **Clerk Code** and **Field Worker Code**. Then issue the delivery reminder — an **Issued Delivery Reminder** is created.
4. **Completion.** Open the **Issued Delivery Reminder** and print or send it in the **Purchase - Report DACH** layout. The selected purchaser appears in the header as **Contact Person:** with **Phone Extension:** and **Contact (E-mail):**; the lines show the overdue positions with the note **due since … days**. The prerequisite is the one-time setup as described in **Setting Up Report Provisioning**.

### Case 2 – Show a clear contact person for queries

1. **Trigger.** A vendor gets in touch with queries about a reminder received and wants to know whom to contact.
2. **Entry in BC.** Open the relevant **Delivery Reminder** (or, for documents already issued, the **Issued Delivery Reminder**).
3. **Core process.** On the **m+m Belegpaket** FastTab, check or set the **Purchaser Code** so that the desired internal contact person is entered. Their name, phone extension and e-mail are pulled from **Salespeople/Purchasers**.
4. **Completion.** When the issued delivery reminder is printed again in the **Purchase - Report DACH** layout, the updated contact-person block appears in the document header, so that the vendor sees the correct contact.

## FAQ and Troubleshooting

### Why is the "Purchase - Report DACH" printout not available?
Because report ID **5613062** has not yet been entered in **Report Selection – Comfort Purch.** for the DACH purchase area. Without this assignment, the DACH layout does not take effect. Enter the ID (see **Setting Up Report Provisioning**).

### What is the app for in the first place?
It extends the m+m Report Package base module with a document missing in the standard: the printed purchase report for the **Issued Delivery Reminder**. In addition, it brings three contact-person codes to the document header.

### What happens if I do not set a Purchaser Code?
Then the contact-person block in the header of the printed document remains empty: neither **Contact Person:** nor **Phone Extension:** nor **Contact (E-mail):** is printed. The rest of the document is still printed in full.

### Where do the name, phone and e-mail of the contact person come from?
From the record in **Salespeople/Purchasers** selected via the **Purchaser Code**. The report reads the name, phone number and e-mail address from there.

### Where do I maintain the logo, footer and further print options?
Not in this app, but centrally in the **Report Setup** of the base module. The options set there also affect the delivery reminder.

### Why does the label "Your Sign:" appear instead of "Your Reference:"?
Because the "Change Your Reference to Your Sign" option is activated in the **Report Setup**. Then the report prints the reference under the label **Your Sign:**.

### Why do I see the three code fields again on the issued reminder?
Because the values are carried over from the delivery reminder to the **Issued Delivery Reminder** when issuing. This way the historical document carries the same details and can be reprinted unchanged.

### What does the addition "due since … days" in the lines mean?
It is printed for every overdue position and indicates how many days the delivery is already overdue. If a position is not overdue, the note does not appear.

### How do I generate additional copies of the document?
Enter the desired number under **No. Of Copies** on the report's request page. The copies are printed in addition to the original and marked with **COPY**.

### Which permission do I need to print the report?
You need the permission set **MuM RPD All** (or an assignment that includes it). It makes the report objects provided by the app available for execution; without this permission, the **Purchase - Report DACH** cannot be started.
