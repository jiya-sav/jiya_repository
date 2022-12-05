---
keywords: fastai
description: A discussion on Web APIs.  This is about creating a Web API (Jokes), and creating API that retains data as long as the Web Server is running.  This is done using List and Dictionaries as the backend.  Ultimately, this example could be extended by adding a database to the backend.  However, for now, we are focussing on interaction of Frontend to Backend, this is called an Endpoint.
title: Python Web API Endpoints using Jokes
toc: true
comments: true
permalink: /techtalk/webapi
image: /images/python_restapi.png
categories: [3.B, 5.A, 5.B]
type: pbl
week: 9
nb_path: _notebooks/2022-10-19-PBL-webapi_tutorial.ipynb
layout: notebook
---

<!--
#################################################
### THIS FILE WAS AUTOGENERATED! DO NOT EDIT! ###
#################################################
# file to edit: _notebooks/2022-10-19-PBL-webapi_tutorial.ipynb
-->

<div class="container" id="notebook-container">
        
<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Model-for-API">Model for API<a class="anchor-link" href="#Model-for-API"> </a></h3><blockquote><p>We will begin our journey into APIs by creating and thinking about data.  We have learned about Python Lists and dictionaries.  In this data example, we are going to make "the best computer jokes ever ;)" and serve them over the Internet.  The ultimate objective is to allow our viewers to provide a like or dislike on each of our jokes.</p>
</blockquote>
<ul>
<li><p>This code planning begins by coming up with some jokes and defining a data "model" to keep and manage the jokes.</p>
<ul>
<li>jokes_data   contains a list of dictionary records containing joke and reactions:haha or boohoo    - joke_list   contains collection of jokes we will put into jokes_data</li>
</ul>
</li>
<li><p>Next comes some functions to interact with our jokes</p>
<ul>
<li>def initJokes(): initializes jokes_data</li>
<li>def getJokes(): returns the complete list of jokes</li>
<li>def getJoke():  returns a single joke from our list</li>
<li>... many more function can be examined by reading comments below ...</li>
</ul>
</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>import random # the jokes data is on the back end (in the AWS server)</p>
<p>jokes_data = []
joke_list = [
    "If you give someone a program... you will frustrate them for a day; if you teach them how to program... you will "
    "frustrate them for a lifetime.",
    "Q: Why did I divide sin by tan? A: Just cos.",
    "UNIX is basically a simple operating system... but you have to be a genius to understand the simplicity.",
    "Enter any 11-digit prime number to continue.",
    "If at first you don't succeed; call it version 1.0.",
    "Java programmers are some of the most materialistic people I know, very object-oriented",
    "The oldest computer can be traced back to Adam and Eve. It was an apple but with extremely limited memory. Just "
    "1 byte. And then everything crashed.",
    "Q: Why did Wi-Fi and the computer get married? A: Because they had a connection",
    "Bill Gates teaches a kindergarten class to count to ten. 1, 2, 3, 3.1, 95, 98, ME, 2000, XP, Vista, 7, 8, 10.",
    "Q: What’s a aliens favorite computer key? A: the space bar!",
    "There are 10 types of people in the world: those who understand binary, and those who don’t.",
    "If it wasn't for C, we’d all be programming in BASI and OBOL.",
    "Computers make very fast, very accurate mistakes.",
    "Q: Why is it that programmers always confuse Halloween with Christmas? A: Because 31 OCT = 25 DEC.",
    "Q: How many programmers does it take to change a light bulb? A: None. It’s a hardware problem.",
    "The programmer got stuck in the shower because the instructions on the shampoo bottle said: Lather, Rinse, Repeat.",
    "Q: What is the biggest lie in the entire universe? A: I have read and agree to the Terms and Conditions.",
    'An SQL statement walks into a bar and sees two tables. It approaches, and asks may I join you?'
]</p>
<h1 id="Initialize-jokes">Initialize jokes<a class="anchor-link" href="#Initialize-jokes"> </a></h1><h1 id="setting-up-a-dictionary-to-store-all-the-jokes-data-and-how-many-likes/dislikes-each-joke-gets">setting up a dictionary to store all the jokes data and how many likes/dislikes each joke gets<a class="anchor-link" href="#setting-up-a-dictionary-to-store-all-the-jokes-data-and-how-many-likes/dislikes-each-joke-gets"> </a></h1><p>def initJokes():</p>

