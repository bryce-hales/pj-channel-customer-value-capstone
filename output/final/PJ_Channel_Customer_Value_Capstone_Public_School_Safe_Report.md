# PJ Channel Customer Value Analysis

Data Technology Capstone - Public / School-Safe Report

## 1. Project Objective and Research Question

This capstone evaluates which acquisition/source channels appear to bring higher-value Permanent Jewelry (PJ) customers. The main research question is:

> Which acquisition/source channels appear to bring higher-value Permanent Jewelry customers when measured by 12-month customer revenue, repeat purchase behavior, and follow-on consumables activity?

The project focuses on customer value rather than only first-order activity. A channel can look productive at acquisition but still produce lower long-term value, lower repeat purchasing, or less follow-on consumables demand. The analysis therefore compares channels using three headline measures:

- Average 12-month customer revenue
- 12-month repeat purchase rate
- Follow-on consumables rate

## 2. Business / Background Context

Permanent Jewelry customer acquisition can come from direct/owned traffic, paid search, organic search, social channels, imported lists, system-created sources, and other CRM buckets. These sources are not equally useful for a business recommendation. Some represent true acquisition channels, while others represent technical syncs, legacy imports, support conversations, or records that are missing usable attribution.

The business value question is not just "which source produced orders?" It is "which source appears to bring customers who continue to create value after acquisition?" For that reason, this project uses a customer-level value window and then reports only aggregate, public-safe channel summaries.

## 3. Data Sources Used

The analysis used local exports from four systems. Raw exports remain private and are not included in this public-facing package.

| Source | Role in Project | Public-Safe Usage |
| --- | --- | --- |
| Shopify | Customers, orders, order lines, and product details | Used locally to build customer value and product behavior measures |
| HubSpot | Customer/source bridge and lifecycle/source context | Used as the main bridge for source/channel labels because of strong Shopify email matching |
| Salesforce | CRM validation, Shop URL validation, PJ context, and directional order/revenue validation | Used as supporting validation and enrichment, not as the primary customer value source |
| GA4 | Marketing channel validation | Used only as aggregate validation because GA4 exports overlap and should not be treated as deduplicated totals |
| Tableau aggregate exports | Visualization layer | Safe aggregate CSVs only |

## 4. Data Privacy and Sanitization Approach

The public-facing package excludes raw exports and customer-level processed data. No customer names, emails, phone numbers, addresses, order IDs, contact records, or raw order rows are included.

The customer-level processed dataset `customer_value_dataset.csv` was regenerated locally and contained 9,021 customer-level rows. It remains local-only and is not included in the public/school-facing deliverables. A local line count showed 9,022 lines including the header.

Public-facing materials use only:

- Aggregate KPI tables
- Aggregate chart-planning tables
- Aggregate Tableau export CSVs
- Sanitized screenshots if available
- Methodology documentation
- Safe summary tables

Monthly value and rate metrics are suppressed for channel-month cells with fewer than 5 customers. This prevents small cells from exposing sensitive or easily identifiable customer behavior.

## 5. Data Cleaning and Preparation

The project began by validating and joining Shopify customer, order, and order-line data. The preparation work included:

- Normalizing email fields for cross-system matching
- Validating customer/order/order-line relationships
- Building first-order and 12-month value windows
- Classifying product activity to identify follow-on consumables behavior
- Creating customer-level source/channel labels for analysis
- Generating aggregate output tables for EDA and Tableau

The final public report does not expose the customer-level rows used to produce the aggregates.

## 6. Joining and Matching Strategy

HubSpot was used as the main customer-source bridge because it had a very high Shopify email match rate. The workflow normalized email addresses and joined Shopify customer records to HubSpot contacts where available. HubSpot source fields were then mapped into derived channel groups.

Salesforce was used as a supporting enrichment and validation layer. It helped confirm CRM context, validate the PJ Shopify store URL, and provide directional checks against PJ order and revenue activity.

GA4 was used as a marketing-platform validation layer. It helped confirm that headline marketing channels were meaningful in aggregate, but it was not used as the primary customer value source because GA4 exports can overlap and should not be interpreted as deduplicated totals.

## 7. Validation Checks

The project included several validation checks before drawing conclusions:

- HubSpot-to-Shopify matching validated the source bridge.
- Salesforce-to-Shopify matching validated CRM/store context.
- Salesforce opportunity/order summaries provided directional validation for PJ order and revenue activity.
- The Salesforce Shop URL `https://sunstonepj.myshopify.com` identified the PJ Shopify store.
- GA4 export validation confirmed that aggregate marketing channels were present, while also documenting overlap limitations.
- Build validation checked that customer value tables and aggregate EDA outputs were generated as expected.

## 8. Channel Eligibility Methodology

Not every source bucket was eligible for headline recommendation. The project separated channels into eligibility classes:

- **Headline Eligible:** true acquisition channels with at least 50 customer-level records.
- **Directional / Supporting Only:** true or potentially useful channels that were too small, imported/list-based, support-based, or otherwise better treated as directional.
- **Excluded from Channel Recommendation:** system, sync, technical, or integration buckets that do not represent true acquisition channels.
- **Needs Review:** missing, unclassified, unassigned, or GA4-only categories that need better mapping before they can support recommendations.

