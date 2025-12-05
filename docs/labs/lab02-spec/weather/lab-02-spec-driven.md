# Lab 2: Agentic Coding with Specs and Engineered Context

## 🎯 Objective

Build the **same Weather Lookup application** from Lab 1, but this time using detailed specifications, engineered context files, and structured planning. Experience how proper preparation leads to faster, more deterministic results.

**Time:** 45 minutes

---

## Learning Goals

By the end of this lab, you will:
- ✅ Create and use specification documents
- ✅ Understand context engineering principles
- ✅ Use Cline's Deep Planning feature
- ✅ Compare results with Lab 1's iterative approach
- ✅ Experience deterministic AI-assisted development

---

## The Approach Difference

| Lab 1 (Vibe Coding) | Lab 2 (Spec-Driven) |
|---------------------|---------------------|
| "Make me a weather app" | Detailed spec document |
| 9+ iterative prompts | 1-2 prompts |
| AI makes assumptions | You define requirements |
| Inconsistent results | Deterministic output |
| Design drift over iterations | Consistent design system |

---

## Setup

### Prerequisites
- VS Code with Cline and/or GitHub Copilot installed
- Completed Lab 1 (for comparison)
- OpenWeatherMap API Key: `81208750b50a113806b890f45520281a`

### Create Your Workspace
```bash
mkdir weather-app-spec
cd weather-app-spec
code .
```

---

## 📝 Lab Instructions

### Phase 1: Create the Specification (10 minutes)

Before writing any code, you'll create a comprehensive specification document that includes **all the features** you built iteratively in Lab 1.

#### Step 1: Create the Spec File

Create a new file called `SPEC.md` in your project root:

