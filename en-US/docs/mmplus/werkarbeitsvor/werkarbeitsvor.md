---
title: Anwenderhandbuch m+m Tool Management with Prod. Order Job Overview
---

# User Guide m+m Tool Management with Prod. Order Job Overview

## Introduction

The app m+m "Tool Management with Prod. Order Job Overview" combines two existing m+m extensions in "Microsoft Dynamics 365 Business Central": the **Tool Management** (m+m Tool Management) and the **Prod. Order Job Overview** (m+m Production Order Job Overview). It adds tool information to the **Prod. Order Job Overview** page and provides two planning views with which the sequence of tool assignments can be planned and transferred to the Prod. Order Job Overview.

Specifically, the app adds:

- in the **Prod. Order Job Overview** a **Tool Status** column as well as the **Required Tools** and **Installed Tools** actions, and it controls when the **Start** action is allowed for an operation;
- the **Planning Tool** view, in which planned tool assignments are displayed per work center group and arranged into a sequence;
- in the tool planning the **Transfer Sequence** action, which writes the planned sequence into the Prod. Order Job Overview.

**Target audience.** The app is aimed primarily at **operational users in production** – operators and setters who start and post operations at the work center and, in doing so, must check whether the required tools are available at the work center. Secondarily, it supports **production planners** who prepare the sequence of tool assignments. The app contains no setup or master data pages of its own; the tool master data (tool types, tools, work center tools) is maintained in the base app m+m Tool Management.

**Process overview.** The user opens the **Prod. Order Job Overview**, selects a **Work Center Group No.** (and optionally a **Work Center No.**) and sees the pending operations. Via the **Tool Status** column the user immediately recognizes whether the tools required by the operation are installed at the work center. If this is not the case, the **Start** action remains blocked; via **Required Tools** and **Installed Tools** the user can identify the difference and install tools. In parallel, the planner plans the sequence in the **Planning Tool** and transfers it with **Transfer Sequence** into the Prod. Order Job Overview.

## Prerequisites

The app is a pure integration layer and requires the three dependent apps as well as existing tool master data. Before first use, ensure the following:

| Setup | Explanation |
|---|---|
| Dependent apps | If the apps **m+m Cloud Base**, **m+m Tool Management** and **m+m Production Order Job Overview** are installed, the **Prod. Order Job Overview**, the tool master data and the additions described here are available; without these apps the tool actions and the **Planning Tool** view cannot be used. |
| Permission set **MuM TMPJ PermSet** | If this assignable permission set is assigned to a user, it determines the permissions for the table and the **Planning Tool** page as well as the related objects; without this set the user cannot open the planning views. |
| Tool master data (base app) | If tool types, tools and the assignment of tools to work centers/work center groups are maintained in the Tool Management, the app can determine the **Tool Status** per operation and populate the **Required Tools** and **Installed Tools** lists; if this master data is missing, the status remains empty or **Not okay**. |
| Released production orders with routing | If production orders are released and operations with work centers as well as required tools are stored in the routing, they appear in the Prod. Order Job Overview and in the Planning Tool; otherwise the views remain empty. |

The maintenance of the tool master data as well as all setup steps (number series, tool types, work center tools) are carried out in the base app m+m Tool Management and are not part of this extension.

## Quick Start for Users

**Operator/Setter – start an operation with tool check:**

1. Open the **Prod. Order Job Overview** via **Search**.
2. Enter the **Work Center Group No.** in the filter area and optionally the **Work Center No.**; the pending operations are displayed.
3. Check the **Tool Status** column in the line: **Okay** means that all required tools are installed at the work center, **Not okay** that at least one required tool is missing.
4. On **Not okay**, open the list of required tools via the **Required Tools** action and the list of available tools via **Installed Tools**; install missing tools via **Install Tools**.
5. Choose **Start** as soon as the status is **Okay** (on **Not okay**, **Start** is blocked).
6. Post the operation as usual via **Partial Finish** or **Finish**.

**Planner – transfer tool sequence:**

1. Open the **Planning Tool** via **Search**.
2. Narrow the display via the **Work Center Group** filter and, if applicable, **Work Center**, **Tool Type** and **Start Date**.
3. Assign the **Sequence** in the lines.
4. Choose **Transfer Sequence**; the sequence is written into the open operations of the Prod. Order Job Overview.

Alternatively, the planner transfers the sequence directly from the **Req. Tool Planning Worksheet** view via the **Transfer Sequence** action.

## Application

The application described below is carried out in "Microsoft Dynamics 365 Business Central".

### Prod. Order Job Overview with tool information

