# AXIA — Managed B2B Resource-Exchange Infrastructure

> *"Where Surplus Finds Its Next Value."*

---

## 👥 1. Team Name & Members

- **Team Name**: **Team AXIA**
- **Team Members**:
  - **Krishi Oza** — Lead Software Engineer, Systems Architect & Product Lead ([krishioza384@gmail.com](mailto:krishioza384@gmail.com))
  - *(Team AXIA Core Contributors)*

---

## 📋 2. Executive Summary (Brief)

**AXIA** is a managed B2B resource-exchange infrastructure platform that resolves a fundamental global market failure: **the geographical value discrepancy of industrial surplus and second-life electronics**.

A resource may have near-zero or negative disposal value in one geography, yet command significant economic utility in another. Traditional marketplaces fail because simple bulletin boards cause commercial disintermediation, tax/customs violations, and logistics failures. 

AXIA operates as the **managed counterparty, escrow layer, and logistics coordinator**:
- **Commercial Anonymity**: Buyers and sellers never interact directly or see each other's margins.
- **Landed Economics Engine**: Pre-calculates freight, duties, testing, compliance, and margins before green-lighting transactions.
- **Deterministic 2-Buyer Auction Rule**: 1 interested buyer executes via **Direct Buy**; 2 or more buyers automatically triggers an **Anonymous Auction**.
- **Dual Strategic Scope**:
  - *Inside India*: Broad industrial resource exchange (metals, steel billets, aluminum offcuts, polymer regrinds, capital machinery).
  - *International (USA/China → India)*: High-arbitrage secondary electronics and component supply chains (laptops, server RAM, NVMe SSDs, smartphones).
- **On-Demand Scope 3 Impact Accounting**: Audit-ready environmental reporting calculated on-demand via life-cycle displacement methodology without greenwashing.

---

## 📌 3. Problem Statement

### The Geographical Value Discrepancy Problem
Enterprise IT asset disposition (ITAD) facilities in Dallas or Silicon Valley frequently decommission thousands of working enterprise laptops (e.g., 11th Gen Core i5 units) with low scrap value domestically due to high labor refurbishment costs. Conversely, rapidly expanding Indian refurbishers and corporate training enterprises face severe hardware deficits and are eager to acquire these units at ₹18,000–₹22,000 landed.

### Why Existing Solutions Fail:
1. **The Unmanaged Bulletin-Board Failure**:
   Traditional B2B listing boards (e.g., Alibaba, IndiaMART) simply introduce buyer and seller. Counterparties quickly bypass the platform ("disintermediation"), encounter payment default, or suffer cargo abandonment due to unforeseen regulatory barriers.
2. **Economic Viability Blindness**:
   Moving physical assets across borders requires factoring in containerized freight, marine cargo insurance, Basic Customs Duty (7.5%), Integrated GST (18%), EPR (Extended Producer Responsibility) authorizations, and risk buffers. Without deterministic pre-calculation, cross-border shipments turn into stranded liabilities.
3. **The Greenwashing Epidemic**:
   Environmental platforms frequently paste speculative carbon badges across catalogs without mathematical grounding, discrediting corporate ESG reports.

---

## 💡 4. The AXIA Solution & Architecture

AXIA acts as the **central transaction, compliance, and logistics authority**:

```
┌──────────────┐             ┌─────────────────────────────────────┐             ┌──────────────┐
│   SUPPLIER   │             │            AXIA PLATFORM            │             │   RECEIVER   │
│  (Surplus)   │ ──────────> │   - Commercial Anonymity & Escrow   │ ──────────> │   (Demand)   │
│              │             │   - Landed Economics Engine         │             │              │
│  Dallas Hub  │             │   - Deterministic 2-Buyer Auction   │             │  Mumbai Hub  │
└──────────────┘             │   - Intermodal Logistics & Customs  │             └──────────────┘
                             └─────────────────────────────────────┘
```

- **Mutual Anonymity**: Supplier sees `IND — Mumbai Distribution Hub`; Receiver sees `USA — Dallas Logistics Hub`.
- **Escrow Settlement**: Supplier is guaranteed net payout upon dispatch confirmation; Receiver pays a single consolidated landed B2B invoice.
- **Physical Chain of Custody**: Assigned logistics partners receive unmasked facility coordinates while commercial parties remain shielded.

---

## 🧮 5. Core Business Logic & Mathematical Engines

### A. Landed Economics Engine (`landedCostEngine.ts`)
For every lot, AXIA evaluates total landed cost against the destination market demand benchmark:

