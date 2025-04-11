---
title: "Ubuntu"
layout: archive
permalink: categories/programming/ubuntu  # 상대 주소
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.Ubuntu %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}