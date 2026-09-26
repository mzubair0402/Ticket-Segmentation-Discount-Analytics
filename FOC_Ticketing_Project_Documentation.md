# FOC Ticketing — Power BI Project Documentation

> **Project:** FOC Ticketing  
> **Platform:** Microsoft Power BI  
> **Business Domain:** Intercity Bus Operations / Complimentary & Free-of-Cost Ticket Management  
> **Organization Context:** Daewoo Express Bus Service  
> **Report Pages:** 8  
> **Primary Focus:** FOC ticket quantity, amount, discount, paid amount, ticket category, requester, terminal and time-based analysis.

---

## 1. Executive Summary

**FOC Ticketing** is a Power BI business-intelligence solution for monitoring and analyzing tickets issued through **Free-of-Cost / complimentary ticketing processes**.

The report is not limited to one type of FOC ticket. It separates the ticket population into operational categories:

- Official
- Weekly Rest
- Un-Official
- Police
- Handicap
- Complimentary

The dashboard combines these categories into a management-level summary and then provides dedicated analytical pages for each category.

The model contains a central calculation layer named:

`FOC Measures`

and a dedicated:

`Date Table`

along with category-specific entities.

The report is designed to answer four major questions:

```text
1. How many FOC tickets are being issued?
2. What is the financial value/discount associated with them?
3. Who, where and why are FOC tickets being issued?
4. How is FOC ticket activity changing over time?
```

---

# 2. Business Problem

FOC ticketing represents revenue that may be waived, discounted or otherwise treated differently from normal ticket sales.

For a transport company, uncontrolled FOC ticket issuance can create:

- revenue leakage,
- weak accountability,
- excessive discounts,
- misuse of complimentary privileges,
- unexplained terminal-level differences,
- unusual requester activity,
- difficulty reconciling ticket quantities and financial impact.

A dedicated BI solution is therefore useful for monitoring both:

### Operational volume

```text
Number of FOC tickets
```

and:

### Financial impact

```text
Ticket Amount
Discount
Amount Paid
```

The PBIX addresses this by providing both summary KPIs and category-specific operational analysis.

---

# 3. Project Objectives

## Primary Objective

Build an interactive dashboard to monitor FOC ticket issuance, utilization and financial impact across different ticket categories.

## Secondary Objectives

- Monitor total FOC ticket quantity.
- Monitor total FOC amount.
- Monitor FOC discount.
- Monitor amount paid where applicable.
- Analyze official FOC tickets.
- Analyze weekly-rest tickets.
- Analyze unofficial tickets.
- Analyze police tickets.
- Analyze handicap tickets.
- Analyze complimentary tickets.
- Identify high-volume terminals.
- Identify frequent requesters/employees.
- Analyze reasons for FOC issuance.
- Analyze discount categories.
- Monitor daily/monthly trends.
- Compare different FOC categories.
- Provide year/date filtering.

---

# 4. PBIX Architecture

The report follows a layered analytical structure:

```text
                   FOC TICKETING DATA
                          │
                          ▼
                 Category-specific Tables
                          │
       ┌──────────┬───────┼────────┬───────────┐
       ▼          ▼       ▼        ▼           ▼
    Official   Weekly   Un-      Police     Handicap
               Rest    Official
                          │
                          └──────────────┐
                                         ▼
                                   Complimentary
                                         │
                                         ▼
                                FOC Measures
                                         │
                                         ▼
                                   Date Table
                                         │
                                         ▼
                              Power BI Visual Layer
                                         │
                ┌────────────────────────┼───────────────────────┐
                ▼                        ▼                       ▼
             Summary                Category Analysis        Time Analysis
```

---

# 5. Report Structure

The PBIX contains **8 report pages**.

| # | Page | Purpose |
|---:|---|---|
| 1 | **FOC Table** | Overall FOC ticket quantity, amount and discount trend/detail |
| 2 | **FOC Summary** | Management-level consolidated FOC overview |
| 3 | **Official** | Official FOC ticket analysis |
| 4 | **Weekly Rest** | Weekly-rest ticket analysis |
| 5 | **Un Official** | Unofficial ticket analysis |
| 6 | **Police** | Police ticket analysis |
| 7 | **Handicap** | Handicap ticket analysis |
| 8 | **Complimentary** | Complimentary ticket analysis |

This is a strong report architecture because it provides:

```text
Executive Overview
        ↓
Overall FOC Analysis
        ↓
Category-specific Analysis
```

---

# 6. Semantic Model

The model diagram identifies the following major entities:

