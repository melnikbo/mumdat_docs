---
title: Anwenderhandbuch m+m Report Package
---

# m+m Report Package User Handbook

## Introduction

The **m+m Report Package** module extends Microsoft Dynamics 365 Business Central with extensive options for customizing the **printed and e-mailed documents** (quotes, orders, invoices, shipments, purchase orders, reminders, service documents, accompanying documents, and the associated posted documents). The module does **not** control posting itself; instead, it defines **which content appears in which form** on the documents: header and footer information, company details, bank accounts, salutations, barcodes, position numbers, return reason legends, as well as clerk and field worker details.

**Target audience.** This handbook is aimed primarily at **operational users** who work with documents every day – in sales, purchasing, service, and shipping – who enter documents, maintain lines, and print or e-mail documents. The **Report Setup** and the maintenance of master data (customers, vendors, contacts, salespeople, bank accounts) are secondarily the responsibility of administrators and key users.

**Process overview.** The typical path through the module runs in three stages: first, administration defines company-wide in the **Report Setup** which details are printed. Next, the **master data** is maintained so that document-controlling values (factoring bank, salutation, clerk, number of copies) are automatically carried into the documents. In **daily operation**, users open the documents, check or complete the header and line fields added by the module, and print the document – the printout then follows exactly the stored setup.

## Quick start for users

The fastest way to a correctly customized document:

1. **Open Report Setup.** In the Business Central search (**Search**), enter the term **Report Setup** and open the page of the same name. Define the company-wide printing options (company information, bank printing, lot/serial no., position number behavior of the legends, etc.).
2. **Set up position numbers.** Via **Search**, open the **Position Nos. Setup** and define the step range per document area (sales, purchase, transfer). Then choose the **Refresh Open Documents** action to number existing open documents.
3. **Prepare master data.** On the **Bank Account Card**, flag the factoring banks; on the **Customer Card** and **Vendor Card**, enter the desired number of copies as well as the **Clerk Code** and **Field Worker Code**; and on the **Contact**, maintain the **Report Salutation Code**.
4. **Edit the document.** Open the desired document (e.g. **Sales Order**). The **Reports** FastTab holds the **Factoring Bank Code**, **Clerk Code**, and **Field Worker Code**; in the lines, the **Position No.** is assigned automatically.
5. **Print/send.** Print or send the document as usual. The printout applies all settings from the Report Setup and master data.

The sequence follows the dependency in the code: without the **Report Setup** and matching **master data**, the document-side automatisms do not take effect.

## Setup

Setup is the most extensive part of this module. For the most part, it is performed once by administration and then permanently controls the document printing for all users.

### Report Setup

**Access:** Via **Search**, enter the term **Report Setup** and open the **Report Setup** page (company-wide single-record setup, type Administration).

**Process.** The **Report Setup** is maintained by administration or a key user **before the first document print**. It is valid company-wide (one record per company) and determines which fields, additional texts, bank accounts, and formatting appear on all documents. All subsequent chapters (master data, daily work) require this setup. The page is divided into the **General**, **Sales**, **Purchase**, and **Service** tabs; it shows exactly the fields that the printout evaluates.

#### General tab

