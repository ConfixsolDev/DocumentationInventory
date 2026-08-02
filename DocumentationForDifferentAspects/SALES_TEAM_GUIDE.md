# TotalTrack ERP (ConfixInv / FML) — Sales Team Guide

**Audience:** Sales, Marketing, Billing, and Client Management teams  
**System:** TotalTrack ERP (ConfixInv) — meat production & inventory ERP for Fauji Meat Limited (FML)  
**Last updated:** August 2026

---

## 1. Purpose of This Document

This guide covers **all sales-related aspects** of the application: how clients are managed, how orders and consignments move through the plant, how invoices and payments work, and how the inventory (IMS) sales path differs from the meat-production Marketing path.

Use it for onboarding, day-to-day reference, and clarifying who owns each step in the quote-to-cash cycle.

---

## 2. What the System Is

TotalTrack ERP is an end-to-end system for a **meat / livestock processing and export** business. It connects:

| Area | What sales cares about |
|------|------------------------|
| **Marketing / CRM** | Clients, agreements, consignments (batches), shipments, destinations |
| **Production & Dispatch** | Order fulfillment through processing batches and dispatch |
| **Finance / Invoicing** | Export invoices, service invoices, payments, AR aging |
| **IMS (Inventory)** | Warehouse customers, sales orders, delivery orders (DOs) |

Sales primarily works in the **Marketing** module. Production and finance screens are used to track fulfillment and collection.

---

## 3. Sales at a Glance — End-to-End Flow

```
Register Client
    → (Optional) Client Agreement + Service & Product rates
    → Create Consignment / Processing Batch (linked to client)
    → Production & Dispatch
    → Create Export or Service Invoice
    → Record Payment(s)
    → Invoice Paid / AR closed
```

**Parallel IMS path (warehouse goods):**

```
Register Customer → Create Sales Order → Create Shipment (DO) → Complete order
```

> **Note:** Meat-production **Clients** and IMS **Customers** are separate master data. Use the correct module for the business type.

---

## 4. Marketing Hub (Main Sales Workspace)

**Menu:** Marketing (CRM) → opens the Marketing home screen.

### 4.1 Client and Order Management

| Module | Purpose | Sales use |
|--------|---------|-----------|
| **Client** | Master record for export / services clients and suppliers | Create and maintain buying accounts |
| **Sub Clients / Suppliers** | Downstream buyers or supplier links under a client | Capture sub-buyers for consignments/invoices |

> Order Management and Quotation Management tiles may be hidden or unavailable depending on system configuration. Consignment (batch) and invoicing remain the primary live sales path.

### 4.2 Finance (from Marketing)

| Module | Purpose |
|--------|---------|
| **Export Invoice** | Commercial invoices for export consignments |
| **Services Invoice** | Invoices for service / processing clients |

### 4.3 Consignments

| Module | Purpose |
|--------|---------|
| **Add Batch** | Create a processing batch (consignment) for a client |
| **Shipment** | Track outbound shipments |
| **Shipment Destinations** | Maintain destination master data |

### 4.4 Client Agreement & Setup (LOVs)

| Module | Purpose |
|--------|---------|
| **Client Agreements** | Contract validity, uploaded PDF, costing rates / discounts |
| **Service & Products** | Sellable service/product catalog with codes and UOM |
| **Payment Terms** | Standard payment terms for clients/invoices |
| **Mode of Delivery** | How product is delivered |
| **Mode of Transport** | Transport mode master |
| **Dispatch Status** | Dispatch status values used in ops |

---

## 5. Client Management

### 5.1 Client types (`UserType`)

When registering a client, choose the correct type:

| Type | Meaning |
|------|---------|
| **Export_Client** | Export buyer (typically export invoice path) |
| **Services_Client** | Client buying processing / service work |
| **Supplier** | Supplier account |
| **Supplier_Services_Client** | Combined supplier + services |

`ClientType` may also indicate whether the client **needs product** or **needs services**.

### 5.2 Key client fields

