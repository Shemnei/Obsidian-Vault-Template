---
date: <%tp.date.now("YYYY-MM-DD")%>T<%tp.date.now("HH:mm")%>
tags:
  - daily
  <% "- " + tp.date.now("dddd").toLowerCase() %>
cssclasses:
  - daily
  <% "- " + tp.date.now("dddd").toLowerCase() %>
---

# <% tp.date.now("dddd, MMMM Do, YYYY") %>

---

## Tasks

## Notes

- <% tp.file.cursor() %>
