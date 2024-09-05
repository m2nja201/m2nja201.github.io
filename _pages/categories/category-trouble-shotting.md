---
title: "TroubleShooting"
layout: archive
permalink: categories/trouble-shooting  # 상대 주소
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.TroubleShooting %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}