**IPL Data Analysis with Apache Spark on Databricks**
This repo contains notebooks, scripts and visual outputs for an end-to-end analysis of Indian Premier League (IPL) ball-by-ball data using Apache Spark (Spark SQL + DataFrame API) on Databricks.
Key insights include top run-scorers per season, economy rates of bowlers, toss-win impact, venue favourability, and season-on-season scoring trends, all illustrated with rich charts exported from the notebook.

Table of Contents
Project Architecture

Dataset

Environment & Setup

Notebooks

Key Findings & Visuals

Running the Project

Future Work

Project Architecture
kotlin
Copy
Edit
├── data/
│   └── ball_by_ball.csv
├── notebooks/
│   └── 01_IPL_Data_Analysis.py
├── images/
│   ├── top_batsmen_runs.png
│   ├── economy_rates.png
│   ├── runs_per_over_time.png
│   └── venue_win_heatmap.png
└── README.md
Raw CSV lives in dbfs:/FileStore/ipl/ and is mounted at runtime; processed data is cached as Delta tables for re-use. 
docs.databricks.com

Dataset
We use the publicly available IPL Ball-by-Ball dataset (all seasons) from Kaggle.
Kaggle
Kaggle

The file includes every delivery with batter, bowler, runs, extras, dismissal, match ID, venue and date.

Environment & Setup
Item	Version / Setting
Databricks Runtime	14.3 LTS (includes Spark 3.5)
Cluster	1 driver + 2 workers (i3.xlarge)
Libraries	pyspark, pandas, matplotlib, seaborn
Notebook Export	.py and .dbc formats for source control & sharing 
docs.databricks.com

Charts are saved with matplotlib.pyplot.savefig('images/<name>.png', dpi=150, bbox_inches='tight').
Matplotlib

Notebooks
Notebook	Description
01_IPL_Data_Analysis	Ingest → Clean → Transform → Analyse → Visualise workflow. Includes Spark SQL queries (GROUP BY, WINDOW) and joins for contextual calculations.
spark.apache.org
02_Structured_Streaming_Demo (optional)	Shows how to tail live score feeds and append to Delta for near real-time dashboards, using Spark Structured Streaming concepts.
docs.databricks.com
docs.databricks.com

Key Findings & Visuals
1. Top Run-Scoring Batsmen per Season

Virat Kohli leads overall with a record 973 runs in 2016; Shubman Gill tops the 2024 season.

2. Economy Rates of Bowlers

Spinners show tighter economy (< 7 RPO) at Chepauk and Ekana stadiums.

3. Scoring Pattern Over Time

Average first-innings total has climbed from ~150 in 2008 to 183 in 2024, reflecting power-hitting era.

4. Venue vs. Win Percentage Heat-Map

Home advantage strong at Eden Gardens and Wankhede; neutral venues like Dubai show balanced results.

(All visuals generated in-notebook using Seaborn bar-/line-plots and saved to /images.
Kaggle
)

Running the Project
Clone repo & import notebook under Workspace → Repos in Databricks.

Upload ball_by_ball.csv to dbfs:/FileStore/ipl/ or point the notebook to your path.

Attach & run the notebook. Initial ingest caches a Bronze Delta table, subsequent runs are fast.

Export charts: cells auto-save to images/; README links will render on GitHub.

Future Work
Delta Lake OPTIMIZE/VACUUM to compact small files and manage log size.
docs.databricks.com
docs.databricks.com

Advanced ML: build XGBoost model to predict win probability after each over.

Real-Time Dashboard: plug Structured Streaming output into a lightweight React/Grafana front-end.

References
Apache Spark docs on GROUP BY and aggregation patterns.
spark.apache.org

Databricks docs on Structured Streaming and notebook export.
docs.databricks.com
docs.databricks.com

Delta Lake optimisation guidelines.
docs.databricks.com
docs.databricks.com

Kaggle IPL datasets for sourcing.
Kaggle
Kaggle

Matplotlib savefig usage for static image export.
Matplotlib

Seaborn visual examples applied to cricket data.
Kaggle