| Setting | Explanation |
|---|---|
| **Logo Position on Fax/E-Mail** | Determines the logo alignment on fax/e-mail documents. When a value is set, the logo is positioned accordingly; the field is only editable when the Logo Position on Documents in the Sales & Receivables Setup is set to **No Logo**. Values: **No Logo** (no logo printed), **Left** (left-aligned), **Center** (centered), **Right** (right-aligned). |
| **Currency Symbol (LCY)** | Defines the symbol printed for the local currency. When filled, this symbol appears on the documents instead of the ISO code. |
| **Company Information in Header/Footer** | Controls where the company details appear. When **Header** is selected, the company data is printed in the document header; with **Footer**, in the document footer; with **(blank)**, no separate printing occurs at this location. |
| **Company Information in Lines** | When enabled, the company data is additionally repeated in the line area of the document; without the flag, the line area remains free of company details. |
| **Company Informormation Multilingual** | When enabled, the company details are printed in the document language (multilingual); without the flag, printing occurs only in the company language. |
| **Use Salutation from Contact** | When enabled, the document draws the salutation from the contact linked to the document (via the **Report Salutation Code**) and builds the personal salutation from it; without the flag, no contact-based salutation is formed. |
| **Delivery and Payment Terms** | When enabled, delivery and payment terms are printed in the document text; without the flag, these details are omitted. |
| **Document No. as Barcode** | When enabled, the document number is additionally printed as a barcode (see the **Barcode setup** chapter); without the flag, only the plain text appears. |
| **Barcode Delimiter** | Defines the delimiter used to separate composite barcode content. When filled, the barcode generator uses this character for segmentation. |
| **Year in four Digits** | When enabled, dates are printed with a four-digit year; without the flag, printing is two-digit. |
| **External Document No.** | When enabled, the external document number is printed on the document. Only when this field is active does the follow-up field **Change "External Document No." in "Your Order No."** become editable. |
| **Change "External Document No." in "Your Order No."** | When enabled, the external document number is printed under the label "Your Order No." instead of "Ext. Document No."; without the flag, the standard label remains. |
| **Change "Your Reference" in "Your Sign"** | When enabled, the field "Your Reference" is printed under the label "Your Sign"; without the flag, "Your Reference" remains. |
| **Compress Ship/Bill to Address** | When enabled, the ship-to and bill-to addresses are combined space-savingly; without the flag, they are printed in full length. |
| **Print Tariff No.** | When enabled, the customs tariff number of the items is printed in the lines; relevant for foreign documents. |
| **Print Lot/Serial No.** | When enabled, lot and serial numbers of the items are printed. Only when this field is active do the appendix fields **Serial/Lot Number as Appendix (Sales/Purchase)** become editable. |
| **Print Drawing No.** | When enabled, the drawing number per item is printed in the lines; without the flag, it is omitted. |
| **Print External Comment Lines** | When enabled, comment lines flagged as external are printed on the document; without the flag, they remain document-internal. |
| **Print Bank (Currency) at the footer, when the country is different** | When enabled, when the customer currency differs, the matching bank account is printed in the document footer. Only when this field is active does **Print additional Bank, when the currency code is different** become available. |
| **Print additional Bank, when the currency code is different** | When enabled, an additional bank is printed when the currency differs. Only when this field is active can a specific bank be selected in the follow-up field. |
| **Additional Bank, which should be printed at the footer when the currency code is different** | Defines the specific bank account that additionally appears in the footer when the currency differs. When filled, exactly this bank is used. |
| **Print Assembly Components** | When enabled, the components contained in assembly items are printed in the document lines; without the flag, only the assembly item appears. |
| **Barcode Server URL** | Defines the URL of the service that generates the barcodes. When filled, barcodes are generated via this server; without an entry, barcode printing is omitted. |
| **Company Name On Letter** | When enabled, the company name is printed in the letterhead; without the flag, the company name is omitted at this location. |
| **Jurisdiction** | Free text for the jurisdiction. When filled, this text is printed in the footer/legal details of the document. |
| **Management** | Free text for the management. When filled, this detail appears in the footer details. |
| **Commercial Registry** | Free text for the commercial registry. When filled, the registry detail is printed in the footer details. |
| **Postbox** | Defines the P.O. box detail. When filled, this is used instead of the street address for documents with a P.O. box address. |
| **Post Code Postbox** | Defines the postal code of the P.O. box; printed together with **Postbox** and **City Postbox**. |
| **City Postbox** | Defines the city of the P.O. box; complements the P.O. box address in the printout. |

#### Sales tab

