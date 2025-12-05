I need to prepare a lab for participants to teach them about agentic programming.  Here are the labs:

1. Vibe coding a Weather Lookup app - given a stated goal, have the participants try to iteratively prompt Copilot or Cline to reproduce that result.  The intent is to show that its possible, but iterative prompting without specific details takes more effort than providing a spec up-front.  In the next lab, we will have them to the same with a spec.
2. Agentic Coding with Specs and Engineered Context - The goal here is to provide them a spec (possibly SpecKit) and/or set of context files in Markdown and have a Plan created with Cline's "deep-panning" tool, then have a better/faster/more-deterministic outcome
3. Create an MCP server and/or Configure/Use MCP Servers w/ Cline or Copilot - Given an API, or Storage Container of information (Context), create a context-providing MCP server with a set of operations.  Also, configure the Microsoft ADO and/or AskESChat
4. Use Copilot/Cline in PLAN mode in your codebase, ask informed questions, create a memory bank / context store.

Help me create the agenda and lab guides for this.  

Lab 1 Iterative prompts, for example:

OpenWeatherMap API Key: 81208750b50a113806b890f45520281a

# Step 1:
Prompt: [Plan Mode] I want a weather app that shows the temperature for a given city or zip code.

Example response:
I'd like to build this weather app for you. To create something that meets your needs, I have a few clarifying questions:

1. __Platform__: What type of app would you like?

    - Web app (HTML/CSS/JavaScript)
    - Desktop app
    - Command-line tool
    - Mobile app

2. __Weather Data Source__: Do you have a preferred weather API, or should I choose one? (e.g., OpenWeatherMap, WeatherAPI, etc.)

3. __Features__: Besides temperature, would you like any additional information displayed?

    - Weather conditions (sunny, cloudy, rain)
    - Humidity
    - Wind speed
    - Forecast (daily/hourly)

4. __Design__: Any preferences for the look and feel?

Answers 1:
  - Web app (HTML/CSS/JavaScript)
  - Choose your datasource
  - All features
  - Make it look good

# Step 2:
Add OpenWeatherMap API Key: 81208750b50a113806b890f45520281a

# Step 3: 
Prompt: [Act Mode] make the UI Microsoft Fluent 2.0

Response:
Weather App updated with Microsoft Fluent 2.0 Design System!

__Fluent 2.0 Features Applied:__

