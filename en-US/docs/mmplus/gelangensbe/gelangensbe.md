---
title: Anwenderhandbuch m+m Certificate of Supply
---

# User Guide m+m Certificate of Supply

## Introduction

The **m+m Certificate of Supply** extension enhances Microsoft Dynamics 365 Business Central with the complete processing of the **Certificate of Supply** (Gelangensbestätigung). For intra-Community supplies, a Certificate of Supply proves that the goods have actually reached another EU member state. This proof is a prerequisite for the tax exemption of the supply.

The extension creates Certificates of Supply **automatically when posting** shipment documents and provides a dedicated **Certificate Of Supplies** list in which the documents are combined, printed, sent by email, reminded, and set to **Received**. Three document types are affected:

- **Sales Shipment** (customer)
- **Service Shipment** (customer)
- **Return Shipment** from purchasing (vendor)

**Target audience.** The primary users are the **operational clerks** in sales, shipping, and accounts receivable/payable who print, send, set to Received, and remind open Certificates of Supply on a daily basis. **Administrators** and key users are the secondary audience; they set up the number series, due date formulas, and the triggering VAT indicator.

**Brief process overview.** The user posts a shipment as usual. If the **Certificate of Supply Required** indicator is set for the line's VAT combination, the extension automatically creates a Certificate of Supply with status **Required**. In the **Certificate Of Supplies** list, the user optionally combines the documents per recipient into a **Certification No.**, prints them or sends them by email, and sets them to **Received** once they are returned. Certificates that are not returned are followed up via **Reminder** and **Combine Reminder**.

## Quick Start for Users

The quick start describes the shortest path from a configured system to a received Certificate of Supply. Setup is a prerequisite and therefore comes first (see chapter **Setup**).

1. **Check setup (one-time, administrator).** In the **Certificate Of Supply Setup**, a **Cert. Of Supply Nos.** number series and a **Default Due Calc. Cert. Sup.** are entered; in the **VAT Posting Setup**, **Certificate of Supply Required** is activated for the affected combinations.
2. **Post shipment.** Post a **Sales Shipment**, **Service Shipment**, or **Return Shipment** in standard Business Central. For lines with the **Certificate of Supply Required** indicator, a Certificate of Supply with status **Required** is created automatically.
3. **Open list.** Enter the term `Certificate Of Supplies` via **Search** and open the link of the same name. The **Certificate Of Supplies** list appears.
4. **Combine (optional).** Select several lines of the same recipient and choose **Combine Certificate Of Supply**. All selected documents receive the same **Certification No.** and can be printed together.
5. **Print.** Choose **Print Certificate Of Supply** (single document) or **Batch Print Certificate of Supply** (combined documents). Printing sets the status to **Not Received**, records the **Certification Date**, and determines the **Due Date**.
6. **Send (as an alternative to printing).** Choose **Mail Certificate Of Supply** or **Mail Combine Certificate Of Supply**.
7. **Post receipt.** When the signed confirmation comes back, select the line(s) and choose **Received Certificate of Supply**. The status changes to **Received** and the **Received Date** is set.
8. **Send reminder (when overdue).** For overdue documents, choose **Reminder** or **Combine Reminder**, or their mail variants.

## Setup

Setup takes place before first use and in dependency order: first the **Certificate Of Supply Setup** (number series, default due date), then, as needed, the **due date formula on the shipment method**, and finally the triggering indicator in the **VAT Posting Setup**. The print and mail report assignments are set up automatically during installation.

### Certificate Of Supply Setup

**Entry point:** Enter the term `Certificate Of Supply Setup` via **Search** and open the link of the same name. This is a company-wide setup card (one record per company); it is created automatically the first time it is opened.

**Process.** Here the administrator sets up, once, the central defaults that apply to **all** Certificates of Supply: the number series for combined documents and the default setting for the due date. These values take effect later when combining (chapter **Application**) and when determining the due date (chapter **Set up due date and reminders**).

