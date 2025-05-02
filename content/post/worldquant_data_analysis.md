---
date: '2025-04-25T11:10:10+08:00'
draft: false
title: 'Worldquant数据字段分析'
categories:
  - quantitive
keywords:
  - quant alpha
  - worldquant brain
tags:
  - quant alpha
  - worldquant brain
mathjax: true
---

# 量价数据集

## 基础字段

| id | description | type | coverage | userCount | alphaCount |
| --- | --- | --- | --- | --- | --- |
| adv20 | Average daily volume in past 20 days | MATRIX | 1.0 | 8077 | 62668 |
| cap | Daily market capitalization (in millions) | MATRIX | 1.0 | 12379 | 90367 |
| close | Daily close price | MATRIX | 1.0 | 23475 | 259573 |
| country | Country grouping | GROUP | 1.0 | 714 | 9994 |
| currency | Currency | GROUP | 0.0 | 77 | 197 |
| dividend | Dividend | MATRIX | 1.0 | 2220 | 6728 |
| exchange | Exchange grouping | GROUP | 1.0 | 957 | 44853 |
| high | Daily high price | MATRIX | 1.0 | 7389 | 36930 |
| industry | Industry grouping | GROUP | 1.0 | 7088 | 94583 |
| low | Daily low price | MATRIX | 1.0 | 7096 | 31347 |
| market | Market grouping | GROUP | 1.0 | 4094 | 39544 |
| open | Daily open price | MATRIX | 1.0 | 6740 | 33858 |
| returns | Daily returns | MATRIX | 1.0 | 11831 | 79329 |
| sector | Sector grouping | GROUP | 1.0 | 5958 | 78522 |
| sedol | Sedol | GROUP | 0.0 | 6 | 12 |
| sharesout | Daily outstanding shares (in millions) | MATRIX | 1.0 | 3179 | 18426 |
| split | Stock split ratio | MATRIX | 1.0 | 841 | 8393 |
| subindustry | Subindustry grouping | GROUP | 1.0 | 10643 | 91179 |
| volume | Daily volume | MATRIX | 1.0 | 13154 | 69987 |
| vwap | Daily volume weighted average price | MATRIX | 1.0 | 11420 | 45953 |


# 基本面数据

## 基础

公司基础数据主要从三个主要财务报表中提取：

1. **资产负债表**: 提供了公司财务状况的快照，详细列出了其资产、负债和所有者权益。
2. **利润表**: 展示了公司的盈利能力，说明了在扣除各种费用后，收入是如何转化为利润的。
3. **现金流量表**: 通过追踪经营活动、投资活动和筹资活动产生的现金流入和流出，揭示了公司的流动性。

基本面数据通常具有如下特征：
1. 更新频率低：一般每季度、半年或每年更新一次
2. 披露周期因上市交易所和公司规模而异
3. 与量价数据不同，基本面数据的更新可能不连续


通过基础数据使了解一家公司的实际业务状况成为可能。可用作预测未来增长潜力的基本材料，并成为公司估值的关键要素。

## fundamental6数据库

