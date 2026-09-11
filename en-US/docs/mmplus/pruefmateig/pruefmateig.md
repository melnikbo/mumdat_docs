---
title: Anwenderhandbuch m+m Test Certificate Management with Material Properties
---

# User Guide m+m Test Certificate Management with Material Properties

## Introduction

The **m+m Test Certificate Management with Material Properties** app connects two existing m+m modules: the rule-based test control from **m+m Test Certificate Management** and the property management from **m+m Material Properties**. It makes it possible to filter in the test control not only by classic document fields, but by the **properties** of the items — depending on the **material type** or across material types.

The central building block is a reusable **property rule filter**: a named set of conditions on material properties. This filter is then stored in a **Test Certificate Rule** as a rule filter. When a document (e.g. a sales, purchase, production, or warehouse line) matches the property values required there, the Test Certificate Rule takes effect — otherwise it has no effect.

**Target audience:** This guide is aimed primarily at **operational quality-assurance users** as well as **clerks in purchasing, sales, and production** whose documents are evaluated by the test control. Secondarily, it addresses **administrators and key users** who set up the number series, maintain the property rule filters, and perform the rule binding in the Test Certificate Rule.

**Short process overview:**

1. The administrator assigns a number series for property rule filters in the **Test Certificate Setup**.
2. The key user creates a filter in the **Property Rule Filter List** and defines a filter value per property in the **Lines**.
3. The key user links the filter in a **Test Certificate Rule** via the **Rule Filter** (field **Field Filter**).
4. In day-to-day operations, the system automatically checks on the affected document lines whether the item's properties match the stored filter, and thereby controls whether the Test Certificate Rule is triggered.

**Dependencies:** The app requires **m+m Test Certificate Management**, **m+m Material Properties**, and **m+m Cloud Base**. The material types and properties themselves are maintained in the **m+m Material Properties** module (**Material Types**, **Property Card**); this guide describes the added value of the linkage, not the basic maintenance of that master data.

## Quick Start for Users

The fastest path from setup to an effective rule. The sequence follows the technical dependency: first the setup, then the master data, and finally the rule binding.

1. **Set up the number series.** Use **Search** to open the **Test Certificate Setup**. On the **Numbering** tab, enter a number series in the **Property Rule Filter Nos** field. Without this entry, no property rule filter can be numbered automatically.
2. **Create a property rule filter.** Use **Search** to open the **Property Rule Filter List** and choose **New**. In the **Property Rule Filter Card**, assign a **Description**, choose the **Type**, and — if the filter should apply only to one material type — the corresponding material type in the **Code** field.
3. **Define filter lines.** In the **Lines** area, enter one line per condition: choose the **Property Code** and store the required value in the **Filter Value** field (supported via AssistEdit).
4. **Bind the filter to a Test Certificate Rule.** Use **Search** to open the **Test Certificate Rule List**, open the desired **Test Certificate Rule**, and enter a line in the **Rule Filter** whose **Table ID** points to the property rule filter header; in the **Field Filter** field, choose the **No.** of the property rule filter you created.

From now on the system evaluates the affected documents automatically. A separate posting or release step is not required in this app.

## Setup

The setup of this app is deliberately lean: you need exactly **one** number series, the appropriate **permissions**, and then the maintenance of the property rule filters (see the **Master Data** section). All further control is handled via the individual filters and their binding in the Test Certificate Rule.

### Test Certificate Setup — Numbering tab

**Process intro.** This setup is performed once by the **administrator** **before first use**. The **Test Certificate Setup** is a company-wide setup card (one record per company). The field added by this app is located on the existing **Numbering** tab, together with the other number series of the test control. Users later reference the number series assigned here whenever they create a property rule filter (cross-link: **Master Data** section).

**Getting there:** Use **Search** to open the **Test Certificate Setup** and switch to the **Numbering** tab.

On this tab, the BC user sees all number series of the test control on a single page. The following table documents the entire **Numbering** tab (base fields of the core module and the field added by this app):

| Setup | Explanation |
|---|---|
| **Test Certificate Template Nos.** | If a number series is set here, then newly created test templates automatically receive a consecutive number from this series; without an entry, the number must be assigned manually. |
| **Test Certificate Nos.** | If set, then newly generated tests are automatically numbered from this series — a prerequisite for the test control to be able to create tests without manual number assignment. |
| **Test Certificate Sample Nos.** | If set, then samples for a test automatically receive a unique number from this series; this ensures the traceability of individual samples. |
| **Test Certificate Rule Nos.** | If set, then new Test Certificate Rules are automatically numbered from this series; the rules thereby remain uniquely referenceable. |
| **Property Rule Filter Nos** | If a number series is stored here, then the system automatically assigns the next number from this series when a new property rule filter is created. If the field is empty, then the system refuses the creation and requires a manual number or a valid series — so the maintenance of property rule filters (**Master Data** section) is only possible after this entry. |

