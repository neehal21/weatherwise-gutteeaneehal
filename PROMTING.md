---
title: "Sample Intentional Prompting Journey"
subtitle: "Weather Dashboard Project"
format:
  pdf:
    toc: false
    number-sections: false
    colorlinks: true
  docx:
    toc: false
    number-sections: false
    highlight-style: github
  html:
    toc: true
    toc-expand: 2
    embed-resources: true
---

This document demonstrates how a student might approach the Weather Dashboard project using intentional prompting techniques. It follows the 6-step programming methodology and showcases a variety of prompt types.

> **Important Note to Students**: This document demonstrates the *approach* to intentional prompting, not specific prompts to copy. Your project will have unique requirements and challenges that will require your own thoughtful prompts. Simply copying these example prompts will not result in the best solution for your specific implementation, and will not demonstrate your personal understanding and engagement with the AI. The assessment focuses on your ability to craft effective prompts specific to your project's needs - not on reproducing this example. Use this as inspiration for your own authentic conversations with AI, where you identify problems, ask clarifying questions, challenge initial solutions, and guide the AI toward better outcomes for your particular implementation.


The 5 Ai Conversations:

Conversation 1:

Me: How do I retrieve weather data for a given location in Python?
AI: You can use the fetch-my-weather package with get_weather(location) to get current weather and forecasts.

Me: Can you show me a function that takes location and days as input and returns the weather data?
AI: Sure! Here’s a simple function:


from fetch_my_weather import get_weather
def get_weather_data(location, forecast_days=5):

    weather = get_weather(location)
    return weather["forecast"]
    [:forecast_days]
    
Conversation 2:

Me: How do I plot temperature trends over multiple days using matplotlib?
AI: Extract the dates and temperature data, then use plt.plot(dates, temps) with proper labels.

Me: Can you help me write a function that creates this plot?
AI: Sure:


import matplotlib.pyplot as plt

def create_temperature_visualisation(weather_data):

    dates = [day['date'] for day in weather_data]
    
    temps = [day['avgtempC'] for day in weather_data]
    
    plt.plot(dates, temps)
    plt.title('Temperature Trend')
    plt.xlabel('Date')
    plt.ylabel('Avg Temperature (°C)')
    plt.show()

    
Conversation 3:

Me: I want to parse a natural language question like "What will the temperature be in Sydney tomorrow?" How do I extract location and time?
AI: You can use regex or NLP libraries like spaCy. A simple approach is keyword matching.

Me: Can you sketch a basic function for this?
AI: Sure, here’s a simple example:


def parse_weather_question(question):

    locations = ["Sydney", "Melbourne", "Brisbane"]
    
    for loc in locations:
        if loc.lower() in question.lower():
            location = loc
            break
    if "tomorrow" in question.lower():
        day = 1
    else:
        day = 0
    return {"location": location, "day_offset": day}

    
Conversation 4:

Me: How do I generate a natural language response from weather data and parsed questions?
AI: Combine the extracted info with the relevant weather forecast and format a string.

Me: Can you show me an example?
AI: Sure:

def generate_weather_response(parsed_question, weather_data):

    location = parsed_question.get("location")
    day_offset = parsed_question.get("day_offset", 0)
    forecast = weather_data[day_offset]
    temp = forecast['avgtempC']
    return f"The average temperature in {location} will be {temp}°C."


Conversation 5:

Me: How can I visualise weather forecast data in Python using matplotlib?
AI: You can use matplotlib.pyplot to plot data like temperature trends over multiple days. For example:


import matplotlib.pyplot as plt

def plot_temperature_forecast(forecast):
    dates = [day["date"] for day in forecast]
    max_temps = [day["max_temp"] for day in forecast]
    min_temps = [day["min_temp"] for day in forecast]

    plt.figure(figsize=(10, 5))
    plt.plot(dates, max_temps, label="Max Temp", marker="o")
    plt.plot(dates, min_temps, label="Min Temp", marker="o")
    plt.title("Temperature Forecast")
    plt.xlabel("Date")
    plt.ylabel("Temperature (°C)")
    plt.legend()
    plt.grid(True)
    plt.tight_layout()
    plt.show()
Me: That’s great! How do I integrate this with my existing weather function?
AI: You can call plot_temperature_forecast() and pass in the forecast list from your weather data like this:

weather = get_weather_data("Perth", forecast_days=3)
if weather:

    plot_temperature_forecast(weather["forecast"])
    
Me: Can I also add precipitation as a bar chart?
AI: Yes, you can use a secondary y-axis to add precipitation:

def plot_weather_with_precip(forecast):
    import matplotlib.pyplot as plt

    dates = [day["date"] for day in forecast]
    max_temps = [day["max_temp"] for day in forecast]
    min_temps = [day["min_temp"] for day in forecast]
    precip = [day["precipitation"]["amount"] for day in forecast]

    fig, ax1 = plt.subplots(figsize=(10, 5))

    ax1.plot(dates, max_temps, label="Max Temp", color="red", marker="o")
    ax1.plot(dates, min_temps, label="Min Temp", color="blue", marker="o")
    ax1.set_xlabel("Date")
    ax1.set_ylabel("Temperature (°C)")
    ax1.tick_params(axis='y')

    ax2 = ax1.twinx()
    ax2.bar(dates, precip, color='skyblue', alpha=0.6, label="Precipitation (mm)")
    ax2.set_ylabel("Precipitation (mm)")

    fig.tight_layout()
    ax1.legend(loc="upper left")
    ax2.legend(loc="upper right")
    plt.title("Weather Forecast with Precipitation")
    plt.show()
