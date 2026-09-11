---
title: Anwenderhandbuch m+m Ext. Text Module with Logistic Management
---

# User Guide m+m Ext. Text Module with Logistic Management

This guide describes how to use the **m+m Ext. Text Module with Logistic Management** module in Microsoft Dynamics 365 Business Central. The module connects the **Extended Text Assignment** (text-block management from the m+m Ext. Text Module) with logistics planning – the **Advice Notification** and **Shipment Planning**. This makes it possible to automatically apply predefined text templates as header and line texts in advice notifications, shipment plannings and their registered documents, to print them on reports and to embed them in e-mails.

All pages, actions, fields and option values mentioned in this guide correspond to the English Business Central user-interface captions.

---

## 1 Introduction

### 1.1 Purpose of the Module

The module is a **connection module**: it brings the functions of the **Extended Text Assignment** into the logistics documents of the Advice Notification and Shipment Planning. Without this module, extended text blocks are only available in the classic sales and purchase documents. With the module, the same text templates also become available for the following processes:

- **Advice Notification** and **Registered Advice Notification**,
- **Shipment Planning** and **Registered Shipment Planning**,
- the **Warehouse Shipment** as the target process of Shipment Planning,
- the **Loading Point** as an additional assignment criterion.

The benefit for the user: recurring note texts (e.g. loading, transport or advice notes) are, after a one-time setup, written **automatically** to the correct place in the document – as pure on-screen information, as print text on the report, or as e-mail text.

### 1.2 Target Audience

The primary target audience are **operational users in logistics** who capture advice notifications and shipment plannings on a daily basis, supplement them with source documents, register and dispatch them. For these users the texts appear largely automatically; they only have to process the documents normally.

The secondary target audience are **administrators and key users** who perform the one-time setup: activating the processes, creating text templates and maintaining the assignment in the **Extended Text Assignment Worksheet**.

### 1.3 Short Process Overview

1. The administrator activates the required processes in the **Advice Notification Setup**, the **Shipment Planning Setup** and – if needed – the **Loading Point Setup**.
2. The key user creates the text blocks in the **Extended Text Templates**.
3. In the **Extended Text Assignment Worksheet**, the key user assigns each template to a **Process** (Advice Notification or Shipment Planning) as well as to a **Type** (Customer/Vendor …) and optionally to a **Sub Type** (Item, Item Category, Loading Point …).
4. The operational user creates an advice notification or shipment planning. The matching texts are applied automatically to the FactBoxes.
5. When the document is registered, the texts are transferred to the registered document and remain permanently available there.

---

## 2 Quick Start for Users

The quick start follows the technical dependency order: **first the setup**, then the templates, then the daily work.

1. **Activate the process (administrator).** Use **Search** to open the **Shipment Planning Setup** or **Advice Notification Setup** and set the respective activation switch (**Activate Shipment Planning** or **Activated**). For Loading Point-related texts, additionally activate the **Loading Point activated** switch in the **Loading Point Setup**.
2. **Create a text template (key user).** Use **Search** to open the **Extended Text Templates** and create a template with **Template No.**, **Printing Type** and the actual text content.
3. **Assign the template (key user).** Use **Search** to open the **Extended Text Assignment Worksheet**. Enter the **Template No.**, choose the logistics process in the **Process** field (**Shipment Planning** or **Advice Notification**), set **Type**/**Type No.** and – for line texts – **Sub Type**/**Sub Type No.**.
4. **Process the document (user).** Create a **Shipment Planning** or **Advice Notification**. The header texts appear automatically in the **Shipment Planning Text** or **Advice Text** FactBox.
5. **Add lines (user).** Retrieve the document lines: in the Shipment Planning via **Get Shipment Planning Lines**, in the Advice Notification via **Get Source Documents**. The line texts then appear in **Shipment Planning Line Text** or **Advice Line Text**.
6. **Check and open (user).** If needed, use the **Extended Shipment Planning Text** or **Extended Advice Text** action to open the preview page in order to check or regenerate the combined texts per document type.
7. **Register (user).** Register the document in the usual Advice Notification/Shipment Planning flow. The texts are thereby transferred to the **Registered Advice Notification** or **Registered Shipment Planning**.

