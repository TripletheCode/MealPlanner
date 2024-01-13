
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Meal Planner</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #222;
            color: #fff;
        }

        h1 {
            text-align: center;
            padding: 20px 0;
        }

        form {
            max-width: 600px;
            margin: 20px auto;
            padding: 20px;
            border: 1px solid #ccc;
            border-radius: 5px;
            background-color: #333;
        }

        label {
            display: block;
            margin-bottom: 10px;
        }

        input[type="checkbox"] {
            margin-right: 5px;
        }

        button {
            display: inline-block;
            width: 48%;
            padding: 10px;
            margin-top: 10px;
            background-color: #4caf50;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }

        #clearBtn {
            background-color: #f44336;
            margin-right: 2%;
        }

        #generateBtn {
            background-color: #4caf50;
        }

        #mealPlan {
            margin-top: 20px;
            background-color: #333;
            padding: 20px;
            border-radius: 5px;
        }
    </style>
</head>
<body>
    <h1>Weekly Meal Planner</h1>
    <form id="mealForm">
        <label for="vegetarian">Vegetarian</label>
        <input type="checkbox" id="vegetarian" name="vegetarian">

        <label for="glutenFree">Gluten-Free</label>
        <input type="checkbox" id="glutenFree" name="glutenFree">

        <label for="lowCarb">Low Carb</label>
        <input type="checkbox" id="lowCarb" name="lowCarb">

        <label for="nutFree">Nut-Free</label>
        <input type="checkbox" id="nutFree" name="nutFree">

        <button id="clearBtn" type="button" onclick="clearSelection()">Clear Selection</button>
        <button id="generateBtn" type="button" onclick="generateMealPlan()">Generate Meal Plan</button>
    </form>

    <div id="mealPlan"></div>

    <script>
        function clearSelection() {
            // Clear all checkbox selections
            document.querySelectorAll('input[type="checkbox"]').forEach(checkbox => {
                checkbox.checked = false;
            });

            // Clear the meal plan display
            document.getElementById('mealPlan').innerHTML = "";
        }

        function generateMealPlan() {
            // Add logic to generate and display the meal plan based on user preferences
            // This can be done using JavaScript and could involve calling an API for meal suggestions
            // For simplicity, let's assume a basic output for now
            const mealPlan = document.getElementById('mealPlan');
            mealPlan.innerHTML = "<h2>Your Meal Plan for the Week:</h2><p>Monday: Grilled Vegetables and Quinoa</p><p>Tuesday: Chicken Salad</p><p>Wednesday: Lentil Soup</p><p>Thursday: Spaghetti with Tomato Sauce</p><p>Friday: Baked Salmon with Steamed Broccoli</p><p>Saturday: Veggie Stir-Fry</p><p>Sunday: Quinoa Salad</p>";
        }
    </script>
</body>
</html>
