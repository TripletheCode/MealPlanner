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

  <!-- Display meal plan with randomly generated meals -->
  <section id="mealPlan">
    <h2>Meal Plan for the Week</h2>
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

    // Function to generate a meal plan for the week
    function generateMealPlan() {
      // Get the days of the week
      const daysOfWeek = ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday"];

      // Loop through each day and add a randomly selected meal
      daysOfWeek.forEach(day => {
        const randomMeal = getRandomItem(predefinedMeals);
        const listItem = document.createElement("li");
        listItem.textContent = `${day}: ${randomMeal}`;
        document.getElementById("planList").appendChild(listItem);
      });
    }

    // Function to get a random item from an array
    function getRandomItem(array) {
      const randomIndex = Math.floor(Math.random() * array.length);
      return array[randomIndex];
    }

    // Generate meal plan when the page is loaded
    window.onload = function() {
      generateMealPlan();
    };
  </script>
</body>
</html>
