# Pokémon Team Builder Application Specification

## Overview

Build a complete Pokémon team builder web application using HTML, CSS, and JavaScript. The application uses **PokéAPI** (free, no API key required) and implements **Microsoft Fluent 2.0 design system**.

### Target Files
```
pokemon-team-builder/
├── index.html    # Single-page application
├── styles.css    # Fluent 2.0 styling
├── app.js        # Application logic
└── README.md     # Setup instructions
```

---

## API Reference: PokéAPI

**Base URL**: `https://pokeapi.co/api/v2`

### Endpoints Used

1. Get Pokémon list by range:
   ```
   GET /pokemon?offset={offset}&limit={limit}
   Response: { results: [{ name, url }] }
   ```

2. Get Pokémon details:
   ```
   GET /pokemon/{name_or_id}
   Response: {
     id: number,
     name: string,
     height: number,
     weight: number,
     types: [{ type: { name: string } }],
     stats: [{ base_stat: number, stat: { name: string } }],
     abilities: [{ ability: { name: string }, is_hidden: boolean }],
     sprites: {
       front_default: string,
       front_shiny: string,
       other: {
         'official-artwork': { front_default: string }
       }
     },
     cries: { latest: string }
   }
   ```

3. Get type effectiveness:
   ```
   GET /type/{type_name}
   Response: {
     damage_relations: {
       double_damage_from: [{ name: string }],
       half_damage_from: [{ name: string }],
       no_damage_from: [{ name: string }],
       double_damage_to: [{ name: string }],
       half_damage_to: [{ name: string }],
       no_damage_to: [{ name: string }]
     }
   }
   ```

---

## Generation Data

Use these ranges for generation filtering:

```javascript
const GENERATIONS = {
  1: { name: 'Kanto', offset: 0, limit: 151 },
  2: { name: 'Johto', offset: 151, limit: 100 },
  3: { name: 'Hoenn', offset: 251, limit: 135 },
  4: { name: 'Sinnoh', offset: 386, limit: 107 },
  5: { name: 'Unova', offset: 493, limit: 156 },
  6: { name: 'Kalos', offset: 649, limit: 72 },
  7: { name: 'Alola', offset: 721, limit: 88 },
  8: { name: 'Galar', offset: 809, limit: 96 },
  9: { name: 'Paldea', offset: 905, limit: 105 }
};
```

---

## Type Colors (use exactly)

```javascript
const TYPE_COLORS = {
  normal: '#A8A878',
  fire: '#F08030',
  water: '#6890F0',
  electric: '#F8D030',
  grass: '#78C850',
  ice: '#98D8D8',
  fighting: '#C03028',
  poison: '#A040A0',
  ground: '#E0C068',
  flying: '#A890F0',
  psychic: '#F85888',
  bug: '#A8B820',
  rock: '#B8A038',
  ghost: '#705898',
  dragon: '#7038F8',
  dark: '#705848',
  steel: '#B8B8D0',
  fairy: '#EE99AC'
};
```

---

## Functional Requirements

### FR-1: Search & Browse

| ID | Requirement |
|----|-------------|
| FR-1.1 | Search input with real-time filtering (debounced 300ms) |
| FR-1.2 | Generation selector buttons (Gen 1-9) |
| FR-1.3 | Grid display of Pokémon cards showing: sprite, name, Pokédex number, type badges |
| FR-1.4 | Sprite image uses official artwork preferred, fallback to front_default |
| FR-1.5 | Name displayed capitalized |
| FR-1.6 | Pokédex number formatted as #001 |
| FR-1.7 | Type badges with correct colors |
| FR-1.8 | Loading spinner while fetching |
| FR-1.9 | "No results" message when search returns empty |

### FR-2: Pokémon Detail Modal

| ID | Requirement |
|----|-------------|
| FR-2.1 | Click Pokémon card to open modal |
| FR-2.2 | Large official artwork (300px height) |
| FR-2.3 | Shiny toggle button to switch to shiny sprite |
| FR-2.4 | Name and Pokédex number |
| FR-2.5 | Type badges |
| FR-2.6 | Base stats with progress bars (HP, Attack, Defense, Sp.Atk, Sp.Def, Speed) |
| FR-2.7 | Stats bars max value: 255 |
| FR-2.8 | Total base stats sum displayed |
| FR-2.9 | Height (convert from decimeters to m) |
| FR-2.10 | Weight (convert from hectograms to kg) |
| FR-2.11 | Abilities list (mark hidden ability with badge) |
| FR-2.12 | "Add to Team" button |
| FR-2.13 | "Compare" checkbox |
| FR-2.14 | "Play Cry" button (plays cries.latest audio) |
| FR-2.15 | Close button (X) |

