# 🎧 Spotify Top 50 — Interactive Power BI Dashboard

A dynamic, interactive Power BI dashboard built from a **Figma-led design** to analyze **Top 50 hit songs and their artists**. The solution consolidates KPIs, trends, and drill-downs so music analysts, playlist managers, and marketing teams can quickly see what’s performing and why.

👉 **Click below to open Spotify Insights:**

[![View Spotify Report](https://img.shields.io/badge/Power%20BI-View%20Spotify%20Dashboard-blue)](https://app.powerbi.com/view?r=eyJrIjoiOTA2OTA1YzAtOWEyYi00MDJjLWJlZWItNTI2OWNiZjM0YzE5IiwidCI6ImM2MDAxOTk3LWQ4MzEtNDY3Zi05NDZhLThhZWU1ZDc0NmQ1NCJ9)

---

## 🔹 Short Description / Purpose
This dashboard is designed to provide quick insights into Spotify’s Top 50 hit songs dataset. It enables stakeholders to monitor KPIs like total songs, distinct artists, popularity trends, explicit vs non-explicit comparison, and album/single distribution for faster decision-making.

---

## 🧰 Tech Stack
- 🎨 **Figma** – UI/UX prototyping for layout, color system, icons, and navigation.
- 📊 **Power BI Desktop** – Main visualization and interactivity platform.
- 📂 **Power Query** – Data cleaning, type conversions, and schema shaping.
- 🧮 **DAX (Data Analysis Expressions)** – Measures for KPIs, rankings, and trends.
- 🗃️ **Data Modeling** – Relationships among Songs, Artists, Albums, and Calendar tables.

---

## 📚 Data Source
Dataset: Spotify Top 50 tracks (latest snapshot), including:
- **song_name**, **artist_name**, **album_type** (single/album/compilation)
- **release_date**, **year**, **month**
- **popularity score**, **explicit flag**, **duration**, **chart position**

---

## ✨ Features / Highlights

### Business Problem
Raw “Top 50” lists only provide rankings, making it hard to identify patterns and trends. Teams need:
- Quick KPI monitoring
- Explicit vs Non-Explicit performance comparison
- Album/single breakdown
- Yearly and monthly trends
- Artist-song drill-down

### Goal of the Dashboard
- Provide a single-view KPI summary
- Compare explicit vs non-explicit performance
- Show album type distribution
- Display yearly and monthly popularity trends
- Highlight top-performing songs and artists

---

## 👣 Walkthrough of Key Visuals
- **KPI Tiles:** Total Songs, Distinct Artists, Avg Popularity, Avg Duration
- **Donut Charts:** Explicit vs Non-Explicit share
- **Bar Chart:** Songs by album type
- **Line Chart:** Avg Popularity by Month (toggle Month/Quarter)
- **Column Chart:** Distinct Songs by Year
- **Top Lists:** Songs & Artists ranked by Popularity
- **Detail Tables:** Artist & Song pages with release date, album type, popularity, duration

---

## 💼 Business Impact & Insights
- **Marketing Optimization:** Identify high-popularity artists/songs for promotions
- **Content Strategy:** Compare explicit vs non-explicit engagement
- **Catalog Planning:** Understand single vs album dominance
- **Trend Tracking:** Spot seasonal surges in popularity
- **Talent Scouting:** Find artists with consistent hits or frequent #1 positions

---

## 📑 Page-by-Page Walkthrough

### Navigation
Top bar page navigator (**Home ▸ Overview ▸ Artists ▸ Songs**) with a consistent dark theme, left-side scroller for songs/artists, and a central spotlight card mimicking a music player.

#### 1) 🏠 Home
- Branding and navigation landing page
- Large Spotify logo and navigation buttons

#### 2) 📊 Overview Page
- KPIs: Avg Popularity, Avg Duration, Distinct Artists, Total Songs
- Charts: Songs by Artist, Popularity by Song, Album Type Distribution, Explicit vs Non-Explicit share, Avg Popularity by Month, Songs by Year

#### 3) 🎤 Artists Page
- Visuals: Top Artists by Popularity, Songs by Artist, Hits by Artist (#1 positions), Popularity by Song
- Detail Table: song_name, release_date, album_type, max_popularity, avg_popularity, duration

#### 4) 🎵 Songs Page
- Visuals: Top Songs by Popularity, Tracks per Song, Songs by Song Count
- Detail Table: song_name, release_date, distinct_artists, avg_popularity, position, duration, year

---

## 🎛️ Interactions & UX
- Global Filters: Year, Month, Album Type, Explicit flag
- Cross-Highlighting: Artist/song selection filters visuals
- Drill-through: Overview → Artist/Song details
- Tooltips: Show min/max popularity and release info
- Navigation Bar: Persistent for smooth page jumps

**##🔧 Data Modeling Notes:**

## Star Schema:

 Fact: Songs
Dimensions: Artists, Albums, Calendar


Date Handling: Calendar table with Year, Month, Quarter
Duration: Convert duration_ms → minutes in Power Query

---

## 🧮 Suggested DAX Measures
*(Adapt table/column names as needed)*

```DAX
Total Songs = COUNTROWS(Songs)
Distinct Artists = DISTINCTCOUNT(Songs[artist_name])
Avg Popularity = AVERAGE(Songs[popularity])
Duration (Minutes) = DIVIDE(Songs[duration_ms], 60000)
Avg Duration (Minutes) = AVERAGE([Duration (Minutes)])

Explicit Songs = CALCULATE(COUNTROWS(Songs), Songs[explicit] = TRUE)
Non-Explicit Songs = CALCULATE(COUNTROWS(Songs), Songs[explicit] = FALSE)
Explicit Share % = DIVIDE([Explicit Songs], [Total Songs])
Non-Explicit Share % = DIVIDE([Non-Explicit Songs], [Total Songs])

Max Popularity by Artist = CALCULATE(MAX(Songs[popularity]), ALLEXCEPT(Songs, Songs[artist_name]))
Avg Popularity by Artist = CALCULATE(AVERAGE(Songs[popularity]), ALLEXCEPT(Songs, Songs[artist_name]))
Top Song Popularity = RANKX(ALL(Songs[song_name]), [Song Popularity], , DESC)
Song Popularity = AVERAGE(Songs[popularity])

Avg Popularity by Month =
    CALCULATE(AVERAGE(Songs[popularity]),
               TREATAS(VALUES('Calendar'[Month]), Songs[month]))

Distinct Songs by Year =
    CALCULATE(DISTINCTCOUNT(Songs[song_name]),
               TREATAS(VALUES('Calendar'[Year]), Songs[year]))

#1 Positions by Artist =
    CALCULATE(COUNTROWS(Songs), Songs[position] = 1)

Avg Tracks per Album = AVERAGEX(VALUES(Albums[album_id]), Albums[track_count])
Songs per Artist = CALCULATE(COUNTROWS(Songs), ALLEXCEPT(Songs, Songs[artist_name]))

```
## 📸 Dashboard Screens (click to view full size)
![Spotify_Index](https://raw.githubusercontent.com/rishikesh199/Spotify_PowerBI/main/Spotify_Index.png).
![Spotify_Overview](https://raw.githubusercontent.com/rishikesh199/Spotify_PowerBI/main/Spotify_Overview.png).
![Spotify_Songs](https://raw.githubusercontent.com/rishikesh199/Spotify_PowerBI/main/Spotify_Songs.png).
![Spotify_Artist](https://raw.githubusercontent.com/rishikesh199/Spotify_PowerBI/main/Spotify_Artist.png).
