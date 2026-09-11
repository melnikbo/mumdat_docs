---
title: Anwenderhandbuch m+m Master Data Management
---

# User Guide m+m Master Data Management

## Introduction

The **m+m Master Data Management** (Main Company) extension makes it possible to automatically keep selected master data **in sync across multiple companies** in Microsoft Dynamics 365 Business Central. If a user changes, for example, the name of a **Customer** in one company, this change is propagated to one or more other companies – without the record having to be edited manually there again.

Synchronization is **field-level**: you define which fields of which tables are transferred between which companies. The exchange can be **bidirectional** (all participating companies are kept at the same state) or **top-down** (a leading master company distributes its data to the remaining companies). Target and source companies can be combined freely; the target companies can reside in the same or in a different Business Central database. After the one-time setup, the data synchronization runs fully automatically.

### Target audience

The primary audience is **operational key users and administrators** who work in multiple companies and must keep the daily data state consistent – for example, customer, vendor, or item management, which maintains a change in one company and expects it to arrive in the remaining companies. Secondarily, this guide addresses **system administration**, which performs the one-time setup (Main Company Setup, transfer service, permissions).

### Brief process overview

1. Activate the **Main Company Setup** once and store the connection data (authorization); use the **Initialise** action to provide the released tables.
2. Create a **Transfer Service** that describes the target database and the authentication.
3. Define a **Main Company Transfer**: synchronization type, participating companies (**Main Company Assignment**), the **Transfer Fields** to be transferred, and optional **Company Filters**.
4. Optionally copy existing base data into new companies via the **Company Initialization**.
5. Monitor ongoing operation via the **Main Company Transfer Data Asynchronous Log** and the **Main Company Error Transfer Log** and follow up on errors.

## Quick start for users

The quick start describes the shortest path from setup to the first running synchronization. The steps follow the technical dependency order (first setup, then configuration, then operation).

1. **Open the Main Company Setup.** Use the **Search** to open the **Main Company Setup** page. Set **Active** to “Yes”, choose the login method under **Authorization** (**Basic** or **OAuth**), and store the corresponding credentials.
2. **Initialise.** In the Main Company Setup, choose the **Initialise** action. Afterwards the released tables are available for selection in the transfers. This action only needs to be run once.
3. **Create a Transfer Service.** Use the **Search** to open the **Transfer Service List**, create a record, and store the **Code**, **ODataV4 Address**, and the **Authorization**. Check the connection with **Test Connection**.
4. **Create a Main Company Transfer.** Use the **Search** to open the **Main Company Transfer List** and create a new record. Open the line to edit the **Main Company Transfer Card**. Enter **Code**, **Description**, **Transfer Service Code**, and the **Synchronization Type**.
5. **Assign companies.** In the **Main Company Assignment** area, add the participating companies. For the synchronization type **Top-Down**, activate the **Master** flag on exactly one company.
6. **Select fields.** In the **Transfer Fields** area, select the tables and fields. Use **Add All Fields From Table** to take over all fields of a table at once.
7. **Set to active.** Set the transfer to **Active** in the header. From now on, changes to the selected fields are transferred automatically.
8. **Optional – Copy base data.** In the **Main Company Transfer List**, choose the **Company Initialization** action, create an **Initialize Companies** run, define **Source Company** and **Target Company** per line, and start with **Start Asynchronous Process**.
9. **Monitor.** If needed, check the **Main Company Error Transfer Log**; correct failed lines and re-trigger them with **Try Again** or **Send data**.

☞ All Main Company setups are **cross-company** and only need to be performed once.

## Setup

The setup is the foundation of the module and is performed by **system administration** before first use. It comprises the global **Main Company Setup**, at least one **Transfer Service**, the designation of the **responsible persons** for notifications, and the **permissions**.

### Main Company Setup

**Process.** The Main Company Setup is a **cross-company single card** (one record for all companies). Here the administrator specifies whether the module is active, with which authorization data is exchanged between companies, and whether the exchange should run asynchronously via job queues. Only when **Active** is set are changes actually transferred; the concrete usage takes place later in the **Main Company Transfers** (see chapter *Setting up Main Company Transfers*).

