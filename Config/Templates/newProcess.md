---
tags:
  - Process
Pid: <% tp.file.title %>
Priority: 0
ReviewCount: 0
Created: <% tp.file.creation_date() %>
Reviewed: <% tp.file.creation_date() %>
Finished: 
Due: 
Stakeholder:
---
  
```dataviewjs
const buttonMaker = () => {
    const btn = this.container.createEl('button', {"text": "Review"});
    btn.addEventListener('click', async (evt) => {
        evt.preventDefault();
        const ActiveFile = app.workspace.getActiveFile();
        await app.fileManager.processFrontMatter(ActiveFile, (frontmatter) => {
          frontmatter["ReviewCount"] = frontmatter["ReviewCount"] == null ? 1 : frontmatter["ReviewCount"] + 1;
          frontmatter["Priority"] = frontmatter["Priority"]  == null ? 1 :  frontmatter["Priority"] + 1;
          frontmatter["Reviewed"] = dv.func.dateformat(dv.date('now'),"yyyy-LL-dd HH:mm");
        });
    });
    //btn.style.float="right";
    return btn;
}

buttonMaker()
```



# Stakeholder  



# Main  
```tasks
description includes <% tp.file.title %>
```



# Log  



# Conclusion  


