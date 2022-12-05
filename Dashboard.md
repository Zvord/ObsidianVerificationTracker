## Uncovered requirements
```dataview
list
from #requirement and -"Templates"
where (!contains(file.outlinks.file.tags, "testcase")) or
      (!contains(file.outlinks.file.tags, "covergroup") and !contains(file.outlinks.file.tags, "coverpoint"))
```


## Requirements with failing testcases
```dataview
list
from #requirement and -"Templates"
where contains(file.outlinks.file.frontmatter.Status, "FAIL")
```


## Failed testcases
```dataview
table Status as "Status", Error as "Error"
from #testcase and -"Templates"
where Status != "PASS"
```

## TODOs
```dataview
task 
from #testcase 
where !completed
group by file.link
```
