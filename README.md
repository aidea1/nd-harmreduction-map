# North Dakota Naloxone Access & Harm Reduction Gap Analysis (2026)

### **Project Overview**

This project provides a data-driven visualization of the geographical disparities in naloxone access across North Dakota. By 2026, shifting population centers and current healthcare infrastructure will create significant **"care deserts."** This **Interactive decision support system** identifies those high-risk areas by calculating the **Population-Weighted Risk Score (PWRS)** and the **Average Time to Care (TTC)** for every county in the state.

### **Core Objectives**

* **Identify Structural Gaps:** Pinpoint counties where population growth outpaces the availability of life-saving harm-reduction sites.
* **Geospatial Accuracy:** Cleanse raw API data to remove out-of-state "noise" (false positives from neighboring states) using strict coordinate geofencing.
* **Interactive Decision Support:** Provide public health practitioners with a tool to visualize exact site locations alongside regional risk metrics.

### **Methodology & Data Pipeline**

The project utilized a multi-stage pipeline to ensure the "Source of Truth" remained accurate:

1. **Data Acquisition:** Aggregated healthcare, pharmacy, and public health site data via the **Google Places API**.
2. **Population Forecasting:** Integrated **2026 Census-based population projections** for all 53 North Dakota counties.
3. **The "Geofence" Filter:** Implemented a strict latitudinal (45.9°N to 49.0°N) and longitudinal (-104.1°W to -96.5°W) boundary to eliminate data artifacts from Minnesota, Wyoming, and Montana.
4. **Risk Metrics:** * **Time to Care (TTC):** Calculated the average travel time from population-weighted centroids to the nearest access point.
* **PWRS:** A proprietary score weighing distance to tertiary hubs against total county population density.


5. **GeoJSON Sanitization:** Developed a recursive "Deep Search" algorithm to repair malformed county border files, ensuring 100% compatibility with Folium/Leaflet.js.

### **Technical Stack**

* **Language:** Python 3.13
* **Analysis:** Pandas (Data manipulation), NumPy (Vectorized distance calculations)
* **Visualization:** Folium / Leaflet.js (Choropleth mapping and interactive markers)
* **Geospatial:** Branca (Color scaling), JSON (GeoJSON boundary management)
* **Deployment:** GitHub Pages / Static Site Hosting

### **Key Findings**

* **Western ND Gaps:** Significant travel times remain a barrier in rural western counties, despite lower total population counts.
* **Urban Saturation:** While hubs like Cass and Burleigh counties have the highest site counts, their high population density keeps their PWRS risk elevated, necessitating high-volume distribution strategies.
* **The 60-Minute Threshold:** Several counties were identified where the "Time to Care" exceeds the critical 60-minute window, highlighting immediate needs for mobile health intervention.

### **How to Use the Interactive decision support system**

* **Hover:** Mouse over any county to see its 2026 Population, Access Site Count, and calculated Risk Score.
* **Markers:** Click the blue circle markers to see the specific name and location of known naloxone providers.
* **Color Scale:** Darker red areas represent higher travel times (lower access), while lighter yellow areas represent higher density of care.

### **Deployment & Sharing**

The interactive decision support system is fully automated and deployed as a static site.

**View the Live Map here:** [https://aidea1.github.io/nd-harmreduction-map/](https://aidea1.github.io/nd-harmreduction-map/)

*Developed by [Akshaya Bhagavathula](https://www.ndsu.edu/people/akshaya-bhagavathula/) PhD, FACE, Associate Professor of Epidemiology, North Dakota State University, Fargo, ND*

**Email: akshaya.bhagavathula@ndsu.edu**