```text
                         ┌───────────────┐
                         │   Date Table  │
                         └───────┬───────┘
                                 │
                                 ▼
                         ┌───────────────┐
                         │  FOC Measures │
                         └───────┬───────┘
                                 │
       ┌─────────────┬───────────┼───────────┬─────────────┐
       ▼             ▼           ▼           ▼             ▼
   Official     Weekly Rest   Un-Official  Police       Handicap
                                                             │
                                                             ▼
                                                       Complimentary
```

The PBIX also contains Power BI-generated local date infrastructure used by date hierarchies.

### Confirmed model entities

- `Date Table`
- `FOC Measures`
- `Official`
- `Weekly Rest`
- `Un-Official Tickets`
- `Police`
- `Handicap`
- `Complimentary`

---

# 7. Core Semantic Layer — FOC Measures

`FOC Measures` is the central analytical calculation table.

It contains measures covering:

### Overall FOC

- `FOC Quantity`
- `FOC Discount`
- `FOC Amount`

### Category ticket quantities

- `Official Tickets Total Quantity`
- `Weekly Rest Tickets Total Quantity`
- `Un-Official Tickets Total Quantity`
- `Police Tickets Total Quantity`
- `Handicap Tickets Total Quantity`
- `Complimentary Tickets Total Quantity`

### Category financial measures

- `Official Tickets Total Amount`
- `Weekly Rest Tickets Total Amount`
- `Un-Official Tickets Total Amount`
- `Police Tickets Total Amount`
- `Handicap Tickets Total Amount`
- `Complimentary Tickets Total Amount`

### Category discount/paid measures

Confirmed through visual references:

- `Police Tickets Discount`
- `Police Tickets Amount Paid`
- `Police Discount %`
- `Handicap Tickets Discount`
- `Handicap Tickets Amount Paid`
- `Handicap Discount %`
- `Complimentary Tickets Discount`
- `Complimentary Tickets Amount Paid`
- `Complimentary Discount %`

This centralized measure layer is one of the strongest technical aspects of the model.

---

# 8. KPI Dictionary

## 8.1 FOC Quantity

**Measure:** `FOC Measures[FOC Quantity]`

### Business meaning

Total quantity of FOC tickets under the current filter context.

### Key uses

- executive KPI,
- trend analysis,
- overall FOC monitoring.

---

## 8.2 FOC Discount

**Measure:** `FOC Measures[FOC Discount]`

### Business meaning

Total discount/revenue waiver associated with FOC tickets.

### Management significance

This is a critical financial-impact metric.

A high ticket count is not necessarily problematic by itself; the **financial value of the discount** is what quantifies the revenue impact.

---

## 8.3 FOC Amount

**Measure:** `FOC Measures[FOC Amount]`

Represents the FOC-related ticket amount/value under the active filter context.

Used in:

- FOC Table,
- FOC Summary,
- KPI cards.

---

# 9. Official Ticket KPIs

Confirmed measures:

- `Official Tickets Total Quantity`
- `Official Tickets Total Amount`

The Official page uses these measures to analyze:

- total official FOC tickets,
- terminal distribution,
- requester distribution,
- reason distribution,
- time trend.

---

# 10. Weekly Rest Ticket KPIs

Confirmed measures:

- `Weekly Rest Tickets Total Quantity`
- `Weekly Rest Tickets Total Amount`

This category is specifically analyzed by:

- reason,
- requester,
- terminal,
- time,
- year.

This suggests a dedicated employee/staff benefit or rest-related ticketing workflow.

---

# 11. Un-Official Ticket KPIs

Confirmed measures:

- `Un-Official Tickets Total Quantity`
- `Un-Official Tickets Total Amount`

The Un Official page provides:

- employee-level analysis,
- terminal analysis,
- daily/monthly analysis,
- trend analysis,
- KPI summary.

The presence of `Employee Name` is particularly useful for accountability and anomaly detection.

---

# 12. Police Ticket KPIs

Confirmed measures:

- `Police Tickets Total Quantity`
- `Police Tickets Total Amount`
- `Police Tickets Discount`
- `Police Tickets Amount Paid`
- `Police Discount %`

This page has a stronger financial-control orientation because it distinguishes:

```text
Total Amount
      ↓
Discount
      ↓
Amount Paid
      ↓
Discount %
```

---

# 13. Handicap Ticket KPIs

Confirmed measures:

- `Handicap Tickets Total Quantity`
- `Handicap Tickets Total Amount`
- `Handicap Tickets Discount`
- `Handicap Tickets Amount Paid`
- `Handicap Discount %`