| Setting | Explanation |
|---|---|
| **Print Shipping Agent** | When enabled, the shipping agent (delivery service provider) is printed on sales documents; without the flag, the detail is omitted. |
| **Serial/Lot Number as Appendix (Sales)** | When enabled, lot/serial numbers in Sales are printed as a separate appendix instead of in the lines. Editable only when **Print Lot/Serial No.** is active. |
| **Always Print Line Discount %** | When enabled, the line discount in percent is always printed on sales documents – even at 0%; without the flag, only when an actual discount exists. |
| **Requested Delivery Date** | When enabled, the requested delivery date is printed on the order confirmation. |
| **Promissed Delivery Date** | When enabled, the promised delivery date is printed on the order confirmation. |
| **Planned Shipment Date** | When enabled, the planned shipment date is printed on the order confirmation. |
| **Planned Delivery Date** | When enabled, the planned delivery date is printed on the order confirmation. |
| **Delivery Date as CW** (order confirmation) | When enabled, the delivery date is printed on the order confirmation as a calendar week instead of as a date. |
| **Export Regulation** | When enabled, export regulations are printed on the invoice/credit memo. When deactivated, the dependent fields **Print Export Regulation in Lines** and **Print VAT Clause Compare without Position Numbers** are automatically reset. |
| **Print Export Regulation in Lines** | When enabled, export regulations are printed per line; only available when **Export Regulation** is active. |
| **Print VAT Clause Compare without Position Numbers** | When enabled, the VAT clause is printed without the position numbers summary. Requires **Export Regulation** to be active (checked on saving). |
| **Credit Memo = Invoice Correction** | When enabled, credit memos from the effective date **Invoice Correction from** onward are labeled and printed as "Invoice Correction"; without the flag, as "Credit Memo". |
| **Invoice Correction from** | Defines the date from which credit memos are treated as invoice corrections. Editable only when **Credit Memo = Invoice Correction** is active. |
| **Insert Order No. Comment** | When enabled, the module automatically inserts a comment line with the order number when creating the sales invoice from a shipment. |
| **Insert External Document No. Comment** | When enabled, a comment line with the external document number is inserted when creating the sales invoice; depending on **Change "External Document No." in "Your Order No."**, the text is worded as "Your Order No." or "Ext. Document No.". |
| **Insert Your Reference Comment** | When enabled, a comment line with "Your Reference" (or "Your Sign") is inserted; the label follows **Change "Your Reference" in "Your Sign"**. |
| **Delivery Date as CW** (shipment) | When enabled, the delivery date on the shipment note is printed as a calendar week. |
| **Disable Zero Quantities** | When enabled, lines with quantity 0 are not printed; without the flag, zero-quantity lines also appear. |
| **Not due Entries** | When enabled, entries not yet due are also printed on the reminder; without the flag, only due entries. |
| **First Reminder = Payment Reminder** | When enabled, the first reminder level is labeled and printed as "Payment Reminder"; without the flag, as "Reminder". |
| **Print Return Reason Legend** (Return Receipt/Return Order) | When enabled, the legend of return reasons is printed on the return receipt/return order; without the flag, the legend is omitted. |

#### Purchase tab

| Setting | Explanation |
|---|---|
| **Serial/Lot Number as Appendix (Purchase)** | When enabled, lot/serial numbers in Purchase are printed as a separate appendix. Editable only when **Print Lot/Serial No.** is active. |
| **Always Print Line Discount %** | When enabled, the line discount in percent is always printed on purchase documents; without the flag, only when an actual discount exists. |
| **Purch. Credit Memo = Debit Advice** | When enabled, purchase credit memos are labeled and printed as "Debit Advice"; without the flag, as "Credit Memo". |
| **Print Return Reason Legend** (Return Order) | When enabled, the legend of return reasons is printed on the purchase return order. |

#### Service tab

| Setting | Explanation |
|---|---|
| **Always Print Line Discount %** | When enabled, the line discount in percent is always printed on service documents; without the flag, only when an actual discount exists. |

#### Additional calls from the Report Setup

Via the **Functions** menu of the Report Setup, you reach supporting cards: **Company Information** (company master data), **Responsibility Center**, and **Bank Accounts**. These links ease the maintenance of the data used by the printout (e.g. bank accounts for the footer printing).

### Barcode setup

**Access:** Via **Search**, open the **Default Report Barcode Setup** page (company-wide single-record setup, type Administration).

**Process.** The barcode setup is defined by administration so that documents carry uniform barcodes. It works together with the **Document No. as Barcode**, **Barcode Delimiter**, and **Barcode Server URL** fields of the Report Setup: only when barcode printing is enabled there and a barcode server is stored do the default values defined here take effect for barcode generation. Depending on the selected **Barcode Type**, the page shows only the matching parameter group.

| Setting | Explanation |
|---|---|
| **Barcode Type** | Defines the symbology to be generated. Depending on the selection, the associated parameter group (Aztec, Code128, DataMatrix, PDF417, QRCode) is displayed. Permitted values are the symbologies **Aztec, Codabar, Code128, Code39, DataMatrix, EAN13, EAN8, ITF, MSI, PDF417, Plessey, QRCode, UPCA** (technical symbology names). Additional parameters exist only for Aztec, Code128, DataMatrix, PDF417, and QRCode (see below); the remaining symbologies are generated without further parameters. |
| **Height (Pixel)** | Defines the height of the generated barcode in pixels. When set, the barcode is rendered at this height. |
| **Width (Pixel)** | Defines the width of the generated barcode in pixels. |
| **Margin (Pixel)** | Defines the margin (quiet zone) around the barcode in pixels; a sufficient margin ensures readability by scanners. |
| **Print Barcode with Content** | When enabled, the barcode content is additionally printed in plain text below the barcode; without the flag, only the barcode appears. |
| **Barcode Image Format** | Defines the image format of the generated barcode. Values: **bmp**, **jpeg**, **png** (technical image formats). |

