# AI Agent Smart Manufacturing System

本專案是一套以 **AI Agent** 為核心的智慧製造系統，目標是模擬工廠生產環境，整合生產資料、設備感測資料、品質紀錄與維護紀錄，並透過多個 Agent 提供生產監控、排程建議、預測維護與品質分析。

系統以電子組裝產線作為主要應用情境，可用於展示智慧工廠中資料整合、AI 分析、決策支援與人機互動介面的設計能力。

---

## 專案目標

本專案希望解決傳統製造現場中常見的問題：

- 生產資料分散於不同系統，難以整合分析
- 排程調整仰賴人工經驗，缺乏即時決策支援
- 設備異常與故障難以及早預測
- 品質缺陷需要人工彙整與分析，效率較低

因此，本系統設計一套 AI Agent 架構，讓系統能夠根據資料自動分析工廠狀態，並提供即時警示、排程建議、維護提醒與品質改善方向。

---

## 核心功能

### 1. 生產監控

透過設備狀態、感測器數據與生產紀錄，監控工廠目前的運作狀況，偵測異常設備或產線瓶頸。

### 2. 排程建議

根據訂單交期、數量、優先級、設備負載與製程時間，分析目前排程是否可能延遲，並提供調整建議。

### 3. 預測維護

分析設備的溫度、震動、功率、週期時間等 sensor data，判斷設備是否存在異常風險，並提前提出維護建議。

### 4. 品質分析

根據品質檢驗紀錄、缺陷類型與缺陷率，分析主要品質問題，協助找出高風險產品、機台或製程環節。

### 5. AI Chat Assistant

透過外層 Chatbot 作為使用者入口，讓使用者可以用自然語言查詢工廠狀態、任務分析結果、報表與通知。

---

## 系統架構

本系統分為四個主要層級：

```text
Factory Layer
├── Machines
├── Sensors
└── Production Orders

Data Layer
├── Sensor Data
├── Production Logs
├── Quality Data
└── Maintenance Records

AI Agent Layer
├── Monitoring Agent
├── Scheduling Agent
├── Maintenance Agent
└── Quality Agent

Application Layer
├── Dashboard
├── Chat Interface
└── Alert System
```

整體流程如下：

```text
Factory Machines
      ↓
Sensor Data Collection
      ↓
Database Storage
      ↓
AI Agent Analysis
      ↓
Decision / Prediction
      ↓
Dashboard & Alerts
```

---

## Agent 設計

### Monitoring Agent

負責監控設備與產線狀態。

主要任務：

- 讀取設備狀態與感測資料
- 偵測設備異常
- 找出生產瓶頸
- 產生即時警示

### Scheduling Agent

負責分析訂單與生產排程。

主要任務：

- 分析訂單交期與優先級
- 檢查設備負載
- 判斷是否有延遲風險
- 提供排程調整建議

### Maintenance Agent

負責設備健康狀態與預測維護分析。

主要任務：

- 分析 sensor data
- 偵測溫度、震動、功率等異常
- 預測設備故障風險
- 提出維護建議

### Quality Agent

負責品質資料與缺陷分析。

主要任務：

- 分析品質檢驗紀錄
- 統計缺陷率與缺陷類型
- 找出高風險機台或產品
- 提供品質改善方向

### Chat / Orchestration Layer

核心 Agent 由系統自行實作，外層可串接 Clawbot 或其他 LLM Chatbot，作為：

- Chat 入口
- 任務編排器
- 報表助手
- 通知助手

---

## 製造流程對應

| 製造情境 | 對應資料 | 對應 Agent | 輸出結果 |
|---|---|---|---|
| 生產規劃 | orders.csv | Scheduling Agent | 排程建議、延遲風險 |
| 設備監控 | sensor_data.csv、machines.csv | Monitoring Agent | 異常偵測、設備狀態 |
| 預測維護 | sensor_data.csv、maintenance_log.csv | Maintenance Agent | 故障風險、維護建議 |
| 品質管制 | quality_log.csv、production_log.csv | Quality Agent | 缺陷分析、品質改善建議 |

---

## 資料集設計

資料集目錄：

```text
smart_factory_dataset/
├── machines.csv
├── orders.csv
├── sensor_data.csv
├── production_log.csv
├── quality_log.csv
└── maintenance_log.csv
```

### machines.csv

| 欄位 | 說明 |
|---|---|
| machine_id | 機台編號 |
| machine_type | 機台類型 |
| status | 機台狀態 |
| max_capacity | 最大產能 |
| install_date | 安裝日期 |

### orders.csv