The Handicap page therefore measures both ticket utilization and the financial value of the concession.

---

# 14. Complimentary Ticket KPIs

Confirmed measures:

- `Complimentary Tickets Total Quantity`
- `Complimentary Tickets Total Amount`
- `Complimentary Tickets Discount`
- `Complimentary Tickets Amount Paid`
- `Complimentary Discount %`

The page also analyzes:

- terminal,
- requester,
- discount category,
- date.

---

# 15. Page 1 — FOC Table

## Purpose

The **FOC Table** page provides detailed overall FOC performance.

### Confirmed visual types

- Line chart
- KPI/card visual
- Table
- Year slicer
- Date slicers
- Layout shapes/text

### Line chart

Measures:

- Official Tickets Total Quantity
- Weekly Rest Tickets Total Quantity
- Un-Official Tickets Total Quantity
- Police Tickets Total Quantity
- Handicap Tickets Total Quantity
- Complimentary Tickets Total Quantity

Axis:

`Date Table[Date]`

### Business question

> How are the different FOC ticket categories changing over time?

This is the primary **category trend comparison** in the report.

---

## FOC KPI Card

The card contains:

- FOC Quantity
- FOC Discount
- FOC Amount

This gives management a compact view of the overall FOC financial and operational footprint.

---

## FOC Detail Table

The table contains:

- FOC Amount
- FOC Quantity
- FOC Discount
- Date

This supports detailed time-based review.

---

# 16. Page 2 — FOC Summary

## Purpose

The **FOC Summary** page is the executive-level overview.

### Confirmed visuals

- Column chart
- Table
- KPI/card
- Year slicer
- Date slicers
- Layout elements

### Category comparison chart

The chart compares:

- Official
- Weekly Rest
- Un-Official
- Police
- Handicap
- Complimentary

using ticket quantities.

This is the most direct view of **FOC mix**.

---

## Summary KPI

The card contains:

- FOC Quantity
- FOC Discount
- FOC Amount

### Management interpretation

A manager can quickly determine:

```text
How many FOC tickets?
+
What financial value?
+
What discount impact?
```

---

# 17. Page 3 — Official

## Purpose

Dedicated analysis of official FOC tickets.

### Visual structure

The page contains:

- Bar chart
- Donut chart
- Bar chart
- Column chart
- KPI card
- Date/year slicers

---

## 17.1 Official Tickets by Terminal

Dimension:

`Official[Terminals]`

Measure:

`Official Tickets Total Quantity`

### Question

> Which terminals issue the most official FOC tickets?

---

## 17.2 Official Tickets by Reason

Dimension:

`Official[Reason]`

Measure:

`Official Tickets Total Quantity`

Visual:

Donut chart

### Question

> Why are official FOC tickets being issued?

---

## 17.3 Official Tickets by Requester

Dimension:

`Official[Requester Name]`

Measure:

`Official Tickets Total Quantity`

### Question

> Which requesters are responsible for the highest official FOC ticket activity?

---

## 17.4 Official Trend

Dimension:

`Date Table[Date]`

Measure:

`Official Tickets Total Quantity`

### Question

> How is official FOC ticket activity changing over time?

---

# 18. Page 4 — Weekly Rest

## Purpose

Dedicated analysis of weekly-rest FOC tickets.

### Visuals

- Donut chart
- Bar chart
- Column chart
- Bar chart
- KPI card
- Date/year filters

---

## 18.1 Weekly Rest by Reason

Dimension:

`Weekly Rest[Reason]`

Measure:

`Weekly Rest Tickets Total Quantity`

---

## 18.2 Weekly Rest by Requester

Dimension:

`Weekly Rest[Requester Name]`

Measure:

`Weekly Rest Tickets Total Quantity`

---

## 18.3 Weekly Rest by Date

Measure:

`Weekly Rest Tickets Total Quantity`

Axis:

`Date Table[Date]`

---

## 18.4 Weekly Rest by Terminal

Dimension:

`Weekly Rest[Terminals]`

Measure:

`Weekly Rest Tickets Total Quantity`

---

## Weekly Rest KPI

- Weekly Rest Tickets Total Quantity
- Weekly Rest Tickets Total Amount

---

# 19. Page 5 — Un Official

## Purpose

Dedicated analysis of unofficial FOC tickets.

### Visuals

- Bar chart
- Column chart
- Bar chart
- Line chart
- KPI card
- Date/year slicers

---

