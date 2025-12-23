---
title: Dofus Retro
subtitle: Liste de tous les articles publiés dans la catégorie "Dofus Retro".
layout: page
permalink: /news/dofus-retro
hidden: true
pagination: 
  enabled: true
---

{% for post in site.categories.dofus-retro %}
  <div class="col-xl-12 col-lg-12 col-md-12 col-sm-12">
    <div class="post-archive-item-container">
      <a class="post-archive-item-link" href="{{post.url}}">
        <div>
          <img class="post-archive-item-image" alt="Preview of post image" src="{{post.image}}" height="100%" width="100%">
          <span class="cattag-{{post.cattag}}" style="color:white;padding:2px;padding-left:5px;margin-right:5px;font-weight:bold;text-transform:uppercase;">
            {{post.cattagText}} 
          </span>
          <span style="font-style:italic;color:#333;"> {{post.date | date: "%-d %b, %Y"}}</span>
          <br>
          <h3>{{post.title}}</h3>
          <p style="color:#000;">{{post.metadescription}}</p>
        </div>
      </a>
    </div>
  </div>
{% endfor %}