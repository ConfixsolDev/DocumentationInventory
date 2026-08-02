# NexusOne Product Bible (BD Reference)

Complete sellable surface of the ConfixInv Portal UI. Use for training, demos, and proposals.

---

## 1. Platform snapshot

| Item | Value |
|------|--------|
| Product | **NexusOne** — *Farm to finance.* |
| Platform family | ConfixInv |
| Vendor | Confixsol |
| UI stack (buzz-safe) | Next.js 15, React 19, TypeScript, Ant Design, Tailwind, Leaflet GIS, MySQL, JWT auth, AI-assisted land tagging (DeepSeek) |
| Currency | PKR |
| Anchor farm story | Fauji Foundation Farm Nukerji — **2,498 acres**, cultivable **1,450 ac**, Est. **1959**, Tando Muhammad Khan, Sindh, Fuleli Canal |

**Login features (official copy):**
- Crop Planning & Management
- Livestock Monitoring & Management
- HR & Financial Management
- Real-Time Reports & Farm Performance Insights

---

## 2. Portal hub — two ecosystems

### Ecosystem A — Nukerji Live Stock Park (Agri Management)

| Tile | Pitch line | Route | Modules |
|------|------------|-------|---------|
| Field Operations | Zones, crops, irrigation & daily farm command center | `/field/dashboard` | FIELD |
| Breed Development | Genetics, herd planning, weight tracking & growth | `/animal-fattening/animals` | FATTEN + FIELD |
| FMD Project | Fattening — sheds, feed, purchases & sales (7.5 ac feedlot) | `/animal-fattening/dashboard` | FATTEN |
| Organic Fertilizer | Nutrient schedules, soil health & crop input programs | `/field/crop-templates` | FIELD |
| Farm Finance | Costs, sales, labour & executive finance | `/field/accounting` | FIELD |
| Land Portfolio | CEO land map — Own/Harishare, geo-tag entry | `/field/map` | FIELD |
| Reports & Analytics | Yield trends, operational KPIs, export-ready summaries | `/field/reports` | FIELD |

**Hub highlights:** Total land 2,498 ac · Cultivable 1,450 ac · Est. 1959

### Ecosystem B — Fauji Meat Limited (Meat Production · FML)

| Tile | Pitch line | Route | Modules |
|------|------------|-------|---------|
| Production | Slaughter lines, lairage, yield & live ops feed | `/slaughtering/dashboard` | FML |
| Clients | Buyer profiles, contracts, shipments & order history | `/slaughtering/clients` | FML |
| Accounts | Invoicing, revenue tracking & financial performance | `/slaughtering/dashboard` | FML |
| Live Stock | Incoming animals, lairage capacity & procurement | `/slaughtering/dashboard` | FML |

**Hub highlights:** Multi-line processing · Export & domestic clients · Halal certified

> BD note: Accounts / Live Stock currently open the same Command Center as Production — pitch as unified command surface, not four separate apps.

---

## 3. Field Operations (FIELD) — detail

### Command & land

| Capability | What BD says | Routes |
|------------|--------------|--------|
| CEO ops dashboard | Single pane for land, crops, yield, pipeline, alerts | `/field/dashboard` |
| Zones / blocks / crops | Hierarchical farm structure | `/field`, `/field/zones/[id]`, `/field/blocks/[id]`, `/field/crops/[id]` |
| Land Portfolio map | Spatial CEO view of portfolio | `/field/map` |
| Land tagging | Section → Zone → Block/Area polygons; Own vs Harishare; categories A/B/C/D | `/field/tagging/*` |
| AI-assisted tagging | AI helps suggest/validate polygons | tagging assist API |
| Multi-farm tagging app | Parallel farm registry & tag taxonomy | `/farm-tagging/*` |

### Operations

| Capability | What BD says | Routes |
|------------|--------------|--------|
| Tasks | Planned → in progress → overdue board | `/field/tasks` |
| Workers / daily wagers | Labour registry & wage costing | `/field/workers` |
| Calendar | Season events | `/field/calendar` |
| Alerts | Critical & operational | `/field/alerts` |
| Crop templates | Input / fertilizer / nutrient programs (“Organic Fertilizer”) | `/field/crop-templates` |
| Reports | Agronomic + strategic | `/field/reports` |

### Farm Finance

| Capability | What BD says | Routes |
|------------|--------------|--------|
| Accounting hub | Costs & sales entry point | `/field/accounting` |
| Executive Farm Finance | Hari share, sale pipeline, purchase vs sale MTD | `/field/accounting/executive` |
| Crop Sales | Ledger + Record Sale (tonnes × PKR/t + grade + buyer) | `/field/accounting/sales` |
| Labour / Equipment / Expenses | Cost side of P&L | `/field/accounting/labour` etc. |

**Sale pipeline statuses:** `IN_GROUND` → `HARVEST_READY` → `PARTIAL_SOLD` → `LISTED` → `SOLD`

**Crop sale fields:** crop, block, date, quality grade, quantity tonnes, price/tonne, buyer, notes → auto revenue.

---

## 4. Animal Fattening / FMD Project (FATTEN) — detail

