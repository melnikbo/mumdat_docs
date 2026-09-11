---
title: Anwenderhandbuch m+m Test Certificate Management with Aided Data Management
---

# User Guide m+m Test Certificate Management with Aided Data Management

## Introduction

The **m+m Test Certificate Management with Aided Data Management** module connects two existing m+m apps in Microsoft Dynamics 365 Business Central: the **aided data management** (rules and rule flows) and the **test certificate management** (test certificates and test certificate templates). The goal is that **test certificates** and **test certificate templates** are no longer entered manually, but are created automatically based on stored **rules** and pre-populated with values as soon as a triggering event occurs in day-to-day operations.

**Target audience:** Primarily these are **operational users** in quality assurance and goods receipt who create test certificates in day-to-day work (for example when posting a goods receipt) and whose test certificates and test certificate templates are prepared automatically by the module. Secondarily, the guide is aimed at **administrators and key users** who configure the rule flows in the **Rule Setup**, in the **Rules**, and on the **Material Type Card**.

**Short process overview:** In the **Rules**, the administrator creates individual test rules (e.g. "Use Test Cert. Template", "Set Test Cert. Line Field"). These rules are assembled per **material type** into a **Rule Flow** — separated into a **Test Certificate Template Rule Flow** and a **Test Certificate Rule Flow**. As soon as an item of this material type is unblocked, or a test certificate is created, the system automatically runs the appropriate rule flow and creates or fills the associated test certificate template or test certificate.

All navigation paths mentioned in this guide take place in "Microsoft Dynamics 365 Business Central". Where a page is reachable via the **Search**, this is indicated; pages without their own search category are opened exclusively via the parent list or action named.

## Quick Start for Users

The quick start describes the shortest path from setup to the automatically created test result. The order follows the technical dependency (first setup, then master data, then execution).

1. **Define number assignment (one-time):** Open the **Rule Setup** page via the **Search** and, on the "General" tab, set the **Test Cert. Nos From** field to **No. Series** or **Item No.** (see chapter *Setup*). This field controls how automatically created test certificate templates receive their number.
2. **Create rules:** Open the **Rules** page via the **Search** and create the required test rules. For each rule, choose the appropriate **Rule Type** (e.g. **Use Test Cert. Template**, **Use Test Cert. Line**, **Set Test Cert. Line Field**) and fill in the fields that are then displayed (see chapter *Rules and Rule Types*).
3. **Attach the rule flow to the material type:** Open the **Material Types** list via the **Search**, open the relevant line (**Material Type Card**) and choose the action **Test Certificate Template Rule Flow** or **Test Certificate Rule Flow**. In the opened **Rule Flow**, assemble the **Line Type** and the **Rule Code** for each line (see chapter *Material Types and Rule Flows*).
4. **Triggering in day-to-day operations:** The flow is then executed **automatically**:
   - The **Test Certificate Template Rule Flow** starts when an **item** of this material type is **unblocked**.
   - The **Test Certificate Rule Flow** starts when a **test certificate** is created (e.g. at goods receipt).
5. **Check the result:** Open the **Test Certificate Templates** via the **Search**, or open the created **test certificate** via the test status, and check the automatically filled values.

> Note: This module contains **no** manual posting or release step. The "execution" is the **automatic** processing of the rule flow by the system (see chapter *Automatic Execution of the Rule Flow*). The user triggers it indirectly by unblocking an item or creating a test certificate.

## Setup

The setup of this module is deliberately lean: the module extends the existing **Rule Setup** of the aided data management by exactly one controlling field. All other basic settings (rules, rule flows) are functional master data and are described in the following chapters.

### Rule Setup

**Entry point:** Open the **Rule Setup** page via the **Search** in Business Central. This page is a company-wide setup record (one record per tenant) and can be found via the "Administration" search category.

**Process:** This page is maintained once by the **administrator** **before first use**. It defines how the aided data management assigns numbers for automatically created objects. The **Test Cert. Nos From** field added by this module is evaluated later in the **Test Certificate Template Rule Flow**, when the system creates a new test certificate template (see *Setting up the Test Certificate Template Rule Flow*).

The page shows the user **one** merged form combining base fields of the aided data management and the field of this module. All visible fields of the "General" tab:

| Rule Setup field | Explanation |
|---|---|
| **Routing Nos. From** | If **No. Series** is selected, a routing created by a rule flow receives its number from the stored number series; if **Item No.** is selected, the item number is used instead as the routing number. Controls the traceability of created routings (base field of the aided data management). |
| **Prod. BOM Nos. From** | If **No. Series** is selected, a created production BOM receives its number from the number series; if **Item No.** is selected, the item number is used. Determines the number assignment of created production BOMs (base field of the aided data management). |
| **Test Cert. Nos From** | Controls the number assignment of automatically created **test certificate templates** in the Test Certificate Template Rule Flow. **No. Series:** If set, when an item is unblocked the system creates a **new** test certificate template with a sequential number from the number series. **Item No.:** If set, the system uses the **item number** as the test certificate template number; if a test certificate template with this item number already exists, it is **overwritten** instead of creating an additional one. |

**Option values of "Test Cert. Nos From" (each value and its effect):**
- **No. Series:** Every item unblocking creates a separate, sequentially numbered test certificate template; earlier test certificate templates remain unchanged.
- **Item No.:** At most **one** test certificate template is created per item (number = item number). Unblocking the item again **overwrites** this item's existing test certificate template with the current rule flow result.

#### Setting up the Test Cert. Nos From

**Process:** This setup is performed once by the **administrator** before first use. It is a prerequisite for the **Test Certificate Template Rule Flow** (chapter *Material Types and Rule Flows*) to be able to number the created test certificate template correctly.

1. Open the **Rule Setup** page via the **Search**.
2. Set the **Test Cert. Nos From** field. If you choose **No. Series**, new, sequentially numbered test certificate templates are created on each unblocking; if you choose **Item No.**, one test certificate template is maintained per item and overwritten on the next unblocking.
3. **Operational completion:** The setting takes effect automatically as soon as an item of the affected material type is unblocked and the Test Certificate Template Rule Flow runs (see *Usage Example 1*).

## Rules and Rule Types

The actual business logic of this module lies in the **Rules** of the aided data management. This module extends the existing rule types with test-specific variants and, depending on the selected **Rule Type**, displays additional fields. A single rule is a building block; several rules are later chained together into a processing logic in a **Rule Flow** per material type.

**Entry point:** Open the **Rules** page via the **Search**. Open a line to edit the individual **rule**. Test-specific rules are usually recognizable by the "Test" component of the name.

### Base fields of a rule

The user defines these base fields for every rule before the test-specific fields become relevant:

| Field | Explanation |
|---|---|
| **Code** | Unique key of the rule. Via this code, the rule is later referenced in the rule flow as the **Rule Code**; without a unique code, the rule cannot be integrated into a flow. |
| **Description** | Plain-text designation of the rule. When maintained, it makes selection in the rule flow easier, because the line there has an understandable name. |
| **Rule Type** | Determines **what** the rule does and displays the fields that match it. The test-specific values are explained individually below. When one of the "Set" rule types is selected, the matrix function is additionally activated, so that the return value can be determined via the matrix. |
| **Value Type** | Defines the data type of the return value (Text, Decimal, Integer, Boolean, Date, Time, DateTime). When set, the system checks and validates the value written to a target field against this type. |
| **Direct** | When activated, the rule returns its value immediately (direct rule), without a further intermediate step; when not activated, the value is determined via the downstream flow logic or matrix. |

### Rule types of this module (Rule Type)

This module adds the following **seven** rule types. Depending on the selection, a dedicated field group is displayed on the rule card. For each rule type, it is explained **what it does** when the user selects it.

| Rule Type | Explanation |
|---|---|
| **Use Test Cert. Template** | When selected, the rule uses an **existing test certificate template** as the basis. The fields **Test Template No.** and **Test Template Version Code** are displayed. During the flow, the system creates a new test certificate template for the processed item from this template (with the description "Created for Item …"). |
| **Use Test Cert. Template Line** | When selected, the rule ensures that a line for the specified **test group** and **characteristic** exists in the target test certificate template. **Test Group Code** and **Characteristics-No.** are displayed. If the line does not exist, it is created; afterwards it is the target of subsequent "Set field" rules. |
| **Set Test Cert. Template Field** | When selected, the rule writes a calculated value into a field of the **test certificate template header**. The **Field Name** field is displayed (the target field is selected via the action on the field). The return value is validated into the selected header field in a type-appropriate manner. |
| **Set Test Cert. Template Line Field** | When selected, the rule writes a value into a field of the previously determined **test certificate template line**. **Field Name** is displayed. The prerequisite is that the target line was previously defined via "Use Test Cert. Template Line". |
| **Set Test Cert. Field** | When selected, the rule writes a value into a field of the **test certificate header** (not the template, but the actual test certificate). **Field Name** is displayed. It is used in the **Test Certificate Rule Flow**, which takes effect when a test certificate is created. |
| **Use Test Cert. Line** | When selected, the rule ensures a **test certificate line** for the specified **test group** and **characteristic** in the current test certificate. **Test Group Code** and **Characteristics-No.** are displayed. If the line is missing, it is created and serves as the target of subsequent "Set field" rules. |
| **Set Test Cert. Line Field** | When selected, the rule writes a value into a field of the previously determined **test certificate line**. **Field Name** is displayed. The prerequisite is a target line previously determined via "Use Test Cert. Line". |

