---
title: Anwenderhandbuch m+m Purchase Quote Manager
---

# User Guide m+m Purchase Quote Manager

## Introduction
The Purchase Quote Manager helps you build structured purchase quote campaigns from demands and existing documents, bundle vendors, and generate purchase quotes and, later, purchase orders from them.

The module is aimed at purchasing staff as well as key users who prepare, compare, and track purchase quotes from sales documents, purchase orders, or the requisition worksheet. The typical flow starts with a purchase quote campaign, proceeds through vendor and item lines to purchase quotes, and ends with purchase orders or the completion of the campaign.

## Quick Start for Users
### Create a new campaign manually
1. Open the campaign list via **Purchase Quote Campaigns**.
2. Choose **New**.
3. On the card, enter at least Description, Location Code, and Purchaser Code.
4. In the **Vendors** area, enter at least one vendor line.
5. In the **Items** area, enter the items and quantities to be requested.
6. Run the **Create Purchase Quotes** action to generate the purchase quotes.
7. Open the generated purchase quotes via the Document No. in the vendor or item lines.

### Create a campaign from an existing document
1. Open a supported document, for example a **Sales Quote**, **Sales Order**, **Sales Blanket Order**, a purchase order, or a line in the **Requisition Worksheet**.
2. There, start the **Create Purch Quote Campaign** action.
3. Open the linked campaign via the **Purchase Campaign No.** in the document.
4. Review the transferred vendor and item lines.
5. Then create the purchase quotes.

## Setup
### Number series in Purchases & Payables Setup
Before you create campaigns, a number series must be defined in the **Purchases & Payables Setup** page under the **Purchase Quote Campaign** area. Without this default, the module reports an error when a campaign is created, because the campaign number cannot be assigned.

| Setup | Explanation |
| --- | --- |
| Purchase Quote Campaign Nos. | If you define a number series here, Business Central automatically assigns a number from this series when a new campaign is created; if the entry is missing, no campaign can be saved. |

The campaign number is read from exactly this number series when a new campaign is inserted. If related series exist for the number series, Business Central can select the matching series.

### Prerequisites for daily use
For later processing, the following master data and default values should be present:

| Setup | Explanation |
| --- | --- |
| Location Code | If you set a Location Code on the campaign, it is transferred to the header of the purchase quotes when they are generated and distributed to the item lines; this controls the location for which the demand is requested. |
| Purchaser Code | If you define a Purchaser Code, it is transferred to the generated purchase quotes and identifies the responsible purchaser there. |
| Vendors | Must exist before vendor lines are created; otherwise no purchase quote can be created. |
| Items | Must exist before item lines are created; when an item is selected, Description, purchase price, and unit of measure are prefilled. |

### License check at sign-in
The module builds on **m+m Cloud Base**. At sign-in, the Purchase Quote Manager checks the license via the billing module. If no valid license is present, Business Central notifies you; the campaign functions are then not fully available.

## Master Data and Campaign Basics
### Campaign list
The **Purchase Quote Campaigns** page (list) serves as the entry point to all existing campaigns. It is sorted in descending order by number and provides the **Open**, **Released**, and **Finished** views. From here you open individual campaign cards and review the processing status. The list itself is not editable; you make changes on the card.

| Field | Explanation |
| --- | --- |
| No. | Unique identifier of the campaign. |
| Description | Free text to name the procurement project. |
| Status | Shows whether the campaign is open, released, or finished, and thereby controls whether the campaign may still be edited. |
| Linked Document Type | Shows the origin from which the campaign was created, for example Sales Quote, Sales Order, Sales Blanket Order, Purchase Order, or Requisition Worksheet. |
| Linked Document No. | Number of the origin document. Using the drill-down function, you jump directly to the associated document card. |
| Linked Worksheet Template Name | For a reference to the requisition worksheet, the name of the worksheet template. |
| Linked Journal Batch Name | For a reference to the requisition worksheet, the name of the journal batch. |

### Campaign card
The **Purchase Quote Campaign** card controls the entire process. Here you maintain the header data and work with the vendor and item lines. The area with the linked document data is only shown when the campaign was created from a document.