- Client Name  
- Contact Details  
- Registration Date  
- User Type / Client Type  
- Related destinations, payment terms, and agreements (as configured)

### 5.3 Sub Clients / Suppliers

Use **Sub Clients** when the commercial party on the invoice or shipment differs from the main client (e.g. end buyer, local agent, or supplier linkage).

### 5.4 Sales checklist — new client

1. Confirm client type (Export vs Services).  
2. Create **Client** record with complete contact details.  
3. Add **Sub Client** records if needed.  
4. Create **Client Agreement** with validity dates and attach contract PDF.  
5. Set **Service & Products** costing (rate, discount) for service clients.  
6. Assign **Payment Terms**.  
7. Confirm **Destination** and delivery/transport modes exist.

---

## 6. Client Agreements & Pricing

### 6.1 Client Agreements

Agreements hold the commercial framework for a client:

- Validity / effective dates  
- Uploaded agreement PDF  
- Linked costing (rates and discount rates) for services/products  

**Sales tip:** Do not generate service invoices from batches without a clear agreement/costing baseline—rates drive invoice lines.

### 6.2 Service & Products catalog

Maintain sellable items:

- Product / service code  
- Description  
- Unit of Measure (UOM) — e.g. Kg, PCS, Box  
- Links to product / subtype taxonomy where used  

### 6.3 Pricing mechanisms in the system

| Mechanism | Where used |
|-----------|------------|
| **Rate per KG / Charges** | Quotation lines, invoice lines |
| **Agreement Rate / DiscountRate** | Client agreement costing |
| **Line discount** | IMS sales order lines |
| **Tax** | Invoice tax type / percentage |
| **Freight** | Invoice header (adjusts grand total) |
| **Currency + Exchange Rate** | Multi-currency invoices |
| **Early payment discount % + validity** | Invoice → applied when payment is recorded |

Rate precision on invoice charges supports high decimal accuracy (important for per-kg pricing).

---

## 7. Orders (Meat Production)

### 7.1 Order Placement (when enabled)

An **Order Placement** is the meat-production sales order (not the IMS Sales Order).

**Header fields:**

- Order No.  
- Order Description  
- Order Status  
- Client  
- Mode of Delivery  
- Destination  
- Packing Type / Packing Details  
- Delivery Date  
- Is Quoted (flag)

**Line fields:**

- Type of Animal / Category of Animal  
- Type of Product / Sub Type of Product / Product Category  
- Male/Female Ratio (where applicable)  
- Pieces  
- Net Weight  
- Remarks  

### 7.2 Typical order statuses (business use)

Orders move through statuses such as open / working / fulfilled as quotations and batches are created. Confirm live status values with your administrator—labels are configurable in data.

---

## 8. Quotations (Designed Sales Path)

**Quotation Management** is designed to support:

1. Create quotation from order / client requirements  
2. Lines: net weight × rate per kg → shipment amount  
3. Approve quotation  
4. Send to client  
5. Client accept  
6. Upload client PO  
7. Proceed to production / invoicing  

**Important for sales:** Depending on deployment, the Quotation Management screens may be temporarily unavailable. In that case, commercial terms are captured via **Client Agreements**, **batch setup**, and **invoice lines**. Confirm with your admin whether quotations are live in your environment.

---

## 9. Consignments — Processing Batches

For day-to-day export/service sales, the **Processing Batch** is the operational unit that sales and ops track together.

### 9.1 Creating a batch

From Marketing → **Add Batch** (or Processing Batches):

- Link to **Client** (and order when used)  
- Choose **Batch Type**: **Export** or **Services**  
- Capture production / packing / dispatch-related details as required by ops  

### 9.2 Batch lifecycle (sales visibility)

Typical progression (ops-driven; sales monitors progress):

```
Open → Slaughtering → In-chiller → Creating Dispatch → Ready for Dispatch → Dispatched
```

Use **Batch Details**, **Batch Scheduler**, and production dashboards to answer client questions on readiness and dispatch dates.

### 9.3 Dispatch & shipment

