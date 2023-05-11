<%*
let name=await tp.file.title;  
let imid=await tp.system.prompt("Please enter IMID of "+name);  
let alias=await tp.system.prompt("Please enter alias of "+name);  
let tag=["contact"];  
let out= 
`---
Name: ${name}
IMID: ${imid}
alias: ${imid}, ${alias}
tag: ${tag}
---
> [!info]  
> Name:\t${name}  
> IMID:\t[${imid}](im:${imid})  
`;
return out;
%>
