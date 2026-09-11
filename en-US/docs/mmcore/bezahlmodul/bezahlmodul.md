---
title: Cloud Base
---

# m+m Cloud Base User Handbook

## Introduction

The m+m app **Cloud Base** is used to license the m+m modules you have purchased in the cloud. The app gives you a single place to see which m+m modules are licensed, which **License Type** applies to each, whether a module is a time-limited trial version, and which users or companies are allowed to use the respective module. In addition, the app shows the payment and reminder status of each module.

The app is intended exclusively for cloud environments (SaaS); in on-premises installations, the license check and license retrieval are disabled.

**Target audience:** Cloud Base is aimed primarily at **administrators and key users** who license the purchased m+m modules and control usage per user or per company. This module has no daily document processes; the operational work consists of a one-time activation of a license key and the ongoing maintenance of user and company assignments. All other m+m modules automatically access the license information stored here in the background.

**Short process overview:**

1. You ensure that the **prerequisites** are met (valid license key, installed modules).
2. You activate the **License Key** on the **m+m Modules** page. The licensed modules are entered or updated automatically.
3. For the license type **per User** or **per Company**, you assign the authorized users or companies via **Value Assigment**.
4. During operation, each m+m module checks the license automatically; overdue payments generate notices and escalate through **Reminder Levels**.

## Quick Start for Users

The fastest path from installation to a usable license. Setup deliberately comes before all further steps, because without an activated license key there is no module information available.

1. **Check prerequisites:** Have your license key ready (format `XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX`) and make sure that the purchased m+m modules are installed (check via **Extension Management**).
2. **Open the page:** Use the **Search** to open the **m+m Modules** page.
3. **Activate the license:** Choose **Actions** → **Update/Insert Entry**. In the **Input Page**, enter your **License Key** and confirm with **OK**. Then leave the page via **Close**.
4. **Check the result:** The licensed modules appear automatically in the **m+m Modules** list with **License Type**, **Valid Until**, and payment data.
5. **Only for license type per User / per Company:** Select the module row and choose the **Value Assigment** action. On the **m+m License Value Assignment** page, enter the authorized **users** or **companies** and leave the **Enabled** flag set.

After that, the app is ready for use; the other m+m modules use the license automatically.

## Prerequisites

Before you activate a license, two prerequisites must be met. The administrator carries out this check once before the first activation.

**Existing license key.** You need a valid **License Key** from markmann+müller datensysteme gmbh. It is usually shown on the delivery note for the purchased modules and has the format `8-4-4-4-12` (`XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX`). When activated, the app uses this key to retrieve the associated module and product data; without a valid key, the **m+m Modules** list remains empty and no module is licensed. If you have not received a key, contact your responsible consultant.

**Installed m+m modules.** The purchased modules should be installed before licensing. You can see the installation status of an app via **Extension Management**. If a module is installed, it can be recognized and matched to the license reconciliation via the **Show installed m+m Modules** action; if a module is missing, contact your responsible consultant.

## Setup

Setup is the core of Cloud Base. It consists of the one-time activation of the license key and – depending on the **License Type** – the assignment of authorized users or companies. The central page is **m+m Modules**.

### "m+m Modules" Page

**Access:** Open the **m+m Modules** page via the **Search**. It is a company-wide administration list; a higher-level document or master record is not required.

The list shows the license and payment status for each module. It cannot be extended manually – new rows are created exclusively by activating a license key. The following fields are displayed:

| Field | Explanation |
|------|-------------|
| **Module GUID** | Unique identifier of the module. When set, it links the module row to the installed app and to the value assignments; it is filled automatically during license retrieval and cannot be edited. |
| **Name** | Display name of the module. Set during license retrieval and used in all messages (e.g. reminder notices) to identify the module. |
| **License Key** | The key stored for this module. When set, the app can retrieve the module and product data from the m+m service and keep them up to date; if it is empty, no reconciliation takes place for this module. |
| **Bought As Bundle** | When enabled, the module was purchased as part of a product bundle; the license data then originates from the associated product rather than from a standalone module key. If the flag is not set, the module is licensed individually. The field is filled automatically and cannot be edited. |
| **Related Product** | Name of the product from which this module originates. When filled, the row refers to an entry in **m+m Products** and shares the license key with other modules of the same bundle. |
| **License Type** | Controls how the usage authorization is checked. The three possible values and their effect are described under "License Type and Its Values". |
| **Assigned Licensed Values** | Number of currently enabled assignments (enabled users or companies) for this module. When this value reaches the **Licensed Values**, the app prevents the creation of another entry on the next assignment. The value is calculated automatically from the value assignments. |
| **Licensed Values** | Maximum number of simultaneously permitted assignments according to the license (e.g. number of licensed users). When reached, the app does not allow any further enabled assignment and reports an error. |
| **Valid Until** | Expiry date for time-limited licenses (trial versions). When set and exceeded, the module is considered no longer valid; it is automatically uninstalled on the next run and the associated data is deleted. If the field is empty, the license is unlimited. |
| **Last Payed** | Date of the last recorded payment. Serves as proof of the payment history and is updated during license retrieval. |
| **Next Pay Day** | Due date of the next payment. If this date is exceeded without a payment being received, the module can become overdue. |
| **Overdued** | When enabled, the payment for this module is outstanding; the app shows a payment notice when the module is called and – depending on the reminder level – sends a notification. If the flag is not set, the module is fine on the payment side. |
| **Overdued Since** | Date since which the payment has been outstanding. Serves to track how long a module has already been overdue. |
| **Reminder Level** | Escalation level of the outstanding payment. When the level is greater than 0, a warning notice appears when the module is called; from level greater than 3, the notice becomes an error message and use of the module is blocked. |

The fields **Last Payed**, **Next Pay Day**, **Overdued**, **Overdued Since**, and **Reminder Level** are filled exclusively by the m+m license service and cannot be edited manually. Their meaning during operation is described in the section "License Check, Payment, and Reminder Levels".

#### License Type and Its Values

The **License Type** field determines which check applies when a module is called and whether an additional assignment is required. It can take exactly three values:

- **per User:** The module may only be used by explicitly assigned users. When selected, you must enter the authorized **users** via **Value Assigment**; if an unassigned user calls the module, the app reports that the user is not authorized for the module. The number of simultaneously enabled users is limited by the **Licensed Values**.
- **per Company:** The module may only be used in explicitly assigned companies. When selected, you enter the authorized **companies** via **Value Assigment**; in an unassigned company, the app reports that the company is not assigned to the module. The number of permitted companies is limited by the **Licensed Values**.
- **Flat-Rate:** The module can be used by all users and all companies without any further assignment. When selected, **Value Assigment** is omitted entirely; the license check ends immediately without any user or company control.

#### Setting Up License Activation

The administrator carries out this setup once per license key, before the associated modules are used for the first time. It connects the purchased key with the m+m license service and fills the **m+m Modules** list.

1. First check the **prerequisites** (see above): valid **License Key** and installed modules.
2. Open the **m+m Modules** page via the **Search**.
3. Choose **Actions** → **Update/Insert Entry**. When run, the app opens the **Input Page**, where you are prompted to enter your license key.
4. In the **Input Page**, under the label **Insert your License Key**, enter your key and confirm with **OK**. When confirmed, the app uses the key to retrieve the associated module and product data from the m+m service and creates or updates the entries in **m+m Modules** (and **m+m Products**). With **Cancel**, you discard the entry without retrieval.
5. Leave the page via **Close**. The licensed modules now appear in the list with **License Type**, **Licensed Values**, and payment data.

**Operational use:** After this step, modules with the license type **Flat-Rate** are immediately ready for use. Modules with the license type **per User** or **per Company** additionally require the appropriate assignment – see the two following sections.

#### Assigning a License per User (Setup)

For modules with **License Type = per User**, the administrator defines which users may use the module. This assignment takes place after license activation and is used during operation on every module call.

