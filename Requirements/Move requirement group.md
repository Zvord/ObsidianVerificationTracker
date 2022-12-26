Subrequirement:: [[Jump]]
Subrequirement:: [[Walk]]

```dataviewjs
let page = dv.current();
let pages = new Set();

let stack = [page];
while (stack.length > 0) {
    let elem = stack.pop();
//    dv.el("b", elem);
	let subreqs = elem.Subrequirement;    
    for (let sr of dv.array(subreqs)) {
	    if (!sr)
		    continue;
        pages.add(dv.page(sr.path));
        stack.push(dv.page(sr.path));
    }
}
pages = dv.array(Array.from(pages));
let links = pages.map(p => p.file.link);
dv.list(links)
```

#requirement_group 