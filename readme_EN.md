# [CASE STUDY] Pizza Sales Performance Analysis 🍕

![Status](https://img.shields.io/badge/Status-Phase%202%20Completed-green)
![Technology](https://img.shields.io/badge/Technology-Power%20BI%20%2F%20DAX-yellow)

## 👤 Author
**André Garcia** *Data Analyst transitioning from Cultural Journalism to the Tech Industry. Focused on transforming raw data into strategic intelligence and decision support.*

---

## 📖 About the Project

### Introduction
This repository documents the development of a Business Intelligence (BI) solution for a fictional pizza franchise. The focus is on transforming raw transactional data into business intelligence through DAX modeling. Rather than focusing solely on visuals, I prioritized calculating real margins and profitability to create a strategic foundation for future dashboards and insight reports.

This project aims to turn sales data into strategic indicators to support decision-making, analyzing both commercial performance and the financial health of the operation.

---

### 🚀 Project Objectives
The core objective is to answer critical business questions:
* Which are the top 5 and bottom 5 pizzas by revenue and quantity sold?
* What is the best-selling pizza size?
* What was the month-over-month revenue throughout the year?
* What was the average revenue for each day of the week?

Additionally, the project performs a **comparison between Sales Share and Profit Margin** to guide strategic decisions, such as:
* Identifying which flavors should be the focus of marketing campaigns.
* Analyzing where operational cost reductions are necessary.
* Defining which products should receive promotions or be removed from the menu.
* Determining, based on average revenue, the best day of the week to close the store or reduce operating hours.

---

### 📊 Data Modeling
The measures created using DAX code are demonstrated and commented on in the [dax.md](https://github.com/amdreh/pizza_sales/blob/main/1_modelagem_dax/dax.md) file, categorized as follows:

1. Pizza sales by flavor
2. Pizza sales by size
3. Monthly/Quarterly sales performance
4. Average revenue per day of the week
5. Profit Margin vs. Sales Share

---

### 🧠 Methodology and Development
In the first phase, I utilized DAX to implement robust business rules for revenue analysis:

1. **Real Margin Calculation:** Implementation of logic to estimate pizza costs by category (Veggie, Classic, Chicken, Supreme), considering variable operational costs.
2. **Performance Matrix:** Cross-referencing *Share* (Popularity) and *Margin* (Profitability) to strategically classify the product mix.
3. **Star Ranking:** Creation of a dynamic rating system to facilitate the visual interpretation of each flavor's performance within the model.

---

### 📂 Repository Structure
The project files are organized as follows:

* **1_modelagem_dax**: Contains the [dax.md](https://github.com/amdreh/pizza_sales/blob/main/1_modelagem_dax/dax.md) file, featuring documentation and explanations for each created measure.
* **2_dashboard**: Reserved for dashboards that answer the proposed business questions. *(In development)*
* **3_relatorio**: Space for the comparative analytical report between share and margin. *(In development)*
* **data**: Original database (.csv files) sourced from Kaggle.
* **README.md**: Main documentation and project presentation.

---

### 🛠️ Technologies Used
* **Power BI / DAX:** Data modeling and Business Intelligence.
* **Markdown:** Technical documentation and project structuring.
* **GitHub:** Version control and portfolio hosting.

---

### 📅 Roadmap
- [x] **Phase 1:** Data modeling, relationships, and DAX dictionary.
- [x] **Phase 2:** Development of the interactive Power BI dashboard (UX/UI Design).
- [ ] **Phase 3:** Publication of the final insights and recommendations report.

---
**Developed by André Garcia** *Data Analyst in Transition*
