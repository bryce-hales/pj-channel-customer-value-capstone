# Public-Safe Reviewer Guide

This guide explains the repository workflow for the PJ Channel Customer Value capstone and separates public/school-safe outputs from local-only sensitive files.

## Public Safety Boundary

The final public-facing package uses only aggregate outputs, sanitized documentation, and optional sanitized screenshots. Do not include raw customer rows, order rows, contact records, names, emails, phone numbers, addresses, order IDs, or internal-only screenshots.

`data/processed/customer_value_dataset.csv` was regenerated locally and contains 9,021 customer-level rows. It is intentionally local-only and must not be committed or included in a public-facing package.

Screenshots should be manually checked before public release. If a screenshot shows customer/contact/order-level detail, leave it out or mark it internal-only.

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

Other aggregate summary files in `output/tables/` can be reviewed for school-safe use when they contain only grouped counts, rates, validation summaries, or chart-planning outputs. Monthly value/rate metrics suppress channel-month cells under 5 customers.

## Local-Only / Internal Files

Treat the following as local-only or internal unless separately reviewed and sanitized:

- Raw exports under `data/raw/`
- Intermediate working data under `data/interim/`
- Customer-level processed datasets under `data/processed/`, especially `customer_value_dataset.csv`
- Any file containing customer names, emails, phone numbers, addresses, order IDs, contact IDs, or order-level rows
- Any screenshot that shows raw records, identifiers, CRM contact details, or internal-only dashboard data

## Script List

### `python/06_validate_hubspot_shopify_match.py`

Validates how well Shopify customer records match HubSpot contacts. This script supports the decision to use HubSpot as the main customer-source bridge. Outputs are aggregate validation summaries, not raw contact data.

### `python/07_build_hubspot_source_mapping.py`

Builds a source mapping layer from HubSpot fields into more usable source/channel labels. This helps translate CRM source values into analysis-ready acquisition groups.

### `python/09_build_customer_value_dataset.py`

Builds the local customer-level value dataset by combining Shopify customer/order/order-line behavior with source/channel context. The resulting `customer_value_dataset.csv` is sensitive, local-only, and not part of the public package.

### `python/10_validate_salesforce_shopify_match.py`

Compares Salesforce CRM records with Shopify context for validation and enrichment. This is supporting validation, not the primary attribution source.

### `python/11_validate_salesforce_opportunity_order_summary.py`

Creates directional Salesforce opportunity/order validation summaries. It helps confirm PJ order and revenue context and supports validation of the Salesforce Shop URL.

### `python/12_validate_ga4_exports.py`

Validates GA4 export files at an aggregate level. GA4 is used as a marketing-platform validation layer only because exports can overlap and should not be treated as deduplicated totals.

### `python/13_build_channel_eligibility.py`

Classifies derived channel groups into headline eligible, directional/supporting, excluded, or needs-review classes. This script prevents system, sync, technical, imported, and unclassified buckets from driving headline acquisition recommendations.

### `python/14_build_eda_chart_tables.py`

Builds aggregate EDA chart-planning tables, including headline channel KPIs, monthly trends, value distribution, and chart recommendation inputs. These are aggregate outputs only.

### `python/15_build_eda_findings_summary.py`

Writes a concise methodology/findings summary from the aggregate EDA outputs. This supports report and presentation documentation.

### `python/16_build_tableau_export_package.py`

Packages safe aggregate CSVs for Tableau, including KPI, monthly trend, value distribution, eligibility, recommendation, manifest, and data dictionary files.

## Notes on Related Workflow Files

`python/08_build_customer_source_enriched.py` is part of the source enrichment workflow even though it is not a headline script in the final rubric list. Treat its outputs carefully because source-enriched customer-level files may still be sensitive.

The Tableau workbook files can be useful for dashboard review, but screenshots exported from Tableau must be inspected before public sharing.

## Public Package Files

The public/school-safe package created for final submission is:

- `output/final/PJ_Channel_Customer_Value_Capstone_Public_School_Safe.pptx`
- `output/final/PJ_Channel_Customer_Value_Capstone_Public_School_Safe_Report.md`
- `docs/work/reviewer_guide_public_safe.md`

## AI Disclosure

I used ChatGPT and Codex to help structure the project, generate Python scripts, document the workflow, and prepare sanitized report/presentation materials. I reviewed the outputs and kept raw company/customer data out of the public-facing submission.
