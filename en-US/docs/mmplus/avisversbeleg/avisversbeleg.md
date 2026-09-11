---
title: Handbuch zur m+m Logistic Management mit Report Package
---

# User Manual m+m Logistic Management with Report Package

## Introduction

The **m+m Logistic Management with Report Package** extension is a connection app between the logistics module **m+m Logistic Management** and the document framework **m+m Report Package**. It provides shipment planning and advice notification with **two additional report layouts** and adds a clerk field to the shipment planning document. The app does **not** introduce any documents, postings, or warehouse processes of its own; all creation, release, registration, and posting steps for advice notification and shipment planning continue to be delivered by the base module m+m Logistic Management.

Specifically, the app does three things:

- It delivers the **Advice Notification** and **Shipment Planning** reports (each including a registered and an archived document variant) as printable documents in the uniform layout of the Report Package.
- During installation it automatically stores these reports in the setup pages **Advice Notification Setup** and **Shipment Planning Setup**, so that the **Print** and **Register and Print** actions on the documents immediately use the correct layout.
- It adds the **Clerk Code** field to the shipment planning document and to the registered shipment planning; the field is carried over automatically during registration.

**Target group.** The primary users are the **operational clerks in shipping and goods receipt** who process, register, and print or dispatch advice notifications and shipment plannings in day-to-day business. Administrators and key users are addressed secondarily: they set up the report assignment and the report setup once.

A technical note for understanding: In the background, two codeunits (`MuM RPAS Report Data Mgt.` and an event subscriber) collect the header, line, and footer data of the documents and hand them over to the Report Package framework. This logic runs without a user interface of its own; the user only notices it on the finished printed document.

## Quick Start for Users

The fastest way from a configured system to a printed document:

1. **Check setup (once, administrator).** Use **Search** to open the **Shipment Planning Setup** or **Advice Notification Setup** page and make sure that the report fields (**Shipment Planning Report ID**, **Reg. Shipment Planning Report** or **Advice Notification Report ID**, **Reg. Adv. Notification Report**, **Archived Advice Notif. Report**) contain the reports delivered by this app. During installation this happens automatically; see the **Setup** chapter.
2. **Process the document.** In day-to-day business, open the **Shipment Planning** (or **Advice Notification**) and enter the lines as usual. In the header, enter the **Clerk Code** if required.
3. **Register.** On the shipment planning, choose the **Register** or **Register and Print** action. This creates the **Registered Shipment Planning**; the entered **Clerk Code** is transferred automatically into the registered shipment planning.
4. **Print.** Choose the **Print** action (or the print part of **Register and Print**). The report request page opens. There, set **No. Of Copies** and, if required, **Print Serial/Lot No. as appendix**; for the advice notification, additionally **Archive Document**. Confirm with **OK**.