| Field | Explanation |
| --- | --- |
| No. | Assigned automatically from the number series on insert; if no automatic series is set up, you must retrieve the number manually. |
| Description | If you enter the purpose of the campaign here, this text is transferred to the new campaign when the campaign is copied. |
| Status | Controlled by the process. Only in the Open status are the header and lines editable; in other statuses the module locks changes. |
| Location Code | If you change the Location Code, the module offers to transfer the new code to all existing item lines, and later passes it to the generated purchase quotes. |
| Purchaser Code | If you set a Purchaser Code, it is written to the header of the purchase quotes when they are generated. |
| Linked Document Type | Indicates whether the campaign was created from a sales document, a purchase order, or the requisition worksheet; the field is not editable. |
| Linked Document No. | Stores the number of the origin document; via drill-down you open the origin document. |
| Linked Worksheet Template Name | For a reference to the requisition worksheet, stores the template used. |
| Linked Journal Batch Name | For a reference to the requisition worksheet, stores the name of the journal batch. |
| Linked Line No. | For a reference to the requisition worksheet, stores the line; after the purchase quotes are generated, it is reset so that the same line can be used again. |

### Vendor lines
In the **Vendors** area, you define which vendors the campaign is to request from. A purchase quote or purchase order can later be created for each line. The vendor field is marked as a mandatory entry.

| Field | Explanation |
| --- | --- |
| Vendor No. | The vendor to be requested. Without a Vendor No., no purchase quote is generated during creation; instead a message is logged. |
| Name | Transferred from the vendor and used for verification. |
| Address | Transferred from the vendor and used for overview. |
| Document Type | Shows whether a purchase quote or purchase order already exists for this line; as long as it is empty, the line is still unprocessed. |
| Document No. | Refers to the generated purchase quote or purchase order; via drill-down you open the respective document. |
| Purchase Quote Status | Shows the status of the generated purchase quote (for example Open or Released) and controls whether the release actions of the line are available. |

### Item lines
In the **Items** area, you define which items are requested per vendor line. When you create an additional vendor line, the module transfers the items already entered as new item lines for that vendor.

| Field | Explanation |
| --- | --- |
| Item No. | The item to be requested. When selected, Description, purchase price, and unit of measure are prefilled from the item. |
| Description | Description of the item; can be adjusted per line. |
| Variant Code | If the item maintains variants, you specify the variant to be requested here. |
| Quantity | Demand for this line. Lines with Quantity 0 are not processed when the purchase quotes are created, but are logged as an error. |
| Location Code | Location of the requested quantity; prefilled from the campaign header on insert. |
| Unit of Measure | Unit of measure of the quantity; transferred to the purchase quote line. |
| Price | Requested or expected purchase price. A change recalculates the line amount. |
| Line Amount | Calculated from Quantity and purchase price and not directly editable. |
| Shipment Date | Planned receipt date; transferred to the receipt and requested delivery dates of the purchase line when the purchase quote is generated. |
| Document Type | Shows whether the line is already bound to a purchase quote or purchase order. |
| Document No. | Number of the associated purchase quote or purchase order; via drill-down you open the document. |
| Document Line No. | Line number in the generated purchase quote or purchase order. |

## Daily Work with the Purchase Quote Campaign
### Create and maintain a campaign
First create the campaign or have it generated from an origin document. Then review the header data. If the campaign originates from a sales document, a purchase order, or the requisition worksheet, the item lines are built based on the linked document type and document number. In each case, only lines of type Item are transferred.

The module recognizes the following origins:

| Field Value | Meaning |
| --- | --- |
| Sales Quote | The campaign was created from a sales quote. The item lines are transferred from the item lines of the quote. |
| Sales Order | The campaign was created from a sales order; the item lines come from the order. |
| Sales Blanket Order | The campaign was created from a sales blanket order. |
| Purchase Order | The campaign was created from a purchase order; its item lines form the campaign items. |
| Req. Worksheet | The campaign was created from one or more lines of the requisition worksheet. |

If you re-trigger a campaign from an already linked document, the module detects the existing campaign and instead offers to open the existing card.

