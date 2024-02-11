---
title: "MultiModal"
layout: archive
permalink: categories/paper-review/multi-modal  # 상대 주소
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.OpenCV %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}