```markdown
# Weather App Specification

## Overview
A modern, responsive weather application built with vanilla HTML, CSS, and JavaScript using **Microsoft Fluent 2.0 Design System**. Displays current weather conditions, 5-day forecast, 48-hour hourly forecast, sun position, and air quality data.

## Technical Requirements

### Stack
- HTML5
- CSS3 (no frameworks, Fluent 2.0 design tokens)
- Vanilla JavaScript (ES6+)
- OpenWeatherMap API (Free Tier)

### API Key
```
81208750b50a113806b890f45520281a
```

### File Structure
```
weather-app/
├── index.html      # Main HTML structure
├── styles.css      # Fluent 2.0 styling
├── app.js          # JavaScript logic
└── README.md       # Documentation
```

## Functional Requirements

### FR-1: Search Functionality
- **FR-1.1**: Text input for city name OR US zip code
- **FR-1.2**: Search button with icon
- **FR-1.3**: Enter key triggers search
- **FR-1.4**: Auto-detect zip code format (5 digits)

### FR-2: Geolocation
- **FR-2.1**: Button to use current location
- **FR-2.2**: Request browser geolocation permission
- **FR-2.3**: Graceful fallback if denied with helpful message

### FR-3: Current Weather Display
- **FR-3.1**: City name and country
- **FR-3.2**: Current date and time (formatted)
- **FR-3.3**: Temperature (Fahrenheit)
- **FR-3.4**: Weather icon from API (@4x resolution)
- **FR-3.5**: Weather description (capitalized)

### FR-4: Weather Details Grid (8 metrics)
- **FR-4.1**: Feels-like temperature
- **FR-4.2**: Humidity percentage
- **FR-4.3**: Wind speed (mph)
- **FR-4.4**: Wind direction (rotating compass icon)
- **FR-4.5**: Pressure (hPa)
- **FR-4.6**: Cloudiness (%)
- **FR-4.7**: Visibility (miles)
- **FR-4.8**: Wind gusts (if available)

### FR-5: 5-Day Forecast
- **FR-5.1**: Display 5 forecast cards in a row
- **FR-5.2**: Show day name (or "Today", "Tomorrow")
- **FR-5.3**: Weather icon (@4x, displayed at 72x72px)
- **FR-5.4**: High/Low temperatures

### FR-6: 48-Hour Hourly Forecast (Table Layout)
- **FR-6.1**: Two-column table layout
- **FR-6.2**: Left column: Rest of today's hours
- **FR-6.3**: Right column: Tomorrow with date header
- **FR-6.4**: Each row: Time, icon, description, temperature
- **FR-6.5**: "Now" indicator highlighted in Microsoft blue
- **FR-6.6**: Scrollable if many hours

### FR-7: Sun Position Card
- **FR-7.1**: Visual arc showing sun's current position
- **FR-7.2**: Sunrise time display
- **FR-7.3**: Sunset time display
- **FR-7.4**: Total daylight hours calculation
- **FR-7.5**: Sun icon dims when below horizon

### FR-8: Air Quality Index (AQI) Card
- **FR-8.1**: Call `/data/2.5/air_pollution` endpoint
- **FR-8.2**: Color-coded AQI rating (Good/Fair/Moderate/Poor/Very Poor)
- **FR-8.3**: Pollutant readings: PM2.5, PM10, O₃, NO₂, SO₂, CO
- **FR-8.4**: Gradient background based on AQI level

### FR-9: UI States
- **FR-9.1**: Initial welcome state with instructions
- **FR-9.2**: Loading state with spinner
- **FR-9.3**: Error state with retry button
- **FR-9.4**: Weather display state

## Non-Functional Requirements

### NFR-1: Microsoft Fluent 2.0 Design System

#### Colors
```css
--colorBrandBackground: #0078D4;  /* Microsoft blue */
--colorNeutralForeground1: #242424;
--colorNeutralForeground2: #616161;
--colorNeutralBackground1: #FFFFFF;
--colorNeutralBackground3: #F5F5F5;
--colorNeutralStroke1: #D1D1D1;
```

#### Typography
```css
font-family: 'Segoe UI Variable', 'Segoe UI', sans-serif;
/* Type scale: 10, 12, 14, 16, 20, 24, 28, 32, 40, 48, 68px */
```

#### Spacing Scale
```
4px, 8px, 12px, 16px, 20px, 24px, 32px
```

#### Border Radius
```
4px (small), 8px (medium), 12px (large), 16px (extra-large)
```

#### Elevation (Shadows)
```css
--shadow2: 0 1px 2px rgba(0,0,0,0.14);
--shadow4: 0 2px 4px rgba(0,0,0,0.14);
--shadow8: 0 4px 8px rgba(0,0,0,0.14);
--shadow16: 0 8px 16px rgba(0,0,0,0.14);
--shadow64: 0 32px 64px rgba(0,0,0,0.24);
```

#### Interactions
- Hover states with subtle background change
- Active/pressed states
- Focus-visible outlines for accessibility
- High contrast mode support
- Reduced motion support

### NFR-2: Responsiveness
- Desktop: Full multi-column layout
- Tablet: Adjusted grid, 2-column weather details
- Mobile: Stacked layout, compact forecast

### NFR-3: Accessibility
- ARIA labels on all interactive elements
- Focus-visible outlines
- High contrast mode support
- prefers-reduced-motion support

## API Integration

### OpenWeatherMap Endpoints (Free Tier)

| Endpoint | Purpose |
|----------|---------|
| `/data/2.5/weather` | Current weather + sunrise/sunset |
| `/data/2.5/forecast` | 5-day/3-hour forecast (48 hours) |
| `/data/2.5/air_pollution` | Air quality data |

### Weather Icons
```
Small: https://openweathermap.org/img/wn/{icon}@2x.png
Large: https://openweathermap.org/img/wn/{icon}@4x.png
```

### Error Handling
| Status | Message |
|--------|---------|
| 401 | "Invalid API key" |
| 404 | "Location not found" |
| 429 | "Too many requests" |
| Other | "Failed to fetch weather data" |

## Acceptance Criteria

### Must Have (P0)
- [ ] Search works for city names and zip codes
- [ ] Current weather displays with all 8 detail metrics
- [ ] 5-day forecast with large (72px) icons
- [ ] 48-hour forecast in Today/Tomorrow table
- [ ] Sun position arc visualization
- [ ] Air quality index with pollutant breakdown
- [ ] Microsoft Fluent 2.0 design applied
- [ ] Responsive on mobile

### Should Have (P1)
- [ ] Smooth animations/transitions
- [ ] Geolocation support
- [ ] Loading and error states
- [ ] Wind direction compass animation

### Nice to Have (P2)
- [ ] Temperature unit toggle (°F/°C)
- [ ] Weather alerts
```

