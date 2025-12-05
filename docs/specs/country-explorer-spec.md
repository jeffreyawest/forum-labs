# Country Explorer Application Specification

## Overview

Build a complete country explorer web application using HTML, CSS, and JavaScript. The application uses **REST Countries API** (free, no API key required) and implements **Microsoft Fluent 2.0 design system**.

### Target Files
```
country-explorer/
├── index.html    # Single-page application
├── styles.css    # Fluent 2.0 styling
├── app.js        # Application logic
└── README.md     # Setup instructions
```

---

## API Reference: REST Countries

**Base URL**: `https://restcountries.com/v3.1`

### Endpoints Used

1. Get all countries:
   ```
   GET /all
   Response: Array of country objects
   ```

2. Get countries by name:
   ```
   GET /name/{name}
   Response: Array of matching countries
   ```

3. Get countries by region:
   ```
   GET /region/{region}
   Regions: Africa, Americas, Asia, Europe, Oceania
   Response: Array of countries in that region
   ```

4. Get country by code:
   ```
   GET /alpha/{code}
   Response: Array with single country (use code cca3)
   ```

### Country Object Structure

```javascript
{
  name: {
    common: "United States",
    official: "United States of America"
  },
  cca2: "US",
  cca3: "USA",
  capital: ["Washington, D.C."],
  region: "Americas",
  subregion: "North America",
  population: 329484123,
  area: 9833520,
  languages: { eng: "English" },
  currencies: { USD: { name: "US Dollar", symbol: "$" } },
  borders: ["CAN", "MEX"],
  flags: {
    svg: "https://...",
    png: "https://..."
  },
  maps: {
    googleMaps: "https://...",
    openStreetMaps: "https://..."
  },
  timezones: ["UTC-12:00", "UTC-11:00", ...],
  car: { side: "right" },
  coatOfArms: { svg: "https://..." },
  latlng: [38, -97]
}
```

---

## Region Data

```javascript
const REGIONS = {
  Africa: { count: 59, emoji: '🌍' },
  Americas: { count: 57, emoji: '🌎' },
  Asia: { count: 50, emoji: '🌏' },
  Europe: { count: 53, emoji: '🏰' },
  Oceania: { count: 27, emoji: '🏝️' }
};
```

---

## Functional Requirements

### FR-1: Browse & Search

| ID | Requirement |
|----|-------------|
| FR-1.1 | Load all countries on initial page load |
| FR-1.2 | Search input with real-time filtering (debounced 300ms) |
| FR-1.3 | Grid display of country cards showing: flag, name, population, region, capital |
| FR-1.4 | Population formatted with locale |
| FR-1.5 | Loading spinner while fetching |
| FR-1.6 | "No countries found" message when search returns empty |

### FR-2: Region Filter

| ID | Requirement |
|----|-------------|
| FR-2.1 | Dropdown filter with options: All Regions, Africa, Americas, Asia, Europe, Oceania |
| FR-2.2 | Use /region/{region} endpoint for filtering (more efficient) |
| FR-2.3 | Search works within filtered region |

### FR-3: Sorting

| ID | Requirement |
|----|-------------|
| FR-3.1 | Sort dropdown with options: Name (A-Z), Name (Z-A), Population (High to Low), Population (Low to High), Area (Largest), Area (Smallest) |
| FR-3.2 | Default: Name (A-Z) |
| FR-3.3 | Instant re-sorting on change |

### FR-4: Country Detail Modal

