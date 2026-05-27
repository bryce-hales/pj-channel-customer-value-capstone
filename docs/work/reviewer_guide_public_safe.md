# Public-Safe Reviewer Guide

This guide explains the public capstone package and the boundary between shareable deliverables and private working files.

## Public Safety Boundary

The final public-facing package uses only aggregate outputs, sanitized documentation, and reviewed screenshots. Record-level source exports and record-level working datasets are intentionally excluded from this repository.

`data/processed/customer_value_dataset.csv` was regenerated locally and contains 9,021 customer-level rows. It is local-only and is not part of the public package.

Screenshots should be reviewed before public release. If a screenshot shows record-level details, leave it out or mark it internal-only.

## Safe Aggregate Outputs

The following Tableau package files are aggregate-only and intended for school/public presentation use:

- `tableau_exports/tableau_headline_channel_kpis.csv`
- `tableau_exports/tableau_headline_monthly_trends.csv`
- `tableau_exports/tableau_headline_value_distribution.csv`
- `tableau_exports/tableau_channel_eligibility_overview.csv`
- `tableau_exports/tableau_channel_eligibility_detail.csv`
- `tableau_exports/tableau_chart_recommendations.csv`
- `tableau_exports/tableau_export_manifest.csv`
- `tableau_exports/tableau_data_dictionary.csv`

Other aggregate summary files in `output/tables/` can be reviewed for school-safe use when they contain only grouped counts, rates, validation summaries, or chart-planning outputs. Monthly value and rate metrics suppress channel-month cells under 5 customers.

## Local-Only / Internal Files

Treat the following as local-only or internal unless separately reviewed and sanitized:

- Source exports under local data folders
- Intermediate working data
- Customer-level processed datasets, especially `customer_value_dataset.csv`
- Screenshots that show record-level details or internal-only dashboard data

## Script List

### `python/06_validate_hubspot_shopify_match.py`

Validates how well Shopify customer records match HubSpot contacts. This script supports the decision to use HubSpot as the main customer-source bridge. Outputs are aggregate validation summaries.

### `python/07_build_hubspot_source_mapping.py`

Builds a source mapping layer from HubSpot fields into more usable source/channel labels. This helps translate CRM source values into analysis-ready acquisition groups.

### `python/09_build_customer_value_dataset.py`

Builds the local customer-level value dataset by combining Shopify customer/order/order-line behavior with source/channel context. The resulting `customer_value_dataset.csv` is local-only and not part of the public package.

### `python/10_validate_salesforce_shopify_match.py`

Compares Salesforce CRM records with Shopify context for validation and enrichment. This is supporting validation, not the primary attribution source.

### `python/11_validate_salesforce_opportunity_order_summary.py`

Creates directional Salesforce opportunity/order validation summaries. It helps confirm PJ order and revenue context and supports validation of the Salesforce Shop URL.

### `python/12_validate_ga4_exports.py`

Validates GA4 export files at an aggregate level. GA4 is used as a marketing-platform validation layer only because exports can overlap and should not be treated as deduplicated totals.

### `python/13_build_channel_eligibility.py`

Classifies derived channel groups into headline eligible, directional/supporting, excluded, or needs-review classes. This script prevents system, sync, technical, imported, and unclassified buckets from driving headline acquisition recommendations.

### `python/14_build_eda_chart_tables.py`

Builds aggregate EDA chart-planning tables, including headline channel KPIs, monthly trends, value distribution, and chart recommendation inputs.

### `python/15_build_eda_findings_summary.py`

Writes a concise methodology/findings summary from the aggregate EDA outputs. This supports report and presentation documentation.

### `python/16_build_tableau_export_package.py`

Packages aggregate CSVs for Tableau, including KPI, monthly trend, value distribution, eligibility, recommendation, manifest, and data dictionary files.

## Public Package Files

The public/school-safe package created for final submission is:

- `output/final/PJ_Channel_Customer_Value_Capstone_Public_School_Safe.pptx`
- `output/final/PJ_Channel_Customer_Value_Capstone_Public_School_Safe_Report.md`
- `docs/work/reviewer_guide_public_safe.md`
