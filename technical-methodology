# Technical Methodology: Naloxone Access Gap Analysis

This document outlines the data acquisition, spatial processing, and scoring logic used to identify harm-reduction infrastructure gaps in North Dakota.

## 1. Data Acquisition (Google Places API)

To ensure comprehensive coverage, the analysis utilized a grid-based search strategy to overcome the 60-result limit of the Google Places API.

* **Endpoint:** `https://maps.googleapis.com/maps/api/place/textsearch/json`
* **Query Strings:** `["naloxone", "pharmacy", "public health department", "syringe service program", "clinic"]`
* **Field Mask:** `place_id, name, formatted_address, geometry/location, types, business_status`
* **Grid Search Strategy:** * **Grid Step:** 0.5 degrees (~35 miles).
* **Radius:** 50,000 meters (approx. 31 miles) per search point to ensure overlap.


* **Max Pages:** 3 pages (max 60 results) per grid point.
* **Throttling:** 2-second delay between `next_page_token` requests to comply with API rate limits.
* **Deduplication:** Results were deduped via a unique `place_id` filter across all grid segments.

## 2. Provider Definition

An "Access Point" is defined as any operational facility likely to stock naloxone or provide harm-reduction services.

* **Included Types:** `pharmacy`, `hospital`, `health`, `local_government_office`.
* **Filtering:** Facilities marked as `CLOSED_PERMANENTLY` were excluded. Specific keywords like "Veterinary" or "Pet" were filtered out to ensure results were limited to human healthcare providers.

## 3. Geofencing Rules

To prevent "border noise" (locations in MN, MT, or SD appearing in ND county searches), a two-tier filter was applied:

1. **Bounding Box:** Latitudes [45.9, 49.0] and Longitudes [-104.1, -96.5].
2. **Point-in-Polygon (PiP):** Every site was cross-referenced against official US Census Bureau TIGER/Line county shapefiles to ensure the coordinates physically reside within North Dakota borders.

## 4. Centroid Definition (The "Starting Point")

The distance analysis does not use the geometric center of a county, as North Dakota's population is highly clustered.

* **Method:** **Population-Weighted Centroids.** * **Computation:** Centroids are calculated by averaging the coordinates of all census blocks within a county, weighted by the 2026 projected population of each block. This ensures that the "average" travel time reflects where people actually live (e.g., Fargo's impact on Cass County).

## 5. Time to Care (TTC) Definition

TTC represents the estimated one-way travel time from the population-weighted centroid to the nearest access point.

* **Routing Method:** Haversine distance (Great Circle) was converted to road distance using a **1.2x circuity factor** (standard for Midwestern rural road networks).
* **Speed Assumptions:** * **Rural Modifier:** 55 mph average (accounting for highway speeds vs. secondary gravel roads).
* **Urban Modifier:** 30 mph average (applied to counties with >50,000 population).


* **Formula:** 

## 6. Population-Weighted Risk Score (PWRS)

The PWRS is an open-source metric designed to prioritize resource allocation. It identifies areas with both high population and high isolation.

**Formula:**


* **TTC:** Average time to care (minutes).
* **Population:** 2026 Projected County Population.
* **Interpretation:** A high PWRS indicates a "High Impact Gap"—an area where a large number of people are underserved by local infrastructure.


### Data Provenance

* **Geography:** US Census TIGER/Line 2023.
* **Population:** ND Department of Commerce / US Census Bureau 2026 Projections.
* **Access Points:** Google Places (Last Scan: February 2026).
