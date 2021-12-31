---
title: MYSQL 删除重复数据并保留ID最小的一条
tags: []
id: '863'
categories:
  - - 个人原创
date: 2018-11-14 13:59:41
---

\[code\]DELETE FROM mtk WHERE \`code\` IN (SELECT \* FROM (SELECT \`code\` FROM mtk GROUP BY \`code\` HAVING COUNT(\`code\`) > 1) t1) AND id NOT IN (SELECT \* FROM (SELECT MIN(id) FROM mtk GROUP BY \`code\` HAVING COUNT(\`code\`) > 1) t2)\[/code\]