### FR-3: Team Builder

| ID | Requirement |
|----|-------------|
| FR-3.1 | Team panel showing 6 slots (always visible) |
| FR-3.2 | Empty slots show placeholder |
| FR-3.3 | Filled slots show: small sprite, Pokémon name, type badges, remove button (X) |
| FR-3.4 | Team limit: 6 Pokémon |
| FR-3.5 | Cannot add duplicates (show warning toast) |
| FR-3.6 | Shows team's total base stat average |

### FR-4: Type Effectiveness Analysis

| ID | Requirement |
|----|-------------|
| FR-4.1 | Calculate and display for current team |
| FR-4.2 | Show Weaknesses (types that deal 2x to team members) |
| FR-4.3 | Show Resistances (types that deal 0.5x) |
| FR-4.4 | Show Immunities (types that deal 0x) |
| FR-4.5 | Show Coverage Gaps (types where team has no resistance) |

#### Calculation Rules for Dual-Types:
- Multiply effectiveness values
- 2x × 2x = 4x (double weakness - highlight red)
- 2x × 0.5x = 1x (neutral)
- 2x × 0x = 0x (immunity wins)
- 0.5x × 0.5x = 0.25x (double resistance)

### FR-5: Multiple Teams

| ID | Requirement |
|----|-------------|
| FR-5.1 | "Save Team" button prompts for team name |
| FR-5.2 | Saved teams list in sidebar |
| FR-5.3 | Click saved team to load it |
| FR-5.4 | Delete button for saved teams |
| FR-5.5 | All teams stored in localStorage |
| FR-5.6 | Maximum 10 saved teams |

### FR-6: Stat Comparison

| ID | Requirement |
|----|-------------|
| FR-6.1 | Compare button/checkbox on Pokémon cards |
| FR-6.2 | Select 2-4 Pokémon for comparison |
| FR-6.3 | Comparison view shows side-by-side: sprites, stats bars overlaid, stat values table |
| FR-6.4 | Highlight highest stat in each category (green) |
| FR-6.5 | Highlight lowest stat in each category (red) |
| FR-6.6 | "Clear comparison" button |

### FR-7: Utility Features

| ID | Requirement |
|----|-------------|
| FR-7.1 | "Random Team" button: fills team with 6 random Pokémon from current generation |
| FR-7.2 | LocalStorage persistence for: current team, saved teams, last selected generation |
| FR-7.3 | Error handling with user-friendly messages |
| FR-7.4 | Responsive design (mobile-friendly) |

---

## Non-Functional Requirements

### NFR-1: Microsoft Fluent 2.0 Design System

#### Color Tokens
```css
:root {
  --brand-primary: #0078D4;
  --brand-primary-hover: #106EBE;
  --brand-primary-active: #005A9E;
  --neutral-background-1: #FFFFFF;
  --neutral-background-2: #FAFAFA;
  --neutral-background-3: #F5F5F5;
  --neutral-foreground-1: #242424;
  --neutral-foreground-2: #616161;
  --neutral-foreground-3: #9E9E9E;
  --neutral-stroke-1: #D1D1D1;
  --neutral-stroke-2: #E0E0E0;
  --status-danger: #D13438;
  --status-warning: #FFB900;
  --status-success: #107C10;
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
| Body 1 | 14px | 400 |
| Body 2 | 12px | 400 |
| Caption | 11px | 400 |

#### Spacing (use consistently)
```css
--spacing-xs: 4px;
--spacing-s: 8px;
--spacing-m: 12px;
--spacing-l: 16px;
--spacing-xl: 20px;
--spacing-xxl: 24px;
--spacing-xxxl: 32px;
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

**Buttons - Primary:**
- Background: var(--brand-primary)
- Color: white
- Border: none
- Padding: 8px 16px
- Border-radius: var(--radius-m)
- Hover: var(--brand-primary-hover)
- Active: var(--brand-primary-active)
- Transition: all 200ms ease

**Buttons - Secondary:**
- Background: transparent
- Color: var(--brand-primary)
- Border: 1px solid var(--brand-primary)

**Buttons - Icon:**
- Width/Height: 32px
- Border-radius: var(--radius-circular)
- Background: transparent
- Hover: var(--neutral-background-3)

**Cards:**
- Background: var(--neutral-background-1)
- Border-radius: var(--radius-l)
- Box-shadow: var(--shadow-4)
- Padding: var(--spacing-l)
- Hover: transform translateY(-2px), box-shadow var(--shadow-8)
- Transition: all 200ms ease