| ID | Requirement |
|----|-------------|
| FR-4.1 | Click country card to open modal |
| FR-4.2 | Large flag (200px height) |
| FR-4.3 | Official name and common name |
| FR-4.4 | Native name (from name.nativeName, first entry) |
| FR-4.5 | Capital city |
| FR-4.6 | Region and subregion |
| FR-4.7 | Population (formatted with locale string) |
| FR-4.8 | Area in km² (formatted) |
| FR-4.9 | Languages (comma-separated values from object) |
| FR-4.10 | Currencies (formatted as "Name (Symbol)") |
| FR-4.11 | Timezones (first 3, then "+X more" if more) |
| FR-4.12 | Driving side (car.side) |
| FR-4.13 | Border countries as clickable buttons |
| FR-4.14 | Click border button loads that country's detail |
| FR-4.15 | If no borders, show "Island nation - no land borders" |
| FR-4.16 | Google Maps link (opens in new tab) |
| FR-4.17 | Coat of Arms (if available) |
| FR-4.18 | "Add to Bucket List" button (heart icon) |
| FR-4.19 | "Mark as Visited" button (checkmark icon) |
| FR-4.20 | Close button |

### FR-5: Bucket List

| ID | Requirement |
|----|-------------|
| FR-5.1 | Sidebar panel showing "Bucket List" |
| FR-5.2 | Countries user wants to visit |
| FR-5.3 | Each entry shows: flag (small), country name, "Move to Visited" button, "Remove" button |
| FR-5.4 | Save to localStorage |
| FR-5.5 | Show count: "X countries" |

### FR-6: Visited Countries

| ID | Requirement |
|----|-------------|
| FR-6.1 | Sidebar panel showing "Visited" |
| FR-6.2 | Countries user has visited |
| FR-6.3 | Each entry shows: flag (small), country name, "Remove" button |
| FR-6.4 | Save to localStorage |
| FR-6.5 | Show count: "X countries" |

### FR-7: State Rules

| ID | Requirement |
|----|-------------|
| FR-7.1 | A country can be in bucket list OR visited, NOT both |
| FR-7.2 | Adding to visited auto-removes from bucket list |
| FR-7.3 | Visual indicator on cards: heart filled = bucket list, checkmark = visited, both hollow = neither |

### FR-8: Statistics Dashboard

| ID | Requirement |
|----|-------------|
| FR-8.1 | Collapsible statistics panel |
| FR-8.2 | Display Total Visited: X / 250 (with progress bar) |
| FR-8.3 | Display Total Bucket List: X countries |
| FR-8.4 | Regional breakdown (only for visited): Africa X/59, Americas X/57, Asia X/50, Europe X/53, Oceania X/27 |
| FR-8.5 | Each region with mini progress bar |
| FR-8.6 | Most recent visited country |
| FR-8.7 | Percentage of world explored |

### FR-9: Country Comparison

| ID | Requirement |
|----|-------------|
| FR-9.1 | "Compare" checkbox on country cards |
| FR-9.2 | Select 2-4 countries |
| FR-9.3 | Comparison panel shows: flags in row, population bar chart (horizontal, proportional), area bar chart |
| FR-9.4 | Table comparison: capital, region, languages, currencies, population (highlight highest), area (highlight largest) |
| FR-9.5 | "Clear Comparison" button |

### FR-10: Additional Features

| ID | Requirement |
|----|-------------|
| FR-10.1 | "Random Country" button in header |
| FR-10.2 | "Share Stats" button copies text summary to clipboard |
| FR-10.3 | Dark mode toggle (persisted in localStorage) |
| FR-10.4 | "Explore Neighbors" in detail modal - shows all bordering countries |

---

## Non-Functional Requirements

### NFR-1: Microsoft Fluent 2.0 Design System

#### Colors (Light Mode)
```css
:root {
  --brand-primary: #0078D4;
  --brand-primary-hover: #106EBE;
  --brand-primary-active: #005A9E;
  --neutral-background-1: #FFFFFF;
  --neutral-background-2: #FAFAFA;
  --neutral-background-3: #F5F5F5;
  --neutral-background-4: #F0F0F0;
  --neutral-foreground-1: #242424;
  --neutral-foreground-2: #616161;
  --neutral-foreground-3: #9E9E9E;
  --neutral-stroke-1: #D1D1D1;
  --neutral-stroke-2: #E0E0E0;
  --status-danger: #D13438;
  --status-warning: #FFB900;
  --status-success: #107C10;
  --status-visited: #107C10;
  --status-bucket: #D13438;
}
```

