Create a single self-contained HTML file: a weather dashboard using the Open-Meteo API (no API key required).

Requirements:
- A city search box using Open-Meteo's geocoding endpoint (https://geocoding-api.open-meteo.com/v1/search).
- Current conditions: temperature, feels-like, wind speed, humidity, and a weather icon or symbol matching the condition code.
- A 7-day forecast row showing each day's high, low, and condition.
- An hourly temperature chart for the next 24 hours, drawn on a canvas with labelled axes.
- Handle the loading state, network errors, and "city not found" with clear messages.
- Clean, responsive layout that works on a phone-width screen.

No libraries, no CDN, no external assets. The only network requests are to Open-Meteo.
Output the complete HTML file and nothing else.
