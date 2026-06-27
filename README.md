# ACG 百家姓 — 二次元虚构角色姓氏统计

基于某 ACG 维基站约 17.7 万条虚构角色数据，通过 **JMnedict**（日本多语言命名实体词典）进行**汉字-读音双重校验**匹配，统计得出的 ACG 角色姓氏分布。

## 数据概况

| 指标 | 数值 |
|------|------|
| 原始角色条目 | 177,143 |
| 有纯假名或罗马字（可处理） | 51,142 |
| 双重匹配成功 | 34,500 |
| 去重姓氏数 | 8,141 |
| 姓氏读音总数 | 141,971 |
| 多读音姓氏 | 21,911 |

## 方法论

1. **读音提取**：从 infobox 的 `纯假名` 或 `罗马字` 字段中提取姓氏读音（空格分隔，取前段）
2. **递减前缀匹配**：从角色原名最长前缀开始，逐步缩短，首次在 JMnedict 中命中即为姓氏
3. **双重校验**：汉字前缀必须在 JMnedict 中同时满足 `keb`（汉字）和 `reb`（读音）双重匹配

## 数据格式

`acg_surnames.json` 包含以下结构：

```json
{
  "title": "ACG百家姓 — 二次元虚构角色姓氏统计",
  "license": "CC BY-NC-SA 4.0",
  "statistics": { ... },
  "surnames": [
    {
      "surname": "橘",
      "readings": ["たちばな"],
      "count": 241,
      "names": ["橘敬介", "橘圭一郎", ...]
    },
    ...
  ]
}
```

每个姓氏条目包含：
- `surname`：姓氏汉字
- `readings`：匹配到的读音列表（可能多个）
- `count`：匹配到的角色数量
- `names`：具体角色原名列表

## 前 20 名

| 排名 | 姓氏 | 人数 |
|:---:|------|:---:|
| 1 | 橘 | 241 |
| 2 | 柊 | 136 |
| 3 | 如月 | 116 |
| 4 | 早乙女 | 95 |
| 5 | 日向 | 93 |
| 6 | 田中 | 92 |
| 7 | 結城 | 91 |
| 8 | 佐藤 | 90 |
| 9 | 鈴木 | 89 |
| 10 | 一条 | 85 |

## 许可

本数据集采用 [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) 许可协议发布。

## 来源

- 角色数据：某 ACG 维基站全量角色 dump（约 17.7 万条）
- 姓氏数据库：[JMnedict](https://www.edrdg.org/enamdict/enamdict_doc.html) — Japanese-Multilingual Named Entity Dictionary
- 罗马字转换：[jaconv](https://github.com/ikegami-yukino/jaconv)
