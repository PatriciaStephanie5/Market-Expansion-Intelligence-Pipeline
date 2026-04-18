# Market Expansion Intelligence Pipeline – Expandly (Series B SaaS)
[![Tableau](https://img.shields.io/badge/Tableau-2024.1-blue)] (https://public.tableau.com/app/profile/timba.patricia.stephanie/viz/MarketExpansionDashboard_17760155743840/Dashboard1)
[![Make](https://img.shields.io/badge/Make-Automation-6D4AFF)](https://eu1.make.com/1318783/scenarios/5239545/logs/7fca548743284c38b6a9c1495f19492f?showCheckRuns=true&showChangeLog=true)

**Freelance GTM Data Analyst and Clay & Data Specialist Project**  
**Q4 2024 | Delivered via Freelancer.com**

Automated market intelligence pipeline that scraped, enriched, and tiered YC SaaS startups across Germany, France, and the Netherlands.

### Business Impact
- Reduced manual research time from 3 weeks to **4 hours per week**
- Delivered weekly prioritized target lists with full firmographic enrichment
- Supported data-driven expansion into **three new European markets**
- Created interactive Tableau dashboard used for sales prioritization

### Project Overview
Built a fully automated pipeline using Apify + Make + Python that delivered production-ready, Clay-compatible datasets for international market expansion.

### STAR Story

**Situation**: Expandly’s growth team lacked clean, enriched data for new European markets.  
**Task**: Create a repeatable weekly intelligence system with geographic heatmaps and priority scoring.  
**Action**: Automated scraping, enrichment, tiering, and Tableau visualization.  
**Result**: 3-week manual process reduced to 4 hours/week with actionable insights.

### Tech Stack
- **Apify** + **Make** – Scraping & automation  
- **Python** – Data processing & JSON formatting  
- **Tableau** – Geographic heatmaps & prioritization dashboard  
- **Clay-ready exports** – For seamless CRM import

## Technical Architecture

| Stage | Tool | Purpose |
|-------|------|---------|
| **Data Collection** | Apify Y Combinator Scraper | Extract YC‑backed startups by location |
| **Data Enrichment** | Apify LinkedIn Company Scraper (simulated) | Add employee count, industry, follower data |
| **Automation** | Make (formerly Integromat) | Parse JSON → Google Sheets (weekly schedule) |
| **Visualization** | Tableau Public | Interactive dashboard with map, tiers, priority scoring |


## Key Features

- **Geographic Mapping:** Visualize company locations sized by employee count
- **Tier Segmentation:** Auto‑categorize as Enterprise / Mid‑Market / SMB
- **Priority Scoring:** Weighted algorithm combining size, hiring activity, and social presence
- **Interactive Filters:** Drill down by country, tier, and industry
- **Live Google Sheets Connection:** Tableau refreshes on schedule

## Make Automation Workflow

The Make scenario runs weekly to:
1. Parse the YC + LinkedIn JSON dataset
2. Append each company record to Google Sheets
3. Maintain a clean, up‑to‑date master list for Tableau

**Blueprint:** `workflows/make_scenario_blueprint.json`

## Tableau Dashboard

### Dashboard Components

| Sheet | Description |
|-------|-------------|
| **Market Map** | Geographic distribution with company size bubbles |
| **Tier by Country** | Stacked bar chart of Enterprise/Mid‑Market/SMB distribution |
| **Industry Heatmap** | Concentration of industries per country |
| **Priority Targets** | Ranked list with Priority Score for sales focus |

### Calculated Fields

tableau
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

### How to Explore This Repo
1. `Master_target_list.csv` – Final enriched dataset  
2. `integration JSON.blueprint.json` – Make automation workflow  
3. `MarketExpansionDashboard.twbx` – Tableau workbook  
4. Live Dashboard: [Market Expansion Dashboard] (https://public.tableau.com/app/profile/timba.patricia.stephanie/viz/MarketExpansionDashboard_17760155743840/Dashboard1)

**Client**: Expandly (Series B SaaS)  
**Role**: Freelance GTM Data Analyst and Clay & Data Specialist  
**Date**: Q4 2024


---

### Acknowledgments

- Data scraped using Y Combinator actor on APIfy and LinkedIn public information
- Built with [Make](https://www.make.com) and [Tableau Public](https://public.tableau.com)
- Special thanks to the Apify and Octoparse communities for 
scraping resources 

---

Built by **Timba Patricia Stephanie**  
GTM Data Analyst and Clay & Data Specialist | Open to remote roles.