#### Colors (Dark Mode)
```css
[data-theme="dark"] {
  --neutral-background-1: #1F1F1F;
  --neutral-background-2: #2D2D2D;
  --neutral-background-3: #383838;
  --neutral-background-4: #424242;
  --neutral-foreground-1: #FFFFFF;
  --neutral-foreground-2: #D1D1D1;
  --neutral-foreground-3: #9E9E9E;
  --neutral-stroke-1: #4D4D4D;
  --neutral-stroke-2: #383838;
}
```

#### Typography
```css
font-family: 'Segoe UI Variable', 'Segoe UI', system-ui, sans-serif;
```

| Role | Size | Weight |
|------|------|--------|
| Display | 40px | 600 |
| Title 1 | 28px | 600 |
| Title 2 | 24px | 600 |
| Title 3 | 20px | 600 |
| Subtitle | 18px | 600 |
| Body 1 | 14px | 400 |
| Body 2 | 12px | 400 |
| Caption | 11px | 400 |

#### Spacing
```css
--spacing-xs: 4px;
--spacing-s: 8px;
--spacing-m: 12px;
--spacing-l: 16px;
--spacing-xl: 20px;
--spacing-xxl: 24px;
--spacing-xxxl: 32px;
--spacing-xxxxl: 48px;
```

#### Shadows
```css
--shadow-2: 0 1px 2px rgba(0,0,0,0.14);
--shadow-4: 0 2px 4px rgba(0,0,0,0.14);
--shadow-8: 0 4px 8px rgba(0,0,0,0.14);
--shadow-16: 0 8px 16px rgba(0,0,0,0.14);
--shadow-28: 0 14px 28px rgba(0,0,0,0.14);
```

#### Border Radius
```css
--radius-s: 4px;
--radius-m: 8px;
--radius-l: 12px;
--radius-xl: 16px;
--radius-circular: 50%;
```

#### Component Specifications

**Country Card:**
- Background: var(--neutral-background-1)
- Border: 1px solid var(--neutral-stroke-2)
- Border-radius: var(--radius-l)
- Box-shadow: var(--shadow-4)
- Overflow: hidden
- Hover: transform translateY(-4px), box-shadow var(--shadow-8)
- Transition: all 200ms ease
- Flag takes full width at top (aspect ratio preserved)
- Content padding: var(--spacing-l)
- Bucket list indicator: heart icon top-right corner
- Visited indicator: checkmark badge

**Input Fields:**
- Height: 40px
- Border: 1px solid var(--neutral-stroke-1)
- Border-radius: var(--radius-m)
- Padding: 0 12px
- Font-size: 14px
- Focus: border-color var(--brand-primary), box-shadow: 0 0 0 2px rgba(0, 120, 212, 0.2)
- Placeholder color: var(--neutral-foreground-3)

**Buttons - Primary:**
- Background: var(--brand-primary)
- Color: white
- Border: none
- Padding: 8px 16px
- Border-radius: var(--radius-m)
- Font-weight: 600
- Hover: var(--brand-primary-hover)
- Active: var(--brand-primary-active)
- Transition: all 200ms ease

**Buttons - Secondary:**
- Background: transparent
- Color: var(--brand-primary)
- Border: 1px solid var(--brand-primary)

**Buttons - Ghost:**
- Background: transparent
- Color: var(--neutral-foreground-1)
- Border: none
- Hover: background var(--neutral-background-3)

**Buttons - Icon:**
- Width/Height: 36px
- Border-radius: var(--radius-circular)
- Display: flex, align-items center, justify-content center
- Background: transparent
- Hover: background var(--neutral-background-3)

