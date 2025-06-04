---
layout: post
title: a post with jupyter notebook
date: 2025-06-04 08:57:00-0400
description: The Reliability and Security of Deep Neural Networks
tags: formatting jupyter
categories: sample-posts
giscus_comments: true
related_posts: false
---

To include a jupyter notebook in a post, you can use the following code:

{% raw %}

```liquid
{::nomarkdown}
{% assign jupyter_path = 'assets/jupyter/Reliability_Security.ipynb' | relative_url %}
{% capture notebook_exists %}{% file_exists assets/jupyter/Reliability_Security.ipynb %}{% endcapture %}
{% if notebook_exists == 'true' %}
  {% jupyter_notebook jupyter_path %}
{% else %}
  <p>Sorry, the notebook you are looking for does not exist.</p>
{% endif %}
{:/nomarkdown}
```

{% endraw %}

