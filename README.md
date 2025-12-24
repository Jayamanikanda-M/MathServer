# Ex.05 Design a Website for Server Side Processing
## Date:24-12-2015

## AIM:
 To design a website to calculate the power of a lamp filament in an incandescent bulb in the server side. 


## FORMULA:
P = I<sup>2</sup>R
<br> P --> Power (in watts)
<br> I --> Intensity
<br> R --> Resistance

## DESIGN STEPS:

### Step 1:
Clone the repository from GitHub.

### Step 2:
Create Django Admin project.

### Step 3:
Create a New App under the Django Admin project.

### Step 4:
Create python programs for views and urls to perform server side processing.

### Step 5:
Create a HTML file to implement form based input and output.

### Step 6:
Publish the website in the given URL.

## PROGRAM :
html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Power Calculation</title>
    <style>
        h1 {
            font-family: 'Times New Roman', Times, serif;
            text-align: center;
            font-style: normal;
            font-weight: bolder;
        }
        body, h2 {
            font-family: Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
            font-style: italic;
            background-image: linear-gradient(90deg,purple,rgba(246, 10, 49, 1),rgba(239, 229, 231, 1),rgba(231, 12, 48, 1),purple);
        }
    </style>    
</head>
<body align="center">
    <h1><u>Power Calculation</u></h1>
    <form method="post">
        {% csrf_token %}
        <label>Current (A):</label>
        <input type="text" name="current" required><br><br>
        <label>Resistance (Ω):</label>
        <input type="text" name="resistance" required><br><br>
        <button type="submit">Calculate Power</button>
    </form><br>

    {% if POWER is not None %}
        <h2 align="center"><u>POWER:</u> {{ POWER }} watt</h2>
    {% endif %}
</body>
</html>

views.py
from django.shortcuts import render

def act(request):
    power = None
    if request.method == "POST":
        try:
            current = float(request.POST.get("current"))
            resistance = float(request.POST.get("resistance"))
            power = round(current * current * resistance, 2)  # Rounded to 2 decimals
            print(f"Current: {current} A, Resistance: {resistance} Ω, Power: {power} W")
        except ValueError:
            power = "Invalid input. Please enter numbers only."
    return render(request, "power.html", {'POWER': power})
    
urls.py
from django.contrib import admin
from django.urls import path
from mathapp import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', views.act, name="home"),
]

    


## SERVER SIDE PROCESSING:
<img width="834" height="417" alt="image" src="https://github.com/user-attachments/assets/1dcf63ee-f44c-4e65-97d3-97e88ab76c8b" />


## HOMEPAGE:


## RESULT:
The program for performing server side processing is completed successfully.
