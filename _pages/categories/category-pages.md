---
title: "Pages"
layout: archive
permalink: categories/pages  # 상대 주소
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.Pages %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}