| id | description | type | coverage | userCount | alphaCount |
| --- | --- | --- | --- | --- | --- |
| assets | Assets - Total | MATRIX | 0.9524 | 20049 | 58890 |
| assets_curr | Current Assets - Total | MATRIX | 0.7655 | 1706 | 9761 |
| bookvalue_ps | Book Value Per Share | MATRIX | 0.9754 | 1618 | 7701 |
| capex | Capital Expenditures | MATRIX | 0.9646 | 6648 | 18006 |
| cash | Cash | MATRIX | 0.7529 | 1527 | 9298 |
| cash_st | Cash and Short-Term Investments | MATRIX | 0.9463 | 974 | 6915 |
| cashflow | Cashflow (Annual) | MATRIX | 0.9251 | 1423 | 7058 |
| cashflow_dividends | Cash Dividends (Cash Flow) | MATRIX | 0.9564 | 1899 | 4734 |
| cashflow_fin | Financing Activities - Net Cash Flow | MATRIX | 0.9709 | 788 | 5688 |
| cashflow_invst | Investing Activities - Net Cash Flow | MATRIX | 0.9709 | 668 | 3855 |
| cashflow_op | Operating Activities - Net Cash Flow | MATRIX | 0.9709 | 2644 | 7581 |
| cogs | Cost of Goods Sold | MATRIX | 0.9557 | 1146 | 8284 |
| current_ratio | Current Ratio | MATRIX | 0.7806 | 1123 | 5348 |
| debt | Debt | MATRIX | 0.7904 | 3997 | 14771 |
| debt_lt | Long-Term Debt - Total | MATRIX | 0.9433 | 5626 | 10976 |
| debt_st | Debt in Current Liabilities | MATRIX | 0.8796 | 2480 | 6638 |
| depre_amort | Depreciation and Amortization - Total | MATRIX | 0.8577 | 585 | 3395 |
| ebit | Earnings Before Interest and Taxes | MATRIX | 0.9578 | 5400 | 14800 |
| ebitda | Earnings Before Interest | MATRIX | 0.9454 | 4856 | 14110 |
| employee | Employees | MATRIX | 0.9588 | 720 | 3734 |
| enterprise_value | Enterprise Value | MATRIX | 0.7359 | 4720 | 11967 |
| eps | Earnings Per Share (Basic) - Including Extraordinary Items | MATRIX | 0.958 | 2193 | 13754 |
| equity | Common/Ordinary Equity - Total | MATRIX | 0.947 | 2281 | 13334 |
| fnd6_acdo | Current Assets of Discontinued Operations | MATRIX | 0.6072 | 868 | 1659 |
| fnd6_acodo | Other Current Assets Excl Discontinued Operations | MATRIX | 0.6119 | 575 | 1581 |
| fnd6_acox | Current Assets - Other - Sundry | MATRIX | 0.8318 | 500 | 1310 |
| fnd6_acqgdwl | Acquired Assets - Goodwill | MATRIX | 0.2632 | 438 | 837 |
| fnd6_acqintan | Acquired Assets - Intangibles | MATRIX | 0.261 | 147 | 350 |
| fnd6_adesinda_curcd | ISO Currency Code - Company Annual Market | MATRIX | 1.0 | 344 | 1570 |
| fnd6_aldo | Long-term Assets of Discontinued Operations | MATRIX | 0.6127 | 187 | 688 |
| fnd6_am | Amortization of Intangibles | MATRIX | 0.6473 | 333 | 1148 |
| fnd6_aodo | Other Assets excluding Discontinued Operations | MATRIX | 0.6158 | 156 | 414 |
| fnd6_aox | Assets - Other - Sundry | MATRIX | 0.8407 | 189 | 581 |
| fnd6_aqc | Acquisitions | MATRIX | 0.8463 | 283 | 532 |
| fnd6_aqi | Acquisitions - Income Contribution | MATRIX | 0.3997 | 141 | 228 |
| fnd6_aqs | Acquisitions - Sales Contribution | MATRIX | 0.401 | 63 | 248 |
| fnd6_beta | beta | MATRIX | 0.7123 | 146 | 414 |
| fnd6_capxs | Capital Expenditures | VECTOR | 0.9179 | 24 | 31 |
| fnd6_capxv | Capital Expend Property, Plant and Equipment Schd V | MATRIX | 0.8288 | 357 | 1181 |
| fnd6_caxts | Cost and Expenses - Total | VECTOR | 0.6384 | 7 | 7 |
| fnd6_ceql | Common Equity - Liquidation Value | MATRIX | 0.8955 | 252 | 1520 |
| fnd6_ch | Cash | MATRIX | 0.8887 | 195 | 1134 |
| fnd6_ci | Comprehensive Income - Total | MATRIX | 0.966 | 263 | 1524 |
| fnd6_cibegni | Comp Inc - Beginning Net Income | MATRIX | 0.8604 | 162 | 620 |
| fnd6_cicurr | Comp Inc - Currency Trans Adj | MATRIX | 0.8513 | 253 | 544 |
| fnd6_cidergl | Comp Inc - Derivative Gains/Losses | MATRIX | 0.8502 | 120 | 278 |
| fnd6_cik | nonimportant technical code | MATRIX | 1.0 | 206 | 1021 |
| fnd6_cimii | Comprehensive Income - Noncontrolling Interest | MATRIX | 0.3545 | 82 | 249 |
| fnd6_ciother | Comp. Inc. - Other Adj. | MATRIX | 0.8601 | 1234 | 1703 |
| fnd6_cipen | Comprehensive Income - Minimum Pension Adjustment | MATRIX | 0.8563 | 180 | 587 |
| fnd6_cisecgl | Comp Inc - Securities Gains/Losses | MATRIX | 0.8509 | 115 | 401 |
| fnd6_citotal | Comprehensive Income - Parent | MATRIX | 0.8605 | 154 | 512 |
| fnd6_city | the city where a company's corporate headquarters or home office is located | MATRIX | 1.0 | 270 | 979 |
| fnd6_cld2 | Capitalized Leases - Due in 2nd Year | MATRIX | 0.6824 | 172 | 375 |
| fnd6_cld3 | Capitalized Leases - Due in 3rd Year | MATRIX | 0.682 | 254 | 716 |
| fnd6_cld4 | Capitalized Leases - Due in 4th Year | MATRIX | 0.6852 | 114 | 268 |
| fnd6_cld5 | Capitalized Leases - Due in 5th Year | MATRIX | 0.6847 | 155 | 317 |
| fnd6_cogss | Cost of Goods Sold | VECTOR | 0.7234 | 11 | 13 |
| fnd6_cptmfmq_actq | Current Assets - Total | MATRIX | 0.7839 | 152 | 458 |
| fnd6_cptmfmq_atq | Assets - Total | MATRIX | 0.9741 | 259 | 776 |
| fnd6_cptmfmq_ceqq | Common/Ordinary Equity - Total | MATRIX | 0.9685 | 202 | 810 |
| fnd6_cptmfmq_dlttq | Long-Term Debt - Total | MATRIX | 0.8172 | 259 | 635 |
| fnd6_cptmfmq_dpq | Depreciation and Amortization - Total | MATRIX | 0.8775 | 111 | 262 |
| fnd6_cptmfmq_lctq | Current Liabilities - Total | MATRIX | 0.7837 | 255 | 889 |
| fnd6_cptmfmq_oibdpq | Operating Income Before Depreciation - Quarterly | MATRIX | 0.8908 | 144 | 541 |
| fnd6_cptmfmq_opepsq | Earnings Per Share from Operations | MATRIX | 0.974 | 121 | 944 |
| fnd6_cptmfmq_saleq | Sales/Turnover (Net) | MATRIX | 0.9634 | 196 | 578 |
| fnd6_cptnewqeventv110_actq | Current Assets - Total | VECTOR | 0.6706 | 12 | 17 |
| fnd6_cptnewqeventv110_apq | Accounts Payable/Creditors - Trade | VECTOR | 0.8042 | 27 | 48 |
| fnd6_cptnewqeventv110_atq | Assets - Total | VECTOR | 0.8066 | 9 | 12 |
| fnd6_cptnewqeventv110_ceqq | Common/Ordinary Equity - Total | VECTOR | 0.806 | 14 | 17 |
| fnd6_cptnewqeventv110_dlttq | Long-Term Debt - Total | VECTOR | 0.8064 | 8 | 9 |
| fnd6_cptnewqeventv110_dpq | Depreciation and Amortization - Total | VECTOR | 0.7764 | 11 | 29 |
| fnd6_cptnewqeventv110_epsf12 | Earnings Per Share (Diluted) - Excluding Extraordinary Items - 12 Months Moving | VECTOR | 0.7719 | 11 | 14 |
| fnd6_cptnewqeventv110_epsfxq | Earnings Per Share (Diluted) - Excluding Extraordinary items | VECTOR | 0.8061 | 15 | 17 |
| fnd6_cptnewqeventv110_epsx12 | Earnings Per Share (Basic) - Excluding Extraordinary Items - 12 Months Moving | VECTOR | 0.8053 | 20 | 26 |
| fnd6_cptnewqeventv110_lctq | Current Liabilities - Total | VECTOR | 0.6772 | 19 | 34 |
| fnd6_cptnewqeventv110_ltq | Liabilities - Total | VECTOR | 0.8066 | 18 | 20 |
| fnd6_cptnewqeventv110_nopiq | Non-Operating Income (Expense) - Total | VECTOR | 0.8063 | 20 | 27 |
| fnd6_cptnewqeventv110_oeps12 | Earnings Per Share from Operations - 12 Months Moving | VECTOR | 1.0 | 24 | 29 |
| fnd6_cptnewqeventv110_oiadpq | Operating Income After Depreciation - Quarterly | VECTOR | 0.8055 | 19 | 23 |
| fnd6_cptnewqeventv110_oibdpq | Operating Income Before Depreciation - Quarterly | VECTOR | 0.7795 | 10 | 12 |
| fnd6_cptnewqeventv110_opepsq | Earnings Per Share from Operations | VECTOR | 1.0 | 15 | 28 |
| fnd6_cptnewqeventv110_rectq | Receivables - Total | VECTOR | 0.8051 | 9 | 15 |
| fnd6_cptnewqeventv110_req | Retained Earnings | VECTOR | 0.8036 | 10 | 14 |
| fnd6_cptnewqeventv110_saleq | Sales/Turnover (Net) | VECTOR | 0.8063 | 9 | 14 |
| fnd6_cptnewqv1300_actq | Current Assets - Total | MATRIX | 0.7655 | 78 | 390 |
| fnd6_cptnewqv1300_apq | Accounts Payable/Creditors - Trade | MATRIX | 0.922 | 138 | 771 |
| fnd6_cptnewqv1300_atq | Assets - Total | MATRIX | 0.9524 | 188 | 568 |
| fnd6_cptnewqv1300_ceqq | Common/Ordinary Equity - Total | MATRIX | 0.947 | 134 | 569 |
| fnd6_cptnewqv1300_dlttq | Long-Term Debt - Total | MATRIX | 0.7998 | 276 | 789 |
| fnd6_cptnewqv1300_dpq | Depreciation and Amortization - Total | MATRIX | 0.8577 | 84 | 287 |
| fnd6_cptnewqv1300_epsf12 | Earnings Per Share (Diluted) - Excluding Extraordinary Items - 12 Months Moving | MATRIX | 0.9465 | 125 | 520 |
| fnd6_cptnewqv1300_epsfxq | Earnings Per Share (Diluted) - Excluding Extraordinary items | MATRIX | 0.9538 | 120 | 600 |
| fnd6_cptnewqv1300_epsx12 | Earnings Per Share (Basic) - Excluding Extraordinary Items - 12 Months Moving | MATRIX | 0.9468 | 108 | 374 |
| fnd6_cptnewqv1300_lctq | Current Liabilities - Total | MATRIX | 0.7652 | 189 | 390 |
| fnd6_cptnewqv1300_ltq | Liabilities - Total | MATRIX | 0.9355 | 157 | 546 |
| fnd6_cptnewqv1300_nopiq | Non-Operating Income (Expense) - Total | MATRIX | 0.8682 | 97 | 605 |
| fnd6_cptnewqv1300_oeps12 | Earnings Per Share from Operations - 12 Months Moving | MATRIX | 0.9466 | 154 | 646 |
| fnd6_cptnewqv1300_oiadpq | Operating Income After Depreciation - Quarterly | MATRIX | 0.8906 | 151 | 515 |
| fnd6_cptnewqv1300_oibdpq | Operating Income Before Depreciation - Quarterly | MATRIX | 0.8714 | 140 | 535 |
| fnd6_cptnewqv1300_opepsq | Earnings Per Share from Operations | MATRIX | 0.9538 | 118 | 686 |
| fnd6_cptnewqv1300_rectq | Receivables - Total | MATRIX | 0.9106 | 217 | 574 |
| fnd6_cptnewqv1300_req | Retained Earnings | MATRIX | 0.9208 | 84 | 310 |
| fnd6_cptnewqv1300_saleq | Sales/Turnover (Net) | MATRIX | 0.9436 | 107 | 354 |
| fnd6_cptrank_gvkeymap | technical code for a company, no need to use it for research | MATRIX | 0.5196 | 47 | 97 |
| fnd6_cshpri | Common Shares Used to Calculate Earnings Per Share - Basic | MATRIX | 0.9348 | 92 | 377 |
| fnd6_cshr | Common/Ordinary Shareholders | MATRIX | 0.7504 | 94 | 344 |
| fnd6_cshtr | Common Shares Traded - Annual | MATRIX | 0.9649 | 181 | 640 |
| fnd6_cshtrq | Common Shares Traded - Quarter | MATRIX | 0.9596 | 183 | 958 |
| fnd6_cstkcv | Common Stock-Carrying Value | MATRIX | 0.876 | 89 | 444 |
| fnd6_cstkcvq | Common Stock-Carrying Value | MATRIX | 0.8815 | 132 | 586 |
| fnd6_curcddv | ISO Currency Code - Dividend | VECTOR | 0.6034 | 3 | 5 |
| fnd6_currencya_curcd | ISO Currency Code - Company Annual Market | MATRIX | 0.9927 | 198 | 340 |
| fnd6_currencyqv1300_curcd | ISO Currency Code - Company Annual Market | MATRIX | 0.9886 | 112 | 426 |
| fnd6_dc | Deferred Charges | MATRIX | 0.7032 | 121 | 780 |
| fnd6_dclo | Debt - Capitalized Lease Obligations | MATRIX | 0.781 | 127 | 398 |
| fnd6_dcpstk | Convertible Debt and Preferred Stock | MATRIX | 0.8285 | 72 | 317 |
| fnd6_dcvsr | Debt - Senior Convertible | MATRIX | 0.8027 | 101 | 531 |
| fnd6_dcvsub | Debt - Subordinated Convertible | MATRIX | 0.8029 | 77 | 162 |
| fnd6_dcvt | Debt - Convertible | MATRIX | 0.8292 | 108 | 283 |
| fnd6_dd | Debt - Debentures | MATRIX | 0.7904 | 104 | 473 |
| fnd6_dd1 | Long-Term Debt Due in 1 Year | MATRIX | 0.8606 | 158 | 440 |
| fnd6_dd1q | Long-Term Debt Due in 1 Year | MATRIX | 0.7897 | 73 | 129 |
| fnd6_dd2 | Debt Due in 2nd Year | MATRIX | 0.7169 | 90 | 213 |
| fnd6_dd3 | Debt Due in 3rd Year | MATRIX | 0.7138 | 121 | 295 |
| fnd6_dd4 | Debt Due in 4th Year | MATRIX | 0.7156 | 68 | 306 |
| fnd6_dd5 | Debt Due in 5th Year | MATRIX | 0.7053 | 60 | 190 |
| fnd6_dilavx | Dilution Available - Excluding Extraordinary Items | MATRIX | 0.9283 | 93 | 320 |
| fnd6_divd | Cash Dividends - Daily | VECTOR | 0.562 | 0 | 0 |
| fnd6_dlcch | Current Debt - Changes | MATRIX | 0.4512 | 52 | 155 |
| fnd6_dltis | Long-Term Debt - Issuance | MATRIX | 0.8586 | 92 | 366 |
| fnd6_dlto | Debt - Long-Term - Other | MATRIX | 0.8024 | 591 | 719 |
| fnd6_dltp | Long-Term Debt - Tied to Prime | MATRIX | 0.6407 | 112 | 262 |
| fnd6_dltr | Long-Term Debt - Reduction | MATRIX | 0.867 | 110 | 338 |
| fnd6_dm | Debt - Mortgages & Other Secured | MATRIX | 0.7523 | 82 | 247 |
| fnd6_dn | Debt - Notes | MATRIX | 0.7958 | 86 | 255 |
| fnd6_donr | Nonrecurring Disc Operations | MATRIX | 0.7034 | 113 | 385 |
| fnd6_dps | Depreciation and Amortization | VECTOR | 0.92 | 6 | 7 |
| fnd6_dpvieb | Depreciation (Accumulated) - Ending Balance (Schedule VI) | MATRIX | 0.7584 | 99 | 292 |
| fnd6_drc | Deferred Revenue - Current | MATRIX | 0.5565 | 1627 | 2235 |
| fnd6_drlt | Deferred Revenue - Long-term | MATRIX | 0.5926 | 2636 | 3527 |
| fnd6_ds | Debt - Subordinated | MATRIX | 0.8021 | 192 | 336 |
| fnd6_dudd | Debt - Unamortized Debt Discount and Other | MATRIX | 0.8187 | 83 | 285 |
| fnd6_dvpa | Preferred Dividends in Arrears | MATRIX | 0.8057 | 183 | 298 |
| fnd6_dvrated | Indicated Annual Dividend Rate - Daily | VECTOR | 0.5446 | 1 | 7 |
| fnd6_dxd2 | Debt (excl Capitalized Leases) - Due in 2nd Year | MATRIX | 0.687 | 44 | 187 |
| fnd6_dxd3 | Debt (excl Capitalized Leases) - Due in 3rd Year | MATRIX | 0.6848 | 65 | 400 |
| fnd6_dxd4 | Debt (excl Capitalized Leases) - Due in 4th Year | MATRIX | 0.6872 | 60 | 186 |
| fnd6_dxd5 | Debt (excl Capitalized Leases) - Due in 5th Year | MATRIX | 0.6809 | 53 | 124 |
| fnd6_ein | Employer Identification Number code for the company | MATRIX | 1.0 | 248 | 747 |
| fnd6_emps | Employees | VECTOR | 0.8543 | 25 | 37 |
| fnd6_esopct | Common ESOP Obligation - Total | MATRIX | 0.8965 | 74 | 208 |
| fnd6_esopnr | Preferred ESOP Obligation - Non-Redeemable | MATRIX | 0.8596 | 67 | 252 |
| fnd6_esopr | Preferred ESOP Obligation - Redeemable | MATRIX | 0.8597 | 82 | 232 |
| fnd6_esubc | Equity in Net Loss - Earnings | MATRIX | 0.7401 | 119 | 334 |
| fnd6_esubs | Equity in Earnings | VECTOR | 0.896 | 11 | 20 |
| fnd6_eventv110_aqdq | Acquisition/Merger Diluted EPS Effect | VECTOR | 0.3774 | 3 | 3 |
| fnd6_eventv110_aqepsq | Acquisition/Merger Basic EPS Effect | VECTOR | 0.3582 | 1 | 2 |
| fnd6_eventv110_cstkcvq | Common Stock - Carrying Value | VECTOR | 0.9307 | 24 | 37 |
| fnd6_eventv110_dd1q | Long Term Debt Due in 1 Year | VECTOR | 0.8768 | 12 | 20 |
| fnd6_eventv110_dtedq | Extinguishment of Debt Diluted EPS Effect | VECTOR | 0.3861 | 7 | 9 |
| fnd6_eventv110_dteepsq | Extinguishment of Debt Basic EPS Effect | VECTOR | 0.3703 | 20 | 28 |
| fnd6_eventv110_gdwlid12 | Impairments Diluted EPS - 12mm | VECTOR | 0.2842 | 4 | 7 |
| fnd6_eventv110_gdwlidq | Impairment of Goodwill Diluted EPS Effect | VECTOR | 0.3005 | 2 | 2 |
| fnd6_eventv110_gdwlieps12 | Impairment of Goodwill Basic EPS Effect 12MM | VECTOR | 0.2842 | 7 | 9 |
| fnd6_eventv110_gdwliepsq | Impairment of Goodwill Basic EPS Effect | VECTOR | 0.294 | 0 | 0 |
| fnd6_eventv110_gldq | Gain/Loss Diluted EPS Effect | VECTOR | 0.4529 | 31 | 40 |
| fnd6_eventv110_glepsq | Gain/Loss Basic EPS Effect | VECTOR | 0.4411 | 12 | 14 |
| fnd6_eventv110_npq | Notes Payable | VECTOR | 0.9001 | 41 | 44 |
| fnd6_eventv110_nrtxtdq | Nonrecurring Income Taxes Diluted EPS Effect | VECTOR | 0.4389 | 0 | 0 |
| fnd6_eventv110_nrtxtepsq | Nonrecurring Income Taxes Basic EPS Effect | VECTOR | 0.4141 | 2 | 2 |
| fnd6_eventv110_optdrq | Dividend Rate - Assumption (%) | VECTOR | 0.8512 | 13 | 20 |
| fnd6_eventv110_optlifeq | Life of Options - Assumption (# yrs) | VECTOR | 0.8569 | 74 | 110 |
| fnd6_eventv110_optvolq | Volatility - Assumption (%) | VECTOR | 0.8606 | 105 | 151 |
| fnd6_eventv110_pncd12 | Core Pension Adjustment Diluted EPS Effect 12MM | VECTOR | 0.638 | 13 | 14 |
| fnd6_eventv110_pncdq | Core Pension Adjustment Diluted EPS Effect | VECTOR | 0.6383 | 10 | 14 |
| fnd6_eventv110_pnceps12 | Core Pension Adjustment Basic EPS Effect 12MM | VECTOR | 0.638 | 12 | 18 |
| fnd6_eventv110_pncepsq | Core Pension Adjustment Basic EPS Effect | VECTOR | 0.6383 | 15 | 19 |
| fnd6_eventv110_pncidq | Core Pension Interest Adjustment Diluted EPS Effect | VECTOR | 0.3093 | 1 | 2 |
| fnd6_eventv110_pncwidq | Core Pension w/o Interest Adjustment Diluted EPS Effect | VECTOR | 0.3157 | 1 | 1 |
| fnd6_eventv110_pncwiepsq | Core Pension w/o Interest Adjustment Basic EPS Effect | VECTOR | 0.3157 | 0 | 0 |
| fnd6_eventv110_setdq | Settlement (Litigation/Insurance) Diluted EPS Effect | VECTOR | 0.4631 | 3 | 4 |
| fnd6_eventv110_setepsq | Settlement (Litigation/Insurance) Basic EPS Effect | VECTOR | 0.449 | 9 | 11 |
| fnd6_eventv110_spced12 | S&P Core Earnings EPS Diluted 12MM | VECTOR | 0.6383 | 10 | 11 |
| fnd6_eventv110_spidq | Other Special Items Diluted EPS Effect | VECTOR | 0.5223 | 2 | 2 |
| fnd6_eventv110_spiepsq | Other Special Items Basic EPS Effect | VECTOR | 0.5029 | 4 | 4 |
| fnd6_eventv110_txdbcaq | Current Deferred Tax Asset | VECTOR | 0.8619 | 21 | 22 |
| fnd6_eventv110_txdbclq | Current Deferred Tax Liability | VECTOR | 0.8477 | 58 | 97 |
| fnd6_eventv110_wddq | Writedowns Diluted EPS Effect | VECTOR | 0.4796 | 3 | 3 |
| fnd6_eventv110_wdepsq | Writedowns Basic EPS Effect | VECTOR | 0.4685 | 7 | 7 |
| fnd6_eventv110_xaccq | Accrued Expenses | VECTOR | 0.7183 | 14 | 20 |
| fnd6_exre | Exchange Rate Effect | MATRIX | 0.882 | 255 | 1015 |
| fnd6_fatb | Plant, Property and Equipment at Cost - Buildings | MATRIX | 0.568 | 88 | 514 |
| fnd6_fatc | Plant, Property and Equipment at Cost - Construction in Progress | MATRIX | 0.6225 | 103 | 420 |
| fnd6_fate | Plant, Property and Equipment at Cost - Machinery & Equipment | MATRIX | 0.508 | 61 | 247 |
| fnd6_fatl | Property, Plant, and Equipment - Leases at Cost | MATRIX | 0.5083 | 1354 | 2081 |
| fnd6_fatn | Property, Plant, and Equipment - Natural Resources at Cost | MATRIX | 0.6273 | 52 | 208 |
| fnd6_fato | Plant, Property and Equipment at Cost - Other | MATRIX | 0.513 | 108 | 374 |
| fnd6_fatp | Plant, Property and Equipment at Cost - Land & Improvements | MATRIX | 0.5688 | 65 | 409 |
| fnd6_fiao | Financing Activities - Other | MATRIX | 0.8836 | 96 | 368 |
| fnd6_fic | identifies the country in which the company is incorporated or legally registered | MATRIX | 1.0 | 202 | 731 |
| fnd6_fopo | Funds from Operations - Other | MATRIX | 0.8832 | 4563 | 6073 |
| fnd6_fopox | Funds from Operations - Other excluding Option Tax Benefit | MATRIX | 0.637 | 247 | 528 |
| fnd6_fyrc | Unimportant technical code, please ignore for research purposes | MATRIX | 1.0 | 147 | 885 |
| fnd6_gdwls | Goodwill | VECTOR | 0.8869 | 12 | 14 |
| fnd6_ias | Identifiable (Total) Assets | VECTOR | 0.927 | 5 | 10 |
| fnd6_ibmii | Income before Extraordinary Items and Noncontrolling Interests | MATRIX | 0.9575 | 121 | 531 |
| fnd6_ibs | Income before Extraordinary Items | VECTOR | 0.8346 | 5 | 5 |
| fnd6_idesindq_curcd | ISO Currency Code - Company Annual Market | MATRIX | 0.9861 | 143 | 357 |
| fnd6_idit | Interest and Related Income - Total | MATRIX | 0.5501 | 71 | 297 |
| fnd6_iints | Interest Income | VECTOR | 0.3619 | 4 | 4 |
| fnd6_incorp | Incorporated | MATRIX | 1.0 | 249 | 804 |
| fnd6_intan | Intangible Assets - Total | MATRIX | 0.8654 | 175 | 616 |
| fnd6_intc | Interest Capitalized | MATRIX | 0.7787 | 717 | 1128 |
| fnd6_intpn | Interest Paid - Net | MATRIX | 0.784 | 86 | 251 |
| fnd6_intseg | Intersegment Eliminations | VECTOR | 0.953 | 15 | 20 |
| fnd6_invfg | Inventories - Finished Goods | MATRIX | 0.5873 | 62 | 373 |
| fnd6_invo | Inventories - Other | MATRIX | 0.5983 | 49 | 195 |
| fnd6_invrm | Inventories - Raw Materials | MATRIX | 0.5822 | 72 | 374 |
| fnd6_invwip | Inventories - Work In Process | MATRIX | 0.5736 | 62 | 466 |
| fnd6_itcb | Investment Tax Credit (Balance Sheet) | MATRIX | 0.8337 | 64 | 231 |
| fnd6_itci | Investment Tax Credit (Income Account) | MATRIX | 0.5774 | 471 | 1209 |
| fnd6_ivaco | Investing Activities - Other | MATRIX | 0.8836 | 2358 | 2968 |
| fnd6_ivaeq | Investment and Advances - Equity | MATRIX | 0.8005 | 86 | 471 |
| fnd6_ivaeqs | Investments at Equity | VECTOR | 0.8923 | 4 | 6 |
| fnd6_ivao | Investment and Advances - Other | MATRIX | 0.8621 | 74 | 347 |
| fnd6_ivch | Increase in Investments | MATRIX | 0.8366 | 76 | 154 |
| fnd6_ivst | Short-Term Investments - Total | MATRIX | 0.8701 | 73 | 312 |
| fnd6_ivstch | Short-Term Investments - Change | MATRIX | 0.6432 | 56 | 124 |
| fnd6_lcox | Current Liabilities - Other - Sundry | MATRIX | 0.8367 | 577 | 1000 |
| fnd6_lcoxdr | Current Liabilities - Other - Excluding Deferred Revenue | MATRIX | 0.8621 | 164 | 651 |
| fnd6_lifr | LIFO Reserve | MATRIX | 0.7681 | 112 | 655 |
| fnd6_lno | Liabilities Netting & Other Adjustments | MATRIX | 0.7102 | 60 | 192 |
| fnd6_loc | string for locating the Headquarters of the company | MATRIX | 1.0 | 183 | 874 |
| fnd6_lol2 | Liabilities Level 2 (Observable) | MATRIX | 0.7082 | 60 | 263 |
| fnd6_loxdr | Liabilities - Other - Excluding Deferred Revenue | MATRIX | 0.8619 | 145 | 406 |
| fnd6_lqpl1 | Liabilities Level 1 (Quoted Prices) | MATRIX | 0.7082 | 53 | 216 |
| fnd6_lul3 | Liabilities Level 3 (Unobservable) | MATRIX | 0.7083 | 88 | 243 |
| fnd6_mfma1_aoloch | Assets and Liabilities - Other - Net Change | MATRIX | 0.9531 | 194 | 368 |
| fnd6_mfma1_apalch | Accounts Payable and Accrued Liabilities - Increase/(Decrease) | MATRIX | 0.6079 | 79 | 279 |
| fnd6_mfma1_at | Assets - Total | MATRIX | 0.9853 | 166 | 789 |
| fnd6_mfma1_capx | Capital Expenditures | MATRIX | 0.8961 | 155 | 333 |
| fnd6_mfma1_csho | Common Shares Outstanding | MATRIX | 0.9782 | 204 | 614 |
| fnd6_mfma1_dp | Depreciation and Amortization | MATRIX | 0.9188 | 103 | 332 |
| fnd6_mfma1_dpc | Depreciation and Amortization (Cash Flow) | MATRIX | 0.9357 | 106 | 305 |
| fnd6_mfma1_invch | Mortgages - Decrease (Increase) | MATRIX | 0.879 | 118 | 390 |
| fnd6_mfma2_oancf | Operating Activities - Net Cash Flow | MATRIX | 0.9661 | 139 | 401 |
| fnd6_mfma2_opeps | Earnings Per Share from Operations | MATRIX | 0.9791 | 172 | 487 |
| fnd6_mfma2_recch | Accounts Receivable - Decrease (Increase) | MATRIX | 0.846 | 93 | 191 |
| fnd6_mfma2_revt | Revenue - Total | MATRIX | 0.9524 | 120 | 372 |
| fnd6_mfma2_txach | Income Taxes - Accrued - Increase/(Decrease) | MATRIX | 0.6171 | 55 | 288 |
| fnd6_mfmq_cheq | Cash and Short-Term Investments | MATRIX | 0.9687 | 122 | 421 |
| fnd6_mfmq_cogsq | Cost of Goods Sold | MATRIX | 0.9614 | 90 | 259 |
| fnd6_mfmq_cshprq | Common Shares Used to Calculate Earnings Per Share - Basic | MATRIX | 0.9855 | 113 | 830 |
| fnd6_mfmq_dlcq | Debt in Current Liabilities | MATRIX | 0.6925 | 83 | 164 |
| fnd6_mfmq_ibcomq | Income Before Extraordinary Items - Available for Common | MATRIX | 0.9803 | 98 | 372 |
| fnd6_mfmq_mibtq | Noncontrolling Interests - Total - Balance Sheet - Quarterly | MATRIX | 0.3958 | 44 | 237 |
| fnd6_mfmq_piq | Pretax Income | MATRIX | 0.9777 | 111 | 547 |
| fnd6_mibn | Noncontrolling Interests - Nonredeemable - Balance Sheet | MATRIX | 0.3608 | 78 | 239 |
| fnd6_mibt | Noncontrolling Interests - Total - Balance Sheet | MATRIX | 0.371 | 84 | 165 |
| fnd6_mkvalt | Market Value - Total | MATRIX | 0.822 | 53 | 172 |
| fnd6_mkvaltq | Market Value - Total | MATRIX | 0.8743 | 33 | 52 |
| fnd6_mrc1 | Rental Commitments - Minimum - 1st Year | MATRIX | 0.7368 | 331 | 686 |
| fnd6_mrc2 | Rental Commitments - Minimum - 2nd Year | MATRIX | 0.7033 | 201 | 910 |
| fnd6_mrc3 | Rental Commitments - Minimum - 3rd Year | MATRIX | 0.7017 | 161 | 475 |
| fnd6_mrc4 | Rental Commitments - Minimum - 4th Year | MATRIX | 0.7021 | 155 | 317 |
| fnd6_mrc5 | Rental Commitments - Minimum - 5th Year | MATRIX | 0.6817 | 193 | 474 |
| fnd6_mrct | Rental Commitments - Minimum - 5-Year Total | MATRIX | 0.6802 | 169 | 461 |
| fnd6_mrcta | Thereafter Portion of Leases | MATRIX | 0.7237 | 1629 | 2349 |
| fnd6_msa | Marketable Securities Adjustment | MATRIX | 0.6262 | 61 | 208 |
| fnd6_naicss | NAICS Code | VECTOR | 0.967 | 56 | 77 |
| fnd6_newa1v1300_aco | Current Assets - Other - Total | MATRIX | 0.8454 | 265 | 459 |
| fnd6_newa1v1300_acominc | Accumulated Other Comprehensive Income (Loss) | MATRIX | 0.6758 | 80 | 192 |
| fnd6_newa1v1300_act | Current Assets - Total | MATRIX | 0.7304 | 136 | 441 |
| fnd6_newa1v1300_ano | Assets Netting & Other Adjustments | MATRIX | 0.7112 | 47 | 251 |
| fnd6_newa1v1300_ao | Assets - Other | MATRIX | 0.9198 | 80 | 252 |
| fnd6_newa1v1300_aocidergl | Accum Other Comp Inc - Derivatives Unrealized Gain/Loss | MATRIX | 0.6398 | 59 | 184 |
| fnd6_newa1v1300_aociother | Accum Other Comp Inc - Other Adjustments | MATRIX | 0.6578 | 66 | 224 |
| fnd6_newa1v1300_aocipen | Accum Other Comp Inc - Min Pension Liab Adj | MATRIX | 0.6459 | 78 | 241 |
| fnd6_newa1v1300_aol2 | Assets Level 2 (Observable) | MATRIX | 0.7091 | 57 | 113 |
| fnd6_newa1v1300_aoloch | Assets and Liabilities - Other - Net Change | MATRIX | 0.8819 | 71 | 199 |
| fnd6_newa1v1300_ap | Accounts Payable - Trade | MATRIX | 0.9168 | 103 | 320 |
| fnd6_newa1v1300_apalch | Accounts Payable and Accrued Liabilities - Increase/(Decrease) | MATRIX | 0.5574 | 64 | 465 |
| fnd6_newa1v1300_aqpl1 | Assets Level 1 (Quoted Prices) | MATRIX | 0.7091 | 58 | 109 |
| fnd6_newa1v1300_at | Assets - Total | MATRIX | 0.9378 | 100 | 437 |
| fnd6_newa1v1300_aul3 | Assets Level 3 (Unobservable) | MATRIX | 0.7093 | 57 | 168 |
| fnd6_newa1v1300_bkvlps | Book Value Per Share | MATRIX | 0.9274 | 118 | 687 |
| fnd6_newa1v1300_caps | Capital Surplus/Share Premium Reserve | MATRIX | 0.896 | 66 | 225 |
| fnd6_newa1v1300_capx | Capital Expenditures | MATRIX | 0.877 | 152 | 346 |
| fnd6_newa1v1300_ceq | Common/Ordinary Equity - Total | MATRIX | 0.9344 | 117 | 357 |
| fnd6_newa1v1300_ceqt | Common Equity - Tangible | MATRIX | 0.8949 | 82 | 328 |
| fnd6_newa1v1300_che | Cash and Short-Term Investments | MATRIX | 0.9332 | 70 | 287 |
| fnd6_newa1v1300_chech | Cash and Cash Equivalents - Increase/(Decrease) | MATRIX | 0.8744 | 121 | 228 |
| fnd6_newa1v1300_cogs | Cost of Goods Sold | MATRIX | 0.9262 | 62 | 290 |
| fnd6_newa1v1300_cshfd | Common Shares Used to Calc Earnings Per Share - Fully Diluted | MATRIX | 0.8992 | 108 | 245 |
| fnd6_newa1v1300_cshi | Common Shares Issued | MATRIX | 0.8969 | 59 | 127 |
| fnd6_newa1v1300_csho | Common Shares Outstanding | MATRIX | 0.9337 | 98 | 306 |
| fnd6_newa1v1300_cstk | Common/Ordinary Stock (Capital) | MATRIX | 0.8992 | 55 | 599 |
| fnd6_newa1v1300_dcom | Deferred Compensation | MATRIX | 0.61 | 85 | 236 |
| fnd6_newa1v1300_dlc | Debt in Current Liabilities - Total | MATRIX | 0.709 | 111 | 269 |
| fnd6_newa1v1300_dltt | Long-Term Debt - Total | MATRIX | 0.7895 | 249 | 353 |
| fnd6_newa1v1300_dp | Depreciation and Amortization | MATRIX | 0.8593 | 72 | 236 |
| fnd6_newa1v1300_dpact | Depreciation, Depletion and Amortization (Accumulated) | MATRIX | 0.7866 | 76 | 164 |
| fnd6_newa1v1300_dpc | Depreciation and Amortization (Cash Flow) | MATRIX | 0.8628 | 83 | 459 |
| fnd6_newa1v1300_dv | Cash Dividends (Cash Flow) | MATRIX | 0.87 | 58 | 325 |
| fnd6_newa1v1300_dvc | Dividends Common/Ordinary | MATRIX | 0.891 | 54 | 436 |
| fnd6_newa1v1300_dvt | Dividends - Total | MATRIX | 0.8904 | 54 | 166 |
| fnd6_newa1v1300_ebit | Earnings Before Interest and Taxes | MATRIX | 0.8734 | 74 | 172 |
| fnd6_newa1v1300_ebitda | Earnings Before Interest | MATRIX | 0.8673 | 81 | 272 |
| fnd6_newa1v1300_emp | Employees | MATRIX | 0.8744 | 77 | 406 |
| fnd6_newa1v1300_epsfi | Earnings Per Share (Diluted) - Including Extraordinary Items | MATRIX | 0.9331 | 102 | 568 |
| fnd6_newa1v1300_epsfx | Earnings Per Share (Diluted) - Excluding Extraordinary Items | MATRIX | 0.9327 | 79 | 389 |
| fnd6_newa1v1300_epspi | Earnings Per Share (Basic) - Including Extraordinary Items | MATRIX | 0.933 | 71 | 346 |
| fnd6_newa1v1300_epspx | Earnings Per Share (Basic) - Excluding Extraordinary Items | MATRIX | 0.9327 | 71 | 309 |
| fnd6_newa1v1300_fca | Foreign Exchange Income (Loss) | MATRIX | 0.3252 | 44 | 76 |
| fnd6_newa1v1300_fincf | Financing Activities - Net Cash Flow | MATRIX | 0.8837 | 86 | 236 |
| fnd6_newa1v1300_gdwl | Goodwill | MATRIX | 0.817 | 89 | 211 |
| fnd6_newa1v1300_gp | Gross Profit (Loss) | MATRIX | 0.9268 | 269 | 787 |
| fnd6_newa1v1300_ib | Income Before Extraordinary Items | MATRIX | 0.9366 | 71 | 226 |
| fnd6_newa1v1300_ibadj | Income Before Extraordinary Items - Adjusted for Common Stock Equivalents | MATRIX | 0.9369 | 72 | 201 |
| fnd6_newa1v1300_ibc | Income Before Extraordinary Items (Cash Flow) | MATRIX | 0.8821 | 197 | 453 |
| fnd6_newa1v1300_ibcom | Income Before Extraordinary Items - Available for Common | MATRIX | 0.9367 | 55 | 138 |
| fnd6_newa1v1300_icapt | Invested Capital - Total | MATRIX | 0.9365 | 87 | 256 |
| fnd6_newa1v1300_intano | Other Intangibles | MATRIX | 0.6592 | 69 | 390 |
| fnd6_newa1v1300_invch | Mortgages - Decrease (Increase) | MATRIX | 0.8012 | 120 | 417 |
| fnd6_newa1v1300_invt | Inventories - Total | MATRIX | 0.8956 | 109 | 311 |
| fnd6_newa1v1300_ivncf | Investing Activities - Net Cash Flow | MATRIX | 0.8839 | 55 | 155 |
| fnd6_newa1v1300_lco | Current Liabilities - Other - Total | MATRIX | 0.8454 | 158 | 228 |
| fnd6_newa1v1300_lct | Current Liabilities - Total | MATRIX | 0.731 | 163 | 318 |
| fnd6_newa1v1300_lo | Liabilities - Other - Total | MATRIX | 0.8535 | 140 | 263 |
| fnd6_newa1v1300_lse | Liabilities and Stockholders Equity - Total | MATRIX | 0.8915 | 75 | 260 |
| fnd6_newa1v1300_lt | Liabilities - Total | MATRIX | 0.9353 | 142 | 388 |
| fnd6_newa2v1300_mib | Minority Interest (Balance Sheet) | MATRIX | 0.869 | 84 | 506 |
| fnd6_newa2v1300_mii | Noncontrolling Interest (Income Account) | MATRIX | 0.8336 | 96 | 342 |
| fnd6_newa2v1300_ni | Net Income (Loss) | MATRIX | 0.9388 | 191 | 493 |
| fnd6_newa2v1300_nopi | Nonoperating Income (Expense) | MATRIX | 0.8765 | 73 | 151 |
| fnd6_newa2v1300_oancf | Operating Activities - Net Cash Flow | MATRIX | 0.8867 | 125 | 267 |
| fnd6_newa2v1300_oiadp | Operating Income After Depreciation | MATRIX | 0.8761 | 135 | 332 |
| fnd6_newa2v1300_oibdp | Operating Income Before Depreciation | MATRIX | 0.8699 | 153 | 351 |
| fnd6_newa2v1300_opeps | Earnings Per Share from Operations | MATRIX | 0.9374 | 91 | 271 |
| fnd6_newa2v1300_optexd | Options - Exercised (-) | MATRIX | 0.7543 | 117 | 244 |
| fnd6_newa2v1300_pi | Pretax Income | MATRIX | 0.8925 | 82 | 316 |
| fnd6_newa2v1300_ppegt | Property, Plant and Equipment - Total (Gross) | MATRIX | 0.7894 | 82 | 145 |
| fnd6_newa2v1300_ppent | Property, Plant and Equipment - Total (Net) | MATRIX | 0.8716 | 256 | 573 |
| fnd6_newa2v1300_prsho | Redeem Pfd Shares Outs (000) | MATRIX | 0.6559 | 558 | 625 |
| fnd6_newa2v1300_rdip | In Process R&D Expense | MATRIX | 0.7202 | 71 | 311 |
| fnd6_newa2v1300_rdipa | In-Process R&D Expense After-tax | MATRIX | 0.7139 | 332 | 469 |
| fnd6_newa2v1300_rdipd | In Process R&D Expense Diluted EPS Effect | MATRIX | 0.712 | 465 | 605 |
| fnd6_newa2v1300_rdipeps | In Process R&D Expense Basic EPS Effect | MATRIX | 0.712 | 1109 | 1256 |
| fnd6_newa2v1300_re | Retained Earnings | MATRIX | 0.8992 | 109 | 408 |
| fnd6_newa2v1300_recch | Accounts Receivable - Decrease (Increase) | MATRIX | 0.7758 | 66 | 302 |
| fnd6_newa2v1300_rect | Receivables - Total | MATRIX | 0.9129 | 80 | 385 |
| fnd6_newa2v1300_reuna | Retained Earnings - Unadjusted | MATRIX | 0.8754 | 91 | 494 |
| fnd6_newa2v1300_revt | Revenue - Total | MATRIX | 0.8924 | 66 | 233 |
| fnd6_newa2v1300_sale | Sales/Turnover (Net) | MATRIX | 0.9256 | 88 | 272 |
| fnd6_newa2v1300_seq | Stockholders Equity - Parent | MATRIX | 0.94 | 111 | 448 |
| fnd6_newa2v1300_seqo | Other Stockholders' Equity Adjustments | MATRIX | 0.61 | 97 | 216 |
| fnd6_newa2v1300_spced | S&P Core Earnings EPS Diluted | MATRIX | 0.7739 | 19 | 183 |
| fnd6_newa2v1300_spceeps | S&P Core Earnings EPS Basic | MATRIX | 0.7738 | 14 | 241 |
| fnd6_newa2v1300_spi | Special Items | MATRIX | 0.8951 | 53 | 196 |
| fnd6_newa2v1300_stkco | Stock Compensation Expense | MATRIX | 0.6256 | 104 | 253 |
| fnd6_newa2v1300_tstk | Treasury Stock - Total (All Capital) | MATRIX | 0.4335 | 50 | 146 |
| fnd6_newa2v1300_tstkn | Treasury Stock - Number of Common Shares | MATRIX | 0.4484 | 52 | 146 |
| fnd6_newa2v1300_txach | Income Taxes - Accrued - Increase/(Decrease) | MATRIX | 0.5685 | 46 | 113 |
| fnd6_newa2v1300_txdb | Deferred Taxes - Balance Sheet | MATRIX | 0.8307 | 98 | 327 |
| fnd6_newa2v1300_txditc | Deferred Taxes and Investment Tax Credit | MATRIX | 0.7976 | 66 | 265 |
| fnd6_newa2v1300_txp | Income Taxes Payable | MATRIX | 0.8221 | 73 | 198 |
| fnd6_newa2v1300_txt | Income Taxes - Total | MATRIX | 0.8583 | 86 | 343 |
| fnd6_newa2v1300_wcap | Working Capital (Balance Sheet) | MATRIX | 0.7315 | 73 | 234 |
| fnd6_newa2v1300_xidoc | Extraordinary Items and Discontinued Operations (Cash Flow) | MATRIX | 0.8833 | 137 | 556 |
| fnd6_newa2v1300_xint | Interest and Related Expense - Total | MATRIX | 0.7928 | 57 | 95 |
| fnd6_newa2v1300_xoptd | Implied Option EPS Diluted | MATRIX | 0.7105 | 13 | 90 |
| fnd6_newa2v1300_xopteps | Implied Option EPS Basic | MATRIX | 0.7105 | 8 | 18 |
| fnd6_newa2v1300_xrd | Research and Development Expense | MATRIX | 0.4893 | 116 | 255 |
| fnd6_newa2v1300_xsga | Selling, General and Administrative Expense | MATRIX | 0.7314 | 157 | 340 |
| fnd6_newq_xoptdqp | Implied Option EPS Diluted Preliminary | MATRIX | 0.4631 | 2 | 2 |
| fnd6_newq_xoptepsqp | Implied Option EPS Basic Preliminary | MATRIX | 0.466 | 5 | 16 |
| fnd6_newq_xoptqp | Implied Option Expense Preliminary | MATRIX | 0.5175 | 9 | 20 |
| fnd6_newqeventv110_acchgq | Accounting Changes - Cumulative Effect | VECTOR | 0.9616 | 12 | 25 |
| fnd6_newqeventv110_acomincq | Accumulated Other Comprehensive Income (Loss) | VECTOR | 1.0 | 17 | 67 |
| fnd6_newqeventv110_acoq | Current Assets - Other - Total | VECTOR | 0.7524 | 13 | 17 |
| fnd6_newqeventv110_altoq | Other Long-term Assets | VECTOR | 0.9163 | 8 | 11 |
| fnd6_newqeventv110_ancq | Non-Current Assets - Total | VECTOR | 0.615 | 5 | 6 |
| fnd6_newqeventv110_anoq | Assets Netting & Other Adjustments | VECTOR | 0.8872 | 5 | 5 |
| fnd6_newqeventv110_aociderglq | Accumulated Other Comprehensive Income - Derivatives Unrealized Gain/Loss | VECTOR | 0.9989 | 12 | 16 |
| fnd6_newqeventv110_aociotherq | Accum Other Comp Inc - Other Adjustments | VECTOR | 1.0 | 13 | 17 |
| fnd6_newqeventv110_aocipenq | Accum Other Comp Inc - Min Pension Liab Adj | VECTOR | 1.0 | 15 | 20 |
| fnd6_newqeventv110_aocisecglq | Accum. Other Comp. Inc. - Unreal G/L Ret. Int. in Sec. Assets | VECTOR | 1.0 | 21 | 32 |
| fnd6_newqeventv110_aol2q | Assets Level 2 (Observable) | VECTOR | 0.8867 | 10 | 11 |
| fnd6_newqeventv110_aoq | Assets - Other - Total | VECTOR | 0.8064 | 12 | 13 |
| fnd6_newqeventv110_aqaq | Acquisition/Merger After-Tax | VECTOR | 0.4117 | 4 | 13 |
| fnd6_newqeventv110_aqpl1q | Assets Level 1 (Quoted Prices) | VECTOR | 0.8871 | 16 | 19 |
| fnd6_newqeventv110_aqpq | Acquisition/Merger Pretax | VECTOR | 0.5211 | 7 | 7 |
| fnd6_newqeventv110_aul3q | Assets Level 3 (Unobservable) | VECTOR | 0.8872 | 10 | 15 |
| fnd6_newqeventv110_capsq | Capital Surplus/Share Premium Reserve | VECTOR | 0.8029 | 26 | 43 |
| fnd6_newqeventv110_cheq | Cash and Short-Term Investments | VECTOR | 0.8065 | 21 | 24 |
| fnd6_newqeventv110_chq | Cash | VECTOR | 0.5366 | 18 | 19 |
| fnd6_newqeventv110_cibegniq | Comp Inc - Beginning Net Income | VECTOR | 0.997 | 10 | 24 |
| fnd6_newqeventv110_cicurrq | Comp Inc - Currency Trans Adj | VECTOR | 0.9942 | 11 | 18 |
| fnd6_newqeventv110_ciderglq | Comprehensive Income - Derivative Gains/Losses | VECTOR | 0.9934 | 5 | 8 |
| fnd6_newqeventv110_cimiiq | Comprehensive Income - Noncontrolling Interest | VECTOR | 1.0 | 11 | 15 |
| fnd6_newqeventv110_ciotherq | Comprehensive Income - Other Adjustments | VECTOR | 0.997 | 14 | 16 |
| fnd6_newqeventv110_cipenq | Comp Inc - Minimum Pension Adj | VECTOR | 0.9959 | 12 | 17 |
| fnd6_newqeventv110_ciq | Comprehensive Income - Total | VECTOR | 1.0 | 5 | 7 |
| fnd6_newqeventv110_cisecglq | Comp Inc - Securities Gains/Losses | VECTOR | 0.9939 | 9 | 13 |
| fnd6_newqeventv110_citotalq | Comprehensive Income - Parent | VECTOR | 0.9972 | 10 | 29 |
| fnd6_newqeventv110_cogsq | Cost of Goods Sold | VECTOR | 0.8063 | 9 | 16 |
| fnd6_newqeventv110_csh12q | Common Shares Used to Calculate Earnings Per Share - 12 Months Moving | VECTOR | 0.8069 | 9 | 10 |
| fnd6_newqeventv110_cshfdq | Common Shares for Diluted EPS | VECTOR | 0.7692 | 14 | 16 |
| fnd6_newqeventv110_cshiq | Common Shares Issued | VECTOR | 1.0 | 24 | 45 |
| fnd6_newqeventv110_cshopq | Total Shares Repurchased - Quarter | VECTOR | 0.8324 | 21 | 25 |
| fnd6_newqeventv110_cshoq | Common Shares Outstanding | VECTOR | 0.8059 | 5 | 13 |
| fnd6_newqeventv110_cshprq | Common Shares Used to Calculate Earnings Per Share - Basic | VECTOR | 0.8062 | 14 | 15 |
| fnd6_newqeventv110_cstkeq | Common Stock Equivalents - Dollar Savings | VECTOR | 0.8064 | 32 | 40 |
| fnd6_newqeventv110_cstkq | Common/Ordinary Stock (Capital) | VECTOR | 0.8032 | 6 | 7 |
| fnd6_newqeventv110_dcomq | Deferred Compensation | VECTOR | 0.9155 | 10 | 15 |
| fnd6_newqeventv110_diladq | Dilution Adjustment | VECTOR | 1.0 | 28 | 33 |
| fnd6_newqeventv110_dilavq | Dilution Available - Excluding Extraordinary Items | VECTOR | 1.0 | 12 | 12 |
| fnd6_newqeventv110_dlcq | Debt in Current Liabilities | VECTOR | 0.8048 | 15 | 21 |
| fnd6_newqeventv110_doq | Discontinued Operations | VECTOR | 0.7952 | 4 | 6 |
| fnd6_newqeventv110_dpactq | Depreciation, Depletion and Amortization (Accumulated) | VECTOR | 0.7312 | 3 | 5 |
| fnd6_newqeventv110_drcq | Deferred Revenue - Current | VECTOR | 0.9012 | 70 | 116 |
| fnd6_newqeventv110_drltq | Deferred Revenue - Long-term | VECTOR | 0.912 | 86 | 155 |
| fnd6_newqeventv110_dteaq | Extinguishment of Debt After-tax | VECTOR | 0.4192 | 9 | 15 |
| fnd6_newqeventv110_dtepq | Extinguishment of Debt Pretax | VECTOR | 0.5134 | 5 | 5 |
| fnd6_newqeventv110_dvpq | Dividends - Preferred/Preference | VECTOR | 0.8064 | 11 | 14 |
| fnd6_newqeventv110_epsfiq | Earnings Per Share (Diluted) - Including Extraordinary Items | VECTOR | 0.8061 | 15 | 25 |
| fnd6_newqeventv110_epspiq | Earnings Per Share (Basic) - Including Extraordinary Items | VECTOR | 0.8061 | 7 | 13 |
| fnd6_newqeventv110_epspxq | Earnings Per Share (Basic) - Excluding Extraordinary Items | VECTOR | 0.8061 | 6 | 10 |
| fnd6_newqeventv110_esopctq | Common ESOP Obligation - Total | VECTOR | 0.9511 | 16 | 34 |
| fnd6_newqeventv110_esopnrq | Preferred ESOP Obligation - Non-Redeemable | VECTOR | 0.9123 | 6 | 7 |
| fnd6_newqeventv110_esoprq | Preferred ESOP Obligation - Redeemable | VECTOR | 0.9123 | 27 | 44 |
| fnd6_newqeventv110_esoptq | Preferred ESOP Obligation - Total | VECTOR | 0.9521 | 9 | 12 |
| fnd6_newqeventv110_fcaq | Foreign Exchange Income (Loss) | VECTOR | 0.419 | 8 | 13 |
| fnd6_newqeventv110_gdwlamq | Amortization of Goodwill | VECTOR | 0.6637 | 3 | 5 |
| fnd6_newqeventv110_gdwlia12 | Impairments of Goodwill After-Tax - 12MM | VECTOR | 0.2863 | 12 | 16 |
| fnd6_newqeventv110_gdwliaq | Impairment of Goodwill After-tax | VECTOR | 0.3177 | 4 | 5 |
| fnd6_newqeventv110_gdwlipq | Impairment of Goodwill Pretax | VECTOR | 0.3809 | 1 | 2 |
| fnd6_newqeventv110_gdwlq | Goodwill (net) | VECTOR | 1.0 | 18 | 39 |
| fnd6_newqeventv110_glaq | Gain/Loss After-Tax | VECTOR | 0.4832 | 3 | 3 |
| fnd6_newqeventv110_glcea12 | Gain/Loss on Sale (Core Earnings Adjusted) After-tax 12MM | VECTOR | 0.5612 | 0 | 0 |
| fnd6_newqeventv110_glceaq | Gain/Loss on Sale (Core Earnings Adjusted) After-tax | VECTOR | 0.6463 | 21 | 23 |
| fnd6_newqeventv110_glced12 | Gain/Loss on Sale (Core Earnings Adjusted) Diluted EPS Effect 12MM | VECTOR | 0.5599 | 7 | 12 |
| fnd6_newqeventv110_glcedq | Gain/Loss on Sale (Core Earnings Adjusted) Diluted EPS | VECTOR | 0.6014 | 20 | 26 |
| fnd6_newqeventv110_glceeps12 | Gain/Loss on Sale (Core Earnings Adjusted) Basic EPS Effect 12MM | VECTOR | 0.5599 | 5 | 5 |
| fnd6_newqeventv110_glceepsq | Gain/Loss on Sale (Core Earnings Adjusted) Basic EPS Effect | VECTOR | 0.5928 | 13 | 14 |
| fnd6_newqeventv110_glcepq | Gain/Loss on Sale (Core Earnings Adjusted) Pretax | VECTOR | 0.7813 | 36 | 54 |
| fnd6_newqeventv110_glpq | Gain/Loss Pretax | VECTOR | 0.575 | 3 | 4 |
| fnd6_newqeventv110_hedgeglq | Gain/Loss on Ineffective Hedges | VECTOR | 0.4306 | 3 | 4 |
| fnd6_newqeventv110_ibadj12 | Income Before Extra Items - Adj for Common Stock Equivalents - 12MM | VECTOR | 0.4901 | 1 | 1 |
| fnd6_newqeventv110_ibadjq | Income Before Extraordinary Items - Adjusted for Common Stock Equivalents | VECTOR | 0.8064 | 8 | 11 |
| fnd6_newqeventv110_ibcomq | Income Before Extraordinary Items - Available for Common | VECTOR | 0.8064 | 3 | 3 |
| fnd6_newqeventv110_ibmiiq | Income before Extraordinary Items and Noncontrolling Interests | VECTOR | 0.9887 | 13 | 21 |
| fnd6_newqeventv110_ibq | Income Before Extraordinary Items | VECTOR | 0.8064 | 2 | 2 |
| fnd6_newqeventv110_icaptq | Invested Capital - Total - Quarterly | VECTOR | 0.8035 | 5 | 5 |
| fnd6_newqeventv110_intanoq | Other Intangibles | VECTOR | 0.9806 | 18 | 21 |
| fnd6_newqeventv110_intanq | Intangible Assets - Total | VECTOR | 0.7356 | 14 | 20 |
| fnd6_newqeventv110_invfgq | Inventory - Finished Goods | VECTOR | 0.7278 | 7 | 11 |
| fnd6_newqeventv110_invoq | Inventory - Other | VECTOR | 0.7373 | 6 | 9 |
| fnd6_newqeventv110_invrmq | Inventory - Raw Materials | VECTOR | 0.7221 | 8 | 14 |
| fnd6_newqeventv110_invtq | Inventories - Total | VECTOR | 0.8043 | 9 | 10 |
| fnd6_newqeventv110_invwipq | Inventory - Work in Process | VECTOR | 0.7152 | 6 | 8 |
| fnd6_newqeventv110_ivltq | Total Long-term Investments | VECTOR | 0.9064 | 13 | 14 |
| fnd6_newqeventv110_ivstq | Short-Term Investments - Total | VECTOR | 0.534 | 5 | 5 |
| fnd6_newqeventv110_lcoq | Current Liabilities - Other - Total | VECTOR | 0.7523 | 12 | 15 |
| fnd6_newqeventv110_lltq | Long-Term Liabilities (Total) | VECTOR | 0.6151 | 4 | 6 |
| fnd6_newqeventv110_lnoq | Liabilities Netting & Other Adjustments | VECTOR | 0.8855 | 6 | 8 |
| fnd6_newqeventv110_lol2q | Liabilities Level 2 (Observable) | VECTOR | 0.8848 | 5 | 8 |
| fnd6_newqeventv110_loq | Liabilities - Other | VECTOR | 0.8064 | 17 | 19 |
| fnd6_newqeventv110_loxdrq | Liabilities - Other - Excluding Deferred Revenue | VECTOR | 0.9122 | 10 | 13 |
| fnd6_newqeventv110_lqpl1q | Liabilities Level 1 (Quoted Prices) | VECTOR | 0.8851 | 6 | 17 |
| fnd6_newqeventv110_lseq | Liabilities and Stockholders' Equity - Total | VECTOR | 0.8066 | 8 | 10 |
| fnd6_newqeventv110_ltmibq | Liabilities - Total and Noncontrolling Interest | VECTOR | 0.8066 | 18 | 22 |
| fnd6_newqeventv110_lul3q | Liabilities Level 3 (Unobservable) | VECTOR | 0.8853 | 12 | 27 |
| fnd6_newqeventv110_mibnq | NonRedeemable Noncontrolling Interest (Balance Sheet) - Quarterly | VECTOR | 0.9935 | 9 | 15 |
| fnd6_newqeventv110_mibq | Noncontrolling Interest - Redeemable - Balance Sheet | VECTOR | 0.8021 | 8 | 11 |
| fnd6_newqeventv110_mibtq | Noncontrolling Interests - Total - Balance Sheet - Quarterly | VECTOR | 0.665 | 3 | 3 |
| fnd6_newqeventv110_miiq | Noncontrolling Interest - Income Account | VECTOR | 0.7975 | 8 | 15 |
| fnd6_newqeventv110_msaq | Accum Other Comp Inc - Marketable Security Adjustments | VECTOR | 0.9986 | 42 | 55 |
| fnd6_newqeventv110_nrtxtq | Nonrecurring Income Taxes - After-tax | VECTOR | 0.5282 | 6 | 7 |
| fnd6_newqeventv110_oepf12 | Earnings Per Share - Diluted - from Operations - 12MM | VECTOR | 1.0 | 17 | 34 |
| fnd6_newqeventv110_oepsxq | Earnings Per Share - Diluted - from Operations | VECTOR | 1.0 | 7 | 14 |
| fnd6_newqeventv110_optfvgrq | Options - Fair Value of Options Granted | VECTOR | 0.7475 | 14 | 21 |
| fnd6_newqeventv110_optrfrq | Risk Free Rate - Assumption (%) | VECTOR | 0.8601 | 178 | 223 |
| fnd6_newqeventv110_piq | Pretax Income | VECTOR | 0.8063 | 10 | 14 |
| fnd6_newqeventv110_pnc12 | Pension Core Adjustment - 12mm | VECTOR | 0.6386 | 5 | 6 |
| fnd6_newqeventv110_pnciapq | Core Pension Interest Adjustment After-tax Preliminary | VECTOR | 0.3108 | 1 | 2 |
| fnd6_newqeventv110_pnciaq | Core Pension Interest Adjustment After-tax | VECTOR | 0.3093 | 0 | 0 |
| fnd6_newqeventv110_pncidpq | Core Pension Interest Adjustment Diluted EPS Effect Preliminary | VECTOR | 0.3107 | 0 | 0 |
| fnd6_newqeventv110_pnciepspq | Core Pension Interest Adjustment Basic EPS Effect Preliminary | VECTOR | 0.3107 | 2 | 3 |
| fnd6_newqeventv110_pnciepsq | Core Pension Interest Adjustment Basic EPS Effect | VECTOR | 0.3093 | 1 | 1 |
| fnd6_newqeventv110_pncippq | Core Pension Interest Adjustment Pretax Preliminary | VECTOR | 0.3108 | 0 | 0 |
| fnd6_newqeventv110_pncipq | Core Pension Interest Adjustment Pretax | VECTOR | 0.3093 | 1 | 1 |
| fnd6_newqeventv110_pncpd12 | Core Pension Adjustment 12MM Diluted EPS Effect Preliminary | VECTOR | 0.6385 | 12 | 16 |
| fnd6_newqeventv110_pncpdq | Core Pension Adjustment Diluted EPS Effect Preliminary | VECTOR | 0.6388 | 13 | 13 |
| fnd6_newqeventv110_pncpeps12 | Core Pension Adjustment 12MM Basic EPS Effect Preliminary | VECTOR | 0.6385 | 9 | 10 |
| fnd6_newqeventv110_pncpepsq | Core Pension Adjustment Basic EPS Effect Preliminary | VECTOR | 0.6388 | 14 | 22 |
| fnd6_newqeventv110_pncpq | Core Pension Adjustment Preliminary | VECTOR | 0.639 | 6 | 8 |
| fnd6_newqeventv110_pncq | Core Pension Adjustment | VECTOR | 0.6386 | 7 | 7 |
| fnd6_newqeventv110_pncwiapq | Core Pension w/o Interest Adjustment After-tax Preliminary | VECTOR | 0.3175 | 0 | 0 |
| fnd6_newqeventv110_pncwiaq | Core Pension w/o Interest Adjustment After-tax | VECTOR | 0.3158 | 1 | 1 |
| fnd6_newqeventv110_pncwidpq | Core Pension w/o Interest Adjustment Diluted EPS Effect Preliminary | VECTOR | 0.3174 | 0 | 0 |
| fnd6_newqeventv110_pncwiepq | Core Pension Without Interest Adjustment Basic EPS Effect Preliminary | VECTOR | 0.3174 | 1 | 1 |
| fnd6_newqeventv110_pncwippq | Core Pension w/o Interest Adjustment Pretax Preliminary | VECTOR | 0.3175 | 0 | 0 |
| fnd6_newqeventv110_pncwipq | Core Pension Without Interest Adjustment Pretax | VECTOR | 0.3158 | 1 | 1 |
| fnd6_newqeventv110_pnrshoq | Nonred Pfd Shares Outs (000) - Quarterly | VECTOR | 1.0 | 19 | 28 |
| fnd6_newqeventv110_ppegtq | Property, Plant and Equipment - Total (Gross) - Quarterly | VECTOR | 0.7306 | 6 | 16 |
| fnd6_newqeventv110_ppentq | Property Plant and Equipment - Total (Net) | VECTOR | 0.7894 | 5 | 5 |
| fnd6_newqeventv110_prcaq | Core Post-Retirement Adjustment | VECTOR | 0.6386 | 3 | 3 |
| fnd6_newqeventv110_prcd12 | Core Post Retirement Adjustment Diluted EPS Effect 12 MM | VECTOR | 0.638 | 3 | 3 |
| fnd6_newqeventv110_prcdq | Core Post-Retirement Adjustment Diluted EPS Effect | VECTOR | 0.6383 | 1 | 1 |
| fnd6_newqeventv110_prce12 | Core Post Retirement Adjustment 12MM | VECTOR | 0.6386 | 7 | 15 |
| fnd6_newqeventv110_prceps12 | Core Post Retirement Adjustment Basic EPS Effect 12MM | VECTOR | 0.638 | 2 | 2 |
| fnd6_newqeventv110_prcepsq | Core Post-Retirement Adjustment Basic EPS Effect | VECTOR | 0.6383 | 2 | 2 |
| fnd6_newqeventv110_prcpd12 | Core Post-Retirement Adjustment 12MM Diluted EPS Effect Preliminary | VECTOR | 0.6385 | 2 | 2 |
| fnd6_newqeventv110_prcpdq | Core Post Retirement Adjustment Diluted EPS Effect Preliminary | VECTOR | 0.6388 | 7 | 8 |
| fnd6_newqeventv110_prcpeps12 | Core Post-Retirement Adjustment 12MM Basic EPS Effect Preliminary | VECTOR | 0.6385 | 0 | 0 |
| fnd6_newqeventv110_prcpepsq | Core Post-Retirement Adjustment Basic EPS Effect Preliminary | VECTOR | 0.6388 | 6 | 6 |
| fnd6_newqeventv110_prcpq | Core Post-Retirement Adjustment Preliminary | VECTOR | 0.639 | 8 | 8 |
| fnd6_newqeventv110_prcraq | Repurchase Price - Average per share | VECTOR | 0.8262 | 50 | 69 |
| fnd6_newqeventv110_prshoq | Redeem Pfd Shares Outs (000) | VECTOR | 1.0 | 22 | 42 |
| fnd6_newqeventv110_pstknq | Preferred/Preference Stock - Nonredeemable | VECTOR | 0.8056 | 44 | 54 |
| fnd6_newqeventv110_pstkq | Preferred/Preference Stock (Capital) - Total | VECTOR | 0.8059 | 13 | 22 |
| fnd6_newqeventv110_pstkrq | Preferred/Preference Stock - Redeemable | VECTOR | 0.8008 | 3 | 28 |
| fnd6_newqeventv110_rcaq | Restructuring Cost After-tax | VECTOR | 0.5045 | 3 | 4 |
| fnd6_newqeventv110_rcdq | Restructuring Cost Diluted EPS Effect | VECTOR | 0.4748 | 1 | 1 |
| fnd6_newqeventv110_rcepsq | Restructuring Cost Basic EPS Effect | VECTOR | 0.4581 | 0 | 0 |
| fnd6_newqeventv110_rcpq | Restructuring Cost Pretax | VECTOR | 0.5951 | 11 | 17 |
| fnd6_newqeventv110_rdipaq | In Process R&D Expense After-tax | VECTOR | 0.7982 | 17 | 26 |
| fnd6_newqeventv110_rdipdq | In-Process R&D Expense Diluted EPS Effect | VECTOR | 0.7889 | 16 | 19 |
| fnd6_newqeventv110_rdipepsq | In-Process R&D Expense Basic EPS Effect | VECTOR | 0.7889 | 27 | 38 |
| fnd6_newqeventv110_rdipq | In Process R&D | VECTOR | 0.9159 | 16 | 92 |
| fnd6_newqeventv110_recdq | Receivables - Estimated Doubtful | VECTOR | 0.778 | 9 | 12 |
| fnd6_newqeventv110_rectaq | Accum Other Comp Inc - Cumulative Translation Adjustments | VECTOR | 1.0 | 14 | 17 |
| fnd6_newqeventv110_rectoq | Receivables - Current Other incl. Tax Refunds | VECTOR | 0.9126 | 27 | 30 |
| fnd6_newqeventv110_rectrq | Receivables - Trade | VECTOR | 0.8992 | 3 | 5 |
| fnd6_newqeventv110_reunaq | Unadjusted Retained Earnings | VECTOR | 0.9825 | 8 | 11 |
| fnd6_newqeventv110_revtq | Revenue - Total | VECTOR | 0.7522 | 11 | 13 |
| fnd6_newqeventv110_rrpq | Reversal - Restructuring/Acquisition Pretax | VECTOR | 0.2572 | 3 | 4 |
| fnd6_newqeventv110_seqoq | Other Stockholders' Equity Adjustments | VECTOR | 0.9153 | 19 | 35 |
| fnd6_newqeventv110_seqq | Stockholders' Equity - Total - Quarterly | VECTOR | 0.8065 | 13 | 28 |
| fnd6_newqeventv110_seta12 | Settlement (Litigation/Insurance) After Tax - 12mm | VECTOR | 0.4381 | 1 | 2 |
| fnd6_newqeventv110_setaq | Settlement (Litigation/Insurance) After-tax | VECTOR | 0.5108 | 2 | 2 |
| fnd6_newqeventv110_setd12 | Settlement (Litigation/Insurance) Diluted EPS Effect 12MM | VECTOR | 0.4367 | 7 | 7 |
| fnd6_newqeventv110_seteps12 | Settlement (Litigation/Insurance) Basic EPS Effect 12MM | VECTOR | 0.4365 | 10 | 11 |
| fnd6_newqeventv110_setpq | Settlement (Litigation/Insurance) Pretax | VECTOR | 0.5792 | 2 | 3 |
| fnd6_newqeventv110_spce12 | S&P Core Earnings 12MM | VECTOR | 0.6386 | 7 | 16 |
| fnd6_newqeventv110_spcedpq | S&P Core Earnings EPS Diluted - Preliminary | VECTOR | 0.6389 | 4 | 4 |
| fnd6_newqeventv110_spcedq | S&P Core Earnings EPS Diluted | VECTOR | 0.6384 | 12 | 18 |
| fnd6_newqeventv110_spceeps12 | S&P Core Earnings EPS Basic 12MM | VECTOR | 0.6383 | 5 | 7 |
| fnd6_newqeventv110_spceepsp12 | S&P Core 12MM EPS - Basic - Preliminary | VECTOR | 0.6387 | 4 | 4 |
| fnd6_newqeventv110_spceepspq | S&P Core Earnings EPS Basic - Preliminary | VECTOR | 0.6389 | 6 | 8 |
| fnd6_newqeventv110_spceepsq | S&P Core Earnings EPS Basic | VECTOR | 0.6384 | 15 | 16 |
| fnd6_newqeventv110_spcep12 | S&P Core Earnings 12MM - Preliminary | VECTOR | 0.639 | 12 | 14 |
| fnd6_newqeventv110_spcepd12 | S&P Core Earnings 12MM EPS Diluted - Preliminary | VECTOR | 0.6387 | 10 | 11 |
| fnd6_newqeventv110_spcepq | S&P Core Earnings - Preliminary | VECTOR | 0.6392 | 7 | 7 |
| fnd6_newqeventv110_spceq | S&P Core Earnings | VECTOR | 0.6386 | 5 | 7 |
| fnd6_newqeventv110_spioaq | Other Special Items After-tax | VECTOR | 0.5741 | 5 | 5 |
| fnd6_newqeventv110_spiopq | Other Special Items Pretax | VECTOR | 0.7134 | 5 | 6 |
| fnd6_newqeventv110_spiq | Special Items | VECTOR | 0.7978 | 6 | 12 |
| fnd6_newqeventv110_stkcoq | Stock Compensation Expense | VECTOR | 0.962 | 18 | 33 |
| fnd6_newqeventv110_stkcpaq | After-tax stock compensation | VECTOR | 0.7545 | 12 | 13 |
| fnd6_newqeventv110_teqq | Stockholders' Equity - Total - Quarterly | VECTOR | 0.6624 | 6 | 7 |
| fnd6_newqeventv110_tfvaq | Total Fair Value Assets | VECTOR | 0.8867 | 11 | 13 |
| fnd6_newqeventv110_tfvceq | Total Fair Value Changes including Earnings | VECTOR | 0.4961 | 1 | 1 |
| fnd6_newqeventv110_tfvlq | Total Fair Value Liabilities | VECTOR | 0.8849 | 11 | 14 |
| fnd6_newqeventv110_tstknq | Treasury Stock - Number of Common Shares | VECTOR | 1.0 | 25 | 37 |
| fnd6_newqeventv110_tstkq | Treasury Stock - Total (All Capital) | VECTOR | 0.7965 | 47 | 61 |
| fnd6_newqeventv110_txdbaq | Deferred Tax Asset - Long Term | VECTOR | 0.5866 | 3 | 4 |
| fnd6_newqeventv110_txdbq | Deferred Taxes - Balance Sheet | VECTOR | 0.4429 | 3 | 6 |
| fnd6_newqeventv110_txdiq | Income Taxes - Deferred | VECTOR | 0.7449 | 1 | 1 |
| fnd6_newqeventv110_txditcq | Deferred Taxes and Investment Tax Credit | VECTOR | 0.7491 | 8 | 8 |
| fnd6_newqeventv110_txpq | Income Taxes Payable | VECTOR | 0.7503 | 7 | 12 |
| fnd6_newqeventv110_txtq | Income Taxes - Total | VECTOR | 0.8064 | 7 | 9 |
| fnd6_newqeventv110_txwq | Excise Taxes | VECTOR | 0.8761 | 5 | 9 |
| fnd6_newqeventv110_wcapq | Working Capital (Balance Sheet) | VECTOR | 0.6672 | 10 | 13 |
| fnd6_newqeventv110_wdaq | Writedowns After-tax | VECTOR | 0.5103 | 0 | 0 |
| fnd6_newqeventv110_wdpq | Writedowns Pretax | VECTOR | 0.6316 | 4 | 5 |
| fnd6_newqeventv110_xidoq | Extraordinary Items and Discontinued Operations | VECTOR | 0.8064 | 18 | 21 |
| fnd6_newqeventv110_xintq | Interest and Related Expense - Total | VECTOR | 0.7389 | 5 | 8 |
| fnd6_newqeventv110_xiq | Extraordinary Items | VECTOR | 0.7881 | 7 | 15 |
| fnd6_newqeventv110_xoprq | Operating Expense - Total | VECTOR | 0.7723 | 12 | 15 |
| fnd6_newqeventv110_xopt12 | Implied Option Expense - 12mm | VECTOR | 0.622 | 11 | 12 |
| fnd6_newqeventv110_xoptd12 | Implied Option EPS Diluted 12MM | VECTOR | 0.6219 | 13 | 20 |
| fnd6_newqeventv110_xoptd12p | Implied Option 12MM EPS Diluted Preliminary | VECTOR | 0.622 | 15 | 19 |
| fnd6_newqeventv110_xoptdq | Implied Option EPS Diluted | VECTOR | 0.9299 | 12 | 23 |
| fnd6_newqeventv110_xoptdqp | Implied Option EPS Diluted Preliminary | VECTOR | 0.6229 | 15 | 22 |
| fnd6_newqeventv110_xopteps12 | Implied Option EPS Basic 12MM | VECTOR | 0.6219 | 14 | 18 |
| fnd6_newqeventv110_xoptepsp12 | Implied Option 12MM EPS Basic Preliminary | VECTOR | 0.622 | 14 | 18 |
| fnd6_newqeventv110_xoptepsq | Implied Option EPS Basic | VECTOR | 0.9299 | 17 | 25 |
| fnd6_newqeventv110_xoptepsqp | Implied Option EPS Basic Preliminary | VECTOR | 0.6229 | 19 | 23 |
| fnd6_newqeventv110_xoptq | Implied Option Expense | VECTOR | 0.93 | 14 | 21 |
| fnd6_newqeventv110_xoptqp | Implied Option Expense Preliminary | VECTOR | 0.6231 | 11 | 15 |
| fnd6_newqeventv110_xrdq | Research and Development Expense | VECTOR | 0.5878 | 28 | 33 |
| fnd6_newqeventv110_xsgaq | Selling, General and Administrative Expenses | VECTOR | 0.6785 | 14 | 17 |
| fnd6_newqv1300_acomincq | Accumulated Other Comprehensive Income (Loss) | MATRIX | 0.6994 | 99 | 1038 |
| fnd6_newqv1300_acoq | Current Assets - Other - Total | MATRIX | 0.8835 | 53 | 210 |
| fnd6_newqv1300_altoq | Other Long-term Assets | MATRIX | 0.6501 | 68 | 209 |
| fnd6_newqv1300_ancq | Non-Current Assets - Total | MATRIX | 0.7647 | 132 | 1412 |
| fnd6_newqv1300_anoq | Assets Netting & Other Adjustments | MATRIX | 0.7359 | 32 | 127 |
| fnd6_newqv1300_aociderglq | Accum Other Comp Inc - Derivatives Unrealized Gain/Loss | MATRIX | 0.8557 | 70 | 215 |
| fnd6_newqv1300_aociotherq | Accumulated Other Comprehensive Income - Other Adjustments | MATRIX | 0.8845 | 56 | 339 |
| fnd6_newqv1300_aocipenq | Accum Other Comp Inc - Min Pension Liab Adj | MATRIX | 0.8637 | 42 | 147 |
| fnd6_newqv1300_aocisecglq | Accum Other Comp Inc - Unreal G/L Ret Int in Sec Assets | MATRIX | 0.8829 | 87 | 277 |
| fnd6_newqv1300_aol2q | Assets Level 2 (Observable) | MATRIX | 0.7352 | 55 | 77 |
| fnd6_newqv1300_aoq | Assets - Other - Total | MATRIX | 0.945 | 131 | 490 |
| fnd6_newqv1300_aqpl1q | Assets Level 1 (Quoted Prices) | MATRIX | 0.7353 | 63 | 183 |
| fnd6_newqv1300_aul3q | Assets Level 3 (Unobservable) | MATRIX | 0.7355 | 32 | 80 |
| fnd6_newqv1300_capsq | Capital Surplus/Share Premium Reserve | MATRIX | 0.8398 | 79 | 326 |
| fnd6_newqv1300_chq | Cash | MATRIX | 0.533 | 56 | 210 |
| fnd6_newqv1300_cibegniq | Comp Inc - Beginning Net Income | MATRIX | 0.8928 | 74 | 179 |
| fnd6_newqv1300_cicurrq | Comp Inc - Currency Trans Adj | MATRIX | 0.878 | 42 | 118 |
| fnd6_newqv1300_ciderglq | Comp Inc - Derivative Gains/Losses | MATRIX | 0.8786 | 41 | 121 |
| fnd6_newqv1300_cimiiq | Comprehensive Income - Noncontrolling Interest | MATRIX | 0.3409 | 43 | 102 |
| fnd6_newqv1300_ciotherq | Comp Inc - Other Adj | MATRIX | 0.8917 | 62 | 301 |
| fnd6_newqv1300_cipenq | Comp Inc - Minimum Pension Adj | MATRIX | 0.884 | 45 | 183 |
| fnd6_newqv1300_ciq | Comprehensive Income - Total | MATRIX | 0.9757 | 75 | 327 |
| fnd6_newqv1300_cisecglq | Comp Inc - Securities Gains/Losses | MATRIX | 0.8792 | 54 | 121 |
| fnd6_newqv1300_citotalq | Comprehensive Income - Parent | MATRIX | 0.8949 | 38 | 217 |
| fnd6_newqv1300_cogsq | Cost of Goods Sold | MATRIX | 0.942 | 86 | 290 |
| fnd6_newqv1300_csh12q | Common Shares Used to Calculate Earnings Per Share - 12 Months Moving | MATRIX | 0.968 | 99 | 233 |
| fnd6_newqv1300_cshfdq | Common Shares for Diluted EPS | MATRIX | 0.9615 | 71 | 314 |
| fnd6_newqv1300_cshiq | Common Shares Issued | MATRIX | 0.8861 | 58 | 282 |
| fnd6_newqv1300_cshopq | Total Shares Repurchased - Quarter | MATRIX | 0.5664 | 13 | 68 |
| fnd6_newqv1300_cshoq | Common Shares Outstanding | MATRIX | 0.9431 | 61 | 124 |
| fnd6_newqv1300_cshprq | Common Shares Used to Calculate Earnings Per Share - Basic | MATRIX | 0.9663 | 96 | 404 |
| fnd6_newqv1300_cstkq | Common/Ordinary Stock (Capital) | MATRIX | 0.9042 | 72 | 402 |
| fnd6_newqv1300_dcomq | Deferred Compensation | MATRIX | 0.6441 | 73 | 376 |
| fnd6_newqv1300_dilavq | Dilution Available - Excluding Extraordinary Items | MATRIX | 0.9557 | 97 | 563 |
| fnd6_newqv1300_dlcq | Debt in Current Liabilities | MATRIX | 0.8796 | 54 | 413 |
| fnd6_newqv1300_dpactq | Depreciation, Depletion and Amortization (Accumulated) | MATRIX | 0.5395 | 59 | 184 |
| fnd6_newqv1300_drcq | Deferred Revenue - Current | MATRIX | 0.5532 | 487 | 1033 |
| fnd6_newqv1300_drltq | Deferred Revenue - Long-term | MATRIX | 0.6034 | 416 | 1023 |
| fnd6_newqv1300_epsfiq | Earnings Per Share (Diluted) - Including Extraordinary Items | MATRIX | 0.954 | 75 | 340 |
| fnd6_newqv1300_epspiq | Earnings Per Share (Basic) - Including Extraordinary Items | MATRIX | 0.954 | 55 | 189 |
| fnd6_newqv1300_epspxq | Earnings Per Share (Basic) - Excluding Extraordinary Items | MATRIX | 0.9537 | 69 | 217 |
| fnd6_newqv1300_esopnrq | Preferred ESOP Obligation - Non-Redeemable | MATRIX | 0.8908 | 181 | 412 |
| fnd6_newqv1300_esoprq | Preferred ESOP Obligation - Redeemable | MATRIX | 0.89 | 165 | 339 |
| fnd6_newqv1300_fcaq | Foreign Exchange Income (Loss) | MATRIX | 0.2598 | 27 | 36 |
| fnd6_newqv1300_gdwlq | Goodwill (net) | MATRIX | 0.691 | 121 | 345 |
| fnd6_newqv1300_glcea12 | Gain/Loss on Sale (Core Earnings Adjusted) After-tax 12MM | MATRIX | 0.263 | 7 | 35 |
| fnd6_newqv1300_glced12 | Gain/Loss on Sale (Core Earnings Adjusted) Diluted EPS Effect 12MM | MATRIX | 0.2625 | 6 | 13 |
| fnd6_newqv1300_glceeps12 | Gain/Loss on Sale (Core Earnings Adjusted) Basic EPS Effect 12MM | MATRIX | 0.2624 | 3 | 13 |
| fnd6_newqv1300_ibadj12 | Income Before Extra Items - Adj for Common Stock Equivalents - 12MM | MATRIX | 0.6686 | 48 | 324 |
| fnd6_newqv1300_ibadjq | Income Before Extraordinary Items - Adjusted for Common Stock Equivalents | MATRIX | 0.9603 | 61 | 209 |
| fnd6_newqv1300_ibcomq | Income Before Extraordinary Items - Available for Common | MATRIX | 0.9602 | 74 | 247 |
| fnd6_newqv1300_ibmiiq | Income before Extraordinary Items and Noncontrolling Interests | MATRIX | 0.982 | 79 | 490 |
| fnd6_newqv1300_ibq | Income Before Extraordinary Items | MATRIX | 0.9603 | 53 | 338 |
| fnd6_newqv1300_icaptq | Invested Capital - Total - Quarterly | MATRIX | 0.9191 | 121 | 514 |
| fnd6_newqv1300_intanoq | Other Intangibles | MATRIX | 0.6529 | 105 | 886 |
| fnd6_newqv1300_intanq | Intangible Assets - Total | MATRIX | 0.7236 | 107 | 418 |
| fnd6_newqv1300_invfgq | Inventory - Finished Goods | MATRIX | 0.6005 | 43 | 265 |
| fnd6_newqv1300_invoq | Inventory - Other | MATRIX | 0.6076 | 64 | 167 |
| fnd6_newqv1300_invrmq | Inventory - Raw Materials | MATRIX | 0.5938 | 52 | 200 |
| fnd6_newqv1300_invtq | Inventories - Total | MATRIX | 0.6619 | 89 | 284 |
| fnd6_newqv1300_invwipq | Inventory - Work in Process | MATRIX | 0.5871 | 43 | 286 |
| fnd6_newqv1300_ivltq | Total Long-term Investments | MATRIX | 0.5692 | 44 | 157 |
| fnd6_newqv1300_ivstq | Short-Term Investments - Total | MATRIX | 0.5136 | 26 | 71 |
| fnd6_newqv1300_lcoq | Current Liabilities - Other - Total | MATRIX | 0.881 | 386 | 591 |
| fnd6_newqv1300_lltq | Long-Term Liabilities (Total) | MATRIX | 0.7648 | 141 | 390 |
| fnd6_newqv1300_lnoq | Liabilities Netting & Other Adjustments | MATRIX | 0.7341 | 36 | 51 |
| fnd6_newqv1300_lol2q | Liabilities Level 2 (Observable) | MATRIX | 0.7335 | 32 | 127 |
| fnd6_newqv1300_loq | Liabilities - Other | MATRIX | 0.8699 | 38 | 145 |
| fnd6_newqv1300_loxdrq | Liabilities - Other - Excluding Deferred Revenue | MATRIX | 0.8892 | 68 | 259 |
| fnd6_newqv1300_lqpl1q | Liabilities Level 1 (Quoted Prices) | MATRIX | 0.7337 | 36 | 251 |
| fnd6_newqv1300_lseq | Liabilities and Stockholders' Equity - Total | MATRIX | 0.9523 | 107 | 330 |
| fnd6_newqv1300_ltmibq | Liabilities - Total and Noncontrolling Interest | MATRIX | 0.9359 | 102 | 351 |
| fnd6_newqv1300_lul3q | Liabilities Level 3 (Unobservable) | MATRIX | 0.7337 | 75 | 121 |
| fnd6_newqv1300_mibnq | Non-Redeemable Noncontrolling Interest (Balance Sheet) - Quarterly | MATRIX | 0.3675 | 38 | 124 |
| fnd6_newqv1300_mibtq | Noncontrolling Interests - Total - Balance Sheet - Quarterly | MATRIX | 0.384 | 27 | 68 |
| fnd6_newqv1300_miiq | Noncontrolling Interest - Income Account | MATRIX | 0.8771 | 76 | 373 |
| fnd6_newqv1300_msaq | Accumulated Other Comprehensive Income - Marketable Security Adjustments | MATRIX | 0.6391 | 52 | 301 |
| fnd6_newqv1300_oepf12 | Earnings Per Share - Diluted - from Operations - 12MM | MATRIX | 0.9356 | 117 | 614 |
| fnd6_newqv1300_oepsxq | Earnings Per Share - Diluted - from Operations | MATRIX | 0.9529 | 86 | 353 |
| fnd6_newqv1300_optfvgrq | Options - Fair Value of Options Granted | MATRIX | 0.3365 | 108 | 211 |
| fnd6_newqv1300_optrfrq | Risk-Free Rate - Assumption (%) | MATRIX | 0.3492 | 20 | 62 |
| fnd6_newqv1300_piq | Pretax Income | MATRIX | 0.9575 | 86 | 314 |
| fnd6_newqv1300_pncq | Core Pension Adjustment | MATRIX | 0.3867 | 5 | 8 |
| fnd6_newqv1300_ppegtq | Property, Plant and Equipment - Total (Gross) - Quarterly | MATRIX | 0.5321 | 90 | 204 |
| fnd6_newqv1300_ppentq | Property Plant and Equipment - Total (Net) | MATRIX | 0.8834 | 121 | 369 |
| fnd6_newqv1300_prcaq | Core Post Retirement Adjustment | MATRIX | 0.3866 | 3 | 3 |
| fnd6_newqv1300_prcdq | Core Post Retirement Adjustment Diluted EPS Effect | MATRIX | 0.3841 | 4 | 10 |
| fnd6_newqv1300_prcepsq | Core Post Retirement Adjustment Basic EPS Effect | MATRIX | 0.3841 | 4 | 4 |
| fnd6_newqv1300_prcraq | Repurchase Price - Average per share | MATRIX | 0.5458 | 49 | 71 |
| fnd6_newqv1300_rcpq | Restructuring Cost Pretax | MATRIX | 0.2662 | 23 | 59 |
| fnd6_newqv1300_rdipaq | In Process R&D Expense After-tax | MATRIX | 0.6201 | 42 | 109 |
| fnd6_newqv1300_rdipdq | In Process R&D Expense Diluted EPS Effect | MATRIX | 0.6186 | 31 | 170 |
| fnd6_newqv1300_rdipepsq | In-Process R&D Expense Basic EPS Effect | MATRIX | 0.6184 | 26 | 64 |
| fnd6_newqv1300_rdipq | In Process R&D | MATRIX | 0.8625 | 125 | 267 |
| fnd6_newqv1300_recdq | Receivables - Estimated Doubtful | MATRIX | 0.4678 | 89 | 370 |
| fnd6_newqv1300_rectaq | Accum Other Comp Inc - Cumulative Translation Adjustments | MATRIX | 0.6575 | 63 | 288 |
| fnd6_newqv1300_rectoq | Receivables - Current Other incl Tax Refunds | MATRIX | 0.5761 | 56 | 216 |
| fnd6_newqv1300_rectrq | Receivables - Trade | MATRIX | 0.5865 | 56 | 198 |
| fnd6_newqv1300_reunaq | Unadjusted Retained Earnings | MATRIX | 0.6993 | 63 | 294 |
| fnd6_newqv1300_revtq | Revenue - Total | MATRIX | 0.8942 | 52 | 231 |
| fnd6_newqv1300_seqoq | Other Stockholders' Equity Adjustments | MATRIX | 0.6418 | 339 | 556 |
| fnd6_newqv1300_seqq | Stockholders' Equity - Total - Quarterly | MATRIX | 0.9349 | 76 | 271 |
| fnd6_newqv1300_spcedpq | S&P Core Earnings EPS Diluted - Preliminary | MATRIX | 0.6805 | 17 | 231 |
| fnd6_newqv1300_spcedq | S&P Core Earnings EPS Diluted | MATRIX | 0.4547 | 4 | 14 |
| fnd6_newqv1300_spceepsp12 | S&P Core 12MM EPS - Basic - Preliminary | MATRIX | 0.426 | 2 | 4 |
| fnd6_newqv1300_spceepspq | S&P Core Earnings EPS Basic - Preliminary | MATRIX | 0.6805 | 13 | 94 |
| fnd6_newqv1300_spceepsq | S&P Core Earnings EPS Basic | MATRIX | 0.4549 | 3 | 4 |
| fnd6_newqv1300_spcep12 | S&P Core Earnings 12MM - Preliminary | MATRIX | 0.4269 | 2 | 6 |
| fnd6_newqv1300_spcepd12 | S&P Core Earnings 12MM EPS Diluted - Preliminary | MATRIX | 0.426 | 6 | 21 |
| fnd6_newqv1300_spcepq | S&P Core Earnings - Preliminary | MATRIX | 0.6823 | 20 | 209 |
| fnd6_newqv1300_spceq | S&P Core Earnings | MATRIX | 0.4603 | 3 | 3 |
| fnd6_newqv1300_spiq | Special Items | MATRIX | 0.5015 | 32 | 102 |
| fnd6_newqv1300_stkcoq | Stock Compensation Expense | MATRIX | 0.6286 | 56 | 115 |
| fnd6_newqv1300_stkcpaq | After-tax stock compensation | MATRIX | 0.3035 | 29 | 114 |
| fnd6_newqv1300_teqq | Stockholders' Equity - Total - Quarterly | MATRIX | 1.0 | 211 | 780 |
| fnd6_newqv1300_tfvaq | Total Fair Value Assets | MATRIX | 0.7355 | 39 | 69 |
| fnd6_newqv1300_tfvceq | Total Fair Value Changes including Earnings | MATRIX | 0.3889 | 38 | 59 |
| fnd6_newqv1300_tfvlq | Total Fair Value Liabilities | MATRIX | 0.7338 | 34 | 76 |
| fnd6_newqv1300_tstknq | Treasury Stock - Number of Common Shares | MATRIX | 0.8899 | 68 | 193 |
| fnd6_newqv1300_tstkq | Treasury Stock - Total (All Capital) | MATRIX | 0.4352 | 43 | 99 |
| fnd6_newqv1300_txdbaq | Deferred Tax Asset - Long Term | MATRIX | 0.3863 | 27 | 306 |
| fnd6_newqv1300_txdbq | Deferred Taxes - Balance Sheet | MATRIX | 0.4074 | 28 | 94 |
| fnd6_newqv1300_txdiq | Income Taxes - Deferred | MATRIX | 0.3141 | 24 | 90 |
| fnd6_newqv1300_txditcq | Deferred Taxes and Investment Tax Credit | MATRIX | 0.7888 | 68 | 475 |
| fnd6_newqv1300_txpq | Income Taxes Payable | MATRIX | 0.7903 | 65 | 349 |
| fnd6_newqv1300_txtq | Income Taxes - Total | MATRIX | 0.8662 | 83 | 432 |
| fnd6_newqv1300_txwq | Excise Taxes | MATRIX | 0.7126 | 120 | 314 |
| fnd6_newqv1300_wcapq | Working Capital (Balance Sheet) | MATRIX | 0.7487 | 55 | 180 |
| fnd6_newqv1300_xintq | Interest and Related Expense - Total | MATRIX | 0.7851 | 50 | 234 |
| fnd6_newqv1300_xoprq | Operating Expense - Total | MATRIX | 0.9895 | 133 | 522 |
| fnd6_newqv1300_xoptdq | Implied Option EPS Diluted | MATRIX | 0.5626 | 5 | 6 |
| fnd6_newqv1300_xoptepsq | Implied Option EPS Basic | MATRIX | 0.5626 | 6 | 13 |
| fnd6_newqv1300_xoptq | Implied Option Expense | MATRIX | 0.5628 | 8 | 99 |
| fnd6_newqv1300_xrdq | Research and Development Expense | MATRIX | 0.4405 | 209 | 474 |
| fnd6_newqv1300_xsgaq | Selling, General and Administrative Expenses | MATRIX | 0.7618 | 76 | 488 |
| fnd6_niadj | Net Income Adjusted for Common/Ordinary Stock (Capital) Equivalents | MATRIX | 0.9295 | 119 | 466 |
| fnd6_nis | Net Income (Loss) | VECTOR | 0.84 | 9 | 10 |
| fnd6_nopio | Nonoperating Income (Expense) - Other | MATRIX | 0.8478 | 65 | 142 |
| fnd6_nopxs | Nonoperating Income (Expense) - excluding Interest | VECTOR | 0.5683 | 7 | 8 |
| fnd6_np | Notes Payable - Short-Term Borrowings | MATRIX | 0.3235 | 49 | 110 |
| fnd6_npq | Notes Payable | MATRIX | 0.889 | 66 | 172 |
| fnd6_nxints | Net Interest Income (Expense) | VECTOR | 0.3591 | 4 | 5 |
| fnd6_obs | Order Backlog | VECTOR | 0.6978 | 2 | 2 |
| fnd6_ocaxs | Other Costs and Expenses | VECTOR | 0.5455 | 3 | 3 |
| fnd6_oelim | Other Eliminations (Income) | VECTOR | 0.9592 | 15 | 18 |
| fnd6_oiadps | Operating Income after Depreciation | VECTOR | 0.9354 | 15 | 19 |
| fnd6_oibdps | Operating Income before Depreciation | VECTOR | 0.9314 | 6 | 7 |
| fnd6_oprepsx | Earnings Per Share - Diluted - from Operations | MATRIX | 0.9345 | 107 | 414 |
| fnd6_ops | Operating Profit (Loss) | VECTOR | 0.9354 | 6 | 9 |
| fnd6_optca | Options - Cancelled (-) | MATRIX | 0.7542 | 159 | 654 |
| fnd6_optdr | Dividend Rate - Assumption (%) | MATRIX | 0.5139 | 97 | 471 |
| fnd6_optdrq | Dividend Rate - Assumption (%) | MATRIX | 0.341 | 68 | 118 |
| fnd6_optex | Options Exercisable (000) | MATRIX | 0.7389 | 145 | 629 |
| fnd6_optfvgr | Options - Fair Value of Options Granted | MATRIX | 0.5051 | 67 | 438 |
| fnd6_optgr | Options - Granted | MATRIX | 0.7566 | 108 | 405 |
| fnd6_optlife | Life of Options - Assumption (# yrs) | MATRIX | 0.5198 | 113 | 454 |
| fnd6_optlifeq | Life of Options - Assumption (# yrs) | MATRIX | 0.3475 | 33 | 146 |
| fnd6_optosby | Options Outstanding - Beginning of Year | MATRIX | 0.7564 | 130 | 508 |
| fnd6_optosey | Options Outstanding - End of Year | MATRIX | 0.6587 | 107 | 634 |
| fnd6_optprcby | Options Outstanding Beginning of Year - Price | MATRIX | 0.7105 | 124 | 428 |
| fnd6_optprcca | Options Cancelled - Price | MATRIX | 0.6328 | 131 | 389 |
| fnd6_optprcex | Options Exercised - Price | MATRIX | 0.6522 | 92 | 409 |
| fnd6_optprcey | Options Outstanding End of Year - Price | MATRIX | 0.6206 | 82 | 290 |
| fnd6_optprcgr | Options Granted - Price | MATRIX | 0.5368 | 80 | 352 |
| fnd6_optprcwa | Options Exercisable - Weighted Avg Price | MATRIX | 0.6865 | 75 | 186 |
| fnd6_optrfr | Risk-Free Rate - Assumption (%) | MATRIX | 0.5245 | 136 | 488 |
| fnd6_optvol | Volatility - Assumption (%) | MATRIX | 0.526 | 115 | 525 |
| fnd6_optvolq | Volatility - Assumption (%) | MATRIX | 0.3504 | 49 | 164 |
| fnd6_pidom | Pretax Income - Domestic | MATRIX | 0.3877 | 107 | 202 |
| fnd6_pifo | Pretax Income - Foreign | MATRIX | 0.3838 | 193 | 321 |
| fnd6_pncdq | Core Pension Adjustment Diluted EPS Effect | MATRIX | 0.3841 | 9 | 13 |
| fnd6_pncepsq | Core Pension Adjustment Basic EPS Effect | MATRIX | 0.3841 | 9 | 26 |
| fnd6_pnrsho | Nonred Pfd Shares Outs (000) | MATRIX | 0.6551 | 136 | 338 |
| fnd6_ppents | Property, Plant & Equipment | VECTOR | 0.5667 | 66 | 130 |
| fnd6_ppeveb | Property, Plant, and Equipment - Ending Balance (Schedule V) | MATRIX | 0.7883 | 101 | 320 |
| fnd6_prcc | Price Close - Annual | MATRIX | 0.9663 | 124 | 517 |
| fnd6_prccq | Price Close - Quarter | MATRIX | 0.9607 | 94 | 461 |
| fnd6_prch | Price High - Annual | MATRIX | 0.9663 | 66 | 172 |
| fnd6_prchq | Price High - Quarter | MATRIX | 0.9607 | 85 | 276 |
| fnd6_prcl | Price Low - Annual | MATRIX | 0.9663 | 85 | 269 |
| fnd6_prclq | Price Low - Quarter | MATRIX | 0.9607 | 70 | 512 |
| fnd6_prstkc | Purchase of Common and Preferred Stock | MATRIX | 0.834 | 73 | 327 |
| fnd6_pstkc | Preferred Stock - Convertible | MATRIX | 0.8372 | 95 | 222 |
| fnd6_pstkl | Preferred Stock - Liquidating Value | MATRIX | 0.8974 | 68 | 132 |
| fnd6_pstkrv | Preferred Stock - Redemption Value | MATRIX | 0.8986 | 65 | 164 |
| fnd6_ptis | Pretax Income | VECTOR | 0.8488 | 5 | 13 |
| fnd6_rank | SP rank with the following meaning: // 0----invalid rank //1----A+//2----A//3----A-//4----B+//5----B//6----B-//7----C+//8----C//9----C- | MATRIX | 0.731 | 66 | 293 |
| fnd6_ranks | Ranking | VECTOR | 0.967 | 41 | 53 |
| fnd6_rds | Research and Development | VECTOR | 0.7722 | 8 | 16 |
| fnd6_rea | Retained Earnings - Restatement | MATRIX | 0.7654 | 388 | 866 |
| fnd6_reajo | Retained Earnings - Other Adjustments | MATRIX | 0.8646 | 118 | 365 |
| fnd6_recco | Receivables - Current - Other | MATRIX | 0.8192 | 122 | 390 |
| fnd6_recd | Receivables - Estimated Doubtful | MATRIX | 0.5943 | 237 | 864 |
| fnd6_recta | Retained Earnings - Cumulative Translation Adjustment | MATRIX | 0.6449 | 111 | 336 |
| fnd6_rectr | Receivables - Trade | MATRIX | 0.8088 | 113 | 488 |
| fnd6_revts | Total Revenues | VECTOR | 0.9655 | 18 | 20 |
| fnd6_sales | Net Sales | VECTOR | 0.9664 | 16 | 33 |
| fnd6_salexg | Export Sales | VECTOR | 0.6372 | 2 | 5 |
| fnd6_sics | SIC Code | VECTOR | 0.967 | 21 | 37 |
| fnd6_siv | Sale of Investments | MATRIX | 0.8429 | 67 | 258 |
| fnd6_snms | Segment Name | VECTOR | 0.967 | 10 | 12 |
| fnd6_spce | S&P Core Earnings | MATRIX | 0.7769 | 18 | 99 |
| fnd6_spis | Special Items | VECTOR | 0.7915 | 11 | 17 |
| fnd6_sppe | Sale of Property | MATRIX | 0.6876 | 71 | 183 |
| fnd6_sppiv | Sale of Property, Plant and Equipment and Investments - Gain (Loss) | MATRIX | 0.8416 | 86 | 277 |
| fnd6_sstk | Sale of Common and Preferred Stock | MATRIX | 0.8671 | 91 | 561 |
| fnd6_state | integer for identifying the state of the company | MATRIX | 1.0 | 233 | 1181 |
| fnd6_stkcpa | After-tax stock compensation | MATRIX | 0.3881 | 32 | 171 |
| fnd6_stype | Segment Type | VECTOR | 0.967 | 78 | 113 |
| fnd6_teq | Stockholders' Equity - Total | MATRIX | 0.9852 | 316 | 915 |
| fnd6_tfva | Total Fair Value Assets | MATRIX | 0.7089 | 108 | 223 |
| fnd6_tfvce | Total Fair Value Changes including Earnings | MATRIX | 0.378 | 30 | 60 |
| fnd6_tfvl | Total Fair Value Liabilities | MATRIX | 0.7077 | 61 | 218 |
| fnd6_tlcf | Tax Loss Carry Forward | MATRIX | 0.5869 | 78 | 244 |
| fnd6_tstkc | Treasury Stock - Common | MATRIX | 0.8986 | 76 | 365 |
| fnd6_txbco | Excess Tax Benefit Stock Options - Cash Flow Operating | MATRIX | 0.6316 | 185 | 446 |
| fnd6_txbcof | Excess Tax Benefit of Stock Options - Cash Flow Financing | MATRIX | 0.8661 | 73 | 159 |
| fnd6_txc | Income Taxes - Current | MATRIX | 0.6786 | 118 | 417 |
| fnd6_txdba | Deferred Tax Asset - Long Term | MATRIX | 0.6818 | 72 | 276 |
| fnd6_txdbca | Deferred Tax Asset - Current | MATRIX | 0.6102 | 59 | 347 |
| fnd6_txdbcl | Deferred Tax Liability - Current | MATRIX | 0.5927 | 38 | 98 |
| fnd6_txdbclq | Current Deferred Tax Liability | MATRIX | 0.7744 | 89 | 152 |
| fnd6_txdc | Deferred Taxes (Cash Flow) | MATRIX | 0.8472 | 92 | 260 |
| fnd6_txdfed | Deferred Taxes - Federal | MATRIX | 0.5981 | 65 | 282 |
| fnd6_txdfo | Deferred Taxes - Foreign | MATRIX | 0.6464 | 43 | 173 |
| fnd6_txdi | Income Taxes - Deferred | MATRIX | 0.8012 | 67 | 209 |
| fnd6_txds | Deferred Taxes - State | MATRIX | 0.5937 | 54 | 197 |
| fnd6_txfed | Income Taxes - Federal | MATRIX | 0.6791 | 78 | 217 |
| fnd6_txfo | Income Taxes - Foreign | MATRIX | 0.6956 | 186 | 679 |
| fnd6_txndb | Net Deferred Tax Asset (Liab) - Total | MATRIX | 0.7344 | 58 | 192 |
| fnd6_txndba | Net Deferred Tax Asset | MATRIX | 0.6794 | 66 | 281 |
| fnd6_txndbl | Net Deferred Tax Liability | MATRIX | 0.679 | 86 | 134 |
| fnd6_txndbr | Deferred Tax Residual | MATRIX | 0.6965 | 40 | 119 |
| fnd6_txo | Income Taxes - Other | MATRIX | 0.8004 | 688 | 1038 |
| fnd6_txpd | Income Taxes Paid | MATRIX | 0.7889 | 116 | 542 |
| fnd6_txr | Income Tax Refund | MATRIX | 0.7987 | 98 | 219 |
| fnd6_txs | Income Taxes - State | MATRIX | 0.6724 | 78 | 164 |
| fnd6_txts | Income Taxes | VECTOR | 0.6032 | 13 | 15 |
| fnd6_txtubadjust | Other Unrecognized Tax Benefit Adjustment | MATRIX | 0.6537 | 58 | 211 |
| fnd6_txtubbegin | Unrecog. Tax Benefits - Beg of Year | MATRIX | 0.6604 | 127 | 184 |
| fnd6_txtubend | Unrecog. Tax Benefits - End of Year | MATRIX | 0.6682 | 134 | 421 |
| fnd6_txtubposdec | Decrease - Current Tax Positions | MATRIX | 0.668 | 115 | 455 |
| fnd6_txtubposinc | Increase - Current Tax Positions | MATRIX | 0.6533 | 82 | 224 |
| fnd6_txtubpospdec | Decrease - Prior Tax Positions | MATRIX | 0.6679 | 51 | 326 |
| fnd6_txtubpospinc | Increase - Prior Tax Positions | MATRIX | 0.6533 | 53 | 127 |
| fnd6_txtubsettle | Settlements with Tax Authorities | MATRIX | 0.6665 | 120 | 224 |
| fnd6_txtubsoflimit | Lapse of Statute of Limitations | MATRIX | 0.6665 | 60 | 361 |
| fnd6_txtubtxtr | Impact on Effective Tax Rate | MATRIX | 0.5706 | 53 | 253 |
| fnd6_txtubxintbs | Interest & Penalties Accrued - B/S | MATRIX | 0.5221 | 49 | 188 |
| fnd6_txtubxintis | Interest & Penalties Recognized - I/S | MATRIX | 0.3951 | 31 | 64 |
| fnd6_txw | Excise Taxes | MATRIX | 0.7538 | 116 | 399 |
| fnd6_txws | Excise Taxes | VECTOR | 0.9609 | 28 | 41 |
| fnd6_weburl | WEB URL code for the company | MATRIX | 0.995 | 299 | 965 |
| fnd6_xacc | Accrued Expenses | MATRIX | 0.6632 | 138 | 498 |
| fnd6_xaccq | Accrued Expenses | MATRIX | 0.5848 | 69 | 305 |
| fnd6_xad | Advertising Expense | MATRIX | 0.3399 | 147 | 367 |
| fnd6_xidos | Extraordinary Items and Discontinued Operations | VECTOR | 0.5466 | 6 | 10 |
| fnd6_xintopt | Implied Option Expense | MATRIX | 0.7117 | 12 | 19 |
| fnd6_xints | Interest Expense | VECTOR | 0.5741 | 8 | 8 |
| fnd6_xopr | Operating Expenses - Total | MATRIX | 0.941 | 213 | 614 |
| fnd6_xpp | Prepaid Expenses | MATRIX | 0.5065 | 82 | 479 |
| fnd6_xpr | Pension and Retirement Expense | MATRIX | 0.7419 | 99 | 285 |
| fnd6_xrent | Rental Expense | MATRIX | 0.7475 | 469 | 855 |
| fnd6_xsgas | Selling, General & Administrative | VECTOR | 0.5256 | 15 | 19 |
| fnd6_zipcode | ZIP code related to the company | MATRIX | 0.9926 | 326 | 1337 |
| goodwill | Goodwill (net) | MATRIX | 0.691 | 2412 | 9552 |
| income | Net Income | MATRIX | 0.9441 | 1591 | 8441 |
| income_beforeextra | Income Before Extraordinary Items | MATRIX | 0.9604 | 567 | 5548 |
| income_tax | Income Taxes - Total | MATRIX | 0.9575 | 815 | 6325 |
| interest_expense | Interest and Related Expense - Total | MATRIX | 0.7851 | 414 | 1986 |
| inventory | Inventories - Total | MATRIX | 0.9246 | 835 | 7545 |
| inventory_turnover | Inventory Turnover | MATRIX | 0.662 | 1011 | 5090 |
| invested_capital | Invested Capital - Total - Quarterly | MATRIX | 0.9191 | 1086 | 4490 |
| liabilities | Liabilities - Total | MATRIX | 0.9356 | 15053 | 27972 |
| liabilities_curr | Current Liabilities - Total | MATRIX | 0.7652 | 1350 | 5672 |
| operating_expense | Operating Expense - Total | MATRIX | 0.9899 | 1041 | 7671 |
| operating_income | Operating Income After Depreciation - Quarterly | MATRIX | 0.8906 | 7913 | 22875 |
| ppent | Property Plant and Equipment - Total (Net) | MATRIX | 0.9027 | 817 | 7698 |
| pretax_income | Pretax Income | MATRIX | 0.9576 | 717 | 5943 |
| rd_expense | Research And Development (Quarterly) | MATRIX | 0.5657 | 411 | 1975 |
| receivable | Receivables - Total | MATRIX | 0.9315 | 932 | 6780 |
| retained_earnings | Retained Earnings | MATRIX | 0.9213 | 2574 | 6704 |
| return_assets | Return on Assets | MATRIX | 0.9559 | 929 | 4982 |
| return_equity | Return on Equity | MATRIX | 0.951 | 939 | 6587 |
| revenue | Revenue - Total | MATRIX | 0.8942 | 1777 | 8073 |
| sales | Sales/Turnover (Net) | MATRIX | 0.9596 | 6830 | 25052 |
| sales_growth | Growth in Sales (Quarterly) | MATRIX | 0.906 | 1129 | 4949 |
| sales_ps | Sales per Share (Quarterly) | MATRIX | 0.9547 | 858 | 4843 |
| sga_expense | Selling, General and Administrative Expenses | MATRIX | 0.7618 | 1007 | 7157 |
| working_capital | Working Capital (Balance Sheet) | MATRIX | 0.7487 | 674 | 3689 |