**Input:**
- Border: 1px solid var(--neutral-stroke-1)
- Border-radius: var(--radius-m)
- Padding: 8px 12px
- Font-size: 14px
- Focus: border-color var(--brand-primary), outline none

**Modal:**
- Backdrop: rgba(0,0,0,0.4)
- Content: background white, border-radius var(--radius-xl), box-shadow var(--shadow-28)
- Max-width: 600px
- Max-height: 90vh
- Overflow: auto

**Toast Notifications:**
- Position: fixed bottom-right
- Background: var(--neutral-background-1)
- Box-shadow: var(--shadow-16)
- Border-radius: var(--radius-m)
- Padding: 12px 16px
- Auto-dismiss: 3 seconds
- Types: success (green left border), warning (yellow), error (red)

**Progress Bar (for stats):**
- Height: 8px
- Background: var(--neutral-background-3)
- Border-radius: var(--radius-s)
- Fill: gradient based on stat value

---

## Stat Bar Colors

```javascript
function getStatColor(value) {
  if (value < 50) return '#D13438';      // Red - poor
  if (value < 80) return '#FFB900';      // Yellow - average
  if (value < 100) return '#107C10';     // Green - good
  return '#0078D4';                       // Blue - excellent
}
```

---

## HTML Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Pokémon Team Builder</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <div class="app">
    <!-- Header -->
    <header class="header">
      <div class="logo">
        <svg class="pokeball-icon">...</svg>
        <h1>Pokémon Team Builder</h1>
      </div>
      <button class="random-team-btn">Random Team</button>
    </header>

    <!-- Main Content -->
    <main class="main-content">
      <!-- Sidebar with Team -->
      <aside class="sidebar">
        <section class="team-panel">
          <h2>My Team</h2>
          <div class="team-stats">
            <span>Avg Stats: <strong id="team-avg">0</strong></span>
          </div>
          <div class="team-slots" id="team-slots">
            <!-- 6 slots rendered by JS -->
          </div>
          <div class="team-actions">
            <button class="save-team-btn">Save Team</button>
            <button class="clear-team-btn">Clear</button>
          </div>
        </section>

        <section class="type-effectiveness">
          <h3>Type Analysis</h3>
          <div class="effectiveness-chart" id="effectiveness-chart">
            <!-- Rendered by JS -->
          </div>
        </section>

        <section class="saved-teams">
          <h3>Saved Teams</h3>
          <ul class="saved-teams-list" id="saved-teams-list">
            <!-- Rendered by JS -->
          </ul>
        </section>
      </aside>

      <!-- Pokédex Section -->
      <section class="pokedex">
        <div class="search-bar">
          <input type="text" id="search-input" placeholder="Search Pokémon...">
        </div>
        
        <div class="generation-selector">
          <!-- Gen buttons 1-9 rendered by JS -->
        </div>

        <div class="pokemon-grid" id="pokemon-grid">
          <!-- Pokémon cards rendered by JS -->
        </div>

        <div class="loading-spinner" id="loading-spinner" hidden>
          <div class="spinner"></div>
          <span>Loading...</span>
        </div>
      </section>
    </main>

    <!-- Compare Panel (hidden by default) -->
    <div class="compare-panel" id="compare-panel" hidden>
      <h3>Compare Pokémon</h3>
      <div class="compare-grid" id="compare-grid">
        <!-- Rendered by JS -->
      </div>
      <button class="clear-compare-btn">Clear Comparison</button>
    </div>

    <!-- Pokémon Detail Modal -->
    <div class="modal-backdrop" id="modal-backdrop" hidden>
      <div class="modal" id="pokemon-modal">
        <button class="modal-close-btn" aria-label="Close">&times;</button>
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
    currentGeneration: 1,
    pokemonList: [],
    currentTeam: [],
    savedTeams: [],
    compareList: [],
    typeEffectivenessCache: {}
  },

  // Initialize app
  async init() {
    this.loadFromStorage();
    this.renderGenerationButtons();
    this.renderTeamSlots();
    this.renderSavedTeams();
    this.setupEventListeners();
    await this.loadGeneration(this.state.currentGeneration);
  },

  // API calls
  async fetchPokemonList(offset, limit) {},
  async fetchPokemonDetails(nameOrId) {},
  async fetchTypeEffectiveness(typeName) {},

  // Rendering
  renderGenerationButtons() {},
  renderPokemonGrid(pokemonList) {},
  renderPokemonCard(pokemon) {},
  renderTeamSlots() {},
  renderTypeEffectiveness() {},
  renderCompareView() {},
  renderPokemonModal(pokemon) {},
  renderSavedTeams() {},

  // Team management
  addToTeam(pokemon) {},
  removeFromTeam(pokemonId) {},
  clearTeam() {},
  saveTeam(teamName) {},
  loadTeam(teamIndex) {},
  deleteTeam(teamIndex) {},
  generateRandomTeam() {},

  // Type effectiveness calculation
  async calculateTeamEffectiveness() {},
  getTypeMultiplier(attackType, defenseTypes) {},

  // Comparison
  addToCompare(pokemon) {},
  removeFromCompare(pokemonId) {},
  clearCompare() {},

  // Utility
  debounce(func, wait) {},
  showToast(message, type) {},
  formatNumber(num) {},
  capitalizeFirst(str) {},
  showLoading() {},
  hideLoading() {},

  // Storage
  saveToStorage() {},
  loadFromStorage() {},

  // Event handlers
  setupEventListeners() {}
};