> Note on scope: The **Test Certificate Setup** contains further tabs that belong to the core module **m+m Test Certificate Management** and are documented there. For this app, only the **Property Rule Filter Nos** field on the **Numbering** tab is relevant; it is explained here in full within the context of the tab.

### Permissions

**Process intro.** Before users may create or edit property rule filters, the administrator assigns the appropriate permission. The app ships an assignable permission set for this purpose.

The permission set **MuM TCMP All** defines which actions users may perform on this app's objects: it covers full read and edit access (create, modify, delete) to the property rule filter header and the property rule filter lines, as well as the execution rights for the associated pages and the rule evaluation. If you assign this set to a user, then that user can maintain property rule filters and use the app functions; without this assignment, the pages and the rule-based evaluation remain blocked for the user.

### Setting up property rule filters

**Process intro.** This is the end-to-end enablement of the single functional capability of this app. It spans several pages and is therefore described here as one coherent flow. Configuration is done by the **administrator** (number series, permission) and the **key user** (filter maintenance, rule binding), once before productive use and thereafter as needed. The setting is then used in day-to-day operations through the automatic evaluation of the document lines (cross-link: **Rule Binding in the Test Certificate Rule** section).

**Enablement steps in dependency order:**

1. **Store the number series.** Enter the **Property Rule Filter Nos** field in the **Test Certificate Setup** on the **Numbering** tab. If this step is missing, then no filter can be created in step 3.
2. **Assign the permission.** Assign the **MuM TCMP All** permission set. If the permission is missing, then the following pages are not editable for the user.
3. **Create the property rule filter and maintain lines.** Create the filter in the **Property Rule Filter List** and define the property conditions in the **Lines** (details in the **Master Data** section). If at least one line carries a **Filter Value**, then the filter can be evaluated.
4. **Bind the filter in the Test Certificate Rule.** Link the filter in the **Rule Filter** of a **Test Certificate Rule** (field **Field Filter**). Only with this binding does the filter take effect in day-to-day operations.

**Operational closing action:** No separate posting or release action is required. As soon as the binding in step 4 is saved, the test control evaluates the affected document lines automatically (cross-link: **Rule Binding in the Test Certificate Rule** section).

## Master Data

The only master data category of this app is the **property rule filter**. It consists of a header (property rule filter header) and any number of lines (property rule filter line).

### Property Rule Filter — List and Card

**Process intro.** This master data is maintained by the **key user** after the basic setup, on an ongoing basis whenever quality assurance has new requirements. A filter bundles the property conditions that are later meant to trigger a Test Certificate Rule. In day-to-day operations the values do not appear on the document, but act in the background via the rule binding (cross-link: **Rule Binding in the Test Certificate Rule** section).

**Getting there:** Use **Search** to open the **Property Rule Filter List**. Use **New** to create a new record; an existing entry opens on double-click in the **Property Rule Filter Card**. The list itself is not editable and serves as an overview; maintenance is done on the card.

The **Property Rule Filter List** shows the header data of one filter per line. It contains no separate filter fields in the query row; the overview is narrowed down using the standard search and sorting of Business Central.

**Header fields (list and General tab of the card):**

| Field | Explanation |
|---|---|
| **No.** | Unique number of the property rule filter. If the field is left empty on creation, then the system automatically draws the next number from the series stored in **Property Rule Filter Nos**; this No. is the value you later reference in the **Field Filter** of the Test Certificate Rule. |
| **Type** | Determines what the filter conditions refer to. Permitted values: <br>**Property:** The filter evaluates material properties of the item. If this type is chosen, then the property values stored in the **Lines** are checked against the properties of the item on the document line. (The type is extensible; in this app only the value **Property** is available.) |
| **Code** | Optionally restricts the filter to one **Material Type** (selection from the material types). If a material type is set here, then the filter applies only to items of this material type and the properties that can be entered are limited to those assigned to this material type; if the field is left empty, then the filter applies across material types to all items to which the respective property is assigned. |
| **Description** | Free text to name the filter. If a descriptive text is maintained, then key users find the right filter more quickly during rule binding; the value has no controlling effect. |

> On the **Code** field: The system only checks the assignment in terms of content when you enter a line (see below). An empty **No.** prevents the code from being saved, because the filter header first needs a valid number.

### Lines of the property rule filter

**Process intro.** In the **Lines**, the key user stores the actual conditions — one property per line with the required filter value. All lines of a filter act together: an item satisfies the filter only if it satisfies **every** line (AND logic).