<pre><code># setup jokes into a dictionary with id, joke, haha, boohoo in a FOR LOOP
item_id = 0
for item in joke_list:
    jokes_data.append({"id": item_id, "joke": item, "haha": 0, "boohoo": 0})
    item_id += 1
# prime some haha responses
for i in range(200):
    id = getRandomJoke()['id']
    addJokeHaHa(id)
# prime some haha responses
for i in range(50):
    id = getRandomJoke()['id']
    addJokeBooHoo(id)

</code></pre>
<h1 id="jokes-are-being-built-into-a-list">jokes are being built into a list<a class="anchor-link" href="#jokes-are-being-built-into-a-list"> </a></h1><h1 id="Return-all-jokes-from-jokes_data">Return all jokes from jokes_data<a class="anchor-link" href="#Return-all-jokes-from-jokes_data"> </a></h1><p>def getJokes():
    return(jokes_data)</p>
<h1 id="Joke-getter">Joke getter<a class="anchor-link" href="#Joke-getter"> </a></h1><p>def getJoke(id):
    return(jokes_data[id])</p>
<h1 id="Return-random-joke-from-jokes_data">Return random joke from jokes_data<a class="anchor-link" href="#Return-random-joke-from-jokes_data"> </a></h1><p>def getRandomJoke():
    return(random.choice(jokes_data))</p>
<h1 id="Liked-joke">Liked joke<a class="anchor-link" href="#Liked-joke"> </a></h1><p>def favoriteJoke():
    best = 0
    bestID = -1
    for joke in getJokes():
        if joke['haha'] &gt; best:
            best = joke['haha']
            bestID = joke['id']
    return jokes_data[bestID]</p>
<h1 id="Jeered-joke">Jeered joke<a class="anchor-link" href="#Jeered-joke"> </a></h1><p>def jeeredJoke():
    worst = 0
    worstID = -1
    for joke in getJokes():
        if joke['boohoo'] &gt; worst:
            worst = joke['boohoo']
            worstID = joke['id']
    return jokes_data[worstID]</p>
<h1 id="Add-to-haha-for-requested-id">Add to haha for requested id<a class="anchor-link" href="#Add-to-haha-for-requested-id"> </a></h1><p>def addJokeHaHa(id):
    jokes_data[id]['haha'] = jokes_data[id]['haha'] + 1
    return jokes_data[id]['haha']</p>
<h1 id="Add-to-boohoo-for-requested-id">Add to boohoo for requested id<a class="anchor-link" href="#Add-to-boohoo-for-requested-id"> </a></h1><p>def addJokeBooHoo(id):
    jokes_data[id]['boohoo'] = jokes_data[id]['boohoo'] + 1
    return jokes_data[id]['boohoo']</p>
<h1 id="Pretty-Print-joke">Pretty Print joke<a class="anchor-link" href="#Pretty-Print-joke"> </a></h1><p>def printJoke(joke):
    print(joke['id'], joke['joke'], "\n", "haha:", joke['haha'], "\n", "boohoo:", joke['boohoo'], "\n")</p>
<h1 id="Number-of-jokes">Number of jokes<a class="anchor-link" href="#Number-of-jokes"> </a></h1><p>def countJokes():
    return len(jokes_data)</p>
<h1 id="Test-Joke-Model">Test Joke Model<a class="anchor-link" href="#Test-Joke-Model"> </a></h1><p>if <strong>name</strong> == "<strong>main</strong>": 
    initJokes()  # initialize jokes</p>

<pre><code># Most likes and most jeered
best = favoriteJoke()
print("Most liked", best['haha'])
printJoke(best)
worst = jeeredJoke()
print("Most jeered", worst['boohoo'])
printJoke(worst)