**Entry point:** Use the **Search** to open the **Main Company Setup** page.

Explanations of the fields on the **Main Company Setup** card:

| Setup | Explanation |
|---|---|
| **Active** | When enabled, the module actually performs the data exchange; without this flag, changes to released fields are **not** sent to other companies. This is the central on/off switch of the entire module. |
| **Log Success Message** | When enabled, **every successful transfer** is recorded in the error log in addition to errors. Use this for traceability during the rollout phase; in continuous operation it produces many entries and is usually left disabled. |
| **Authorization** | Determines how the module authenticates against the target database. Choose the value according to the login method (see the following value list). The selection shows the matching login fields. |
| **Transfer User** | When set, the module logs in with this user account for **Basic** authorization. The user must have SUPER rights in **all** companies; otherwise the entry is rejected. |
| **Password** | When set, this password together with the Transfer User is used for the **Basic** login. Without a Transfer User, no entry is possible. |
| **Different ODataV4 Address** | When set, the module uses this server port/endpoint address for the web service calls instead of the environment's default address. Use this when the target database is reachable via a different OData address. |
| **Asyncronous Mode** | When enabled, data changes are not sent synchronously right away but are queued for later processing. In combination with the Asynchronous Option, this controls how transfers are executed with a time delay. |
| **Asynchronous Option** | Determines the method of the delayed sending (see the following value list). When **Job Queue** is selected, a note appears that a job queue must be set up in each participating company. |
| **Start Date/Time Asynchronous Option** | When set, the asynchronous job queues start from this point in time. The field is only active for the Asynchronous Option **Job Queue**; the point in time must be in the future. |
| **Client ID** | When **OAuth** is selected: the application ID (Client ID) of the registered Azure app with which the module authenticates. Mandatory field for OAuth. |
| **Client Secret** | When **OAuth** is selected: the client secret of the app. Mandatory field for OAuth; stored masked. |
| **Authority URL** | When **OAuth** is selected: the endpoint address at which the access token is requested. Mandatory field for OAuth. |

**Values of the Authorization option** (task-relevant meaning per value):

- **Basic:** Login with **Transfer User** and **Password**. The Basic fields are shown; the OAuth fields are cleared.
- **OAuth:** Login via **Client ID**, **Client Secret**, and **Authority URL**. The OAuth fields are shown; the Basic fields are cleared.

**Values of the Asynchronous Option:**

- **Default:** Queued changes are sent via a one-time background task as soon as they arise. No permanent job queue per company is required.
- **Job Queue:** Sending is done via recurring job queues that must be set up **in each participating company**. Note: If another company assigns the same value in the meantime, the data can diverge – this option must be chosen with care.

Explanations of the actions on the **Main Company Setup** card:

| Action | Explanation |
|---|---|
| **Initialise** | When run, all tables permitted for the module are inserted and the internal web service is registered; with asynchronous mode active, the job queues in the participating companies are additionally prepared. This action must be run once so that tables can subsequently be selected in the transfers. |

**Sequence of the initial activation (in dependency order):**
1. **First**, set **Active** and store the **Authorization** together with the credentials. If this is missing, no data transfer takes place despite defined transfers.
2. **Then** run the **Initialise** action so that the permitted tables are available.
3. **Finally** – if delayed operation is desired – set **Asyncronous Mode** and **Asynchronous Option** and, if applicable, define the **Start Date/Time Asynchronous Option**.

☞ Permission rule: Not every table may be synchronized. The **Initialise** action provides the permitted tables (e.g. **Customer**, **Vendor**, **Item**, **Contact**, **G/L Account**, and related master tables); other tables are excluded to preserve data consistency.

### Setting up the Transfer Service

**Process.** A **Transfer Service** describes **one target database** together with authentication. It is created by the administrator before the first transfer and is later referenced in the **Main Company Transfer Card** (field **Transfer Service Code**) and per company in the **Main Company Assignment**. For transfers within the same database, the service can be flagged as **Same Database**; for a separate target environment, store its OData address and login.