The **Lines** area is shown directly on the **Property Rule Filter Card** below the header data.

| Field | Explanation |
|---|---|
| **Property Code** | Selects the property to be checked (selection from the properties of the m+m Material Properties module). If a code is chosen, then the system immediately checks whether this property is assigned at all: if a **Material Type** (field **Code**) is set on the header, the property must be assigned to this material type; if no material type is set, the property must be assigned to at least one material type. Otherwise the system reports "The property … is not assigned." and refuses the line. |
| **Property Name** | Shows the name of the selected property (looked up automatically). If you change the Property Code, then the name updates accordingly; the field is not editable and serves readability. |
| **Filter Value** | The required value of the property against which the item is checked. If a filter value is set, then the relevant property of the item must satisfy this value (or value range) for the filter to match. The AssistEdit function opens a selection aid: if the property uses fixed **Property Values**, then you choose from these values; otherwise you assemble a filter expression. The field must not be left empty — empty lines are not considered during evaluation, and when leaving the lines the system enforces a value. If you change the **Property Code** of a line, then the previous **Filter Value** is reset. |

**Validation and dependencies:** When leaving the lines, the system checks that every line carries a **Filter Value**. A **Filter Value** without a **Property Code** is not possible; the system requires the property first. If the filter header is deleted, then all associated lines are automatically deleted with it.

## Rule Binding in the Test Certificate Rule

This section describes **how** the configured property rule filter takes effect in day-to-day operations. The effect is not created on a dedicated page of this app, but via the **Test Certificate Rule** of the core module, which is extended by this app to include the evaluation of material properties.

**Controlling pages:** The evaluation is prepared by the **property rule filters** (master data of this app, **Master Data** section) and by the **Test Certificate Setup** (number series, **Setup** section), and is activated in the **Test Certificate Rule** via the **Rule Filter**. The administrator/key user configures the binding there; the operational evaluation then runs without user intervention.

### Storing a filter in a Test Certificate Rule

**Getting there:** Use **Search** to open the **Test Certificate Rule List**, open the desired **Test Certificate Rule**, and switch to the **Rule Filter** area.

Enter a line in the **Rule Filter** and set the property rule filter header's table in the **Table ID** field. The **Related Table ID** field then shows the linked table. In the **Field Filter** field, store the **No.** of the property rule filter you created earlier. When this binding is saved, then the Test Certificate Rule includes the property conditions of the filter in its evaluation.

| Field (Rule Filter) | Explanation |
|---|---|
| **Table ID** | Determines what the filter line refers to. If you choose the property rule filter header here, then you activate this app's property-based evaluation for this rule. |
| **Related Table ID** | Shows the related table belonging to the Table ID. If it points to the property rule filter header, then the evaluation recognizes that a property rule filter is to be applied (the field is not editable). |
| **Field Filter** | Holds the **No.** of the property rule filter to be applied. If a filter number is entered here, then for each affected document the system checks exactly the property conditions defined in this filter. |

### Which documents are evaluated

The app hooks into the evaluation of the Test Certificate Rule and assesses the item of the respective document line. On installation, the app automatically registers the following document types as evaluable sources; for the user this means that the property-based rule can take effect on these lines:

- Sales lines and purchase lines (in each case only for lines of type Item),
- Production order lines, production order components, and production order routing lines,
- Pick lines (warehouse activity lines),
- Warehouse receipt lines and warehouse shipment lines,
- Transfer lines.

For each of these lines, the system determines the **Material Type** of the item and compares the item's properties with the lines of the property rule filter.

### How the evaluation decides

The decision follows a clear logic that the user should know in order to build filters correctly:

1. The system reads all lines of the property rule filter referenced in the **Field Filter** that carry a **Filter Value**.
2. If a **Material Type** (field **Code**) is set on the filter header, then the filter takes effect only if the item on the document line belongs to exactly this material type; if no material type is set, then the filter applies regardless of the material type.
3. For each filter line, the system checks whether the corresponding property of the item satisfies the required **Filter Value**.
4. Only if **all** filter lines are satisfied does the filter count as matching and the Test Certificate Rule is triggered; if even a single line fails, then the rule has no effect for this document.

## Typical Use Cases

The following scenarios show the app in use along realistic triggers. All steps refer to the pages and flows described in this guide and stored in the code.

### Use case 1: New test specification for a material type

**Trigger:** Quality assurance reports internally that items of a certain material type should in future only receive a test if a certain material property has a defined value.

**Getting started in BC:** The key user uses **Search** to open the **Property Rule Filter List** and creates a filter via **New**.

