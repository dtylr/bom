---
layout: default
title: The List
---
<img src="img/dunlin1.jpeg" alt="Dunlin" width="800" height="376">

<div class="home">

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

<script>
var searchBox = document.getElementById("search");
var message = document.getElementById("message");
var list = document.getElementById("bird-list");
var items = list.getElementsByTagName("li");
var extras = list.getElementsByClassName("yellow").length;
var total = items.length;
var netTotal = items.length - extras;
var totalString = " " + total + " (" + netTotal + " + " + extras + ")"
var count = document.getElementById("count");
var categories = {{ site.data.categories | jsonify }}

function slugify(Text) {
    return Text
        .toLowerCase()
        .replace(/[^\w]+/g, " ")
        .replace(/\s+/g, "-");
}

function showAll() {
        for (var i = 0; i < items.length; i++) { 
        items[i].style.display = "";
        count.innerHTML = "Showing all " + totalString + " species."
    }
}

function show(term) {
        var shownItems = 0;
        var resultType = "match";
        if( term in categories ) {
            resultType = term;
            var categorySlugs = [];
            for (var i = 0; i < categories[term].length; i++ ) {
                categorySlugs.push(slugify(categories[term][i]));
            };
            for (var i = 0; i < items.length; i++) {
                if ( categorySlugs.indexOf(items[i].getAttribute("id")) !== -1 ) {
                    items[i].style.display = "";
                    shownItems++;
                } else {
                    items[i].style.display = "none";
                };    
            };
        } else {
        for (var i = 0; i < items.length; i++) {
            if ( items[i].getAttribute("id").indexOf(term) !== -1 ) {
                items[i].style.display = "";
                shownItems++;
            } else {
                items[i].style.display = "none";
            }
            if (shownItems > 1) resultType = "matches";
        }
    }
    if ( shownItems == 0 ) {
        count.innerHTML = "Nothing matches this search.";
    } else {
        count.innerHTML = "Showing " + shownItems + " " + resultType;
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