#### Step 2: Create Context Files (Optional but Recommended)

Create a `.context/` folder with additional context:

**`.context/api-reference.md`**
```markdown
# OpenWeatherMap API Reference

## Current Weather
```
GET https://api.openweathermap.org/data/2.5/weather
```

### Parameters
- `q` - City name (e.g., "Seattle" or "Seattle,US")
- `zip` - Zip code (e.g., "98101,US")
- `lat`, `lon` - Coordinates
- `appid` - API key (required)
- `units` - "imperial" for Fahrenheit

### Response Fields Used
```json
{
  "coord": { "lon": -122.33, "lat": 47.61 },
  "weather": [{ "main": "Clear", "description": "clear sky", "icon": "01d" }],
  "main": { 
    "temp": 72.5, 
    "feels_like": 71.2, 
    "humidity": 45,
    "pressure": 1015
  },
  "visibility": 10000,
  "wind": { "speed": 5.2, "deg": 180, "gust": 8.5 },
  "clouds": { "all": 20 },
  "sys": { "country": "US", "sunrise": 1700000000, "sunset": 1700040000 },
  "name": "Seattle"
}
```

## 5-Day Forecast
```
GET https://api.openweathermap.org/data/2.5/forecast
```
Returns `list` array with 3-hour intervals for 5 days (40 entries = 48 hours displayable).

## Air Pollution
```
GET https://api.openweathermap.org/data/2.5/air_pollution?lat={lat}&lon={lon}&appid={key}
```

### Response
```json
{
  "list": [{
    "main": { "aqi": 2 },
    "components": {
      "co": 201.94,
      "no2": 0.77,
      "o3": 68.66,
      "so2": 0.64,
      "pm2_5": 0.5,
      "pm10": 0.54
    }
  }]
}
```
AQI Scale: 1=Good, 2=Fair, 3=Moderate, 4=Poor, 5=Very Poor
```

**`.context/fluent-design-system.md`**
```markdown
# Microsoft Fluent 2.0 Design Tokens

## Colors
### Brand
- Primary: #0078D4 (Microsoft Blue)
- Primary Hover: #106EBE
- Primary Active: #005A9E

### Neutral
- Foreground 1: #242424
- Foreground 2: #616161
- Background 1: #FFFFFF
- Background 2: #FAFAFA
- Background 3: #F5F5F5
- Stroke 1: #D1D1D1

### Status
- Success: #107C10
- Warning: #FFB900
- Error: #D13438

## Typography
```css
font-family: 'Segoe UI Variable', 'Segoe UI', system-ui, sans-serif;
```

| Name | Size | Weight | Line Height |
|------|------|--------|-------------|
| Caption | 12px | 400 | 16px |
| Body | 14px | 400 | 20px |
| Body Large | 16px | 400 | 22px |
| Subtitle | 20px | 600 | 28px |
| Title | 28px | 600 | 36px |
| Display | 40px | 600 | 52px |

## Spacing
4px, 8px, 12px, 16px, 20px, 24px, 32px, 40px, 48px

## Border Radius
- Small: 4px
- Medium: 8px
- Large: 12px
- XLarge: 16px
- Circular: 50%

## Shadows (Elevation)
```css
--shadow2: 0 1px 2px rgba(0,0,0,0.14), 0 0 2px rgba(0,0,0,0.12);
--shadow4: 0 2px 4px rgba(0,0,0,0.14), 0 0 2px rgba(0,0,0,0.12);
--shadow8: 0 4px 8px rgba(0,0,0,0.14), 0 0 2px rgba(0,0,0,0.12);
--shadow16: 0 8px 16px rgba(0,0,0,0.14), 0 0 2px rgba(0,0,0,0.12);
--shadow28: 0 14px 28px rgba(0,0,0,0.24), 0 0 8px rgba(0,0,0,0.12);
--shadow64: 0 32px 64px rgba(0,0,0,0.24), 0 0 8px rgba(0,0,0,0.12);
```

## Motion
- Duration Fast: 100ms
- Duration Normal: 200ms
- Duration Slow: 300ms
- Easing: cubic-bezier(0.33, 0, 0.67, 1)
```