Symbology-specific parameters (visible only for the corresponding Barcode Type):

- **Aztec:** **Aztec Layers** (number of layers) and **Aztec Error Correction %** (level of error correction; the higher, the more robust against damage).
- **Code128:** **Code 128 Force Codeset B** – when enabled, character set B is enforced (relevant for alphanumeric content).
- **DataMatrix:** **DataMatrix Encodation Type** (values: **Default, C40, Text, X12, Edifact, Base256**) and **DataMatrix Shape** (**Default**, **Force Rectangle**, **Force Square**) – define the encoding and shape of the code.
- **PDF417:** **PDF417 Use UTF8 Character Set**, **PDF417 Use Compact Mode**, **PDF417 Compaction** (**Default, Byte, Numeric, Text**), **PDF417 Minimum/Maximum Columns/Rows**, **PDF417 Disable ECI**, **PDF417 Error Correction Level** (**Default, L1–L8**) – control size, encoding, and error correction.
- **QRCode:** **QRCode Use UTF8 Character Set**, **QRCode Disable ECI**, **QRCode Error Correction Level** (**Default, L, M, Q, H** – from low to high error correction).

**Completion/transition.** Via the **Report Barcode Selection** action, you open the **Report Barcode Selection List**. There you can store barcode settings deviating from the default values per report (**Report ID**, **Report Name**); you maintain the detail values via the **Report Barcode Selection Card**. This way, individual documents receive deviating barcodes, while all others use the default values.

### Set up position numbers

**Access:** Via **Search**, open the **Position Nos. Setup** page (company-wide single-record setup, type Administration).

**Process.** This setup is performed by administration **before the first document entry**. It causes lines in sales, purchase, and transfer documents to automatically receive a continuous **Position No.** that is also carried into the posted documents and printed on the documents. The numbering is automatically recalculated for each new or changed line.

| Setting | Explanation |
|---|---|
| **Sales Step Range** | Defines the step range by which position numbers are incremented in sales documents. For example, if 10 is set, the lines receive the numbers 10, 20, 30 …; this leaves room for later insertions. |
| **Disable Sales Position Charge (Item)** | When enabled, sales lines of type **Charge (Item)** receive **no** position number; without the flag, these lines are also numbered (and sorted to the end of the lines). |
| **Purchase Step Range** | Defines the step range of position numbers in purchase documents (e.g. 100 → 100, 200, 300 …). |
| **Disable Purchase Position Charge (Item)** | When enabled, purchase lines of type **Charge (Item)** receive no position number; without the flag, they are numbered. |
| **Transfer Step Range** | Defines the step range of position numbers in transfer orders (e.g. 1000). |
| **Use In Client Sorting** | When enabled, the line order in the document window is sorted by position number; this way the user already sees the lines in printing order in the client. |
| **Use Report Sorting** | When enabled, the printout of the lines is sorted by position number; without the flag, printing follows the internal line number. |

*Note:* The underlying table additionally contains a **Service Step Range**; this is not displayed as a separate field on the setup page, but takes effect via the **Refresh Open Service Documents** action.

**Actions (process completion).** After the initial setup, you number existing open documents via the actions in the ribbon:

| Action | Explanation |
|---|---|
| **Refresh Open Documents** | Refreshes the position numbers of **all** open sales, purchase, and transfer documents. Before execution, the prompt "Do you want to refresh the position numbers of all open documents?" appears; after the run, the number of refreshed documents per document type is reported. |
| **Refresh Open Sales Documents** | Refreshes only the open sales documents. The prompt "Do you want to modify all relative open documents?" appears. |
| **Refresh Open Purchase Documents** | Refreshes only the open purchase documents (same prompt). |
| **Refresh Open Transfer Documents** | Refreshes only the open transfer documents (same prompt). |
| **Refresh Open Service Documents** | Refreshes only the open service documents (same prompt). |

**Transition to daily operation.** From now on, every newly entered line automatically assigns its **Position No.** – see the chapter **Daily work on the document**.

### Set up report salutations

**Access:** Via **Search**, open the **Report Salutations** list; you open the formulas per salutation via the **Formulas** action (**Report Salutation Formulas** page, opened for the selected salutation).

