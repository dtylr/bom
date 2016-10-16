---
layout: default
title: The List
---
<img src="img/dunlin1.jpg" alt="">

<div class="home">

    <input id="search"  type="text" placeholder="Search the list" autocomplete="off" autofocus>

    <ul id="bird-list">
        {% for bird in site.data.list %}
            <li id="{{ bird.name | slugify }}">
                <h2>{{ bird.name }} </h2>
                <h3>({{ bird.latin }}) </h3>
                <p>{{ bird.text | markdownify }}</p>
            </li>
        {% endfor %}
    </ul>

<script>
var searchBox = document.getElementById("search");
var list = document.getElementById("bird-list");
var items = list.getElementsByTagName("li");

function slugify(Text) {
    return Text
        .toLowerCase()
        .replace(/[^\w]+/g, " ")
        .replace(/\s+/g, "-");
}

function showAll() {
        for (var i = 0; i < items.length; i++) { 
        items[i].style.display = "";
    }
}

function show(Text) {
        for (var i = 0; i < items.length; i++) {
            if ( items[i].getAttribute("id").indexOf(Text) !== -1 ) {
                items[i].style.display = "";
            } else {
                items[i].style.display = "none";
            }
    }
}
searchBox.onkeyup = function(evt) {
    var term = slugify(searchBox.value);
        if (term) {
            show(term);
        } else {
            showAll();
        }
};
</script>

</div>