# Random joke
print("Random joke")
printJoke(getRandomJoke()) # have to get jokes out of the back end

# Count of Jokes
print("Jokes Count: " + str(countJokes())) # we have to store data -- use "str" to add to the counter</code></pre>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Backend-Interface-for-Web-API-(Control)">Backend Interface for Web API (Control)<a class="anchor-link" href="#Backend-Interface-for-Web-API-(Control)"> </a></h3><blockquote><p>An application programming interface (API) is the medium by which different systems of software interact. In our applications we have two big systems:1. Python Backend that stores data beyond a single Web page2. GH Pages/Fastpages Frontend that is responsible for presenting data</p>
</blockquote>
<p>To communicate data between Frontend and Backend, this section Backend code provides and interface to the Frontend using a Web Service Endpoint.  Examples of endpoints are listed below and can be typed within a browser, which will return JSON data:</p>
<ul>
<li><a href="https://flask.nighthawkcodingsociety.com/api/jokes">https://flask.nighthawkcodingsociety.com/api/jokes</a></li>
<li><a href="https://flask.nighthawkcodingsociety.com/api/jokes/2">https://flask.nighthawkcodingsociety.com/api/jokes/2</a></li>
<li><a href="https://flask.nighthawkcodingsociety.com/api/jokes/random">https://flask.nighthawkcodingsociety.com/api/jokes/random</a></li>
</ul>
<p>As you can see, these Endpoints return JSON.  They are NOT that readable by normal humans.  However, they are very effective in passing requested data across the Internet.  The Frontend code is responsible for formatting and presenting and interface that allows the typical computer user to interact with this data.</p>
<p>The next cell of code is Creating Endpoints that return JSON.  This allows developers in the Frontend to interact with Backend data.  API is a contract between the Frontend and Backend on how to share data.</p>
<p>FYI, <mark>there is NO output from this section </mark>.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="How-to-Make-an-API">How to Make an API<a class="anchor-link" href="#How-to-Make-an-API"> </a></h2>
</div>
</div>
</div>
    {% raw %}
    
<div class="cell border-box-sizing code_cell rendered">
<div class="input">

<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="kn">from</span> <span class="nn">flask</span> <span class="kn">import</span> <span class="n">Blueprint</span><span class="p">,</span> <span class="n">jsonify</span>  <span class="c1"># jsonify creates an endpoint response object</span>
<span class="kn">from</span> <span class="nn">flask_restful</span> <span class="kn">import</span> <span class="n">Api</span><span class="p">,</span> <span class="n">Resource</span> <span class="c1"># used for REST API building</span>
<span class="kn">import</span> <span class="nn">requests</span>  <span class="c1"># used for testing </span>
<span class="kn">import</span> <span class="nn">random</span>

