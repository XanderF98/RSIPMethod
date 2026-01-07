
# RSIP Method — Resistant Starch & Indigenous Pairing (Execution Demo)

**Role:** Technical Project Manager / Program Manager  
**Focus:** AI-assisted nutrition guidance for low-resource, low-literacy contexts  
**Type:** AI Development · Global Health · Socio-Technical Design  
**Level:** Medium

---

## Overview

In many rural African communities, “avoiding starch” is not realistic—cassava, maize, and yams are the primary calorie sources. The **RSIP Method** (Resistant Starch & Indigenous Pairing) is an AI-assisted approach that **optimizes preparation and pairing of local staples** to blunt glycemic spikes, using culturally relevant foods and constraints.

This project demonstrates an **AI-powered nutrition engine** that:
- Rewards **resistant starch** preparation (e.g., boil → cool → reheat)  
- Recommends **indigenous fiber pairings** (e.g., bitter leaf, baobab, okra)  
- Adapts to **seasonal supply** and **cold-chain limitations**  
- Generates **visual plates** and **audio coaching** for **low-literacy** users

> **Disclaimer:** This is a demonstration of responsible AI for global health. Outputs are **educational** and **not medical advice**.

---

## Why This Project Matters

- **Not a generic calorie counter:** It’s designed for the “next billion” users where Western foods, refrigeration, and continuous glucose monitors aren’t available.
- **Technical sophistication:** Custom RSIP scoring and preparation-aware logic show algorithmic thinking beyond UI “skins.”
- **Empathy-driven design:** The system is built around real constraints (subsistence farming cycles, intermittent power, low literacy) and cultural respect.

---

## Key Features

### Milestone 1 — RSIP Optimization Engine
- **Preparation-Aware Logic:** Adjusts health score based on preparation method; rewards resistant starch workflows (boil → cool ≥12–24h → reheat).  
- **Indigenous Pairing Algorithm:** Suggests local fiber/viscous foods (e.g., okra, baobab, bitter leaf) to **reduce glycemic load (GL)** impact of staples.

### Milestone 2 — Socio-Economic & Geographic Adaptation
- **Seasonal Supply Integration:** Uses region + season metadata (or GPS) to prioritize what’s actually available/affordable.  
- **Cold-Chain Constraints:** Prefers shelf-stable, fermented, or sun-dried options for users without reliable electricity.

### Milestone 3 — Visual Literacy & Accessibility
- **Generative Visual Plates:** Text-light meal visuals showing **portioning and bowl division** using local utensils and food shapes.  
- **Audio-First Coaching:** Text-to-Speech (TTS) in local dialects / simplified English for accessible guidance.

---

## Architecture (High-Level)
client (mobile-first)
├── UX: low-literacy visuals, audio-first prompts
├── Input: region, staple, prep method, constraints (refrigeration, budget)
└── Output: visual plate + audio coaching + simple checklist
backend (or local agent)
├── RSIP Engine
│   ├── Preparation scoring (resistant starch boost)
│   ├── Indigenous pairing recommender (fiber/viscous foods)
│   └── Glycemic load adjustment (context-aware)
├── Context adapters
│   ├── Seasonal supply model (region × harvest calendar)
│   └── Cold-chain constraints (prefer shelf-stable/fermented)
└── Generators
├── Prompted meal guidance (empathetic, non-technical)
└── Visual plate & audio coaching assets

---

## Data & Inputs (Synthetic / Placeholder)

- **User Context:** region/country, language, household size, electricity reliability  
- **Staple Foods:** cassava, maize, yam, plantain, sorghum, millet  
- **Pairing Foods:** okra, bitter leaf, baobab, moringa, groundnuts, beans  
- **Preparation Methods:** boil, cool (≥12–24h), reheat, ferment, pound, roast  
- **Constraints:** budget, markets open days, storage capability, water access

> All data in this repo should be **synthetic** for demonstration. Replace with field-validated datasets only with proper approvals.

---

## Example RSIP Scoring (Pseudo-Logic)

```python
def rsip_score(staple, prep_method, pairings, constraints):
    """
    Returns a health-oriented score for a meal plan, considering resistant starch
    and indigenous pairing. Synthetic demonstration only.
    """
    base_gl = estimate_glycemic_load(staple)  # e.g., cassava high, maize medium, yam medium-high

    # Preparation-aware adjustment (resistant starch boost)
    rs_bonus = 0
    if prep_method in ["boil_cool_24h", "boil_cool_12h_reheat"]:
        rs_bonus = 0.15  # 15% reduction in effective GL (synthetic)

    # Indigenous pairing effect: fiber/viscous foods reduce GL impact
    pairing_effect = 0
    for p in pairings:
        pairing_effect += pairing_gl_modifier(p)  # e.g., okra gel reduces absorption (synthetic)

    # Cold-chain constraint: prioritize shelf-stable/fermented (bonus for feasibility)
    feasibility_bonus = 0.1 if not constraints.get("refrigeration", True) else 0

    # Adjusted GL (bounded for demo)
    adjusted_gl = max(0.0, base_gl * (1 - rs_bonus - pairing_effect))

    # Score combines adjusted GL and feasibility
    score = round((1 / (1 + adjusted_gl)) + feasibility_bonus, 3)  # synthetic scoring
    return score