$$\text{Assessable Value} = \text{Acquisition Cost} + \text{Freight} + \text{Marine Insurance}$$

$$\text{Customs Duty} = \text{Acquisition Cost} \times \text{Duty Rate (7.5\%) } \quad [\text{Cross-border only}]$$

$$\text{GST/IGST} = (\text{Assessable Value} + \text{Customs Duty}) \times 18\%$$

$$\text{Total Landed Cost} = \text{Acquisition} + \text{Freight} + \text{Insurance} + \text{Domestic Hub Transport} + \text{Testing/Refurb} + \text{Compliance} + \text{Duty} + \text{GST} + \text{Risk Reserve} + \text{Receiver Fee}$$

$$\text{Net Economic Outcome} = \text{Destination Market Value} - \text{Total Landed Cost}$$

$$\textbf{Feasibility Gate: } \begin{cases} \textbf{VIABLE}, & \text{if } \text{Landed Cost} \le \text{Max Buyer Budget} \land \text{Margin} \ge 8\% \\ \textbf{NOT VIABLE}, & \text{otherwise (route suppressed / deprioritized)} \end{cases}$$

### B. Weighted Deterministic Matching Algorithm (`matchingEngine.ts`)
Pairwise compatibility between listings and requirements is scored deterministically:

$$\text{Match Score} = (0.35 \times \text{Material}) + (0.20 \times \text{Quantity}) + (0.20 \times \text{Economics}) + (0.15 \times \text{Distance}) + (0.10 \times \text{Timing})$$

- **Hard Gates**: Material category match and Economic Feasibility (**VIABLE**) are non-negotiable prerequisites.
- **Checklist Badges**: Material compatible, Quantity available, Within budget, Logistics feasible, Timing feasible, Compliance check passed.

### C. Deterministic Commercial Auction Rule
- $\text{Interested Buyers} < 2 \implies \textbf{DIRECT BUY}$ (No artificial delay or auction overhead).
- $\text{Interested Buyers} \ge 2 \implies \textbf{ANONYMOUS MULTI-BUYER AUCTION}$ (Bids submitted anonymously as Buyer A, Buyer B, Buyer C; Supplier sees winning offer without identities).

### D. Scope 3 Life-Cycle Avoidance Environmental Accounting (`impactCalculator.ts`)
Strictly optional and calculated only when explicitly requested:

$$\text{Avoided } \text{CO}_2\text{e} = \text{Baseline Pathway Emissions} - \text{AXIA Pathway Emissions}$$

- **Baseline Footprint**: Cradle-to-gate embodied carbon of displaced virgin manufacturing + end-of-life incineration/landfill emissions.
- **AXIA Pathway Footprint**: $(\text{Intermodal Freight Distance} \times \text{Tonnage} \times \text{Freight Factor}) + (\text{Units} \times \text{Workshop Diagnostic Electricity})$.

---

## 🛠️ 6. Tech Stack

| Layer | Technologies | Purpose |
| :--- | :--- | :--- |
| **Frontend Framework** | **React 19.0.1** | Modern component architecture, functional hooks, concurrent rendering |
| **Language** | **TypeScript 7.0.2** | Strict end-to-end type safety across commercial & logistics interfaces |
| **Build & Tooling** | **Vite 8.3.0** | Ultra-fast HMR and optimized production bundling |
| **Styling & Design System**| **Tailwind CSS v4.3.3** (`@tailwindcss/vite`) | Custom corporate B2B design system, responsive utility tokens |
| **Icons & Visuals** | **Lucide React 0.546.0** | Consistent, crisp vector interface iconography |
| **Animation** | **Motion 12.23.24** | Subdued micro-interactions, modal transitions, and drawer choreography |
| **Typography** | **Plus Jakarta Sans** + **JetBrains Mono** | Tabular figures (`tabular-nums`) for vertical ledger financial alignment |

---

## 🚀 7. Setup & Installation Instructions

### Prerequisites
- **Node.js**: v18.0.0 or higher
- **npm**: v9.0.0 or higher

### Step-by-Step Installation:

```bash
# 1. Clone the repository
git clone <repository-url>
cd <repository-folder>

# 2. Install all dependencies from package.json
npm install

# 3. Configure environment variables (copy example)
cp .env.example .env

# 4. Start the local development server on port 3000
npm run dev
```

Open your browser to `http://localhost:3000`.

### Production Build & Linting:

```bash
# Validate TypeScript compilation without emitting files
npm run lint

# Build production assets into /dist
npm run build

# Preview production build locally
npm run preview
```

