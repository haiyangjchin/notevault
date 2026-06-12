---
title: "知识库健康仪表盘"
type: wiki
tags: [dashboard, system]
created: 2026-06-12
updated: 2026-06-12
status: mature
---

# 📊 知识库健康仪表盘

> 本页面由 Dataview 插件自动生成，展示知识库的健康状态。

---

## 📈 统计概览

### 按类型统计

```dataview
TABLE length(rows) AS "数量"
FROM "01-Concepts" OR "02-Papers" OR "03-Projects" OR "04-Daily" OR "05-Wiki"
GROUP BY type
```

### 按状态统计

```dataview
TABLE length(rows) AS "数量"
FROM "01-Concepts" OR "02-Papers" OR "03-Projects" OR "05-Wiki"
GROUP BY status
```

---

## 🌱 种子笔记（待成长）

> 状态为 seed 的笔记，需要补充内容和链接。

```dataview
TABLE type AS "类型", created AS "创建日期", length(file.outlinks) AS "出链数"
FROM "01-Concepts" OR "02-Papers" OR "03-Projects" OR "05-Wiki"
WHERE status = "seed"
SORT created DESC
LIMIT 20
```

---

## 🔴 孤立笔记（无链接）

> 没有任何双向链接的笔记，需要建立关联。

```dataview
TABLE type AS "类型", file.mtime AS "最后修改"
FROM "01-Concepts" OR "02-Papers" OR "03-Projects" OR "05-Wiki"
WHERE length(file.inlinks) = 0 AND length(file.outlinks) = 0
SORT file.mtime ASC
LIMIT 20
```

---

## ⏰ 过期内容（>90天未更新）

> 超过 90 天未更新的笔记，考虑更新或归档。

```dataview
TABLE type AS "类型", updated AS "最后更新", status AS "状态"
FROM "01-Concepts" OR "02-Papers" OR "03-Projects" OR "05-Wiki"
WHERE updated AND date(today) - date(updated) > dur(90 days)
SORT updated ASC
LIMIT 20
```

---

## 🔥 高连接度笔记

> 被最多笔记链接的核心概念。

```dataview
TABLE length(file.inlinks) AS "入链数", length(file.outlinks) AS "出链数", type AS "类型"
FROM "01-Concepts" OR "02-Papers" OR "03-Projects" OR "05-Wiki"
SORT length(file.inlinks) DESC
LIMIT 10
```

---

## 📥 Inbox 待整理

> 00-Inbox 中尚未分类的笔记。

```dataview
TABLE file.mtime AS "收集时间"
FROM "00-Inbox"
SORT file.mtime DESC
```

---

*最后更新: 2026-06-12 | 由 LLM Wiki 系统生成*