- __Colors__: Microsoft brand blue (#0078D4), neutral grays, proper foreground/background tokens
- __Typography__: Segoe UI Variable font with Fluent type scale (10px-68px)
- __Spacing__: Consistent 4/8/12/16/20/24/32px spacing scale
- __Border Radius__: Fluent corners (4/8/12/16px)
- __Elevation__: Fluent shadow tokens (shadow-2 through shadow-64)
- __Components__: Cards, inputs, and buttons styled per Fluent specs
- __Interactions__: Proper hover, active, and focus states
- __Accessibility__: Focus-visible outlines, high contrast mode, reduced motion support

Refresh your browser to see the new Fluent 2.0 design.

**

Step 4:
Prompt: [Act Mode] add an hourly forecast for the next 48 hours

Response:
48-Hour Hourly Forecast has been added to the Weather App!

**New Features:**
- Scrollable hourly forecast showing next 48 hours (16 x 3-hour intervals)
- "Now" indicator highlights the current hour with Microsoft blue
- Left/right scroll buttons for easy navigation
- Weather icons and temperatures for each hour
- Smooth horizontal scrolling with hidden scrollbars
- Fluent 2.0 styled hourly cards with hover effects

**Updated Files:**
- `index.html` - Added hourly forecast section with scroll container
- `styles.css` - Added Fluent 2.0 styled hourly cards and scroll buttons
- `app.js` - Added `displayHourlyForecast()` and scroll button functionality

Refresh your browser and search for a city to see the new hourly forecast section.

# Step 5:
Prompt: [Act Mode] Make the 48 hour forecast be a table with the rest of today on the left, and tomorrow on the right.

Response: 48-Hour Forecast updated to a two-column table layout!

**New Layout:**
- **Left Column (Today)**: Shows remaining hours for today with "Now" indicator
- **Right Column (Tomorrow)**: Shows all hourly forecasts for the next day with date header

**Each row displays:**
- Time (e.g., "Now", "3 PM", "6 PM")
- Weather icon
- Weather description (e.g., "clear sky", "scattered clouds")
- Temperature

**Features:**
- Scrollable lists if many hours to show
- "Now" row highlighted in Microsoft blue
- Tomorrow's header shows full date (e.g., "Tuesday, Dec 3")
- Fluent 2.0 styled with hover effects

Refresh your browser and search for a city to see the new table layout.

# Step 6:
Prompt: [Act Mode] make the icons/conditions picture in the 5-day forecast larger

Response:
5-day forecast icons enlarged from 48px to 72px with increased margin for better visibility.

Refresh your browser to see the larger weather icons in the 5-day forecast section.

# Step 7:
Prompt: [Act Mode] they look the same size

Response:
5-day forecast icons now use higher resolution @4x images (100x100 native) displayed at 72x72px for sharper, larger weather icons.

Refresh your browser and search for a city to see the larger, higher-quality icons in the 5-day forecast section.

Step 8: what else can I add to the page that is available on the OpenWeatherMap free API tier?
Prompt: [Act Mode] 

Response:
Here are additional features available on the **OpenWeatherMap Free API tier** that you could add:

## Currently Unused Data from Current Weather API
Your app already fetches this data but doesn't display it:
1. **Pressure** - Atmospheric pressure (hPa)
2. **Cloudiness** - Cloud coverage percentage
3. **Sunrise/Sunset times** - Can display as icons with times
4. **Wind direction** - Wind degrees (can show as compass direction)
5. **Wind gusts** - If available

## New API Endpoints (Free Tier)
1. **Air Pollution API** - `api.openweathermap.org/data/2.5/air_pollution`
    - Air Quality Index (AQI)
    - CO, NO, NO2, O3, SO2, PM2.5, PM10 levels
    - Good for health-conscious users

2. **Geocoding API** - `api.openweathermap.org/geo/1.0/direct`
    - Better city search with autocomplete suggestions
    - Shows city, state, country for disambiguation

3. **UV Index** - Available in One Call API (if you have access)

## UI Enhancements with Existing Data
1. **Sun position indicator** - Visual arc showing current time between sunrise/sunset
2. **Pressure trend** - High/low pressure indicator
3. **Day/Night mode** - Auto-switch based on sunrise/sunset
4. **Wind compass** - Visual wind direction indicator
5. **"Feels like" context** - Add humidity/wind chill explanation

Would you like me to implement any of these features? I'd suggest:
- **Air Quality Index** (most useful health info)
- **Sunrise/Sunset display** (easy win with existing data)
- **Pressure & cloudiness cards** (expand weather details)

Followup: add all of it.  Use your best judgement how to do it.  YOLO!

Response:
Weather app enhanced with all available OpenWeatherMap free tier features!

**New Features Added:**

1. **Expanded Weather Details (8 metrics now):**
    - Feels Like, Humidity, Wind Speed, Wind Direction (with rotating compass icon)
    - Pressure (hPa), Cloudiness (%), Visibility, Wind Gusts

2. **Sun Position Card:**
    - Visual arc showing sun's current position in the sky
    - Sunrise and sunset times
    - Total daylight hours calculation
    - Sun dims when below horizon (night time)

3. **Air Quality Index (AQI) Card:**
    - Color-coded AQI rating (Good/Fair/Moderate/Poor/Very Poor)
    - Individual pollutant readings: PM2.5, PM10, O₃, NO₂, SO₂, CO
    - Gradient backgrounds based on air quality level

**API Endpoints Used:**
- `/weather` - Current weather + sunrise/sunset
- `/forecast` - 5-day/3-hour forecast
- `/air_pollution` - Air quality data

Refresh your browser and search for a city to see all the new features!