The **Prod. Order Job Overview** view is accessible via **Search**. When the user selects a **Work Center Group No.** in the header area, the associated operations of the released production orders appear. This app adds tool information to the view; the remaining operation (Start, Setup, Interrupt, Partial Finish, Finish) corresponds to the Prod. Order Job Overview of the base app.

#### Filters in the Prod. Order Job Overview

The header area controls which operations are displayed. When a filter is set, the lines are narrowed accordingly.

| Filter field | Explanation |
|---|---|
| Work Center Group No. | When set, only operations of this work center group are displayed; this is the operator's usual entry point at the start of the shift. |
| Work Center Group Name | When a work center group is selected, this field shows its name for verification; it is display-only. |
| Work Center No. | When set, the display is additionally narrowed to a single work center within the work center group; the entry is optional and is used for work at a specific machine. |
| Work Center Name | When a work center is selected, this field shows its name; display only. |
| Prod. Order No. | When set, only the operations of the specified released production order are displayed; helpful when the user works specifically on one order. |
| Date | When set, the lines are displayed with reference to the selected date; controls the time-based view of the operations. |
| Sorting | When a sorting is selected, the lines are ordered accordingly (e.g. by sequence, status or date); this determines the processing order in the display. |
| Hide finished | When activated, already finished operations disappear from the list; the user only sees open work. |
| Hide open | When activated, open operations are hidden; useful for checking work already completed. |
| Feedback in previous operation | When activated, only operations for which feedback already exists in the previous operation are displayed; this way the user only processes operations whose preceding stage is ready. |

#### Columns in the Prod. Order Job Overview

This app adds the **Tool Status** column to the line. The remaining columns come from the Prod. Order Job Overview of the base app and are listed here for orientation.

| Field | Explanation |
|---|---|
| Tool Status | When all tools required for the operation are installed at the work center, this shows **Okay** and the **Start** action is allowed; if at least one tool is missing, this shows **Not okay** and **Start** remains blocked until the tools are installed. The column is automatically recalculated per line when scrolling and is highlighted in color. |
| Prod. Order Status | Shows the status of the production order (e.g. Released). Via **Show Document** the matching production order (simulated, planned, firm planned, released, finished) is opened depending on this status. |
| Prod. Order No. | When filled, the line references the released production order; serves as a jump to the document. |
| Prod. Order Line No. | Identifies the production order line within the order; display only. |
| Sequence | When set, the value determines the processing order of the operation at the work center; it is populated by **Transfer Sequence** from the tool planning. |
| Status | Shows the status of the operation (open, started, finished, etc.) and controls which actions are allowed. |
| Previous Operation Status | Shows the status of the preceding operation; helps to recognize whether the preceding stage is completed. |
| Operation No. | Identifies the operation in the routing; display only. |
| Work Center Group No. (Line) | Shows the work center group of the operation; display only. |
| Personnel No. | When filled, the operation is assigned to an employee; the field is only editable if the personnel assignment is activated in the base app. |
| Work Center No. | Shows the work center (machine) of the operation; when changed, the line display is recalculated. |
| Interruption Reason Code / Interruption Reason Description | When an operation was interrupted, these fields document the reason; they are set when interrupting. |
| Start Date / Start Time | When filled, they indicate when the operation was started; display only. |
| Finished Quantity | Shows the quantity of the operation already posted; increases with each partial or final posting. |
| Unit of Measure Code | Shows the unit of measure of the posting; display only. |
| Prod. Order Item No. / Prod. Order Variant Code / Prod. Order Item Description / Prod. Order Item Description 2 | Describe the item to be produced of the production order line; serve to identify the work. |
| Last Operation | When set, the value marks the last operation of the production order line; relevant for completion. |
| Sales Order No. / Sell-to Customer No. / Sell-to Customer Name | When filled, they link the operation to the triggering sales order and customer; help with queries about priority. |
| Target Time / Reported Time / Open Time / Time incl. Setup | Represent the time progress of the operation (planned, reported and still open time including setup); serve for progress control. |
| Shipping Agent / Shipping Agent Service | When filled, they document shipment data of the production order line; display only. |
| Further operation context columns (Description, Description 2, Prev. Operation Type/Descr., Next Operation Type/Descr. as well as previous/next operation and production quantity) | These additional context columns of the Prod. Order Job Overview describe the operation and its neighboring operations; they support classification without being required for the tool check. |

#### Tool actions in the Prod. Order Job Overview

| Action | Explanation |
|---|---|
| Required Tools | Open the list of tools required for the selected operation (tool type, tool number, description) via the **Required Tools** action. When the **Tool Status** is **Not okay**, the user recognizes here which tools the operation requires according to the routing. |
| Installed Tools | Open the view of the tools currently installed at the work center or at the work center group via the **Installed Tools** action. From this view, tools can be added via **Install Tools** and removed via **Uninstall Tools**, so that the **Tool Status** changes to **Okay**. |
| Start (controlled by this app) | When the **Tool Status** is **Not okay**, the base **Start** action is blocked; only once the required tools are installed can the operation be started. This way the app prevents the start of an operation without the required tool equipment. |