- **Dispatch** records packaging and dispatch date against the order/batch.  
- **Shipment** (Marketing) tracks consignments leaving the plant.  
- Maintain accurate **Destinations**, **Mode of Delivery**, and **Mode of Transport**.

### 9.4 Export documentation fields sales should know

These appear on export invoices / shipping documents:

| Field | Use |
|-------|-----|
| Bill of Lading | Shipping document reference |
| E Form # | Export form reference |
| Port of Discharge | Arrival port |
| Port of Loading | Origin port |
| Mode of Shipment | How goods ship |
| Destination | Final destination |
| Data Logger Id | Cold-chain logger reference |
| Container Number | Container ID |
| Number of Pieces | Piece count |
| Gross / Net Weight | Weight for commercial & logistics docs |

---

## 10. Invoicing

Invoices are the commercial bill to the client. Types:

| Invoice type | Typical use |
|--------------|-------------|
| **Export** | Export consignments |
| **Domestic** | Domestic sales |
| **Service** | Services / processing clients (often generated from batch) |

### 10.1 Export / Domestic invoice

**Path:** Marketing → Export Invoice (or Accounts / Invoice menu)

**Common header data:**

- Invoice Number & Type  
- Client / Sub Client  
- Linked Processing Batch (one invoice per batch/type in normal flow)  
- Invoice Date / Due Date  
- Payment Terms  
- Company Bank Details  
- Currency & Exchange Rate  
- Tax Type / Tax Amount  
- Freight  
- Export fields (B/L, E Form, ports, data logger, etc.)  
- Early payment discount offer (optional %) and validity date  
- Notes  

**Line data:**

- Item details / description  
- UOM (e.g. Per KG)  
- Quantity (often net weight)  
- Charges (rate)  
- Discount  
- Line total  
- Flags for include-in-invoice / other charges  

**Create flow (sales/billing):**

1. Select client and batch.  
2. Add product lines (attribute, UOM, weight, rate/kg).  
3. Adjust tax, freight, currency.  
4. Save invoice.  
5. Print / view invoice (PDF with QR where enabled).  
6. On edit: maintain lines carefully—create vs edit line behavior differs (new lines on create; persisted line edits on edit).

### 10.2 Service invoice

**Path:** Service Invoice module, often via **Generate Invoice** from Batch Details.

- Driven by client agreement costing where configured.  
- Suited to **Services** batch types.  
- Print available from Service Invoice screens.

### 10.3 Invoice payment status (sales/AR view)

| Status concept | Meaning |
|----------------|---------|
| **Unpaid** | No payment applied |
| **Partially Paid** | Some amount received |
| **Paid** | Balance due ≈ 0 |
| **Overdue** | Unpaid/partial and past Due Date |

**Aging buckets:** Current · 1–30 · 31–60 · 61–90 · 90+ days.

### 10.4 Confidential rates

Some roles can view invoice **rates**; others may see invoice totals without rate detail. Request the correct permission if you need rate visibility for negotiations.

---

## 11. Payments & Collections

**Path:** Accounts / Finance → Payments

### 11.1 Recording a payment

1. Select the invoice.  
2. Enter **Amount**, **Payment Method**, **Reference Number**.  
3. Apply **early-payment discount** if offered and still valid.  
4. Save — system updates invoice paid amount / balance due.  
5. Finance may **reconcile** and post to General Ledger.

### 11.2 Payment fields sales should understand

- Payment Number  
- Payment Date  
- Amount / Discount Amount  
- Method (cash, bank, instrument, etc.)  
- Reference / Instrument Number  
- Reconciled flag  

### 11.3 Collections best practices

- Agree payment terms before dispatch when possible.  
- Use Due Date and aging buckets to prioritize follow-up.  
- Offer early-payment discount only with approval and within validity window.  
- Keep Sub Client vs Client correct so AR statements match the commercial party.

---

## 12. IMS Sales Path (Warehouse / Inventory)

Use this path for **store/warehouse product sales**, not carcass export consignments.

