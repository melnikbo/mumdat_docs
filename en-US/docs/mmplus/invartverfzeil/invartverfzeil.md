---
title: Anwenderhandbuch m+m Physical Inventory Item Tracking
---

# User Guide m+m Physical Inventory Item Tracking

## Introduction

The **m+m Physical Inventory Item Tracking** extension enhances the physical inventory process in Microsoft Dynamics 365 Business Central with an additional function when creating the physical inventory recording. It is aimed primarily at **operational users in the warehouse and in physical inventory** who process a **Physical Inventory Order** and use it to generate and count the **Physical Inventory Recording**. Warehouse management and system administration are affected only secondarily, since the app does not include any setup pages of its own.

The purpose of the module is to **substantially simplify the counting of items with item tracking** (serial numbers, lot numbers and package numbers). Without the extension, the user usually receives a single recording line per physical inventory order line and has to add the existing serial and lot numbers by hand. With the extension, Business Central can create **a separate recording line for each expected serial, lot or package number** when the recording is created, so that the user only has to enter the actually counted quantity.

The process involves only a few steps: The user opens a **Physical Inventory Order**, starts the **Make New Recording** action, enables the **Create Seperate Line Per Item Tracking** option in the dialog, and then receives a physical inventory recording in which the expected item tracking numbers are already present as separate lines.

## Quick Start for Users

The app requires no setup of its own; after installation, the additional option is immediately available in the recording creation dialog. The fastest way to separate recording lines per item tracking:

1. Open the desired **Physical Inventory Order** from the physical inventory order list and select the order line with the tracked item.
2. In the physical inventory order, choose the **Make New Recording** action. The dialog for entering options and parameters opens.
3. In the **Options** area, select the **Create Seperate Line Per Item Tracking** check box.
4. Confirm the dialog. Business Central determines the item-tracked inventory available as of the **Posting Date** of the order and creates **a separate recording line for each serial number, lot number and package number** in the physical inventory recording.
5. Open the generated **Physical Inventory Recording**, count the individual numbers, and enter the counted **Quantity** for each line.

Leave the option in step 3 disabled if you want to proceed as in the standard: In that case a recording line without prefilled tracking numbers is created, and the serial or lot numbers have to be captured manually.

## Setup

For use in the web client of Microsoft Dynamics 365 Business Central, **no additional setup is required**. The only prerequisite is that the **m+m Physical Inventory Item Tracking** app is installed and enabled in Extension Management. The extension does not include any setup pages, number series or master data of its own; it merely supplements the existing standard flow of the physical inventory recording.

For the automatic line creation to be functionally meaningful, the affected items must, in the standard, have **item tracking** (serial, lot or package number tracking) and have corresponding inventory as of the effective date. These prerequisites are fully maintained in the Business Central standard (item tracking code on the item, warehouse or bin management at the location). The extension only evaluates this existing data; it does not change the standard setup.

## Usage: Recording with Separate Tracking Lines

The entire function of the extension lies in the flow **Physical Inventory Order → Make New Recording → Physical Inventory Recording**. This section describes the additional option and its effect in detail.

### Entry Point and Invocation

**Entry point:** Physical inventory order list → open **Physical Inventory Order** → **Make New Recording** action.

Using the **Make New Recording** action in the physical inventory order, open the dialog for creating the physical inventory recording. The dialog corresponds to the Business Central standard and is supplemented by the extension with exactly one option.

### Additional Option in the Dialog

In the **Options** area of the dialog, the extension adds the following check box:

| Option | Explanation |
|--------|-------------|
| **Create Seperate Line Per Item Tracking** | When enabled, Business Central determines the item-tracked inventory available as of the **Posting Date** of the physical inventory order when the recording is created and creates a separate recording line in the **Physical Inventory Recording** for each expected **Serial No.**, **Lot No.** and **Package No.** The user then only has to enter the counted **Quantity** for each number. When not enabled, as in the standard a recording line without prefilled tracking numbers is created; the serial or lot numbers then have to be captured manually. |

The check box is **not** set by default; the standard flow therefore remains unchanged as long as the user does not deliberately enable the option. The setting applies to the respective invocation of the recording creation and is reset again after the run.

### Which Inventory Is Determined

When the option is enabled, the extension determines the existing item tracking depending on the warehouse management of the location of the order line:

- **Bin-mandatory location with bin tracking:** The basis is the **Warehouse Entries** for the matching **Location Code**, **Bin Code**, **Item No.** and **Variant Code** whose registering date is up to the **Posting Date** of the physical inventory order. Entries with a **Serial No.** or **Lot No.** are taken into account.
- **Other locations:** The basis is the **Item Ledger Entries** for the matching **Item No.**, **Variant Code** and **Location Code** up to the **Posting Date**. Entries with a **Serial No.**, **Lot No.** or **Package No.** are taken into account.

The determined quantities are summed up per combination of serial, lot and package number. **Combinations with an expected quantity of zero are not created as a recording line**, so that only tracking numbers that actually carry inventory appear in the recording.