### Generate purchase quotes
After the vendor and item lines are fully maintained, you use the **Create Purchase Quotes** action on the campaign card to generate the purchase quotes for all vendor lines. For safety, the module prompts for confirmation and then reports success.

Processing takes place in this order:
1. For each vendor line, it is checked whether a Vendor No. is present.
2. For each vendor line, unprocessed item lines must still exist.
3. For each valid vendor line, a purchase quote is created.
4. The header data Location Code, Purchaser Code, and campaign number are transferred to the purchase quote.
5. Then the item lines with Item, Variant, Quantity, Shipment Date, Unit of Measure, and Location are written to the purchase quote.
6. Vendor and item lines then receive the Document Type **Purchase Quote** and the matching Document No.

Alternatively, you create purchase quotes specifically for individual vendors: in the **Vendors** area, select the desired lines and run the **Create Purchase Quote** action. Then the module processes only the selected vendor lines.

Typical reasons why no purchase quote is generated:

| Question | Answer |
| --- | --- |
| Why is no purchase quote generated for a vendor line? | Because the Vendor No. is empty or no unprocessed item lines exist for this vendor line. |
| Why does an item line remain without a purchase quote? | Because the Quantity is 0 or the line has already been processed. |

### Changes after generating purchase quotes
As long as an item line is bound to a purchase quote, changes to the campaign item line are synchronized with the purchase quote. In particular, quantity, price, and date changes are written back to the existing purchase quote line.

Conversely, the module can create new item lines that are entered directly on the purchase quote as campaign item lines again, provided the purchase quote is linked to a campaign and a vendor line and the campaign has the Open status.

For linked purchase quotes, the module also locks certain fields against direct change. If you try, for example, to change the vendor, item, quantity, unit of measure, variant, or location code in the header or line of the purchase quote, the module points out with a message that the field originates from the campaign. Instead, maintain these values in the campaign.

### Create purchase orders from purchase quotes
After vendor selection or after reviewing individual item lines, you can create purchase orders.

There are two business paths:
1. Via selected vendor lines with the **Make Order(s)** action. Here all matching item lines of the respective vendor are transferred into purchase orders.
2. Via selected item lines with the **Make Order** action. Here only the selected positions are carried forward; unselected positions of the same purchase quote are removed before the conversion.

The prerequisite is always that purchase quotes are already assigned to the lines. If no valid lines with a purchase quote exist, the module reports an error.

During the conversion, the following happens:
1. The module reads all affected purchase quotes.
2. The standard function for converting a purchase quote into an order is called.
3. Then vendor and item lines are switched from **Purchase Quote** to **Purchase Order**.
4. Then the module checks whether the campaign can be completed, provided no open remaining lines are left.

### Release and reopen purchase quotes
In the **Vendors** area, you can directly release or reopen the purchase quote generated for a line, without having to call up the quote individually.

| Action | Explanation |
| --- | --- |
| Release | Available when the line refers to a purchase quote in the Open status. Sets the purchase quote to Released via the standard release. |
| Reopen | Available when the linked purchase quote is released. Reopens it for editing. |

### Copy a campaign
If you want to request again based on an existing campaign, copy the campaign via the **Copy Campaign** action. Here Description, Location Code, Purchaser Code, and the existing vendor and item structure are transferred into a new campaign, but without the document links. The new campaign receives its own number; on request the module opens the new card directly.

### Control the status
The status of a campaign is managed via the **Release**, **Reopen**, and **Finish** actions.

| Status | Meaning |
| --- | --- |
| Open | The campaign is editable. In this status, lines can be maintained and purchase quotes can be generated. Via **Release** you switch to the Released status. |
| Released | The campaign is released for further processing. Via **Reopen** you return to Open in order to make changes; from this status the campaign can be ended via **Finish**. |
| Finished | The campaign is completed and only serves for tracking. |

The **Release** action is only active in the Open status, and **Reopen** and **Finish** only in the Released status. A campaign can only be ended when all required vendor and item lines have already been transferred to purchase quotes or purchase orders. If unprocessed lines remain, the module does not allow completion and reports an error.