The other actions of the Prod. Order Job Overview (**Setup**, **Interrupt**, **Partial Finish**, **Finish**, **Reopen**, **Show Document**, **Refresh Data**, **Event Log**) come from the base app and are not changed by this extension.

### Manage installed tools (Planning Tool List)

The **Installed Tools** view (Planning Tool List page) is opened exclusively modally from the Prod. Order Job Overview via the action of the same name; it is not accessible via Search. It shows the planned tool assignments for the selected line and, on the right, an **Installed Tools** FactBox with the reconciliation between required and installed tools.

| Field | Explanation |
|---|---|
| Prod. Order No. | Shows the production order of the line; display only. |
| Prod. Order Line No. | Identifies the production order line; display only. |
| Operation No. | Shows the operation for which the tools are planned. |
| Work Center (work center group of the line) | Shows the work center group of the operation; together with the type it determines the target of the installation. |
| Machine Center Name / Work Center Name | Show the names of the work center group or the work center for verification; display only. |
| Tool Type | Shows the type of the tool; display only. |
| Tool No. | Shows the specific tool; display only. |
| Tool Operation No. | Identifies the tool line in the routing; display only. |
| Type | **Work Center Group:** When the type is work center group, **Install Tools** / **Uninstall Tools** act on the work center group. **Work Center:** When the type is work center, these actions act on the individual work center. The type therefore determines at which level the tool is installed or removed. |

| Action | Explanation |
|---|---|
| Install Tools | When you choose this action, the selected tool is assigned to the work center group or the work center depending on the **Type**; afterwards it counts as installed in the reconciliation and the **Tool Status** can switch to **Okay**. |
| Uninstall Tools | When you choose this action, the assignment of the tool to the work center group or the work center is removed; the tool then no longer counts as installed. |

The two actions are grouped under the **Manage Tools** button group.

### Plan the tool sequence in the Planning Tool

The **Planning Tool** view is accessible via **Search**. It shows the planned tool assignments of the operations and serves to define their **Sequence** and then transfer it into the Prod. Order Job Overview.

#### Filters in the Planning Tool

When a filter is set, the lines are narrowed accordingly.

| Filter field | Explanation |
|---|---|
| Work Center Group | When set, only tool assignments of this work center group are displayed; usual entry point of the planner. |
| Work Center | When set, the display is additionally narrowed to a single work center; optional. |
| Tool Type | When set, only assignments of the selected tool type are displayed; helpful when a specific tool group is planned. |
| Start Date | When set, only assignments from this start date onwards are displayed; narrows the planning in time. |

#### Columns in the Planning Tool

| Field | Explanation |
|---|---|
| Prod. Order No. | Shows the production order of the planned assignment; display only. |
| Prod. Order Line No. | Identifies the production order line; display only. |
| Operation No. | Shows the operation for which the tool is required. |
| Work Center (work center group) | Shows the work center group of the operation; display only. |
| Work Center (machine) | Shows the work center of the operation; display only. |
| Tool Type | Shows the type of the required tool; display only. |
| Tool No. | Shows the specific tool; display only. |
| Tool Operation No. | Identifies the tool line; display only. |
| Start Date Time / End Date Time | Show the planned start and end date/time of the operation; serve for the time-based classification of the sequence. |
| Sequence | When you enter a value here, you define the planned processing order of the tool assignment; this value is written into the Prod. Order Job Overview when transferring. |

#### Actions in the Planning Tool

The actions are grouped under the **Process** button group.

| Action | Explanation |
|---|---|
| Transfer Sequence | When you choose this action, the **Sequence** assigned in the **Planning Tool** is numbered consecutively per work center group and written into the not-yet-finished operations of the Prod. Order Job Overview; there it appears in the **Sequence** column and controls the processing order. |
| Installed Tools | When you choose this action, the list of the tools installed at the work center is displayed, so that you can reconcile the planning with the actual equipment. |
| Show Document | When you choose this action, the associated production order is opened depending on the prod. order status. |
| Show Routing | When you choose this action, the routing of the production order for the selected operation is opened. |

### Transfer the sequence from the Req. Tool Planning Worksheet

The app adds the **Transfer Sequence** action to the **Req. Tool Planning Worksheet** view (worksheet of the tool planning). In this view the planner filters via **Work Center Group/Work Center Type**, **Work Center Group / Work Center No.**, **Tool Type** and **Start Date** and assigns the **Sequence** in the lines.

