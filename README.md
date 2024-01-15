<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Meal Planner</title>
  <style>
    body {
      font-family: 'Arial', sans-serif;
      text-align: center;
      margin: 20px;
    }
    h1 {
      color: #333;
    }
    section {
      margin-bottom: 20px;
    }
  </style>
</head>
<body>
  <h1>Weekly Meal Planner</h1>

  <!-- Form to input meal details -->
  <form id="mealForm">
    <label for="day">Select a day:</label>
    <select id="day" name="day">
      <option value="Monday">Monday</option>
      <option value="Tuesday">Tuesday</option>
      <option value="Wednesday">Wednesday</option>
      <option value="Thursday">Thursday</option>
      <option value="Friday">Friday</option>
      <option value="Saturday">Saturday</option>
      <option value="Sunday">Sunday</option>
    </select>
    <br>

    <label for="mealType">Select a meal type:</label>
    <select id="mealType" name="mealType">
      <option value="Breakfast">Breakfast</option>
      <option value="Lunch">Lunch</option>
      <option value="Dinner">Dinner</option>
    </select>
    <br>

    <label for="meal">Enter meal details:</label>
    <input type="text" id="meal" name="meal" required>
    <br>

    <button type="button" onclick="addMeal()">Add Meal</button>
  </form>

  <!-- Display meal plan with stored and user input meals -->
  <section id="mealPlan">
    <h2>Meal Plan</h2>
    <ul id="planList"></ul>
  </section>

  <script>
    // Predefined list of meals
    const predefinedMeals = [
      "Oatmeal",
      "Sandwich",
      "Grilled Chicken",
      "Pasta",
      "Salad",
      // Add more meals as needed
    ];

    // Function to add a meal to the list
    function addMeal() {
      // Get user input values
      const day = document.getElementById("day").value;
      const mealType = document.getElementById("mealType").value;
      const meal = document.getElementById("meal").value;

      // Create a new list item
      const listItem = document.createElement("li");
      listItem.textContent = `${day} - ${mealType}: ${meal}`;

      // Append the new item to the list
      document.getElementById("planList").appendChild(listItem);

      // Clear the form fields
      document.getElementById("mealForm").reset();

      // Save the meal to localStorage
      saveMeal(day, mealType, meal);
    }

    // Function to save a meal to localStorage
    function saveMeal(day, mealType, meal) {
      // Check if localStorage is supported
      if (typeof(Storage) !== "undefined") {
        // Retrieve existing meals or initialize an empty array
        const savedMeals = JSON.parse(localStorage.getItem("meals")) || [];

        // Add the new meal to the array
        savedMeals.push(`${day} - ${mealType}: ${meal}`);

        // Save the updated array to localStorage
        localStorage.setItem("meals", JSON.stringify(savedMeals));
      } else {
        // Fallback for browsers that do not support localStorage
        console.error("LocalStorage is not supported in this browser.");
      }
    }

    // Function to load stored meals from localStorage
    function loadMeals() {
      // Check if localStorage is supported
      if (typeof(Storage) !== "undefined") {
        // Retrieve stored meals
        const savedMeals = JSON.parse(localStorage.getItem("meals")) || [];

        // Display stored meals on the webpage
        const planList = document.getElementById("planList");
        savedMeals.forEach(meal => {
          const listItem = document.createElement("li");
          listItem.textContent = meal;
          planList.appendChild(listItem);
        });
      } else {
        // Fallback for browsers that do not support localStorage
        console.error("LocalStorage is not supported in this browser.");
      }
    }

    // Function to add a randomly generated meal to the list
    function addRandomMeal() {
      // Get a random meal from the predefined list
      const randomMeal = getRandomItem(predefinedMeals);

      // Get a random day from the days of the week
      const daysOfWeek = ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday"];
      const randomDay = getRandomItem(daysOfWeek);

      // Get a random meal type
      const mealTypes = ["Breakfast", "Lunch", "Dinner"];
      const randomMealType = getRandomItem(mealTypes);

      // Create a new list item
      const listItem = document.createElement("li");
      listItem.textContent = `${randomDay} - ${randomMealType}: ${randomMeal}`;

      // Append the new item to the list
      document.getElementById("planList").appendChild(listItem);
    }

    // Function to get a random item from an array
    function getRandomItem(array) {
      const randomIndex = Math.floor(Math.random() * array.length);
      return array[randomIndex];
    }

    // Load stored meals when the page is loaded
    window.onload = function() {
      loadMeals();
      // Uncomment the line below to add a random meal on page load
      // addRandomMeal();
    };
  </script>
</body>
</html>
