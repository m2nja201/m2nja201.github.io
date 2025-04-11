---
title: "Programming"
layout: archive
permalink: categories/programming  # 상대 주소
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.Ubuntu %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}

{% assign posts = site.categories.TroubleShooting %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}