---
# category들의 archive page.
title: "Projects"
layout: archive
permalink: categories/projects # projects 카테고리의 상대주소.
author_profile: True
sidebar_main: true
---


{% assign posts = site.categories.projects %}
{% for post in posts %} {% include archive-single2.html type=page.entries_layout %} {% endfor %}
