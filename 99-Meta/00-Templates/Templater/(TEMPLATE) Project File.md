<%*
	const projectNames = app.vault.getAllLoadedFiles()
	  .filter(x => x instanceof tp.obsidian.TFolder)
	  .filter(x => {
		  const parts = x.path.split("/");
		  return parts.length === 2 && parts[0] === "02-Projects";
	  })
	  .map(x => x.name);
	const projectName = await tp.system.suggester(item => item, projectNames, true);
	const subProjectNames = app.vault.getAllLoadedFiles()
	  .filter(x => x instanceof tp.obsidian.TFolder)
	  .filter(x => {
		  const parts = x.path.split("/");
		  return parts.length === 3 && parts[0] === "02-Projects" && parts[1] === projectName;
	  })
	  .map(x => x.name);
	const subProjectName = await tp.system.suggester(item => item, subProjectNames, false);
	const fileName = await tp.system.prompt("File name?", null, true);
	const projectTag = "prj-" + projectName.toLowerCase().replace(" ", "_");
	const subProjectTag = subProjectName ? "sprj-" + subProjectName.toLowerCase().replace(" ", "_") : undefined;

	await tp.file.move("/02-Projects/" + projectName + "/" + (subProjectName ? subProjectName +  "/" : "") + tp.date.now("YYYY-MM-DD") + " " + fileName);
	
	tR += "---";
%>
date: <%tp.date.now("YYYY-MM-DD")%>T<%tp.date.now("HH:mm")%>
tags:
  - project-file
  - <% projectTag %><% subProjectTag ? "\n  - " + subProjectTag : "" %>
cssclasses:
  - project-file
---

# <% subProjectName ? subProjectName : projectName %> - <% fileName %>

---

<% tp.file.cursor() %>