| Setup | Explanation |
|-------------|-------------|
| **Cert. Of Supply Nos.** | If a number series is entered, a sequential **Certification No.** per recipient group is assigned automatically when **combining** several Certificates of Supply; without a number series, combining is not possible, and the **Combine Certificate Of Supply** call aborts with an error message. |
| **Default Due Calc. Cert. Sup.** | If a date formula (e.g. `14D`) is set, the **Due Date** is calculated as the work date plus the formula when a Certificate of Supply is printed; from this date on, the certificate is considered overdue and enters the reminder run. If the respective **Shipment Method** has its own due date formula entered, that formula takes precedence. If no formula at all is entered, the work date is used as the due date. |

### Due Date Formula on the Shipment Method

**Entry point:** Enter the term `Shipment Methods` via **Search** and open the link of the same name. Edit the desired **Shipment Method** directly in the line.

**Process.** Here the administrator defines whether a specific shipment method should receive a **differing** due date. For this, the extension adds an additional field to the shipment method. This per-shipment-method formula overrides the central **Default Due Calc. Cert. Sup.** from the Certificate Of Supply Setup and takes effect when printing (chapter **Application**).

| Field | Explanation |
|------|-------------|
| **Code** | Identifies the shipment method (standard field). It is transferred to the Certificate of Supply as the **Shipment Method Code** and controls which due date formula applies. |
| **Description** | Plain-text designation of the shipment method (standard field). |
| **Due Date Calculation (Cert. of Supply)** | If a date formula is set here, the **Due Date** of Certificates of Supply with this shipment method is calculated using this formula and overrides the central default formula; if the field is empty, the **Default Due Calc. Cert. Sup.** of the Certificate Of Supply Setup applies. If the field is not visible in the view, show it via **Personalize**. |

### Setting Up Automatic Creation of Certificates of Supply

For Certificates of Supply to be created at all, the administrator must set the triggering indicator in the VAT Posting Setup. Without this step, the user posts shipments but no certificates are created.

1. **Open VAT Posting Setup.** Enter the term `VAT Posting Setup` via **Search** and open the link of the same name. The matrix contains, per line, a combination of **VAT Bus. Posting Group** and **VAT Prod. Posting Group**.
2. **Set the triggering indicator.** For each affected combination, activate the **Certificate of Supply Required** field.

   | Setup | Explanation |
   |-------------|-------------|
   | **VAT Bus. Posting Group** | Together with the product posting group, determines for which business transactions the rule applies (standard field). |
   | **VAT Prod. Posting Group** | Complements the business posting group to form the unique combination (standard field). |
   | **Certificate of Supply Required** | If activated, Business Central automatically creates a Certificate of Supply with status **Required** for lines of this VAT combination when a shipment is posted; if the indicator is not set, no certificate is created. In addition, when the indicator is active, the extension prevents **direct invoicing** without a separate shipment (see the process note below). If the field is not visible, show it via **Personalize**. |
3. **Effect in daily operations.** After setting the indicator, a line is created automatically in the **Certificate Of Supplies** list (chapter **Application**) for every posted **Sales Shipment**, **Service Shipment**, or **Return Shipment** with a matching VAT combination.

**Process note (validation from the code).** If **Certificate of Supply Required** is set for a line, Business Central does not allow **direct invoicing** (posting with invoice without a separate shipment); the document must first be **shipped** and then invoiced. Otherwise an error message appears advising you to use the path via the sales invoice. This ensures that a Certificate of Supply is created for every tax-exempt supply.

### Set Up Due Date and Reminders

This setup controls **when** a Certificate of Supply is considered overdue and appears in reminders. It is performed by the administrator before first use and takes effect in daily work during printing and the reminder actions (chapter **Application**).

