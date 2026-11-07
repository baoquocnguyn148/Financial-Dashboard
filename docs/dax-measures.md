# Danh mục Measures — `_Measure_Finance`

**97 measures** · **6 nhóm chức năng** · **11 thư mục con** — mỗi measure có mô tả nghiệp vụ/guardrail ngay trong semantic model.

> Đơn vị tiền tệ: **tỷ VND** (các measure tài chính chia `1.000.000.000`).

## Cấu trúc

| Nhóm | Thư mục con | Số measure |
|---|---|---|
| **01 Tài chính** | Doanh thu, Lợi nhuận & biên, Chi phí, Định dạng, Kế hoạch | 60 |
| **02 Ngân sách** | — | 7 |
| **03 Công nợ** | — | 14 |
| **04 Bán hàng** | — | 9 |
| **05 Nguồn vốn** | — | 5 |
| **06 Thời gian** | — | 1 |
| **Khác** | — | 1 |

## 01 Tài chính

### Doanh thu

| Measure | DAX | Mô tả / guardrail |
|---|---|---|
| **Total Revenue** | `SUM(Fact_Finance_GL[Revenue_VND]) / 1000000000` | — |
| **OEM Revenue** | `SUM(Fact_Finance_GL[OEM_Revenue_VND]) / 1000000000` | — |
| **YTD Revenue** | `IF(HASONEVALUE(Dim_Date[FiscalYear]), CALCULATE([Total Revenue], DATESYTD(Dim_Date[Date], "09/30")), BLANK())` | — |
| **Revenue PY** | `CALCULATE([Total Revenue], SAMEPERIODLASTYEAR(Dim_Date[Date]))` | — |
| **Revenue YoY Growth %** | `DIVIDE([Total Revenue] - [Revenue PY], [Revenue PY])` | — |
| **SPTT Revenue** | `SUM(Fact_Finance_GL[SPTT_Revenue_VND]) / 1000000000` | — |
| **SPTM Revenue** | `SUM(Fact_Finance_GL[SPTM_Revenue_VND]) / 1000000000` | — |
| **Revenue Trend** | `[Total Revenue]` | — |
| **Revenue PY Trend** | `[Revenue PY]` | — |
| **OEM Revenue Visible** | `IF([OEM Revenue] = 0, BLANK(), [OEM Revenue])` | — |
| **Revenue Contribution %** | `DIVIDE([Total Revenue], CALCULATE([Total Revenue], REMOVEFILTERS(Dim_Store)))` | — |
| **Revenue YTD PY** | `CALCULATE([YTD Revenue], SAMEPERIODLASTYEAR(Dim_Date[Date]))` | — |
| **Revenue YTD YoY %** | `DIVIDE([YTD Revenue] - [Revenue YTD PY], [Revenue YTD PY], BLANK())` | — |
| **OEM Revenue MTD** | `CALCULATE([OEM Revenue], DATESMTD(Dim_Date[Date]))` | — |
| **OEM Revenue YTD** | `IF(HASONEVALUE(Dim_Date[FiscalYear]), CALCULATE([OEM Revenue], DATESYTD(Dim_Date[Date], "09/30")), BLANK())` | — |
| **Product Revenue Share %** | `DIVIDE([Total Revenue], CALCULATE([Total Revenue], REMOVEFILTERS(Dim_ProductCategory)))` | — |

### Lợi nhuận & biên