**Modal:**
- Backdrop: rgba(0,0,0,0.4) with backdrop-filter: blur(4px)
- Content: background var(--neutral-background-1), border-radius var(--radius-xl)
- Box-shadow: var(--shadow-28)
- Max-width: 700px
- Max-height: 90vh
- Overflow-y: auto
- Animation: fade in + scale up 200ms

**Sidebar:**
- Width: 300px
- Background: var(--neutral-background-2)
- Border-left: 1px solid var(--neutral-stroke-2)
- Padding: var(--spacing-l)
- Sections separated by dividers

**Progress Bar:**
- Height: 8px
- Background: var(--neutral-background-4)
- Border-radius: var(--radius-s)
- Fill: var(--brand-primary)
- Transition: width 300ms ease

**Toast Notifications:**
- Position: fixed bottom 24px right 24px
- Background: var(--neutral-background-1)
- Box-shadow: var(--shadow-16)
- Border-radius: var(--radius-m)
- Padding: 12px 16px
- Min-width: 280px
- Success: left border 3px solid var(--status-success)
- Error: left border 3px solid var(--status-danger)
- Auto-dismiss: 3 seconds

---

## HTML Structure

```html
<!DOCTYPE html>
<html lang="en" data-theme="light">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Country Explorer</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <div class="app">
    <!-- Header -->
    <header class="header">
      <div class="header-left">
        <span class="logo">🌍</span>
        <h1>Country Explorer</h1>
      </div>
      <div class="header-right">
        <button class="random-btn" aria-label="Random Country">
          🎲 Random
        </button>
        <button class="theme-toggle" aria-label="Toggle Theme">
          🌙
        </button>
      </div>
    </header>

    <!-- Main Content -->
    <main class="main">
      <!-- Controls Bar -->
      <div class="controls">
        <div class="search-wrapper">
          <input type="text" id="search" placeholder="Search for a country...">
          <span class="search-icon">🔍</span>
        </div>
        <select id="region-filter">
          <option value="">All Regions</option>
          <option value="Africa">Africa</option>
          <option value="Americas">Americas</option>
          <option value="Asia">Asia</option>
          <option value="Europe">Europe</option>
          <option value="Oceania">Oceania</option>
        </select>
        <select id="sort-select">
          <option value="name-asc">Name (A-Z)</option>
          <option value="name-desc">Name (Z-A)</option>
          <option value="pop-desc">Population (High)</option>
          <option value="pop-asc">Population (Low)</option>
          <option value="area-desc">Area (Largest)</option>
          <option value="area-asc">Area (Smallest)</option>
        </select>
      </div>

      <!-- Content Layout -->
      <div class="content-layout">
        <!-- Country Grid -->
        <section class="country-grid-container">
          <div class="country-grid" id="country-grid">
            <!-- Country cards rendered by JS -->
          </div>
          <div class="loading" id="loading" hidden>
            <div class="spinner"></div>
            <p>Loading countries...</p>
          </div>
          <div class="empty-state" id="empty-state" hidden>
            <span class="empty-icon">🔍</span>
            <p>No countries found</p>
          </div>
        </section>

        <!-- Sidebar -->
        <aside class="sidebar">
          <!-- Statistics Section -->
          <section class="stats-section">
            <div class="section-header">
              <h2>📊 Statistics</h2>
              <button class="share-btn" aria-label="Share Stats">📋</button>
            </div>
            <div class="stats-content">
              <div class="stat-main">
                <span class="stat-label">World Explored</span>
                <div class="stat-value" id="total-visited">0 / 250</div>
                <div class="progress-bar">
                  <div class="progress-fill" id="total-progress"></div>
                </div>
                <span class="stat-percent" id="total-percent">0%</span>
              </div>
              <div class="stat-regions" id="region-stats">
                <!-- Rendered by JS -->
              </div>
            </div>
          </section>

          <!-- Bucket List Section -->
          <section class="bucket-section">
            <div class="section-header">
              <h2>❤️ Bucket List</h2>
              <span class="count" id="bucket-count">0</span>
            </div>
            <ul class="country-list" id="bucket-list">
              <!-- Rendered by JS -->
            </ul>
          </section>

          <!-- Visited Section -->
          <section class="visited-section">
            <div class="section-header">
              <h2>✅ Visited</h2>
              <span class="count" id="visited-count">0</span>
            </div>
            <ul class="country-list" id="visited-list">
              <!-- Rendered by JS -->
            </ul>
          </section>
        </aside>
      </div>
    </main>

    <!-- Compare Panel (hidden by default) -->
    <div class="compare-panel" id="compare-panel" hidden>
      <div class="compare-header">
        <h3>Compare Countries</h3>
        <button class="clear-compare-btn">Clear</button>
      </div>
      <div class="compare-content" id="compare-content">
        <!-- Rendered by JS -->
      </div>
    </div>

    <!-- Country Detail Modal -->
    <div class="modal-backdrop" id="modal-backdrop" hidden>
      <div class="modal" id="country-modal">
        <button class="modal-close" aria-label="Close">&times;</button>
        <div class="modal-content" id="modal-content">
          <!-- Rendered by JS -->
        </div>
      </div>
    </div>

    <!-- Toast Container -->
    <div class="toast-container" id="toast-container"></div>
  </div>

  <script src="app.js"></script>
</body>
</html>
```

