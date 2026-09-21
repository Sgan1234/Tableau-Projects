NYC Tree Census: Get to Know the Local Urban Tree Canopy

Overview

This project explores New York City's urban forest using the 2015 NYC Tree Census dataset. Through SQL queries and an interactive Tableau dashboard, I analyzed the distribution, diversity, and physical characteristics of trees across the five boroughs — identifying the most and least common species, mapping tree density by neighborhood, and comparing tree heights across boroughs.

The goal is to make the urban canopy more legible: which species dominate, where the canopy is dense or sparse, and how tree characteristics vary across the city.

Research Questions

What are the most and least common tree species in NYC?
How does tree density vary across neighborhoods and boroughs?
Which boroughs have the tallest trees on average?
What does the species distribution reveal about the urban forest's composition?
Data Source

Source	Description	Access
NYC Open Data	2015 Street Tree Census — species, location, height, diameter, health condition, and stewardship data for every street tree in NYC	NYC Open Data
Note: The dataset is publicly available and contains no personally identifiable information.

Repository Structure

text
nyc-tree-census/
├── README.md
├── sql/
│   └── analysis.sql           # Core analytical queries
├── data/
│   └── sample_data.csv        # Anonymized sample subset
├── tableau/
│   └── tree_census.twb        # Tableau workbook
└── results/
    └── screenshots/           # Dashboard previews
Setup and Reproduction

Prerequisites

PostgreSQL 14 or higher
psql command-line tool
Tableau Desktop or Tableau Public (for the dashboard)
Installation

bash
# Clone the repository
git clone https://github.com/yourusername/nyc-tree-census.git
cd nyc-tree-census

# Create the database
createdb nyc_trees

# Load schema and data
psql -d nyc_trees -f sql/analysis.sql
SQL Techniques Demonstrated

Technique	Application
GROUP BY + COUNT	Identifying most and least common species
ORDER BY + LIMIT	Ranking species by frequency
AVG aggregation	Calculating average tree height by borough
Joins	Linking tree records to borough and neighborhood boundaries
CAST	Converting height and diameter values for numeric sorting
Key Findings

Species dominance: The most common tree species in NYC is the London plane tree (Platanus × acerifolia), followed by honey locust and callery pear. The least common species appear only a handful of times across the entire census.
Density is uneven: Tree density varies dramatically across neighborhoods, with some areas showing dense canopy coverage while others — often lower-income neighborhoods — have sparse tree populations.
Height varies by borough: Staten Island and Queens generally have taller trees on average, while Manhattan and the Bronx show shorter average heights, likely reflecting planting age, species mix, and growing conditions.
Canopy equity matters: The uneven distribution of trees across neighborhoods has implications for air quality, heat island effects, and environmental equity.
Sample Queries

Most common species:

sql
SELECT
    spc_common AS species,
    COUNT(*) AS tree_count
FROM
    tree_census
GROUP BY
    spc_common
ORDER BY
    tree_count DESC
LIMIT 10;
Average tree height by borough:

sql
SELECT
    boroname AS borough,
    ROUND(AVG(tree_height_ft)::numeric, 1) AS avg_height_ft
FROM
    tree_census
WHERE
    tree_height_ft IS NOT NULL
GROUP BY
    boroname
ORDER BY
    avg_height_ft DESC;
Dashboard Preview

https://results/screenshots/tree_density_map.png

Tree density map showing canopy distribution across NYC neighborhoods.

https://results/screenshots/tree_height_borough.png

Average tree height comparison across the five boroughs.

Skills Demonstrated

PostgreSQL querying with aggregation and ranking
Data cleaning and handling of null values in tree measurements
Geographic data interpretation for density mapping
Tableau dashboard design for non-technical audiences
Environmental data storytelling
References

NYC Open Data. (2015). 2015 Street Tree Census — Tree Data. https://data.cityofnewyork.us/Environment/2015-Street-Tree-Census-Tree-Data/uvpi-gqnh
