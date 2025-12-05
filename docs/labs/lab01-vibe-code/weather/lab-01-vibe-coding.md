# Lab 1: Vibe Coding - The Iterative Approach

## 🎯 Objective

Build a Weather Lookup application using only high-level, conversational prompts. Experience firsthand how "vibe coding" (iterative prompting without specifications) requires more effort to achieve a polished result.

**Time:** 45 minutes

---

## Learning Goals

By the end of this lab, you will:
- ✅ Experience iterative AI-assisted development
- ✅ Understand the challenges of unstructured prompting
- ✅ Track the number of iterations needed to reach your goal
- ✅ Identify gaps that specifications could fill

---

## The Challenge

**Your Goal:** Create a weather application that:
- Shows temperature for a given city or zip code
- Uses HTML, CSS, and JavaScript
- Looks professional and polished (Microsoft Fluent 2.0)
- Has all the features you'd expect from a weather app

**The Catch:** You can only use high-level, conversational prompts. No detailed specifications allowed!

---

## Setup

### Prerequisites
- VS Code with GitHub Copilot and/or Cline installed
- A new empty folder for your project
- OpenWeatherMap API Key (provided below)

### API Key
Use this OpenWeatherMap API key for the lab:
```
81208750b50a113806b890f45520281a
```

### Create Your Workspace
```bash
mkdir weather-app-vibe
cd weather-app-vibe
code .
```

---

## 📝 Lab Instructions

### Phase 1: Initial Prompt (5 minutes)

Start with a simple, high-level prompt in Cline (use **PLAN mode** first):

#### Step 1 - The Opening Prompt
```
[PLAN MODE]
I want a weather app that shows the temperature for a given city or zip code.
```

**Expected Response:** The AI should ask clarifying questions like:

> I'd like to build this weather app for you. To create something that meets your needs, I have a few clarifying questions:
>
> 1. **Platform**: What type of app would you like?
>    - Web app (HTML/CSS/JavaScript)
>    - Desktop app
>    - Command-line tool
>    - Mobile app
>
> 2. **Weather Data Source**: Do you have a preferred weather API?
>
> 3. **Features**: Besides temperature, would you like any additional information?
>    - Weather conditions (sunny, cloudy, rain)
>    - Humidity
>    - Wind speed
>    - Forecast (daily/hourly)
>
> 4. **Design**: Any preferences for the look and feel?

#### Your Answers:
```
- Web app (HTML/CSS/JavaScript)
- Choose your datasource
- All features
- Make it look good
```

**📊 Track Your Progress:**

| Metric | Value |
|--------|-------|
| Iteration # | 1 |
| Time spent | |
| Files created | |
| What's missing? | |

**🤔 Reflection Questions:**
- Did the AI ask clarifying questions, or just build something?
- What assumptions did it make?
- Does it work? Does it look good?

---

### Phase 2: Iterative Refinement (20 minutes)

Now iterate to improve what was generated. Follow these steps:

#### Step 2 - Add the API Key
```
[ACT MODE]
Add OpenWeatherMap API Key: 
```

#### Step 3 - Improve the Design
```
[ACT MODE]
Make the UI Microsoft Fluent 2.0
```

