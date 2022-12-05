
```dataview
table without id
	file.link as Requirement,
	filter(file.outlinks, (t) => contains(t.file.tags, "testcase")) as Testcases,
	map(filter(file.outlinks, (t) => contains(t.file.tags, "testcase")).Status, (x) => choice(x = "PASS", "✅", "❌")) as Status,
	filter(file.outlinks, (t) => contains(t.file.tags, "covergroup") or contains(t.file.tags, "coverpoint")) as Covergroups,
	filter(file.outlinks, (t) => contains(t.file.tags, "covergroup") or contains(t.file.tags, "coverpoint")).coverage as Coverage
from #requirement and -"Templates"
```