1. Open the **m+m Modules** page and select the row of the module with the **License Type** **per User**.
2. In the row, choose the **Value Assigment** action. When run, the app opens the **m+m License Value Assignment** page, already filtered to this module and this license type.
3. Enter one row per authorized user. Field meanings:

| Field | Explanation |
|------|-------------|
| **Type** | Shows the assignment type and corresponds to the **License Type** of the module (**per User**). The value **Flat-Rate** is not permitted here; if you select it, the app reports that this type may not be used. The field cannot be changed manually and is taken from the module. |
| **No.** | The user to be assigned (user name). When entered, exactly this user may use the module; the selection refers to the BC user management. When entered, the **Enabled** flag is set automatically. |
| **Assigend Module GUID** | Reference to the module for which the assignment applies. It is a mandatory field (highlighted as required); via the module GUID, the app ensures that the assignment belongs to the correct module and the correct license type. |
| **Module Name** | Name of the assigned module. Determined automatically from the **Assigend Module GUID** and used for display only. |
| **Enabled** | When enabled, the user may use the module. If the flag is disabled, the user can no longer use the module and receives an error message when calling it. Disabled assignments do not count against the **Licensed Values**. |

4. Pay attention to the module's **Licensed Values**: if the number of enabled users exceeds the licensed quantity, the app prevents creation and reports that the license does not allow any further users (stating the current assignment and the licensed values).
5. Leave the page via **Close**. The enabled assignments appear immediately in the module's **Assigned Licensed Values** field.

**Operational use:** If an assigned and enabled user calls one of the m+m modules, the license check permits use. A user who is no longer enabled receives the corresponding notice. If a user is disabled in the BC user management, the app automatically sets the associated assignment to not **Enabled**; if the user is deleted, the app automatically removes their assignments.

#### Assigning a License per Company (Setup)

For modules with **License Type = per Company**, the administrator defines in which companies the module may be used. The procedure corresponds to the user assignment, but companies are entered instead of users.

1. Open the **m+m Modules** page and select the row of the module with the **License Type** **per Company**.
2. Choose the **Value Assigment** action. The **m+m License Value Assignment** page opens for this module.
3. Enter one row per authorized company. The fields **Type**, **No.**, **Assigend Module GUID**, **Module Name**, and **Enabled** have the same meaning as in the user assignment – but in the **No.** field you select the **company**.
4. Here too, the **Licensed Values** limit the number of permitted companies. When reached, the app prevents further assignments.
5. Leave the page via **Close**.

**Operational use:** In an assigned company, the license check permits use of the module; in an unassigned company, the app reports that the company is not assigned to the module. If a company is deleted, the app automatically removes its assignments.

#### Show Installed m+m Modules

This action supports the administrator in reconciling actually installed apps with licensed modules – helpful during initial licensing and when purchasing additional modules later.

1. Open the **m+m Modules** page.
2. Choose the **Show installed m+m Modules** action. When run, the app determines all installed apps of the publisher and opens the **m+m Module Overview**.

The **m+m Module Overview** is a pure display list (not editable) with the following fields:

| Field | Explanation |
|------|-------------|
| **App ID** | Unique identifier of the installed app. Used for reconciliation with the **Module GUID** in the license list. |
| **License Key** | The key stored for the app, provided the module is already licensed. When filled, the app is already part of an active license. |
| **Licensed** | When enabled, a license entry with a key already exists for this app. If the flag is not set, the installed app is not yet licensed and should be activated via a license key if applicable. |
| **Name** | Display name of the installed app. |

#### Permissions

Cloud Base includes the permission set **All permissions** (`MuM PAY Permission`). It defines the permissions for the app's tables and pages and determines which actions users may perform in Cloud Base (read, create, modify, and delete the license and assignment data). Assign this permission set to the users who are to activate licenses and maintain assignments.

## Master Data

Cloud Base does not maintain its "master data" – modules and products – manually, but automatically via the license key. The two following lists show the retrieved data. They are filled by the m+m license service; creating rows manually is not intended.

### Modules

