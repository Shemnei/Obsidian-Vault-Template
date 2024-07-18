```dataview
TASK
FROM #daily
WHERE status = " " or status = "/"
GROUP BY file.link
SORT rows.file.ctime DESC
```