**Core flow:** In the **Property Rule Filter Card**, the key user assigns a **Description**, leaves the **Type** at **Property**, and chooses the relevant material type in the **Code** field. In the **Lines** area, they enter a line with the appropriate **Property Code** and record the required value in the **Filter Value** (via AssistEdit). Then they use **Search** to open the **Test Certificate Rule List**, choose the responsible **Test Certificate Rule**, and store a line in the **Rule Filter** with the **Table ID** of the property rule filter header and the **No.** of the new filter in the **Field Filter**.

**Conclusion:** No posting step is required. From now on, the Test Certificate Rule triggers for items of this material type only when the required property satisfies the filter value.

### Use case 2: Test only for a matching property in purchasing

**Trigger:** On the warehouse receipt for a purchase order, a test should be initiated for an item only if a safety-relevant property has a certain value.

**Getting started in BC:** The key user uses an existing or new property rule filter (**Master Data** section) and binds it to the responsible **Test Certificate Rule** as in use case 1.

**Core flow:** The purchasing clerk records the purchase order as usual with a purchase line of type Item. On the warehouse receipt, the test control evaluates the warehouse receipt line or the underlying purchase line: the system determines the **Material Type** of the item and compares its properties with the bound property rule filter. If the item satisfies the filter, the Test Certificate Rule takes effect; otherwise the warehouse receipt proceeds without an additional test.

**Conclusion:** The clerk posts the warehouse receipt with the standard BC process. The property-based control happens automatically in the background; a dedicated operating step for the app is not needed.

### Use case 3: Maintaining the filter value conveniently via the selection aid

**Trigger:** A key user wants to refine an existing property rule filter and is unsure about the correct value of a property.

**Getting started in BC:** Using **Search**, the key user opens the **Property Rule Filter List** and, within it, the relevant filter.

**Core flow:** In the **Lines** area, they select the line of the desired property and call the AssistEdit function in the **Filter Value** field. If the property uses fixed **Property Values**, then they choose the value from the offered list; otherwise they assemble a filter expression via the selection aid. The system adopts the result as the **Filter Value**.

**Conclusion:** When leaving the lines, the system checks that every line carries a **Filter Value**. The adjusted filter takes effect without any further step in all Test Certificate Rules in which its **No.** is stored.

## FAQ and Troubleshooting

### Why can I not create a new property rule filter?

Because the **Property Rule Filter Nos** field on the **Numbering** tab in the **Test Certificate Setup** is empty. On creation, the system needs either a valid number series or a manually entered number. Enter the number series, then new filters can be numbered automatically.

### Why does the message "The property … is not assigned." appear?

Because the **Property Code** chosen in the line is not assigned for the selected constellation. If a **Material Type** is set on the header in the **Code** field, the property must be assigned to this material type; if no material type is set, the property must be assigned to at least one material type. Assign the property in m+m Material Properties or choose a matching property.

### Why can the card not be opened via the search?

The **Property Rule Filter Card** is deliberately not directly reachable via **Search**. Instead, open the **Property Rule Filter List** via **Search** and, within it, the desired record; the card opens from the list.

### Why can I not change any values in the Property Rule Filter List?

Because the list is not editable and serves only as an overview. You make all changes in the **Property Rule Filter Card**, which you open from the list by double-click.

### Why is my Test Certificate Rule not triggered even though the item matches?

Check three points: First, the **No.** of the filter must be entered correctly in the **Field Filter** in the **Rule Filter** of the **Test Certificate Rule**. Second, the **Material Type** on the filter header (field **Code**) must match the item — or be empty. Third, **all** filter lines must be satisfied; if one line fails, the rule does not take effect.

### Why is it not enough for only one of several filter lines to match?

Because the lines of a property rule filter are linked with "AND". The item must satisfy every line. If you want "OR" logic, then distribute the conditions across several filters and bind them to separate Test Certificate Rules.

### Why is my filter value cleared when I change the property?

Because the **Filter Value** always belongs to a specific **Property Code**. If you change the property code of a line, then the system resets the previous filter value so that no value matching the old property is left in place by accident. Enter the filter value again afterward.

### Why can I not leave the lines?

Because at least one line contains no **Filter Value**. When leaving the lines, the system enforces that every recorded line carries a filter value. Add the value or delete the empty line.

### Why does the filter act across material types even though I did not want that?

Because the **Code** field (material type) on the filter header was left empty. Without a material type, the filter applies to all items to which the respective property is assigned. Enter the desired **Material Type** in the **Code** field, then the filter is restricted to that type.

### On which documents does the property-based evaluation take effect at all?

On the document types registered at installation: sales and purchase lines (type Item), production order lines, production order components and routing lines, pick lines, warehouse receipt and warehouse shipment lines, as well as transfer lines. On other documents the property rule filter is not evaluated.
