## data_visualization

Power BI-focused data assets for exploring **gender parity / gender inequality indicators** (primarily World Bank–style indicator series) and building report-ready datasets.

## Project structure

- **`powerbi/`**: Source data (CSV/Excel) and supporting material used for Power BI modeling and reporting.
  - **Model tables (recommended for a star schema)**
    - **`powerbi/Gender_inequality/Gender_inequality.csv`**: *Fact table* with columns `Country_ID`, `Year`, `Indicator_ID`, `Indicator_value`.
    - **`powerbi/Country.csv`** (also duplicated under `powerbi/Gender_inequality/`): *Country dimension* with `Country_ID`, `Country_name`, and region fields.
    - **`powerbi/Indicator_combined.csv`**: *Indicator dimension* / mapping table with `Indicator_ID`, names/descriptions, gender/type, and combined indicator ids.
  - **Report-ready / curated datasets**
    - **`powerbi/Gender_parity_2022.csv`** (and `Gender_parity_2022(1).csv`): Snapshot-style table by country with multiple 2022 indicators (e.g., labor force participation, literacy, rural/urban population) plus GDP per capita and population.
    - **`powerbi/Gender_Egypt.csv`**: Country-specific time series for Egypt across multiple indicators.
    - **`powerbi/Gender_parity_data_transformations.csv`**: Denormalized series with `Country_ID`, `Year`, `Indicator_ID`, `Indicator_description`, `Indicator_value` (useful for Power Query transformations / reshaping).
    - **`powerbi/Building_reports_and_dashboards.xlsx - Country_demographic.csv`**: CSV exported from an Excel source (kept as-is).
  - **Notes / learning material**
    - **`powerbi/Subqueries in WHERE.ipynb`**: SQL learning notebook about subqueries in a `WHERE` clause; expects a local MySQL database (per notebook instructions).
  - **Exploration copies**
    - **`powerbi/Exploring_the_data_model_view/Exploring_the_data_model_view/...`**: Duplicated `Gender_inequality` assets used while exploring Power BI’s model view.

## Using this in Power BI (suggested)

1. **Get Data**
   - Load `powerbi/Gender_inequality/Gender_inequality.csv`, `powerbi/Country.csv`, and `powerbi/Indicator_combined.csv`.
2. **Model relationships**
   - `Gender_inequality[Country_ID]` → `Country[Country_ID]` (many-to-one)
   - `Gender_inequality[Indicator_ID]` → `Indicator_combined[Indicator_ID]` (many-to-one)
3. **Data types**
   - Ensure `Year` is whole number and `Indicator_value` is decimal number.
4. **Build visuals**
   - Slice by `Country`, `Year`, `Indicator_name` (from `Indicator_combined`) and chart `Indicator_value`.

## Notes

- The repository currently contains **data files** (CSV/Excel) and a **SQL learning notebook**, but no committed `.pbix` report file.
- Some datasets are duplicated in subfolders for convenience; prefer the canonical versions in `powerbi/` unless you’re reproducing a specific exploration.