The complete field list of the **m+m Modules** page is documented in the **Setup** chapter. The page is at the same time the central master data list of the module: each row represents a licensed m+m module with **License Type**, **Licensed Values**, **Assigned Licensed Values**, validity, and payment status. Here, administrators maintain only the **License Key** (via **Update/Insert Entry**); all other values are the result of the license retrieval.

### Products

A product bundles several modules under a common license key. The **m+m Products** list shows the retrieved product data.

**Access:** Open the **m+m Products** page via the **Search**.

| Field | Explanation |
|------|-------------|
| **Product GUID** | Unique identifier of the product. When set, it assigns the associated modules to the product via their **Related Product**; it is filled during license retrieval. |
| **Product Name** | Display name of the product. Serves to recognize the purchased bundle in the list and among the assigned modules. |
| **License Key** | The key under which the product and all included modules are licensed. When filled, the modules bought as a bundle share this key; another retrieval via **Update/Insert Entry** updates all included modules together. |

The **m+m Products** page offers the same **Update/Insert Entry** action as the module list: it opens the **Input Page**, where you enter a **License Key** to retrieve or update the product and module data.

## License Check, Payment, and Reminder Levels

This section describes how Cloud Base uses the stored license and payment data during operation. These processes run automatically; they are not triggered via an action, but are initiated when the individual m+m modules are called. You control the behavior via the setup (license key and value assignments); the result appears as a notice or error message to the user.

**License check when a module is called.** When a user calls an m+m module, Cloud Base checks the license based on the **License Type**:

- **Flat-Rate:** no further check – the module is usable by everyone.
- **per User:** It is checked whether the current **user** has an enabled assignment. If it is missing, the user receives the notice that the user is not authorized for the module.
- **per Company:** It is checked whether the current **company** is assigned. If the assignment is missing, the notice appears that the company is not assigned to the module.

**Validity.** If a **Valid Until** date is set and exceeded, the app reports that the module is no longer valid (stating the validity date). Such time-limited modules (trial versions) are automatically uninstalled on the next run and the associated data is deleted.

**Payment status and reminder levels.** The m+m license service updates **Overdued**, **Overdued Since**, **Next Pay Day**, **Last Payed**, and **Reminder Level**. This results in the following escalation when a module is called:

- **Reminder Level = 0:** no notice – the payment is fine.
- **Reminder Level > 0:** The user receives the warning notice that the module must be paid and that the warning becomes an error after the 3rd reminder level.
- **Reminder Level > 3:** Use is treated as an error; the user is prompted to settle the outstanding invoice.

**Automatic notification.** In the case of an outstanding payment, Cloud Base additionally sends an email automatically. The recipient is your company's email address stored in the **Company Information**; the support and billing addresses of markmann+müller are informed in copy. The subject states the reminder level reached, the customer, and the affected module. This notification takes place without any action by the user; the prerequisite is a maintained email address in the **Company Information** as well as a configured email connection in Business Central.

## Module Lifecycle

### Valid Until (Demo Version)

For a demo version of certain modules, the **Valid Until** field is filled. When this date is exceeded, the module is automatically uninstalled and the associated data is deleted. If you want to use a demo module permanently, activate a regular license key in good time.

### Subsequent Purchase of Modules

To add further modules later, apply the **Setting Up License Activation** step again: open **m+m Modules**, choose **Update/Insert Entry**, and enter the (possibly new) **License Key**. The retrieval adds new modules and updates existing entries. Via **Show installed m+m Modules**, you can then check whether all installed apps are licensed.

### Removing a Module from the License

If a module is removed from the license, for example in the case of a cancellation, the associated app is automatically uninstalled on the next run. Where applicable, the app data is also deleted in the process. Manually removing the module row is not required.

## Typical Use Cases

The following examples show the two most common workflows. All pages and actions mentioned correspond to the actual application.

### Use Case 1: Activating a New License After a Module Purchase

**Trigger:** Your company has purchased a new m+m module. A **License Key** is shown on the delivery note.

