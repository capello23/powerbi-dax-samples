# Power BI DAX Samples

Collection of DAX measures for logistics and business intelligence analytics.

## 📊 Overview

This repository contains practical DAX measures I've developed for:
- Cost analysis and tracking
- Time intelligence calculations  
- Logistics KPIs
- Performance comparisons

## 📁 Files

- `logistics-kpis.dax` - Basic cost measures
- `time-intelligence.dax` - Period comparisons and YTD

## 🛠️ Data Model Assumptions

Star schema with:
- Fact tables: `FactInvoice`, `FactSales`
- Dimension tables: `DimDate`, `DimProduct`

**Note:** Adjust table/column names for your model.

## 💡 Usage

1. Power BI Desktop → Modeling → New Measure
2. Copy-paste desired measure
3. Modify references as needed

## 👤 Author

**Kacper Szelukowski**  
Power BI Developer | Data Analyst

📧 k.szelukowski@gmail.com  
💼 [LinkedIn](https://linkedin.com/in/kszelukowski)

## 📝 License

MIT License - Free to use
