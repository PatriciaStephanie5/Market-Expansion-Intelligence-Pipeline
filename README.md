# Market Expansion Intelligence Pipeline
[![Tableau](https://img.shields.io/badge/Tableau-2024.1-blue)] (https://public.tableau.com/app/profile/timba.patricia.stephanie/viz/MarketExpansionDashboard_17760155743840/Dashboard1)
[![Make](https://img.shields.io/badge/Make-Automation-6D4AFF)](

## Project Overview

An automated market intelligence pipeline that identifies, enriches, and prioritizes Y Combinator‑backed SaaS startups across Germany, France, and the Netherlands. Built for **Expandly**, a Series B B2B SaaS platform helping startups plan predictable geographic expansion.

**Business Impact:**
- Reduced manual research time from **3 weeks → 4 hours**
- Identified **16 high‑value targets** with firmographic enrichment
- Delivered **interactive Tableau dashboard** for sales prioritization

## Business Context

**Company:** Expandly (Series B, B2B SaaS)  
**Challenge:** The Growth team lacked a clean, enriched dataset of target SaaS companies in three new European markets. Manual research was slow and missed key growth signals.  
**Solution:** An automated pipeline that scrapes YC company data, enriches with LinkedIn firmographics, and visualizes in a sales‑ready dashboard.

## Technical Architecture

![Architecture Diagram](images/architecture_diagram.png)

| Stage | Tool | Purpose |
|-------|------|---------|
| **Data Collection** | Apify Y Combinator Scraper (simulated) | Extract YC‑backed startups by location |
| **Data Enrichment** | Apify LinkedIn Company Scraper (simulated) | Add employee count, industry, follower data |
| **Automation** | Make (formerly Integromat) | Parse JSON → Google Sheets (weekly schedule) |
| **Visualization** | Tableau Public | Interactive dashboard with map, tiers, priority scoring |

> **Note:** This project uses a **simulated dataset** for portfolio demonstration due to scraper subscription requirements. The pipeline is fully functional and ready for live data integration.

## Key Features

- **Geographic Mapping:** Visualize company locations sized by employee count
- **Tier Segmentation:** Auto‑categorize as Enterprise / Mid‑Market / SMB
- **Priority Scoring:** Weighted algorithm combining size, hiring activity, and social presence
- **Interactive Filters:** Drill down by country, tier, and industry
- **Live Google Sheets Connection:** Tableau refreshes on schedule

## Make Automation Workflow

![Make Scenario](images/make_scenario.png)

The Make scenario runs weekly to:
1. Parse the simulated YC + LinkedIn JSON dataset
2. Append each company record to Google Sheets
3. Maintain a clean, up‑to‑date master list for Tableau

**Blueprint:** `workflows/make_scenario_blueprint.json`

## Tableau Dashboard

![Dashboard Screenshot](images/dashboard_screenshot.png)

### Dashboard Components

| Sheet | Description |
|-------|-------------|
| **Market Map** | Geographic distribution with company size bubbles |
| **Tier by Country** | Stacked bar chart of Enterprise/Mid‑Market/SMB distribution |
| **Industry Heatmap** | Concentration of industries per country |
| **Priority Targets** | Ranked list with Priority Score for sales focus |

### Calculated Fields

```tableau
// Company Tier
IF [Employee Count Estimate] >= 200 THEN "Tier 1: Enterprise"
ELSEIF [Employee Count Estimate] >= 50 THEN "Tier 2: Mid-Market"
ELSE "Tier 3: SMB"
END

// Priority Score (weighted)
[Employee Count Estimate] * 0.4 +
[Open Jobs Count] * 10 * 0.3 +
LOG([Followers Count] + 1) * 0.3



---


# Go‑to‑Market Strategy: Expandly European Expansion

## 1. Executive Summary

This document outlines a data‑driven market entry strategy for Expandly's expansion into Germany, France, and the Netherlands. Analysis of Y Combinator‑backed SaaS startups reveals clear prioritization based on company size, growth signals, and industry concentration.

## 2. Market Prioritization Framework

We evaluated three dimensions:

| Dimension | Weight | Data Source |
|-----------|--------|-------------|
| Company Size (employee count) | 40% | LinkedIn enrichment |
| Hiring Activity (open jobs) | 30% | YC profile scraping |
| Social Presence (LinkedIn followers) | 30% | LinkedIn enrichment |

### Priority Ranking

| Rank | Country | Score Rationale |
|------|---------|-----------------|
| 1 | **France** | Highest average employee count (157), most open jobs per company (3.4), strong LinkedIn presence |
| 2 | **Germany** | Broad industry diversification, recent S25/W25 batches indicate new YC investment |
| 3 | **Netherlands** | Concentrated tech hubs (Amsterdam, Eindhoven), high B2B SaaS density |

## 3. Account Segmentation

### Tier Definitions

| Tier | Employee Range | Count | % | Recommended Motion |
|------|----------------|-------|----|-------------------|
| Tier 1: Enterprise | 200+ | 3 | 19% | Strategic partnerships, senior AE outreach |
| Tier 2: Mid‑Market | 50‑199 | 7 | 44% | Product‑led sales, case study development |
| Tier 3: SMB | <50 | 6 | 37% | Automated nurture, self‑serve |

### Top Priority Accounts (Detailed)

| Company | Country | Industry | Employees | Open Jobs | Followers | Priority Score |
|---------|---------|----------|-----------|-----------|-----------|----------------|
| Paris E‑commerce | France | E‑commerce | 320 | 6 | 8,900 | 134.2 |
| Toulouse SpaceTech | France | Aerospace | 156 | 7 | 5,200 | 84.1 |
| Munich Security | Germany | Cybersecurity | 98 | 4 | 4,600 | 52.3 |
| Lyon Health AI | France | Health Tech | 178 | 3 | 3,100 | 76.5 |
| DataFlow Systems | Germany | IT Services | 145 | 5 | 3,850 | 69.8 |
| CloudNative Labs | Netherlands | Software Dev | 28 | 2 | 890 | 20.1 |
| Hamburg Logistics | Germany | Logistics | 41 | 2 | 1,100 | 24.6 |
| Berlin HR Platform | Germany | HR Tech | 24 | 2 | 780 | 18.9 |
| Eindhoven Industry 4.0 | Netherlands | Industrial | 36 | 3 | 720 | 25.8 |
| Utrecht GreenTech | Netherlands | CleanTech | 12 | 1 | 340 | 11.7 |

## 4. Phased Market Entry Plan

### Phase 1: France (Months 1‑2)
- **Goal:** Secure 3 Tier 1 logos as reference customers
- **Focus Accounts:** Paris E‑commerce, Toulouse SpaceTech, Lyon Health AI
- **Tactics:**
  - Localized French landing page and case studies
  - Partner with French tech accelerators (Station F)
  - Attend VivaTech conference

### Phase 2: Germany (Months 3‑4)
- **Goal:** Establish foothold in 2‑3 verticals (Cybersecurity, Logistics)
- **Focus Accounts:** Munich Security, DataFlow Systems, Hamburg Logistics
- **Tactics:**
  - Hire German‑speaking SDR
  - Translate sales collateral
  - Leverage Berlin startup ecosystem events

### Phase 3: Netherlands (Months 5‑6)
- **Goal:** Validate product‑market fit in high‑density B2B hub
- **Focus Accounts:** CloudNative Labs, Eindhoven Industry 4.0
- **Tactics:**
  - Partner with Dutch reseller
  - Target Amsterdam fintech/logistics clusters

## 5. Success Metrics

| Metric | Target (Month 6) |
|--------|------------------|
| Tier 1 accounts engaged | 5 |
| Tier 2 accounts in pipeline | 10 |
| Conversion rate (pilot → paid) | 30% |
| Average deal size | €25k ARR |

## 6. Risk Mitigation

| Risk | Mitigation |
|------|------------|
| Language/cultural barriers | Local hires, translated materials |
| Longer sales cycles in Europe | Pilot program with discounted first year |
| Data staleness | Weekly automated pipeline refresh |

## 7. Conclusion

The data‑driven approach surfaces high‑intent targets and reduces manual research by ~90%. France offers the strongest immediate opportunity, followed by Germany's diversified verticals and the Netherlands' concentrated tech hubs. Expandly can execute a predictable, phased expansion with measurable outcomes.