---

### Phase 2: Use Deep Planning (10 minutes)

Now let's use Cline's Deep Planning feature to create an implementation plan.

#### Step 1: Open Cline and Enable Plan Mode

In VS Code, open Cline and look for the "Plan" mode toggle (not "Act" mode).

#### Step 2: Provide Your Specification

Use this single prompt:

```
[PLAN MODE]
I need to build a weather application. Please read the SPEC.md file in this project.

The spec includes:
- Microsoft Fluent 2.0 design system
- 8 weather detail metrics
- 48-hour hourly forecast in Today/Tomorrow table layout
- Sun position arc visualization
- Air Quality Index card
- All OpenWeatherMap Free API endpoints

Please:
1. Analyze the complete specification
2. Create a detailed implementation plan
3. Identify the order of implementation

After planning, switch to ACT mode and implement the full application in one pass.
```

#### Step 3: Review the Plan

Cline should generate a comprehensive plan covering:
- [ ] HTML structure (all sections including sun position and AQI)
- [ ] CSS with Fluent 2.0 tokens
- [ ] JavaScript modules (API calls, display functions, utilities)
- [ ] Implementation order

**📊 Record the Plan:**
```
[Paste or summarize the generated plan here]




```

---

### Phase 3: Execute the Plan (15 minutes)

#### Single Execution (Recommended)

Let Cline execute the entire plan:

```
[ACT MODE]
The plan looks good. Please implement the complete weather application according to SPEC.md.
```

**⏱️ Start your timer!**

The goal is to see how quickly a well-specified app can be built compared to the iterative approach in Lab 1.

---

### Phase 4: Validation and Comparison (10 minutes)

#### Test Your Application

1. Open `index.html` in a browser (or use Live Server)
2. API key should already be configured from spec
3. Test all features:

**Core Features:**
- [ ] Search "Seattle" → weather displays
- [ ] Search "98101" → same location via zip
- [ ] Geolocation button works

**Weather Details (8 metrics):**
- [ ] Feels Like
- [ ] Humidity
- [ ] Wind Speed
- [ ] Wind Direction (compass)
- [ ] Pressure
- [ ] Cloudiness
- [ ] Visibility
- [ ] Wind Gusts

**Forecasts:**
- [ ] 5-day forecast with 72px icons
- [ ] 48-hour table with Today/Tomorrow columns
- [ ] "Now" highlighted in table

**Advanced Features:**
- [ ] Sun position arc shows current position
- [ ] Sunrise/sunset times display
- [ ] AQI card with color coding
- [ ] Pollutant breakdown displayed