---

## 3 Setup

The setup is the most extensive part of this module. It consists of three activation pages (process enablement), the template maintenance and the actual assignment in the worksheet. The activation pages are company-wide setup pages (one record per company) and are opened via **Search**.

### 3.1 Activating Processes

Before the module generates texts, the respective logistics process must be activated. If the process is not activated, the module generates **no** texts – the FactBoxes remain empty.

**Entry point:** Use **Search** to open the respective setup page.

| Setup | Explanation |
|---|---|
| **Activated** (in **Advice Notification Setup**) | When activated, the module automatically generates the assigned advice texts when an **Advice Notification** is created or changed and provides them in the FactBoxes; if the switch is not set, the text transfer for advice notifications is completely omitted. |
| **Activate Shipment Planning** (in **Shipment Planning Setup**) | When activated, the module automatically generates the assigned shipment planning texts when a **Shipment Planning** is created or changed; without activation, no extended texts are formed for shipment plannings. |
| **Loading Point activated** (in **Loading Point Setup**) | When activated, the sub types **Loading Point** and **All Loading Points** may be used in the **Extended Text Assignment Worksheet**, and Loading Point-related texts are determined per Loading Point; if the switch is not set, an attempt to save a Loading Point assignment is rejected with the message “The Loading Points are not activated or set up.”. |

> Note: The activation switches belong to the base module m+m Logistic Management; this module only reads them to decide whether texts are formed. The complete setup of Advice Notification and Shipment Planning itself is described in the base module's guide – for text generation the respective activation switch mentioned is sufficient.

### 3.2 Creating Extended Text Templates

Before you can assign texts, the text blocks must exist as **Extended Text Templates**.

**Process intro:** This task is performed by the key user once or as needed. The templates form the content basis; only afterwards can an assignment be made in the worksheet (see section 3.3). The templates later take effect on the documents during daily work (chapter 6).

**Entry point:** Use **Search** to open the **Extended Text Templates**; create a template with **+New** or open an existing one for editing.

The most important fields of the template:

| Field | Explanation |
|---|---|
| **Template No.** | Unique number of the text template; assigned from the number series when created. The template is later referenced in the worksheet via this number. |
| **Description** | Freely selectable internal short name of the template; makes it easier for the key user to find it again, is not printed on documents. |
| **Printing Type** | When set, the printing type determines **where** the text appears. See values below. |
| **Sub-Printing Type** | If the printing type **Report** is chosen, the sub-printing type sets the print position in the report; for the printing types **FactBox** and **Mail** the field has no effect. See values below. |

**Values of the Printing Type field** (each template receives exactly one printing type):

- **FactBox:** The text appears only in the FactBox of the respective page as internal on-screen information and is **not** printed.
- **Report:** The text is output in the report of the selected process and may therefore be printed on documents. The **Sub-Printing Type** can be selected only for this printing type.
- **Mail:** The text is embedded in the e-mail when an e-mail is sent for the document.

**Values of the Sub-Printing Type field** (only for printing type **Report**):

- **Header:** Print of the text in the header area of the report.
- **Footer:** Print of the text in the footer area of the report.
- **Before Position:** Print of the text before the respective document line.
- **After Position:** Print of the text after the respective document line.

### 3.3 Assignment in the Extended Text Assignment Worksheet

**Process intro:** In the **Extended Text Assignment Worksheet**, the key user defines **which** text template applies to **which** process and for **which** business partner or item. This assignment is the central control of the module; it is evaluated automatically during daily work (chapter 6). The prerequisites are created templates (section 3.2) and activated processes (section 3.1).

**Entry point:** Use **Search** to open the **Extended Text Assignment Worksheet**. The worksheet is a global page without a superordinate master document.

