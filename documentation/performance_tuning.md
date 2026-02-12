# ⚡ High-Performance DAX Tuning

## 1. Understanding Cardinality
The VertiPaq engine compresses data by looking for unique values.
- **Problem:** High-cardinality columns (like Order IDs or precise Timestamps) consume massive amounts of memory.
- **Solution:** Remove unnecessary ID columns. Split `DateTime` into separate `Date` and `Time` columns to improve compression ratios.



## 2. Row Context vs. Filter Context
- **Iterators (`SUMX`, `AVERAGEX`):** These create a row context. They are computationally expensive on large tables.
- **Strategy:** Only use `SUMX` if you need to perform a calculation *before* aggregating (e.g., `SUMX(Table, Price * Quantity)`). If you just need a sum, use `SUM(Column)`.

## 3. Variables as Performance Boosters
Variables in DAX are **lazy and static**. 
- They are calculated only once within the measure's scope.
- **Performance Gain:** If you reference `[Total Sales]` four times in an `IF` statement, DAX might calculate it four times. Assigning it to a `VAR` ensures it is calculated only once.

## 4. Star Schema Optimization
This repository assumes a **Star Schema** layout. Snowflake schemas or "Flat Tables" lead to complex DAX and slow "Relationship Propagation."
- Fact tables should contain quantitative data.
- Dimension tables should contain descriptive attributes.
