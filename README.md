<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Meal Planner with Background Color</title>
  <style>
    body {
      font-family: 'Arial', sans-serif;
      text-align: center;
      margin: 20px;
      background-color: #f0f0f0; /* Set a default background color */
      transition: background-color 0.5s;
    }
    h1 {
      color: #333;
    }
    #calendar {
      display: grid;
      grid-template-columns: repeat(7, 1fr);
      grid-gap: 10px;
      margin-bottom: 20px;
    }
    #colorPicker {
      margin-top: 20px;
    }
    ul {
      list-style-type: none;
      padding: 0;
    }
    li {
      margin: 8px 0;
    }
    button {
      padding: 10px;
      margin: 10px;
      font-size: 16px;
      cursor: pointer;
      background-color: #4CAF50;
      color: white;
      border: none;
      border-radius: 5px;
    }
  </style>
</head>
<body>

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

  <!-- Display meal plan and shopping list -->
  <section id="mealPlan">
    <h2>Meal Plan for the Week</h2>
    <ul id="planList"></ul>
  </section>

  <section id="shoppingList">
    <h2>Shopping List</h2>
    <ul id="listItems"></ul>
  </section>

  <!-- Print buttons for meal plan and shopping list -->
  <button onclick="printList('Meal Plan', 'planList')">Print Meal Plan</button>
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
      "Burrito": ["Tortilla", "Black Beans", "Rice", "Salsa", "Avocado"],
      "Pizza": ["Dough", "Tomato Sauce", "Cheese", "Pepperoni"],
      "Sushi": ["Rice", "Nori", "Fish", "Soy Sauce", "Wasabi", "Ginger"],
      "Chicken Caesar Wrap": ["Chicken Breast", "Lettuce", "Parmesan Cheese", "Caesar Dressing"],
      "Vegetable Curry": ["Curry Sauce", "Vegetables", "Rice"],
      "Fajitas": ["Chicken Strips", "Bell Peppers", "Onions", "Tortillas"],
      "Greek Salad": ["Cucumber", "Tomato", "Olives", "Feta Cheese"],
      "Quinoa Bowl": ["Quinoa", "Black Beans", "Corn", "Avocado"],
      "BBQ Ribs": ["Pork Ribs", "BBQ Sauce", "Coleslaw"],
      "Taco": ["Tortillas", "Ground Beef", "Lettuce", "Cheese", "Salsa", "Roma Tomatoes"],
      "Pesto Pasta": ["Pasta", "Pesto Sauce", "Cherry Tomatoes", "Parmesan Cheese"],
      "Chicken Alfredo": ["Fettuccine", "Chicken Breast", "Alfredo Sauce", "Broccoli"],
      "Caprese Salad": ["Tomato", "Mozzarella", "Basil", "Balsamic Glaze"],
      "Shrimp Stir Fry": ["Shrimp", "Vegetables", "Soy Sauce", "Rice"],
      "Nachos": ["Tortilla Chips", "Cheese", "Ground Beef", "Salsa", "Guacamole"],
      "Chicken Teriyaki": ["Chicken Thighs", "Teriyaki Sauce", "Broccoli", "Rice"],
      "Vegetarian Burrito": ["Tortilla", "Black Beans", "Rice", "Salsa", "Guacamole"],
      "Beef and Broccoli": ["Beef Strips", "Broccoli", "Soy Sauce", "Rice"],
      "Caesar Salad": ["Lettuce", "Croutons", "Parmesan Cheese", "Caesar Dressing"],
      "Mango Salsa Chicken": ["Chicken Breast", "Mango", "Red Onion", "Cilantro"]
    };

    // Function to generate a meal plan and shopping list for the week
    function generateMealPlan() {
      // Get the days of the week
      const daysOfWeek = ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday"];

      // Initialize meal plan and shopping list arrays
      const mealPlan = [];
      const shoppingList = {};

      // Loop through each day and add a randomly selected meal
      daysOfWeek.forEach(day => {
        const randomMeal = getRandomItem(Object.keys(predefinedMeals));
        const ingredients = predefinedMeals[randomMeal];

        // Add the meal to the meal plan
        mealPlan.push(`${day}: ${randomMeal}`);

        // Update the shopping list with quantities (number of times ingredient appears)
        ingredients.forEach(ingredient => {
          shoppingList[ingredient] = (shoppingList[ingredient] || 0) + 1;
        });
      });

      // Display the meal plan
      displayList("planList", mealPlan);

      // Display the shopping list
      displayShoppingList("listItems", shoppingList);

      // Display the calendar-style layout
      displayCalendar("calendar", daysOfWeek, mealPlan);
    }

    // Function to get a random item from an array
    function getRandomItem(array) {
      const randomIndex = Math.floor(Math.random() * array.length);
      return array[randomIndex];
    }

    // Function to display the calendar-style layout
    function displayCalendar(elementId, daysOfWeek, mealPlan) {
      const calendarElement = document.getElementById(elementId);
      calendarElement.innerHTML = "";

      // Create calendar cells for each day
      daysOfWeek.forEach(day => {
        const cell = document.createElement("div");
        cell.textContent = day;

        // Highlight the cell if the meal plan has a meal for that day
        if (mealPlan.some(item => item.includes(day))) {
          cell.style.backgroundColor = "#4CAF50"; // Green color for highlighting
          cell.style.color = "white";
        }

        calendarElement.appendChild(cell);
      });
    }

    // Function to display the shopping list with quantities
    function displayShoppingList(elementId, shoppingList) {
      const listElement = document.getElementById(elementId);
      listElement.innerHTML = "";

      Object.entries(shoppingList).forEach(([ingredient, quantity]) => {
        const listItem = document.createElement("li");
        listItem.textContent = `${ingredient} - Quantity: ${quantity}`;
        listElement.appendChild(listItem);
      });
    }

    // Function to display a list in the specified HTML element
    function displayList(elementId, items) {
      const listElement = document.getElementById(elementId);
      listElement.innerHTML = "";
      items.forEach(item => {
        const listItem = document.createElement("li");
        listItem.textContent = item;
        listElement.appendChild(listItem);
      });
    }

    // Function to change the background color
    function changeBackgroundColor() {
      const selectedColor = document.getElementById("colorPicker").value;
      document.body.style.backgroundColor = selectedColor;

      // Save the selected color to localStorage
      localStorage.setItem("backgroundColor", selectedColor);
    }

    // Function to print the specified list
    function printList(listName, elementId) {
      const listElement = document.getElementById(elementId);
      const listItems = listElement.getElementsByTagName("li");
      const printableList = Array.from(listItems).map(item => item.textContent).join('\n');

      // Create a new window for printing
      const printWindow = window.open('', '_blank');
      printWindow.document.write(`<pre>${listName}\n\n${printableList}</pre>`);
      printWindow.document.close();

      // Print the window
      printWindow.print();
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
