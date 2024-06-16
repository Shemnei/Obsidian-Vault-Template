<%*
	const projectNames = app.vault.getAllLoadedFiles()
	  .filter(x => x instanceof tp.obsidian.TFolder)
	  .filter(x => {
		  const parts = x.path.split("/");
		  return parts.length === 2 && parts[0] === "02-Projects";
	  })
	  .map(x => x.name);
	const projectName = await tp.system.suggester(item => item, projectNames, true);
	const subProjectName = await tp.system.prompt("Subproject name?", null, true);
	const projectTag = "prj-" + projectName.toLowerCase().replace(" ", "_");
	const subProjectTag = "sprj-" + subProjectName.toLowerCase().replace(" ", "_");
	
	await tp.file.move("/02-Projects/" + projectName + "/" + subProjectName + "/@" + subProjectName);

	tR += "---";
%>
date: <%tp.date.now("YYYY-MM-DD")%>T<%tp.date.now("HH:mm")%>
tags:
  - subproject
  - <% projectTag %>
  - <% subProjectTag %>
cssclasses:
  - subproject
---

# <% projectName %> - <% subProjectName %>

---

## Files

```dataview
TABLE file.folder, task
FROM #<% projectTag %> and #<% subProjectTag %>
```

## Tasks

```dataview
TASK
FROM #<% projectTag %> and #<% subProjectTag %>
GROUP BY file.link
```

## Notes

<% tp.file.cursor() %>