```dataview
TABLE without id 图片
FROM "要查询的文件的路径"
FLATTEN filter(file.outlinks, (x) => endswith(meta(x).path,"png") AS 图片
```