The order follows the dependency in the code: first setup (report assignment), then document processing, then **Register**/**Register and Print** and **Print**.

## Setup

Setting up this app consists of the **report assignment** on two existing setup pages of the base module and the assignment of the permission. In addition, the reports access two global default values of the Report Package's **Report Setup**.

### Assign Reports Automatically (Installation Logic)

**Who and when.** The app performs this assignment automatically **per company at installation** (install codeunit `MuM RPAS Install Mgt`). The administrator only needs to check and, if necessary, add missing entries. The assignment is later consumed on every print from shipment planning and advice notification (see **Printing Documents**).

**What happens.** If the report fields in the setup pages are still set to `0` (no report), the app enters its own reports there:

1. First, the app checks the **Advice Notification Setup**. If **Advice Notification Report ID**, **Reg. Adv. Notification Report**, or **Archived Advice Notif. Report** is still empty, the **Advice Notification** report of this app is entered in each case. Once set, the **Print** and **Register and Print** actions on the advice notification, the registered advice notification, and the advice notification archive automatically use this layout.
2. Next, the app checks the **Shipment Planning Setup**. If **Shipment Planning Report ID** or **Reg. Shipment Planning Report** is still empty, the **Shipment Planning** report of this app is entered in each case. Once set, the shipment planning and the registered shipment planning print using this layout.
3. Finally, the app saves the entries so that they remain permanently in effect.

The app does **not** overwrite reports that have already been assigned manually — only empty fields are filled. This preserves any customer-specific report choice.

**Entry point:** Use **Search** to open the **Advice Notification Setup** or **Shipment Planning Setup** page (global, company-wide setup, category Administration). These pages are singletons — there is exactly one record per company, which cannot be deleted or created anew.

#### Advice Notification Setup — Fields Relevant to This App

Documented here are the fields that this app sets or whose value it processes during printing. The remaining fields on this page belong to the base module process (creating/registering advice notifications) and are described there.

| Setup | Explanation |
|---|---|
| **Activated** | When enabled, the advice notification is usable in the company; only then do advice notification documents exist that this app can print. |
| **Archiving Advice Notification** | Controls whether a document archive is created during printing. **Never:** No archive is created; the **Archive Document** option in the report request page has no effect. **On Request:** The user decides per print, via **Archive Document**, whether an **Arch. Advice Notification** is created. **Always:** An **Arch. Advice Notification** is created on every print and can later be printed via the **Advice Notification** report as an archived variant. |
| **Advice Notification Report ID** | Report for the open advice notification. If the report of this app is entered here, the **Print** action on the advice notification prints this layout. |
| **Reg. Adv. Notification Report** | Report for the **Reg. Advice Notification**. When set, the print of the registered advice notification uses this layout. |
| **Archived Advice Notif. Report** | Report for the **Arch. Advice Notification**. When set, an archived advice notification is printed with this layout. |

Additional fields on this setup page (number series for advice notification and registered advice notification, default capacity unit, posting options, Direct Register, quantity reconciliation via item tracking, and the default values for purchase lines) control the **creation and registration process of the base module** and not the printing; they are described in the manual of the base module m+m Logistic Management.

#### Shipment Planning Setup — Fields Relevant to This App

| Setup | Explanation |
|---|---|
| **Activate Shipment Planning** | When enabled, the shipment planning is usable in the company; only then do shipment planning documents exist that this app can print. |
| **Shipment Planning Nos.** | Number series of the shipment planning. When set, each new shipment planning receives a consecutive number that appears as the document number on the printed report. |
| **Qty. To Assign Default Value** | Suggested value for the quantity to assign when retrieving an order line. **Remaining Quantity:** The open remaining quantity of the order line is suggested. **Finished Quantity:** The quantity already finished is suggested. The value determines the quantity that subsequently appears in the printed shipment planning document as the assigned quantity. |
| **Shipment Planning Report ID** | Report for the open shipment planning. If the report of this app is entered here, the **Print** action on the shipment planning prints this layout. |
| **Reg. Shipment Planning Report** | Report for the **Reg. Shipment Planning**. When set, the print of the registered shipment planning uses this layout. |

The remaining fields on this page (number series of the registered shipment planning, loading sequence increments, default values for purchase lines, date filters for assignment and inventory control) control the shipment planning process of the base module and are described there.

### Report Setup of the Report Package (Global Default Values)

**Who and when.** The administrator maintains the **Report Setup** of the Report Package once. These values apply to all documents of the framework and are read by both reports of this app during printing.

**Entry point:** Use **Search** to open the **Report Setup** page.

| Setup | Explanation |
|---|---|
| **Logo Position on Fax/E-Mail** | Defines the logo position when a document is not printed regularly but is output by fax or e-mail. When set, the report adopts this position, provided no logo position is stored for regular printing. |
| **Company Information in Lines** | When enabled, the report prints the company information within the line area; without the flag, the lines remain without these additional details. |

The default value **Serial/Lot Number as Appendix (Sales)** of the Report Setup determines the preset of the appendix option in the report request page (see **Printing Documents**): if it is active, the **Print Serial/Lot No. as appendix** option is preselected when the request page opens.

### Permissions

**Who and when.** The administrator assigns the supplied permission to the users who are to print advice notifications and shipment plannings.

The permission set **All Logistic Mgt. Report permissions** (`MuM MPAS All Perm.`) defines which objects of this app a user may execute: the two reports **Advice Notification** and **Shipment Planning** as well as the associated background codeunits (installation, data collection, and subscriber logic). Assign this set in addition to the permissions of the base module; it is not sufficient on its own, because creation and registration of the documents take place in the base module and require its permissions.

## Master Data and Document Attribute: Clerk Code

**Who and when.** The operational user maintains the **Clerk Code** directly on the shipment planning document while processing the shipment planning — it is a header attribute of the document, not a master data table of its own. The value is used in the registered shipment planning and is the basis for later evaluation and traceability of who was responsible for the shipment planning.

**Entry point:** Open the **Shipment Planning** and, on the **General** tab, choose the **Clerk Code** field.

| Field | Explanation |
|---|---|
| **Clerk Code** | Links the shipment planning to a salesperson/purchaser. When set, the responsible clerk is stored on the document and is automatically transferred into the **Registered Shipment Planning** during registration; without an entry, the document remains without a clerk assignment. Only existing salespersons/purchasers are permitted (selection from the corresponding list). |

**Transfer during registration.** When the user registers the shipment planning (action **Register** or **Register and Print**), the app copies the **Clerk Code** from the open document into the registered shipment planning. The user does not have to enter the value there again; in the registered document, the field is only displayed. This preserves the clerk assignment across registration.

This app does not add a separate field to item, vendor, or customer master data; the **Clerk Code** exists exclusively on the shipment planning header and on the registered shipment planning.

## Printing Documents

The actual benefit of this app lies in the two report layouts. They are not called via **Search** but via the **print and register actions on the documents** of the base module; the layout results from the report assignment in the setup.

### Shipment Planning Report

The **Shipment Planning** report prints both the open **Shipment Planning** and the **Registered Shipment Planning**. It determines the net and gross weight of the shipment planning lines, adopts the recipient and delivery address, and presents the positions with quantity, unit, and weight; on request, lot and serial numbers are printed as an appendix.

**Entry point:** Use the **Print** action (or the print part of **Register and Print**) on the shipment planning to open the report request page.

| Field | Explanation |
|---|---|
| **No. Of Copies** | Determines how many additional copies are printed beyond the original. When set to > 0, the additional copies are output with the **COPY** note. |
| **Print Serial/Lot No. as appendix** | When enabled, an appendix with the assigned **Lot No.** and **Serial No.** details (with quantity per lot/serial) is attached to the shipment planning; without the flag, these details do not appear as a separate appendix. Preset from the default value of the Report Setup. |

For the **Registered Shipment Planning**, the request page contains the same appendix option; the visibility of the respective group (**Shipment Planning** or **Reg. Shipment Planning**) depends on which document type is printed via filter.

### Advice Notification Report

The **Advice Notification** report prints the open **Advice Notification**, the **Reg. Advice Notification**, and the **Arch. Advice Notification**. It draws contact and vendor data, determines the quantities to assign and the loading details, and can optionally output lot/serial numbers as an appendix.

**Entry point:** Use the **Print** action (or **Register and Print**) on the advice notification to open the report request page.

| Field | Explanation |
|---|---|
| **No. Of Copies** | Determines how many copies are printed in addition. When set to > 0, the copies carry the **COPY** note. |
| **Print Serial/Lot No. as appendix** | When enabled, an appendix with **Lot No.**/**Serial No.** per position is printed; without the flag, the appendix is omitted. Preset from the Report Setup. |
| **Archive Document** | Visible only for the open advice notification. When enabled, an **Arch. Advice Notification** is saved during printing, which can be printed again later. The preset and visibility depend on the setup option **Archiving Advice Notification** (Never/On Request/Always). |

