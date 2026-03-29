# Skill: PDF OCR 文本提取

## 目标
从古籍 PDF（如《李白全集王琦注》）中批量提取文本内容，用于后续的注释识别和结构化处理。

## 工具和技术
- **PaddleOCR API**: https://paddleocr.aistudio-app.com/api/v2/ocr/jobs
- **PDF 转图片**: `pdf2image` 或 `pdftoppm`
- **批量处理**: Python 脚本

## 核心流程

### 1. PDF 转图片
```bash
pdftoppm -png input.pdf output_prefix
```

### 2. 批量 OCR 识别
使用 PaddleOCR API 批量提交图片：

```python
import requests
import json

API_URL = "https://paddleocr.aistudio-app.com/api/v2/ocr/jobs"
TOKEN = "your_token_here"

def submit_ocr(image_path):
    with open(image_path, 'rb') as f:
        files = {'file': f}
        headers = {'Authorization': f'Bearer {TOKEN}'}
        response = requests.post(API_URL, files=files, headers=headers)
        return response.json()
```

### 3. 结果保存
将 OCR 结果保存为 Markdown 文件，每页一个文件：
- `data/raw/page_001.md`
- `data/raw/page_002.md`
- ...

## 注意事项
- PaddleOCR API 有速率限制，需要控制并发
- 古籍竖排文字识别准确率约 85-90%
- 需要人工校对关键页面
- 保存原始 OCR 结果，便于后续重新处理

## 输出
- 原始 OCR 文本（Markdown 格式）
- 页面索引文件