<span class="c1"># Blueprints allow this code to be procedurally abstracted from main.py, meaning code is not all in one place</span>
<span class="n">app_api</span> <span class="o">=</span> <span class="n">Blueprint</span><span class="p">(</span><span class="s1">&#39;api&#39;</span><span class="p">,</span> <span class="vm">__name__</span><span class="p">,</span>
                   <span class="n">url_prefix</span><span class="o">=</span><span class="s1">&#39;/api/jokes&#39;</span><span class="p">)</span>  <span class="c1"># endpoint prefix avoid redundantly typing /api/jokes over and over</span>

<span class="c1"># API generator https://flask-restful.readthedocs.io/en/latest/api.html#id1 --&gt; this URL calls the API from the backend</span>
<span class="n">api</span> <span class="o">=</span> <span class="n">Api</span><span class="p">(</span><span class="n">app_api</span><span class="p">)</span>

<span class="k">class</span> <span class="nc">JokesAPI</span><span class="p">:</span>
    <span class="c1"># not implemented, this would be where we would allow creation of a new Joke</span>
    <span class="k">class</span> <span class="nc">_Create</span><span class="p">(</span><span class="n">Resource</span><span class="p">):</span>
        <span class="k">def</span> <span class="nf">post</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">joke</span><span class="p">):</span>
            <span class="k">pass</span>
            
    <span class="c1"># getJokes()</span>
    <span class="k">class</span> <span class="nc">_Read</span><span class="p">(</span><span class="n">Resource</span><span class="p">):</span>
        <span class="k">def</span> <span class="nf">get</span><span class="p">(</span><span class="bp">self</span><span class="p">):</span>
            <span class="k">return</span> <span class="n">jsonify</span><span class="p">(</span><span class="n">getJokes</span><span class="p">())</span>

    <span class="c1"># getJoke(id)</span>
    <span class="k">class</span> <span class="nc">_ReadID</span><span class="p">(</span><span class="n">Resource</span><span class="p">):</span>
        <span class="k">def</span> <span class="nf">get</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="nb">id</span><span class="p">):</span>
            <span class="k">return</span> <span class="n">jsonify</span><span class="p">(</span><span class="n">getJoke</span><span class="p">(</span><span class="nb">id</span><span class="p">))</span>

    <span class="c1"># getRandomJoke()</span>
    <span class="k">class</span> <span class="nc">_ReadRandom</span><span class="p">(</span><span class="n">Resource</span><span class="p">):</span>
        <span class="k">def</span> <span class="nf">get</span><span class="p">(</span><span class="bp">self</span><span class="p">):</span>
            <span class="k">return</span> <span class="n">jsonify</span><span class="p">(</span><span class="n">getRandomJoke</span><span class="p">())</span>
    
    <span class="c1"># getRandomJoke()</span>
    <span class="k">class</span> <span class="nc">_ReadCount</span><span class="p">(</span><span class="n">Resource</span><span class="p">):</span>
        <span class="k">def</span> <span class="nf">get</span><span class="p">(</span><span class="bp">self</span><span class="p">):</span>
            <span class="n">count</span> <span class="o">=</span> <span class="n">countJokes</span><span class="p">()</span>
            <span class="n">countMsg</span> <span class="o">=</span> <span class="p">{</span><span class="s1">&#39;count&#39;</span><span class="p">:</span> <span class="n">count</span><span class="p">}</span>
            <span class="k">return</span> <span class="n">jsonify</span><span class="p">(</span><span class="n">countMsg</span><span class="p">)</span>

    <span class="c1"># put method: addJokeHaHa</span>
    <span class="k">class</span> <span class="nc">_UpdateLike</span><span class="p">(</span><span class="n">Resource</span><span class="p">):</span>
        <span class="k">def</span> <span class="nf">put</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="nb">id</span><span class="p">):</span>
            <span class="n">addJokeHaHa</span><span class="p">(</span><span class="nb">id</span><span class="p">)</span>
            <span class="k">return</span> <span class="n">jsonify</span><span class="p">(</span><span class="n">getJoke</span><span class="p">(</span><span class="nb">id</span><span class="p">))</span>

    <span class="c1"># put method: addJokeBooHoo</span>
    <span class="k">class</span> <span class="nc">_UpdateJeer</span><span class="p">(</span><span class="n">Resource</span><span class="p">):</span>
        <span class="k">def</span> <span class="nf">put</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="nb">id</span><span class="p">):</span>
            <span class="n">addJokeBooHoo</span><span class="p">(</span><span class="nb">id</span><span class="p">)</span>
            <span class="k">return</span> <span class="n">jsonify</span><span class="p">(</span><span class="n">getJoke</span><span class="p">(</span><span class="nb">id</span><span class="p">))</span>

    <span class="c1"># building RESTapi interfaces, these routes are added to Web Server http://&lt;server&lt;/api/jokes</span>
    <span class="c1"># BASICALLY THE STEPS TO MAKE AN API</span>
    <span class="n">api</span><span class="o">.</span><span class="n">add_resource</span><span class="p">(</span><span class="n">_Create</span><span class="p">,</span> <span class="s1">&#39;/create/&lt;string:joke&gt;&#39;</span><span class="p">)</span>
    <span class="n">api</span><span class="o">.</span><span class="n">add_resource</span><span class="p">(</span><span class="n">_Read</span><span class="p">,</span> <span class="s1">&#39;/&#39;</span><span class="p">)</span>    <span class="c1"># default, which returns all jokes</span>
    <span class="n">api</span><span class="o">.</span><span class="n">add_resource</span><span class="p">(</span><span class="n">_ReadID</span><span class="p">,</span> <span class="s1">&#39;/&lt;int:id&gt;&#39;</span><span class="p">)</span>
    <span class="n">api</span><span class="o">.</span><span class="n">add_resource</span><span class="p">(</span><span class="n">_ReadRandom</span><span class="p">,</span> <span class="s1">&#39;/random&#39;</span><span class="p">)</span>
    <span class="n">api</span><span class="o">.</span><span class="n">add_resource</span><span class="p">(</span><span class="n">_ReadCount</span><span class="p">,</span> <span class="s1">&#39;/count&#39;</span><span class="p">)</span>
    <span class="n">api</span><span class="o">.</span><span class="n">add_resource</span><span class="p">(</span><span class="n">_UpdateLike</span><span class="p">,</span> <span class="s1">&#39;/like/&lt;int:id&gt;/&#39;</span><span class="p">)</span>
    <span class="n">api</span><span class="o">.</span><span class="n">add_resource</span><span class="p">(</span><span class="n">_UpdateJeer</span><span class="p">,</span> <span class="s1">&#39;/jeer/&lt;int:id&gt;/&#39;</span><span class="p">)</span>
    
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">

<div class="output_area">

<div class="output_subarea output_text output_error">
<pre>
<span class="ansi-red-fg">---------------------------------------------------------------------------</span>
<span class="ansi-red-fg">ModuleNotFoundError</span>                       Traceback (most recent call last)
<span class="ansi-green-intense-fg ansi-bold">/home/jiya_sav/vscode/jiya_repository/_notebooks/2022-10-19-PBL-webapi_tutorial.ipynb Cell 6</span> in <span class="ansi-cyan-fg">&lt;cell line: 3&gt;</span><span class="ansi-blue-fg">()</span>
<span class="ansi-green-intense-fg ansi-bold">      &lt;a href=&#39;vscode-notebook-cell://wsl%2Bubuntu/home/jiya_sav/vscode/jiya_repository/_notebooks/2022-10-19-PBL-webapi_tutorial.ipynb#W5sdnNjb2RlLXJlbW90ZQ%3D%3D?line=0&#39;&gt;1&lt;/a&gt;</span> # HOW TO MAKE AN API
<span class="ansi-green-fg">----&gt; &lt;a href=&#39;vscode-notebook-cell://wsl%2Bubuntu/home/jiya_sav/vscode/jiya_repository/_notebooks/2022-10-19-PBL-webapi_tutorial.ipynb#W5sdnNjb2RlLXJlbW90ZQ%3D%3D?line=2&#39;&gt;3&lt;/a&gt;</span> from flask import Blueprint, jsonify  # jsonify creates an endpoint response object
<span class="ansi-green-intense-fg ansi-bold">      &lt;a href=&#39;vscode-notebook-cell://wsl%2Bubuntu/home/jiya_sav/vscode/jiya_repository/_notebooks/2022-10-19-PBL-webapi_tutorial.ipynb#W5sdnNjb2RlLXJlbW90ZQ%3D%3D?line=3&#39;&gt;4&lt;/a&gt;</span> from flask_restful import Api, Resource # used for REST API building
<span class="ansi-green-intense-fg ansi-bold">      &lt;a href=&#39;vscode-notebook-cell://wsl%2Bubuntu/home/jiya_sav/vscode/jiya_repository/_notebooks/2022-10-19-PBL-webapi_tutorial.ipynb#W5sdnNjb2RlLXJlbW90ZQ%3D%3D?line=4&#39;&gt;5&lt;/a&gt;</span> import requests  # used for testing 

<span class="ansi-red-fg">ModuleNotFoundError</span>: No module named &#39;flask&#39;</pre>
</div>
</div>

</div>
</div>

</div>
    {% endraw %}

<div class="cell border-box-sizing text_cell rendered"><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Frontend-(View-Simulation)-and-Hacks">Frontend (View Simulation) and Hacks<a class="anchor-link" href="#Frontend-(View-Simulation)-and-Hacks"> </a></h3><blockquote><p>This python codes tests endpoints on a server.  This can be handy for development and testing when making modifications to the Jokes Web APIs. This code works off of the server <mark>endpoint/url</mark>, not from code cells above it in this notebook.</p>
</blockquote>
<p>To work with this code and make observation for learning...</p>
<ul>
<li>Run a local server from flask_portfolio project and the change server variable to be local</li>
<li>Observe the requests endpoints and the output, see if you can observe what is happening/changing on put requests</li>
<li>The "requests" are captured into a List, the List is used in the for loop to extract from RESTful API format.  </li>
<li>Try running this with Debugging and observe what data is being created at each step (Required)</li>
<li>Try to format this data in Python print statements to be more readable (Required)</li>
<li>Start and stop local server and observe errors</li>
</ul>

</div>
</div>
</div>
    {% raw %}
    
<div class="cell border-box-sizing code_cell rendered">
<div class="input">

<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># server = &quot;http://127.0.0.1:5000/&quot; # run local</span>
<span class="n">server</span> <span class="o">=</span> <span class="s1">&#39;https://flask.nighthawkcodingsociety.com/&#39;</span> <span class="c1"># run from web server</span>
<span class="n">url</span> <span class="o">=</span> <span class="n">server</span> <span class="o">+</span> <span class="s2">&quot;api/jokes/&quot;</span>
<span class="n">responses</span> <span class="o">=</span> <span class="p">[]</span>  <span class="c1"># responses list</span>

<span class="c1"># Get the count of jokes on server</span>
<span class="n">count_response</span> <span class="o">=</span> <span class="n">requests</span><span class="o">.</span><span class="n">get</span><span class="p">(</span><span class="n">url</span><span class="o">+</span><span class="s2">&quot;count&quot;</span><span class="p">)</span>
<span class="n">count_json</span> <span class="o">=</span> <span class="n">count_response</span><span class="o">.</span><span class="n">json</span><span class="p">()</span>
<span class="n">count</span> <span class="o">=</span> <span class="n">count_json</span><span class="p">[</span><span class="s1">&#39;count&#39;</span><span class="p">]</span>

<span class="c1"># Update likes/dislikes test sequence</span>
<span class="n">num</span> <span class="o">=</span> <span class="nb">str</span><span class="p">(</span><span class="n">random</span><span class="o">.</span><span class="n">randint</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span> <span class="n">count</span><span class="o">-</span><span class="mi">1</span><span class="p">))</span> <span class="c1"># test a random record</span>
<span class="n">responses</span><span class="o">.</span><span class="n">append</span><span class="p">(</span>
    <span class="n">requests</span><span class="o">.</span><span class="n">get</span><span class="p">(</span><span class="n">url</span><span class="o">+</span><span class="n">num</span><span class="p">)</span>  <span class="c1"># Get/read joke by id</span>
    <span class="p">)</span> 
<span class="n">responses</span><span class="o">.</span><span class="n">append</span><span class="p">(</span>
    <span class="n">requests</span><span class="o">.</span><span class="n">put</span><span class="p">(</span><span class="n">url</span><span class="o">+</span><span class="s2">&quot;like/&quot;</span><span class="o">+</span><span class="n">num</span><span class="p">)</span> <span class="c1"># Put/add to like count</span>
    <span class="p">)</span> 
<span class="n">responses</span><span class="o">.</span><span class="n">append</span><span class="p">(</span>
    <span class="n">requests</span><span class="o">.</span><span class="n">put</span><span class="p">(</span><span class="n">url</span><span class="o">+</span><span class="s2">&quot;jeer/&quot;</span><span class="o">+</span><span class="n">num</span><span class="p">)</span> <span class="c1"># Put/add to jeer count</span>
    <span class="p">)</span> 

<span class="c1"># Get a random joke</span>
<span class="n">responses</span><span class="o">.</span><span class="n">append</span><span class="p">(</span>
    <span class="n">requests</span><span class="o">.</span><span class="n">get</span><span class="p">(</span><span class="n">url</span><span class="o">+</span><span class="s2">&quot;random&quot;</span><span class="p">)</span>  <span class="c1"># Get/read a random joke</span>
    <span class="p">)</span> 

<span class="c1"># Cycle through and print responses</span>
<span class="k">for</span> <span class="n">response</span> <span class="ow">in</span> <span class="n">responses</span><span class="p">:</span>
    <span class="nb">print</span><span class="p">(</span><span class="n">response</span><span class="p">)</span>
    <span class="k">try</span><span class="p">:</span>
        <span class="nb">print</span><span class="p">(</span><span class="n">response</span><span class="o">.</span><span class="n">json</span><span class="p">())</span>
    <span class="k">except</span><span class="p">:</span>
        <span class="nb">print</span><span class="p">(</span><span class="s2">&quot;data error&quot;</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">

<div class="output_area">

<div class="output_subarea output_text output_error">
<pre>
<span class="ansi-red-fg">---------------------------------------------------------------------------</span>
<span class="ansi-red-fg">NameError</span>                                 Traceback (most recent call last)
<span class="ansi-green-intense-fg ansi-bold">/home/jiya_sav/vscode/jiya_repository/_notebooks/2022-10-19-PBL-webapi_tutorial.ipynb Cell 8</span> in <span class="ansi-cyan-fg">&lt;cell line: 8&gt;</span><span class="ansi-blue-fg">()</span>
<span class="ansi-green-intense-fg ansi-bold">      &lt;a href=&#39;vscode-notebook-cell://wsl%2Bubuntu/home/jiya_sav/vscode/jiya_repository/_notebooks/2022-10-19-PBL-webapi_tutorial.ipynb#X10sdnNjb2RlLXJlbW90ZQ%3D%3D?line=4&#39;&gt;5&lt;/a&gt;</span> responses = []  # responses list
<span class="ansi-green-intense-fg ansi-bold">      &lt;a href=&#39;vscode-notebook-cell://wsl%2Bubuntu/home/jiya_sav/vscode/jiya_repository/_notebooks/2022-10-19-PBL-webapi_tutorial.ipynb#X10sdnNjb2RlLXJlbW90ZQ%3D%3D?line=6&#39;&gt;7&lt;/a&gt;</span> # Get the count of jokes on server
<span class="ansi-green-fg">----&gt; &lt;a href=&#39;vscode-notebook-cell://wsl%2Bubuntu/home/jiya_sav/vscode/jiya_repository/_notebooks/2022-10-19-PBL-webapi_tutorial.ipynb#X10sdnNjb2RlLXJlbW90ZQ%3D%3D?line=7&#39;&gt;8&lt;/a&gt;</span> count_response = requests.get(url+&#34;count&#34;)
<span class="ansi-green-intense-fg ansi-bold">      &lt;a href=&#39;vscode-notebook-cell://wsl%2Bubuntu/home/jiya_sav/vscode/jiya_repository/_notebooks/2022-10-19-PBL-webapi_tutorial.ipynb#X10sdnNjb2RlLXJlbW90ZQ%3D%3D?line=8&#39;&gt;9&lt;/a&gt;</span> count_json = count_response.json()
<span class="ansi-green-intense-fg ansi-bold">     &lt;a href=&#39;vscode-notebook-cell://wsl%2Bubuntu/home/jiya_sav/vscode/jiya_repository/_notebooks/2022-10-19-PBL-webapi_tutorial.ipynb#X10sdnNjb2RlLXJlbW90ZQ%3D%3D?line=9&#39;&gt;10&lt;/a&gt;</span> count = count_json[&#39;count&#39;]

<span class="ansi-red-fg">NameError</span>: name &#39;requests&#39; is not defined</pre>
</div>
</div>

</div>
</div>

</div>
    {% endraw %}

</div>
 