**Design:**
- [ ] Fluent 2.0 styling (blue #0078D4)
- [ ] Proper shadows and border radius
- [ ] Responsive on mobile

#### Scorecard

Rate your result (same criteria as Lab 1):

| Criteria | Lab 1 Score | Lab 2 Score | Notes |
|----------|-------------|-------------|-------|
| **Functionality** | /5 | /5 | |
| **Completeness** | /5 | /5 | |
| **Design** | /5 | /5 | |
| **Code Quality** | /5 | /5 | |
| **UX** | /5 | /5 | |
| **TOTAL** | /25 | /25 | |

#### Metrics Comparison

| Metric | Lab 1 | Lab 2 |
|--------|-------|-------|
| Total prompts used | ~9 | |
| Spec writing time | N/A | |
| Implementation time | | |
| Total time (spec + impl) | | |
| Major bugs encountered | | |
| Features missing | | |

---

## 📊 Analysis

### The Key Comparison

**Lab 1 Journey:**
```
Prompt 1 → Basic app
Prompt 2 → API key
Prompt 3 → Fluent 2.0
Prompt 4 → 48-hour forecast
Prompt 5 → Table layout
Prompt 6 → Larger icons
Prompt 7 → Icon fix
Prompt 8 → What else?
Prompt 9 → Add everything (YOLO)
─────────────────────────────
Total: 9+ prompts, multiple context switches
```

**Lab 2 Journey:**
```
Write SPEC.md → 10 minutes
Prompt 1 → Plan (review)
Prompt 2 → Execute (full app)
─────────────────────────────
Total: 2 prompts + spec time
```

### What Improved?

```
[Write your observations here]
- First-time quality?
- Feature completeness?
- Design consistency?
- Code organization?

```

### What Was Different About the Experience?

```
[Write your observations here]
- Mental overhead?
- Confidence in output?
- Need for fixes?

```

### Were There Any Disadvantages to Specs?

```
[Write your observations here]
- Upfront time investment?
- Over-specification?
- Flexibility lost?

```

---

## 🔑 Key Takeaways

### The Power of Specifications

1. **Clarity reduces iteration** - AI knows exactly what to build
2. **Consistency is maintained** - Fluent 2.0 tokens ensure cohesion
3. **Requirements are explicit** - No assumptions about features
4. **Context is preserved** - Spec files persist across sessions
5. **Quality is measurable** - Acceptance criteria enable validation

### The ROI of Spec Writing

| Investment | Return |
|------------|--------|
| 10 min writing spec | Avoid 7+ iteration prompts |
| Fluent 2.0 tokens | Consistent, professional design |
| API reference | Correct integration first time |
| Acceptance criteria | Testable, verifiable output |

### When to Use Each Approach

| Approach | Best For |
|----------|----------|
| **Vibe Coding** | Exploration, prototypes, learning, small tasks |
| **Spec-Driven** | Production code, team projects, complex features, repeatable results |
| **Hybrid** | Start with vibe to explore, then spec what works |

---

## 🚀 Advanced: Using the Pre-Built Spec

For convenience, a complete specification is available at:

📄 **[specs/weather-app-spec.md](../specs/weather-app-spec.md)**

You can use this directly with Cline:

```
[PLAN MODE then ACT MODE]
Build the weather application defined in docs/specs/weather-app-spec.md
```

---

## ✅ Completion Checklist

Before the debrief:

- [ ] Created SPEC.md with all features from Lab 1
- [ ] Created context files (API reference, design system)
- [ ] Used Cline's Plan mode to review
- [ ] Generated the complete application in 1-2 prompts
- [ ] Tested all functionality matches Lab 1 output
- [ ] Compared metrics between labs
- [ ] Documented observations

---

## 💭 Discussion Questions for Debrief

1. **Iteration Count:** How many prompts did you use in each lab?
2. **Time Comparison:** Was total time (spec + implementation) less than vibe coding?
3. **Quality:** Was the spec-driven output more complete/less buggy?
4. **Code Organization:** How did code structure compare?
5. **Design Consistency:** Was Fluent 2.0 applied more consistently?
6. **Real World:** Would you use specs for your actual projects?
7. **Spec Investment:** What's the minimum spec that provides value?

---

*Next: [Lab 3 - MCP Server Development](./lab-03-mcp-servers.md)*
