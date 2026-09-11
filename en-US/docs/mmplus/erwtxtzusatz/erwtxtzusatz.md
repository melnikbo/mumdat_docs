---
title: Anwenderhandbuch m+m Ext. Text Module with Ext. Production Information
---

# User Guide m+m Ext. Text Module with Ext. Production Information

## Introduction

The **m+m Ext. Text Module with Ext. Production Information** app is a connector app: it links the material-type-based text assignment of the **Extended Text Module** to the **operations (routing lines) of production orders**. The goal is that an **Extended Text** assigned via a **Material Type** appears not only on sales and production order lines, but additionally on the **operation lines of the production order**, and from there is printed on or carried over to documents, FactBoxes, and emails.

The app itself does **not** provide any **pages, lists, or actions of its own**. It exclusively supplements the processing logic in the background. All screens the user works with come from the required m+m apps:

- **m+m Ext. Text Module** — text templates, assignment (subtype), document texts, operation texts, print and mail control.
- **m+m Material Properties** — material types and their assignment to the item.
- **m+m Ext. Text Module with Material Properties** — connects material type and Extended Text (subtype **Material Type** / **All Material Types**).
- **m+m Ext. Production Information** — extended production information on operations.

Without these base apps the function cannot be used; they are installed as dependencies.

**Target audience.** This guide is primarily aimed at **operational users in production and sales** who process production orders and their operations and who create documents and emails and there view and check the extended text. Secondarily it addresses **administrators and master data managers** who maintain the material types, configure the Extended Text settings, and set up text assignment by material type.

**Short process overview.** The administrator maintains the **Material Types** and assigns them to the **item**. In the **Extended Text Setup** they define which fields of the material property are used in formulas. Next they create a **Text Template** and assign it via the **subtype Material Type** or **All Material Types**. As soon as a production order contains operations for an item of this material type, this app links the matching **Extended Text** to the respective **operation line** and makes it available for **Report**, **FactBox**, and **Mail**.

**Typical user path.** Maintain the material type (**Material Types** → **Material Type Card**) → store the material type on the **item** → assign the text template via **Subtype = Material Type / All Material Types** → open the production order and operation → check the **Extended Text** on the operation → print the document or send it as an email.

## Quick Start for Users

The quick start describes the shortest path to the result "material-type-based Extended Text on an operation line of the production order". The order follows the dependency in the code: first setup and master data, then the daily work on the production order.

1. **Create a material type.** Open **Material Types** and create a material type via **+ New**; in the **Material Type Card**, enter the properties and turn off the **Blocked** toggle so that the material type can be used on lines.
2. **Store the material type on the item.** Assign the material type to the relevant **item** (via the material list of the item in the **m+m Material Properties** app).
3. **Check the Extended Text Setup.** Open **Extended Text Setup** and, on the **Material Text** tab, use the **Material Property Setup** action to define which fields of the material property are used in the Extended Text.
4. **Assign the text template via the material type.** Create a **Text Template**, enter the text (with an optional formula), and assign it via the **subtype Material Type** (for a specific material type) or **All Material Types** (for any material type) with **Process Object Type = Page** to the desired production document.
5. **Open the production order.** Open the production order that has operations for an item of the assigned material type.
6. **Check the Extended Text on the operation.** Use the **Extended Text** action to open the text for the relevant **operation line** (**Operation No.**) and check the content and display for **Report**, **FactBox**, and **Mail**.
7. **Output the document.** Print the production document or send it as an email; the assigned text appears on the respective operation line.

> This app does not provide a page of its own. All screens mentioned belong to the connected m+m apps (see **Setup** and **Master Data**).

## Setup

The app itself has **no setup page**. However, for the material-type-based text assignment on operations to take effect, the setups of the connected modules must be in place. This section describes the structure in dependency order. All pages come from the base apps; the designations are taken from their translations.

### Setting up Extended Text Setup

