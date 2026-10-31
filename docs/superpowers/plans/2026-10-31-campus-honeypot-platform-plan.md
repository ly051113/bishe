# 校园蜜罐分析平台 Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** 在 `bishe` 仓库中实现一个可运行的 Flask + SQLite 校园低交互蜜罐攻击行为分析与可视化平台。

**Architecture:** Flask 单体应用提供页面与 REST 接口；SQLite 保存用户、节点、原始日志、攻击事件、规则、告警和审计记录；规则服务负责标准化、去重和时间窗口检测；前端使用 Jinja、原生 JavaScript、CSS 与 ECharts，提供蓝白科技风看板。

**Tech Stack:** Python 3, Flask, SQLite, pytest, Jinja2, vanilla JavaScript, CSS, ECharts CDN.

---

### Task 1: 创建应用骨架与依赖

**Files:**
- Create: `app.py`
- Create: `requirements.txt`
- Create: `config.py`
- Create: `templates/base.html`
- Create: `static/css/app.css`
- Create: `static/js/app.js`

- [ ] 创建 Flask app factory、配置类和本地启动入口，默认绑定 `127.0.0.1:5003`。
- [ ] 添加基础模板、导航布局、ECharts CDN 和蓝白科技风 CSS 变量。
- [ ] 添加依赖：Flask、Werkzeug、pytest。
- [ ] 运行 `python app.py`，确认首页返回 200。

### Task 2: 实现 SQLite 数据层与初始化数据

**Files:**
- Create: `db.py`
- Create: `schema.sql`
- Create: `seed_data.py`
- Create: `data/.gitkeep`

- [ ] 创建 `users`、`honeypots`、`raw_logs`、`attack_events`、`rules`、`alerts`、`audit_logs` 表。
- [ ] 提供连接管理、初始化、参数化查询和事务封装。
- [ ] 创建演示账号、4 条规则、SSH/HTTP 节点和 100 条脱敏样例日志。
- [ ] 运行初始化脚本，确认数据库表和样例数据存在。

### Task 3: 实现日志标准化与规则检测

**Files:**
- Create: `services/log_service.py`
- Create: `services/rule_engine.py`
- Create: `services/replay_service.py`
- Create: `tests/test_rules.py`

- [ ] 实现 JSON、JSONL、CSV 解析，限制文件大小、行数和字段长度。
- [ ] 标准化时间、IP、端口、协议、服务、动作和脱敏摘要；重复事件按 event_id 或内容哈希去重。
- [ ] 实现 SSH 暴力破解、端口扫描、Web 路径探测、敏感文件探测、高频访问和多类连续行为规则。
- [ ] 为每条规则编写正例、负例和阈值边界测试。
- [ ] 运行 `pytest tests/test_rules.py -q`，确认检测结果稳定。

### Task 4: 实现 Flask 页面与 API

**Files:**
- Modify: `app.py`
- Create: `services/query_service.py`
- Create: `services/report_service.py`
- Create: `templates/login.html`
- Create: `templates/dashboard.html`
- Create: `templates/events.html`
- Create: `templates/analysis.html`
- Create: `templates/alerts.html`
- Create: `templates/replay.html`
- Create: `templates/nodes.html`
- Create: `templates/rules.html`
- Create: `templates/reports.html`

- [ ] 实现登录、注销和会话保护。
- [ ] 实现总览统计、趋势、类型分布、风险分布、来源排行 API。
- [ ] 实现事件筛选、分页、详情和 IP 行为时间线 API。
- [ ] 实现告警确认、关闭、备注和审计记录。
- [ ] 实现日志导入、回放控制、节点状态和规则读取/更新。
- [ ] 实现 CSV 与打印版 HTML 报告导出。

### Task 5: 实现前端交互与可视化

**Files:**
- Modify: `static/css/app.css`
- Modify: `static/js/app.js`
- Create: `static/js/dashboard.js`
- Create: `static/js/events.js`
- Create: `static/js/replay.js`

- [ ] 实现蓝白科技风侧边栏、顶部状态栏、指标卡片、表格、抽屉和响应式布局。
- [ ] 用 ECharts 实现攻击趋势、类型分布、风险等级、来源排行和 IP 时间线。
- [ ] 实现筛选联动、分页、加载态、空态、错误态和告警状态按钮。
- [ ] 实现日志回放进度、暂停、重置和倍速。
- [ ] 在 1440×900 和窄屏尺寸下检查布局。

### Task 6: 集成验证与仓库提交

**Files:**
- Create: `README.md`
- Create: `.gitignore`
- Create: `tests/test_app.py`

- [ ] 编写首页、登录、导入、告警更新和报告导出的集成测试。
- [ ] 运行 `pytest -q` 和手动演示流程：登录 → 查看总览 → 导入日志 → 查看事件 → 确认告警 → 导出报告。
- [ ] 运行 `python app.py`，确认 `http://127.0.0.1:5003` 可访问。
- [ ] 提交代码并推送到 `git@github.com:ly051113/bishe.git` 对应的 `main` 分支。