| Setup | Explanation |
|---|---|
| **Template No.** | Refers to the text template to be used. Via the lookup you select an existing template or create a new one with **+New**. When filled, the content of this template is applied in the matching process. |
| **Printing Type** | Inherited from the template and indicates whether the assigned text takes effect as **FactBox**, **Report** or **Mail** (see section 3.2). |
| **Type** | When set, the type restricts the assignment to a business-partner context at header level. See values below. |
| **Type No.** | If an individual-related type (Customer, Vendor, Customer Group, Vendor Group) is chosen, the specific number or posting group is stored here; the assignment applies only to this partner/this group. |
| **Sub Type** | When set, the sub type turns the assignment into a **line text** (line level). If the sub type remains **(blank)**, the assignment takes effect as a **header text**. See values below. |
| **Sub Type No.** | Specifies the sub type (e.g. the item number, the item category or the loading point number), provided the selected sub type requires a number. |
| **Process** | When set, the process determines for which logistics document the template applies. For this module, **Shipment Planning**, **Advice Notification** and **Warehouse Shipment** in particular are relevant. The text is formed only for this process. |
| **Process Object Name** | Shows the name of the object selected in the **Process** field; display only, for control purposes. |

**Values of the Type field** (each assignment receives at most one type):

- **(blank):** The assignment is not restricted to a business partner and takes effect regardless of the customer/vendor of the document.
- **Customer:** The assignment applies to exactly one customer; the customer is stored in **Type No.**. In the Shipment Planning, the customer is determined from the shipment or the driver contact.
- **All Customers:** The assignment applies uniformly to all customers.
- **Customer Group:** The assignment applies to a customer posting group; the group is stored in **Type No.**.
- **Vendor:** The assignment applies to exactly one vendor (relevant for the Advice Notification, which originates from purchase documents); the vendor is stored in **Type No.**.
- **All Vendors:** The assignment applies uniformly to all vendors.
- **Vendor Group:** The assignment applies to a vendor posting group; the group is stored in **Type No.**.

**Values of the Sub Type field** (controls the line text; if the field remains blank, a header text is created):

- **(blank):** The assignment is a **header text** and is not evaluated per line.
- **All Items:** The line text applies to all items of the lines.
- **Item:** The line text applies to only one item; the item number is in **Sub Type No.**.
- **Item Category:** The line text applies to all items of an item category; the category is in **Sub Type No.**.
- **All Loading Points:** The line text applies to all loading points (only usable if **Loading Point activated** is set).
- **Loading Point:** The line text applies to only one specific loading point; the loading point number is in **Sub Type No.**. On saving, it is checked whether the loading points are activated; otherwise the message “The Loading Points are not activated or set up.” appears.

> Rule of thumb: **If the sub type is filled, it is a line text.** For pure header texts the sub type must remain **(blank)**.

**Process steps for an assignment:**