| Measure | DAX | Mô tả / guardrail |
|---|---|---|
| **Gross Profit** | `SUM(Fact_Finance_GL[GrossProfit_VND]) / 1000000000` | — |
| **EBITDA** | `SUM(Fact_Finance_GL[EBITDA_VND]) / 1000000000` | — |
| **Net Profit** | `SUM(Fact_Finance_GL[NetProfit_VND]) / 1000000000` | — |
| **Gross Margin %** | `DIVIDE([Gross Profit], [Total Revenue])` | — |
| **EBITDA Margin %** | `DIVIDE([EBITDA], [Total Revenue])` | — |
| **Net Profit Margin %** | `DIVIDE([Net Profit], [Total Revenue])` | — |
| **Gross Margin LY %** | `IF(ISBLANK([Revenue PY]), BLANK(), CALCULATE([Gross Margin %], SAMEPERIODLASTYEAR(Dim_Date[Date])))` | — |
| **EBITDA LY** | `CALCULATE([EBITDA], SAMEPERIODLASTYEAR(Dim_Date[Date]))` | — |
| **EBITDA YoY %** | `DIVIDE([EBITDA] - [EBITDA LY], [EBITDA LY])` | — |
| **Gross Profit YTD** | `CALCULATE([Gross Profit], DATESYTD(Dim_Date[Date], "09/30"))` | — |
| **EBITDA YTD** | `CALCULATE([EBITDA], DATESYTD(Dim_Date[Date], "09/30"))` | — |
| **Gross Margin YTD %** | `DIVIDE([Gross Profit YTD], [YTD Revenue], BLANK())` | — |
| **OEM Region Share %** | `DIVIDE([OEM Revenue], CALCULATE([OEM Revenue], REMOVEFILTERS(Dim_Region)))` | — |
| **Gross Profit LY** | `CALCULATE([Gross Profit], SAMEPERIODLASTYEAR(Dim_Date[Date]))` | — |
| **Gross Profit YoY %** | `DIVIDE([Gross Profit] - [Gross Profit LY], [Gross Profit LY])` | — |
| **Gross Margin YoY pp** | `IF(ISBLANK([Gross Margin LY %]), BLANK(), ([Gross Margin %] - [Gross Margin LY %]) * 100)` | — |
| **Net Profit LY** | `CALCULATE([Net Profit], SAMEPERIODLASTYEAR(Dim_Date[Date]))` | — |
| **Net Profit YoY %** | `DIVIDE([Net Profit] - [Net Profit LY], [Net Profit LY])` | — |

### Chi phí

| Measure | DAX | Mô tả / guardrail |
|---|---|---|
| **SG&A Expense** | `SUM(Fact_Finance_GL[SGA_Expense_VND]) / 1000000000` | — |
| **SG&A Ratio %** | `DIVIDE([SG&A Expense], [Total Revenue])` | — |
| **COGS** | `SUM(Fact_Finance_GL[COGS_VND]) / 1000000000` | — |
| **Depreciation** | `SUM(Fact_Finance_GL[Depreciation_VND]) / 1000000000` | — |
| **Interest Expense** | `SUM(Fact_Finance_GL[InterestExpense_VND]) / 1000000000` | — |
| **Tax Expense** | `SUM(Fact_Finance_GL[TaxExpense_VND]) / 1000000000` | — |
| **Discount Amount GL** | `SUM(Fact_Finance_GL[Discount_VND]) / 1000000000` | — |
| **SG&A YTD** | `CALCULATE([SG&A Expense], DATESYTD(Dim_Date[Date], "09/30"))` | — |
| **SG&A Ratio YTD %** | `DIVIDE([SG&A YTD], [YTD Revenue], BLANK())` | — |
| **Discount Rate GL %** | `DIVIDE([Discount Amount GL], [Total Revenue], BLANK())` | — |

### Định dạng

| Measure | DAX | Mô tả / guardrail |
|---|---|---|
| **Color_Variance_EBITDA** | `IF([EBITDA] >= 0, "#36B37E", "#FF5630")` | — |
| **Color_Variance_GrossProfit** | `IF([Gross Profit] >= 0, "#36B37E", "#FF5630")` | — |
| **Color_KPI_Revenue** | `IF([Revenue YoY Growth %] >= 0, "#36B37E", "#FF5630")` | — |
| **Color_KPI_EBITDA** | `IF([EBITDA YoY %] >= 0, "#36B37E", "#FF5630")` | — |
| **Color_KPI_GrossProfit** | `IF([Gross Profit YoY %] >= 0, "#36B37E", "#FF5630")` | — |
| **Color_KPI_GrossMargin** | `IF([Gross Margin YoY pp] >= 0, "#36B37E", "#FF5630")` | — |
| **Color_KPI_Budget** | `IF([YTD Budget Variance] >= 0, "#36B37E", "#FF5630")` | — |
| **Color_KPI_NetProfit** | `IF([Net Profit YoY %] >= 0, "#36B37E", "#FF5630")` | — |