## 19.1 Unofficial Tickets by Employee

Dimension:

`Un-Official Tickets[Employee Name]`

Measure:

`Un-Official Tickets Total Quantity`

### Business purpose

Supports employee-level monitoring and accountability.

---

## 19.2 Unofficial Tickets by Terminal

Dimension:

`Un-Official Tickets[Terminals]`

Measure:

`Un-Official Tickets Total Quantity`

---

## 19.3 Unofficial Daily/Monthly Trend

Measure:

`Un-Official Tickets Total Quantity`

Axis:

`Date Table[Date]`

The page contains both column and line trend visuals.

---

# 20. Page 6 — Police

## Purpose

Dedicated analysis of FOC tickets associated with police-related issuance.

### Visuals

- Bar chart
- Column chart
- Line chart
- KPI card
- Date/year slicers

---

## 20.1 Police Tickets by Terminal

Dimension:

`Police[Terminals]`

Measure:

`Police Tickets Total Quantity`

---

## 20.2 Police Ticket Trend

Measure:

`Police Tickets Total Quantity`

Axis:

`Date Table[Date]`

---

## 20.3 Police Financial KPI

The KPI card contains:

- Police Tickets Total Quantity
- Police Tickets Total Amount
- Police Tickets Discount
- Police Tickets Amount Paid
- Police Discount %

This provides a complete financial concession view.

---

# 21. Page 7 — Handicap

## Purpose

Dedicated analysis of handicap-related FOC tickets.

### Visuals

- Bar chart
- Column chart
- Line chart
- KPI card
- Date/year slicers

---

## 21.1 Handicap Tickets by Terminal

Dimension:

`Handicap[Terminals]`

Measure:

`Handicap Tickets Total Quantity`

---

## 21.2 Handicap Trend

Measure:

`Handicap Tickets Total Quantity`

Axis:

`Date Table[Date]`

---

## 21.3 Handicap Financial KPI

Measures:

- Handicap Tickets Total Quantity
- Handicap Tickets Total Amount
- Handicap Tickets Discount
- Handicap Tickets Amount Paid
- Handicap Discount %

This provides both social-benefit utilization and financial impact monitoring.

---

# 22. Page 8 — Complimentary

## Purpose

Dedicated analysis of general complimentary ticket issuance.

### Visuals

- Bar chart
- Column chart
- Bar chart
- Donut chart
- KPI card
- Date/year slicers

---

## 22.1 Complimentary Tickets by Terminal

Dimension:

`Complimentary[Terminals]`

Measure:

`Complimentary Tickets Total Quantity`

---

## 22.2 Complimentary Tickets by Requester

Dimension:

`Complimentary[Requester Name]`

Measure:

`Complimentary Tickets Total Quantity`

---

## 22.3 Complimentary Trend

Dimension:

`Date Table[Date]`

Measure:

`Complimentary Tickets Total Quantity`

---

## 22.4 Complimentary by Discount Category

Dimension:

`Complimentary[Discount Category]`

Measure:

`Complimentary Tickets Total Quantity`

### Business question

> How are complimentary tickets distributed across discount categories?

---

# 23. Date and Time Intelligence

The report uses:

`Date Table`

and Power BI's local date hierarchy.

Confirmed date hierarchy usage includes:

- Year
- Month
- Date

This supports:

```text
Year
 ↓
Month
 ↓
Day
```

The report has synchronized date/year slicer patterns across pages.

The visual configuration also shows a stored **2026 year context** in the report layout.

---

# 24. Filter Architecture

The recurring filter structure across the report includes:

### Year

Used to select reporting year.

### Date

Used to filter the detailed reporting period.

### Month

Used in some page-level date filtering.

The category-specific pages additionally expose dimensions such as:

- Terminal
- Requester
- Reason
- Employee
- Discount Category

depending on the ticket type.

---

# 25. Analytical Dimensions

The project supports multiple analytical dimensions.

| Dimension | Business Use |
|---|---|
| Date | Trend / period analysis |
| Year | Annual comparison |
| Month | Monthly monitoring |
| Terminal | Location performance |
| Requester | Accountability |
| Employee | Unofficial ticket monitoring |
| Reason | Purpose of issuance |
| Discount Category | Complimentary classification |
| FOC Category | Overall mix |

---

# 26. FOC Category Framework

The report's central classification is:

```text
FOC Tickets
│
├── Official
├── Weekly Rest
├── Un-Official
├── Police
├── Handicap
└── Complimentary
```

This classification is valuable because different FOC categories may have different:

- authorization rules,
- business justification,
- financial implications,
- monitoring requirements.

---

# 27. Financial-Control Framework

The strongest financial-control component of the project is the use of:

```text
Ticket Quantity
       │
       ▼
Total Amount
       │
       ▼
Discount
       │
       ▼
Amount Paid
       │
       ▼
Discount %
```

This is particularly visible on:

- Police
- Handicap
- Complimentary

pages.

It allows management to evaluate not only the **number of tickets**, but also the **financial concession associated with them**.

---

# 28. Recommended KPI Framework

A mature FOC management dashboard should group KPIs into four layers.

## Volume

- Total FOC Tickets
- Official Tickets
- Weekly Rest Tickets
- Unofficial Tickets
- Police Tickets
- Handicap Tickets
- Complimentary Tickets

## Financial

- Total FOC Amount
- Total Discount
- Amount Paid
- Average Ticket Value

## Control

- Discount %
- Ticket share %
- Terminal share %
- Requester share %

## Trend

- MoM Growth %
- YoY Growth %
- YTD Quantity
- YTD Discount
- YTD Financial Impact

---

# 29. Recommended Advanced KPIs

## 29.1 FOC Share of Total Ticket Sales

If normal ticket sales are available:

```text
FOC Ticket Share % =
FOC Tickets / Total Tickets
```

This would quantify how significant FOC activity is relative to the entire ticketing operation.

---

## 29.2 FOC Revenue Impact

```text
FOC Revenue Impact =
FOC Discount / Total Potential Sales
```

This helps management understand the actual financial opportunity cost.

---

## 29.3 Average FOC Ticket Value

```text
Average FOC Value =
FOC Amount / FOC Quantity
```

This can identify categories with unusually high ticket value.

---

## 29.4 Average Discount per Ticket

```text
Average Discount =
FOC Discount / FOC Quantity
```

This is useful for detecting categories where each FOC ticket has a high financial concession.

---

# 30. Recommended Control Analytics

Because FOC ticketing is a potential revenue-control area, the following analytics would significantly strengthen the solution.

### Top Requesters

Rank requesters by:

```text
FOC Quantity
FOC Discount
FOC Amount
```

### Top Terminals

Rank terminals by:

```text
FOC Quantity
FOC Amount
Discount
```

### High-Value Requests

Identify tickets with:

```text
High Ticket Amount
High Discount
```

### Unusual Activity

Detect:

- sudden requester spikes,
- unusual terminal spikes,
- abnormal daily FOC volume,
- high discount percentage,
- repeated requests,
- unusually high unofficial ticket activity.

---

# 31. Recommended FOC Governance Dashboard

A future governance page could be:

```text
┌──────────────────────────────────────────────────────┐
│              FOC GOVERNANCE OVERVIEW                  │
├──────────┬──────────┬──────────┬──────────┬──────────┤
│ FOC Qty  │ FOC Value│ Discount │ Avg Disc │ FOC Share│
├──────────┴──────────┴──────────┴──────────┴──────────┤
│                                                      │
│ FOC Trend                    Discount Trend           │
│                                                      │
├──────────────────────────────┬───────────────────────┤
│ Terminal Ranking             │ Requester Ranking     │
│                              │                       │
├──────────────────────────────┴───────────────────────┤
│ High-Risk / Exception Tickets                         │
└──────────────────────────────────────────────────────┘
```

---

# 32. Recommended Exception Monitoring

Create a dedicated exception table containing:

| Exception | Example Logic |
|---|---|
| High FOC Volume | Above selected threshold |
| High Discount | Discount above threshold |
| High Requester Activity | Requester above normal baseline |
| High Terminal Activity | Terminal above normal baseline |
| Unofficial Spike | Unofficial tickets above expected level |
| High Discount % | Discount % above threshold |
| Duplicate Request | Same requester/date/category pattern |
| Weekend/Off-Hours | Ticket issued outside normal rules |

---

# 33. Data Quality Recommendations

A production version should add a Data Quality page.

Recommended checks:

### Completeness

- Missing date
- Missing terminal
- Missing requester
- Missing reason
- Missing ticket category

### Validity

- Invalid ticket category
- Invalid terminal
- Invalid requester
- Invalid discount category

### Financial consistency

```text
Amount Paid > Total Amount
Discount > Total Amount
Discount % > 100%
Negative Amount
Negative Quantity
```

### Duplicate control

- Duplicate ticket ID
- Duplicate requester/date/category combination
- Duplicate transaction reference