1. **Define central due date.** Enter the **Default Due Calc. Cert. Sup.** (e.g. `14D`) in the **Certificate Of Supply Setup**. When set, the **Due Date** is calculated from it during printing.
2. **Differing due date per shipment method (optional).** Enter the **Due Date Calculation (Cert. of Supply)** on individual **Shipment Methods**. When set, it overrides the central formula for documents with this shipment method.
3. **Number series for combined documents.** Enter the **Cert. Of Supply Nos.** in the Certificate Of Supply Setup so that a **Certification No.** can be assigned when **combining**.
4. **Completion in daily operations.** The user prints certificates (setting status **Not Received** and **Due Date**) and reminds overdue documents via **Reminder**/**Combine Reminder**; the **Do increase Reminder Level** field on the request page increases the **Reminder Level** (cross-reference: chapter **Application**).

### Assigning Reports

For printing and mailing, the extension uses two of its own m+m reports: one for the **Certificate Of Supply** and one for the **Reminder Certificate Of Supply**. This report assignment is created automatically during the **installation** of the extension; a manual setup step is normally not required. If differing or multilingual layouts are to be used (the Certificate of Supply is additionally available in French), the administrator adjusts the assignment in the standard report selection of Business Central.

## Application — Daily Work with Certificates of Supply

Once Certificates of Supply have been created from posted business transactions, the user processes them in the **Certificate Of Supplies** list.

**Entry point:** Enter the term `Certificate Of Supplies` via **Search** and open the link of the same name. Business Central displays the **Certificate Of Supplies** list provided by the extension, showing all created certificates.

**Relationship to setup.** Which lines appear here is controlled by the **Certificate of Supply Required** indicator in the **VAT Posting Setup**; the **Due Date** results from the due date formulas of the **Certificate Of Supply Setup** or the **Shipment Method**; the **Certification No.** originates from the **Cert. Of Supply Nos.** number series (chapter **Setup**).

### Fields of the Certificate Of Supplies List

The list is read-only; all values are transferred from the posted shipment document or set by the actions.

| Field | Explanation |
|------|-------------|
| **Document Type** | Source document type of the certificate. **Sales Shipment:** from a posted sales shipment (customer). **Service Shipment:** from a posted service shipment (customer). **Return Shipment:** from a posted return shipment in purchasing (vendor). The document type determines from which source document the address and quantity data originate. |
| **Document No.** | Number of the posted shipment document to which the certificate belongs. Together with the document type, it uniquely identifies the certificate. |
| **Status** | Controls the processing state and the permitted follow-up actions. **Not Applicable:** no Certificate of Supply required; the **No.** field and the **Certification No.** remain empty. **Required:** the certificate is created but not yet printed; it can be combined and printed. **Received:** the signed certificate is available; **Received Date** and **Receipt Date** are set, further changes are locked. **Not Received:** the certificate has been printed or sent but has not yet been returned; only this status enters reminders. If the status is manually reset from **Received**, a confirmation prompt appears. |
| **No.** | Document number of the Certificate of Supply. With status **Not Applicable**, the field must be empty; with **Required**, **Received**, or **Not Received**, it must not be empty (validation from the code). |
| **Receipt Date** | Date on which the certificate was set to **Received**. When setting to **Received**, the action transfers the **Shipment/Posting Date**; the receipt date must not be earlier than the shipment/posting date. |
| **Printed** | If set, the certificate has already been printed or sent by email; only then can the receipt be posted. |
| **Customer/Vendor Name** | Name of the recipient, transferred from the source document. |
| **Shipment Method Code** | Shipment method of the source document; controls which **Due Date Calculation (Cert. of Supply)** applies when printing. |
| **Shipment/Posting Date** | Posting date of the underlying shipment; serves as the lower limit for the receipt date. |
| **Ship-to Country/Region Code** | Destination country of the shipment; for intra-Community supplies, the EU member state into which the goods enter. |
| **Customer/Vendor No.** | Number of the recipient; together with the **Ship-to Code**, it forms the group for combining into a **Certification No.** |
| **Vehicle Registration No.** | Vehicle identifier that can be recorded for the proof. With status **Received**, this field can no longer be changed (validation from the code). |
| **Source No.** | Document number of the triggering business transaction, e.g. sales order or purchase order. |
| **Due Date** | Determined during printing from the applicable due date formula; from this date on, the certificate is overdue. |
| **Reminder Level** | Counts how often the certificate has been reminded; increased via the reminder report as needed. |
| **Invoice No.** | Associated invoice number of the business transaction; added when invoicing. |
| **Invoice/Posting Date** | Invoice or posting date of the invoice document. |
| **Certification No.** | Assigned when combining several certificates and entered into all associated lines; enables batch printing and batch sending. |
| **Certification Date** | Date on which the combined document was created or printed. |
| **Received Date** | Date of the receipt confirmation; filled when setting to **Received** and cleared again when resetting. |
| **Type** | Recipient type of the certificate. **Customer:** from a sales or service shipment; address and contact data originate from the bill-to/ship-to address of the customer. **Vendor:** from a return shipment; data originate from the vendor. The type controls to whom the document is printed and mailed and which language code applies to the report. |
| **Ship-to Address** (Ship-to Name, Name 2, Contact, Code, Address, Address 2, City, Post Code, Country) | Read-only ship-to address transferred from the source document; appears in the proof as the place of receipt. It is maintained as a field group, since all values originate together from the document. |
| **Bill-to Address** (Bill-to Name, Name 2, Contact, Address, Address 2, City, Post Code, Country, Country/Region Code) | Read-only bill-to/payment address transferred from the source document; names the confirming customer. It is maintained as a field group. |

The list does not provide its own request or table filters; to narrow it down, users use the standard column filters of Business Central (e.g. by **Status** = `Not Received` for open documents).

### Actions of the Certificate Of Supplies

The following actions are available in the ribbon; the most important are pinned under **Process** or **Report**.

| Action | Explanation |
|--------|-------------|
| **Combine Certificate Of Supply** | Combines the selected certificates with status **Not Applicable** or **Required** per group of **Type**, **Customer/Vendor No.**, and **Ship-to Code**, and assigns a common **Certification No.** from the **Cert. Of Supply Nos.** number series. Afterwards, they can be printed or sent by email directly. A prerequisite is an entered number series. |
| **Print Certificate Of Supply** | Prints the selected single certificate. Printing changes the status from **Required**/**Not Applicable** to **Not Received**, records **Printed**, the **Certification Date**, and determines the **Due Date**. |
| **Batch Print Certificate of Supply** | Prints all certificates combined under a **Certification No.** in one combined document. |
| **Mail Certificate Of Supply** | Sends the single certificate as an attachment by email to the recipient (customer or vendor). |
| **Mail Combine Certificate Of Supply** | Sends the certificates combined under a **Certification No.** together by email. |
| **Received Certificate of Supply** | Sets the selected certificates to status **Received**, fills the **Received Date**, and transfers the **Shipment/Posting Date** as the **Receipt Date**. If the lines belong to a **Certification No.**, a confirmation prompt asks whether **all** documents of this combined document should be changed. |
| **Undo Receivied Certificate of Supply** | Resets the selected certificates from **Received** back to **Not Received**, clears the **Received Date** and **Receipt Date**. For combined documents, the same confirmation prompt applies as when receiving. |
| **Reminder** | Prints a reminder for the selected, not yet received certificates. |
| **Combine Reminder** | Prints a combined reminder for the not yet received certificates combined under a **Certification No.** |
| **Send Reminder via Mail** | Sends the reminder for a single certificate by email. |
| **Mail Combine Reminder** | Sends the combined reminder by email. |

