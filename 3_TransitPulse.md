# 🚌 TransitPulse: Mapping Transit Access Inequality in U.S. Cities

**TransitPulse** is a visual analytics project that explores the **inequality of public transit access** across urban neighborhoods in the United States. Using open datasets and graph-based modeling, this dashboard highlights where transit systems fail to connect underserved communities to essential destinations like schools, hospitals, and workplaces.

Built with **Python** for data processing and **Apache ECharts** for front-end visualization, TransitPulse delivers an interactive experience to policymakers, urbanists, and the curious public.

---

## 📊 Features

- **Node-Link Graphs**  
  Visualize transit networks as connected graphs, with neighborhoods as nodes and transit routes as edges.

- **Time-Series Analysis**  
  Track changes in transit coverage over the past decade and correlate it with population growth or decline.

- **Choropleth & Heatmaps**  
  Identify "transit deserts" where low-income areas have limited or no reliable access.

- **Filtering & Drill-Down**  
  Select cities, filter by income level, or zoom into zip codes for detailed insights.

---

## 🧠 Project Motivation

Equitable access to public transit is a fundamental issue in urban development. This project seeks to answer questions like:

- Which neighborhoods are most underserved by transit infrastructure?
- How has transit coverage changed over time in major U.S. cities?
- Is there a correlation between income inequality and poor transit access?

---

## 📂 Data Sources

- [GTFS Feeds](https://transitfeeds.com/) – Transit routes and stops for multiple U.S. cities  
- [U.S. Census Bureau ACS](https://data.census.gov) – Demographic and income data  
- [OpenStreetMap](https://www.openstreetmap.org/) – Street-level geospatial context  

---

## 🛠️ Tech Stack

- **Python 3.10+**  
  - `pandas` for data wrangling  
  - `networkx` for graph construction  
  - `geopandas` for spatial joins  
- **Apache ECharts** for all visualizations (embedded via HTML/JS or Streamlit)  
- **Streamlit** *(optional)* for interactive UI  
- **Jupyter Notebooks** for preprocessing and EDA  

---

## 📈 Example Visualizations

- `transit_network_graph.html` — Interactive node-edge graph showing neighborhood connectivity  
- `coverage_timeseries.html` — Line chart tracking stop density per square mile over 10 years  
- `accessibility_heatmap.html` — Map of accessibility scores by income level

---

## 🚀 Getting Started

```bash
git clone https://github.com/yourusername/transitpulse.git
cd transitpulse
pip install -r requirements.txt
streamlit run dashboard.py
```

> Or open `index.html` directly in your browser if using the static ECharts version.

---

## 📌 Future Plans

- Add real-time transit API integration  
- Use ML clustering to predict underserved growth zones  
- Integrate biking/walking route overlays  
- Build comparison dashboards between cities

---

## 📜 License

This project is licensed under the MIT License.

---

## 🙏 Acknowledgements

- Apache ECharts team  
- TransitFeeds API  
- U.S. Census Bureau  
- OpenStreetMap contributors  
