---
cp_name: bw_speed_cp
coverage: 100
---

Belongs to a covergroup:
```dataview
list
from #covergroup 
where contains(cp_names, this.cp_name)
```

#coverpoint