1. First you choose the **Template No.** (the **Printing Type** is displayed).
2. Then you set the **Process** to the desired logistics document (Shipment Planning, Advice Notification or Warehouse Shipment).
3. Next you define the business-partner context via **Type**/**Type No.**.
4. Finally you decide on the **Sub Type**: leave it blank for a header text, or set Item/Item Category/Loading Point for a line text.

### 3.4 Setting Up Advice Texts (Process Chain)

**Process intro:** In order for advice notifications to be provided with texts automatically, several pages have to be configured in dependency order. This chain takes effect during daily work on the Advice Notification (section 6.2).

1. **Activate Advice Notification.** Set the **Activated** switch in the **Advice Notification Setup**. When activated, the module forms texts when an advice notification is created/changed; without this switch nothing happens.
2. **Create a text template.** Create the desired template with a suitable **Printing Type** in the **Extended Text Templates** (section 3.2).
3. **Capture the assignment.** Assign the template to the **Advice Notification process** in the **Extended Text Assignment Worksheet**. For header texts set **Type** (e.g. Vendor/All Vendors), **Sub Type** remains **(blank)**. For line texts additionally set the **Sub Type** (Item, Item Category or Loading Point).
4. **Operational completion.** During daily work the user creates the advice notification and adds lines via **Get Source Documents**; the texts then appear automatically (see section 6.2).

### 3.5 Setting Up Shipment Planning Texts (Process Chain)

**Process intro:** Analogous to the Advice Notification, but for the Shipment Planning and the customer context.

1. **Activate Shipment Planning.** Set the **Activate Shipment Planning** switch in the **Shipment Planning Setup**. When activated, texts are formed when a shipment planning is created/changed – both for the **Shipment Planning** process and for the downstream **Warehouse Shipment**.
2. **Create a text template** (section 3.2).
3. **Capture the assignment.** Assign the template to the **Shipment Planning process**. Header texts via **Type** (Customer/All Customers/Customer Group), line texts additionally via **Sub Type**.
4. **Operational completion.** The user creates the shipment planning and retrieves lines via **Get Shipment Planning Lines**; the texts appear automatically (see section 6.1).

### 3.6 Setting Up Loading Point-Related Texts (Process Chain)

**Process intro:** Loading Point-related texts are a standalone capability of this module: they allow line texts that apply only to a specific **Loading Point**. A separate activation is a prerequisite.

1. **Activate loading points.** Set the **Loading Point activated** switch in the **Loading Point Setup**. When activated, the sub types **Loading Point** and **All Loading Points** are available; if it is not set, every Loading Point assignment is rejected with “The Loading Points are not activated or set up.”.
2. **Assignment with sub type Loading Point.** In the **Extended Text Assignment Worksheet**, capture a line assignment with **Sub Type = Loading Point** and the desired loading point number in **Sub Type No.** (or **All Loading Points**).
3. **Operational completion.** As soon as the **Loading Point** is set in an advice notification or shipment planning line, the module re-determines the matching text and applies it to the line texts (see chapter 6). In addition, the assignment can be maintained directly from the Loading Point (see section 4.1).

### 3.7 Permissions

To use the module, assign the users the supplied permission set **MuM ETAS All**. It determines the permissions for the objects of this module (codeunits and preview pages) and thereby defines which users can use the text combination and the preview pages.

---

## 4 Master Data

This module extends only one classic master-data page: the **Loading Point**.

### 4.1 Loading Point – Maintaining Extended Texts

**Process intro:** The **Loading Point** is a logistics master-data card of the base module. This module adds the **Extended Text** action there so that the key user can view and maintain the text assignments matching a loading point directly from the Loading Point. The assignments maintained there later take effect in the advice notification and shipment planning lines with the respective loading point (chapter 6). The **Loading Point activated** switch is a prerequisite (section 3.6).

**Entry point:** Open the desired **Loading Point** and choose the **Extended Text** action.

| Field / Action | Explanation |
|---|---|
| **Extended Text** (action) | When chosen, the action opens the text-assignment worksheet filtered to the current loading point; assignments with **Sub Type = Loading Point** (for this loading point number) as well as **All Loading Points** are shown. This way the user sees exactly the texts that take effect for this loading point and can supplement them. |

This makes the maintenance of Loading Point-related texts possible without the detour via the global search; it complements the setup from section 3.6.

---

## 5 Daily Work

During daily work the module is largely automatic: because of the setup (chapter 3), the texts appear on their own while the documents are processed. The following sections describe on which documents which fields, FactBoxes and actions of this module take effect.

Every logistics document receives two control fields of this module in the **General** area:

| Field | Explanation |
|---|---|
| **Printing Type** | When set, the printing type controls how the texts formed for the document are handled (as FactBox, Report or Mail text); it is passed on to the FactBoxes and the preview so that exactly the matching text variant is displayed there. |
| **Sub-Printing Type** | If the printing type is **Report**, the sub-printing type chooses the print position (Header, Footer, Before Position, After Position); for other printing types the field is disabled and has no effect. |

### 5.1 Shipment Planning

**Controlling setup:** This document is controlled by the **Shipment Planning Setup** (**Activate Shipment Planning** switch) and the assignments of the **Shipment Planning** process stored in the **Extended Text Assignment Worksheet** (see sections 3.1, 3.3, 3.5).

**Entry point:** Open the **Shipment Planning** from the navigation of the logistics module.

Flow:

1. **Create a shipment planning.** When the shipment planning is created, the module automatically forms the header texts – provided **Activate Shipment Planning** is set – and displays them in the **Shipment Planning Text** FactBox.
2. **Retrieve lines.** Use the **Get Shipment Planning Lines** action to take over the sales order lines to be shipped. For each line taken over, the module forms the line texts and shows them in the **Shipment Planning Line Text** FactBox.
3. **Set the Loading Point (optional).** As soon as the loading point is changed in a line, the module re-determines the Loading Point-related texts.
4. **Open the preview (optional).** Use the **Extended Shipment Planning Text** action to open the preview page (see section 5.4) in order to check or regenerate the combined texts per document type.

The two control fields **Printing Type** and **Sub-Printing Type** are available in the header of the Shipment Planning (see table above).

### 5.2 Advice Notification

**Controlling setup:** This document is controlled by the **Advice Notification Setup** (**Activated** switch) and the assignments of the **Advice Notification** process (see sections 3.1, 3.3, 3.4).

**Entry point:** Open the **Advice Notification** from the navigation of the logistics module.

Flow:

1. **Create an advice notification.** When the advice notification is created, the module automatically forms the header texts – provided **Activated** is set – and shows them in the **Advice Text** FactBox.
2. **Get source documents.** Use the **Get Source Documents** action to link, for example, a purchase order to the advice notification. For the lines arising from this, the module forms the line texts and shows them in the **Advice Line Text** FactBox.
3. **Set the Loading Point (optional).** As with the Shipment Planning, the line texts are re-determined when the loading point is changed.
4. **Open the preview (optional).** Use the **Extended Advice Text** action to open the preview page (see section 5.4).

Here, too, **Printing Type** and **Sub-Printing Type** are available in the header.

### 5.3 Shipment Planning Assignment (Sales/Purchase Source)

**Controlling setup:** As with the Shipment Planning; in addition, the text from the origin document (sales or purchase document) is taken into account.

On the assignment page of the Shipment Planning (assignment of open documents), the module adds two FactBoxes for header and line texts as well as the **Extended Text** action.

| Action | Explanation |
|---|---|
| **Extended Text** | When chosen, the action opens the extended texts of the underlying origin document: for a sales source the sales texts, for a purchase source the purchase texts. This way the user can view the source texts from which the shipment planning texts are combined. |

The FactBoxes automatically display the header and line texts matching the selected origin document.

### 5.4 Preview Pages “Extended Advice Text” and “Extended Shipment Planning Text”

**Process intro:** Both preview pages are built the same way. They show the combined texts of a document, grouped by **Document Type**, and allow the targeted regeneration of the texts.

**Entry point:** Use the **Extended Advice Text** action (on the Advice Notification) or **Extended Shipment Planning Text** action (on the Shipment Planning) to open the respective preview page.

| Field / Area | Explanation |
|---|---|
| **Printing Type** | When set, the printing type filters which text variant is displayed in the preview and FactBoxes (FactBox, Report or Mail). |
| **Sub-Printing Type** | Active only for printing type **Report**; determines the print position considered (Header, Footer, Before Position, After Position). |
| **Document Types** (list) | Shows one **Document Type** and its **No.** per line. If the document type matches the source document type, the line is highlighted. This way the user recognizes which text sources feed into the document. |
| **Lines** area (subpage) | Shows, for the selected document type, the line rows with **Item No.** and **Description**, so that the user can trace the text ↔ line assignment. |

**Values of the Document Type field** (which text sources are merged):

- **Advice Notification:** Texts assigned to the advice notification process.
- **Registered Advice Notification:** Texts of the already registered advice notification.
- **Archived Advice Notification:** Texts of an archived advice notification.
- **Shipment Planning:** Texts assigned to the shipment planning process.
- **Registered Shipment Planning:** Texts of the already registered shipment planning.
- **Warehouse Shipment:** Texts formed for the warehouse shipment as the target process of the Shipment Planning.

**Action on the preview page:**

| Action | Explanation |
|---|---|
| **Create Extended Texts for Documents** | When chosen, a selection with two options opens: (1) newly create or update the extended texts **for the current document and the current document type**, or (2) rebuild and refresh **all** texts of the preview document types. This way the user can regenerate the texts in a targeted manner after a changed assignment, without recreating the document. |

---

## 6 E-mail Dispatch and Printing of the Texts

The assigned texts take effect not only on screen, but also during dispatch and printing. How they are handled is controlled by the **Printing Type** of the template:

- **FactBox:** on-screen display only in the mentioned FactBoxes; no printing, no e-mail text.
- **Report:** The text is printed on the report at the chosen position (Header, Footer, Before Position, After Position) according to the **Sub-Printing Type**.
- **Mail:** When an advice notification is sent by e-mail, the assigned text is automatically appended to the e-mail text. For this, the module assembles the matching header and line texts; if both pure FactBox and Mail texts are present, the Mail text is preferred.

In this way the recipient receives exactly the notes that the key user assigned to the respective combination of process, business partner, item or loading point.

---

## 7 History: Registered Documents

When an advice notification or shipment planning is **registered**, the extended texts formed on the working document up to that point are transferred to the registered document and permanently stored there; the working texts of the open document are removed in the process. This way the printed/dispatched text state remains traceably preserved.

### 7.1 Registered Advice Notification

**Entry point:** Open the **Registered Advice Notification**.

- In the header, the fields **Printing Type** and **Sub-Printing Type** are displayed read-only (state at the time of registration).
- The FactBoxes **Advice Text** and **Advice Line Text** show the header and line texts belonging to the registered document.

### 7.2 Registered Shipment Planning

**Entry point:** Open the **Registered Shipment Planning**.

- Analogous to the registered advice notification, **Printing Type** and **Sub-Printing Type** are displayed read-only.
- The FactBoxes **Shipment Planning Text** and **Shipment Planning Line Text** show the registered header and line texts.

This means the texts remain retrievable at the document in an audit-proof manner even after registration.

---

## 8 FAQ and Troubleshooting

### 8.1 Why don't any texts appear in my Shipment Planning?

First check whether the **Activate Shipment Planning** switch is set in the **Shipment Planning Setup**. If it is not set, the module forms no texts. Then check whether an assignment with **Process = Shipment Planning** that matches the customer or the customer group of the document exists in the **Extended Text Assignment Worksheet**.

### 8.2 Why does the “Advice Text” FactBox stay empty?

The Advice Notification must be enabled via the **Advice Notification Setup** with **Activated**, and a matching assignment with **Process = Advice Notification** must exist. Without a matching **Type** (e.g. the vendor of the advice notification or **All Vendors**), the module finds no template.

### 8.3 Why do I get the message “The Loading Points are not activated or set up.” when saving?

You are trying to save an assignment with **Sub Type = Loading Point** or **All Loading Points**, although the **Loading Point activated** switch is not set in the **Loading Point Setup**. Activate the loading points first (section 3.6).

### 8.4 What is the difference between a header text and a line text?

The decisive factor is the **Sub Type** field: if it remains **(blank)**, the assignment is a **header text** and appears in the header FactBoxes (**Advice Text** / **Shipment Planning Text**). If the **Sub Type** is filled (Item, Item Category, Loading Point …), it is a **line text** and appears in the line FactBoxes.

### 8.5 Why can't I select the “Sub-Printing Type”?

The **Sub-Printing Type** is active only for **Printing Type = Report**. For **FactBox** or **Mail** the field is disabled, because the print position is only meaningful for report printing.

### 8.6 What happens to the texts when I change the vendor or the driver contact on the document?

The module detects the change and rebuilds the header texts: when the vendor number of the advice notification or the external contact no. (driver contact) of the shipment planning is changed, the assigned texts are re-determined and replaced.

### 8.7 Why do the line texts change after I change the item number or the loading point in the line?

Line texts depend on the **Sub Type** (Item/Item Category/Loading Point). If you change the item number or the loading point in the line, the module re-determines the matching line texts so that the correct text is always shown for the current line.

### 8.8 Do I have to create a text template before the assignment?

Yes. In the **Extended Text Assignment Worksheet**, the **Template No.** refers to an existing **Extended Text Template**. Via the lookup with **+New** you can create the template directly before assigning it.

### 8.9 Where do I see which texts actually feed into the document?

Use the **Extended Advice Text** or **Extended Shipment Planning Text** action to open the preview page. There the combined texts are grouped by **Document Type**; with **Create Extended Texts for Documents** you can regenerate them after an assignment change.

### 8.10 Are the texts still available after registration?

Yes. During registration the texts are transferred to the **Registered Advice Notification** or **Registered Shipment Planning** and remain retrievable there; the working texts of the open document are removed after the transfer.

---

## 9 Typical Use Cases (Usage Examples)

### 9.1 Standard Note on Every Shipment Planning of a Customer

**Trigger:** A customer requires a fixed loading note on all delivery papers. The request comes in by phone to the key user.

**Entry point in BC:** The key user uses **Search** to open the **Extended Text Templates** and creates a template with **Printing Type = Report** and **Sub-Printing Type = Header**. Then they open the **Extended Text Assignment Worksheet**.

**Core flow:**
1. The key user enters the **Template No.**.
2. They set **Process = Shipment Planning**.
3. They choose **Type = Customer** and enter the customer in **Type No.**; **Sub Type** remains **(blank)** (header text).
4. The operational user later creates a **Shipment Planning** for this customer – the note appears automatically in **Shipment Planning Text**.

**Completion:** On registration the text moves to the **Registered Shipment Planning**; on printing it appears in the header of the report.

### 9.2 Advice Text from a Purchase Order

**Trigger:** A vendor announces a delivery; the goods are to be advised.

**Entry point in BC:** The user opens the **Advice Notification** (prerequisite: **Activated** in the **Advice Notification Setup**, an assignment with **Process = Advice Notification** and **Type = Vendor**/**All Vendors** present).

**Core flow:**
1. The user creates the advice notification – header texts appear in **Advice Text**.
2. Via **Get Source Documents** they link the purchase order to the advice notification.
3. For the lines taken over, the line texts appear in **Advice Line Text**.
4. If needed, they check the result via **Extended Advice Text**.

**Completion:** If the advice notification is sent by e-mail and the template is of **Printing Type Mail**, the module automatically appends the text to the e-mail. On registration, the text state is preserved in the **Registered Advice Notification**.

### 9.3 Text Only for a Specific Loading Point

**Trigger:** A special approach rule applies to a specific loading point (ramp) and is to appear on the lines.

**Entry point in BC:** The key user ensures that the **Loading Point activated** switch is set in the **Loading Point Setup**. They open the relevant **Loading Point** and choose the **Extended Text** action.

**Core flow:**
1. The key user captures an assignment with **Sub Type = Loading Point** and the loading point number in **Sub Type No.** (line text).
2. During daily work the user sets this **Loading Point** in a shipment planning or advice notification line.
3. The module then determines the Loading Point-related text and shows it in **Shipment Planning Line Text** or **Advice Line Text**.

**Completion:** The Loading Point-related line text is printed according to the printing type, sent by e-mail or only displayed, and is transferred along during registration.
