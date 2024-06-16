<%*
	const projectName = await tp.system.prompt("Project name?", null, true);
	const projectTag = "prj-" + projectName.toLowerCase().replace(" ", "_");

	await tp.file.move("/02-Projects/" + projectName + "/@" + projectName);

	tR += "---";
%>
date: <%tp.date.now("YYYY-MM-DD")%>T<%tp.date.now("HH:mm")%>
tags:
  - project
  - <% projectTag %>
cssclasses:
  - project
---

# <% projectName %>

---

```dataview
CALENDAR file.ctime
FROM #<% projectTag %>
```

## Files

```dataview
TABLE file.folder, task
FROM #<% projectTag %>
```

## Tasks

```dataview
TASK
FROM #<% projectTag %> 
GROUP BY file.link
```

## Notes

<% tp.file.cursor() %>