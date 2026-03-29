# 李白全集知识库 - Skills 总览

本目录包含构建李白全集知识库的核心技能文档。

## Skills 列表

1. **[PDF OCR 文本提取](01-pdf-ocr-extraction.md)**
   - 使用 PaddleOCR API 从古籍 PDF 中批量提取文本
   - 处理竖排文字识别
   - 输出: Markdown 格式的 OCR 文本

2. **[王琦注释识别与链接](02-annotation-extraction.md)**
   - 使用 Claude API 提取和结构化注释
   - 批量链接注释到诗句行号
   - 繁简转换
   - 输出: JSON 格式的注释数据

3. **[诗人关系网络提取](03-poet-relations.md)**
   - 从诗歌中提取人物关系
   - 构建交游网络
   - D3.js 可视化
   - 输出: 关系图数据和可视化页面

4. **[实体标注指南](04-entity-annotation.md)**
   - 11 类实体标注规范
   - 使用 Claude API 批量标注
   - 实体高亮显示
   - 输出: 结构化实体数据

5. **[地名提取与游历地图构建](05-travel-map.md)**
   - 提取地名并标注坐标
   - 设计历史旅游路线
   - Leaflet.js 地图可视化
   - 输出: 地图数据和交互式地图

6. **[太白诗曰 - 李白风格诗歌生成](08-taibai-poetry-generator.md)**
   - 基于 820 首诗歌语料
   - 学习李白的意象、典故、修辞
   - AI 生成李白风格诗歌
   - 输出: 创意诗歌作品

## 项目结构
```
唐诗宋词/
├── app/              # 前端页面
├── data/             # 数据文件
├── docs/skills/      # 技能文档（本目录）
└── scripts/          # 处理脚本（不提交到 Git）
```

## 技术栈
- **OCR**: PaddleOCR API
- **AI**: Claude API (Sonnet 4.6, Haiku 4.5)
- **前端**: HTML/CSS/JavaScript, Leaflet.js, D3.js
- **部署**: GitHub Pages
- **工具**: Python, OpenCC, Git