document.addEventListener('DOMContentLoaded', () => App.init());
```

---

## Error Handling

- Wrap all fetch calls in try/catch
- Show toast notification on API errors
- Retry failed requests once after 1 second
- Show "Failed to load" message in grid on persistent errors
- Never leave UI in broken state

---

## Responsive Breakpoints

```css
@media (max-width: 1024px) {
  /* Sidebar moves to top */
  /* Grid becomes 3 columns */
}

@media (max-width: 768px) {
  /* Grid becomes 2 columns */
  /* Modal full width */
}

@media (max-width: 480px) {
  /* Grid single column */
  /* Reduce font sizes */
  /* Stack team slots 2x3 */
}
```

---

## Accessibility

- All buttons have aria-labels
- Modal traps focus
- Escape key closes modal
- High contrast type badges (white text on color backgrounds)
- Focus indicators on interactive elements
- Semantic HTML structure

---

## Pokeball Icon SVG

```html
<svg viewBox="0 0 100 100" width="32" height="32">
  <circle cx="50" cy="50" r="48" fill="#f00" stroke="#000" stroke-width="4"/>
  <rect x="2" y="48" width="96" height="8" fill="#000"/>
  <circle cx="50" cy="50" r="48" fill="#fff" clip-path="inset(50% 0 0 0)"/>
  <circle cx="50" cy="50" r="20" fill="#fff" stroke="#000" stroke-width="4"/>
  <circle cx="50" cy="50" r="10" fill="#fff" stroke="#000" stroke-width="4"/>
</svg>
```

---

## Acceptance Criteria

### Must Have (P0)
- [ ] Generation buttons load Pokémon
- [ ] Search filters results in real-time
- [ ] Clicking card opens detail modal
- [ ] Stats show as proportional bars
- [ ] Type badges have correct colors (18 types)
- [ ] "Add to Team" adds Pokémon to team panel
- [ ] Can't add duplicates (toast warning)
- [ ] Can remove Pokémon from team
- [ ] Type effectiveness updates for team
- [ ] LocalStorage persistence for current team
- [ ] Fluent 2.0 design tokens applied

### Should Have (P1)
- [ ] "Save Team" stores team with custom name
- [ ] Saved teams can be loaded
- [ ] Compare feature shows side-by-side stats
- [ ] "Random Team" fills with 6 random Pokémon
- [ ] Shiny toggle works in modal
- [ ] Play Cry plays audio

### Nice to Have (P2)
- [ ] Works on mobile viewport
- [ ] Multiple saved teams management
- [ ] Team stat average display

---

## Testing Checklist

### API Tests
- [ ] Loading Gen 1 returns 151 Pokémon
- [ ] Search "Pikachu" finds correct result
- [ ] Pokémon details load with stats
- [ ] Type effectiveness data loads

### Team Tests
- [ ] Can add 6 Pokémon to team
- [ ] Cannot add 7th Pokémon
- [ ] Duplicate prevention works
- [ ] Remove button removes Pokémon
- [ ] Team persists after refresh

### Type Effectiveness Tests
- [ ] Single-type calculations correct
- [ ] Dual-type multiplications correct
- [ ] Immunity (0x) overrides weakness
- [ ] 4x weakness highlighted

### Design Tests
- [ ] Brand color (#0078D4) used correctly
- [ ] Type colors match specification
- [ ] Cards have proper shadow and hover lift
- [ ] Stat bars proportional to 255 max
- [ ] Smooth 200ms transitions