**Expected Result:** The AI should apply Fluent 2.0 design principles:
- Colors: Microsoft brand blue (#0078D4), neutral grays
- Typography: Segoe UI Variable font with Fluent type scale
- Spacing: 4/8/12/16/20/24/32px scale
- Border Radius: Fluent corners (4/8/12/16px)
- Elevation: Fluent shadow tokens (shadow-2 through shadow-64)
- Proper hover, active, and focus states
- Accessibility: Focus-visible outlines, high contrast mode support

#### Step 4 - Add Hourly Forecast
```
[ACT MODE]
Add an hourly forecast for the next 48 hours
```

**Expected Result:** Scrollable hourly forecast with:
- "Now" indicator highlighted in Microsoft blue
- Left/right scroll buttons for navigation
- Weather icons and temperatures per hour
- Smooth horizontal scrolling

#### Step 5 - Refine the Layout
```
[ACT MODE]
Make the 48 hour forecast be a table with the rest of today on the left, and tomorrow on the right.
```

**Expected Result:** Two-column table layout:
- **Left column (Today):** Remaining hours with "Now" indicator
- **Right column (Tomorrow):** Full forecast with date header
- Each row: Time, icon, description, temperature

#### Step 6 - Visual Tweaks
```
[ACT MODE]
Make the icons/conditions picture in the 5-day forecast larger
```

> **Note:** This might not work on the first try!

#### Step 7 - Follow-up Fix
```
[ACT MODE]
They look the same size
```

**Expected Result:** Higher resolution @4x images (100x100 native) displayed at 72x72px

---

### Phase 3: Expand Features (15 minutes)

#### Step 8 - Discover Available Features
```
[PLAN MODE]
What else can I add to the page that is available on the OpenWeatherMap free API tier?
```

**Expected Response:** The AI should list available features:

**From Current Weather API (already fetched but not displayed):**
- Pressure (hPa)
- Cloudiness (%)
- Sunrise/Sunset times
- Wind direction (degrees → compass)
- Wind gusts

**New API Endpoints (Free Tier):**
- Air Pollution API (`/data/2.5/air_pollution`)
  - Air Quality Index (AQI)
  - CO, NO, NO2, O3, SO2, PM2.5, PM10 levels
- Geocoding API (better city search)

**UI Enhancement Ideas:**
- Sun position indicator (arc visualization)
- Day/Night mode auto-switch
- Wind compass visualization

#### Step 9 - Add Everything!
```
[ACT MODE]
Add all of it. Use your best judgement how to do it. YOLO!
```

**Expected Result:** Full-featured weather app with:

1. **Expanded Weather Details (8 metrics):**
   - Feels Like, Humidity, Wind Speed, Wind Direction (rotating compass icon)
   - Pressure (hPa), Cloudiness (%), Visibility, Wind Gusts

2. **Sun Position Card:**
   - Visual arc showing sun's current position in the sky
   - Sunrise and sunset times
   - Total daylight hours calculation
   - Sun dims when below horizon (night time)

3. **Air Quality Index (AQI) Card:**
   - Color-coded rating (Good/Fair/Moderate/Poor/Very Poor)
   - Individual pollutant readings: PM2.5, PM10, O₃, NO₂, SO₂, CO
   - Gradient backgrounds based on air quality level

**📊 Update Your Tracking:**

| Step # | What you asked for | What you got | Issues/Gaps |
|--------|-------------------|--------------|-------------|
| 1 | Weather app | Clarifying questions | |
| 2 | API key | Configured | |
| 3 | Fluent 2.0 UI | Design update | |
| 4 | 48-hour forecast | Scrollable list | |
| 5 | Table layout | Two columns | |
| 6 | Larger icons | No change? | |
| 7 | Fix icons | Higher res images | |
| 8 | What else? | Feature list | |
| 9 | Add all | Full features | |

---

### Phase 4: Final Assessment (5 minutes)

#### Scorecard

Rate your final result (1-5 scale):

| Criteria | Score (1-5) | Notes |
|----------|-------------|-------|
| **Functionality** - Does it work? | | |
| **Completeness** - All features present? | | |
| **Design** - Does it look good? | | |
| **Code Quality** - Is code organized? | | |
| **UX** - Loading, errors, edge cases? | | |
| **TOTAL** | /25 | |

#### Metrics Summary

| Metric | Value |
|--------|-------|
| Total prompts used | ~9 |
| Total time spent | |
| Major bugs encountered | |
| Features still missing | |

---

## 🎯 Target Features Checklist

Compare your result to this feature list:

### Core Features
- [ ] Search by city name
- [ ] Search by zip code
- [ ] Current temperature display
- [ ] Weather condition (sunny, cloudy, etc.)
- [ ] Weather icon

### Extended Features
- [ ] Feels-like temperature
- [ ] Humidity percentage
- [ ] Wind speed & direction
- [ ] Visibility
- [ ] Pressure (hPa)
- [ ] Cloudiness (%)
- [ ] Wind gusts

### Forecast Features
- [ ] 5-day forecast with icons
- [ ] 48-hour hourly forecast
- [ ] Today/Tomorrow split view table

### Advanced Features
- [ ] Sun position arc visualization
- [ ] Sunrise/sunset times
- [ ] Daylight hours calculation
- [ ] Air Quality Index (AQI)
- [ ] Pollutant breakdown (PM2.5, PM10, O₃, NO₂, SO₂, CO)

### Design Features
- [ ] Microsoft Fluent 2.0 design system
- [ ] Responsive layout
- [ ] Loading states
- [ ] Error handling
- [ ] Accessibility (focus states, high contrast)

---

## 💡 Observations to Record

### What Worked Well?
```
[Write your observations here]
- PLAN mode helped the AI ask clarifying questions
- "YOLO" prompt let the AI make good decisions
- Incremental refinement was possible



```

### What Was Frustrating?
```
[Write your observations here]
- Icon size didn't change on first try
- Had to switch between PLAN and ACT modes
- Context about previous changes sometimes lost



```

### How Many "Back and Forth" Iterations?
```
[Write your count and notes here]
- 9 main prompts
- 1 follow-up fix (icons)
- Could have been more with other issues



```

### What Would You Do Differently?
```
[Write your thoughts here]
- Start with a complete spec document?
- Define Fluent 2.0 design tokens upfront?
- List all desired features before starting?



```

---

## 🔑 Key Takeaways

### The Vibe Coding Experience

1. **PLAN mode helps** - The AI asks clarifying questions when you let it
2. **Iteration is still needed** - 9+ prompts to get to the final result
3. **"YOLO" can work** - Letting the AI make decisions sometimes works well
4. **Fixes require context** - "They look the same size" needs prior context
5. **Mode switching matters** - PLAN for discovery, ACT for implementation

### The Hidden Costs of Vibe Coding

| Cost | Description |
|------|-------------|
| **Time** | 9 prompts × context switching = significant overhead |
| **Quality** | Results depend on AI's interpretation of vague requests |
| **Context** | AI might forget earlier requirements |
| **Consistency** | Design may drift across iterations |

### What We Built (Summary)

| Feature | Prompts Required |
|---------|------------------|
| Basic weather app | 1-2 |
| Fluent 2.0 design | 1 |
| Hourly forecast | 1 |
| Table layout | 1 |
| Icon fixes | 2 |
| Advanced features (AQI, sun position) | 2 |
| **Total** | **~9** |

---

## 🚀 Preview of Lab 2

In the next lab, you'll build the **exact same application** using:

- ✅ A detailed specification document with all features defined upfront
- ✅ Design system tokens (Fluent 2.0) pre-specified
- ✅ API integration details documented
- ✅ Cline's Deep Planning feature
- ✅ One-shot or minimal iteration approach

**Hypothesis:** With proper specs and context, you'll achieve the same (or better) result in **1-2 prompts** instead of 9+.

---

## 📚 Reference

### OpenWeatherMap API Endpoints Used

| Endpoint | Purpose |
|----------|---------|
| `/data/2.5/weather` | Current weather + sunrise/sunset |
| `/data/2.5/forecast` | 5-day/3-hour forecast (48 hours of data) |
| `/data/2.5/air_pollution` | Air quality data (AQI, pollutants) |

### Sample Follow-up Prompts

If you want to keep iterating:

```
Add a temperature unit toggle (°F/°C)
```

```
Add weather alerts if available
```

```
Make it a Progressive Web App (PWA)
```

```
Add dark mode support
```

```
Add city search autocomplete using the Geocoding API
```

### Troubleshooting

| Issue | Try This |
|-------|----------|
| API not working | "The API call is failing, can you debug it?" |
| Design looks off | "The Fluent 2.0 styling seems inconsistent, can you review?" |
| Features missing | "I expected X but don't see it, can you add it?" |
| Layout broken | "The two-column layout isn't working on mobile" |

---

## ✅ Completion Checklist

Before moving to Lab 2:

- [ ] Completed all 9 steps (or your own variation)
- [ ] Recorded your metrics and observations
- [ ] Have a working weather app with:
  - [ ] Microsoft Fluent 2.0 design
  - [ ] 48-hour forecast in table layout
  - [ ] Sun position visualization
  - [ ] Air quality index display
- [ ] Saved your code for comparison
- [ ] Reflected on the iterative experience

**💾 Save your work in a folder called `weather-app-vibe` for comparison later!**

---

*Next: [Lab 2 - Agentic Coding with Specs](lab-02-spec-driven.md)*
