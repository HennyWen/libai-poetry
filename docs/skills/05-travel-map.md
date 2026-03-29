# Skill: 地名提取与游历地图构建

## 目标
从李白诗歌中提取地名，标注地理坐标，构建游历地图和旅游路线。

## 工具和技术
- **实体识别**: 提取地名实体
- **地理编码**: 手动标注古今地名对应的经纬度
- **Leaflet.js**: 地图可视化
- **leaflet-polylinedecorator**: 路线箭头

## 核心流程

### 1. 地名提取
从诗歌标题和内容中提取地名实体：
```json
{
  "place": "金陵",
  "poem_count": 38,
  "poems": [
    {"id": "libai_0074", "title": "鼓吹入朝曲"}
  ],
  "location": {
    "lat": 32.06,
    "lon": 118.77,
    "note": "今南京"
  }
}
```

### 2. 地理坐标标注
手动标注古今地名对应：
- 金陵 → 南京 (32.06, 118.77)
- 长安 → 西安 (34.27, 108.93)
- 峨眉 → 峨眉山 (29.6, 103.48)

### 3. 旅游路线设计
根据历史记录设计 4 条路线：

**出蜀漫游** (725年):
峨眉 → 成都 → 三峡 → 白帝城 → 黄鹤楼 → 洞庭 → 金陵

**长安求仕** (742年):
梁园 → 洛阳 → 黄河 → 长安

**江南游历**:
扬州 → 金陵 → 宣城 → 庐山 → 东山 → 天台 → 剡溪

**晚年流放** (757年):
长安 → 黄鹤楼 → 洞庭 → 夜郎 → 白帝城 → 当涂

### 4. 地图可视化
```javascript
// 圆圈大小 = sqrt(poem_count) * 6000
const radius = Math.sqrt(place.poem_count) * 6000;
L.circle([lat, lon], {radius, color: '#c87941'}).addTo(map);

// 路线箭头
L.polylineDecorator(line, {
  patterns: [{
    offset: '10%', repeat: '20%',
    symbol: L.Symbol.arrowHead({pixelSize: 10})
  }]
}).addTo(map);
```

## 注意事项
- 合并重复地名（如"秦"和"长安"）
- 使用 CartoDB light_nolabels 底图
- 移动端优化：缩小面板，调整位置

## 输出
- `libai_places.json`: 地名数据
- `app/map/index.html`: 地图页面
