---
title: Anwenderhandbuch m+m Calculation with Aided Data Management
---

# User Guide m+m Calculation with Aided Data Management

## Introduction

The **m+m Calculation with Aided Data Management** module links the m+m Calculation with the rule-based data management (rules and rule flows). It makes it possible to determine individual values in a **Calculation** no longer only manually or via a **Formula**, but to have them set automatically by a stored **Rule Flow**. This lets surcharges and deductions, base values, and alternative values of a calculation line be derived depending on the item, material type, properties, or other conditions, without the user maintaining the values by hand in every calculation.

**Target audience:** The module is primarily aimed at **operational users in Sales and Costing** who, in day-to-day business, create and recalculate a **Calculation** for a sales quote or sales order. For them the rule processing runs in the background; they see the result as an automatically set **Value** in the calculation line. Secondarily, it addresses **key users and administrators** who set up the **Calculation Template** and the **Rules**: they define which line is filled by which rule.

**Brief process overview:** An administrator flags a line in the **Calculation Template** with the **Field Type** **Rule** and assigns a **Rule Flow** to the template. In the rule-based data management they define a **Rule** of the **Rule Type** **Set Calc. Line Value**, link it to the template line, and specify which value fields are set. When the user later creates a **Calculation** using that template and recalculates it, the module automatically processes the **Rule Flow** and writes the results into the relevant calculation line.

This module provides **no** setup page of its own, no lists of its own, and no reports of its own. It only extends the **Calculation Template** from the m+m Calculation and the **Rule** from the rule-based data management with the fields and actions required for the coupling. All screens described in this guide are extended base pages of these two modules.

## Quick start for users

The fastest route from setup to an automatically calculated value. The setup steps (1–4) are performed once by an administrator or key user; the day-to-day steps (5–7) concern the operational user.

1. **Prepare the Calculation Template:** Using **Search**, open the **Calculation Templates** list and open the desired **Calculation Template**. In the line whose value is to be determined automatically, set the **Field Type** to **Rule**. This sets the line's **Value** and **Alt. Value 1** through **Alt. Value 4** to 0 and locks them for manual entry — the line will from now on be filled by the rule processing.
2. **Create a Rule Flow for the template:** On the **Calculation Template**, choose the **Rule Flow** action. On the first call, an empty **Rule Flow** is automatically assigned to the template and opened.
3. **Define a Rule:** Using **Search**, open the **Rules** list and create a **Rule**. Set the **Rule Type** to **Set Calc. Line Value**. The **Calculation** group appears: enter the **Calculation Template Code** and the **Calculation Template Line** there and select the target fields via **Set Value** / **Set Alt. Value 1** … . If required, maintain the rule's result via the **Matrix** action.
4. **Add the Rule to the Rule Flow:** Add the rule as a step to the **Rule Flow** opened in step 2 (line type **Rule**, field **Rule Code**). Optionally, control execution via **If (True)** / **If (False)** / **If (Compare)**, **Else**, and **End**.
5. **Create a Calculation:** In day-to-day business, create a **Calculation** from the sales line and choose the same **Calculation Template**.
6. **Recalculate:** Trigger the recalculation of the calculation (status **Under Development**). Before the line calculation, the module automatically processes the template's **Rule Flow**.
7. **Check the result:** In the calculation line with **Field Type** **Rule**, check the set **Value** (or **Alt. Value 1**–**4**). It was determined by the rule and cannot be edited manually.

> This module has no posting or release run of its own. The only triggering process is the **recalculation** of the calculation.

## Setup

The setup of this module does not consist of a dedicated setup card, but of two interacting configuration surfaces of the base modules: the **Calculation Template** (m+m Calculation) and the **Rule** (rule-based data management). Both are described here in full for the part relevant to this module, so that the screen can be configured without an additional guide.

### Calculation Template: flagging a line as a rule target

**Who/when:** An administrator or key user prepares the **Calculation Template** once, before users run calculations with this template. The flags set here determine which lines of the later calculation are filled by the rule processing instead of by manual entry or a formula.

**Entry point:** Using **Search**, open the **Calculation Templates** list and open the desired **Calculation Template** (card). You edit the template lines in the card's subform.

The following table describes the fields of the template line that are controlling for this module. The **Field Type** is the central field of this module; the remaining fields belong to the base Calculation Template and determine how the line would be calculated without a rule.