| Step | Module | Notes |
|------|--------|-------|
| 1 | **Customer** (+ contacts) | IMS customer master |
| 2 | **Sales Order** | Statuses: Draft → Open → Completed |
| 3 | Lines | Product, qty, price, discount |
| 4 | **Shipment / DO** | Delivery Order from warehouse (`#DO` numbers) |
| 5 | Complete SO | Completed orders should not be edited |

**PIC Internal / PIC Customer** = persons in charge on the sales order.  
**Store** in the UI = Warehouse.

---

## 13. Dashboards & Reports for Sales

### 13.1 Operational visibility

| Report / screen | Sales value |
|-----------------|-------------|
| Production Dashboard | Filter by export client; overall fulfillment view |
| Batch Scheduler / Batches Scheduler | When consignments are planned |
| Operational / Yield / Weight reports | Answer client queries on output |
| Dispatched Dashboard | What has left the plant |

### 13.2 Financial / AR

| Report / screen | Sales value |
|-----------------|-------------|
| Accounting Dashboard | Finance overview |
| Payment Reports / Reconciliation | Collection status |
| AR Aging / Customer Statement | Overdue follow-up (where enabled) |
| Invoice lists (Export / Service) | Open invoices by client |

> Some financial report menu links may depend on your deployment. If a report link is empty, escalate to the system administrator.

### 13.3 Exports

Many reports support **PDF** and **Excel** export for client packs and internal reviews.

---

## 14. Recommended Sales Role Access

Access is **permission-based** (controller/action), not a single fixed “Sales” role. Ask Admin to grant packs similar to:

| Role pack | Suggested access |
|-----------|------------------|
| **Sales / Marketing** | CRM, Clients, Sub Clients, Agreements, Destinations, Batches (view/create as needed), Shipments |
| **Sales + Billing** | Above + Export Invoice, Service Invoice (create/edit/print) |
| **Sales Manager** | Above + rate viewing, agreement costing, dashboards, batch scheduler |
| **Collections** | Invoice view, Payments create, Payment reports, AR aging |
| **Read-only Sales** | Client list, invoice view (no rates if confidential), batch/dispatch view |

Sensitive: **invoice rates**, **agreement costing**, **payment reconciliation**, **GL posting**.

---

## 15. Day-to-Day Playbooks

### A. New Export Client — first consignment

1. Register **Export_Client**.  
2. Add destinations and contacts / sub clients.  
3. Create **Client Agreement** if contract exists.  
4. Coordinate with ops to **Add Batch** (Export).  
5. Monitor batch through dispatch.  
6. Create **Export Invoice** with B/L, ports, weights, rates.  
7. Share printed invoice; track payment to Paid.

### B. Services Client — processing job

1. Register **Services_Client**.  
2. Set **Service & Products** rates on agreement.  
3. Create **Services** batch.  
4. After work completes, **Generate Service Invoice** from batch.  
5. Collect payment per terms.

### C. Client asks “Where is my order?”

1. Open client → related **batch / shipment**.  
2. Check **Batch Status** and **Dispatch**.  
3. Use **Batch Scheduler** / Production Dashboard if needed.  
4. Communicate status using system dates (chiller / ready / dispatched)—do not invent ETA outside ops confirmation.

### D. Overdue payment follow-up

1. Open invoice list → filter unpaid / overdue.  
2. Note **Aging Bucket** and **Balance Due**.  
3. Confirm early-discount still valid before offering it.  
4. Record payment when funds clear; escalate reconciliation to finance.

### E. Warehouse product sale (IMS)

1. Create/find **Customer**.  
2. Create **Sales Order** (Draft → Open).  
3. Arrange **Shipment / DO**.  
4. Mark order **Completed** when delivered—do not reopen casually.

---

## 16. Glossary (Sales Terms in the App)

