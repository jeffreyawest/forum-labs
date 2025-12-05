# Weather App Specification (Enhanced)

> **Purpose**: This specification document provides complete requirements for building a full-featured weather application with Microsoft Fluent 2.0 design. Use this with AI coding assistants (Copilot, Cline) for deterministic, spec-driven development.

---

## Overview

A modern, responsive weather application built with vanilla HTML, CSS, and JavaScript using **Microsoft Fluent 2.0 Design System**. Displays current weather conditions, 5-day forecast, 48-hour hourly forecast, sun position visualization, and air quality data.

### Target Outcome
- **Look & Feel**: Microsoft Fluent 2.0 design system with professional polish
- **Functionality**: Full-featured weather lookup with advanced visualizations
- **Technology**: No frameworks, vanilla web technologies only
- **API**: OpenWeatherMap Free Tier (all available endpoints)

---

## Technical Requirements

### Technology Stack
| Layer | Technology | Notes |
|-------|------------|-------|
| Structure | HTML5 | Semantic elements |
| Styling | CSS3 | Fluent 2.0 design tokens, no frameworks |
| Logic | JavaScript ES6+ | Async/await, modules |
| Data | OpenWeatherMap API | Free tier (weather, forecast, air_pollution) |

### API Key
```javascript
const API_KEY = '81208750b50a113806b890f45520281a';
```

### File Structure
```
weather-app/
├── index.html      # Single-page application markup
├── styles.css      # Fluent 2.0 styling with design tokens
├── app.js          # Application logic and API integration
└── README.md       # Setup and usage documentation
```

### Browser Support
- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)

---

## Functional Requirements

### FR-1: Search Functionality

| ID | Requirement | Priority |
|----|-------------|----------|
| FR-1.1 | Text input accepts city name (e.g., "Seattle", "London, UK") | Must |
| FR-1.2 | Text input accepts US zip code (5-digit format) | Must |
| FR-1.3 | Search button triggers weather lookup | Must |
| FR-1.4 | Enter key in input triggers search | Must |
| FR-1.5 | Auto-detect zip code format using regex `/^\d{5}$/` | Must |
| FR-1.6 | Clear feedback when search is in progress | Must |

### FR-2: Geolocation Support

| ID | Requirement | Priority |
|----|-------------|----------|
| FR-2.1 | Button to use current device location | Must |
| FR-2.2 | Request browser geolocation permission | Must |
| FR-2.3 | Show appropriate error if permission denied | Must |
| FR-2.4 | Provide manual search fallback | Must |

### FR-3: Current Weather Display

| ID | Requirement | Priority |
|----|-------------|----------|
| FR-3.1 | Display city name and country code | Must |
| FR-3.2 | Display current date and time (formatted) | Must |
| FR-3.3 | Display temperature in Fahrenheit | Must |
| FR-3.4 | Display weather icon from API (@4x resolution) | Must |
| FR-3.5 | Display weather description (capitalized) | Must |

### FR-4: Weather Details Grid (8 Metrics)

| ID | Requirement | Priority |
|----|-------------|----------|
| FR-4.1 | Feels-like temperature | Must |
| FR-4.2 | Humidity percentage | Must |
| FR-4.3 | Wind speed (mph) | Must |
| FR-4.4 | Wind direction with rotating compass icon | Must |
| FR-4.5 | Atmospheric pressure (hPa) | Must |
| FR-4.6 | Cloudiness percentage | Must |
| FR-4.7 | Visibility (miles) | Must |
| FR-4.8 | Wind gusts (if available from API) | Should |

### FR-5: 5-Day Forecast

| ID | Requirement | Priority |
|----|-------------|----------|
| FR-5.1 | Display 5 forecast cards in a horizontal row | Must |
| FR-5.2 | Show day name (or "Today", "Tomorrow") | Must |
| FR-5.3 | Weather icon at 72x72px using @4x images | Must |
| FR-5.4 | Show high temperature per day | Must |
| FR-5.5 | Show low temperature per day | Must |

### FR-6: 48-Hour Hourly Forecast (Table Layout)

