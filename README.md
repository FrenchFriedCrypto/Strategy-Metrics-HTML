# Trading Dashboard Suite

This repository contains a comprehensive suite of dashboard applications for analyzing trading performance and efficiency. The dashboards ingest CSV data and use popular libraries to render interactive charts, tables, and visualizations. They are designed for traders, analysts, and portfolio managers to gain insights into trade metrics, risk-adjusted performance, and overall trading results.

---

## Table of Contents

- [Overview](#overview)
- [Suite Components](#suite-components)
  - [Results Comparison Dashboard](#results-comparison-dashboard)
  - [Trade Metrics Dashboard Suite](#trade-metrics-dashboard-suite)
  - [Trade Efficiency Metrics Dashboard](#trade-efficiency-metrics-dashboard)
- [Dependencies](#dependencies)
- [Usage](#usage)
- [Customization](#customization)
- [License](#license)

---

## Overview

This dashboard suite enables users to:
- **Compare Results by Symbol:** Visualize and filter financial metrics (e.g., NetProfit, USDTvolume) aggregated by symbol.
- **Assess Trade Metrics:** Analyze capped PnL performance, review individual symbol trade data, and explore summary performance metrics.
- **Evaluate Trade Efficiency:** Compute and visualize trade efficiency (final PnL divided by maximum unrealized PnL) along with risk-adjusted metrics.

Each application within the suite pulls data from CSV files and uses libraries such as PapaParse, Chart.js, and Plotly.js for parsing and visualization.

---

## Suite Components

### Results Comparison Dashboard

**Files:**  
- `rs_summary.html`  
- `rs_metrics.html`  
- `rs_graph.html`

**Detailed Description:**

- **rs_summary.html**  
  - **Purpose:** Provides an overview of the results by displaying grouped bar charts.
  - **Key Features:**
    - **Grouping Options:** Choose how to group data based on the `Params` field (first part, middle value, or last part).
    - **Multiple Metrics:** Charts are generated for a variety of metrics (e.g., `USDTvolume`, `TxnFee`, `NetProfit`, etc.).
    - **Dynamic Chart Generation:** Uses Chart.js to create responsive bar charts.
    - **CSV Parsing:** Utilizes PapaParse to load and filter CSV data.

- **rs_metrics.html**  
  - **Purpose:** Displays computed metrics for each symbol in a grid format with filtering options.
  - **Key Features:**
    - **Filters:** Allows users to set minimum values for metrics like Profit (%), Trades, Success Rate, and more.
    - **Metrics Grid:** Generates a mini table for each symbol showing aggregated metrics.
    - **CSV Data Aggregation:** Processes the CSV data to calculate averages and percentages for display.

- **rs_graph.html**  
  - **Purpose:** Visualizes average NetProfit by symbol using a line chart.
  - **Key Features:**
    - **Param Section Selector:** Users can select different parts of the `Params` field (Section 1, 2, or 3) to group the data.
    - **Scale Toggle:** Switches the y-axis between a symlog (logarithmic) and normal scale for enhanced data interpretation.
    - **Interactive Filters:** Updates both the chart and the metrics grid based on user-defined filter criteria.
    - **CSV Data Processing:** Aggregates data per symbol and parameter section, then renders the line chart using Chart.js.

---

### Trade Metrics Dashboard Suite

**Files:**  
- `qm_capped_pnl.html`  
- `qm_individual.html`  
- `qm_index.html`

**Detailed Description:**

- **qm_capped_pnl.html**  
  - **Purpose:** Displays consolidated PnL metrics by applying a user-defined cap to individual trades. It calculates and compares the raw total PnL with the capped total PnL across a range of cap values.
  - **Key Features:**
    - **Cap Input Field:** Adjust the cap value used to limit individual trade contributions.
    - **Summary Section:** Displays the raw and capped PnL totals.
    - **Interactive Charts:**  
      - An overall chart shows how the capped PnL total varies as the cap value increases.
      - Separate charts for **Long Trades** and **Short Trades** help analyze trade-type performance.
    - **CSV Parsing:** Uses PapaParse to load trade data from `daily_trades.csv`.

- **qm_individual.html**  
  - **Purpose:** Provides a multi-file dashboard for analyzing trade metrics for individual symbols. CSV files (one per symbol) are loaded dynamically from a designated "data" folder.
  - **Key Features:**
    - **CSV Files List:** An editable textarea to list CSV filenames (one per line) for the symbols you wish to analyze.
    - **Trade Type Filters:** Checkboxes to toggle the display of All Trades, Long Trades, and Short Trades.
    - **Risk Size Input:** Adjust the risk size per trade, which is used in various normalization calculations.
    - **Dynamic File Containers:** For each symbol (derived from the CSV filename), the dashboard creates a dedicated section with:
      - Multiple interactive charts such as Unrealized Profit Distribution, PnL Distribution, Portfolio Unrealized PnL Over Time, Equity Line (Cumulative PnL), and various distributions based on risk ratios.
      - A summary section displaying key metrics for the symbol.
    - **CSV Parsing & Charting:** Uses PapaParse and Chart.js to load and render data interactively.

- **qm_index.html**  
  - **Purpose:** Acts as the summary dashboard for overall trade metrics. It allows you to load a CSV file containing aggregate trade data and view key performance indicators, interactive charts, and a detailed table of trade data.
  - **Key Features:**
    - **CSV Input Field:** Specify the filename of the CSV file to load (default is set to a compiled CSV file).
    - **Settings Bar:** Toggle the visibility of additional columns (such as Entry Prices, Trade Type, Quantities, ATR Values, Txn Fee, and Volume) in the trade data table.
    - **Summary Metrics:** Displays key performance indicators like Total Trades, Net Profit, Daily Average Profit, Success Rate, Maximum Drawdown, and more.
    - **Interactive Charts:**  
      - Charts for overall trade data including Unrealized Profit Distribution, PnL Distribution, Portfolio Unrealized PnL Over Time, Equity Line, and various PnL and duration distributions based on risk ratios.
      - Separate charts for Long Trades and Short Trades.
    - **Trade Data Table:** A detailed table of individual trades with an optional mini graph column to visualize daily unrealized PnL trends.

---

### Trade Efficiency Metrics Dashboard

**File:**  
- `st_consolidated.html`

**Detailed Description:**

- **st_consolidated.html**  
  - **Purpose:** Provides an interactive dashboard for analyzing trade efficiency metrics. It processes CSV data to compute efficiency values for each trade (defined as final PnL divided by the maximum unrealized PnL) and renders various charts.
  - **Key Features:**
    - **CSV Parsing:** Loads data from `consolidated_long.csv` and expects fields such as `symbol`, `param1`, `param2`, `param3`, `PnL`, and `unrealized`.
    - **Metric Computations:**  
      - Calculates the maximum unrealized PnL from the daily unrealized values.
      - Computes trade efficiency as _final PnL / max unrealized PnL_.
      - Derives risk-adjusted metrics by normalizing max unrealized PnL using a risk size of 50.
    - **Interactive Controls:**  
      - **Negative Trades Toggle:** A slider to include or exclude trades with negative PnL.
      - **X-Axis Parameter Options:** Buttons (Param1, Param2, Param3) to select the grouping variable.
    - **Charts:**  
      - **Average Efficiency Line Chart:** (via Plotly) Displays the average efficiency per symbol.
      - **Distribution Charts:** (via Chart.js) Show distributions of normalized unrealized PnL (uPnL/RR) and final PnL (PnL/RR).
      - **Box & Whisker Plots:** (via Plotly) Present grouped box plots for risk-adjusted maximum unrealized values by symbol.

---

## Dependencies

This dashboard suite uses the following external libraries (loaded via CDN):

- **[PapaParse](https://www.papaparse.com/):** For parsing CSV files.
- **[Chart.js](https://www.chartjs.org/):** For creating interactive and responsive charts.
- **[Plotly.js](https://plotly.com/javascript/):** For rendering advanced visualizations such as line charts and box plots.

---

## Usage

1. **Prepare Your Data:**
   - For the **Results Comparison Dashboard**, ensure that `Results_comparison.csv` is placed in the same directory as the HTML files.
   - For the **Trade Metrics Dashboard Suite**, ensure that your main CSV file (e.g., `daily_trades.csv` or `compiled_csv_data/daily_trades.csv`) is available, and for individual symbol analysis, store the CSV files in the `data` folder.
   - For the **Trade Efficiency Metrics Dashboard**, ensure that `consolidated_long.csv` is accessible and formatted correctly with required columns such as `symbol`, `param1`, `param2`, `param3`, `PnL`, and `unrealized`.

2. **Open the Dashboard Files:**
   - Open any of the HTML files (e.g., `rs_summary.html`, `qm_capped_pnl.html`, or `st_consolidated.html`) in a modern web browser.
   - Use the navigation buttons provided in each application to switch between different views.

3. **Interact with the Dashboards:**
   - **Results Comparison Dashboard:**  
     - Use filter options and grouping selectors to refine data presentation.
     - Toggle between different chart scales (normal vs. symlog) and view charts by symbol.
   - **Trade Metrics Dashboard Suite:**  
     - In **qm_capped_pnl.html**, adjust the cap value to see how capped PnL changes for overall, long, and short trades.
     - In **qm_individual.html**, edit the list of CSV filenames, use trade type filters, and adjust risk size per trade to update metrics and charts for each symbol.
     - In **qm_index.html**, specify the CSV filename and use the settings bar to toggle additional columns in the trade data table.
   - **Trade Efficiency Metrics Dashboard:**  
     - Use the "Include negative" slider to toggle negative PnL trades.
     - Select the desired parameter (Param1, Param2, or Param3) using the provided buttons.
     - Review the average efficiency line chart, distribution charts, and box plots to assess trade efficiency and risk-adjusted performance.

---

## Customization

- **CSV Data Files:**  
  Modify your CSV files as needed. Ensure that the header names (e.g., `PnL`, `Daily unrealized`, `Entry Dates`, `symbol`, etc.) match those referenced in the JavaScript code.

- **Default Values:**  
  Default risk sizes, cap values, and filter thresholds are set within the code. These can be adjusted directly in the scripts or via the provided input fields.

- **Chart Settings:**  
  Customize chart appearance (colors, labels, tooltips, etc.) by editing the configuration objects for Chart.js and Plotly.js in the code.

- **Styling:**  
  The CSS styles are embedded within each HTML file. Update these styles to match your branding or design preferences.

---

## License

*Include license information here if applicable.*
