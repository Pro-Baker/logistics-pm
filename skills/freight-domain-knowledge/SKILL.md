---
name: freight-domain-knowledge
description: "This skill provides freight forwarding and logistics domain expertise for product management work. It should be used when the user mentions shipping, freight, logistics, forwarding, customs, RFQ, BOL, rate quoting, container types, Incoterms, carrier management, or any B2B supply chain workflow. It covers terminology, industry workflows, common integrations, and stakeholder dynamics specific to freight forwarding operations."
---

# Freight Domain Knowledge for Product Managers

## Purpose

Provide logistics-specific context so that PM artifacts (PRDs, specs, user stories, strategy docs) are grounded in how freight forwarding actually works. Generic PM plugins lack this vertical knowledge, leading to specs that miss critical domain constraints.

## Core Terminology

### Shipment Types
- **FCL** (Full Container Load) -- Shipper books an entire container. Pricing is per container.
- **LCL** (Less than Container Load) -- Cargo is consolidated with other shippers. Pricing is per CBM (cubic meter) or weight ton, whichever is greater.
- **FTL / LTL** -- Full/Less Truckload, the domestic equivalent.
- **Breakbulk** -- Cargo too large for containers; loaded individually.
- **Reefer** -- Temperature-controlled container for perishables or pharmaceuticals.

### Key Documents
- **BOL** (Bill of Lading) -- The contract between shipper and carrier. Proof of shipment.
  - **MBL** (Master BOL) -- Issued by the ocean carrier to the freight forwarder.
  - **HBL** (House BOL) -- Issued by the freight forwarder to the shipper (their client).
- **Commercial Invoice** -- Describes goods, value, buyer/seller. Required for customs.
- **Packing List** -- Itemized contents of each package/container.
- **Certificate of Origin** -- Proves where goods were manufactured. Affects tariff rates.
- **ISF** (Importer Security Filing) -- Required by US CBP 24 hours before vessel departure.

### Pricing and Quoting
- **RFQ** (Request for Quotation) -- Client requests a price for moving cargo from A to B.
- **Buy rate** -- The rate the forwarder pays to the carrier or NVOCC.
- **Sell rate** -- The rate the forwarder charges the client. Margin = Sell - Buy.
- **All-in rate** -- Includes ocean/air freight plus surcharges (BAF, CAF, THC, etc.).
- **Surcharges** -- BAF (Bunker Adjustment Factor), CAF (Currency Adjustment Factor), THC (Terminal Handling Charges), ETS (Emissions Trading System), PSS (Peak Season Surcharge).
- **Spot rate** -- One-time rate for a single shipment.
- **Contract rate** -- Negotiated rate for a defined period and volume commitment.

### Incoterms (2020)
Define where responsibility transfers from seller to buyer:
- **EXW** (Ex Works) -- Buyer bears all risk from seller's premises.
- **FOB** (Free On Board) -- Seller delivers to the vessel; risk transfers at the ship's rail.
- **CIF** (Cost, Insurance, Freight) -- Seller pays freight and insurance to destination port.
- **DDP** (Delivered Duty Paid) -- Seller bears all cost and risk to buyer's door, including customs.

### Key Stakeholders in a Forwarding Company
- **Operations team** -- Manages bookings, documentation, tracking. Heaviest app users.
- **Quoting/Sales team** -- Responds to RFQs, negotiates rates with clients and carriers.
- **Finance team** -- Invoicing, payment reconciliation, credit management.
- **Account managers** -- Client relationship, upselling, retention.
- **Customs brokers** -- Handle import/export compliance, duties, classification.

## Core Workflows

### 1. Quoting Flow
Client sends RFQ -> Sales pulls buy rates from carriers/NVOCCs -> Applies margin -> Optional benchmark check (e.g., Xeneta) -> Sends quote to client -> Client accepts/negotiates/rejects.

### 2. Booking Flow
Quote accepted -> Ops creates booking with carrier -> Receives booking confirmation -> Cargo pickup scheduled -> Container loaded -> BOL issued -> Vessel departs.

### 3. Tracking Flow
Vessel departs -> Container tracked via carrier API or AIS data -> Milestones updated (departed, in transit, arrived, customs hold, delivered) -> Client notified at each stage.

### 4. Invoicing Flow
Shipment delivered -> Invoice generated (based on agreed rates + actuals) -> Synced to accounting system (QuickBooks, Xero) -> Payment tracked -> Credit position updated.

### 5. Credit Management Flow
New client onboarded -> Financial documents collected -> Credit limit assigned -> Monitored against outstanding invoices -> Alerts at near-limit/over-limit -> Periodic review and revision.

## Common Integrations

| System | Purpose | Examples |
|--------|---------|----------|
| TMS (Transport Management System) | Core operational platform | CargoWise, Magaya, internal builds |
| Rate providers / NVOCCs | Buy rates for quoting | Shipco, OOCL, Maersk, MSC |
| Rate intelligence | Market benchmarking | Xeneta, Freightos Baltic Index |
| Accounting | Invoicing and payments | QuickBooks, Xero, SAP |
| Carrier tracking APIs | Real-time shipment visibility | INTTRA, Project44, FourKites |
| Customs / compliance | Filing, classification, duties | US CBP ABI, single-window systems |
| CRM | Client management | Salesforce, HubSpot |
| Document management | BOLs, commercial docs | Internal or DocuSign-type systems |

## Domain-Specific PM Considerations

When writing specs or PRDs for logistics features, always address:

1. **Data sync direction and frequency** -- Which system is the source of truth? How often do systems sync? What happens when sync fails?
2. **Speed constraints** -- Quoting is time-sensitive. Any feature in the quoting path must add minimal latency (<3 seconds).
3. **Multi-party data** -- Shipments involve shipper, consignee, carrier, customs broker, and the forwarder. Data flows between all of them.
4. **Compliance requirements** -- Customs regulations, trade sanctions, Incoterms obligations. These are not "nice to have" sections.
5. **Financial exposure** -- Credit limits, payment terms, currency conversion. Features that touch money need explicit risk handling.
6. **Audit trails** -- Regulated industry. Every change to a BOL, invoice, or credit limit needs a who/when/why log.
7. **Fallback behavior** -- When an API (carrier, rate provider, QuickBooks) is down, what does the user experience? Always define graceful degradation.