| ID | Requirement | Priority |
|----|-------------|----------|
| FR-6.1 | Two-column table layout | Must |
| FR-6.2 | Left column: Remaining hours for today | Must |
| FR-6.3 | Right column: Tomorrow with date header (e.g., "Tuesday, Dec 3") | Must |
| FR-6.4 | Each row displays: Time, icon, description, temperature | Must |
| FR-6.5 | "Now" indicator highlighted in Microsoft blue (#0078D4) | Must |
| FR-6.6 | Scrollable lists if many hours | Should |
| FR-6.7 | Hover effects on rows (Fluent 2.0 style) | Should |

### FR-7: Sun Position Card

| ID | Requirement | Priority |
|----|-------------|----------|
| FR-7.1 | Visual arc showing sun's path across sky | Must |
| FR-7.2 | Sun icon positioned on arc based on current time | Must |
| FR-7.3 | Sunrise time display (formatted) | Must |
| FR-7.4 | Sunset time display (formatted) | Must |
| FR-7.5 | Total daylight hours calculation | Must |
| FR-7.6 | Sun icon dims when below horizon (night time) | Should |

### FR-8: Air Quality Index (AQI) Card

| ID | Requirement | Priority |
|----|-------------|----------|
| FR-8.1 | Call `/data/2.5/air_pollution` endpoint using coords | Must |
| FR-8.2 | Display AQI number (1-5 scale) | Must |
| FR-8.3 | Color-coded rating label | Must |
| FR-8.4 | Individual pollutant readings | Must |
| FR-8.5 | Gradient background based on AQI level | Should |

**AQI Color Coding:**
| AQI | Label | Color |
|-----|-------|-------|
| 1 | Good | Green (#107C10) |
| 2 | Fair | Yellow (#FFB900) |
| 3 | Moderate | Orange (#FF8C00) |
| 4 | Poor | Red (#D13438) |
| 5 | Very Poor | Purple (#881798) |

**Pollutants to Display:**
- PM2.5 (Fine particles)
- PM10 (Coarse particles)
- O₃ (Ozone)
- NO₂ (Nitrogen dioxide)
- SO₂ (Sulfur dioxide)
- CO (Carbon monoxide)

### FR-9: Application States

| ID | Requirement | Priority |
|----|-------------|----------|
| FR-9.1 | Initial state: Welcome message with instructions | Must |
| FR-9.2 | Loading state: Spinner with "Fetching..." message | Must |
| FR-9.3 | Error state: Error message with retry button | Must |
| FR-9.4 | Success state: Full weather display | Must |
| FR-9.5 | Only one state visible at a time | Must |

---

## Non-Functional Requirements

### NFR-1: Microsoft Fluent 2.0 Design System

#### Color Tokens
```css
:root {
    /* Brand */
    --colorBrandBackground: #0078D4;
    --colorBrandBackgroundHover: #106EBE;
    --colorBrandBackgroundPressed: #005A9E;
    
    /* Neutral */
    --colorNeutralForeground1: #242424;
    --colorNeutralForeground2: #616161;
    --colorNeutralForeground3: #707070;
    --colorNeutralBackground1: #FFFFFF;
    --colorNeutralBackground2: #FAFAFA;
    --colorNeutralBackground3: #F5F5F5;
    --colorNeutralStroke1: #D1D1D1;
    --colorNeutralStroke2: #E0E0E0;
    
    /* Status */
    --colorStatusSuccessBackground: #DFF6DD;
    --colorStatusSuccessForeground: #107C10;
    --colorStatusWarningBackground: #FFF4CE;
    --colorStatusWarningForeground: #FFB900;
    --colorStatusDangerBackground: #FDE7E9;
    --colorStatusDangerForeground: #D13438;
}
```

#### Typography
```css
font-family: 'Segoe UI Variable', 'Segoe UI', system-ui, -apple-system, sans-serif;
```

| Name | Size | Weight | Line Height |
|------|------|--------|-------------|
| Caption | 12px | 400 | 16px |
| Body | 14px | 400 | 20px |
| Body Large | 16px | 400 | 22px |
| Subtitle | 20px | 600 | 28px |
| Title | 28px | 600 | 36px |
| Display | 40px | 600 | 52px |
| Hero (Temperature) | 68px | 300 | 76px |

#### Spacing Scale
```
4px, 8px, 12px, 16px, 20px, 24px, 32px, 40px, 48px
```

#### Border Radius
| Token | Value | Usage |
|-------|-------|-------|
| Small | 4px | Inputs, small buttons |
| Medium | 8px | Cards, containers |
| Large | 12px | Modal, large cards |
| XLarge | 16px | Hero sections |
| Circular | 50% | Icon buttons, avatars |

#### Elevation (Shadows)
```css
--shadow2: 0 1px 2px rgba(0,0,0,0.14), 0 0 2px rgba(0,0,0,0.12);
--shadow4: 0 2px 4px rgba(0,0,0,0.14), 0 0 2px rgba(0,0,0,0.12);
--shadow8: 0 4px 8px rgba(0,0,0,0.14), 0 0 2px rgba(0,0,0,0.12);
--shadow16: 0 8px 16px rgba(0,0,0,0.14), 0 0 2px rgba(0,0,0,0.12);
--shadow28: 0 14px 28px rgba(0,0,0,0.24), 0 0 8px rgba(0,0,0,0.12);
--shadow64: 0 32px 64px rgba(0,0,0,0.24), 0 0 8px rgba(0,0,0,0.12);
```

#### Component States
| State | Visual Change |
|-------|---------------|
| Hover | Background lightens/darkens slightly |
| Active/Pressed | Background darkens, slight scale(0.98) |
| Focus | 2px solid outline with brand color |
| Disabled | 40% opacity, cursor: not-allowed |

### NFR-2: Animations & Motion

| Element | Animation |
|---------|-----------|
| All transitions | 200ms cubic-bezier(0.33, 0, 0.67, 1) |
| Buttons hover | background-color transition |
| Cards hover | translateY(-2px), shadow increase |
| Wind compass | rotate() based on wind.deg |
| Loading spinner | rotate 360° (1s linear infinite) |
| Sun on arc | position based on time |

### NFR-3: Responsive Design

#### Breakpoints
| Size | Width | Adjustments |
|------|-------|-------------|
| Desktop | > 1024px | Full layout, all features visible |
| Tablet | 768-1024px | Adjusted grids, 2-column details |
| Mobile | < 768px | Stacked layout, compact forecast |

#### Specific Adjustments
- Weather details: 4 columns → 2 columns on mobile
- Hourly table: Full width, may need scroll
- 5-day forecast: Horizontal scroll on small screens
- Temperature: 68px → 48px on mobile
- Cards: Reduced padding on mobile

### NFR-4: Accessibility

- Focus-visible outlines (2px solid brand color)
- ARIA labels on all interactive elements
- prefers-reduced-motion: reduce for users who prefer less motion
- prefers-color-scheme support (optional dark mode)
- Color contrast meets WCAG AA (4.5:1 for text)
- Screen reader friendly structure

---

## API Integration

### OpenWeatherMap Configuration

```javascript
const API_KEY = '81208750b50a113806b890f45520281a';
const BASE_URL = 'https://api.openweathermap.org/data/2.5';
```

### Endpoints Used

| Endpoint | Purpose | Parameters |
|----------|---------|------------|
| `/weather` | Current weather + sunrise/sunset | q, zip, lat/lon, appid, units |
| `/forecast` | 5-day/3-hour forecast (40 entries) | lat, lon, appid, units |
| `/air_pollution` | Air quality data | lat, lon, appid |

### Request Examples

```javascript
// Current weather by city
`${BASE_URL}/weather?q=${city}&appid=${API_KEY}&units=imperial`

// Current weather by zip
`${BASE_URL}/weather?zip=${zip},US&appid=${API_KEY}&units=imperial`

// Current weather by coords
`${BASE_URL}/weather?lat=${lat}&lon=${lon}&appid=${API_KEY}&units=imperial`

// Forecast (use coords from current weather response)
`${BASE_URL}/forecast?lat=${lat}&lon=${lon}&appid=${API_KEY}&units=imperial`

// Air pollution
`${BASE_URL}/air_pollution?lat=${lat}&lon=${lon}&appid=${API_KEY}`
```

### Response Data Used

**Current Weather (`/weather`):**
```javascript
{
  name,                    // City name
  sys.country,            // Country code
  sys.sunrise,            // Unix timestamp
  sys.sunset,             // Unix timestamp
  main.temp,              // Temperature
  main.feels_like,        // Feels like
  main.humidity,          // Humidity %
  main.pressure,          // Pressure hPa
  wind.speed,             // Wind mph
  wind.deg,               // Wind direction degrees
  wind.gust,              // Wind gust (if available)
  visibility,             // Visibility meters
  clouds.all,             // Cloudiness %
  weather[0].main,        // Condition (Clear, Clouds, etc.)
  weather[0].description, // Description
  weather[0].icon,        // Icon code
  coord.lat,              // Latitude (for other API calls)
  coord.lon               // Longitude
}
```

**Forecast (`/forecast`):**
```javascript
{
  list: [                 // 40 entries (3-hour intervals)
    {
      dt,                 // Unix timestamp
      main.temp,
      main.temp_max,
      main.temp_min,
      weather[0].description,
      weather[0].icon
    }
  ]
}
```

**Air Pollution (`/air_pollution`):**
```javascript
{
  list: [{
    main.aqi,             // 1-5 scale
    components: {
      co,                 // μg/m³
      no2,
      o3,
      so2,
      pm2_5,
      pm10
    }
  }]
}
```

### Weather Icons
```
Standard: https://openweathermap.org/img/wn/{icon}@2x.png (100x100)
Large:    https://openweathermap.org/img/wn/{icon}@4x.png (200x200)
```

### Error Handling

| HTTP Status | User Message |
|-------------|--------------|
| 401 | "Invalid API key. Please check your configuration." |
| 404 | "Location not found. Please check the city name or zip code." |
| 429 | "Too many requests. Please wait and try again." |
| Network | "Network error. Please check your connection." |
| Other | "Failed to fetch weather data. Please try again." |

---

## HTML Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weather App</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="app-container">
        <!-- Header with search -->
        <header class="header">
            <h1>Weather</h1>
            <div class="search-container">
                <input type="text" id="searchInput" placeholder="City or zip code...">
                <button id="searchBtn" aria-label="Search">🔍</button>
                <button id="locationBtn" aria-label="Use my location">📍</button>
            </div>
        </header>

        <!-- Loading state -->
        <div id="loading" class="loading hidden">
            <div class="spinner"></div>
            <p>Fetching weather data...</p>
        </div>

        <!-- Error state -->
        <div id="error" class="error hidden">
            <p id="errorMessage"></p>
            <button id="retryBtn">Try Again</button>
        </div>

        <!-- Weather content -->
        <main id="weatherContent" class="weather-content hidden">
            <!-- Current weather -->
            <section class="current-weather">
                <div class="location-info">
                    <h2 id="cityName"></h2>
                    <p id="dateTime"></p>
                </div>
                <div class="weather-main">
                    <img id="weatherIcon" alt="Weather icon">
                    <span id="temperature"></span>
                    <p id="description"></p>
                </div>
            </section>

            <!-- Weather details grid (8 metrics) -->
            <section class="weather-details">
                <!-- Feels like, Humidity, Wind, Direction, Pressure, Clouds, Visibility, Gusts -->
            </section>

            <!-- Sun position card -->
            <section class="sun-card">
                <div class="sun-arc"><!-- SVG arc with sun position --></div>
                <div class="sun-times">
                    <span id="sunrise"></span>
                    <span id="daylight"></span>
                    <span id="sunset"></span>
                </div>
            </section>

            <!-- Air quality card -->
            <section class="aqi-card">
                <h3>Air Quality</h3>
                <div id="aqiValue" class="aqi-value"></div>
                <div id="pollutants" class="pollutants"></div>
            </section>

            <!-- 48-hour forecast table -->
            <section class="hourly-forecast">
                <h3>48-Hour Forecast</h3>
                <div class="hourly-table">
                    <div class="hourly-column" id="todayColumn">
                        <h4>Today</h4>
                        <!-- Hourly rows -->
                    </div>
                    <div class="hourly-column" id="tomorrowColumn">
                        <h4 id="tomorrowDate">Tomorrow</h4>
                        <!-- Hourly rows -->
                    </div>
                </div>
            </section>

            <!-- 5-day forecast -->
            <section class="forecast">
                <h3>5-Day Forecast</h3>
                <div id="forecastContainer" class="forecast-container">
                    <!-- 5 forecast cards -->
                </div>
            </section>
        </main>

        <!-- Initial state -->
        <div id="initialState" class="initial-state">
            <h2>Welcome to Weather</h2>
            <p>Search for a city or use your current location.</p>
            <button id="getLocationBtn">📍 Use My Location</button>
        </div>
    </div>

    <script src="app.js"></script>
</body>
</html>
```

---

## JavaScript Architecture

```javascript
// ==========================================
// 1. CONFIGURATION
// ==========================================
const API_KEY = '81208750b50a113806b890f45520281a';
const BASE_URL = 'https://api.openweathermap.org/data/2.5';

// ==========================================
// 2. DOM ELEMENT REFERENCES
// ==========================================
const elements = {
    searchInput: document.getElementById('searchInput'),
    searchBtn: document.getElementById('searchBtn'),
    // ... all elements
};

// ==========================================
// 3. STATE
// ==========================================
let lastSearch = null;

// ==========================================
// 4. EVENT LISTENERS
// ==========================================
function initEventListeners() {
    elements.searchBtn.addEventListener('click', handleSearch);
    elements.searchInput.addEventListener('keypress', handleKeyPress);
    elements.locationBtn.addEventListener('click', handleGeolocation);
    elements.retryBtn.addEventListener('click', handleRetry);
}

// ==========================================
// 5. API FUNCTIONS
// ==========================================
async function fetchWeatherByQuery(query) { }
async function fetchWeatherByCoords(lat, lon) { }
async function fetchForecast(lat, lon) { }
async function fetchAirQuality(lat, lon) { }
async function fetchData(url) { }

// ==========================================
// 6. DISPLAY FUNCTIONS
// ==========================================
function displayCurrentWeather(data) { }
function displayWeatherDetails(data) { }
function displayForecast(data) { }
function displayHourlyForecast(data) { }
function displaySunPosition(sunrise, sunset) { }
function displayAirQuality(data) { }

// ==========================================
// 7. UI STATE FUNCTIONS
// ==========================================
function showLoading() { }
function showError(message) { }
function showWeatherContent() { }
function showInitialState() { }

// ==========================================
// 8. UTILITY FUNCTIONS
// ==========================================
function formatDateTime(timestamp) { }
function formatTime(timestamp) { }
function formatDay(timestamp) { }
function getWindDirection(degrees) { }
function getAQILabel(aqi) { }
function getAQIColor(aqi) { }
function calculateSunPosition(sunrise, sunset) { }

// ==========================================
// 9. INITIALIZATION
// ==========================================
document.addEventListener('DOMContentLoaded', () => {
    initEventListeners();
    showInitialState();
});
```

---

## Acceptance Criteria

### Must Have (P0)
- [ ] Search by city name returns complete weather data
- [ ] Search by zip code returns complete weather data
- [ ] Current temperature displays with @4x icon
- [ ] All 8 weather detail metrics display
- [ ] 5-day forecast shows 5 cards with 72px icons
- [ ] 48-hour forecast displays in Today/Tomorrow table
- [ ] "Now" row highlighted in Microsoft blue
- [ ] Sun position arc visualizes current sun location
- [ ] Sunrise/sunset times display
- [ ] Air Quality Index displays with color coding
- [ ] Pollutant breakdown shows all 6 values
- [ ] Microsoft Fluent 2.0 design tokens applied
- [ ] Responsive layout works on mobile

### Should Have (P1)
- [ ] Geolocation button works
- [ ] Loading spinner during API calls
- [ ] Error messages display appropriately
- [ ] Retry button works
- [ ] Wind direction compass rotates
- [ ] Smooth transitions (200ms)
- [ ] Hover states on interactive elements
- [ ] Focus-visible outlines

### Nice to Have (P2)
- [ ] Sun icon dims at night
- [ ] Daylight hours calculation
- [ ] Reduced motion support
- [ ] Dark mode support
- [ ] Temperature unit toggle (°F/°C)

---

## Testing Checklist

### Functionality Tests
- [ ] Search "Seattle" → Shows Seattle, US weather
- [ ] Search "98101" → Shows Seattle weather (zip)
- [ ] Search "London" → Shows London, GB weather
- [ ] Search "InvalidCity123" → Shows error message
- [ ] Click location → Prompts for permission
- [ ] Deny location → Shows helpful error
- [ ] Click retry → Re-attempts last search

### Display Tests
- [ ] Temperature shows whole number in °F
- [ ] All 8 weather details show values
- [ ] 5-day forecast has 5 cards
- [ ] Hourly table has Today and Tomorrow columns
- [ ] Sun arc shows sun in correct position
- [ ] AQI shows colored badge
- [ ] Wind compass points correct direction

### Responsive Tests
- [ ] Desktop (1200px): Full layout
- [ ] Tablet (768px): 2-column details
- [ ] Mobile (375px): Stacked, scrollable

### Accessibility Tests
- [ ] Tab navigation works
- [ ] Focus outlines visible
- [ ] ARIA labels present
- [ ] Color contrast sufficient

---

## Reference

This spec is used in **Lab 2: Agentic Coding with Specs** to demonstrate how detailed specifications lead to deterministic AI-assisted development with minimal iteration.

Compare results with **Lab 1: Vibe Coding** which achieves the same features through 9+ iterative prompts.
