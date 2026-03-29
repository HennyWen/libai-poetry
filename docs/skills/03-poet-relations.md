# Skill: 诗人关系网络提取

## 目标
从李白诗歌中提取人物关系，构建诗人交游网络图。

## 工具和技术
- **实体识别**: 从诗歌标题和内容中提取人物
- **关系推断**: 基于诗歌类型（赠诗、送别）判断关系
- **D3.js**: 前端可视化

## 核心流程

### 1. 人物实体提取
从诗歌标题中提取人物：
- 赠XX、送XX、别XX
- 与XX同游、怀XX

### 2. 关系类型判断
```python
def infer_relationship(title, content):
    if '赠' in title or '送' in title:
        return '赠答往来'
    elif '怀' in title or '忆' in title:
        return '怀念'
    elif '同' in title:
        return '同游'
    return '交游'
```

### 3. 数据结构
```json
{
  "poet": "李白",
  "relations": [
    {
      "target": "杜甫",
      "type": "赠答往来",
      "poems": [
        {"id": "libai_0123", "title": "赠杜甫"}
      ],
      "poem_count": 5
    }
  ]
}
```

### 4. 前端可视化
使用 D3.js force-directed graph：
- 节点大小 = 往来诗作数量
- 连线粗细 = 关系强度
- 点击连线显示诗作列表

## 输出
- `libai_poet_relations.json`: 关系数据
- `app/graph/index.html`: 可视化页面
