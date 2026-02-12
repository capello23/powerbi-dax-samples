# 🛠️ DAX Best Practices & Standards

## 1. The "Golden Rule" of Naming
To ensure the model is intuitive for both developers and end-users:
- **Measures:** Always use standalone names (e.g., `Total Revenue`). **Never** prefix them with table names.
- **Columns:** Always include the table name (e.g., `Fact_Orders[Sales]`).
- **Logic:** This distinction allows you to identify at a glance whether a value is an aggregate (measure) or a raw data point (column).

## 2. Formatting & Readability
We follow the "DAX Formatter" standard (by SQLBI). 
- Use **Variables (VAR/RETURN)** to break down complex logic.
- Use indentation for nested functions like `CALCULATE`.
- Provide comments for "Magic Numbers" (e.g., `VAR LeadTimeThreshold = 5 // Days`).

## 3. Defensive Programming with `DIVIDE`
The `/` operator is prone to `Divide by Zero` errors which return `Infinity` or `NaN` in visuals. 
- **Standard:** `DIVIDE( [Numerator], [Denominator], 0 )`
- **Benefit:** Ensures that if a category has no sales, the visual remains clean or shows a zero instead of an error.

## 4. Avoiding "Naked Columns"
Never use a column directly in a visual (e.g., dragging `Sales` to a chart). 
- **Rule:** Every data point must be wrapped in a measure. 
- **Why?** If you later need to change the logic (e.g., excluding tax from sales), you change it in one measure rather than updating every single chart in the report.

## 5. Boolean Logic in Filters
When using `CALCULATE`, prefer filtering on columns rather than using the `FILTER` function unless necessary.
- ✅ `CALCULATE([Sales], DimProduct[Color] = "Red")`
- ❌ `CALCULATE([Sales], FILTER(DimProduct, DimProduct[Color] = "Red"))`
- *Reason:* The first method is optimized by the VertiPaq engine as a simple lookup.