**Who and when.** The administrator sets up the **Extended Text Setup** once before first use. These settings control how formula expressions in the Extended Text are recognized and which fields of the material property can be used as placeholders. The user consumes the result later when entering text templates (see **Assign the text template via the material type**).

**Entry point:** Open the **Extended Text Setup** page (base app m+m Ext. Text Module) and switch to the **Material Text** tab.

Fields on the **Material Text** tab:

| Setup | Explanation |
|-------------|-------------|
| Formula Start/End | If you set a character here (default `^`), the Extended Text recognizes the start and end of a formula expression from this character on; this lets you formulate conditional material texts in text templates that are evaluated when the document text is assembled. |
| Sub-Formula Start | If you set this character (default `{`), it marks the start of the text block that is output when the condition is met; without the character the conditional text block is not delimited. |
| Sub-Formula End | If you set this character (default `}`), it marks the end of the conditional text block; this tells processing how far the text extends when the condition is met. |
| Update Ext. Text automatically | If enabled, the Extended Text is automatically reassembled as soon as the value of the material property changes; without the toggle, a text that has already been generated remains unchanged until it is rebuilt manually. |

**Process step.** In the **Extended Text Setup**, start the **Material Property Setup** action. There you define which field values of the material property are used in the Extended Text.

Fields in the **Material Property Setup**:

| Setup | Explanation |
|-------------|-------------|
| Table ID | If you specify the material property table here, this defines which table the field values for the Extended Text are read from; only then are its fields available for placeholders. |
| Field No. | If you select a field number from the specified Table ID, exactly this field value becomes available as a possible placeholder in the Extended Text. |
| Field Name | Shows the name for the selected Field No.; it serves to uniquely map the placeholder in the text template. |
| Start Characteristic | If you set this start character (length 1), processing recognizes the start of the field value to be inserted in the text from this character on. |
| End Characteristic | If you set this end character (length 1), processing recognizes the end of the field value to be inserted; only with a start and end characteristic is the placeholder correctly replaced by the material property value. |

**Conclusion / relation to daily work.** After this setup, text templates can contain formulas and material property values that are evaluated when the document text is assembled on the production order and its operations (see **Daily Work on the Production Order**).

### Setting up material-type-based operation text

This is the central setup that makes exactly this connector app effective. It connects three levels: **Material Type (master data)** → **Text Template with subtype Material Type / All Material Types** → **Effect on the operation line of the production order**.

**Who and when.** The administrator or key user sets up the assignment once, before production orders with material-type-based texts are printed. The operational user consumes the result in the **daily work on the production order**.

**Numbered setup steps (in dependency order):**

1. **Create the material type as master data.** Open **Material Types** and create the required material type. If the material type is not **Blocked**, it can be used on document lines and in the text assignment; as long as it is blocked, the assignment does not take effect (see **Master Data – Material Types**).
2. **Assign the material type to the item.** Store the material type on the **item**. If an item carries a material type, processing can determine the matching material type for the production order via the production order line and link the associated text to the operation.
3. **Create and assign the text template.** Create a **Text Template** with the desired text or formula expression. Set the **Subtype** to **Material Type** if the text should apply only to a specific material type, or to **All Material Types** if it should apply to any material type. Select **Page** as the **Process Object Type** and the production document page for which the text should apply as the **Process Object ID**. This controls on which production document the text appears at the operation.
4. **Check the material property field values.** Make sure that the placeholders used in the text template are stored in the **Material Property Setup** (see above); without this mapping, placeholders in the text remain unresolved.

**Operational conclusion.** As soon as a production order contains operations for an item of the configured material type, the app automatically links the matching Extended Text to the **operation line** (**Operation No.**). The user checks and prints it in the **daily work on the production order**.

**Subtype – meaning of the relevant values** (enum **Subtype**, decisive for this app):

- **Material Type:** The text takes effect only if the material type of the item on the operation line matches the material type stored in the assignment. This lets you control material-type-specific notes (e.g. processing or safety notes per material).
- **All Material Types:** The text takes effect for every material type, provided a material property exists at all on the item of the operation line. This lets you distribute a universally applicable material text across all materials.

