## Uncovered requirements
```dataview
list
from #requirement and -"Templates"
where (!contains(file.outlinks.file.tags, "testcase")) or
      (!contains(file.outlinks.file.tags, "covergroup") and !contains(file.outlinks.file.tags, "coverpoint"))
```

## Uncovered requirement groups
```dataviewjs
function is_uncovered(req_page) {
	return (!req_page.file.outlinks.file.tags.includes("#testcase")) ||
           (!req_page.file.outlinks.file.tags.includes("#covergroup") &&
            !req_page.file.outlinks.file.tags.includes("#coverpoint"));
};

let req_groups = dv.array(dv.pages("#requirement_group"));
let uncovered_reqs = new Set();
for (let top_req of req_groups) {
	let pages = new Set();
	let stack = [top_req];
	while (stack.length > 0) {
	    let elem = stack.pop();
		let subreqs = elem.Subrequirement;    
	    for (let sr of dv.array(subreqs)) {
		    if (!sr)
			    continue;
	        pages.add(sr.path);
	        stack.push(dv.page(sr.path));
	    }
	}
	pages = dv.array(Array.from(pages)).map(p => dv.page(p));
	if (pages.some(is_uncovered))
		uncovered_reqs.add(top_req);	
}
//dv.list(uncovered_reqs);
//pages = dv.array(Array.from(pages)).map(p => dv.page(p));
//pages = pages.filter(p => p.file.tags.includes("#requirement"));
let links = dv.array(Array.from(uncovered_reqs)).map(p => p.file.link);
dv.list(links)
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