---

## JavaScript Architecture

```javascript
const App = {
  state: {
    countries: [],
    filteredCountries: [],
    bucketList: [],        // Array of country cca3 codes
    visited: [],           // Array of country cca3 codes
    compareList: [],       // Array of country objects (max 4)
    currentRegion: '',
    currentSort: 'name-asc',
    searchQuery: '',
    theme: 'light'
  },

  // Initialize app
  async init() {
    this.loadFromStorage();
    this.applyTheme();
    this.setupEventListeners();
    await this.loadAllCountries();
    this.renderStats();
    this.renderBucketList();
    this.renderVisitedList();
  },

  // API methods
  async loadAllCountries() {},
  async loadCountriesByRegion(region) {},
  async getCountryByCode(code) {},

  // Data transformation helpers
  formatPopulation(num) {
    return num.toLocaleString();
  },
  formatArea(num) {
    return num.toLocaleString() + ' km²';
  },
  getLanguages(langObj) {
    if (!langObj) return 'N/A';
    return Object.values(langObj).join(', ');
  },
  getCurrencies(currObj) {
    if (!currObj) return 'N/A';
    return Object.values(currObj)
      .map(c => `${c.name} (${c.symbol || '-'})`)
      .join(', ');
  },
  getNativeName(nameObj) {
    if (!nameObj?.nativeName) return null;
    const first = Object.values(nameObj.nativeName)[0];
    return first?.common || first?.official;
  },

  // Filtering and sorting
  filterCountries() {},
  sortCountries(countries) {},
  handleSearch(query) {},
  handleRegionChange(region) {},
  handleSortChange(sortKey) {},

  // Rendering
  renderCountryGrid() {},
  renderCountryCard(country) {},
  renderCountryModal(country) {},
  async renderBorderCountries(borders) {},
  renderStats() {},
  renderBucketList() {},
  renderVisitedList() {},
  renderComparePanel() {},

  // List management
  addToBucketList(country) {},
  removeFromBucketList(code) {},
  markAsVisited(country) {},
  removeFromVisited(code) {},
  isInBucketList(code) {},
  isVisited(code) {},

  // Comparison
  addToCompare(country) {},
  removeFromCompare(code) {},
  clearCompare() {},

  // Utilities
  debounce(func, wait) {},
  showToast(message, type) {},
  showLoading() {},
  hideLoading() {},
  generateShareText() {},
  copyToClipboard(text) {},

  // Random feature
  showRandomCountry() {},

  // Theme
  toggleTheme() {},
  applyTheme() {},

  // Storage
  saveToStorage() {},
  loadFromStorage() {},

  // Event handlers
  setupEventListeners() {},

  // Modal
  openModal(content) {},
  closeModal() {}
};

document.addEventListener('DOMContentLoaded', () => App.init());
```