For **Reg. Advice Notification** and **Arch. Advice Notification**, the request page shows the matching group in each case; the **Archive Document** option is omitted there, because these documents are already registered or archived.

### Print and Register Flow

The complete flow using the example of the shipment planning, as it is defined in the code:

1. Select the **Shipment Planning** to be processed and complete the header (including **Clerk Code**) and the lines.
2. Choose the **Register** or **Register and Print** action. The **Registered Shipment Planning** is created; the **Clerk Code** is transferred.
3. With **Register and Print**, the report request page opens immediately; with **Register**, you then call the print via **Print**.
4. Set **No. Of Copies** and, if required, **Print Serial/Lot No. as appendix**, and confirm with **OK**.
5. After printing (not in the preview), the system increases the document's print counter, so that it remains traceable how often the document was output.

The same flow applies to the advice notification; additionally, an **Arch. Advice Notification** can be created via **Archive Document**. A separate posting or release step does not belong to this app — it delivers only the layout and the counting of outputs; release, registration, and any warehouse shipments are controlled by the base module.

## FAQ and Troubleshooting

### 1. Why does the shipment planning print immediately in the new layout after installation?
Because the install codeunit automatically populates the report fields **Shipment Planning Report ID** and **Reg. Shipment Planning Report** in the **Shipment Planning Setup** with the **Shipment Planning** report of this app, provided they were still empty.

