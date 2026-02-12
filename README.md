# 📊 Power BI DAX Samples for Logistics Analytics

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-E97627?style=for-the-badge&logo=dax&logoColor=white)
![Status](https://img.shields.io/badge/Status-Active-success?style=for-the-badge)

Collection of **production-ready DAX measures** for logistics and supply chain analytics in Power BI. Built from real-world projects processing **500K+ monthly transactions**.

---

## 🎯 What's Inside

This repository contains **25+ DAX measures** across 5 categories:

| Category | Measures | Use Cases |
|----------|----------|-----------|
| **Basic Metrics** | 6 measures | Sales, Orders, Profit, AOV |
| **Time Intelligence** | 5 measures | YoY/MoM growth, YTD, comparisons |
| **Delivery Performance** | 4 measures | On-time %, delays, late deliveries |
| **Advanced Filtering** | 6 measures | CALCULATE patterns, dynamic filters |
| **Performance Optimization** | 4 measures | Variables, optimization techniques |

---

## 🚀 Quick Start

### Prerequisites
- Power BI Desktop (latest version)
- Basic understanding of DAX
- Star schema data model (recommended)

### How to Use

1. **Clone the repository:**
```bash
git clone https://github.com/kszelukowski/powerbi-dax-samples.git
```

2. **Browse measures by category:**
   - Navigate to `/measures/` folder
   - Each `.dax` file contains related measures with comments

3. **Copy-paste into Power BI:**
   - Open your Power BI report
   - Create a new measure
   - Copy the DAX code from the repository
   - Adjust table/column names to match your model

---

## 📚 Measure Categories

### 1️⃣ Basic Metrics (`01_basic_metrics.dax`)

Essential KPIs for any business analytics:
```dax
Total Sales = SUM(Fact_Orders[sales])

Total Orders = COUNTROWS(Fact_Orders)

Average Order Value = DIVIDE([Total Sales], [Total Orders], 0)

Profit Margin % = DIVIDE([Total Profit], [Total Sales], 0)
```

**Use Cases:**
- Executive dashboards
- Sales performance tracking
- Financial reporting

---

### 2️⃣ Time Intelligence (`02_time_intelligence.dax`)

Compare performance across time periods:
```dax
Sales YoY Growth % = 
VAR CurrentYear = [Total Sales]
VAR PreviousYear = [Sales Previous Year]
RETURN
IF(
    NOT ISBLANK(PreviousYear) && PreviousYear <> 0,
    DIVIDE(CurrentYear - PreviousYear, PreviousYear, 0),
    BLANK()
)
```

**Use Cases:**
- Trend analysis
- Year-over-year comparisons
- Seasonal pattern detection

---

### 3️⃣ Delivery Performance (`03_delivery_performance.dax`)

Logistics-specific KPIs:
```dax
On-Time Delivery % = 
VAR OnTime = CALCULATE(COUNTROWS(Fact_Orders), Fact_Orders[is_late] = FALSE)
VAR Total = COUNTROWS(Fact_Orders)
RETURN DIVIDE(OnTime, Total, 0)
```

**Use Cases:**
- Supply chain monitoring
- Carrier performance evaluation
- SLA compliance tracking

---

### 4️⃣ Advanced Filtering (`04_advanced_filtering.dax`)

Complex CALCULATE patterns:
```dax
Top 10 Products Sales = 
CALCULATE(
    [Total Sales],
    TOPN(
        10,
        ALL(DimProduct[product_name]),
        [Total Sales],
        DESC
    )
)
```

**Use Cases:**
- Dynamic top N analysis
- Custom segmentation
- Complex filtering scenarios

---

### 5️⃣ Performance Optimization (`05_performance_optimization.dax`)

Optimized measures using variables:
```dax
Optimized Sales Growth = 
VAR CurrentSales = [Total Sales]
VAR PreviousSales = [Sales Previous Month]
VAR GrowthRate = DIVIDE(CurrentSales - PreviousSales, PreviousSales, 0)
RETURN
IF(NOT ISBLANK(PreviousSales), GrowthRate, BLANK())
```

**Benefits:**
- Faster calculation engine
- Better readability
- Easier debugging

---

## 🏗️ Data Model Requirements

These measures are designed for a **star schema** model:
```
        DimDate
           |
           |
    DimCustomer ← Fact_Orders → DimProduct
                       |
                       ↓
                  DimDelivery
```

### Required Tables:
- `Fact_Orders` - Main transaction table
- `DimDate` - Date dimension (marked as date table)
- `DimProduct` - Product dimension
- `DimCustomer` - Customer dimension

### Required Columns (adjust names in DAX):
- `Fact_Orders[sales]` - Sales amount
- `Fact_Orders[is_late]` - Boolean for late delivery
- `Fact_Orders[delivery_delay_days]` - Numeric delay
- `DimDate[Date]` - Date column

---

## 💡 Real-World Implementation

These measures were battle-tested in production environments:

### DataCo Supply Chain Analytics Dashboard
**Project:** [PowerBI-DataCo-SupplyChain](https://github.com/kszelukowski/PowerBI-DataCo-SupplyChain)

**Stats:**
- 📊 180K+ transactions analyzed
- ⚡ 60% faster load time through optimization
- 📈 15+ production measures deployed
- ✅ 500K+ monthly transaction processing

**Key Results:**
- Reduced weekly reporting from 8 hours to 45 minutes (89% reduction)
- Enabled real-time delivery performance monitoring
- Identified 42.7% on-time delivery rate → triggered improvement initiatives

---

## 📖 Documentation

### Best Practices Guide
👉 [DAX Best Practices](documentation/dax_best_practices.md)

Topics covered:
- Naming conventions
- Variable usage
- CALCULATE patterns
- Filter context management
- Performance optimization

### Performance Tips
👉 [Performance Optimization]([documentation/performance_tuning.md])

Topics covered:
- Using variables effectively
- Avoiding expensive operations
- DirectQuery vs Import considerations
- Aggregation strategies

---

## 🎓 Learning Resources

### Measures by Complexity:

**Beginner** (Basic aggregations):
- `Total Sales`, `Total Orders`, `Average Order Value`

**Intermediate** (Time Intelligence):
- `Sales YoY Growth %`, `Sales MoM Growth %`, `Sales YTD`

**Advanced** (Complex filtering):
- `Top 10 Products Sales`, `Sales High Value Customers`

---

## 🛠️ Customization Guide

### Adapting to Your Model

1. **Update table names:**
```dax
// Replace "Fact_Orders" with your fact table name
Total Sales = SUM(YourFactTable[sales_column])
```

2. **Adjust column references:**
```dax
// Replace column names to match your schema
On-Time Delivery % = 
CALCULATE(
    COUNTROWS(YourFactTable),
    YourFactTable[YourLateFlagColumn] = FALSE
)
```

3. **Modify date table reference:**
```dax
// Replace "DimDate" with your date table name
Sales YTD = TOTALYTD([Total Sales], YourDateTable[DateColumn])
```

---

## 📊 Example Use Cases

### Use Case 1: Executive Dashboard
**Required Measures:**
- `Total Sales`
- `Profit Margin %`
- `Sales YoY Growth %`
- `Sales YTD`

**Visual Recommendations:**
- KPI cards for key metrics
- Line chart for sales trend with YTD
- Donut chart for profit margin by category

---

### Use Case 2: Delivery Performance Dashboard
**Required Measures:**
- `On-Time Delivery %`
- `Average Delivery Delay`
- `Late Deliveries Count`

**Visual Recommendations:**
- Gauge chart for on-time % (target: 95%)
- Table with performance by shipping mode
- Area chart showing trend over time

---

### Use Case 3: Product Analytics
**Required Measures:**
- `Top 10 Products Sales`
- `Products Sold`
- `Average Order Value`

**Visual Recommendations:**
- Bar chart for top products
- Treemap for category hierarchy
- Matrix with conditional formatting

---

## 🤝 Contributing

Contributions are welcome! Here's how:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/new-measure`)
3. Add your DAX measure with comments
4. Update documentation
5. Submit a pull request

### Contribution Guidelines:
- ✅ Include clear comments explaining the measure
- ✅ Provide use case examples
- ✅ Test with sample data
- ✅ Follow existing naming conventions

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

You are free to:
- ✅ Use these measures in commercial projects
- ✅ Modify and adapt to your needs
- ✅ Share with your team
- ✅ Include in your Power BI templates

---

## 🙏 Acknowledgments

- Built from production experience with **500K+ monthly transactions**
- Tested across multiple industries: Logistics, Supply Chain, Manufacturing
- Optimized through real-world performance challenges
- Community feedback from Power BI developers

---

## 👨‍💻 Author

**Kacper Szelukowski**  
*Power BI Developer | Data Analytics Specialist*

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/kszelukowski/)
[![GitHub](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/kszelukowski)
[![Email](https://img.shields.io/badge/Email-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:k.szelukowski@gmail.com)

---

## 📈 Repository Stats

![GitHub stars](https://img.shields.io/github/stars/kszelukowski/powerbi-dax-samples?style=social)
![GitHub forks](https://img.shields.io/github/forks/kszelukowski/powerbi-dax-samples?style=social)
![GitHub watchers](https://img.shields.io/github/watchers/kszelukowski/powerbi-dax-samples?style=social)

---

## 🔗 Related Projects

- [DataCo Supply Chain Analytics](https://github.com/kszelukowski/PowerBI-DataCo-SupplyChain) - Full Power BI dashboard implementation
- [Python ETL Scripts](https://github.com/kszelukowski) - Data preprocessing for Power BI

---

⭐ **If you find this repository helpful, please give it a star!** ⭐

*Last updated: January 2026*