The final headline-eligible channels were:

- Direct / Owned
- Paid Search
- Organic Search

GA4-only categories such as Cross-network and Organic Shopping were visible in aggregate validation, but they were not cleanly mapped into customer-level derived channel groups. They are therefore flagged as needs-review rather than used as headline customer value channels.

## 9. Exploratory Data Analysis

EDA outputs were built as aggregate chart-planning tables only. The EDA stage focused on:

- Channel KPI comparisons
- Monthly first-order cohort trends
- Value distribution views
- Repeat and follow-on consumables behavior
- Channel eligibility summaries
- Chart recommendations for Tableau

The EDA outputs did not include raw customer rows. The aggregate files were then packaged for Tableau.

## 10. Visualizations and Dashboard Summary

The Tableau package includes safe aggregate CSVs only:

- `tableau_headline_channel_kpis.csv`
- `tableau_headline_monthly_trends.csv`
- `tableau_headline_value_distribution.csv`
- `tableau_channel_eligibility_overview.csv`
- `tableau_channel_eligibility_detail.csv`
- `tableau_chart_recommendations.csv`
- `tableau_export_manifest.csv`
- `tableau_data_dictionary.csv`

The PowerPoint includes sanitized Tableau screenshots for the average 12-month revenue view, repeat/follow-on behavior view, and full dashboard summary. The screenshots were reviewed for obvious public-safety issues and show aggregate channel-level outputs rather than customer/contact/order-level records. Any future screenshot replacement should still be reviewed before public release to confirm that no names, emails, order IDs, contact records, or other sensitive details are visible.

## 11. Key Findings

Headline aggregate KPI results:

| Channel | Customers | Avg 12M Revenue | Repeat Rate | Follow-On Consumables Rate |
| --- | ---: | ---: | ---: | ---: |
| Direct / Owned | 139 | $1,101.06 | 30.00% | 15.00% |
| Paid Search | 89 | $1,455.22 | 42.70% | 21.35% |
| Organic Search | 70 | $1,338.89 | 37.14% | 22.86% |

Paid Search appears strongest for average 12-month customer revenue and repeat purchase rate among headline-eligible channels. Organic Search appears strongest for follow-on consumables rate. Direct / Owned has the largest sample size among headline channels, but lower value and repeat metrics.

These findings should be interpreted as strong directional evidence, not as a final profitability conclusion, because acquisition cost data was not included in the headline customer value tables.

## 12. Limitations

The analysis has several important limitations:

- Headline channel sample sizes are modest, especially once the project focuses only on true acquisition channels.
- GA4 exports overlap and should not be treated as deduplicated totals.
- Source attribution gaps remain for missing, unclassified, imported, or technical buckets.
- Cross-network and Organic Shopping appear in GA4 but are not cleanly mapped to customer-level derived channel groups.
- Product classification and follow-on consumables logic depend on the current heuristic.
- The results compare customer value, not channel profitability, because CAC/ROAS inputs were not included.

## 13. Recommendations

Recommended actions based on the aggregate findings:

- Continue investing in Paid Search, but monitor profitability and CAC before scaling aggressively.
- Strengthen Organic Search because it shows the highest follow-on consumables rate among headline channels.
- Use Direct / Owned as a volume baseline, while working to improve long-term value and repeat behavior.
- Improve UTM discipline and source/channel capture so future customer value analysis has fewer unclassified records.
- Keep system, sync, imported, and technical sources out of headline acquisition recommendations.

## 14. Future Work

Useful next steps include:

- Add Google Ads, Meta, or other cost exports to calculate CAC, ROAS, and contribution-level performance.
- Improve customer-level mapping for GA4-only categories such as Cross-network and Organic Shopping.
- Revisit product classification rules as the PJ catalog changes.
- Connect future Console logic to aggregate-safe customer value metrics.
- Track cohort performance over time with the same small-cell suppression rule.

## 15. Code and Repository Structure

Major workflow scripts live in the `python/` directory. Numbered scripts support validation, source mapping, customer value table generation, channel eligibility classification, EDA tables, and Tableau aggregate exports.

Aggregate output tables live in:

- `output/tables/`
- `tableau_exports/`

Public-facing final deliverables live in:

- `output/final/`
- `docs/work/reviewer_guide_public_safe.md`

Raw exports and customer-level processed files remain local/internal only.

## 16. AI Disclosure / Tools Used

I used ChatGPT and Codex to help structure the project, generate Python scripts, document the workflow, and prepare sanitized report/presentation materials. I reviewed the outputs and kept raw company/customer data out of the public-facing submission.

## 17. Conclusion

The capstone shows that acquisition/source channels should be evaluated on customer value and retention behavior, not just first purchase or aggregate traffic. Among headline-eligible channels, Paid Search has the strongest 12-month revenue and repeat purchase signals, while Organic Search has the strongest follow-on consumables signal. The next version of the analysis should add cost data and strengthen attribution capture so customer value can be connected to profitability.
