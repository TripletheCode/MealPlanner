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
      transition: background-color 0.5s;
    }
    h1 {
      color: #333;
    }
    section {
      margin-bottom: 20px;
    }
    #colorPicker {
      margin-top: 20px;
    }
  </style>
</head>
<body>
  <h1>Weekly Meal Planner</h1>

  <!-- Color picker for background color selection -->
  <label for="colorPicker">Select background color:</label>
  <select id="colorPicker" onchange="changeBackgroundColor()">
    <option value="lightcoral">Light Coral</option>
    <option value="lightsalmon">Light Salmon</option>
    <option value="darkorange">Dark Orange</option>
    <option value="lightgreen">Light Green</option>
    <option value="lightblue">Light Blue</option>
    <option value="lightpink">Light Pink</option>
    <option value="lightseagreen">Light Sea Green</option>
    <option value="plum">Plum</option>
    <option value="lightsteelblue">Light Steel Blue</option>
    <option value="palevioletred">Pale Violet Red</option>
    <option value="mediumorchid">Medium Orchid</option>
    <option value="thistle">Thistle</option>
    <option value="darkslategray">Dark Slate Gray</option>
    <option value="cadetblue">Cadet Blue</option>
    <option value="burlywood">Burly Wood</option>
    <option value="lightgoldenrodyellow">Light Goldenrod Yellow</option>
  </select>

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
      "Pasta": ["Pasta", "Tomato Sauce", "Ground Beef", "Parmesan Cheese"],
      "Salad": ["Lettuce", "Tomato", "Cucumber", "Dressing"],
      // Add more meals as needed
    };

    // Function to generate a meal plan and shopping list for the week
    function generateMealPlan() {
      // Get the days of the week
      const daysOfWeek = ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday"];

      // Initialize meal plan and shopping list arrays
      const mealPlan = [];
      const shoppingList = [];

      // Loop through each day and add a randomly selected meal
      daysOfWeek.forEach(day => {
        const randomMeal = getRandomItem(Object.keys(predefinedMeals));
        const ingredients = predefinedMeals[randomMeal];

        // Add the meal to the meal plan
        mealPlan.push(`${day}: ${randomMeal}`);

        // Add the ingredients to the cumulative shopping list (avoid duplicates)
        ingredients.forEach(ingredient => {
          if (!shoppingList.includes(ingredient)) {
            shoppingList.push(ingredient);
          }
        });
      });

      // Display the meal plan
      displayList("planList", mealPlan);

      // Display the shopping list
      displayList("listItems", shoppingList);
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

    // Function to get a random item from an array
    function getRandomItem(array) {
      const randomIndex = Math.floor(Math.random() * array.length);
      return array[randomIndex];
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

      generateMealPlan();
    };
  </script>
</body>
</html>
