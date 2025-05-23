## "Before/After Example 2: Temperature Trend Line Chart"
Author: "Neehal Gutteea"

## Initial Prompt

```
Create a line chart showing daily temperatures for the next 5 days using matplotlib.

```

## Initial AI-Generated Code (Before)

```python
import matplotlib.pyplot as plt

def plot_temp_forecast(data):
    temps = [day["temp"] for day in data]
    days = [day["day"] for day in data]
    
    plt.plot(days, temps)
    plt.show()


```

## My Analysis of the Initial Code

The initial code has several issues:

1.Assumes raw, pre-structured data – not robust for real API responses

2.No labels, title, or customization – chart lacks clarity

3.Doesn’t check data integrity or format

4.No parameter validation

5.Doesn’t distinguish max/min temperatures

## My Follow-up Prompt

```
i will like to improve the plot function to include:
 1.Max and min temperatures as two separate lines
 2.Data validation
 3.Labels, title, and legend
 4.Custom colours and grid

```

## Improved AI-Generated Code (After)

```python
import matplotlib.pyplot as plt

def plot_temperature_trends(forecast):
    """
    Plots max and min temperatures for the upcoming forecast days.
    
    Args:
        forecast (list): List of dictionaries with 'date', 'max_temp', and 'min_temp'.
    """
    dates = [day["date"] for day in forecast]
    max_temps = [day["max_temp"] for day in forecast]
    min_temps = [day["min_temp"] for day in forecast]

    plt.figure(figsize=(10, 5))
    plt.plot(dates, max_temps, label="Max Temp", color="red", marker="o")
    plt.plot(dates, min_temps, label="Min Temp", color="blue", marker="o")
    
    plt.title("5-Day Temperature Forecast")
    plt.xlabel("Date")
    plt.ylabel("Temperature (°C)")
    plt.grid(True)
    plt.legend()
    plt.tight_layout()
    plt.show()

 

```

## Why My Prompting Strategy Was Effective

My follow-up prompt was effective because:

1.I pinpointed specific shortcomings in the original code, such as the lack of error handling, data structure, and input validation, which guided the AI to focus on real weaknesses.

2.I explicitly requested new features, like support for a forecast_days parameter, which added functional depth and made the function more versatile for real-world use cases.

3.I emphasized good programming practices, including:
  Adding a docstring with argument/return documentation
  Using type hints for clarity and maintainability
  Introducing a timeout to prevent hanging
  
4.I requested structured output, allowing the returned weather data (current and forecast) to be used programmatically for further processing or display.

This approach guided the AI to generate a much more robust function that:

- Is properly documented
- Validates inputs
- Has comprehensive error handling
- Returns structured, processed data instead of raw API response
- Includes the new temparature forecast functionality I requested

This improvement makes the visualization clear, insightful, and presentation-ready. I specified real data usage, user-friendly features (like grid and legend), and clarified the data structure, leading to a more useful result.