### Result in the Physical Inventory Recording

In the generated **Physical Inventory Recording**, a separate recording line is created for each determined tracking number, with a prefilled **Serial No.**, **Lot No.** and **Package No.** The **Quantity** is deliberately prefilled with **0** and the **Recorded** indicator initially remains empty, so that the user can enter the actually counted quantity for each number and then mark the line as recorded. The remainder of the physical inventory flow (counting, recording, posting the physical inventory order) follows the Business Central standard unchanged.

### Extended Field on the Physical Inventory Order

The extension maintains an additional, internal control indicator on the **Physical Inventory Order**:

| Field | Explanation |
|------|-------------|
| **Cr. Sep. L. Item Track.** | When set, Business Central processes the separate tracking lines for this physical inventory order when the recording is created. The field is set automatically by the option in the dialog and reset again after the run; it is **not editable** and does not need to be maintained by the user. It serves solely for internal control and requires no manual editing. |

## Typical Use Cases

The following scenarios show the use of the extension in everyday work. All steps correspond to the verified flow of the app.

### Counting Lot-Tracked Items for a Cut-Off Date Physical Inventory

**Trigger:** As of the physical inventory cut-off date, a lot-tracked item has to be counted for which several lots with inventory are held in the warehouse.

**Entry point in BC:** The user opens the relevant **Physical Inventory Order** from the physical inventory order list and selects the order line of the item.

**Core flow:** Using the **Make New Recording** action, the user opens the dialog, enables **Create Seperate Line Per Item Tracking** and confirms. Business Central determines the lots available as of the **Posting Date** from the **Item Ledger Entries** and creates a separate line with a prefilled **Lot No.** for each lot in the **Physical Inventory Recording**. The user counts the individual lots and enters the respective **Quantity**.

**Completion:** After capturing the quantities, the user marks the lines as **Recorded**; further processing of the physical inventory order takes place in the standard.

### Serial-Tracked Items in a Bin-Managed Warehouse

**Trigger:** In a bin-mandatory warehouse with bin tracking, a serial-tracked item is to be counted for physical inventory.

**Entry point in BC:** The user opens the **Physical Inventory Order** and selects the order line with the matching **Location Code** and **Bin Code**.

**Core flow:** Using **Make New Recording**, the user enables **Create Seperate Line Per Item Tracking**. In this case, Business Central evaluates the **Warehouse Entries** per **Location Code**, **Bin Code**, **Item No.** and **Variant Code** up to the **Posting Date** and creates a recording line for each expected **Serial No.** The user checks the physical presence of each serial number and enters the counted **Quantity**.

**Completion:** Missing serial numbers remain with quantity 0 and thereby become visible as a shortage; the lines are marked as **Recorded** and the physical inventory order is processed further in the standard.

## FAQ and Troubleshooting

### Why are multiple lines created per item in the physical inventory recording?

Because the **Create Seperate Line Per Item Tracking** option was enabled in the **Make New Recording** dialog. Business Central then creates a separate recording line for each existing serial, lot or package number, instead of a single combined line.

### How do I still get only one recording line per item?

Leave the **Create Seperate Line Per Item Tracking** option disabled in the dialog. Then, as in the standard, a single recording line is created, and the serial or lot numbers have to be captured manually.

### Why does a particular lot not appear as its own recording line?

Only tracking numbers for which inventory is determined up to the **Posting Date** of the physical inventory order are created. Combinations with an expected quantity of zero are deliberately not created as a line.

### Why do the generated lines initially show quantity 0?

The extension deliberately prefills the expected count quantity with 0. This way, only the user enters the actually counted **Quantity**, and the count result is not anticipated by the expected inventory.

### Up to which date is inventory taken into account?

The **Posting Date** of the physical inventory order is decisive. Warehouse or item ledger entries up to and including this date are evaluated.

### What determines whether warehouse entries or item ledger entries are evaluated?

For a **bin-mandatory location with bin tracking**, the **Warehouse Entries** per location and bin are used. For all other locations, the **Item Ledger Entries** are the basis.

### Are package numbers also taken into account?

Yes. When evaluating the item ledger entries, in addition to serial and lot numbers, **Package No.** values are also evaluated and taken into account as separate recording lines.

### Do I have to set the "Cr. Sep. L. Item Track." field on the physical inventory order myself?

No. The field of the same name on the physical inventory order is not editable and is set automatically by the option in the dialog and reset again after the run. Manual maintenance is neither necessary nor possible.

### Is setup necessary before I can use the option?

No. For use in the web client, no additional setup is required; the app merely has to be installed. The affected items must have item tracking in the standard.

### Why is a serial number not included in the recording despite inventory being present?

Check the **Location Code**, **Bin Code**, **Item No.** and **Variant Code** of the order line as well as the **Posting Date**. Only entries that exactly match these values and whose date lies within the cut-off date are taken into account; without a matching movement, no line is created.