**Process.** The report salutations are maintained by the key user so that documents can build a **personal, multilingual salutation** from the contact data. The chain takes effect when the field **Use Salutation from Contact** is enabled in the **Report Setup** and a **Report Salutation Code** is stored on the **Contact** (see the master data chapter).

Numbered setup steps in dependency order:

1. **Create salutation.** In **Report Salutations**, create a record with **Code** and **Description** per salutation type. When a salutation is deleted, all associated formulas are automatically removed.
2. **Store a formula per language.** Via **Formulas**, open the **Report Salutation Formulas** and maintain a **Salutation** template with placeholders per **Language Code**, as well as the building blocks **Name 1** to **Name 4**. Each name building block is filled from the contact; permitted values per building block: **Job Title**, **First Name**, **Middle Name**, **Surname**. Empty name building blocks are removed together with their placeholder on printing, so that no gaps arise.
3. **Operational completion.** Assign the salutation code on the **Contact** (field **Report Salutation Code**) and enable **Use Salutation from Contact** in the Report Setup. On document print, the salutation is composed in the document language from the formula and the contact data.

### Set up factoring bank additional texts

**Access:** On the **Bank Account Card** (bank account), in the **MuM Reports** FastTab, set the **Factoring Bank** flag; you maintain the additional texts via the **Factoring Bank - Additional Texts** action (opens the **Factoring Bank - Additional Texts** page filtered to the current bank account).

**Process.** This chain enables a **language-dependent additional text** of a factoring bank to appear on the documents (footer) during factoring processing. It is configured by administration; in daily operation it takes effect via the **Factoring Bank Code** on the document or customer.

1. **Flag the bank as a factoring bank.** On the **Bank Account Card**, set the **Factoring Bank** field. If you later deactivate the flag again and additional texts already exist, the system asks: "You intend to deactivate the Bank '…' as Factoring Bank. It will be deleted the assigned Additional Texts. Do you want to continue?" – on confirmation, the additional texts are deleted.
2. **Define the print sequence.** Set **Sequence Document Print** when multiple banks are printed: when filled, the value determines in which order the bank accounts appear on printing.
3. **Maintain additional texts.** Via the **Factoring Bank - Additional Texts** action, open the page of the same name and enter an **Additional Text** per **Language Code**. The text is printed on documents in the respective language.
4. **Operational completion.** Store the **Factoring Bank Code** on the customer or directly on the document (**Reports** FastTab). Together with the Report Setup fields **Print Bank (Currency) at the footer …** and **Print additional Bank …**, the additional text is output on printing.

### Set up translations (countries/return reasons)

**Access:** **Country/Region Trans.** via the **Countries/Regions** list (action **Country/Region Trans.**); **Return Reason Translation** via the **Return Reasons** list (action **Return Reason Translations**). Both target pages can additionally be found as separate lists.

**Process.** These master data translations ensure that country names and return reasons appear on foreign-language documents in the document language. They are maintained by the key user and are automatically evaluated in the printout by **Language Code** (among others for the return reason legend, see Report Setup).

- **Country/Region Trans.:** a translated **Name** per **Country/Region Code** and **Language Code**. When filled, the translated country name is printed in the document language.
- **Return Reason Translation:** a translated **Description** per return reason **Code** and **Language Code**. When filled, the translated return reason description appears in the return reason legend.

## Master data

Besides the setup pages, the module adds document-controlling fields to central master data cards. These values are automatically carried over when entering documents and control the printout and number of copies.

### Customer

**Access:** **Customers** (list) → open customer → **Reports** FastTab.

**Process.** Administration or sales maintains the customer-specific printing and copy defaults here. When creating a sales document, **Clerk Code** and **Field Worker Code** are automatically carried from the customer into the document header (supplemented, if applicable, by contact and user setup).

| Field | Explanation |
|---|---|
| **Factoring Bank Code** | Defines the factoring bank of the customer (reference to a bank account). When filled, the associated factoring bank additional text is used on document print. |
| **Clerk Code** | Defines the responsible clerk (salesperson/purchaser). When filled, the code is automatically carried into the document header when creating sales documents and printed. |
| **Field Worker Code** | Defines the responsible field worker. When filled, it is automatically carried into the document when creating sales documents and printed. |
| **No. Of Invoice Copies** | Defines how many copies of a sales invoice are printed for this customer. When > 0, printing is multiplied accordingly. |
| **No. Of Copies Sales Shpt.** | Defines the number of copies of the sales shipment for this customer. |
| **No. Of Copies SO. Conf.** | Defines the number of copies of the order confirmation for this customer. |

