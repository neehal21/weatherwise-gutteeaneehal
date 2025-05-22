## "Before/After Example 1: Weather Data Retrieval Function"
Author: "Neehal Gutteea"

## Initial Prompt

```
Write a function to get weather data from the wttr.in API for a given location.
```

## Initial AI-Generated Code (Before)

```python
def get_weather_simple(city):
    import requests
    url = f"https://wttr.in/{city}"
    result = requests.get(url)
    print(result.text)
```

## My Analysis of the Initial Code

The initial code has several issues:

1.No error handling – it will crash if the network request fails.
   
2.No flexibility – it always prints the result instead of returning it.

3.No structured data – doesn’t use the JSON format which makes processing impossible.

4.No input validation – doesn’t check whether the city input is valid.

5.No documentation – it lacks a docstring and type hints.

## My Follow-up Prompt

```
Thanks for the starting point. I'd like to improve this function with:

1.Adding error handling for network issues
2.Returning the weather as structured JSON data
3.Validating the city input
4.Using a timeout to avoid indefinite waits
5.Adding a docstring and type hints

Also, can you make it handle the forecast_days parameter to allow getting forecast for multiple days?
```

## Improved AI-Generated Code (After)

```python

   import requests
from typing import Optional, Dict, Any, List

def get_weather_data(city: str, forecast_days: int = 3, timeout: int = 10) -> Optional[Dict[str, Any]]:
    """
    Fetch current weather data and forecast for a given city using the wttr.in API in JSON format.
    
    Args:
        city (str): The city or location to retrieve the weather for.
        forecast_days (int): Number of forecast days to retrieve (1–5).
        timeout (int): Timeout for the HTTP request in seconds.
        
    Returns:
        dict: Dictionary containing current weather and forecast data if successful.
        None: If the request fails or input is invalid.
    """
    if not isinstance(city, str) or not city.strip():
        print("Invalid input: City name must be a non-empty string.")
        return None

    if not isinstance(forecast_days, int) or not (1 <= forecast_days <= 5):
        print("Invalid input: forecast_days must be between 1 and 5.")
        return None

    formatted_city = city.strip().replace(" ", "+")
    url = f"https://wttr.in/{formatted_city}?format=j1"

    try:
        response = requests.get(url, timeout=timeout)
        response.raise_for_status()
        data = response.json()

        current = data["current_condition"][0]
        forecast_raw = data.get("weather", [])[:forecast_days]

        forecast = []
        for day in forecast_raw:
            midday_hour = day["hourly"][4] if len(day["hourly"]) > 4 else day["hourly"][0]
            forecast.append({
                "date": day["date"],
                "max_temp_C": day["maxtempC"],
                "min_temp_C": day["mintempC"],
                "condition": midday_hour["weatherDesc"][0]["value"],
                "chance_of_rain": midday_hour.get("chanceofrain", "N/A"),
                "precip_mm": midday_hour["precipMM"]
            })

        return {
            "city": city.strip(),
            "current": {
                "temperature_C": current["temp_C"],
                "feels_like_C": current["FeelsLikeC"],
                "description": current["weatherDesc"][0]["value"],
                "humidity": current["humidity"],
                "wind_speed_kmph": current["windspeedKmph"],
                "precip_mm": current["precipMM"]
            },
            "forecast": forecast
        }

    except requests.exceptions.RequestException as e:
        print(f"Network error occurred: {e}")
        return None
    except (KeyError, ValueError, TypeError) as e:
        print(f"Error processing weather data: {e}")
        return None
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
- Includes the new forecast functionality I requested

The key to effective prompting was being specific about what needed improvement and why, rather than making vague requests for "better" code.