## Working in Connected Documents
### Sales Quote, Sales Order, and Sales Blanket Order
On sales quotes, sales orders, and sales blanket orders, the module adds the **Purchase Campaign No.** field on the **General** FastTab as well as the FactBox element with the associated purchase quotes. Via the **Create Purch Quote Campaign** action you create a new campaign directly.

The flow is always the same:
1. Open the sales document.
2. Start the **Create Purch Quote Campaign** action.
3. The module checks whether a campaign already exists and, on request, opens the existing one.
4. If no campaign exists yet, a new campaign is created and linked to the document.
5. The item lines of the document are transferred as campaign items.

Via the **Purchase Campaign No.** field you can jump to the associated campaign card at any time using drill-down.

### Purchase Order
On purchase orders too, the **Purchase Campaign No.** field, the FactBox, and the **Create Purch Quote Campaign** action are available. In this case the purchase order serves as the source of the item lines. If the order is later deleted, the module removes the campaign link from the document again.

### Purchase Quote
The **Purchase Quote** card shows the **Purchase Campaign No.** field on the **General** FastTab, and the **Purchase Campaign No.** field in the line (subpage) as well. Via the drill-down you reach the campaign card in each case. This way, on the quote you immediately recognize which campaign it originates from.

### Requisition Worksheet
In the **Requisition Worksheet**, a campaign can be created for a single line or for several selected lines. For this, the campaign stores the worksheet template, journal batch name, and line number; the displayed **Campaign No.** field shows the campaign already linked to the current line.

For this, the worksheet provides several actions:

| Action | Explanation |
| --- | --- |
| Create Purch Quote Campaign | Creates a purchase quote campaign from the selected lines and transfers the item lines. |
| Add to Purchase Quote | Adds the selected lines (with accepted action message) to an existing, open purchase quote of the same vendor. |
| Add to Purchase Order | Adds the selected lines to an existing, open purchase order of the same vendor. |
| Create New Purchase Quote | Creates a new purchase quote from the selected lines and offers to open it directly. |
| Create New Purchase Order | Creates a new purchase order from the selected lines and offers to open it directly. |

For the actions to add or create documents, all selected worksheet lines must carry the same vendor; otherwise the module reports that the vendor number must be the same in all lines.

This makes the module particularly suitable for the following situation:
1. Demand is first collected in the requisition worksheet.
2. From this, a purchase quote campaign is created.
3. The item lines of the selected worksheet lines are transferred into the campaign.
4. Then you generate the purchase quotes from the campaign.

## Purchase Quotes, Orders, Printing, and Email
### Open documents
As soon as a Document No. is present for a vendor or item line, you use it to open the associated purchase quote or purchase order directly via drill-down. Depending on the document type, the module navigates to the matching card.

### Printing
From within a campaign, you print all assigned purchase quotes together via the **Print** action. For this, the module marks all purchase quotes of the campaign and starts the print defined in Business Central via the report selection for vendor documents. If no purchase quotes exist, the module reports this.

### Send email
Likewise, you send the assigned purchase quotes together by email via the **Send email** action. The module marks the purchase quotes of the campaign and uses the standard function for sending the documents.

### Behavior after posting a purchase order
When a purchase order created from the campaign is posted, the module removes the document links on vendor and item lines again. The campaign is retained for tracking, but the specific order link of the lines is cleared.

## History and Tracking
Tracking takes place mainly via the campaign card and the document information stored in it.

| Area | Benefit |
| --- | --- |
| Campaign list | Overview of all campaigns and their status, with the Open, Released, and Finished views. |
| Vendor lines | Evidence of which vendor already has a purchase quote or purchase order, including the purchase quote status. |
| Item lines | Evidence of which position was bound to which purchase quote or order line. |
| Linked document | Return to the origin document from which the campaign was created. |
| FactBox on the sales/purchase document | Shows the purchase quotes belonging to the campaign with number and vendor. |

A dedicated archive or log page is not identifiable in the module. Tracking therefore runs via status, document links, and the standard history of the generated purchase and sales documents.