| Term | Meaning |
|------|---------|
| **Client / ClientInfo** | Meat-production customer |
| **Customer** | IMS warehouse customer |
| **Sub Client** | Related buyer/supplier under a client |
| **Order Placement** | Meat-production sales order |
| **Sales Order (SO)** | IMS sales order |
| **Quotation Management** | Customer quote (rate/kg based) |
| **Processing Batch / Consignment** | Production lot for a client |
| **Batch Type** | Export or Services |
| **Dispatch / Dispatched** | Goods leaving the plant |
| **DO Number** | Delivery Order (IMS shipment) |
| **Rate / Charges** | Selling price (often per kg) |
| **Net Weight / Quantity** | Billable weight |
| **Export / Domestic / Service Invoice** | Invoice types |
| **Payment Terms** | When payment is due |
| **Early Payment Discount** | Optional % if paid before validity date |
| **Aging Bucket** | How long invoice is overdue |
| **Store** | Warehouse |
| **Product Code** | Item / SKU-style code (IMS) |
| **UOM** | Unit of measure |
| **Hot Weight / Chill Weight** | Production weight stages |
| **Lairage** | Live animal receiving (ops) |
| **FML** | Fauji Meat Limited branding in documents/numbers |
| **IMS** | Inventory Management System module |
| **TotalTrack ERP** | Product brand name in the app |

---

## 17. Quick Navigation Map

| I need to… | Go to |
|------------|--------|
| Register a buyer | Marketing → Client |
| Add end-buyer / supplier link | Marketing → Sub Clients / Suppliers |
| Set contract rates | Marketing → Client Agreements / Service & Products |
| Start a consignment | Marketing → Add Batch |
| See shipment destinations | Marketing → Shipment Destinations |
| Bill an export | Marketing → Export Invoice |
| Bill a service job | Service Invoice (or generate from Batch Details) |
| Record money received | Accounts → Payments |
| Check production status | Production Dashboard / Batch Scheduler |
| Sell warehouse stock | IMS → Customer → Sales Order → Shipment |

---

## 18. Handoffs — Who Owns What

| Stage | Primary owner | Sales involvement |
|-------|---------------|-------------------|
| Client setup & agreement | Sales / Marketing | Owns |
| Pricing / rates | Sales + Finance approval | Owns commercially |
| Batch creation | Sales / Ops (per policy) | Initiates / confirms |
| Slaughter → chiller → debone | Operations / QA | Monitors only |
| Dispatch & shipping docs | Dispatch / Logistics | Supplies commercial fields |
| Invoice creation | Billing / Sales | Owns accuracy of rates & client |
| Payment & reconciliation | Finance | Sales follows up collections |
| AR aging escalation | Finance + Sales | Joint |

---

## 19. Common Mistakes to Avoid

1. **Using IMS Customer for export meat clients** — use Marketing **Client**.  
2. **Wrong client type** (Export vs Services) — drives batch and invoice path.  
3. **Invoicing without correct batch link** — breaks traceability.  
4. **Missing export fields** (B/L, ports, data logger) — delays shipping document packs.  
5. **Editing rates without permission / approval** — commercial and audit risk.  
6. **Applying early-payment discount after validity** — system and policy may reject.  
7. **Marking IMS SO Completed too early** — completed orders are locked from normal edit.  
8. **Promising dispatch dates** without checking batch status with ops.

---

## 20. Support & Permissions

- If a menu tile is missing, your role likely lacks that **controller/action** permission.  
- Contact the **system administrator** to grant Marketing, Invoice, Payment, or rate-view permissions.  
- For process exceptions (credit notes, rate overrides, re-open completed SO), follow company finance/ops policy—do not bypass system controls.

---

## Document Control

| Item | Detail |
|------|--------|
| System | TotalTrack ERP (ConfixInv) |
| Brand references | FML / Fauji Meat Limited |
| Scope | All sales aspects: CRM, agreements, consignments, invoicing, payments, IMS SO |
| Related technical notes | `README_IMPLEMENTATION.md`, `INVOICE_LINE_EDIT_GUIDE.md` (invoice line edit behavior for billing users) |

---

*This guide describes the sales functionality as implemented in the application. Feature availability (especially Quotation Management and some financial reports) can vary by deployment and role permissions.*