---

# 34. Data Model Improvement Recommendations

The current category-specific entities are understandable for reporting, but a more scalable enterprise model would ideally use a **single FOC fact table** with a category dimension.

### Current conceptual structure

```text
Official
Weekly Rest
Un-Official
Police
Handicap
Complimentary
```

### Recommended future structure

```text
                    Dim Date
                       │
                       ▼
Dim Terminal ───► Fact FOC Ticket ◄─── Dim Requester
                       │
                       ▼
                 Dim FOC Category
                       │
                       ▼
                 Dim Reason/Type
```

The fact table could contain:

- Ticket ID
- Date
- Terminal
- Requester
- FOC Category
- Reason
- Discount Category
- Ticket Quantity
- Ticket Amount
- Discount
- Amount Paid

This would simplify:

- DAX,
- filtering,
- cross-category comparison,
- data governance,
- maintenance,
- future analytics.

---

# 35. Recommended Star Schema

```text
                 ┌──────────────┐
                 │  Dim Date    │
                 └──────┬───────┘
                        │
                        ▼
┌──────────────┐  ┌───────────────┐  ┌────────────────┐
│ Dim Terminal │──│ Fact FOC      │──│ Dim Requester  │
└──────────────┘  │ Ticket        │  └────────────────┘
                  │               │
                  │ Quantity      │
                  │ Amount        │
                  │ Discount      │
                  │ Amount Paid   │
                  └───────┬───────┘
                          │
                          ▼
                  ┌───────────────┐
                  │Dim FOC Category│
                  └───────────────┘
```

This would be the recommended enterprise architecture for future versions.

---

# 36. Visualization Assessment

The report makes good use of multiple visual types.

| Visual | Primary Use |
|---|---|
| KPI/Card | Management summary |
| Bar Chart | Terminal/requester ranking |
| Column Chart | Time/category comparison |
| Line Chart | Trend analysis |
| Donut Chart | Reason/category composition |
| Table | Detailed review |
| Slicer | User-driven filtering |

The visual structure is consistent across category pages, making the report easy to navigate.

---

# 37. Dashboard UX Assessment

### Strengths

- Consistent page structure.
- Repeated date/year filtering.
- Dedicated category pages.
- KPI cards near the top.
- Mix of executive and detailed visuals.
- Clear separation between FOC categories.
- Multiple analytical dimensions.

### Potential improvements

- Add explicit page navigation menu.
- Add KPI definitions/tooltips.
- Add dynamic titles based on selected filters.
- Add conditional formatting to exception tables.
- Add drill-through to ticket-level details.
- Add bookmarks for executive vs operational views.
- Add tooltip pages for requester/terminal analysis.

---

# 38. Drill-Through Recommendation

A future version should include a ticket-level drill-through page.

Example:

```text
FOC Category
     ↓
Terminal
     ↓
Requester
     ↓
Ticket
     ↓
Transaction Detail
```

Recommended drill-through fields:

- Ticket ID
- Date
- Terminal
- Requester
- Category
- Reason
- Quantity
- Amount
- Discount
- Amount Paid

---

# 39. Management Questions Answered

## Overall

- How many FOC tickets were issued?
- What is the total FOC value?
- What is the total discount?

## Category

- Which FOC category has the highest volume?
- Which category has the highest financial impact?
- Which category is growing fastest?

## Terminal

- Which terminals issue the most FOC tickets?
- Which terminals have the highest FOC value?

## Requester

- Who requests the most FOC tickets?
- Are there unusual requester patterns?

## Reason

- Why are FOC tickets being issued?
- Which reasons dominate each category?

## Trend

- What is the daily/monthly FOC trend?
- Are FOC tickets increasing?

## Financial

- How much is being discounted?
- What percentage is discounted?
- What amount is actually paid?

---

# 40. Business Impact

The dashboard creates a control-oriented analytical workflow:

```text
FOC Ticket Issuance
        ↓
Quantity Monitoring
        ↓
Category Analysis
        ↓
Terminal Analysis
        ↓
Requester Analysis
        ↓
Reason Analysis
        ↓
Financial Impact
        ↓
Exception Identification
        ↓
Management Action
```

This can help management monitor FOC activity and identify areas requiring additional review.

---

# 41. Project Strengths

## 41.1 Category-Specific Reporting

Separating:

- Official
- Weekly Rest
- Un-Official
- Police
- Handicap
- Complimentary

makes the dashboard operationally meaningful.

---

## 41.2 Centralized Measures