**Entry point:** Use the **Search** to open the **Transfer Service List** and open the **Transfer Service Card** with “New”.

Explanations of the fields on the **Transfer Service Card**:

| Setup | Explanation |
|---|---|
| **Code** | When set, this unique code identifies the service; it is selected under this code in transfers and assignments. Mandatory field. |
| **Description** | When set, the explanatory text makes it easier to select the correct service in lists. |
| **ODataV4 Address** | When set, the module sends the transfers to this OData V4 endpoint address of the target database. |
| **Default** | When enabled, this service is considered the preset service and is used when no other service is selected elsewhere. Only **one** default service is allowed; a second one is rejected. |
| **Same Database** | When enabled, the service points to the **same** database; log entries are then created only once to avoid duplicates. Use this for cross-company synchronization within a single environment. |
| **Authorization** | Determines the login method (**Basic** or **OAuth**); the selection shows the matching field group and clears the other. |
| **Transfer User** | When **Basic** is selected: user name for logging in to the target database. The user must have SUPER rights in all companies. |
| **Password** | When **Basic** is selected: associated password; can only be entered together with the Transfer User. |
| **Client ID** | When **OAuth** is selected: application ID (Client ID) for the OAuth login. |
| **Client Secret** | When **OAuth** is selected: client secret; stored masked and only entered together with the Client ID. |
| **Authority URL** | When **OAuth** is selected: authority URL at which the token is requested (e.g. the tenant's Microsoft login endpoint). |
| **Scope** | When **OAuth** is selected: the requested OAuth scope for accessing the Business Central API. |

**Values of the field groups Basic Authentication / OAuth:** The **Basic Authentication** group is only visible when **Authorization = Basic**; the **OAuth** group only when **Authorization = OAuth**. Exactly one group is always shown.

Action of the **Transfer Service Card**:

| Action | Explanation |
|---|---|
| **Test Connection** | When run, the module first checks the completeness of the credentials and then establishes a test connection to the target database. On success, a confirmation appears; otherwise an error text with the cause. Run the test before using the service productively. |

The **Transfer Service List** shows the services at a glance:

| Field | Explanation |
|---|---|
| **Code** | Unique code of the service. |
| **Description** | Explanatory text for quick selection. |
| **ODataV4 Address** | Target address of the transfer. |
| **Authorization** | Login method (Basic/OAuth) of the service. |
| **Default** | Marks the preset service. |

☞ A Transfer Service cannot be deleted as long as it is used by one or more Main Company Transfers.

**Relationship to the Main Company Setup:** If Authorization and credentials are fully maintained in the Main Company Setup, the module automatically creates or updates a default Transfer Service with the code **DEFAULT**. Transfers without their own Transfer Service Code use this default service.

### Responsible persons and notifications (User Setup)

**Process.** So that the right people are informed about failed transfers and about obsolete fields, the administrator marks the responsible users in the **User Setup**. The flags control the email sending from ongoing operation (see chapter *Asynchronous operation and logs*).

**Entry point:** Use the **Search** to open the **User Setup** and select the line of the responsible user.

| Setup | Explanation |
|---|---|
| **Main Company Resp. Person** | When enabled, this user receives an email as soon as a transfer fails and an entry is created in the error log. A prerequisite is a stored **Email** address in the user line; without an email, setting the flag is rejected. |
| **Main Company Receive Email Obsolete Fields** | When enabled, this user receives a regular email about tables and fields that have been made obsolete or no longer exist in the database. When activating, a recurring job queue for the sending is created automatically. Here too, an email address is a prerequisite. |

**Sequence:** **First** store an **Email** address in the user line, **then** activate the respective flag. Without an email address, activation is not possible.

### Permissions

For using the module, a permission set is available that bundles access to the tables, pages, and processing of the module. The permission set **defines which actions users can perform in the module** – from reading the transfers to creating and changing the configuration. Assign it to the users who set up or monitor Main Company Transfers.

☞ Independently of the permission set, the **Transfer User** stored in the setup or in the Transfer Service must have SUPER rights in **all** participating companies, because it technically performs the cross-company data exchange.

## Setting up Main Company Transfers

A **Main Company Transfer** is the actual configuration of a synchronization. It bundles three areas in one card: the **header** (basic data and synchronization type), the **Main Company Assignment** (which companies participate), and the **Transfer Fields** (which fields of which tables are transferred). In addition, a **Company Filter** can be stored per company.

**Controlling preconditions.** This configuration is controlled by the **Main Company Setup** (activation, authorization, asynchronous mode) and the selected **Transfer Service** (target database, authentication). If the module is not **Active** or credentials are missing, no data is sent despite a complete transfer. Therefore set up the setup and the Transfer Service first (see chapter *Setup*).

**Entry point:** Use the **Search** to open the **Main Company Transfer List**. Create a new line and open it to edit the **Main Company Transfer Card**.

The overview **Main Company Transfer List** shows:

| Field | Explanation |
|---|---|
| **Code** | Unique name of the transfer; it is referenced by this in all further steps. |
| **Description** | Explanatory text for the transfer. |
| **Synchronization Type** | Shows whether synchronization is bidirectional or top-down (for details, see header). |

### Header of the transfer (General area)

| Field | Explanation |
|---|---|
| **Code** | When set, this unique code serves as the key of the transfer; assignments, fields, and filters refer to it. |
| **Description** | When set, the description makes it easier to recognize the transfer in lists and in the Initialize Companies. |
| **Transfer Service Code** | When set, synchronization is done via this Transfer Service (target database + login). When changing, the module checks that the same table of the same company is not already configured in another transfer with the same service – this prevents duplicate, contradictory transfers. |
| **Synchronization Type** | Determines the transfer direction (see value list). The selection determines whether a master company is required. |
| **Initialize Order** | When set (value other than 0), this transfer participates in the **Company Initialization** and is processed in this order. The value must be unique; a duplicate value is rejected. If the field remains 0, the transfer is skipped during initialization. |
| **Active** | When enabled, the transfer is armed and field changes are transferred; when activating, the point in time is recorded in **Active From**. Without this flag, the configuration has no effect. |
| **Active From** | Automatically shows the point in time from which the transfer was set to active (not editable). |

**Values of the Synchronization Type:**

- **Bidirectional:** The data is kept at the same state in **all** participating companies. A change in any company is distributed to the others. Suitable when all companies should carry the same data. For this type, **no** master company may be set; if one is still present, it must be removed.
- **Top-Down:** Only the changes of the **master company** are copied to the remaining (target) companies. Changes in the subordinate companies are **not** redistributed. Suitable when there is a leading company and the remaining companies may adjust field contents individually. For this type, exactly **one** master company must be defined.

☞ Only the fields stored in the **Transfer Fields** are transferred.

### Main Company Assignment

**Process.** In the Main Company Assignment, the administrator defines **which companies** participate in this transfer and – for “Top-Down” – which company is the source/master company. Per company, a different Transfer Service and a Company Filter can be stored.

| Field | Explanation |
|---|---|
| **Company Name** | When set, this company participates in the transfer. Via the lookup, you select a local company or – if a Transfer Service is stored – a company of the target database. Company names with special characters are rejected. |
| **Master** | When enabled, this company is the **source company** from which, for “Top-Down”, the data is distributed; all remaining companies are automatically target companies. The flag is only allowed for the synchronization type **Top-Down**, and there may only ever be **one** master company. If the master is to be changed later, the entire transfer must be recreated. |
| **Transfer Service Code** | When set, this company uses a **different** Transfer Service; if the field is empty, the service from the header applies or own (local) companies are shown. Use this when individual target companies reside in a different database. |
| **Filter Exists** | Indicates whether a filter has already been set up for this company via the **Company Filter** action (not editable). |
| **Job Queue Status** | For asynchronous mode, shows the current status of the company's associated job queue (see value list); it serves to monitor whether sending is running. |

**Values of the Job Queue Status:** **Ready** (task can start), **In Process** (sending is running), **Error** (execution failed), **On Hold** (paused – e.g. until release), **Finished** (completed), **On Hold with Inactivity Timeout** (paused due to a time limit on inactivity).

Action of the Main Company Assignment:

| Action | Explanation |
|---|---|
| **Company Filter** | When run, the **Main Company Table Filter** opens for the selected company of this transfer. There you restrict which records are considered before the transfer (see section *Company Filter*). |

**Entry point for the Company Filter:** In the **Main Company Assignment**, open the desired line and choose the **Company Filter** action.

### Transfer Fields

**Process.** Here the administrator defines, **field by field**, which fields of which tables are synchronized. Only after the **Initialise** action (Main Company Setup) are the permitted tables available for selection.

| Field | Explanation |
|---|---|
| **Table ID** | When set, the selected field is transferred from this table. A table may only be used **once** within a transfer; this prevents endless loops and inconsistencies. |
| **Table Caption** | Shows the name of the selected table (not editable). |
| **Field ID** | When set, this field is synchronized between the companies. Via the drilldown, you select the field from the table; normal, non-obsolete fields are available. |
| **Field Caption** | Shows the name of the selected field (not editable). |
| **Is Primary Key** | Indicates whether the field is part of the table's primary key. These fields identify the record and are needed for the assignment in the target company. |
| **Validate Value** | When enabled, the check/validation logic stored for the field is run when the value is transferred in the target company (e.g. a check for permissibility). Without this flag, the value is written without any additional check. Activate it to avoid inconsistencies. |
| **Obsolete State** | Indicates whether the field has been made obsolete (“Pending”) or removed (“Removed”) in the database. A value indicates that the transfer of this field should be reviewed. *(Note: The status values “Pending”/“Removed” are shown in English form in the current delivery.)* |

Actions of the Transfer Fields:

| Action | Explanation |
|---|---|
| **Add All Fields From Table** | When run, the module takes over all normal, active, non-obsolete non-key fields of the table into the Transfer Fields at once. Use this when nearly the entire table is to be synchronized, instead of selecting each field individually. |
| **Show Related Tables and Fields** | When run, the module shows, in a tree display, the tables and fields connected to the selected table via table relations and allows them to be taken over. This ensures that dependent master tables (e.g. linked codes) are also synchronized. |

The **Main Company Related Table Fields** page (tree view) highlights in color which connected entries are already included in the transfer and which are missing; with **Show all Fields** you undo a set filter again. The helper pages **Fields** and **Tables** serve solely for the selection or review of obsolete objects via the drilldowns.

**Sequence of the field selection (in order):**
1. **First** select the table via **Table ID** (only permitted tables).
2. **Then** select the **Field ID** per field or take them over with **Add All Fields From Table**.
3. Optionally use **Show Related Tables and Fields** to add dependent tables.
4. For sensitive fields, activate **Validate Value**.

### Company Filter (Main Company Table Filter)

**Process.** For each company stored in the Main Company Assignment, it can be defined **which records** are considered before the transfer. This way, for example, only customers of a particular city are synchronized.

**Entry point:** In the **Main Company Assignment**, open the line of the company and choose the **Company Filter** action. The **Main Company Table Filter** opens.

| Field | Explanation |
|---|---|
| **Table ID** | When set, the filter is applied to records of this table before synchronization. The tables used in the Transfer Fields are available for selection. |
| **Table Caption** | Shows the name of the table (not editable). |
| **Field ID** | When set, the filter is applied to this field. Via the drilldown, you select the field. |
| **Field Caption** | Shows the name of the field (not editable). |
| **Filter Expression** | Determines the comparison type with which the filter value is checked (see value list). For comparisons such as “less than”/“greater than”, only numeric, date, or time fields are allowed; otherwise the entry is rejected. |
| **Filter Value** | When set, only records whose field value matches the condition are transferred. For fields with a table relation, Yes/No, or option fields, the lookup offers the permitted values. |

**Values of the Filter Expression:** **=** (equal), **<** (less than), **>** (greater than), **=<** (less than or equal), **>=** (greater than or equal), **<>** (not equal).

☞ Per table, each field can only be used **once** as a filter; multiple filter conditions across different fields are possible.

## Company Initialization

**Process.** When building a **new** company, no master data is present at first. The Company Initialization copies the base data defined in the transfers **once** from the source company into the target company – in a defined order (e.g. first customers, then dependent tables). It supplements the ongoing synchronization with the initial base data stock.

**Prerequisite.** Only transfers with an **Initialize Order** other than 0 participate (see header of the transfer). The source company corresponds, for “Top-Down”, to the master company.

**Entry point:** Use the **Search** to open the **Main Company Transfer List** and choose the **Company Initialization** action. The **Main Company Initialize Companies List** opens; open a line for the **Main Company Initialize Companies Card**.

Fields of the **Initialize Companies** (header):

| Field | Explanation |
|---|---|
| **Sequence** | Shows the automatically assigned, consecutive number of the initialization run (not editable). |
| **Description** | When set, the text names the purpose of the run and appears in the generated job queues. |
| **Start Date/Time** | When set, processing starts from this point in time; the value must be in the future. If it is in the past at start, the module offers to set it to one minute after the current time. |
| **Status** | Shows the progress of the run (see value list; not editable). Changes to the header and lines are only possible in the status **New**. |

Fields of the **Initialize Companies** (lines):

| Field | Explanation |
|---|---|
| **Transmission Code** | When set, this line is initialized via the selected Main Company Transfer; only transfers with a set Initialize Order can be selected. Upon selection, the source company is automatically prefilled from the master company. |
| **Transmission Description** | Shows the description of the selected transfer (not editable). |
| **Source Company** | When set, this is the company from which the base data is copied. It must correspond to the master company stored in the assignment; special characters are not allowed. |
| **Target Company** | When set, this is the company into which the data is copied. Source and target company must be **different**. |
| **Status** | Shows the line status of the run (analogous to the header). |
| **Total Queues** | Shows the number of job queues created for this line in the source company; via the drilldown you reach the job queue entries (for local companies). |

**Values of the Status (Initialize Companies):**

- **New:** Run created, not yet started. Only in this status are the header and lines editable.
- **Scheduled:** Job queues have been created in the source companies; processing is scheduled. Changes are no longer possible.
- **In progress:** The initialization is running.
- **Completed:** The run was completed fully and without errors.
- **Completed with errors:** The run was completed, but errors occurred (see error log).

Actions of the **Main Company Initialize Companies Card**:

| Action | Explanation |
|---|---|
| **Start Asynchronous Process** | When run, the module checks the lines, creates job queues in each source company, and sets the header and lines to **Scheduled**. From the start time, these tasks copy the base data into the target companies. Only one source company is allowed per creation transfer. |
| **Set Status to New** | When run, the associated job queues are removed and the header and lines are reset to **New**, so that the run can be edited again. Only possible in the statuses **Scheduled**, **Completed**, or **Completed with errors**. |

**Sequence (in dependency order):**
1. **First** set the **Initialize Order** in the transfers (chapter *Setting up Main Company Transfers*).
2. **Then** create an **Initialize Companies** run via **Company Initialization** and enter **Description** and **Start Date/Time**.
3. Per line, define **Transmission Code**, **Source Company**, and **Target Company**.
4. **Finally**, start with **Start Asynchronous Process**; monitor the progress via **Status** and **Total Queues**.

## Asynchronous operation and logs

After setup, synchronization runs automatically. Two logs are available for monitoring and error handling: the **Main Company Transfer Data Asynchronous Log** for queued changes still to be sent, and the **Main Company Error Transfer Log** for failed transfers.

### Main Company Transfer Data Asynchronous Log

**Entry point:** Use the **Search** to open the **Main Company Transfer Data Asynchronous Log**.

In asynchronous mode, data changes are first queued here and then sent in batches.

| Field | Explanation |
|---|---|
| **From Company** | Shows the company from which the change originates. |
| **Table ID** | Shows the table of the changed data. |
| **Table Caption** | Name of the table. |
| **Record Information** | Brief information about the affected record. |
| **Action** | Shows the queued action (see value list). |
| **Record-ID** | Internal identifier of the affected record. |
| **Status Text** | Shows an additional status/error message about the queued entry. |
| **Pending Sending** | When enabled, the entry is queued for sending and has not yet been sent. |

**Values of the Action:** **Insert** (new record), **Modify** (change), **Delete** (deletion), **Rename** (key change).

Actions of the Asynchronous Log:

| Action | Explanation |
|---|---|
| **Send Data** | When run, the selected entries are queued for sending and the asynchronous sending is triggered; successfully sent entries are subsequently removed. |
| **Mark as Sent** | When run, the selected entries are marked as sent (the **Pending Sending** flag is removed) without a new sending taking place. Use this to take changes that have already been taken over elsewhere out of the queue. |
| **Show Data** | When run, the associated data content (JSON) of the entry is displayed – useful for analysis. |

### Main Company Error Transfer Log

**Entry point:** Use the **Search** to open the **Main Company Error Transfer Log**.

If a transfer fails, this is recorded here. If **Log Success Message** is additionally active in the setup, successful transfers also appear.

| Field | Explanation |
|---|---|
| **Entry No.** | Automatically generated internal count number of the entry. |
| **From Company** | Company from which the data was to be transferred. |
| **To Company** | Company to which the data was to be transferred. |
| **Transfer Service Code** | Shows the Transfer Service used for the entry. |
| **Table ID** | ID of the table at which the operation occurred. |
| **Table Caption** | Name of the affected table. |
| **Record-ID** | Identifier of the affected record, if available. |
| **Action** | Action last executed for this table (see value list). |
| **Status** | Result of the transfer (see value list). |
| **Status Text** | Additional error or status text for analysis. |

**Values of the Status:** **(blank)** (no result yet), **Success** (transferred successfully), **Error** (transfer failed), **Corrected** (entry was reprocessed after correction).

Actions of the error log:

| Action | Explanation |
|---|---|
| **Show Data** | When run, the data content (JSON) pending transfer is displayed – helpful for error analysis. |
| **Try Again** | When run, the transfer of the active line is triggered again. Prerequisite: The **To Company** is the currently opened company. Only lines whose target company corresponds to the current company are processed (with a confirmation prompt). |
| **Send data** | When run, the selected entries are (re-)sent to the target company; afterwards, invalid error entries are cleaned up. Only lines whose source company is the current company are processed (with a confirmation prompt). |
| **Send data as Modified** | Like **Send data**, but the data is transferred as a change (Modify) instead of as a new record. Use this when the record already exists in the target company. |

☞ Notification: If a **Main Company Resp. Person** with an email is stored in the **User Setup**, this person automatically receives a notification email with the entry number for every new error entry.

## Typical use cases

The following examples show realistic triggers and the flow in Business Central. All pages and actions mentioned are present in the module.

### 1. Propagate a customer name change to all companies

- **Trigger:** Accounting reports that a customer has been renamed; the new name should apply in all companies.
- **Entry point in BC:** The one-time setup has been done: In the **Main Company Transfer List**, a transfer exists with **Synchronization Type = Bidirectional**, in the **Main Company Assignment** the participating companies are stored, and in the **Transfer Fields** the field **Name** is included for the customer.
- **Core flow:** The user opens the customer in the leading company and changes the name. Because the table and field are released and the module is **Active**, the change is automatically transferred to the remaining companies. For the bidirectional type, it does not matter in which company the change is made.
- **Completion:** If **Log Success Message** is active, an entry with status **Success** appears in the **Main Company Error Transfer Log**. Otherwise the log remains empty as long as no error occurs.

### 2. Populate a new company with master data

- **Trigger:** A new legal entity has been founded; the new company should receive the existing customers and dependent master data of the main company.
- **Entry point in BC:** The administrator uses the **Search** to open the **Main Company Transfer List** and chooses **Company Initialization**.
- **Core flow:** In the **Initialize Companies**, they create a run and enter **Description** and **Start Date/Time**. Per line, they select the **Transmission Code** (the transfer must have an **Initialize Order**); **Source Company** is prefilled from the master, and the new legal entity is chosen as **Target Company**. With **Start Asynchronous Process**, they start the run; the header and lines switch to **Scheduled**.
- **Completion:** The progress can be read from the **Status** and the **Total Queues**. After complete processing, **Completed** is shown (or **Completed with errors** if individual records failed – then check the error log).

### 3. Follow up on a failed transfer

- **Trigger:** A **Main Company Resp. Person** receives a notification email about a new error entry.
- **Entry point in BC:** They use the **Search** to open the **Main Company Error Transfer Log** and select the entry with status **Error**.
- **Core flow:** Via **Show Data**, they check the data content and the cause in the **Status Text** (e.g. a missing dependent record). After remediation, they switch to the affected **To Company** and choose **Try Again**; if the record already exists in the target, they use **Send data as Modified**.
- **Completion:** The entry receives the status **Corrected** or **Success**; invalid error entries are cleaned up in the process.

### 4. Set up a transfer to another database

- **Trigger:** The group operates two separate Business Central environments; master data should be synchronized from one to the other.
- **Entry point in BC:** The administrator uses the **Search** to open the **Transfer Service List** and creates a new **Transfer Service**.
- **Core flow:** They store the **ODataV4 Address** of the target environment and the **Authorization** (for **OAuth**: **Client ID**, **Client Secret**, **Authority URL**, **Scope**). With **Test Connection**, they check the reachability. Afterwards, they enter the **Transfer Service Code** in the header of the Main Company Transfer or per company in the **Main Company Assignment**.
- **Completion:** After a successful connection test, the transfers run via the service into the target database; errors appear with the respective **Transfer Service Code** in the error log.

## FAQ and troubleshooting

### Why are my changes not transferred to the other companies?
In the **Main Company Setup**, the **Active** flag is not set, or the transfer itself is not **Active**. Without these flags, the module sends no data. Also check whether the changed field is actually included in the **Transfer Fields**.

### Why can't I set a master company?
The **Master** flag is only allowed for the **Synchronization Type “Top-Down”**. For **Bidirectional**, no master may be set; if one is still present, remove it first. In addition, there can only ever be **one** master company per transfer.

### Why does the system report “It exists a Master Company” when switching to Bidirectional?
You changed the synchronization type from “Top-Down” to **Bidirectional**, but a company is still marked as **Master**. Remove the Master flag; after that, the switch is possible.

### Why is the Transfer User rejected?
The **Transfer User** stored in **Main Company Setup** or **Transfer Service** must have SUPER rights in **all** companies. If these are missing, the system reports that the user must have SUPER rights in all companies.

### Why can't a table be selected in the Transfer Fields?
Only the tables released by the **Initialise** action are available. Run **Initialise** in the **Main Company Setup**. To preserve data consistency, many tables are deliberately excluded.

### Why can't I delete or change a line in the transfer tables?
Transfer Fields are already stored for that table. First remove the associated fields; after that, the table line can be deleted or changed.

### Why do I get “Table is already configured”?
The same table of the same company is already configured in **another** Main Company Transfer with the **same Transfer Service**. This check prevents duplicate, contradictory transfers. Use the existing transfer or a different service.

### Why can I no longer edit the Initialize Companies?
Changes to the header and lines of the **Initialize Companies** are only possible in the status **New**. Reset the run with **Set Status to New** (from the statuses **Scheduled**, **Completed**, or **Completed with errors**) to edit it again.

### Why can't “Try Again” be run in the error log?
The **Try Again** action only works for lines whose **To Company** is the currently opened company. Switch to the target company and repeat the action. To send from the source company, use **Send data**.

### Why does the User Setup require an email address?
The flags **Main Company Resp. Person** and **Main Company Receive Email Obsolete Fields** trigger email notifications. Without a stored **Email** address in the user line, the respective flag cannot be activated. Enter the email address first.