| Setup | Explanation |
|-------------|-------------|
| **Description** | If you enter a text, it appears as the caption of the line in the later calculation; it makes it easier for the user to recognize the rule-driven line. |
| **Field Type** | If you choose the value **Rule**, this line is no longer valued manually or by formula, but is set by the rule processing; **Value** and **Alt. Value 1**–**4** are immediately set to 0 and locked. With the other field types the standard calculation logic remains active. For the values, see the list below the table. |
| **Calculated Value** | If you assign a calculated value, the line result flows into the corresponding cost category of the calculation (e.g. material costs); controls which subtotal block the determined amount enters. |
| **Calculation Base** | If you specify a base line, the line value is applied as a percentage of the result of that base line; without a base the value acts absolutely. |
| **Formula** | If you store a formula, the line calculates its value from other line numbers; this field is only active for a formula field type and competes with the rule control — for rule-driven lines, use the **Field Type** **Rule** instead of a formula. |
| **Value** | If you enter an amount here with a manual field type, it is used directly as the line value. With **Field Type** **Rule** the field is set to 0 and overwritten by the rule. |
| **Alt. Value 1** … **Alt. Value 4** | If you maintain alternative values, additional value columns (e.g. for variants or scale tiers) are available to the calculation. With **Field Type** **Rule** these fields are also set to 0 and can be filled by the rule. |
| **Fix Value** | If enabled, the line value is retained unchanged during a recalculation; without the flag the value is re-determined at each calculation. |
| **Percent Included** | If enabled, the percentage is calculated "on the hundred" (on the gross amount) instead of "of the hundred"; affects the amount of the determined surcharge. |
| **Usage Type** | If you assign a usage type to a line, it marks its special role in the calculation; a usage type is assigned only once per template and is automatically removed from the previous line when set anew. |

**Values of the Field Type (excerpt — relevant for this module):**

- **Rule:** The value added by this module. When chosen, the line becomes the target line of a rule flow; **Value** and **Alt. Value 1**–**4** are set to 0 and locked, and are filled exclusively by the linked rule.
- All other field types of the base Calculation Template (e.g. **Calculated Value**) remain available unchanged and calculate according to the standard logic of the m+m Calculation. For the rule-driven automation, only the value **Rule** is decisive.

> The full functional meaning of all calculation fields (cost categories, multi-level calculation, certification) is part of the m+m Calculation. For this module the key point is: only lines with **Field Type** **Rule** are served by the rule flow.

**Process step:** First you define in the **Calculation Template** *which* line is rule-driven (**Field Type** **Rule**); then you assign a flow to the template via the **Rule Flow** action (see the next sections). You define the rule that supplies the value under **Master Data**.

### Setting up the Rule Flow for the Calculation Template

This dedicated setup describes activating the automation across several pages (Calculation Template → Rule Flow → Rule) and concludes with the triggering process in day-to-day business.

**Process intro:** The **Rule Flow** is the bracket that combines one or more rules into an executable sequence. It is maintained per **Calculation Template** and is created and edited via the **Rule Flow** action on the template card. It is configured by a key user before the template is first used; it is executed automatically at each recalculation of a calculation that uses this template (see **Daily Work**).

**Entry point:** Using **Search**, open the **Calculation Templates** list, open the **Calculation Template**, and choose the **Rule Flow** action (in the ribbon under Navigation, additionally as a promoted action in the process area).

**Numbered activation steps (in dependency order):**

1. **Flag the target line (template master data):** In the template line, set the **Field Type** to **Rule**. When set, this line is initialized empty and released for rule filling — without this flag no rule accesses the line.
2. **Open the Rule Flow (global coupling):** On the template, choose the **Rule Flow** action. If the template does not yet have a flow, a new, empty **Rule Flow** of type **Calculation** is automatically created on the first call, assigned to the template (via the **Rule Flow Id**), and opened. On every subsequent call the same flow is opened.
3. **Provide the Rule (master data):** In the **Rules** list, create the required **Rule** of the **Rule Type** **Set Calc. Line Value** (see **Master Data**). When set, this rule can write a target value into the calculation line.
4. **Add the Rule to the flow (scoped coupling):** In the **Rule Flow**, enter a line of the **Line Type** **Rule** and enter the previously created rule in the **Rule Code** field. When set, the rule is executed when the flow is processed. Using **If (True)**, **If (False)**, **If (Compare)**, **Else**, and **End** you control the conditions under which the step takes effect.

**Fields of the Rule Flow (line):**