`FOC Measures` provides a clean semantic calculation layer.

---

## 41.3 Financial and Operational KPIs

The project combines:

```text
Quantity + Amount + Discount + Paid Amount
```

rather than only counting tickets.

---

## 41.4 Requester-Level Accountability

Several pages include requester/employee analysis.

This is highly valuable for operational control.

---

## 41.5 Terminal-Level Accountability

Terminal-level charts allow location benchmarking.

---

## 41.6 Time-Based Monitoring

The Date Table supports daily/monthly trend analysis.

---

# 42. Potential Weaknesses

## 42.1 Category-Specific Fact Tables

Maintaining separate category entities can become difficult as the number of FOC types increases.

### Recommendation

Move toward a unified FOC fact table with a category dimension.

---

## 42.2 Limited Exception Monitoring

The current report is primarily descriptive.

A future version should include:

- anomaly detection,
- threshold alerts,
- exception tables,
- high-risk requester detection.

---

## 42.3 Limited Financial Ratios

The model has discount percentages for some categories, but the dashboard could benefit from standardized metrics across all categories.

---

## 42.4 No Explicit SLA/Authorization Layer

If approval or authorization timestamps exist, add:

- approval status,
- approver,
- approval time,
- SLA,
- exception reason.

---

# 43. Recommended Future-State Architecture

```text
                Source Ticketing System
                         │
                         ▼
                  Power Query / ETL
                         │
                         ▼
                  Fact FOC Ticket
                         │
        ┌────────────────┼────────────────┐
        ▼                ▼                ▼
    Dim Date        Dim Terminal     Dim Requester
        │
        ▼
 Dim FOC Category
        │
        ▼
     DAX KPI Layer
        │
        ├── Volume KPIs
        ├── Financial KPIs
        ├── Discount KPIs
        ├── YoY KPIs
        └── Exception KPIs
        │
        ▼
      Power BI
        │
   ┌────┼─────────┐
   ▼    ▼         ▼
Executive Ops   Governance
```

---

# 44. GitHub Repository Structure

Recommended repository:

```text
foc-ticketing-powerbi/
│
├── README.md
│
├── PowerBI/
│   └── FOC Ticketing.pbix
│
├── Documentation/
│   ├── Project_Documentation.md
│   ├── Data_Model.md
│   ├── KPI_Dictionary.md
│   ├── Business_Logic.md
│   └── Dashboard_Guide.md
│
├── DAX/
│   ├── FOC_Measures.md
│   ├── Category_Measures.md
│   ├── Financial_Measures.md
│   └── Time_Intelligence.md
│
├── PowerQuery/
│   └── Queries.md
│
├── Screenshots/
│   ├── foc-table.png
│   ├── foc-summary.png
│   ├── official.png
│   ├── weekly-rest.png
│   ├── un-official.png
│   ├── police.png
│   ├── handicap.png
│   └── complimentary.png
│
└── DataModel/
    └── FOC_Model.png
```

---

# 45. GitHub README Project Description

```markdown
# FOC Ticketing Analytics — Power BI

An interactive Power BI analytics solution developed to monitor
Free-of-Cost (FOC) ticket issuance, operational volume and financial impact
across multiple ticket categories.

## Key Analysis

- FOC ticket quantity
- FOC amount
- FOC discount
- Amount paid
- Official tickets
- Weekly Rest tickets
- Un-Official tickets
- Police tickets
- Handicap tickets
- Complimentary tickets
- Terminal analysis
- Requester/employee analysis
- Reason analysis
- Discount category analysis
- Daily/monthly trends

## Technology

- Microsoft Power BI
- DAX
- Power Query
- Data Modeling
- Time Intelligence
- Data Visualization

## Business Domain

Transportation / Ticketing / Revenue Control / Operations Analytics
```

---

# 46. Portfolio / CV Description

### Detailed Portfolio Description

> **FOC Ticketing Analytics Dashboard — Power BI:** Developed an 8-page Power BI business intelligence solution for monitoring Free-of-Cost ticket issuance across Official, Weekly Rest, Un-Official, Police, Handicap and Complimentary categories. Built a centralized DAX measure layer for ticket quantity, ticket value, discount, amount paid and discount percentage, with interactive terminal, requester, reason, category and date analysis. The solution provides management-level FOC monitoring as well as category-specific operational analysis.

### Short CV Version

> Developed an 8-page Power BI FOC Ticketing Analytics Dashboard covering ticket volume, financial impact, discounts, terminal/requester analysis and category-wise trends using DAX, data modeling and interactive Power BI visualization.