### Posting and Status Flow

This flow mirrors the flow stored in the code and is repeated in the **Quick Start** as well as in **Use Case 1** with the same action names.

1. **Post shipment** (standard Business Central): sales shipment, service shipment, or return shipment. For lines with **Certificate of Supply Required**, a certificate with status **Required** is created automatically.
2. **Combine Certificate Of Supply** (optional): assigns the **Certification No.**
3. **Print Certificate Of Supply** or **Batch Print Certificate of Supply**: the status becomes **Not Received**, **Due Date** and **Certification Date** are set, and **Printed** is recorded.
4. Alternatively or additionally, **Mail Certificate Of Supply** / **Mail Combine Certificate Of Supply**.
5. **Received Certificate of Supply**: status **Received**, **Received Date** and **Receipt Date** are set; for combined documents, the confirmation prompt appears.
6. When overdue: **Reminder** / **Combine Reminder**; the **Do increase Reminder Level** field in the request page increases the **Reminder Level**.

There is no fixed quantity reconciliation ("do not close until the quantity matches"); each certificate is set to Received individually or per certification number.

## Certificate of Supply Report and Reminder

### Certificate Of Supply Report

The **Certificate Of Supply** report generates the official proof form. It is grouped by **Customer/Vendor No.** or ship-to address and **Language Code** and also serves for batch printing. The report is called via the **Print Certificate Of Supply** and **Batch Print Certificate of Supply** actions.