**Entry point in BC:** The administrator checks in **Extension Management** that the app is installed, and then opens the **m+m Modules** page via the **Search**.

**Core workflow:**

1. On **m+m Modules**, the administrator chooses **Actions** → **Update/Insert Entry**.
2. In the **Input Page**, they enter the **License Key** and confirm with **OK**.
3. Cloud Base retrieves the module and product data; the modules appear in the list with **License Type**, **Licensed Values**, and payment data.
4. They leave the page via **Close**.

**Completion:** Via **Show installed m+m Modules**, the administrator checks in the **m+m Module Overview** that the **Licensed** flag is set for the installed app. Modules with the license type **Flat-Rate** are now usable without any further steps.

### Use Case 2: Enabling a New Employee for a Module

**Trigger:** A new colleague is to use a module with the **License Type** **per User**. The request reaches the administrator by email.

**Entry point in BC:** The administrator opens the **m+m Modules** page via the **Search** and selects the relevant module row.

**Core workflow:**

1. In the row, they choose the **Value Assigment** action; the **m+m License Value Assignment** page opens for this module.
2. They create a new row and select the new user in the **No.** field. The **Enabled** flag is set automatically.
3. If the license is not sufficient, Cloud Base reports that no further users may be assigned (stating the current assignment and the **Licensed Values**). In this case, the administrator contacts their consultant to increase the license.
4. They leave the page via **Close**.

**Completion:** The module's **Assigned Licensed Values** field increases by one. The employee can now use the module. If the authorization is to be revoked later, the administrator removes the **Enabled** flag in the corresponding row.

## FAQ and Troubleshooting

### 1. Why is the "m+m Modules" list empty after installation?

Because no **License Key** has been activated yet. The modules are only retrieved from the m+m license service via **Update/Insert Entry** and the entry of a valid key. Carry out the activation as described in the **Setup** chapter.

### 2. Why does Cloud Base not work in my on-premises installation?

The app is intended exclusively for the cloud. In on-premises environments, license retrieval and the license check are disabled; no module or payment data is retrieved.

### 3. Why does a user receive the message that they are not authorized for a module?

The module has the **License Type** **per User**, and no enabled **value assignment** exists for this user. Enter the user on the **m+m License Value Assignment** page and make sure that the **Enabled** flag is set.

### 4. Why can I not assign another user?

The number of enabled assignments has reached the module's **Licensed Values**. Cloud Base then prevents further assignments and reports the current assignment as well as the licensed values. Disable an assignment that is no longer needed, or increase the license via your consultant.

### 5. Why can the "Flat-Rate" type not be used in the value assignment?

A **Flat-Rate** license applies to all users and companies without an assignment. An individual assignment would therefore be contradictory; the app explicitly rejects the **Flat-Rate** type in the **m+m License Value Assignment**.

### 6. What does a filled "Valid Until" field mean?

The module runs as a time-limited demo version. After the **Valid Until** date is exceeded, the module is automatically uninstalled and the data is deleted. Activate a regular **License Key** before expiry to continue use.

### 7. Why does a payment notice appear when a module is called?

A payment is outstanding for the module (**Overdued** is set, **Reminder Level** greater than 0). The notice prompts for payment and points out that the warning becomes an error after the 3rd reminder level. Settle the invoice so that the m+m license service resets the status.

### 8. What happens when the reminder level rises above 3?

From a **Reminder Level** greater than 3, the outstanding payment is treated as an error and use of the module is blocked. The user is prompted to settle the invoice. Once payment is received, the license service updates the status.

### 9. Who receives the automatic payment email?

The email address of your company stored in the **Company Information**, with a copy to the support and billing addresses of markmann+müller. For sending to work, an email address must be maintained in the **Company Information** and an email connection must be configured in Business Central.

### 10. What happens to the assignments when I delete a user or a company?

Cloud Base removes the associated **value assignments** automatically: when a user or a company is deleted, their assignments are deleted. If a user is only disabled in the user management, the app automatically sets the assignment to not **Enabled**, so that it no longer counts against the **Licensed Values**.
