---
Created: <% tp.file.creation_date() %>
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



# 开始  

```dataviewjs
const buttonMaker = () => {
    const btn = this.container.createEl('button', {"text": "ResetPriority"});
    btn.addEventListener('click', async (evt) => {
        evt.preventDefault();
        const pages = dv.pages("#diary").file.tasks
            .where(t=>t.outlinks.length>0 && t.completed == false)
            .map(t => dv.page(t.outlinks[0]));
        console.log(pages.length);
        for(const page of pages){
            console.log(page.file.path);
            const abfile = this.app.vault.getAbstractFileByPath(page.file.path);
            await app.fileManager.processFrontMatter(abfile, (frontmatter) => {
                frontmatter["Priority"] = 0;
                });
        }
    });
    btn.style["color"]="red";
    btn.style["font-weight"]="bolder";
    btn.style.float="right";
    return btn;
}

buttonMaker()
```
  
```dataviewjs
dv.table(["Task","Due","Priority","Reviewed","ReviewCount"],
    dv.pages("#diary").file.tasks
    .where(t=>t.outlinks.length>0 && t.completed == false && dv.page(t.outlinks[0]) != null)
    .sort(t=> [dv.page(t.outlinks[0]).Priority,dv.page(t.outlinks[0]).Reviewed])
    .map(t=>[t.text,t.due, dv.page(t.outlinks[0]).Priority,dv.page(t.outlinks[0]).Reviewed,dv.page(t.outlinks[0]).ReviewCount])
)
```
