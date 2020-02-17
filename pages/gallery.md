---
layout: page
title: TechTree
subtitle: From the pexels folder
permalink: /TechTree/
gallery_path: "assets/img/tech"
feature-img: "assets/img/pexels/disco-full.webp"
tags: [tech]
---

This is a photo gallery made from the static files in the `assets/img/pexels` folder. 
I wanted to create automatically a simple gallery from a folder without having to create a markdown page as you would for the portfolio.


{% include gallery.html gallery_path=page.gallery_path %}
