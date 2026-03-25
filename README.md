# 燕儿归 ✈ 机场 & 航司速查

一个轻量的机场三字码和航司二字码查询工具，支持多字段模糊搜索，Threecode / City / AirlineCode 严格匹配。

## 数据来源

### airport.json（机场数据）

1. 从 [OurAirports](https://ourairports.com/airports.csv) 下载全球机场 CSV 原始数据
2. 提取其中的机场 IATA 三字码
3. 使用三字码逐个请求携程接口，获取携程收录的准确机场信息（中文名、城市、省份、国家等）
4. 整理合并为最终的 `airport.json`

### airline.json（航司数据）

1. 从维基百科抓取全球航空公司二字码列表
2. 使用二字码逐个请求 IATA 官方接口，获取 IATA 官方认证的：
   - 航司二字码（AirlineCode）
   - 英文名称（AirlineEnglishName）
   - 所属国家（AirlineCountry）
3. 英文名称通过腾讯翻译 API 直译为中文名（AirlineName）
4. 中文名与维基百科已有的中文译名进行人工对照校验，确保准确性

## 搜索规则

| 字段 | 匹配方式 |
|------|----------|
| Threecode / City | 严格匹配 |
| AirlineCode | 严格匹配 |
| 其他字段 | 模糊匹配 |

### 排序优先级

搜索结果按相关度排序，优先级从高到低：

1. 代码严格匹配（如搜 `CA` → 中国国际航空排第一）
2. 名称完全匹配
3. 名称开头匹配
4. 名称包含匹配
5. 其他字段匹配

## 参与纠错

数据量较大，难免存在疏漏或错误，欢迎大家提 Issue 或 PR 进行人工纠错和补充。