### Vendor

**Access:** **Vendors** (list) → open vendor → **Reports** FastTab.

**Process.** Purchasing maintains the vendor-specific defaults here; when creating purchase documents, **Clerk Code** and **Field Worker Code** are carried into the document header analogously to the customer.

| Field | Explanation |
|---|---|
| **Clerk Code** | Defines the responsible clerk. When filled, it is carried into the document header when creating purchase documents and printed. |
| **Field Worker Code** | Defines the responsible field worker. When filled, it is carried over when creating purchase documents and printed. |
| **No. Of Copies Purch. Order** | Defines the number of copies of the purchase order for this vendor. When > 0, printing is multiplied accordingly. |

### Contact

**Access:** **Contacts** (list) → open contact → **Reports** FastTab.

**Process.** On the contact, the values relevant for the personal salutation and responsibility are maintained. The **Report Salutation Code** links the contact with a **report salutation**/formula; together with **Use Salutation from Contact** (Report Setup), the document builds the salutation from it in the document language.

| Field | Explanation |
|---|---|
| **Report Salutation Code** | Defines the report salutation to be used (reference to **Report Salutations**). When filled and **Use Salutation from Contact** is active, the document builds the personal salutation from the associated formula and the contact names. |
| **Clerk Code** | Defines the clerk. When filled, it is carried into the document header when creating documents for this contact (takes precedence over the customer value when the contact is set on the document). |
| **Field Worker Code** | Defines the field worker. When filled, it is carried over when creating documents for this contact. |

### Salesperson/Purchaser

**Access:** **Salespeople/Purchasers** (list) → open card → **Reports** FastTab.

**Process.** Details are maintained here that identify the responsible person on documents.

| Field | Explanation |
|---|---|
| **Signature** | Stores a signature image. When filled, the signature of the clerk/salesperson is printed on the documents. |
| **Company Procuration** | Indicates whether or with which procuration the person signs. When filled, the detail is taken into account in the signature area of the document. |

### User Setup

**Access:** Via **Search**, open the **User Setup**.

**Process.** In the User Setup, default values are stored per user that take effect when creating documents if the customer/contact does not supply their own value.

| Field | Explanation |
|---|---|
| **Clerk Code** | Defines the default clerk of the logged-in user. When filled and no clerk is yet set on the document, this value is automatically carried over on creation. |
| **Field Worker Code** | Defines the default field worker of the user. When filled and not yet set on the document, it is automatically carried over on creation. |

### VAT Posting Groups (Reverse Charge)

**Access:** Via **Search**, open the **VAT Posting Groups** and choose the relevant card.

| Field | Explanation |
|---|---|
| **Print Reverse Charge** | When enabled, for documents with this VAT posting group combination the reverse charge note (tax reversal) is printed per position on the document; without the flag, the note is omitted. |

### Bank Account

See the chapter **Set up factoring bank additional texts**. On the Bank Account Card, you flag a bank as a **Factoring Bank** in the **MuM Reports** FastTab and define the **Sequence Document Print**; you maintain the language-dependent additional texts via the associated action.

## Daily work on the document

In daily operation, users work with the standard Business Central documents (sales quote/order/invoice/credit memo/return order, purchase quote/order/invoice, etc.). The module adds uniform **header** and **line fields** there, which require the Report Setup and the master data.

### Document header

On the document cards, the **Reports** FastTab holds the following fields:

| Field | Explanation |
|---|---|
| **Factoring Bank Code** | Defines the factoring bank to be printed for this document. Is pre-filled from the customer on creation and can be overwritten on the document. When filled, the associated additional text appears in the footer. |
| **Clerk Code** | Shows/sets the responsible clerk. Is automatically carried over from contact, customer, or user setup when setting **Sell-to Customer**/**Sell-to Contact** (or the purchase equivalents) and printed on the document. |
| **Field Worker Code** | Shows/sets the responsible field worker; is pre-filled and printed analogously. |

This pre-filling is stored in the code: when changing customer or contact on the sales document, the module draws clerk, field worker, and salesperson from the contact, alternatively from the customer, and supplementally from the user setup, provided the fields on the document are still empty.

On posted documents (posted sales invoice, posted shipment, posted purchase invoice, posted return receipt, etc.) as well as on reminders and issued reminders, the **Factoring Bank Code**, **Clerk Code**, **Field Worker Code**, and – for reminders – the **Salesperson Code** are also displayed, so that the details remain traceable after posting.

### Document lines (position numbers)

In the line subforms of all sales, purchase, service, and transfer documents, the module adds the **Position No.** column; on some (posted/archived) documents additionally **Sorting Position No.**:

| Field | Explanation |
|---|---|
| **Position No.** | Shows the automatically assigned position number of the line. Lines of type **G/L Account, Item, Resource, Fixed Asset**, and **Charge (Item)** receive a number according to the configured step range; empty lines receive none. The number is automatically recalculated on entry/change and carried into the posted document. |
| **Sorting Position No.** | Internal sort value for the printing/display order. When set, it controls the order of the lines independently of the internal line number (e.g. charge lines to the end of the lines). |

Whether the position numbers are sorted by position no. in the document window and/or in the printout is controlled by the fields **Use In Client Sorting** and **Use Report Sorting** of the Position Nos. Setup.

### Comment lines and printing per document type

On the **sales** and **purchase comment sheets**, the module adds flags per comment line that define **on which document types** the respective comment is printed – e.g. **External**, **Quote/Request for Quote**, **Order**, **Blanket Order**, **Invoice**, **Credit Memo**, **Shipment**, **Return Receipt/Return Shipment**, **Return Order**, **Pick List**, and **Posted Return Receipt**. When a flag is set, the comment appears exactly on the corresponding document type; without the flag, it remains invisible on that document type. This way, comments can be controlled specifically per document type.

## Documents and reports

After setup and report selection, the m+m documents print the customized layouts. The central document reports of the module are:

| Report | Report ID | Covered document types |
|---|---|---|
| **Sales Report** | 5400420 | Quote, Blanket Order, Order, Quote/Order Archive, Shipment, Invoice, Return Order, Credit Memo, Return Receipt, Reminder, Accompanying Document, Pro Forma Invoice |
| **Purchase - Report** | 5400427 | Request for Quote, Blanket Order, Order, Credit Memo, Return Shipment, Invoice, Quote/Order Archive |
| **Service - Report** | 5400432 | Service Order, Service Quote, Service Invoice, Service Contract, Service Shipment, Service Credit Memo |
| **Prod. Order Sheet** | 5400411 | Production Order Work Sheet |
| **Pro Forma Invoice** | 5400430 | Sales – Pro Forma Invoice |

The **report type** (Quote, Order, Invoice, Credit Memo, Return Order, Return Receipt, Shipment, Accompanying Document, Transfer Shipment, Blanket Order, Contract, Shipment Planning, Pro Forma Invoice, posted invoice, posted credit memo) controls which processing the report selects. The **number of printed copies** results from the customer or vendor fields (**No. Of Copies …**).

On **archived** and **posted** documents, the additional header and line fields (Factoring Bank Code, Clerk/Field Worker Code, Position No.) are carried along and printed, so that the documents remain fully traceable even after posting and archiving.

**Permissions.** For access to the module pages and data, the supplied permission set **MuM RP Permission** is used; it determines which actions the users can perform on the module pages.

## FAQ and troubleshooting

### Why do no position numbers appear in my document lines?
Position numbers are only assigned when a **step range** is stored for the respective area in the **Position Nos. Setup**. If no step range is maintained, the **Position No.** remains empty. Also check whether the line type receives a number (empty lines are never numbered).

### Why do my charge lines have no position number?
Presumably **Disable Sales Position Charge (Item)** or **Disable Purchase Position Charge (Item)** is enabled. In this state, lines of type **Charge (Item)** deliberately receive no number. Disable the flag if these lines should be numbered.

### How do I refresh position numbers in already existing documents?
Open the **Position Nos. Setup** and choose **Refresh Open Documents** (all areas) or one of the area-specific actions (**Refresh Open Sales/Purchase/Transfer/Service Documents**). Confirm the prompt; the system then reports the number of refreshed documents.

### Why is the personal salutation not built on the document?
For the salutation, three things must match: in the **Report Setup**, **Use Salutation from Contact** must be active; on the **Contact**, a **Report Salutation Code** must be stored; and in the **Report Salutation Formulas**, a **Salutation** formula must exist for the document language. If any of these is missing, the salutation remains empty.

### Why is a factoring bank not printed in the document footer?
The footer printing of the bank depends on several places: the bank must be flagged as a **Factoring Bank** on the **Bank Account Card**, the **Factoring Bank Code** must be set on the document (or customer), and in the **Report Setup** the fields **Print Bank (Currency) at the footer …** or **Print additional Bank …** must be set accordingly.

### What happens to the additional texts when I remove the "Factoring Bank" flag?
If the bank already contains additional texts and you deactivate the **Factoring Bank** flag, the system warns: "…It will be deleted the assigned Additional Texts. Do you want to continue?" If you confirm, the additional texts are irreversibly deleted; if you cancel, the flag remains set.

### Why can't I set "Print Export Regulation in Lines"?
This field is only available when **Export Regulation** is active. When **Export Regulation** is deactivated, the system automatically resets **Print Export Regulation in Lines** and **Print VAT Clause Compare without Position Numbers**.

### Why do the labels "Credit Memo" or "Your Reference" change on the document?
This is intended and is controlled via the Report Setup: **Credit Memo = Invoice Correction** (from **Invoice Correction from**) prints "Invoice Correction", **Purch. Credit Memo = Debit Advice** prints "Debit Advice", **Change "Your Reference" in "Your Sign"** prints "Your Sign", and **Change "External Document No." in "Your Order No."** prints "Your Order No.".

### Why is the printed number of copies incorrect?
The number of copies per document type is maintained on the **Customer Card** (sales invoice, sales shipment, order confirmation) or **Vendor Card** (purchase order). Check the **No. Of Copies (…)** fields there for the affected business partner.

### Why is my barcode on the document empty or not generated?
For barcode printing, **Document No. as Barcode** must be enabled in the **Report Setup** and a **Barcode Server URL** must be stored; additionally, a valid **Barcode Type** and matching dimensions must be maintained in the **Default Report Barcode Setup**. If the barcode server is missing, generation is omitted.

## Typical use cases

### Use case 1: Set up and print a factoring bank with a foreign-language footer text

**Trigger.** Accounting reports that for foreign customers the assigning factoring bank, including a note text, should appear in the invoice footer.

**Access in BC.** Open the **Bank Accounts**, select the relevant bank, and open the **Bank Account Card**. In the **MuM Reports** FastTab, set the **Factoring Bank** flag and define the **Sequence Document Print**.

**Core process.** Via the **Factoring Bank - Additional Texts** action, open the page of the same name (filtered to the bank account) and enter an **Additional Text** per **Language Code**. Then store the **Factoring Bank Code** on the customer (**Reports** FastTab) and set the fields **Print Bank (Currency) at the footer, when the country is different** as well as, if applicable, **Print additional Bank, when the currency code is different**, including the specific bank, in the **Report Setup**.

**Completion.** On printing the sales invoice, the factoring bank appears with the language-dependent additional text in the footer. If you later deactivate the **Factoring Bank** flag, the system points out the deletion of the additional texts.

### Use case 2: Continuous position numbers in the sales order

**Trigger.** Sales wants a continuous, easily readable position numbering of the lines on the order confirmation.

**Access in BC.** Via **Search**, open the **Position Nos. Setup** and enter, for example, 10 under **Sales Step Range**. Decide via **Disable Sales Position Charge (Item)** whether charge lines are numbered. If needed, enable **Use In Client Sorting** and **Use Report Sorting**.

**Core process.** Choose the **Refresh Open Sales Documents** action and confirm the prompt to number existing open orders. Then open a **Sales Order**: in the lines, the **Position No.** is automatically assigned according to the step range; new lines receive the next number consecutively.

**Completion.** On printing the order confirmation, the position numbers appear in the lines; after posting, they are carried into the posted document.

### Use case 3: Multilingual personal salutation from the contact

**Trigger.** For an English-speaking customer, the invoice should carry a correct, personalized salutation.

**Access in BC.** Via **Search**, open the **Report Salutations** and create a salutation with **Code** and **Description**. Via the **Formulas** action, open the **Report Salutation Formulas** and store a **Salutation** template per **Language Code** as well as the building blocks **Name 1**–**Name 4** (e.g. **Job Title**, **First Name**, **Surname**).

**Core process.** Assign the **Report Salutation Code** on the **Contact** (**Reports** FastTab) and enable the field **Use Salutation from Contact** in the **Report Setup**. Enter the sales document with the relevant contact/customer.

**Completion.** On printing, the document builds the salutation in the document language from the formula and the contact data; missing name building blocks are automatically removed together with their placeholder, so that no gaps arise.