---

## Error Handling

- Wrap all fetch calls in try/catch
- Show toast notification on API errors: "Failed to load countries. Please try again."
- Show "No countries found" empty state when search returns no results
- Handle missing data gracefully with fallbacks
- Never leave UI in broken state

---

## Responsive Breakpoints

```css
@media (max-width: 1200px) {
  /* Sidebar collapses to bottom panel */
  /* Grid 3 columns */
}

@media (max-width: 768px) {
  /* Grid 2 columns */
  /* Modal full width */
  /* Stack controls vertically */
}

@media (max-width: 480px) {
  /* Grid 1 column */
  /* Reduce card size */
  /* Simplified stats */
}
```

---

## Accessibility Requirements

- All interactive elements have aria-labels
- Modal traps focus when open
- Escape key closes modal
- Focus indicators on all interactive elements
- High contrast for text on images (text shadow on flag)
- Semantic HTML structure
- Support for keyboard navigation

---

## Animation Specifications

- Card hover: transform translateY(-4px) 200ms ease
- Modal open: opacity 0→1, transform scale(0.95→1) 200ms ease
- Toast enter: slideInRight 200ms, exit: fadeOut 200ms
- Progress bar: width change 300ms ease
- Theme transition: all colors 200ms ease
- Loading spinner: rotate 1s linear infinite

---

## localStorage Keys

```javascript
'countryExplorer_bucketList': // JSON array of cca3 codes
'countryExplorer_visited':    // JSON array of cca3 codes  
'countryExplorer_theme':      // 'light' or 'dark'
```

---

## Share Text Format

When user clicks "Share Stats", copy this format:

```
🌍 My Country Explorer Stats
✈️ Visited: X / 250 countries (X%)
❤️ Bucket List: X countries
🌍 Africa: X/59 | 🌎 Americas: X/57 | 🌏 Asia: X/50
🏰 Europe: X/53 | 🏝️ Oceania: X/27
Explore your world at countryexplorer.app
```

---

## Acceptance Criteria

### Must Have (P0)
- [ ] Countries load on page open
- [ ] Search filters in real-time
- [ ] Region filter works
- [ ] Sorting options work
- [ ] Clicking card opens detail modal
- [ ] Flag displays correctly
- [ ] Languages formatted correctly
- [ ] Currencies formatted correctly
- [ ] Border countries are clickable
- [ ] Add to bucket list works
- [ ] Mark as visited works
- [ ] Can't be in both lists
- [ ] LocalStorage persistence
- [ ] Fluent 2.0 design tokens applied

### Should Have (P1)
- [ ] Statistics update correctly
- [ ] Regional breakdown shows progress
- [ ] Compare feature works
- [ ] Random country button works
- [ ] Dark mode toggle works
- [ ] Google Maps link opens new tab
- [ ] Share stats copies to clipboard

### Nice to Have (P2)
- [ ] Works on mobile viewport
- [ ] Data persists on refresh
- [ ] Animation specifications met

---

## Testing Checklist

### API Tests
- [ ] All countries load (250 total)
- [ ] Search "United" finds relevant results
- [ ] Region filter returns correct countries
- [ ] Country code lookup works

### List Tests
- [ ] Add country to bucket list
- [ ] Move country to visited
- [ ] Remove from visited
- [ ] Can't add to both lists
- [ ] Lists persist after refresh

### Data Formatting Tests
- [ ] Languages show correctly (Object.values)
- [ ] Currencies show with symbol
- [ ] Population formatted with commas
- [ ] Border countries show names, not codes

### Design Tests
- [ ] Brand color (#0078D4) used correctly
- [ ] Cards have proper shadow and hover lift
- [ ] Dark mode colors apply
- [ ] Smooth 200ms transitions
- [ ] Focus outlines visible
