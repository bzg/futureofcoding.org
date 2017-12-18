---
title: Log
---

<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
<link rel="shortcut icon" type="image/x-icon" href="../favicon.ico">
  
<style>
  .header {
    font-size: 35px;
    font-weight: bold;
    margin-bottom: 5px;
  }
  #title {
    font-size: 50px;
  }
  .date {
    font-size: 15px;
    color: #aaa;
    margin-bottom: 10px;
    font-style: italic;
  }
  .commit > .files {
    color: rgb(255,169,77);
    margin-bottom: 5px;
  }
  .hash {
    font-size: 15px;
  }
</style>

<h1 id="title">Log</h1>

This log represents my progress on the Future of Coding project. I intend to update this log every weekday, except when otherwise specified.

The data for this log are pulled from the commit message history for this repository, which can be found in [`/_data/git-log.json`](/_data/git-log.json).

<div id="commits-container">
{% for commit in site.data.git-log %} 
  {% if commit.message != 'updated git log' %}
    {% unless commit.message contains 'Merge branch' %}
      {% assign first_line = commit.message | newline_to_br | split: '<br />' | first %} 
      {% assign date = commit.committer.date | date_to_string %}
      {% assign message = commit.message | remove_first: first_line %}
      <div class="commit">
        <h2 class="header">
          {{ first_line | remove: "#" }}
          <a class="hash" href="https://github.com/stevekrouse/futureofcoding.org/commit/{{ commit.commit }}">{{ commit.commit | truncate: 7, ""}}</a>
        </h2>
        <div class="date">{{ date }}</div>
        {% if commit.changes != empty %}
          <div class="files">
            {% for change in commit.changes %}
              {% if change[2] != '_data/git-log.json' %}
               <div class="file">
                  edited: <a target="_blank" href="https://github.com/stevekrouse/futureofcoding.org/blob/{{commit.commit}}/{{change[2]}}">{{change[2]}}</a>
                </div>
              {% endif %}  
            {% endfor %}
          </div>
        {% endif %}
        {{ message | markdownify }}
      </div>
    {% endunless %} 
  {% endif %}
{% endfor %}
</div>

<script>
  (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
  (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
  m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
  })(window,document,'script','https://www.google-analytics.com/analytics.js','ga');
  ga('create', 'UA-103157758-1', 'auto');
  ga('send', 'pageview');
</script>
<script repoPath="stevekrouse/futureofcoding.org" type="text/javascript" src="/unbreakable-links/index.js"></script>