| Field | Explanation |
|------|-------------|
| **Flow** | Displays the flow text of the line generated from line type, rule, and comparison (display only); if a line is shown indented, it lies within a condition. |
| **Line Type** | If you choose a line type, it determines the function of the flow line. For the values, see the list below the table. |
| **Rule Code** | If you choose a rule code for line type **Rule**, exactly this rule is executed at this point of the flow. |
| **Variable** | If you specify a flow variable, the evaluated value of this variable is used in the comparison or as an intermediate result. |
| **Compare Sign** | If you set a comparison sign on an If line, it defines the comparison operation (e.g. equal, greater, less) between the two comparison sides. |
| **Compare Rule Code** | If you specify a comparison rule, its result is used as the right-hand side of the comparison. |
| **Compare Variable** | If you specify a comparison variable, its value is used as the right-hand side of the comparison. |
| **Value Type** | Displays the value type of the line and ensures that rules and comparisons are evaluated type-consistently (e.g. decimal). |

**Values of the Line Type (relevant for this module):**

- **Rule:** When chosen, the rule stored in **Rule Code** is executed at this point — here you embed the **Set Calc. Line Value** rule.
- **If (True):** When chosen, the following, indented lines are only executed if the condition rule returns the truth value *true*.
- **If (False):** When chosen, the following lines are only executed if the condition rule returns *false*.
- **If (Compare):** When chosen, the following lines are only executed if the comparison from **Compare Sign**, **Compare Rule Code**/**Compare Variable** applies.
- **Else:** When chosen, the condition of the associated If block is reversed for the following lines.
- **End:** When chosen, it closes a condition block; subsequent lines are again executed independently of the condition.

**Operational conclusion:** The chain becomes effective as soon as the user recalculates the calculation in day-to-day business — then the module processes the flow and fills the target line. See **Daily Work: Recalculating a Calculation**.

> As an alternative to line-based editing, a graphical flow editor is available in the rule-based data management. The functional effect is identical; for this module, line-based maintenance of the **Rule Flow** is sufficient.

## Master Data

### Maintaining the "Set Calc. Line Value" Rule

**Process intro:** The **Rule** is the master record that determines a specific value and writes it into a calculation line. It is maintained by a key user in the rule-based data management before the associated **Rule Flow** is used. The values maintained here later appear as an automatically set **Value** in the calculation (see **Daily Work**). This module extends the **Rule** with the **Rule Type** **Set Calc. Line Value** and with the **Calculation** group, in which you define the target template, target line, and target fields.

**Entry point:** Using **Search**, open the **Rules** list and open the **Rule** card from a line. The **Rules** list can be found via the search; you open the **Rule** card from the list.

**General fields of the Rule (base, relevant for this module):**

| Field | Explanation |
|------|-------------|
| **Code** | If you assign a code, it uniquely identifies the rule; under this code you later embed the rule in the **Rule Flow** via the **Rule Code**. |
| **Description** | If you enter a description, it makes it easier to find the rule again in lists and in the rule flow. |
| **Rule Type** | If you choose the rule type, it determines which action the rule performs. For this module the value **Set Calc. Line Value** is decisive; only then does the **Calculation** group appear. Other base rule types (e.g. **Get Value**, **Set Property**) remain available but do not fill a calculation line. |
| **Value Type** | If you choose **Set Calc. Line Value**, the value type is automatically set to **Decimal**, because calculation values are decimal amounts; a different value type is not meaningful for this rule type. |
| **Direct** | If enabled, the rule is evaluated directly (without the detour via a flow); for the calculation filling, however, the rule is triggered via the template's **Rule Flow**. |
| **Material Type** / **Material Type Code** | If you store a material type, the rule can determine material-type-dependent values via the **Matrix**; without a material type the rule acts independently of the material type. |
| **Property** / **Characteristic Code** | If you store a property, the rule includes its value (e.g. a material property of the calculated item) in the determination. |
| **Use Defaults** | If enabled, the rule falls back to stored constant values when there is no matrix hit; without the flag a missing hit yields no value. |
| **Output Text** | If you store an output text, it is output for rule types with a message; without meaning for **Set Calc. Line Value**. |

> The Rule base page contains further fields depending on the **Rule Type** (constants, **Formula**, **Return Expression**, routing/BOM reference). These are only visible and editable for the respective base rule types. For the rule type **Set Calc. Line Value**, the fields of the **Calculation** group are decisive.

**"Calculation" group (added by this module):** This group is only visible when the **Rule Type** is set to **Set Calc. Line Value**.

| Field | Explanation |
|------|-------------|
| **Calculation Template Code** | If you choose a calculation template here, you define in which template the target line lies; only then can the rule address the correct line. The selection is limited to existing calculation templates. |
| **Calculation Template Line** | If you choose a line number, you define the specific target line within the template. Only lines of this template with **Field Type** **Rule** can be selected. When you set this field, **Set Value** is automatically enabled, so that by default the rule fills the main value. |
| **Set Value** | If enabled, the rule writes its result into the **Value** field of the target line; without the flag **Value** remains untouched by the rule. |
| **Set Alt. Value 1** | If enabled, the rule additionally writes its result into **Alt. Value 1** of the target line; useful for variant or scale-tier values. |
| **Set Alt. Value 2** | If enabled, the rule additionally writes its result into **Alt. Value 2** of the target line. |
| **Set Alt. Value 3** | If enabled, the rule additionally writes its result into **Alt. Value 3** of the target line. |
| **Set Alt. Value 4** | If enabled, the rule additionally writes its result into **Alt. Value 4** of the target line. |

**Process steps (order):**

1. First you define **Code**, **Description**, and **Rule Type** **Set Calc. Line Value**; then the **Calculation** group appears.
2. Choose **Calculation Template Code** and **Calculation Template Line** (only lines with **Field Type** **Rule** are available for selection).
3. Activate the target fields via **Set Value** / **Set Alt. Value 1** through **Set Alt. Value 4**.
4. Maintain the actual calculation result of the rule via the **Matrix** action (automatically active for this rule type), material-type- or property-dependent if required.

**Actions of the Rule:** The **Matrix** action is enabled for the rule type **Set Calc. Line Value** and opens the rule's value matrix. The **Properties** action is available as with the other rule types.

**Validation and dependency notes:**

- The **Calculation Template Line** can only be set to lines that carry the **Field Type** **Rule** in the chosen template — so the target line must first be flagged accordingly in the template (see **Setup**).
- When selecting the **Calculation Template Line**, **Set Value** is automatically enabled; adjust the target fields afterwards if required.
- The **Value Type** is fixed to **Decimal** for this rule type.

## Daily Work: Recalculating a Calculation

**Setup reference:** This process requires that the used **Calculation Template** has a line with **Field Type** **Rule**, that a **Rule Flow** is assigned to the template, and that a **Rule** of the **Rule Type** **Set Calc. Line Value** serves the target line (see **Setup** and **Master Data**). Without this setup, the calculation behaves as in the standard of the m+m Calculation.

The operational user works exclusively in the **Calculation**. The rule processing is a background process without a screen of its own.

**Process:**

1. Create a **Calculation** for the sales line and choose the prepared **Calculation Template**. The template lines are taken over as calculation lines; the line flagged with **Field Type** **Rule** initially remains with **Value** 0.
2. Make sure the calculation has the status **Under Development** — only then is a recalculation possible.
3. Trigger the **recalculation** of the calculation. Immediately before the line calculation, this module automatically processes the template's **Rule Flow**: for each **Set Calc. Line Value** rule, the determined decimal value is written into the fields stored as target (**Value** or **Alt. Value 1**–**4**) of the calculation line.
4. For the value determination, the module considers the calculated item: if the calculation is assigned to a sales line and that line is an item, this item is used; otherwise the Item No. stored in the calculation header. This allows material- and property-dependent rules to supply the appropriate value.
5. Check the set **Value** in the rule-driven line. It cannot be edited manually and is re-determined at each recalculation (unless the line is flagged as **Fix Value**).

> No additional window opens during the rule processing. If no rule flow is assigned to the template, or if the flow is empty, the calculation is computed without rule filling as in the standard.

## FAQ and Troubleshooting

### Why does the value of my calculation line remain 0 despite the rule?

Check three conditions: (1) The template line carries the **Field Type** **Rule**. (2) A **Rule Flow** is assigned to the **Calculation Template** and it contains a line of the **Line Type** **Rule** with the matching **Rule Code**. (3) In the rule, the correct **Calculation Template Line** is chosen under **Calculation** and at least **Set Value** is enabled. If one of these conditions is missing, no value is written.

### Why can't I change the value in the rule-driven line by hand?

As soon as a template line has the **Field Type** **Rule**, **Value** and **Alt. Value 1**–**4** are set to 0 and locked for manual entry. The values are reserved exclusively for the rule processing, so that manual and automatic values do not conflict.

### Why doesn't the "Calculation" group appear on the Rule?

The **Calculation** group is only visible when the **Rule Type** of the rule is set to **Set Calc. Line Value**. With any other rule type the group is hidden, because then no calculation line is served.

### Why can't I select a particular Calculation Template Line in the Rule?

The selection of the **Calculation Template Line** is limited to lines of the chosen template that carry the **Field Type** **Rule**. Flag the target line accordingly in the **Calculation Template** first; then it becomes available for selection in the rule.

### Why is "Set Value" automatically enabled when the target line is set?

When selecting the **Calculation Template Line**, the system automatically enables **Set Value**, so that the rule fills the line's main value by default. If you instead (or additionally) want to set alternative values, enable **Set Alt. Value 1** through **Set Alt. Value 4** and adjust **Set Value** if required.

### Why is the value type of my rule fixed to "Decimal"?

For the **Rule Type** **Set Calc. Line Value**, the module automatically sets the **Value Type** to **Decimal**, because calculation values are decimal amounts. A different value type would not fit type-consistently into the calculation line.

### Why does nothing visible happen except an empty list when I open "Rule Flow" on the template?

On the first call of the **Rule Flow** action, the module creates a new, empty **Rule Flow** of type **Calculation** and assigns it to the template (via the **Rule Flow Id**). The flow is empty at first; you then enter the execution steps as lines.

### Do I have to post or release the calculation for the rule to take effect?

No. This module has no posting or release step. The only trigger is the **recalculation** of the calculation in status **Under Development**. The rule processing runs automatically before the line calculation.

### How does the rule know which item it is calculating for?

The module determines the item from the calculation: if the calculation is assigned to a sales line of type Item, this item is used; otherwise the Item No. of the calculation header. On this basis, material- and property-dependent rules can supply the correct value via the **Matrix**.

### Can I fill several lines of a template in a rule-driven way?

Yes. Flag each desired template line with **Field Type** **Rule** and create one **Set Calc. Line Value** rule per target line (with the matching **Calculation Template Line**). Add all rules as steps to the template's **Rule Flow**; using **If**/**Else**/**End** lines you control which rules take effect under which conditions.

## Typical Use Cases

### Use case 1: Material-dependent surcharge automatically in the calculation

**Trigger:** Sales calculates a sales item in which a surcharge depends on the item's material type. Previously the clerk entered this surcharge manually in every calculation.

**Entry into BC:** A key user opens the **Calculation Templates** via **Search**, opens the relevant **Calculation Template**, and sets the **Field Type** to **Rule** in the surcharge line.

**Core process:**
1. On the template, the key user chooses the **Rule Flow** action; a new, empty flow is created and opened.
2. Via **Search** → **Rules** they create a **Rule** with **Rule Type** **Set Calc. Line Value**, choose the **Calculation Template Code** and the surcharge line as the **Calculation Template Line** in the **Calculation** group, and leave **Set Value** enabled.
3. Via the **Matrix** action they store the material-type-dependent surcharge values.
4. In the **Rule Flow** they enter a line of the **Line Type** **Rule** with the **Rule Code** of this rule.
5. The operational user later creates a **Calculation** with this template and recalculates it.

**Conclusion:** After the recalculation, the material-type-dependent surcharge is automatically in the **Value** of the surcharge line; manual entry is no longer required.

### Use case 2: Conditional value via an If branch

**Trigger:** A value is to be set only under a certain condition (e.g. only for a certain material type), otherwise the line should remain 0.

**Entry into BC:** The key user opens the prepared **Calculation Template** and, from there, the **Rule Flow**.

**Core process:**
1. In the rule-based data management they create two rules: a condition rule (base rule type that returns a truth value or comparison value) and a **Set Calc. Line Value** rule that writes the actual value.
2. In the **Rule Flow** they enter an **If (True)** line (or **If (Compare)** with **Compare Sign** and **Compare Rule Code**/**Compare Variable**) with the condition rule.
3. Below it — indented — they enter the line **Line Type** **Rule** with the **Rule Code** of the value rule.
4. They close the block with an **End** line; optionally they add an **Else** branch.
5. The user recalculates the calculation.

**Conclusion:** The value is only set if the condition applies; otherwise the line remains at 0. The branch is recognizable by the indentation in the **Flow** text of the rule flow.
