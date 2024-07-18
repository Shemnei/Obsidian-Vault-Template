<%*
	const meetinName = await tp.system.prompt("Meeting name?");
	
	await tp.file.move("/01-Daily/" + tp.date.now("YYYY") + "/" + tp.date.now("MM") + "/" + tp.date.now("DD") + "/" + tp.date.now("YYYY-MM-DD") + " (MEETING) " + meetingName )

	tR += "---";
%>
date: <%tp.date.now("YYYY-MM-DD")%>T<%tp.date.now("HH:mm")%>
tags:
  - meeting
cssclasses:
  - meeting
---

## Attendees

- <% tp.file.cursor() %>

## Tasks

## Minutes