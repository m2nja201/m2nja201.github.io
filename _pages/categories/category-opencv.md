---
title: "OpenCV"
layout: archive
permalink: categories/computer-vision/open-cv  # 상대 주소
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.categories %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}