> Observe the order: for line-related rule types the following applies throughout — **first** determine the line (Use Test Cert. Template Line / Use Test Cert. Line), **then** set the individual fields. This order must be observed in the rule flow, otherwise the target for the "Set field" rules is missing.

### Test-specific fields of the rule (Field | Explanation)

The module displays these fields depending on the selected **Rule Type**. They are the control fields added to the rule card by this module.

| Field | Explanation |
|---|---|
| **Test Template No.** | When set (with rule type **Use Test Cert. Template**), it determines the base test certificate template from which the flow copies a new test certificate template. Selection only from existing test certificate templates; together with the version code it acts as the key. |
| **Test Template Version Code** | When set (with rule type **Use Test Cert. Template**), it selects the specific **version** of the base test certificate template. Without a matching version code, the flow does not find the base template and creates nothing. |
| **Test Group Code** | When set (with the "…use line" rule types), it determines for which **test group** a line is ensured in the test certificate template or test certificate. Together with the Characteristics-No. it identifies the target line uniquely. |
| **Characteristics-No.** | When set (with the "…use line" rule types), it determines the specific **characteristic** within the test group. If the value is 0/empty, no specific characteristic is filtered. |
| **Field Name** | When a "Set field" rule type is selected, this field shows the currently selected **target field**. Via the action on the field, the user selects the table and field; the system remembers the field number and field name for the later value assignment. |

## Material Types and Rule Flows

For the individual rules to take effect, they are assembled per **material type** into a **Rule Flow**. This module extends the **Material Type Card** with two actions used to open and maintain the respective rule flow. Each material type internally carries two system-managed links (one GUID each for the test certificate template and the test certificate rule flow); these are created automatically the first time the respective action is opened and are not directly visible to the user.

**Entry point:** Open the **Material Types** list via the **Search** and open the desired line. On the **Material Type Card**, both actions are available in the ribbon.

### Opening rule flows from the Material Type Card

| Action (Material Type Card) | Explanation |
|---|---|
| **Test Certificate Template Rule Flow** | Opens the rule flow of type **Test Certificate Template** for this material type. If no flow yet exists for the material type, the system creates it on first invocation. This flow is executed later when an **item** of this material type is **unblocked**. |
| **Test Certificate Rule Flow** | Opens the rule flow of type **Test Certificate** for this material type. This one is also created on first invocation if not yet present. It is executed later when a **test certificate is created**. |

### The Rule Flow (Rule Flow page)

Both actions open the same **Rule Flow** page — filtered to the respective flow type (**Test Certificate Template** or **Test Certificate**). Here the user assembles the processing line by line.

| Field / Action | Explanation |
|---|---|
| **Line Type** | Defines how the line acts in the flow (e.g. execute a **rule**, a condition "If (True)/(False)/(Comparison)", set a variable, or output a message). When **Rule** is selected, the **Rule Code** field becomes editable. |
| **Flow** | Shows the indented plain-text representation of the flow assembled from line type and rule. Serves as an overview and is updated on every change. |
| **Rule Code** | References the **Code** of a previously created rule (chapter *Rules and Rule Types*). When set, exactly this rule is executed during the flow. |
| Action **Flow Editor** | Opens the graphical or structured editing of the same flow for more convenient maintenance of branched flows. |
| Action **Variables** | Opens the list of **Variables** of this flow. Variables hold intermediate results that later lines reuse. |

> Practical recommendation: build a line with a message rule at the end of each flow. It shows the user, after the automatic execution, that the flow actually ran through.

#### Setting up the Test Certificate Template Rule Flow

