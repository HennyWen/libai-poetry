# 李白全集知识库

从古籍 PDF 到结构化知识图谱的完整数据集，涵盖 820 首诗词、9,379 个实体标注、注释、地理与关系数据。

在线演示：**https://hennywen.github.io/libai-poetry/**

---

## 数据集（`data/`）

### 诗词主体 `data/poems/tang/libai/`

| 文件 | 条目 | 说明 |
|------|------|------|
| `libai_poems_index.json` | 822 首 | 轻量索引：`id / title / volume`，用于快速加载目录 |
| `libai_poems_structured.json` | 822 首 | 完整结构：正文、卷号、体裁、创作年份、地点、背景、来源 |
| `libai_poems_parsed.json` | — | OCR 原始解析结果，含分行文本 |

字段说明（`libai_poems_structured`）：

```
id / title / author / dynasty / volume / form
year / year_note / location / location_note
text / context / source
```

---

### 实体标注 `data/entities/`

| 文件 | 条目 | 说明 |
|------|------|------|
| `libai_entities_round1.json` | 820 首诗 · 9,379 个实体 | 11 类实体，逐诗标注 |

实体类型分布：

| 类型 | 数量 |
|------|------|
| 地名 | 2,435 |
| 意象 | 1,911 |
| 情感主题 | 1,574 |
| 自然物 | 1,062 |
| 人物 | 1,045 |
| 神话仙道 | 516 |
| 典故 | 351 |
| 时令 | 301 |
| 典籍 | 96 |
| 官职 | 83 |

---

### 注释 `data/annotations/`

| 文件 | 条目 | 说明 |
|------|------|------|
| `libai_wangqi_annotations.json` | — | 王琦注 OCR 原始提取 |
| `libai_wangqi_annotations_fixed.json` | — | 繁简转换 + 格式修正版本 |
| `libai_wangqi_annotations_linked.json` | 49 首 | 注释精确链接到诗句行号 |
| `libai_allusions.json` | 323 条 | 典故数据：出处、诗句、典故类型 |

---

### 关系与地理 `data/relations/`

| 文件 | 条目 | 说明 |
|------|------|------|
| `libai_poet_relations.json` | 8 对 | 诗人交游关系（含相关诗目），如李白-杜甫、李白-孟浩然 |
| `libai_places.json` | 1,234 条 | 地名出现记录，含古今坐标、关联诗目 |

---

### 知识单元 `data/knowledge_units/`

| 文件 | 条目 | 说明 |
|------|------|------|
| `libai_imagery_system.json` | 645 个意象 | 每个意象含：出现频次、情感主题、共现意象、例诗 |

---

### 诗人档案 `data/poets/`

| 文件 | 说明 |
|------|------|
| `libai.json` | 基本信息：字号、生卒年、籍贯、风格、代表作 |
| `libai_timeline.json` | 生平年表：重要事件与对应时间 |

---

## 技能文档（`docs/skills/`）

记录每个数据集的构建方法，可作为同类古籍数字化项目的复用配方。

| 文档 | 对应产出 | 核心技术 |
|------|---------|---------|
| [01-pdf-ocr-extraction.md](docs/skills/01-pdf-ocr-extraction.md) | `libai_poems_parsed.json` | PaddleOCR API，竖排古籍识别 |
| [02-annotation-extraction.md](docs/skills/02-annotation-extraction.md) | `libai_wangqi_annotations_linked.json` | Claude Sonnet 识别 + Haiku 批量链接行号 |
| [03-poet-relations.md](docs/skills/03-poet-relations.md) | `libai_poet_relations.json` | 从诗题提取人物关系，D3.js 网络图 |
| [04-entity-annotation.md](docs/skills/04-entity-annotation.md) | `libai_entities_round1.json` | Claude API 批量标注 11 类实体 |
| [05-travel-map.md](docs/skills/05-travel-map.md) | `libai_places.json` | 地名坐标标注，Leaflet.js 游历地图 |
| [08-taibai-poetry-generator.md](docs/skills/08-taibai-poetry-generator.md) | — | 基于 820 首语料生成李白风格诗歌 |

---

## 技术栈

- **OCR**：PaddleOCR API
- **AI 处理**：Claude API（Sonnet 4.6 + Haiku 4.5）
- **前端**：HTML / CSS / JavaScript，Leaflet.js，D3.js
- **部署**：GitHub Pages

## 项目结构

```
├── app/                    # 前端页面
├── data/
│   ├── annotations/        # 王琦注释 & 典故
│   ├── entities/           # 实体标注
│   ├── knowledge_units/    # 意象系统
│   ├── poems/tang/libai/   # 诗词主体
│   ├── poets/              # 诗人档案
│   ├── relations/          # 关系 & 地名
│   └── raw/                # OCR 原始文件（不入库）
└── docs/skills/            # 构建方法文档
```
