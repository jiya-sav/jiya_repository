---
toc: true
layout: post
title: FRESH Meal Plan Planning
categories: [week 20]
---

<!-- below is the code for the html calorie dropdown -->
<html>
<head>
<meta name="viewport" content="width=device-width, initial-scale=1">
<style>
.dropbtn {
  background-color: #04AA6D;
  color: white;
  padding: 16px;
  font-size: 16px;
  border: none;
}

.dropdown {
  position: relative;
  display: inline-block;
}

.dropdown-content {
  display: none;
  position: absolute;
  background-color: #f1f1f1;
  min-width: 160px;
  box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
  z-index: 1;
}

.dropdown-content a {
  color: black;
  padding: 12px 16px;
  text-decoration: none;
  display: block;
}

.dropdown-content a:hover {background-color: #ddd;}

.dropdown:hover .dropdown-content {display: block;}

.dropdown:hover .dropbtn {background-color: #3e8e41;}
</style>
</head>
<body>

<h2>Daily Specifications</h2>
<p>Move the mouse over the button to open the dropdown menu.</p>

<div class="dropdown">
  <button class="dropbtn">Calorie Selection</button>
  <div class="dropdown-content">
    <a href="#">under 1000</a>
    <a href="#">1000-2000</a>
    <a href="#">2000-3000</a>
    <a href="#">over 3000</a>
  </div>

</body>
</html>

<!-- below is the code for selecting how many meals -->
<html>
<body>

<h1>The select multiple attribute</h1>

<p>You may select multiple meals</p>

<form action="/action_page.php">
  <label for="mealtype">Choose which meals you want to include in meal prep:</label>
  <br><br>
  <select name="mealtype" id="mealtype" multiple>
    <option value="breakfast">breakfast</option>
    <option value="lunch">lunch</option>
    <option value="dinner">dinner</option>
    <option value="dessert">dessert</option>
  </select>
  <br><br>
  <input type="submit" value="Submit">
</form>

<p>Hold down the Ctrl (windows) or Command (Mac) button to select multiple options.</p>

</body>
</html>

<!-- below is the code for snacks and servings input, and submit -->
<html>
<body>

<form action="/action_page.php">
  <label for="snacknum">How many snacks would you like to include?</label>
  <input type="text" id="snacknum" name="snacknum"><br><br>
  <label for="servings">How many people are included in your meal plan?</label>
  <input type="text" id="servings" name="servings"><br><br>
  <input type="submit" value="Submit">
</form>

<p>Click the "Submit" button once finished</p>

</body>
</html>

<!-- below is sample calander code -->

<html>
<head>
<style>
* {box-sizing: border-box;}
ul {list-style-type: none;}
body {font-family: Verdana, sans-serif;}

.month {
  padding: 70px 25px;
  width: 100%;
  background: #FFA63B;
  text-align: center;
}

.month ul {
  margin: 0;
  padding: 0;
}

.month ul li {
  color: white;
  font-size: 20px;
  text-transform: uppercase;
  letter-spacing: 3px;
}

.month .prev {
  float: left;
  padding-top: 10px;
}

.month .next {
  float: right;
  padding-top: 10px;
}

.weekdays {
  margin: 0;
  padding: 10px 0;
  background-color: #ddd;
}

.weekdays li {
  display: inline-block;
  width: 13.6%;
  color: #666;
  text-align: center;
}

.days {
  padding: 10px 0;
  background: #eee;
  margin: 0;
}

.days li {
  list-style-type: none;
  display: inline-block;
  width: 13.6%;
  text-align: center;
  margin-bottom: 5px;
  font-size:12px;
  color: #777;
}

.days li .active {
  padding: 5px;
  background: #FFA63B;
  color: white !important
}

/* Add media queries for smaller screens */
@media screen and (max-width:720px) {
  .weekdays li, .days li {width: 13.1%;}
}

@media screen and (max-width: 420px) {
  .weekdays li, .days li {width: 12.5%;}
  .days li .active {padding: 2px;}
}

@media screen and (max-width: 290px) {
  .weekdays li, .days li {width: 12.2%;}
}
</style>
</head>
<body>

<h1>Sample Calander</h1>
<div class="month">      
  <ul>
    <li class="prev">&#10094;</li>
    <li class="next">&#10095;</li>
    <li>
      January<br>
      <span style="font-size:18px">2023</span>
    </li>
  </ul>
</div>

<ul class="weekdays">
  <li>Mo</li>
  <li>Tu</li>
  <li>We</li>
  <li>Th</li>
  <li>Fr</li>
  <li>Sa</li>
  <li>Su</li>
</ul>

<ul class="days">  
  <li>1</li>
  <li>2</li>
  <li>3</li>
  <li>4</li>
  <li>5</li>
  <li>6</li>
  <li>7</li>
  <li>8</li>
  <li>9</li>
  <li><span class="active">26</span></li>
  <li>11</li>
  <li>12</li>
  <li>13</li>
  <li>14</li>
  <li>15</li>
  <li>16</li>
  <li>17</li>
  <li>18</li>
  <li>19</li>
  <li>20</li>
  <li>21</li>
  <li>22</li>
  <li>23</li>
  <li>24</li>
  <li>25</li>
  <li>26</li>
  <li>27</li>
  <li>28</li>
  <li>29</li>
  <li>30</li>
  <li>31</li>
</ul>

</body>
</html>