## FAQ and Troubleshooting
### 1. Why can I not save a new campaign?
Because no number series for purchase quote campaigns is defined in the Purchases & Payables Setup.

### 2. Why is no new campaign created from the origin document?
Because a campaign already exists for this document. The module detects the existing link and, on request, opens the existing campaign.

### 3. Why is the purchase quote missing for a vendor line?
Because the Vendor No. is empty or no unprocessed item lines exist for this vendor line.

### 4. Why does an error message about item lines appear when creating the purchase quotes?
Because at least one item line has a Quantity of 0; such lines are not transferred to the purchase quote.

### 5. Why can I not finish the campaign?
Because there are still vendor or item lines that have not been fully transferred to purchase quotes or purchase orders, or because the campaign is not in the Released status.

### 6. Why does the Document No. jump to a purchase quote and not to a purchase order?
Because the line has so far only been processed up to the purchase quote. Only after the conversion is the Document Type switched to Purchase Order.

### 7. Why do values in the purchase quote change when I change the campaign line?
Because the module synchronizes changes to already linked campaign item lines back into the purchase quote.

### 8. Why can I no longer change certain fields in the purchase quote?
Because the purchase quote is linked to a campaign. The module locks changes to fields such as vendor, item, quantity, unit of measure, variant, and location code, so that the campaign and document remain consistent.

### 9. Why is the link to a purchase order empty after posting?
Because the module deliberately removes the document links from the campaign lines after a purchase order is posted.

### 10. Why is a Campaign No. already present in the requisition worksheet?
Because the module found a campaign for exactly this worksheet line based on the worksheet template, journal batch name, and line number.

## Typical Use Cases
### Convert a sales quote into vendor requests
**Trigger:** Sales has created a sales quote with several item positions for which current purchase prices are needed.

**Entry in BC:** Open the **Sales Quote** and start the **Create Purch Quote Campaign** action there.

**Core flow:**
1. The module creates a new campaign and links it to the sales quote.
2. The item lines of the quote are transferred into the campaign.
3. On the campaign card, in the **Vendors** area, add the desired vendors.
4. Run the **Create Purchase Quotes** action.
5. Open the generated purchase quotes via the Document No. and review purchase prices, quantities, and receipt dates.

**Completion:** Print or send the purchase quotes directly from the campaign via **Print** or **Send email**.

### Bundle demand from the requisition worksheet
**Trigger:** Planning has built several demand lines in the requisition worksheet that are to be requested together on the market.

**Entry in BC:** Open the **Requisition Worksheet**.

**Core flow:**
1. Select the desired lines and run **Create Purch Quote Campaign**.
2. The module stores the worksheet template, journal batch name, and line reference in the campaign.
3. Review the automatically transferred item lines.
4. In the **Vendors** area, add the vendors to be requested.
5. Run **Create Purchase Quotes**.

**Completion:** Via the **Campaign No.** field in the requisition worksheet, you can later switch back to the campaign at any time.

### Convert existing purchase quotes into purchase orders
**Trigger:** One or more vendors have responded to the purchase quote, and the quote is to be transferred into a purchase order.

**Entry in BC:** Open the **Purchase Quote Campaign**.

**Core flow:**
1. In the **Vendors** area, select the affected lines, or in the **Items** area select individual positions specifically.
2. Start **Make Order(s)** (vendor lines) or **Make Order** (item lines).
3. The module converts the associated purchase quotes into purchase orders.
4. Vendor and item lines are switched to the Purchase Order document type.
5. Review the generated purchase orders via the Document No.

**Completion:** Then end the campaign via **Finish**, provided no open remaining lines are left.

### Reuse an existing campaign for a follow-up request
**Trigger:** An already completed request situation is to be carried out again with similar data.

**Entry in BC:** Open the existing **Purchase Quote Campaign**.

**Core flow:**
1. Use the **Copy Campaign** action.
2. On request, open the newly created campaign directly.
3. Adjust vendors, quantities, purchase prices, or dates.
4. Run **Create Purchase Quotes**.

**Completion:** The old campaign is retained; the new campaign has its own number and its own document links.
