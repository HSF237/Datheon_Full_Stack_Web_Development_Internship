# Skyline · Live Weather Telemetry

A single-file, responsive weather dashboard. Search any city in the world and get live conditions, animated icons, a 5-day forecast, and a background that changes with the weather and time of day. No build step, no dependencies, no framework.

## Features

- **Global city search** with live autocomplete (debounced, keyboard-navigable)
- **Current conditions:** temperature, feels-like, high/low, weather description
- **Telemetry tiles:** humidity, wind speed (km/h), atmospheric pressure (hPa), visibility (km)
- **5-day forecast** cards with high/low, a range bar and chance of precipitation
- **Dynamic icons:** hand-built animated SVGs (sun, moon, clouds, rain, snow, thunderstorm, mist)
- **Dynamic backgrounds:** muted gradients for clear, cloudy, rain, thunderstorm, snow and mist, switching to a night palette after the city's local sunset
- **Ambient effects:** canvas rain, snowfall and twinkling stars, drifting clouds, a soft sun glow
- **Loading spinner** while data is fetched
- **Graceful errors:** unknown city, offline, invalid or inactive API key, rate limiting, server errors
- **°C / °F toggle**, and the last five searches saved as quick chips
- Respects `prefers-reduced-motion`

## Quick start

1. Download `weather-telemetry.html`.
2. Open it directly in a modern browser (Chrome, Edge, Safari or Firefox) while online.

That's it. It must be opened in a real browser tab. Sandboxed previews (for example inside a chat window) block outside network requests, so the app will report that it can't reach the weather service.

## Configuration

Near the top of the `<script>` block:

```js
const KEY = 'YOUR_OPENWEATHERMAP_API_KEY';
```

Get a free key at [openweathermap.org](https://openweathermap.org/api). New keys can take up to about two hours to activate.

> **Security note:** this is a client-side app, so the key is visible to anyone who opens the file. That is fine for personal use. If you publish the page, use a key you can rotate, or proxy requests through your own server.

## Data sources

| Purpose | Service | Key needed |
|---|---|---|
| Current weather + 5-day / 3-hour forecast | OpenWeatherMap `/weather` and `/forecast` | Yes |
| City autocomplete suggestions | Open-Meteo Geocoding API | No |
| Automatic fallback weather data | Open-Meteo Forecast API | No |

The app tries OpenWeatherMap first. If the key is rejected (HTTP 401) or rate limited (HTTP 429), it transparently falls back to Open-Meteo, and the footer shows which source is in use. Once your OpenWeatherMap key activates, it is used automatically.

## How it works

| Piece | What it does |
|---|---|
| `getJSON()` | Wraps `fetch()` with `try/catch` and maps HTTP status codes to error types |
| `fetchWeather()` | Requests current weather and forecast in parallel with `Promise.all`, with fallback |
| `fetchOpenMeteo()` | Geocodes (if needed), fetches data and normalises it to the same shape |
| `fiveDays()` | Groups 3-hourly data into the city's local days and picks the dominant condition |
| `theme()` | Sets the background class and the particle effect from condition and day/night |
| `render()` | Builds the dashboard; the forecast cards are produced with `Array.map()` |
| `icon()` | Returns an animated inline SVG for a given condition |
| Autocomplete | Debounced geocoding lookup with arrow-key, Enter and Esc handling |

Day versus night is decided from the city's own sunrise and sunset times, and all displayed times use the city's timezone offset rather than your computer's.

## Customising

- **Colours:** edit the `body.clear`, `body.rain`, `body.night` and similar rules (`--c1`, `--c2`, `--c3`). Background transitions use CSS `@property`, so they animate smoothly.
- **Default city:** change the fallback in `store.get('last','Kochi')`.
- **Forecast length:** `fiveDays()` ends with `.slice(0,5)`.
- **Particle density:** adjust the counts in `seed()`.

## Browser support

Any current evergreen browser. Animated background colour transitions rely on CSS `@property` (Chrome, Edge, Safari 16.4+, Firefox 128+); older browsers still work but switch themes without the fade.

## Limitations

- Visibility is not available for every location and shows "—" when missing.
- The OpenWeatherMap free tier is rate limited.
- Forecast "today" may cover only the remaining hours of the day.

## Credits

Weather data from [OpenWeatherMap](https://openweathermap.org) and [Open-Meteo](https://open-meteo.com). Typeface: Outfit via Google Fonts, with a system-font fallback.
