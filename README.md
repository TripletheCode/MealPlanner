
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
    // Predefined list of meals with ingredients
    const predefinedMeals = {
      "Oatmeal": ["Oats", "Milk", "Fruits"],
      "Sandwich": ["Bread", "Cheese", "Tomato", "Lettuce", "Turkey"],
      "Grilled Chicken": ["Chicken Breast", "Olive Oil", "Herbs", "Vegetables"],
      "Pasta": ["Pasta", "Tomato Sauce", "Ground Beef", "Parmesan Cheese", "Roma Tomatoes"],
      "Salad": ["Lettuce", "Tomato", "Cucumber", "Dressing"],
      "Smoothie": ["Banana", "Yogurt", "Berries", "Honey"],
      "Stir Fry": ["Tofu", "Broccoli", "Soy Sauce", "Rice"],
      "Taco": ["Tortillas", "Ground Beef", "Lettuce", "Tomato", "Cheese", "Salsa"],
      "Pizza": ["Pizza Dough", "Tomato Sauce", "Cheese", "Pepperoni", "Mushrooms"],
      "Burger": ["Burger Patty", "Bun", "Lettuce", "Tomato", "Onion", "Ketchup"],
      "Sushi": ["Sushi Rice", "Nori", "Fish", "Avocado", "Soy Sauce", "Wasabi"],
      "Chicken Caesar Salad": ["Chicken Breast", "Romaine Lettuce", "Croutons", "Parmesan Cheese", "Caesar Dressing"],
      "Vegetarian Burrito": ["Tortilla", "Black Beans", "Rice", "Corn", "Guacamole"],
      "Fruit Salad": ["Mixed Fruits", "Honey", "Lime Juice"],
      "Chicken Alfredo": ["Fettuccine Pasta", "Chicken Breast", "Alfredo Sauce", "Broccoli"],
    };

    // Function to generate a non-repeating meal plan  and shopping list for the week
    function generateMealPlan() {
      // Get the days of the week
      const daysOfWeek = ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"];

      // Initialize shopping list array
      const shoppingList = {};

      // Copy the predefined meals to avoid modification
      const availableMeals = { ...predefinedMeals };

      // Loop through each day and add a randomly selected meal without repeats
      daysOfWeek.forEach(day => {
        const availableMealNames = Object.keys(availableMeals);
        
        if (availableMealNames.length === 0) {
          // If all meals have been used, break out of the loop
          return;
        }

        const randomMealName = getRandomItem(availableMealNames);
        const ingredients = availableMeals[randomMealName];

        // Add the meal to the calendar
        const cell = document.createElement("div");
        cell.textContent = `${day}: ${randomMealName}`;
        cell.style.backgroundColor = "#87ceeb"; // Light blue background for days
        cell.style.padding = "10px";
        cell.style.borderRadius = "5px";
        document.getElementById("calendar").appendChild(cell);

        // Update the shopping list with quantities (number of times ingredient appears)
        ingredients.forEach(ingredient => {
          shoppingList[ingredient] = (shoppingList[ingredient] || 0) + 1;
        });

        // Remove the used meal from the available meals
        delete availableMeals[randomMealName];
      });

      // Display the shopping list
      displayShoppingList("listItems", shoppingList);
    }

    // Function to add an item to the shopping list
    function addItemToList() {
      const itemName = document.getElementById("itemName").value;
      const itemQuantity = parseInt(document.getElementById("itemQuantity").value, 10);

      if (!isNaN(itemQuantity) && itemQuantity > 0) {
        const listItem = document.createElement("li");
        listItem.textContent = `${itemName} x${itemQuantity}`;
        listItem.classList.add("remove-button");
        listItem.onclick = function() {
          this.parentNode.removeChild(this);
        };
        document.getElementById("listItems").appendChild(listItem);
      }
    }

    // Function to display the shopping list
function displayShoppingList(listId, shoppingList) {
  const listContainer = document.getElementById(listId);
  listContainer.innerHTML = ""; // Clear previous list items

  for (const item in shoppingList) {
    const listItem = document.createElement("li");
    listItem.textContent = `${item} x${shoppingList[item]}`;
    listItem.classList.add("remove-button");
    listItem.onclick = function() {
      this.parentNode.removeChild(this);
    };
    listContainer.appendChild(listItem);
  }
  listContainer.style.textAlign = "left"; // Ensure the list is left-aligned
}

    // Function to print a list
    function printList(title, listId) {
      const listContainer = document.getElementById(listId);
      const items = Array.from(listContainer.children).map(item => item.textContent);
      const formattedList = items.join('\n');
      alert(`${title}:\n${formattedList}`);
    }

    // Function to change the background color
    function changeBackgroundColor() {
      const selectedColor = document.getElementById("colorPicker").value;
      document.body.style.backgroundColor = selectedColor;
      localStorage.setItem("backgroundColor", selectedColor);
    }

    // Function to get a random item from an array and remove it
    function getRandomItem(array) {
      const randomIndex = Math.floor(Math.random() * array.length);
      const randomItem = array[randomIndex];
      array.splice(randomIndex, 1); // Remove the selected item
      return randomItem;
    }

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
