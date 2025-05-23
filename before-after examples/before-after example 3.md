## "Before/After Example 3: : Precipitation Chance Bar Chart"
Author: "Neehal Gutteea"

## Initial Prompt

```
Plot precipitation chances for each day in the forecast using matplotlib.


```

## Initial AI-Generated Code (Before)

```python
def plot_precip(data):
    import matplotlib.pyplot as plt
    
    days = [d["day"] for d in data]
    rain_chances = [d["chance"] for d in data]
    
    plt.bar(days, rain_chances)
    plt.show()

```

## My Analysis of the Initial Code

1.Missing chart labels

2.Doesn’t validate inputs

3.Hard to interpret without axes titles and percentage formatting

4.Uses ambiguous variable names

## My Follow-up Prompt

```
i would like to update this chart to:
1. Show percentages on the y-axis
2. Label axes and add a title
3. Format values above bars
4. Use clear naming and docstrings

```

## Improved AI-Generated Code (After)

```python
iimport matplotlib.pyplot as plt

def plot_precipitation_chances(forecast):
    """
    Plots bar chart of precipitation chances over forecasted days.
    
    Args:
        forecast (list): List of dictionaries with 'date' and 'precipitation' -> 'chance'.
    """
    dates = [day["date"] for day in forecast]
    chances = [day["precipitation"]["chance"] for day in forecast]

    plt.figure(figsize=(8, 5))
    bars = plt.bar(dates, chances, color='skyblue')
    plt.ylim(0, 100)
    plt.title("Chance of Rain Over Forecasted Days")
    plt.xlabel("Date")
    plt.ylabel("Chance of Rain (%)")
    
    for bar in bars:
        height = bar.get_height()
        plt.text(bar.get_x() + bar.get_width()/2, height + 2, f"{height}%", ha='center')
    
    plt.tight_layout()
    plt.show()


```

## Why My Prompting Strategy Was Effective

My follow-up prompt was effective because:
My prompt focused on clarity
visual readability, resulting in an intuitive, 
easy-to-read bar chart with helpful context through labels and percentage annotations.
