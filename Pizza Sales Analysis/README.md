# Pizza Sales Analysis

## Executive Summary

This project analyses a full pizza restaurant operation — sales, inventory, and staffing — by designing a relational SQL Server data warehouse and building a four-page interactive Power BI dashboard on top of it. SQL views pre-join and aggregate order, ingredient, inventory, and staff-rota data to power revenue, cost, and workforce reporting, giving the business a single, queryable source of truth across sales performance, ingredient stock levels, labor cost, and customer behaviour.


## Project Objectives

- Design a normalised SQL Server database covering customers, orders, items, ingredients, inventory, staff, and shifts
- Build analytical SQL views to pre-join and aggregate data for reporting
- Track sales performance — revenue, order volume, order value, and product mix
- Monitor ingredient usage and stock levels against inventory
- Analyse staff scheduling and labor cost by shift and position
- Understand customer ordering behaviour and delivery patterns
- Visualise all of the above in an interactive, multi-page Power BI dashboard

## Overview of the Data

The database, **PizzaSalesDW**, is structured around eight core tables:

- **Customers** — customer ID and name
- **Address** — delivery addresses linked to orders
- **Items** — pizza/menu items, including SKU, category, size, and price
- **Ingredients** — ingredient ID, name, weight, unit of measurement, and price
- **Inventory** — stock quantity per ingredient
- **Recipe** — maps ingredients and required quantities to each menu item
- **Staff** — staff members, position, and hourly rate
- **Shifts** / **Rotations** — shift definitions and the staff-to-shift schedule by date
- **Orders** — each customer order, linking item, quantity, delivery flag, and address

## Database Design & Analytical Views

Four SQL views sit on top of the base tables to simplify reporting and pre-compute key metrics:

- **`query_overview1`** — Order Overview: joins Orders, Items, Address, and Customers into a single order-level table (item, category, price, delivery address, and time of order) — the base table for all sales analysis.
- **`stock1`** — Stock & Ingredient Cost Analysis: joins Orders → Items → Recipe → Ingredients to compute ordered weight and ingredient cost per item, using `ingredient price ÷ ingredient weight` as the unit cost.
- **`query_inventory1`** — Inventory Analysis: compares total ordered ingredient weight against on-hand inventory weight to calculate `remaining_weight` per ingredient.
- **`query_staff1`** — Staff Cost Analysis: joins Rotations, Staff, and Shifts, calculating hours worked per shift (handling overnight shifts that cross midnight) and the resulting staff cost (`hours × hourly_rate`).

## Power BI Dashboard

The report is built as four linked pages, each driven by the SQL views above:

### 1. Dashboard (Sales Overview)
Headline sales KPIs — **Total Revenue, Total Orders, Avg Order Value, and Net Profit** — alongside sales by pizza category/name, order volume by hour, order type breakdown, and a geographic map of delivery cities, with slicers for interactive filtering.

### 2. Inventory & Ingredient Cost
Tracks **Total Ingredient Cost, Pizza Cost per item, and Most Used Ingredient**, alongside **Inventory Utilization %**, **Low Stock Count**, and **Percent Remaining** per ingredient — giving a clear view of stock health against ordered demand.

### 3. Staff & Labor Cost
Summarises **Total Staff Cost** and **Avg Hourly Cost**, broken down by staff position and hours worked per shift, to understand labor cost drivers across the rota.

### 4. Customer Insights
A searchable customer order table (name, delivery address/city, items ordered) with slicer-based filtering, supporting lookups into individual customer ordering behaviour and delivery patterns.

## Tech Stack

- **Database:** Microsoft SQL Server
- **Concepts:** Table design & foreign keys, analytical views, subqueries, CASE expressions, DATEDIFF-based shift calculations, cost/utilization calculated columns
- **Visualization:** Power BI (DAX measures, interactive slicers, map visual, drill-through pages)

## Conclusion

This project demonstrates an end-to-end SQL-to-BI workflow: a normalised relational schema, SQL views that translate raw transactional and operational data into report-ready metrics, and a Power BI dashboard that surfaces sales, inventory, staffing, and customer insights in one place — supporting decisions on pricing, stock replenishment, staffing levels, and customer/delivery strategy.



[PowerBI Dashobaord Link](https://app.powerbi.com/view?r=eyJrIjoiOGFiMTg2ZjMtNWJjYi00YzkyLWIzNTctY2IxMmU2YjQyMTljIiwidCI6IjUxYTBhNjljLTBlNGYtNGIzZC1iNjQyLTEyZTAxMzE5ODYzNSIsImMiOjh9)
