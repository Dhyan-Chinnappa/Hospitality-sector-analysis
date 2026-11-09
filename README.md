# 🏨 Hospitality Revenue Analytics Dashboard (Power BI)

An interactive Power BI dashboard that analyses hotel booking performance across **25 properties in 4 Indian cities** (Delhi, Mumbai, Hyderabad, Bangalore) for **May – July 2022**. It tracks revenue, occupancy, ADR, RevPAR and booking realisation, with week-over-week change tracking, so revenue and operations teams can see what is driving (or hurting) performance.

> 📸 Add a screenshot here: `![Dashboard Preview](images/dashboard.png)`

---

## 🎯 Business Problem

A hotel group wants to understand why revenue is changing and where to act. The dashboard answers questions such as:

- How are Revenue, Occupancy, ADR and RevPAR trending week over week?
- Which cities, room classes, hotel categories and booking platforms perform best?
- How much revenue is lost to cancellations and no-shows (realisation)?
- Do weekdays and weekends behave differently?

---

## 📊 Dashboard Pages

| Page | What it shows |
|---|---|
| **Page 1 – Overview** | Headline cards (Revenue, RevPAR, DSRN), a weekly trend of ADR / Occupancy % / RevPAR, Occupancy % by hotel category (donut), a property-level KPI table, and WoW revenue change |
| **Page 2 – Detailed Analysis** | KPI cards (Revenue, Occupancy %, ADR, RevPAR, DSRN, Realisation %) each with a WoW change %, ADR vs Realisation % by booking platform (combo chart), weekday vs weekend breakdown, and a property KPI table |
| **Tooltip pages (6)** | Hover-over detail for Revenue, RevPAR, DSRN, Occupancy %, ADR and Realisation % by week number (split by Weekday/Weekend where relevant) |

**Slicers:** City · Month · Week No · Room Class · Booking Status

---

## 📐 Key Metrics (DAX)

| Measure | Definition |
|---|---|
| **Revenue** | Sum of `revenue_realized` |
| **Total Bookings** | Count of `booking_id` |
| **Total Capacity** | Sum of available room capacity |
| **Occupancy %** | Successful bookings ÷ Capacity |
| **ADR** (Average Daily Rate) | Revenue ÷ Total Bookings |
| **RevPAR** (Revenue per Available Room) | Revenue ÷ Total Capacity |
| **Cancellation %** | Cancelled bookings ÷ Total bookings |
| **No Show Rate %** | No-show bookings ÷ Total bookings |
| **Realisation %** | 1 − (Cancellation % + No Show %) |
| **Average Rating** | Average of guest ratings |
| **DBRN** | Daily Booked Room Nights = Bookings ÷ No. of days |
| **DSRN** | Daily Sellable Room Nights = Capacity ÷ No. of days |
| **DURN** | Daily Utilised Room Nights = Checked-out bookings ÷ No. of days |
| **WoW Change %** | Week-over-week change for Revenue, Occupancy, ADR, RevPAR, Realisation and DSRN |
| **Booking % by Platform / Room Class** | Share of total bookings |

---

## 🗂️ Data Model

Star schema with two fact tables and three dimensions:

```
              Dim_date ──┐
                         ├── fact_bookings            (134,590 rows)
Dim_hotels ──────────────┤
                         ├── fact_aggregated_bookings (9,200 rows)
Dim_rooms ───────────────┘
```

| Table | Type | Key fields |
|---|---|---|
| `fact_bookings` | Fact | booking_id, property_id, booking_date, check_in_date, checkout_date, no_guests, room_category, booking_platform, ratings_given, booking_status, revenue_generated, revenue_realized |
| `fact_aggregated_bookings` | Fact | property_id, check_in_date, room_category, successful_bookings, capacity |
| `Dim_date` | Dimension | date, mmm yy, week no, Day type (Weekday/Weekend) |
| `Dim_hotels` | Dimension | property_id, property_name, category (Luxury/Business), city |
| `Dim_rooms` | Dimension | room_id, room_class (Standard, Elite, Premium, Presidential) |
| `Key_measures` | Measure table | All DAX measures above |

Relationships are many-to-one (single direction) from the facts to the dimensions on `property_id`, `check_in_date` and `room_category`.

---

## 🛠️ Tools & Skills Used

- **Power BI Desktop**: data modelling, report design, tooltip pages
- **Power Query**: CSV ingestion and transformation
- **DAX**: KPI measures, time-intelligence-style WoW logic with variables
- **Star-schema data modelling**
- **Hospitality KPIs**: ADR, RevPAR, Occupancy, Realisation

---

## 🚀 How to Use

1. Clone this repository  
   ```bash
   git clone https://github.com/<your-username>/<your-repo>.git
   ```
2. Open `Mycode.pbix` in **Power BI Desktop**.
3. If the data source path breaks, go to **Home → Transform data → Data source settings** and point the CSV folder to your local copy of the `/data` folder.
4. Refresh and explore using the slicers on each page.

---

## 📁 Repository Structure

```
├── Mycode.pbix        # Power BI dashboard
├── data/              # Source CSV files (dim_date, dim_hotels, dim_rooms, fact_bookings, fact_aggregated_bookings)
├── images/            # Dashboard screenshots
└── README.md
```

---

## 💡 Insights You Can Draw

*(Fill these in from your final numbers)*

- Best / worst performing city by RevPAR
- Platform with the highest realisation vs. highest cancellation
- Weekend vs. weekday gap in occupancy and ADR
- Weeks with the sharpest WoW revenue drop and the likely cause

---

## 👤 Author

**Your Name**  
[LinkedIn](https://linkedin.com/in/your-profile) · [GitHub](https://github.com/your-username)

⭐ If you found this useful, consider starring the repo!