### Kế hoạch

| Measure | DAX | Mô tả / guardrail |
|---|---|---|
| **Budget Variance** | `IF([Comparable Budget] > 0, [Total Revenue] - [Comparable Budget], BLANK())` | — |
| **Budget Achievement %** | `IF([Comparable Budget] > 0, DIVIDE([Total Revenue], [Comparable Budget]), BLANK())` | — |
| **Comparable Budget Trend** | `[Comparable Budget]` | — |
| **Budget Variance Trend** | `IF([Comparable Budget Trend] > 0, [Revenue Trend] - [Comparable Budget Trend], BLANK())` | — |
| **EBITDA YoY Variance** | `[EBITDA] - [EBITDA LY]` | — |
| **YTD Budget Achievement %** | `DIVIDE([YTD Revenue], [YTD Budget], BLANK())` | — |
| **YTD Budget Variance** | `IF([YTD Budget] > 0, [YTD Revenue] - [YTD Budget], BLANK())` | — |
| **YTD Budget Variance %** | `IF([YTD Budget] > 0, DIVIDE([YTD Budget Variance], [YTD Budget]), BLANK())` | — |

## 02 Ngân sách

| Measure | DAX | Mô tả / guardrail |
|---|---|---|
| **Total Budget** | `IF(DISTINCTCOUNT(Fact_Budget[BudgetVersion]) = 1, SUM(Fact_Budget[Budget_Revenue_VND]) / 1000000000, BLANK())` | Chỉ công bố kế hoạch khi ngữ cảnh có đúng một phiên bản ngân sách. |
| **Budget Scale Factor** | `1` | — |
| **Comparable Budget** | `[Total Budget]` | — |
| **Budget Gross Profit** | `IF(DISTINCTCOUNT(Fact_Budget[BudgetVersion]) = 1, SUM(Fact_Budget[Budget_GrossProfit]) / 1000000000, BLANK())` | Chỉ so sánh lợi nhuận gộp với một phiên bản ngân sách trong ngữ cảnh hiện tại. |
| **Budget Volume (Ton)** | `SUM(Fact_Budget[Budget_Volume_Ton])` | — |
| **YTD Budget** | `IF(HASONEVALUE(Dim_Date[FiscalYear]), CALCULATE([Comparable Budget], DATESYTD(Dim_Date[Date], "09/30")), BLANK())` | — |
| **Gross Profit Budget Variance** | `IF(NOT ISBLANK([Gross Profit]) && NOT ISBLANK([Budget Gross Profit]), [Gross Profit] - [Budget Gross Profit], BLANK())` | Chênh lệch theo kỳ lọc, không phải chênh lệch lũy kế. |

## 03 Công nợ

