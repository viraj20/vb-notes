# All Projects
```dataview
Table start_date, end_date, status, progress, type, dri
from "1. Projects"
where created_date 
```
# Project Tasks
```dataview
task 
from "1. Projects"
WHERE !completed
GROUP BY file.link
```