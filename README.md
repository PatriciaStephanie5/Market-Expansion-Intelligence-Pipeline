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