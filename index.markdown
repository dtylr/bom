---
layout: default
---

<img src="img/dunlin1.jpg" alt="">

<div class="home">

  <h1 class="page-heading">Systematic List</h1>

  <input id="search">

  <ul id="bird-list">
    {% for bird in site.data.list %}
      <li id="{{ bird.name | slugify }}">
        <h2>{{ bird.name }}</h2>
        <h3>{{ bird.latin }} </h3>
        <p>{{ bird.text | markdownify }}</p>
      </li>
    {% endfor %}
  </ul>

  <p class="rss-subscribe">subscribe <a href="{{ "/feed.xml" | prepend: site.baseurl }}">via RSS</a></p>


  <script src = "http://code.jquery.com/jquery-3.1.1.min.js"></script>
  <script>
      function slugify(Text)  // http://stackoverflow.com/a/1054862
      {
          return Text
              .toLowerCase()
              .replace(/[^\w ]+/g,'')
              .replace(/ +/g,'-')
              ;
      }

      $("#search").keyup(function(){
        var term = slugify($(this).val());
          if (term) {
            $("li").hide();
            $("li[id*='"+ term +"']").show();
          } else {
            $("li").show();
          }
      });
    // $(function(
      // var birdList = $("#bird-list")
      //        .find("li") //Find the bird names
      //        .map(function() { return this.id; }) //Project Ids
      //        .get(); //ToArray
      // $(document.body).append(birdList);

      
      // ))





  </script>

</div>