### 2. What happens if a custom report was already assigned?
Then it is retained. The app only fills report fields that are set to `0` (no report); it does not overwrite assignments that have already been made.

### 3. Why can't I find the reports via the search?
The two reports are deliberately not callable via **Search**. They are started exclusively via the **Print** or **Register and Print** actions on the shipment planning and advice notification.

### 4. How does the clerk appear on the registered shipment planning?
The **Clerk Code** entered on the open document is automatically transferred into the **Registered Shipment Planning** during registration; re-entry is not necessary.

### 5. Why can't I change the Clerk Code in the registered shipment planning?
Because the registered shipment planning represents the document in its evidentiary state. The value is only displayed there; it is editable on the open document before registration.

### 6. Which value may the Clerk Code take?
Only an existing salesperson/purchaser. The field is linked to the corresponding master data list; free entries without a matching record are not permitted.

### 7. When is an Arch. Advice Notification created?
When printing the open advice notification, if the setup option **Archiving Advice Notification** is set to **Always**, or is set to **On Request** and the user enables **Archive Document** in the report request page. With **Never**, no archive is created.

### 8. Why are lot and serial numbers not printed?
Because the **Print Serial/Lot No. as appendix** option in the report request page was not enabled. Its preset comes from the default value of the **Report Setup**; set it per print or adjust the default value.

### 9. Why doesn't the number of printouts on the document match my prints?
The print counter is only increased on an actual print, not in the preview. Preview calls therefore do not count.

### 10. Why can a user not print a document even though they can see the shipment planning?
The permission set **All Logistic Mgt. Report permissions** is probably missing. It grants the two reports and the background logic of this app and must be assigned in addition to the permissions of the base module.

## Typical Use Cases

### Use Case 1: Print Shipment Planning with Clerk

- **Trigger:** Shipping is preparing an upcoming delivery and needs a shipment planning document with a clearly assigned clerk.
- **Entry in BC:** The user opens the **Shipment Planning**, in which the retrieved order lines are already contained.
- **Core flow:** On the **General** tab, the user enters the **Clerk Code** and completes the lines. Then they choose **Register and Print**. The system creates the **Registered Shipment Planning**, transfers the **Clerk Code**, and opens the report request page. The user sets **No. Of Copies** and, if required, **Print Serial/Lot No. as appendix**, and confirms with **OK**.
- **Conclusion:** The **Shipment Planning** document is printed in the Report Package layout; the document's print counter is increased. The registered document, including the clerk, can be found in the overview of registered shipment plannings.

### Use Case 2: Print and Archive Advice Notification

- **Trigger:** For an advised delivery, an advice notification document is to be printed and an archived version kept at the same time.
- **Entry in BC:** The user opens the **Advice Notification** with the entered positions.
- **Core flow:** They choose the **Print** action. In the report request page, they enable **Archive Document** (provided the **Archiving Advice Notification** setup leaves this open at **On Request**) and, if required, **Print Serial/Lot No. as appendix**, and set **No. Of Copies**. After **OK**, the **Advice Notification** report is printed.
- **Conclusion:** In addition to the printed document, an **Arch. Advice Notification** is created, which can later be printed again via the same report as an archived variant. The advice notification's print counter is increased.