**Process:** This configuration is performed by the **administrator/key user** per material type, **before** items of this material type are unblocked productively. The configured flow is executed automatically later in day-to-day operations (see *Automatic Execution* and *Usage Example 1*).

1. **Prerequisite number assignment:** Ensure that **Test Cert. Nos From** is set in the **Rule Setup** (see *Setting up the Test Cert. Nos From*). It decides whether a new test certificate template is created per unblocking (**No. Series**) or the item's test certificate template is overwritten (**Item No.**).
2. **Provide rules:** Create the required building blocks in the **Rules**, typically **Use Test Cert. Template** (base template), **Use Test Cert. Template Line** (target line per test group/characteristic) and **Set Test Cert. Template Line Field** or **Set Test Cert. Template Field** (value assignment). When these rules exist, they can be referenced in the flow.
3. **Assemble the flow:** Open **Material Types → Material Type Card → Test Certificate Template Rule Flow** and set the **Line Type** and — for line type **Rule** — the **Rule Code** for each line. Note: first "Use Test Cert. Template Line", then the associated "…set field" rules.
4. **Operational completion:** As soon as an **item** of this material type is **unblocked**, the system runs the flow and creates or overwrites the test certificate template (see *Usage Example 1*).

#### Setting up the Test Certificate Rule Flow

**Process:** This configuration is an **independent** capability alongside the Test Certificate Template Rule Flow and is likewise performed per material type by the **administrator/key user**. It controls what happens automatically when a **test certificate is created**.

1. **Provide rules:** Create the rule types suitable for test certificates — typically **Set Test Cert. Field** (e.g. number of samples in the test certificate header), **Use Test Cert. Line** (target line per test group/characteristic) and **Set Test Cert. Line Field** (values in the line, e.g. from/to).
2. **Assemble the flow:** Open **Material Types → Material Type Card → Test Certificate Rule Flow** and arrange the rules via **Line Type** and **Rule Code**. Here too, observe the line-before-field order.
3. **Operational completion:** When a **test certificate is created** (e.g. at the goods receipt of an item of this material type), the flow starts automatically and fills the test certificate header and lines (see *Usage Example 2*).

## Automatic Execution of the Rule Flow

This module has no manual posting or release button. The rule flows are executed in an **event-driven** manner. The user triggers them indirectly; the system performs the processing in the background.

| Triggering event | Executed flow | Effect |
|---|---|---|
| **Item is unblocked** | **Test Certificate Template Rule Flow** of the item's material type | According to **Test Cert. Nos From**, the system creates a new test certificate template (No. Series) or overwrites the item's existing test certificate template (Item No.) and fills lines and fields according to the rules. An empty flow triggers nothing. |
| **Test certificate is created** (header inserted or object reference changed) | **Test Certificate Rule Flow** of the material type of the item referenced in the test certificate header | The system fills the test certificate header and lines according to the rules (e.g. number of samples, from/to values). Applies only to test certificates with object type **Item**; nothing happens without a stored material type or with an empty flow. |

Prerequisite in both cases: the respective rule flow of the material type is **not empty**. If no flow is stored or it contains no lines, the system skips the processing without a message.

## Typical Use Cases (Usage Examples)

The following scenarios show the end-to-end path from the trigger to the result. Each step corresponds to a page or action of this module confirmed in the code or via MCP.

### Usage Example 1: Create a test certificate template automatically from rules

1. **Trigger:** Quality assurance defines, for a specific material type, that a test certificate template with defined test lines should be created automatically for every new item. A clerk receives a new item to create.
2. **Entry point in BC (setup, one-time):** In the **Rule Setup**, the administrator sets the **Test Cert. Nos From** field (e.g. to **Item No.**, so that exactly one test certificate template is maintained per item). He then creates the building blocks in the **Rules** (**Use Test Cert. Template**, **Use Test Cert. Template Line**, **Set Test Cert. Template Line Field**) and chains them via **Material Types → Material Type Card → Test Certificate Template Rule Flow** into a flow.
3. **Core flow:** The clerk creates the new **item**, enters **Material Type Code** and **Base Unit of Measure Code** and initially sets the item to **Blocked**. After maintaining the property values, he unblocks the item again. With the unblocking, the system starts the **Test Certificate Template Rule Flow** automatically; a message rule confirms the run at the end.
4. **Completion:** The user opens the **Test Certificate Templates** via the **Search** and finds the test certificate template automatically created for the item; lines and from/to values are pre-populated according to the rules. With the **Item No.** setting, the test certificate template carries the item number and is overwritten on the next unblocking.