| Action | Explanation |
|---|---|
| Transfer Sequence | When you choose this action, the **Sequence** recorded in the tool planning is transferred into the matching operations of the Prod. Order Job Overview; after a successful transfer the message "Transfer of the Sequence to the Production Job overview finished successfully" appears. |

This action is assigned to the **Production Tools** group in the view.

## FAQ and Troubleshooting

### 1. Why does the Tool Status column show "Not okay"?
**Not okay** means that at least one tool required for the operation is not installed at the work center or at the work center group. Compare the requirement via **Required Tools** with the available tools shown via **Installed Tools** and install the missing ones.

### 2. Why is the Start action grayed out?
The app blocks **Start** as long as the **Tool Status** is **Not okay**. As soon as all required tools are installed and the status switches to **Okay**, **Start** is available again.

### 3. How is the Tool Status determined?
The status is calculated automatically per line when scrolling, by reconciling the tools required in the routing of the operation with the tools installed at the work center. If they match, **Okay** appears, otherwise **Not okay**.

### 4. Where do I maintain the required tools of an operation?
The assignment of required tools to operations is done in the routing or in the tool management of the base app m+m Tool Management. This extension only displays the requirement via **Required Tools**.

### 5. How do I install a missing tool at the work center?
In the Prod. Order Job Overview, open the **Installed Tools** action, select the line and then **Install Tools**. Depending on the **Type**, the tool is assigned to the work center group or the individual work center.

### 6. What does "Transfer Sequence" do?
The **Sequence** assigned in the **Planning Tool** is numbered consecutively per work center group and written into the not-yet-finished operations of the Prod. Order Job Overview. Operations already finished are not changed in the process.

### 7. Why can't I find the "Installed Tools" list via Search?
The Planning Tool List view is deliberately not accessible via Search. It is opened exclusively modally from the Prod. Order Job Overview via the **Installed Tools** action.

### 8. The Prod. Order Job Overview is empty – why is that?
There are no matching operations available or the filters narrow too strongly. Check the **Work Center Group No.**, remove the **Work Center No.** filter if applicable, and make sure that released production orders with operations at this work center group exist.

### 9. What is the difference between "Required Tools" and "Installed Tools"?
**Required Tools** shows what the operation requires according to the routing; **Installed Tools** shows what is actually available at the work center. The difference between the two lists explains a **Not okay** status.

### 10. Can I post an operation partially even though there is still a remaining quantity open?
Yes. Posting is done via the base actions **Partial Finish** (partial quantity) and **Finish** (completion). The tool extension does not restrict this; it only controls whether **Start** is allowed.

## Typical Use Cases (Usage Examples)

### Use Case 1: Tool check before the operation start

**Trigger:** The operator begins their shift and wants to start the next operation at their work center group.

**Entry in BC:** They open the **Prod. Order Job Overview** via **Search** and enter their **Work Center Group No.**; the pending operations appear.

**Core process:** In the line they check the **Tool Status** column. If it shows **Not okay**, they open **Required Tools** and see which tool the operation requires. Via **Installed Tools** they determine that this tool is missing at the work center and add it with **Install Tools**. The status switches to **Okay**, and the **Start** action becomes available. They choose **Start** and process the operation.

**Completion:** After completion they post the operation via **Partial Finish** or **Finish**; the **Finished Quantity** is updated.

### Use Case 2: Plan and transfer the tool sequence

**Trigger:** The production planner wants to define the sequence of tool assignments for a work center group for the coming day.

**Entry in BC:** They open the **Planning Tool** via **Search** and filter on the **Work Center Group**, and if applicable on **Work Center**, **Tool Type** and **Start Date**.

**Core process:** In the lines they assign the desired order in the **Sequence** column. Then they choose **Transfer Sequence**. The app numbers the sequence consecutively per work center group and writes it into the still-open operations of the Prod. Order Job Overview.

**Completion:** In the **Prod. Order Job Overview** the **Sequence** column appears filled; the operators can process the operations in the planned order.

### Use Case 3: Adopt the sequence from the tool planning

**Trigger:** The planner maintains the tool planning in the **Req. Tool Planning Worksheet** view and wants to adopt the sequence defined there directly into the job overview.

**Entry in BC:** They open the **Req. Tool Planning Worksheet** via **Search** and narrow via **Work Center Group/Work Center Type**, **Work Center Group / Work Center No.**, **Tool Type** and **Start Date**.

**Core process:** After recording the **Sequence** in the lines, they choose the **Transfer Sequence** action in the **Production Tools** group. The app transfers the sequence into the matching operations of the Prod. Order Job Overview.

**Completion:** The confirmation "Transfer of the Sequence to the Production Job overview finished successfully" appears. The sequence is then available in the **Prod. Order Job Overview**.