| Measure | DAX | Mô tả / guardrail |
|---|---|---|
| **Total Debt** | `SUM(Fact_Debt[OutstandingBalance_VND])` | — |
| **Bad Debt** | `CALCULATE([Total Debt], Fact_Debt[IsBadDebt] = TRUE())` | — |
| **Bad Debt Ratio** | `DIVIDE([Bad Debt], [Total Debt], 0)` | — |
| **Total Credit Limit** | `SUM(Fact_Debt[CreditLimit_VND])` | — |
| **Credit Utilization %** | `DIVIDE([Total Debt], [Total Credit Limit], 0)` | — |
| **Overdue Debt** | `CALCULATE([Total Debt], Fact_Debt[IsOverdue] = TRUE())` | — |
| **Overdue Ratio** | `DIVIDE([Overdue Debt], [Total Debt], 0)` | — |
| **Near Due Debt** | `CALCULATE([Total Debt], Fact_Debt[IsNearDue] = TRUE())` | — |
| **Unsecured Debt** | `CALCULATE([Total Debt], Fact_Debt[IsGuaranteed] = FALSE())` | — |
| **Unsecured Ratio** | `DIVIDE([Unsecured Debt], [Total Debt], 0)` | — |
| **Days Until Due** | `MIN(Fact_Debt[DaysUntilDue])` | — |
| **Discount & Rebate** | `VAR Amount = SUM(Fact_Debt[MonthlyDiscount_VND]) + SUM(Fact_Debt[MonthlyRebate_VND]) RETURN IF(Amount = 0, BLANK(), Amount)` | — |
| **DSO** | `AVERAGE(Fact_DSO[DSO_Days])` | — |
| **ECL Provision** | `SUM(Fact_Provision[ProvisionExpense_VND])` | — |

## 04 Bán hàng

| Measure | DAX | Mô tả / guardrail |
|---|---|---|
| **Sales Revenue** | `SUM(Fact_Sales[Revenue_VND])` | — |
| **Sales Volume (Ton)** | `SUM(Fact_Sales[Quantity_Ton])` | — |
| **# Orders** | `DISTINCTCOUNT(Fact_Sales[OrderID])` | — |
| **Sales Gross Margin %** | `DIVIDE(SUM(Fact_Sales[GrossProfit_VND]), SUM(Fact_Sales[Revenue_VND]), 0)` | — |
| **Avg Unit Price** | `DIVIDE(SUM(Fact_Sales[Revenue_VND]), SUM(Fact_Sales[Quantity_Ton]), 0)` | — |
| **Total Discount (Sales)** | `SUM(Fact_Sales[Discount_Amount_VND])` | — |
| **Discount Rate (Sales) %** | `DIVIDE([Total Discount (Sales)], [Sales Revenue])` | — |
| **Discount Amount (Sales) Tỷ** | `DIVIDE([Total Discount (Sales)], 1000000000)` | Tỷ lệ chiết khấu dùng cùng fact và cùng thời điểm với doanh thu đơn hàng. |
| **Sales Revenue Tỷ** | `DIVIDE([Sales Revenue], 1000000000)` | — |

## 05 Nguồn vốn

| Measure | DAX | Mô tả / guardrail |
|---|---|---|
| **Total Assets** | `BLANK()` | Bảng cân đối chưa được liên kết theo ngày/BU; không cộng nhiều snapshot. |
| **Equity** | `BLANK()` | Chưa có vốn chủ sở hữu bình quân theo kỳ chọn. |
| **ROE** | `BLANK()` | Chưa đủ quan hệ snapshot và vốn chủ sở hữu bình quân để công bố ROE. |
| **ROIC** | `BLANK()` | Không dùng công nợ phải thu làm nợ vay; cần NOPAT và invested capital bình quân. |
| **Color_KPI_ROE** | `"#36B37E"` | — |

## 06 Thời gian

| Measure | DAX | Mô tả / guardrail |
|---|---|---|
| **DB06 Period Context** | `IF(HASONEVALUE(Dim_Date[FiscalYear]), "NĐTC " & FORMAT(SELECTEDVALUE(Dim_Date[FiscalYear]), "0") & " · " & FORMAT(COUNTROWS(VALUES(Dim_Date[FiscalMonth])), "0") & " tháng được chọn", "NHIỀU NĐTC") & " · DỮ LIỆU MẪU, CHƯA ĐỐI SOÁT"` | — |

## Khác

| Measure | DAX | Mô tả / guardrail |
|---|---|---|
| **Color_GP_Budget_Variance** | `IF([Gross Profit Budget Variance] >= 0, "#3B82F6", "#FF5630")` | — |

---

*Danh mục được trích xuất trực tiếp từ semantic model của file PBIX; nội dung DAX giữ nguyên.*