| Capability | What BD says | Routes |
|------------|--------------|--------|
| Feedlot dashboard | Headcount, ADG, valuation, Sales MTD, Ready-for-sale | `/animal-fattening/dashboard` |
| Sheds | Shed performance | `/animal-fattening`, `/sheds/[id]` |
| Animals | Cattle/buffalo herd; weight, ADG, breed | `/animal-fattening/animals` |
| Animal dossier | Cost to date, weights, Record Sale | `/animal-fattening/animals/[id]` |
| Feed inventory & entries | Stock + consumption → cost | `/feed/inventory`, `/feed/entries` |
| Purchases | Cost basis for animals | `/animal-fattening/purchases` |
| Sales | Live weight × PKR/kg; revenue, profit, margin, buyer | `/animal-fattening/sales` |
| Reports | Fattening analytics | `/animal-fattening/reports` |

**Animal sale fields:** animal (ACTIVE only), date, live weight kg, price/kg, buyer, notes → revenue; animal status → SOLD.

**Economics story:** Purchase + feed → ADG → target weight (~95% Ready for sale) → exit → per-animal net profit & margin %.

### FMD Freezone (outreach / geo livestock)

| Capability | Pitch | Routes |
|------------|-------|--------|
| Freezone KPIs | Villages, animals, owners | `/animal-fattening/fmd-freezone` |
| Villages | Registry + boundary polygons | `.../villages` |
| Animals | Tag with photo, owner, village, GPS | `.../animals` |
| Feeding | Feeding log + OSM geo pin | `.../feeding` |
| Visits | Health visits — medicine/vaccine inventory | `.../visits` |

Species story: cow, bull, buffalo, camel, sheep, goat (program animals — not only feedlot cattle).

---

## 5. FML Meat Production — detail

| Capability | What BD says | Routes |
|------------|--------------|--------|
| Operation Command Center | Lairage + beef + mutton lines; YTD animals / production / revenue | `/slaughtering/dashboard` |
| Channel sales | Export · Service (tolling) · Local (domestic) | Dashboard drilldowns |
| Invoice KPIs | Channel invoices, collection %, pending-invoice alerts | Dashboard panels |
| Clients | Export / local / service buyers | `/slaughtering/clients` |
| Client detail | Information · Sales history · Documentation · Payments & ledger | `/slaughtering/clients/[id]` |

**Client documentation categories:** Contract · Halal · Health · E-Form · Invoice · Other

**Shipment statuses:** Dispatched · In transit · Delivered · Pending invoice

**Export market narrative (demo data):** UAE, KSA, Qatar, Malaysia, etc.

**By-product narrative:** BNP, offal, hide, tallow (supplementary income story for processors).

---

## 6. Identity & admin

| Capability | Detail |
|------------|--------|
| Roles | admin · manager · viewer |
| Modules | FIELD · FATTEN · FML (tile visibility) |
| User admin | `/settings/users` (admin) |
| Protected areas | dashboard, modules, field, animal-fattening, slaughtering, farm-tagging, settings |

---

## 7. End-to-end value chains (teach BD these stories)

### Chain 1 — Crop to cash
Templates → assign crop to block → grow → tasks/labour/inputs → HARVEST_READY → Record Crop Sale → crop P&L & executive finance.

### Chain 2 — Feedlot margin
Purchase animal → shed → feed entries → weight/ADG → Ready for sale → Record live-weight sale → profit/margin.

### Chain 3 — Farm–feedlot loop
Napier / fodder crop sales or transfers → feedlot feed inventory → animal gain → livestock revenue.

### Chain 4 — Plant to client cash
Lairage intake → beef/mutton lines → channel dispatch → client sales history → invoice docs → payments & ledger → clear pending invoices.

### Chain 5 — Disease-zone / development
Village polygons → tag animals → geo feeding → health visits & vaccines → program KPIs (FMD Freezone).

---

## 8. KPI cheat sheet (memorize)

| KPI | Module | Why buyers care |
|-----|--------|-----------------|
| Cultivable acres / land categories | Field / tagging | Asset visibility |
| Yield / crop P&L | Farm Finance | Profit per crop |
| Sale pipeline value | Farm Finance | Forward revenue |
| ADG (kg/day) | FMD | Biological performance |
| Sales MTD | FMD | Cash pace |
| Avg margin % | FMD Sales | Exit quality |
| Lairage / line throughput | FML | Plant utilization |
| Channel sales mix | FML | Export vs local vs service |
| Pending invoices | FML | Working capital |
| Village / tagged animals | Freezone | Program coverage |

---

## 9. Do-not-oversell list

| Claim | Reality |
|-------|---------|
| Full Salesforce CRM | Not present — no leads/quotes/stages |
| Dedicated Sales role | Use admin/manager/viewer + modules |
| Barcode WMS / multi-warehouse SKU POS | Not the product |
| All FML quick actions live | Some (Shipments, E-Forms, Reports) are UI stubs |
| Every ledger always persisted | Confirm tenant/backend with engineering |

---

## 10. Route map (one screen)

```
/login → /dashboard (hub)
├── /field/*                 FIELD
│   ├── dashboard, zones, blocks, crops, tasks, workers
│   ├── map, tagging/*, crop-templates, calendar, alerts, reports
│   └── accounting, accounting/executive, accounting/sales, labour, equipment, expenses
├── /animal-fattening/*      FATTEN
│   ├── dashboard, sheds, animals, feed/*, purchases, sales, reports
│   └── fmd-freezone/* (villages, animals, feeding, visits)
├── /slaughtering/*          FML
│   ├── dashboard
│   └── clients, clients/[id]
├── /farm-tagging/*          multi-farm GIS registry
└── /settings/users          admin
```