---

## 🧭 8. Complete 16-Step Hackathon Demo Walkthrough

The platform includes a sticky **Demo Walkthrough Bar** at the top with next/previous controls:

1. **Step 1 (Supplier View)**: USA Supplier lists 4,000 Dell Latitude laptops from Dallas Logistics Hub.
2. **Step 2 (Admin View)**: AXIA Landed Economics Engine evaluates acquisition, ocean freight, 7.5% duty, 18% IGST, and testing costs.
3. **Step 3 (Receiver View)**: Mumbai refurbisher posts requirement `AX-REQ-8021`: 1,000 laptops under ₹20,000 landed cost.
4. **Step 4 (Receiver View)**: AXIA discovers USA $\to$ India opportunity at ₹15,000 landed cost (**STATUS: VIABLE**, ₹8,500 margin spread).
5. **Step 5 (Admin View)**: China $\to$ India opportunity at ₹21,800 landed cost is automatically marked **NOT VIABLE** (exceeds receiver budget).
6. **Step 6 (Receiver View)**: Receiver expresses commercial intent on the USA listing.
7. **Step 7 (Receiver View)**: With 1 interested buyer, AXIA enables **Direct Buy** mode.
8. **Step 8 (Supplier View)**: On lot `AX-RES-2089` (Steel Billets), 3 buyers express interest $\implies$ AXIA automatically starts an **Anonymous Auction** (Buyer A: ₹45/kg, Buyer B: ₹48/kg, Buyer C: ₹51/kg).
9. **Step 9 (Admin View)**: Transaction `AX-20481` executes through AXIA commercial escrow.
10. **Step 10 (Logistics View)**: Carrier manages intermodal milestones from Dallas depot to Nhava Sheva port customs clearance.
11. **Step 11 (Logistics View)**: Delivery completes at Bhiwandi destination facility; weighbridge slip clears.
12. **Step 12 (Receiver View)**: User clicks **"View Environmental Impact"** on the completed order.
13. **Step 13 (Receiver View)**: Transparent Scope 3 avoided carbon calculation displays ($220\text{t baseline} - 28\text{t AXIA pathway} = 192\text{t CO}_2\text{e avoided}$).
14. **Step 14 (Receiver View)**: User clicks **"Generate Institutional Impact Report"** to render an audit-grade printable PDF/document.
15. **Step 15 (Supplier View)**: Supplier accesses 30/60/90-day surplus volume forecast (80t $\to$ 110t $\to$ 140t).
16. **Step 16 (Supplier View)**: For 25 tonnes unsold surplus, AXIA recommends downstream industrial applications (Construction Aggregate, Road-base Stabilizer).

---

## 🔐 9. Commercial Anonymity & Data Permissions Matrix

| Data Field | Supplier View | Receiver View | Logistics Partner | Admin Master Console |
| :--- | :---: | :---: | :---: | :---: |
| **Counterparty Corporate Name** | ❌ Shielded | ❌ Shielded | ❌ Shielded | ✅ **Unmasked** |
| **Physical Facility Address** | Regional Hub Alias | Regional Hub Alias | ✅ **Exact Address** | ✅ **Exact Address** |
| **Base Acquisition Cost** | ✅ Visible | ❌ Hidden | ❌ Hidden | ✅ **Visible** |
| **Duties, Taxes & Platform Fees** | ❌ Hidden | ❌ Hidden | ❌ Hidden | ✅ **Line-by-Line Breakdown** |
| **Gross / Net Payout** | ✅ Net Payout Only | ❌ Hidden | ❌ Hidden | ✅ **Full Escrow Ledger** |
| **Total Landed Invoice** | ❌ Hidden | ✅ Landed Cost / Unit | ❌ Hidden | ✅ **Visible** |
| **Auction Bidding Identities** | Winning Offer Only | Own Bids + Anonymized | ❌ Hidden | ✅ **Full Bidder Resolution** |
| **Environmental Impact Report** | On-Demand | On-Demand | ❌ Hidden | ✅ **Audited Access** |

---

## ⚖️ 10. Disclaimer & Regulatory Compliance Notice

All tax rates (7.5% Basic Customs Duty, 18% IGST), freight distances, and carbon factors utilized in this MVP are deterministic model prototypes. Calculations are intended for economic demonstration and internal Scope 3 corporate sustainability accounting; they do not constitute official legal, statutory customs advice, or sovereign carbon credit issuance.

---

## 📄 11. License

Licensed under the **Apache-2.0 License**. Developed for Google AI Studio Hackathon 2026.
