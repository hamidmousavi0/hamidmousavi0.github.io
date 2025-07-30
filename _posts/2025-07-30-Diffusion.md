---
layout: post
title: Generative AI Seminar (Diffusion Models)
date: 2025-07-30 08:57:00-0400
description: Basics of diffusion model
tags: formatting jupyter
categories: sample-posts
giscus_comments: false
related_posts: false
---

{::nomarkdown}
{% assign jupyter_path = "assets/jupyter/Diffusion_slides.ipynb" | relative_url %}
{% capture notebook_exists %}{% file_exists assets/jupyter/blog.ipynb %}{% endcapture %}
{% if notebook_exists == "true" %}
{% jupyter_notebook jupyter_path %}
{% else %}

<p>Sorry, the notebook you are looking for does not exist.</p>
{% endif %}
{:/nomarkdown}

