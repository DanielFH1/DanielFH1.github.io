---
# category들의 archive page.
title: "After Reading"
layout: archive
permalink: categories/reading # Blog 카테고리의 상대주소. 블로그 주소에 이 부분 뒤에 적어주면 됨.
author_profile: True
sidebar_main: true
---


{% assign posts = site.categories.Reading %}
{% for post in posts %} {% include archive-single2.html type=page.entries_layout %} {% endfor %}
