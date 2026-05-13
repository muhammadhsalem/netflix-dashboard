# Netflix Content Analysis Dashboard
### Tools: Excel · Power Query · Power BI

A 2-page interactive dashboard analyzing Netflix titles across genres, countries, ratings, and content type — built on a normalized star-schema data model with 6 related tables.

---

## Dashboard Preview

> Add screenshots here after exporting from Power BI Desktop (File → Export → Export to PDF / use Snipping Tool per page)

| Page | Description |
|---|---|
| <img width="1808" height="1021" alt="Screenshot 2026-05-13 193732" src="https://github.com/user-attachments/assets/508febf7-270a-4cce-ba80-293160194f25" /> | Overview page — trends, genres, map, ratings |
| <img width="1803" height="1018" alt="Screenshot 2026-05-13 193652" src="https://github.com/user-attachments/assets/5c073ac8-7be4-4290-aee7-38b3cf7d77f8" /> | Detail page — cards, pivot tables, country map |

---

## Data Model

The raw Netflix dataset was split and normalized into **6 related tables** using Power Query:

| Table | Key columns |
|---|---|
| `netflix info` | show_id, title, type, rating, date_added, release_year, description |
| `netflix category` | category (genre) |
| `netflix country_released` | country |
| `netflix cast` | cast |
| `netflix director` | director |

> Power Query was used to unpack multi-value fields (genres, countries, cast) into separate normalized tables — a proper star-schema model rather than a flat file.

---

## Dashboard Pages

### Page 1 — Overview
| Visual | Type | Fields |
|---|---|---|
| Shows added by Date | Area chart | date_added (year hierarchy), COUNT(show_id), type |
| Top 10 Genres | Bar chart | category, COUNT(show_id) |
| Countries' Shows count | Azure Map | country, COUNT(show_id) |
| Shows by Rating | Column chart | rating, COUNT(show_id), type (Movie/TV Show) |

### Page 2 — Detail / Explorer
| Visual | Type | Fields |
|---|---|---|
| Countries' Shows count | Azure Map | country, COUNT(show_id) |
| Rating | Card | rating |
| Release Year | Card | release_year |
| Movie/TV Show | Slicer | title (filtered by type) |
| Genre table | Pivot table | category |
| Director table | Pivot table | director |
| Cast table | Pivot table | cast |

---

## Key Data Preparation Steps (Power Query)

1. **Loaded raw Netflix CSV** — 6,000+ rows with multi-value columns (genres, countries, cast as comma-separated strings)
2. **Split multi-value columns** — used `Text.Split` and `Table.ExpandListColumn` to unpivot genres, countries, and cast into separate rows
3. **Created normalized tables** — each entity (cast, director, category, country) became its own query/table
4. **Handled missing values** — replaced nulls in `director`, `cast`, `country`, and `date_added`
5. **Standardized date formats** — parsed `date_added` into proper Date type and extracted year hierarchy
6. **Built relationships** — linked all tables back to `netflix info` via show_id

---

## Key Insights

- Content volume grew significantly year-over-year, with peak additions in the 2018–2020 period
- **Movies outnumber TV Shows** across the catalogue
- **International Drama, Comedies, and Documentaries** are the top genres
- The **US, India, and UK** dominate content origin
- TV-MA and TV-14 are the most common ratings, covering the majority of titles

---

## Files

| File | Description |
|---|---|
| `screenshots/overview.png` | Page 1 — trends, genres, map, ratings |
| `screenshots/detail_explorer.png` | Page 2 — cards, pivot tables, country map |

**[▶ View live dashboard on Power BI](https://app.powerbi.com/view?r=eyJrIjoiZWI5MDhmNzQtYzM0OS00NmNiLWEzY2MtMjFhNzdkYmVhZWQ4IiwidCI6ImVhZjYyNGM4LWEwYzQtNDE5NS04N2QyLTQ0M2U1ZDc1MTZjZCIsImMiOjh9)**
