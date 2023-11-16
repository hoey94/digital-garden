```dataview
LIST L.text AS "语句"
FROM "Diary/2023"
FLATTEN file.lists AS L
WHERE icontains(L.text, "特定文字")
```