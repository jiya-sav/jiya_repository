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
