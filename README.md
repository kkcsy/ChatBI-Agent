# ChatBI 交互式 BI 报表助手

这是一个基于大模型工具调用的交互式 BI 报表项目。用户可以用自然语言提问，系统根据股票历史行情数据生成 SQL 查询、返回表格结果，并按需要生成可视化图表或进行简单预测分析。

## 项目功能

- 自然语言查询：将用户问题转换为股票行情数据查询。
- SQL 执行：连接 MySQL 数据库，查询 `stock_price` 表。
- 自动可视化：根据查询结果生成折线图或柱状图。
- 技术指标分析：支持 BOLL 布林带等指标分析。
- 时间序列预测：支持 ARIMA、Prophet 等模型进行股价趋势预测。
- Web 交互界面：通过 `qwen_agent` 的 WebUI 运行聊天式 BI 助手。

## 目录结构

```text
.
├── 【完成参考】CASE-ChatBI助手/
│   ├── stock_query_assistant-5.py  # 主要版本，包含 SQL、图表、预测工具
│   ├── stock_query_assistant-*.py  # 不同阶段的实现版本
│   ├── stock_data.py              # 股票历史数据获取脚本
│   ├── stock_history_data.sql     # 股票数据 SQL
│   ├── stock_history_data.xlsx    # 股票历史数据
│   ├── requirements.txt           # 项目依赖
│   └── image_show/                # 运行后生成的图表
├── CASE-ChatBI助手/               # 初始版本或说明文件
└── 笔记20251015.txt               # 学习笔记
```

## 数据表

核心数据表为 `stock_price`，主要字段包括：

- `stock_name`：股票名称
- `ts_code`：股票代码
- `trade_date`：交易日期
- `open`：开盘价
- `high`：最高价
- `low`：最低价
- `close`：收盘价
- `vol`：成交量
- `amount`：成交额

## 安装依赖

进入完成参考目录：

```bash
cd "【完成参考】CASE-ChatBI助手"
pip install -r requirements.txt
```

如果运行预测功能，还需要安装：

```bash
pip install statsmodels prophet qwen-agent dashscope sqlalchemy mysql-connector-python matplotlib tabulate
```

## 运行方式

配置好 DashScope/Qwen API Key 和数据库连接后，运行主程序：

```bash
python stock_query_assistant-5.py
```

程序会启动 WebUI，用户可以直接在页面中输入问题，例如：

```text
查询贵州茅台最近 30 天收盘价走势
分析 600519.SH 的布林带信号
用 ARIMA 预测 600519.SH 未来 7 天收盘价
```

## 基本流程

1. 准备股票历史数据，并导入 MySQL。
2. 启动 ChatBI 助手。
3. 用户输入自然语言问题。
4. 大模型判断需要调用的工具。
5. 工具执行 SQL 查询、图表生成或预测分析。
6. 系统把表格、统计信息和图表返回给用户。

## 注意事项

- 数据库账号、API Key、Tushare Token 等敏感信息不要提交到公开仓库。
- `image_show/` 中的图片是运行过程中生成的结果，可以按需清理。
- 当前项目用于学习交互式 BI 和大模型工具调用流程，生产使用前需要补充权限控制、SQL 安全校验和异常处理。