When called, two request options are available:

| Setup | Explanation |
|-------------|-------------|
| **Print Line Details** | If activated, the report additionally prints the shipment lines (Item No., Description, Quantity, Unit of Measure); lines with zero quantity are automatically suppressed. Without activation, only the header confirmation appears. For combined documents (call with **Certification No.**), the detail printout is switched on automatically. |
| **Set As Printed** | If activated, the certificate is also marked as **Printed** in the page preview and set to **Not Received**; without activation, this status update does not occur in the preview. |

When printing, the report determines the **Due Date** via the applicable due date formula, sets **Certification Date** and **Printed**, and updates the status to **Not Received**. The printout is produced in the language of the recipient (language code from the customer or vendor).

### Reminder Certificate Of Supply Report

The **Reminder Certificate Of Supply** report reminds recipients of certificates that have not yet been returned. It considers only certificates with status **Not Received** and is called via **Reminder**, **Combine Reminder**, and their mail variants.

| Setup | Explanation |
|-------------|-------------|
| **Do increase Reminder Level** | If activated, the reminder run increases the **Reminder Level** of the affected certificates by one at the actual printout (not in the preview); without activation, the reminder is printed but the reminder level remains unchanged. |

### Create Certificates of Supply Report

The **Create Certificates of Supply** report subsequently creates certificates for already posted shipments for which no certificate exists yet (e.g. when initially introducing the extension into the existing data). It checks, per document, whether **Certificate of Supply Required** is set for the VAT combination and only then creates a certificate.

| Setup | Explanation |
|-------------|-------------|
| **Create Certificates for Sales Shipments** | If activated, posted sales shipments are considered. |
| **Create Certificates for Return Shipments** | If activated, posted return shipments (purchasing) are considered. |
| **Create Certificates for Service Shipments** | If activated, posted service shipments are considered. |

### Content of the Proof Form

The printed form contains the official confirmation text (singular or plural depending on the number of objects), the name and address of the customer, the reference documents, and — when **Print Line Details** is active — a line table with **Description**, **Item No.**, **Quantity**, and **Unit of Measure**. Sample printouts of the Certificate of Supply and the reminder are available on the official mumdat handbook page.

## FAQ and Troubleshooting

### Why is no Certificate of Supply created after posting a shipment?
Because the **Certificate of Supply Required** indicator is not set in the **VAT Posting Setup** for the VAT combination of the shipment line. The extension automatically creates a certificate only for flagged combinations.

### Why does Business Central report an error during direct invoicing?
If **Certificate of Supply Required** is set, posting with invoice without a separate shipment is blocked because the process must create a Certificate of Supply. Post the shipment first and then invoice via the sales invoice.

### Why can the Combine Certificate Of Supply call not be executed?
Because no **Cert. Of Supply Nos.** number series is entered in the **Certificate Of Supply Setup**. Without a number series, no **Certification No.** can be assigned, and the action aborts with an error message.

### How is the due date determined?
When printing: if a **Due Date Calculation (Cert. of Supply)** is entered on the **Shipment Method**, that formula applies. Otherwise the **Default Due Calc. Cert. Sup.** from the Certificate Of Supply Setup applies. If no formula is entered, the work date is used.