> Other subtype values of the Extended Text Module (e.g. **Work Center Group**) belong to the base module and are not changed by this connector app; for material-type-based operation processing, only **Material Type** and **All Material Types** are relevant.

## Master Data

### Material Types

**Who and when.** The master data manager maintains the **Material Types** before material-type-based texts are assigned and output on production orders. The maintained values later appear as a selection in the text assignment (**subtype Material Type**) and determine which text is linked to which operation line.

**Entry point:** Open the **Material Types** list; create a material type via **+ New**, and open the **Material Type Card** via **Manage → Edit**.

In the **Material Types** overview you see all available material types as well as the number of items that use a material type. Via the FlowField of the item count, you open a filtered **item list** for the respective material type.

Key fields of the material type:

| Field | Explanation |
|------|-------------|
| Material Type (code/description) | If you enter the code and the description here, the material type is available as master data for assignment to items and for text assignment; without a code, the material type cannot be referenced. |
| Blocked | If enabled, the material type is blocked and cannot be used on document lines or assigned; turn off the toggle so that the material type takes effect on the item and in the text assignment. |

**Relation to daily work.** Only an unblocked material type assigned to the item causes this app to determine the matching Extended Text on the operation lines of the production order (see **Daily Work on the Production Order**).

> The full range of fields and actions of the **Material Type Card** (e.g. templates for item descriptions, copy templates) belongs to the **m+m Material Properties** app and is documented there. For the present connector app, the existence of an unblocked material type and its assignment to the item are the only master-data prerequisite.

## Daily Work on the Production Order

This section describes what the operational user sees and does in the production order once the setup is in place. The connector app works in the background here: when assembling the document text for an **operation line** of a production order, it checks the existing text assignments with **subtype Material Type** or **All Material Types** and marks the matching text templates.

**Prerequisites (reference to setup).** The effect requires an unblocked material type assigned to the item (see **Master Data – Material Types**) as well as a text assignment with **subtype Material Type / All Material Types** and **Process Object Type = Page** (see **Setting up material-type-based operation text**).

**Core flow:**

1. **Open the production order.** Open the production order whose operations concern items with a configured material type.
2. **Select the operation line.** Select the relevant **operation line** (**Operation No.**). The app maps the text assignment to the correct operation based on the operation (determined via the production order line belonging to the operation and its material type).
3. **Open the Extended Text.** Use the **Extended Text** action to open the assembled text for the operation line. The text contains the content assigned via the material type; contained placeholders were replaced based on the item's material property values.
4. **Check the display types.** Check the text separately by purpose:
   - **Report:** The text is printed on the document (with optional sub-areas such as header, footer, before/after position).
   - **FactBox:** The text is shown in the FactBox for the line.
   - **Mail:** The text is carried over into an email.

**Order and priority logic.** If the text on the operation line has already been **changed manually**, this changed text takes precedence and is not overwritten by the material-type-based assignment. Otherwise, the app assembles the text from the applicable templates. This way, individual adjustments on the specific production order are preserved.

## Documents and Email

The operation text assigned via the material type is not only visible on screen but also flows into the **document output** and **mail dispatch** of the Extended Text Module.

- **Report (print).** When the production document is printed, the assembled text of the operation line is output. Via the subtypes of the report text (header, footer, before position, after position) you control where on the document the text appears.
- **FactBox.** In the FactBox for the operation line, the text is displayed for visual inspection, without needing to print.
- **Mail.** The text is carried over into the email output, so that material-type-based notes are also carried along with electronic dispatch.

Which document type is affected is determined by the **Process Object ID** (the production document page) of the text assignment. This lets you specifically control on which production document the material-type-based operation text appears.

## Typical Use Cases

The following scenarios show realistic triggers and the chronological flow in Business Central. Each step is secured via the connected modules; the connector app ensures that the material-type-based text lands on the operations of the production order.

