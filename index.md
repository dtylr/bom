---
layout: default
title: The List
---
<img src="img/dunlin1.jpeg" alt="Dunlin" width="800" height="376">

<div class="home">

    <input id="search"  type="text" placeholder="Search the list" autocomplete="off" autofocus />

    <ul id="bird-list">
        {% for bird in site.data.list %}
            <li id="{{ bird.name | slugify }}" class="{{ bird.highlight }}">
                <h2>{{ bird.name }} </h2>
                <h3>({{ bird.latin }}) </h3>
                {{ bird.text | markdownify }}
            </li>
        {% endfor %}
    </ul>

    <div id="message">No species match this search!</div>

<script>
var searchBox = document.getElementById("search");
var message = document.getElementById("message");
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
        message.style.display = "none";
    }
}

function show(Text) {
        var emptyList = true;
        for (var i = 0; i < items.length; i++) {
            if ( items[i].getAttribute("id").indexOf(Text) !== -1 ) {
                items[i].style.display = "";
                emptyList = false;
            } else {
                items[i].style.display = "none";
            };
        if ( emptyList ) {
            message.style.display = "block";
        } else {
            message.style.display = "none";
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