### Why can I not record the receipt date?
The **Receipt Date** is allowed only with status **Received**. It is automatically transferred from the **Shipment/Posting Date** when setting to **Received** and must not be earlier than it. With other statuses, it must remain empty.

### What do the four statuses of a Certificate of Supply mean?
**Not Applicable:** no proof needed. **Required:** created, not yet printed. **Not Received:** printed or sent, but not yet returned. **Received:** the signed certificate is available. Only **Not Received** enters reminders.

### Why does a confirmation prompt appear when setting to Received?
If the certificate belongs to a combined document (shared **Certification No.**), the extension asks whether **all** documents of this certification number should be set to **Received** together. Confirm if the complete combined document has come back.

### Why are my posted legacy shipments not shown in the list?
For shipments posted before the indicator was activated, no certificates are created automatically. Use the **Create Certificates of Supply** report to create them subsequently for the existing data.

### Why does the reminder level not increase after printing the reminder?
The **Reminder Level** increases only if the **Do increase Reminder Level** field is activated in the request page and the report is **actually printed** (not just shown in the preview).

### In which language is the Certificate of Supply printed?
The report uses the **Language Code** of the recipient (customer or vendor). The Certificate of Supply is additionally available in French.

## Typical Use Cases

### Use Case 1: Proving an EU Sales Shipment

**Trigger.** Sales ships goods to a customer in another EU member state; the shipment is tax-exempt and must be substantiated by a Certificate of Supply.

**Entry point in BC.** The clerk posts the **Sales Shipment** in the standard. Since **Certificate of Supply Required** is set for the VAT combination, a certificate with status **Required** is created automatically. Via **Search**, they open the **Certificate Of Supplies** list.

**Core flow.** The clerk selects the associated documents of the customer and chooses **Combine Certificate Of Supply** (shared **Certification No.**). Then they choose **Print Certificate Of Supply** or **Batch Print Certificate of Supply** — the status changes to **Not Received**, and **Due Date** and **Certification Date** are set. Alternatively, they send the form directly to the customer via **Mail Certificate Of Supply**.

**Completion.** When the signed certificate comes back, they select the line and choose **Received Certificate of Supply**; the status becomes **Received**, and **Received Date** and **Receipt Date** are set. The proof is thereby documented.

### Use Case 2: Reminding About Open Certificates

**Trigger.** During the weekly review, accounting finds that several printed Certificates of Supply have not yet come back after the **Due Date** has passed.

**Entry point in BC.** Via **Search**, the clerk opens the **Certificate Of Supplies** list and filters the **Status** column to `Not Received`.

**Core flow.** She selects the overdue documents and chooses **Reminder** (single document) or **Combine Reminder** (combined under a **Certification No.**). In the request page, she leaves **Do increase Reminder Level** activated so that the **Reminder Level** rises per reminder run. For electronic sending, she uses **Send Reminder via Mail** or **Mail Combine Reminder**.

**Completion.** The reminder is printed or mailed, and the **Reminder Level** has increased. When the certificate arrives, she sets the document to **Received** via **Received Certificate of Supply**.

### Use Case 3: Substantiating a Return Shipment to a Supplier

**Trigger.** From purchasing, goods are returned to a supplier in another EU member state; a certificate of supply is required for this as well.

**Entry point in BC.** The purchasing clerk posts the **Return Shipment** in the standard. For flagged VAT combinations, a certificate with **Type** = **Vendor** is created automatically. Via **Search**, they open the **Certificate Of Supplies** list.

**Core flow.** They check the address data transferred from the return shipment, combine several documents of the same supplier via **Combine Certificate Of Supply** if needed, and send the proof to the supplier via **Mail Certificate Of Supply**.

**Completion.** After return, they set the certificate to **Received** via **Received Certificate of Supply**. If the return fails to arrive, they send a reminder via **Reminder**.

## Permissions

The extension ships its own permission set, which bundles read and write rights to the tables and pages of the Certificate of Supply as well as execution rights to the codeunits and reports. The administrator assigns this permission set to the users; it determines the permissions for editing, printing, sending, and following up Certificates of Supply.