### Usage Example 2: Pre-populate a test certificate automatically at goods receipt

1. **Trigger:** For a purchase item, a test certificate with a suitable sample count and pre-populated limit values should be created automatically at every goods receipt, without the goods receipt employee entering values manually.
2. **Entry point in BC (setup, one-time):** The administrator creates rules of type **Set Test Cert. Field** (e.g. number of samples), **Use Test Cert. Line** and **Set Test Cert. Line Field** (limit values) and chains them via **Material Types → Material Type Card → Test Certificate Rule Flow**.
3. **Core flow:** Purchasing creates a purchase order and releases it. When the goods receipt is created, a **test certificate** is created for the item. With the insertion of the test certificate header, the system starts the **Test Certificate Rule Flow** automatically; it sets the fields in the test certificate header (e.g. number of samples) and fills the from/to values in the lines from the item properties.
4. **Completion:** The goods receipt employee opens the created **test certificate** via the test status and checks the automatically set values. A final message rule signals that the flow ran through completely.

## FAQ and Troubleshooting

### 1. Why does nothing happen when I unblock an item?
The **Test Certificate Template Rule Flow** is only executed if the item's **material type** has a **non-empty** flow. If the material type code is missing on the item, if no flow is assigned to the material type, or if the flow is empty, the system skips the processing without a message. Check the material type code and open the **Test Certificate Template Rule Flow** via the **Material Type Card**.

### 2. Why is my test certificate template overwritten on every unblocking instead of being newly created?
This is controlled by the **Test Cert. Nos From** field in the **Rule Setup**. With **Item No.**, the system maintains exactly one test certificate template per item (number = item number) and **overwrites** it on the next unblocking. If instead you want a new test certificate template on every run, choose **No. Series**.

### 3. Why does a test certificate line remain empty after "Set Test Cert. Line Field"?
The rule type **Set Test Cert. Line Field** writes only into an already determined line. If a **Use Test Cert. Line** rule with a matching **Test Group Code** and matching **Characteristics-No.** is missing beforehand, there is no target for the field. In the flow, set "Use Test Cert. Line" first and then "Set Test Cert. Line Field".

### 4. How do I select the target field for a "Set field" rule type?
First select the rule type (e.g. **Set Test Cert. Field**). The **Field Name** field then appears. Via its action, you select the table and field; the system internally remembers the field number and field name and displays the field name.

### 5. Why are the line fields not available with the rule type "Use Test Cert. Template"?
Each rule type displays only its own fields. **Use Test Cert. Template** shows **Test Template No.** and **Test Template Version Code**. For line-related entries (Test Group Code, Characteristics-No.) you need a separate rule with a "…use line" rule type.

### 6. Why doesn't the flow find the base test certificate template?
With **Use Test Cert. Template**, **Test Template No.** and **Test Template Version Code** together identify the base template. If the version code is wrong or empty, the system cannot load the template and creates nothing. Check both values.

### 7. Why is the Test Certificate Rule Flow not executed again when an existing test certificate is changed?
The Test Certificate Rule Flow starts when a test certificate is **created**, and on change only if the **object reference** (object type/object number) changes. Pure value changes to an existing test certificate do not trigger another run.

### 8. Is there a posting or release step in this module?
No. The processing is **automatic** and event-driven (unblock item or create test certificate). There is no separate posting or release action in this module.

### 9. How do I know that a flow actually ran through?
Build a line with a **message rule** (line type Message) into the flow. After the automatic processing, it shows a confirmation and is the most reliable way to make the run visible in day-to-day operations.

### 10. The Test Certificate Template Rule Flow and the Test Certificate Rule Flow use the same material type — do they influence each other?
No. Each material type runs two separate flows: one for **test certificate templates** (trigger: unblock item) and one for **test certificates** (trigger: create test certificate). They are maintained and executed at different times and via different actions of the **Material Type Card**.

## Permissions

The module ships the **MuM TCNO Permission** permission set. It determines the execution permissions for the processing logic of this module and defines which actions the assigned users can perform in the rule flow. The permission set covers the module's four codeunits (event subscribers as well as the processing codeunits for test certificates and test certificate templates) and is assignable. The actual visibility of rules, material types and test certificates additionally depends on the permissions of the underlying base modules (aided data management, material properties, test certificate management).
