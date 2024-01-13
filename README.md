
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Meal Planner</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #333;
            color: #fff;
        }

        h1 {
            text-align: center;
            padding: 20px 0;
            color: #4caf50;
        }

        form {
            max-width: 600px;
            margin: 20px auto;
            padding: 20px;
            border: 1px solid #555;
            border-radius: 10px;
            background-color: #444;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
        }

        label {
            display: block;
            margin-bottom: 10px;
            color: #ccc;
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
            background-color: #444;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
        }

        #mealPlan h2 {
            color: #4caf50;
        }

        #mealPlan p {
            margin-bottom: 10px;
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
            // Get user preferences
            const vegetarian = document.getElementById('vegetarian').checked;
            const glutenFree = document.getElementById('glutenFree').checked;
            const lowCarb = document.getElementById('lowCarb').checked;
            const nutFree = document.getElementById('nutFree').checked;

            // Sample meal plan (replace with actual logic or API call)
            let mealPlanText = "<h2>Your Meal Plan for the Week:</h2>";

            if (vegetarian) {
                mealPlanText += "<p>Monday: Quinoa Salad</p>";
                mealPlanText += "<p>Tuesday: Lentil Soup</p>";
                mealPlanText += "<p>Wednesday: Veggie Stir-Fry</p>";
            } else {
                mealPlanText += "<p>Monday: Grilled Chicken with Roasted Vegetables</p>";
                mealPlanText += "<p>Tuesday: Spaghetti Bolognese</p>";
                mealPlanText += "<p>Wednesday: Grilled Salmon with Quinoa</p>";
            }

            if (glutenFree) {
                mealPlanText += "<p>Thursday: Gluten-Free Pizza</p>";
            } else {
                mealPlanText += "<p>Thursday: Spaghetti with Garlic Bread</p>";
            }

            if (lowCarb) {
                mealPlanText += "<p>Friday: Cauliflower Fried Rice</p>";
            } else {
                mealPlanText += "<p>Friday: Baked Potato with Sour Cream</p>";
            }

            if (nutFree) {
                mealPlanText += "<p>Saturday: Chicken Caesar Salad</p>";
            } else {
                mealPlanText += "<p>Saturday: Walnut Pesto Pasta</p>";
            }

            mealPlanText += "<p>Sunday: Grilled Veggie Wrap</p>";

            // Display the meal plan
            document.getElementById('mealPlan').innerHTML = mealPlanText;
        }
    </script>
</body>
</html>

</html>
