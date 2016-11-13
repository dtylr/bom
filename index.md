---
layout: default
title: Home
---
<section id="list">
<img src="img/dunlin1.jpeg" alt="Dunlin" width="800" height="376">

<input id="search"  type="text" placeholder="Search the list" autocomplete="off" autofocus />
<div id="count">Showing all species</div>
<ul id="bird-list">
    {% for bird in site.data.list %}
        <li id="{{ bird.name | slugify }}" class="{{ bird.highlight }}">
            <h2>{{ bird.name }} </h2>
            <h3>({{ bird.latin }}) </h3>
            {{ bird.text | markdownify }}
        </li>
    {% endfor %}
</ul>

</section>

<section id="about">
    {% capture about %}{% include about.md %}{% endcapture %}
    {{ about | markdownify }}
</section>

<section id="help" style="display:none">
    {% capture help %}{% include help.md %}{% endcapture %}
    {{ help | markdownify }}   
</section>

{% include script.html %}