| 欄位 | 說明 |
|---|---|
| order_id | 訂單編號 |
| product | 產品名稱 |
| quantity | 訂單數量 |
| due_date | 交期 |
| priority | 優先級 |
| processing_time | 加工時間 |
| required_machine | 所需機台 |

### sensor_data.csv

| 欄位 | 說明 |
|---|---|
| timestamp | 資料時間 |
| machine_id | 機台編號 |
| temperature | 溫度 |
| vibration | 震動 |
| power | 功率 |
| cycle_time | 週期時間 |

### production_log.csv

| 欄位 | 說明 |
|---|---|
| order_id | 訂單編號 |
| machine_id | 機台編號 |
| start_time | 開始時間 |
| end_time | 結束時間 |
| produced_units | 產出數量 |
| status | 生產狀態 |

### quality_log.csv

| 欄位 | 說明 |
|---|---|
| order_id | 訂單編號 |
| machine_id | 機台編號 |
| defect_type | 缺陷類型 |
| defect_rate | 缺陷率 |
| inspection_result | 檢驗結果 |

### maintenance_log.csv

| 欄位 | 說明 |
|---|---|
| machine_id | 機台編號 |
| maintenance_type | 維護類型 |
| date | 維護日期 |
| downtime | 停機時間 |
| cost | 維護成本 |

---

## 技術架構

| 類別 | 技術 |
|---|---|
| Backend | Python、FastAPI |
| Database | PostgreSQL、InfluxDB |
| AI / ML | Machine Learning、LLM Agent |
| Frontend | React、Streamlit |
| API | RESTful API |
| Visualization | Dashboard、Charts、Alerts |

---

## API 設計範例

FastAPI 可提供各 Agent 的 API 入口：

```text
GET  /api/monitoring/status
POST /api/monitoring/analyze

GET  /api/scheduling/orders
POST /api/scheduling/recommend

POST /api/maintenance/predict
GET  /api/maintenance/risk-machines

POST /api/quality/analyze
GET  /api/quality/defect-summary

POST /api/chat/query
```

---

## 專案目錄範例

```text
ai-agent-smart-manufacturing-system/
├── app/
│   ├── main.py
│   ├── agents/
│   │   ├── monitoring_agent.py
│   │   ├── scheduling_agent.py
│   │   ├── maintenance_agent.py
│   │   └── quality_agent.py
│   ├── api/
│   │   ├── monitoring.py
│   │   ├── scheduling.py
│   │   ├── maintenance.py
│   │   └── quality.py
│   ├── services/
│   ├── models/
│   └── utils/
├── data/
│   └── smart_factory_dataset/
├── dashboard/
│   ├── streamlit_app.py
│   └── components/
├── tests/
├── requirements.txt
└── README.md
```

---

## 安裝方式

### 1. Clone 專案

```bash
git clone https://github.com/your-username/ai-agent-smart-manufacturing-system.git
cd ai-agent-smart-manufacturing-system
```

### 2. 建立虛擬環境

```bash
python -m venv venv
```

Windows：

```bash
venv\Scripts\activate
```

macOS / Linux：

```bash
source venv/bin/activate
```

### 3. 安裝套件

```bash
pip install -r requirements.txt
```

---

## 執行方式

### 啟動 FastAPI Backend

```bash
uvicorn app.main:app --reload
```

啟動後可進入：

```text
http://127.0.0.1:8000/docs
```

查看 API 文件。

### 啟動 Streamlit Dashboard

```bash
streamlit run dashboard/streamlit_app.py
```

---

## 預期成果

本專案完成後，預期可提供：

1. 智慧工廠模擬資料集
2. 多 Agent 分析架構
3. 工廠即時監控 Dashboard
4. AI Chat Factory Assistant
5. 生產排程、設備維護與品質分析建議

---

## 專案特色

- 以 AI Agent 作為智慧工廠決策核心
- 將製造現場資料轉換為可分析的決策資訊
- 結合排程、監控、維護與品質四大製造管理情境
- 可透過 Chatbot 進行自然語言查詢
- 架構可擴充至 Digital Twin、多 Agent 協作與即時 IoT 感測資料

---

## 未來延伸

- Digital Twin simulation
- Multi-agent factory system
- Reinforcement Learning Scheduling
- IoT real-time sensor integration
- 自動報表產生
- 即時異常通知
- 更完整的工廠 KPI 分析，例如 OEE、良率、稼動率與交期達成率

---

## 專案狀態

目前專案屬於智慧製造 AI Agent 系統設計與原型開發階段，主要目標為展示資料建模、Agent 分工、API 架構、Dashboard 與智慧決策支援流程。

