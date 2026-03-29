# Skill: 王琦注释识别与链接

## 目标
从 OCR 提取的文本中识别王琦注释，并将注释链接到对应的诗句行号。

## 工具和技术
- **Claude API**: claude-sonnet-4-6 (识别注释), claude-haiku-4-5 (批量链接行号)
- **OpenCC**: 繁体转简体 (t2s)
- **批处理**: 避免 token 限制

## 核心流程

### 1. 提取注释
使用 Claude Sonnet 从 OCR 文本中提取注释：

**Prompt 模板**:
```
从以下王琦注释文本中提取所有注释条目。每条注释包含：
- target: 注释对象（诗句中的词语或典故）
- content: 注释内容
- line: 对应诗句行号（如果能识别）

OCR文本：
{ocr_text}

输出JSON格式。
```

### 2. 链接行号
使用 Claude Haiku 批量处理（BATCH_SIZE=5），将注释链接到诗句：

```python
BATCH_SIZE = 5
for i in range(0, len(annotations), BATCH_SIZE):
    batch = annotations[i:i+BATCH_SIZE]
    prompt = f"""
    诗歌全文：
    {poem_text}

    注释列表：
    {json.dumps(batch, ensure_ascii=False)}

    为每条注释添加 line 字段（行号，从1开始）。
    """
    # 调用 Claude Haiku API
```

### 3. 繁简转换
```bash
opencc -i input.json -o output.json -c t2s
```

### 4. 数据格式
```json
{
  "title": "梁甫吟",
  "annotations": [
    {
      "target": "长啸",
      "content": "《世说》：阮籍能为青白眼...",
      "line": 3
    }
  ]
}
```

## 注意事项
- Haiku 批处理避免超 token 限制
- 约 76.5% 注释能自动链接行号
- 剩余需 Sonnet 人工修复
- 过滤无效注释（"未找到"、"无匹配"）

## 输出文件
- `libai_wangqi_annotations.json`: 原始注释
- `libai_wangqi_annotations_fixed.json`: 带行号的注释
- `libai_allusions.json`: 典故格式（用于前端展示）