### Scenario 1: Material-specific processing note on the production document

1. **Trigger.** Production reports that an additional processing note should appear on every operation line for a specific material.
2. **Entry in BC.** The administrator opens **Material Types**, ensures that the relevant material type exists and is not **Blocked**, and checks that the relevant items carry this material type.
3. **Core flow.** They create a **Text Template** with the note text and assign it via the **subtype Material Type** (for exactly this material), **Process Object Type = Page**, and the matching **Process Object ID** of the production document page. The production user then opens a production order with operations for an item of this material type, selects the **operation line** (**Operation No.**), and checks the display for **Report** via **Extended Text**.
4. **Conclusion.** The production document is printed; the material-specific note appears on the respective operation line.

### Scenario 2: General material note by email to production

1. **Trigger.** A generally applicable material note should be sent along, independent of the specific material, with every material-related operation.
2. **Entry in BC.** The key user opens the **Extended Text Setup** and checks the formula characters and the **Material Property Setup** on the **Material Text** tab.
3. **Core flow.** They create a **Text Template** with the general note and assign it via the **subtype All Material Types**. When building the document text for a production order, the connector app marks this template for every operation whose item has a material property. The user checks the display for **Mail** at the **operation line** via **Extended Text**.
4. **Conclusion.** The production document is sent as an email; the general material note is included at the operation.

## FAQ and Troubleshooting

### 1. Why does this app not come with a page of its own?
The app is a pure connector app. In the background, it supplements the processing of the Extended Text Module so that material-type-based texts also take effect on the operation lines of production orders. All user interfaces come from the connected m+m apps.

### 2. Which apps must be installed for the function to work?
The prerequisites are **m+m Ext. Text Module**, **m+m Material Properties**, **m+m Ext. Text Module with Material Properties**, **m+m Ext. Production Information**, and **m+m Cloud Base**. Without this base, neither material types nor text assignment nor the operation texts are available.

### 3. Why does no material-type-based text appear on the operation line?
Check in this order: Is the **material type** unblocked and assigned to the item? Does a text assignment with **subtype Material Type / All Material Types** exist? Is the **Process Object Type = Page** and the **Process Object ID** the correct production document page? If one of these prerequisites is missing, processing finds no matching template and ends without text.

### 4. What is the difference between the subtypes Material Type and All Material Types?
**Material Type** takes effect only if the material type of the item on the operation line matches the material type stored in the assignment. **All Material Types** takes effect for every material type, provided a material property exists at all on the item.

### 5. Why is my manually changed operation text not overwritten by the assignment?
A text already changed manually on the operation line takes precedence. Processing detects the manual change and keeps the changed text instead of replacing it with the material-type-based template. This way, individual adjustments are preserved.

### 6. How does the app map the text to the correct operation?
For the **operation line** (via **Operation No.** and routing), the app determines the associated production order line and its material type and compares it with the text assignment. Only on a match is the template marked and the text carried over.

### 7. Why do placeholders in the text remain unresolved?
Placeholders are only replaced if the fields used are stored in the **Material Property Setup** and the formula characters are set correctly in the **Extended Text Setup**. If the field mapping or the start/end characteristic is missing, the placeholder remains in place.

### 8. On which documents does the material-type-based operation text appear?
On the production document page you have specified via the **Process Object ID** of the text assignment. Via the display types **Report**, **FactBox**, and **Mail** you additionally control where the text becomes visible.

### 9. Does the app also affect sales and production order lines?
The material-type-based assignment on **sales lines** and **production order lines** is already handled by the **m+m Ext. Text Module with Material Properties** module. This connector app specifically supplements the **operation lines (operations)** of the production order.

### 10. Do I have to rebuild the Extended Text after changing the material property?
Only if the **Update Ext. Text automatically** toggle is not enabled in the **Extended Text Setup**. If it is enabled, the text is automatically reassembled when a material property value changes.