---

# 47. Skills Demonstrated

## Power BI

- Multi-page dashboard design
- Interactive reporting
- Slicers
- KPI cards
- Tables
- Bar charts
- Column charts
- Line charts
- Donut charts
- Business intelligence reporting

## DAX

- Centralized measure architecture
- Ticket quantity measures
- Financial measures
- Discount measures
- Percentage measures
- Category-specific measures

## Data Modeling

- Central measure table
- Date dimension
- Category entities
- Terminal dimensions
- Requester dimensions
- Time hierarchy

## Business Analysis

- Revenue control
- FOC monitoring
- Operational accountability
- Terminal benchmarking
- Requester analysis
- Financial impact analysis
- Exception identification

---

# 48. Project Maturity Assessment

| Area | Assessment |
|---|---|
| Power BI Reporting | **Strong** |
| Dashboard Architecture | **Strong** |
| KPI Layer | **Strong** |
| Category Analysis | **Strong** |
| Terminal Analysis | **Strong** |
| Requester Analysis | **Good** |
| Financial Analysis | **Strong** |
| Time Analysis | **Good** |
| Data Modeling | **Good** |
| Exception Monitoring | Opportunity |
| SLA/Authorization Analytics | Opportunity |
| Predictive Analytics | Not evident |
| Automated Alerts | Not evident |
| Overall Level | **Intermediate–Advanced BI Reporting** |

---

# 49. Recommended Next-Level Features

To make this project significantly stronger for a professional portfolio, add:

### Level 1 — KPI enhancement

- FOC Share %
- Average FOC Value
- Average Discount/Ticket
- YoY Growth %
- MoM Growth %
- YTD FOC Quantity
- YTD Discount

### Level 2 — Control

- Top 10 Requesters
- Top 10 Terminals
- High-value FOC tickets
- High-discount tickets
- Exception dashboard

### Level 3 — Governance

- Approval workflow
- Approver analysis
- Authorization status
- SLA
- Aging
- Duplicate detection

### Level 4 — AI/Advanced Analytics

- Anomaly detection
- Expected FOC volume
- Requester risk score
- Terminal risk score
- Forecast FOC volume
- Automated management alerts

---

# 50. Final Assessment

**FOC Ticketing** is a strong Power BI operations/revenue-control project.

Its most valuable characteristics are:

1. **Eight-page structured reporting architecture**
2. **Centralized `FOC Measures` semantic layer**
3. **Dedicated Date Table**
4. **Six distinct FOC business categories**
5. **Terminal-level analysis**
6. **Requester/employee accountability**
7. **Reason-based analysis**
8. **Financial impact monitoring**
9. **Discount and amount-paid KPIs**
10. **Daily/monthly trend analysis**

The project is particularly strong for demonstrating:

> **Power BI + DAX + Data Modeling + Operations Analytics + Revenue Control**

The biggest opportunity is to move from descriptive reporting toward **FOC governance and anomaly detection**.

The ideal future-state product would answer not only:

> "How many FOC tickets were issued?"

but also:

> "Who issued them, where, why, at what financial impact, whether the activity is normal, and which transactions require management review?"

---

# 51. Technical Documentation Note

This documentation is based on the report/layout/model metadata available inside the uploaded PBIX.

### Directly confirmed from the PBIX

- 8 report pages
- Model entities
- Visual types
- Visual fields
- KPI/measure names
- Date hierarchy usage
- Category-specific analytical structure
- Terminal/requester/reason dimensions
- Financial measures
- Report-level year context
- Theme/resource metadata

### Not safely reconstructed

- Complete Power Query M scripts
- Complete source-system connection definitions
- Exact DAX expression of every measure
- Full physical column metadata
- Raw transaction-level values

The internal Power BI `DataModel` is stored in Microsoft's compressed format. Therefore, unavailable formulas/source logic have intentionally **not been fabricated**.

---

## Project Classification

**Business Intelligence / Transportation Analytics / FOC Ticketing / Revenue Control**

### Technology Stack

```text
Power BI
   │
   ├── DAX
   ├── Power Query
   ├── Data Modeling
   ├── Time Intelligence
   └── Data Visualization
```

### End-to-End Outcome

```text
FOC Ticket Data
      ↓
Category-specific Model
      ↓
Central DAX Measure Layer
      ↓
KPI + Financial Analysis
      ↓
Terminal / Requester / Reason Analysis
      ↓
Time-Series Monitoring
      ↓
Management Control & Decision Making
```
