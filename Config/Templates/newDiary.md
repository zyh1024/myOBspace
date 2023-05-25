---
CreatedOn: <% tp.file.creation_date() %>
tag: diary
---
```dataviewjs
// Get list of notes ordered alphanumerically.
const pages = dv.pages("#diary").sort((page) => page.file.path);
 
// Get index of current page in list of pages.
const currPageIndex = pages.findIndex(
  (page) => page.file.path === dv.current().file.path
);
 
// Create links to previous and next notes. If no previous/next note, use a fallback.
const getLinkSafe = (page, fallback) => page?.file?.link || fallback;
const prevLink = getLinkSafe(pages[currPageIndex - 1], "Earliest Entry");
const nextLink = getLinkSafe(pages[currPageIndex + 1], "Latest Entry");
 
dv.header(6, `<< ${prevLink} | ${nextLink} >>`);
```


# Old
```tasks
not done
limit 10
```
