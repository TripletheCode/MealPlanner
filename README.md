<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Weekly Meal Planner</title>
  <style>
    body {
      font-family: 'Arial', sans-serif;
      text-align: center;
      margin: 20px;
      background-color: #f4f4f4; /* Light gray background */
      color: #000; /* Dark black text color */
    }
    h1 {
      color: #2e8b57; /* Sea Green header color */
    }
    #colorPicker {
      margin-top: 20px;
    }
    #calendar {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
      grid-gap: 10px;
      margin-top: 20px;
      margin-bottom: 20px;
    }
    ul {
      list-style-type: none;
      padding: 0;
      margin: 0;
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
    }
    li {
      margin: 10px;
      padding: 10px;
      background-color: #fff; /* White background for list items */
      border-radius: 5px;
      box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
      transition: background-color 0.3s;
      color: #000; /* Dark black text color */
      position: relative;
    }
    li:hover {
      background-color: #f0f0f0; /* Light gray background on hover */
    }
    .remove-button {
      position: absolute;
      top: 0;
      right: 0;
      margin: 5px;
      cursor: pointer;
      font-weight: bold;
      color: #ff0000; /* Red color for the remove button */
    }
    button {
      padding: 10px;
      margin: 10px;
      font-size: 16px;
      cursor: pointer;
      background-color: #2e8b57; /* Sea Green button color */
      color: white;
      border: none;
      border-radius: 5px;
      transition: background-color 0.3s;
    }
    button:hover {
      background-color: #228b22; /* Forest Green button color on hover */
    }
    form {
      margin-top: 20px;
      display: flex;
      flex-direction: column;
      align-items: center;
    }
    label {
      margin-bottom: 5px;
      color: #2e8b57; /* Sea Green label color */
    }
    input {
      margin-bottom: 10px;
      padding: 5px;
      border: 1px solid #ccc;
      border-radius: 3px;
    }

    @media screen and (max-width: 600px) {
      #calendar {
        grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
      }
    }
  </style>
</head>
<body>
  <h1>Weekly Meal Planner</h1>

  <!-- Color picker for background color selection -->
  <label for="colorPicker">Select background color:</label>
  <select id="colorPicker" onchange="changeBackgroundColor()">
    <option value="#a52a2a">Brown</option>
    <option value="#8b4513">Saddle Brown</option>
    <option value="#2f4f4f">Dark Slate Gray</option>
    <option value="#556b2f">Dark Olive Green</option>
    <option value="#483d8b">Dark Slate Blue</option>
    <option value="#006400">Dark Green</option>
    <option value="#8b0000">Dark Red</option>
    <option value="#8b008b">Dark Magenta</option>
    <option value="#87ceeb">Sky Blue</option>
    <option value="#f08080">Light Coral</option>
    <option value="#dda0dd">Plum</option>
    <option value="#7fffd4">Aquamarine</option>
  </select>
  <!-- Display calendar-style layout for the meal plan -->
  <div id="calendar"></div>

  <!-- Display shopping list -->
  <section id="shoppingList">
    <h2>Shopping List</h2>
    <ul id="listItems"></ul>
    <!-- Form to add and remove items from the shopping list -->
    <form id="listForm">
      <label for="itemName">Item Name:</label>
      <input type="text" id="itemName" required>
      <label for="itemQuantity">Quantity:</label>
      <input type="number" id="itemQuantity" required>
      <button type="button" onclick="addItemToList()">Add to List</button>
    </form>
  </section>

  <!-- Print button for shopping list -->
  <button onclick="printList('Shopping List', 'listItems')">Print Shopping List</button>

  <script>
    // ... (Previous JavaScript code)

    // Load the saved background color or set default when the page is loaded
    window.onload = function() {
      const savedColor = localStorage.getItem("backgroundColor");
      const defaultColor = document.getElementById("colorPicker").options[0].value;
      const backgroundColor = savedColor ? savedColor : defaultColor;

      document.body.style.backgroundColor = backgroundColor;
      document.getElementById("colorPicker").value = backgroundColor;

      // Delay the meal plan generation to allow smoother background color transition
      setTimeout(generateMealPlan, 100);
    };
  </script>
</body>
</html>