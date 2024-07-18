<%*
	const personName = await tp.system.prompt("Person name?", null, true);
	const personNameFirst = personName.split(' ')[0];
	const personNameLast = personName.split(' ')[1];
	const personGroup = await tp.system.prompt("Person group?", null, true);

	await tp.file.move("/03-People/" + personName);

	tR += "---";
%>
date: <%tp.date.now("YYYY-MM-DD")%>T<%tp.date.now("HH:mm")%>
tags:
  - person
  - psn-<% personName.toLowerCase().replace(" ", "_") %>
  - grp-<% personGroup.toLowerCase().replace(" ", "_") %>
cssclasses:
  - person
person:
	firstName: <% personNameFirst %>
	lastName: <% personNameLast %>
	group: <% personGroup %>
---

## Notes

- <% tp.file.cursor() %>