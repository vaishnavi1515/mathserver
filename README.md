# Ex.05 Design a Website for Server Side Processing
# Date:09/11/2024
# AIM:
To design a website to calculate the power of a lamp filament in an incandescent bulb in the server side.

# FORMULA:
P = I2R
P --> Power (in watts)
 I --> Intensity
 R --> Resistance

# DESIGN STEPS:
## Step 1:
Clone the repository from GitHub.

## Step 2:
Create Django Admin project.

## Step 3:
Create a New App under the Django Admin project.

## Step 4:
Create python programs for views and urls to perform server side processing.

## Step 5:
Create a HTML file to implement form based input and output.

## Step 6:
Publish the website in the given URL.

# PROGRAM :
~~~
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lamp Filament Power Calculator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f9;
            padding: 20px;
        }
        h1 {
            text-align: center;
            color: #333;
        }
        .container {
            max-width: 500px;
            margin: 0 auto;
            background-color: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
        }
        label {
            font-size: 16px;
            margin-bottom: 8px;
            display: block;
        }
        input[type="number"] {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            font-size: 16px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        button {
            width: 100%;
            padding: 10px;
            background-color: #4CAF50;
            color: white;
            font-size: 16px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        button:hover {
            background-color: #45a049;
        }
        .result {
            margin-top: 20px;
            font-size: 18px;
            font-weight: bold;
            color: #333;
        }
    </style>
</head>
<body>
    <h1>Lamp Filament Power Calculator</h1>
    <div class="container">
        <label for="intensity">Intensity (I) in Amps</label>
        <input type="number" id="intensity" placeholder="Enter Intensity (I)" step="any">
        
        <label for="resistance">Resistance (R) in Ohms</label>
        <input type="number" id="resistance" placeholder="Enter Resistance (R)" step="any">
        
        <label for="power">Power (P) in Watts</label>
        <input type="number" id="power" placeholder="Enter Power (P)" step="any">

        <button onclick="calculatePower()">Calculate</button>
        <div class="result" id="result"></div>
    </div>

    <script>
        function calculatePower() {
            let intensity = parseFloat(document.getElementById('intensity').value);
            let resistance = parseFloat(document.getElementById('resistance').value);
            let power = parseFloat(document.getElementById('power').value);
            let result = '';

            if (!isNaN(intensity) && !isNaN(resistance)) {
                // If intensity and resistance are given, calculate power
                power = Math.pow(intensity, 2) * resistance;
                result = Calculated Power (P) = ${power.toFixed(2)} Watts;
            } 
            else if (!isNaN(power) && !isNaN(resistance)) {
                // If power and resistance are given, calculate intensity
                intensity = Math.sqrt(power / resistance);
                result = Calculated Intensity (I) = ${intensity.toFixed(2)} Amps;
            } 
            else if (!isNaN(power) && !isNaN(intensity)) {
                // If power and intensity are given, calculate resistance
                resistance = power / Math.pow(intensity, 2);
                result = Calculated Resistance (R) = ${resistance.toFixed(2)} Ohms;
            } else {
                result = 'Please enter at least two values to calculate.';
            }

            document.getElementById('result').textContent = result;
        }
    </script>
</body>
</html>

from django.shortcuts import render

def calculate_power(request):
    result = None
    power = None
    intensity = None
    resistance = None

    if request.method == "POST":
        # Get the form data
        intensity = request.POST.get('intensity')
        resistance = request.POST.get('resistance')
        power = request.POST.get('power')

        # Perform calculation based on the inputs
        try:
            if intensity and resistance:  # If intensity and resistance are provided
                intensity = float(intensity)
                resistance = float(resistance)
                power = intensity ** 2 * resistance
                result = f"Calculated Power (P) = {power:.2f} Watts"
            elif power and resistance:  # If power and resistance are provided
                power = float(power)
                resistance = float(resistance)
                intensity = (power / resistance) ** 0.5
                result = f"Calculated Intensity (I) = {intensity:.2f} Amps"
            elif power and intensity:  # If power and intensity are provided
                power = float(power)
                intensity = float(intensity)
                resistance = power / (intensity ** 2)
                result = f"Calculated Resistance (R) = {resistance:.2f} Ohms"
            else:
                result = "Please enter at least two values to calculate."
        except ValueError:
            result = "Invalid input. Please enter numeric values."

    return render(request, 'webapp/math.html', {'result': result, 'power': power, 'intensity': intensity, 'resistance': resistance})

from django.urls import path
from webapp import views

urlpatterns = [
    path('', views.calculate_power, name='calculate_power'),
]
~~~
# SERVER SIDE PROCESSING:
 
![Screenshot (39) (1)](https://github.com/user-attachments/assets/1a7f9c69-1cf7-4ca7-89a2-3c70fef72882)

# RESULT:
The program for performing server side processing is completed successfully.
