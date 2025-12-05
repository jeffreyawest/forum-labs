# Meal Planner Application Specification

## Overview

Build a complete meal planning web application using vanilla HTML, CSS, and JavaScript. The application uses **TheMealDB API** (free, no key required) and implements **Microsoft Fluent 2.0 design system**.

### Target Files
```
meal-planner/
├── index.html    # Single-page application
├── styles.css    # Fluent 2.0 styling
├── app.js        # Application logic
└── README.md     # Setup instructions
```

---

## API Reference: TheMealDB

**Base URL**: `https://www.themealdb.com/api/json/v1/1`

### Endpoints Used

| Endpoint | Purpose | Example |
|----------|---------|---------|
| `/search.php?s={name}` | Search by meal name | `/search.php?s=chicken` |
| `/filter.php?c={category}` | Filter by category | `/filter.php?c=Seafood` |
| `/lookup.php?i={id}` | Get full meal details | `/lookup.php?i=52772` |
| `/random.php` | Get random meal | `/random.php` |
| `/categories.php` | List all categories | `/categories.php` |

### Response Structure

**Search/Lookup Response** (`meals` array):
```javascript
{
  idMeal: "52772",
  strMeal: "Teriyaki Chicken",
  strCategory: "Chicken",
  strArea: "Japanese",
  strInstructions: "...",
  strMealThumb: "https://www.themealdb.com/images/media/meals/...",
  strIngredient1: "Chicken", strMeasure1: "500g",
  strIngredient2: "Soy Sauce", strMeasure2: "2 tbsp",
  // ... up to strIngredient20/strMeasure20
}
```

**Filter Response** (partial data, requires lookup for details):
```javascript
{
  idMeal: "52772",
  strMeal: "Teriyaki Chicken",
  strMealThumb: "https://..."
}
```

### Important Notes
- Filter endpoint returns minimal data; use `lookup.php` to get full details including ingredients
- Ingredients are in `strIngredient1` through `strIngredient20` (empty string if unused)
- Measures are in `strMeasure1` through `strMeasure20`
- Images can be resized: append `/preview` for thumbnails

---

## Functional Requirements

### FR-1: Recipe Search

| ID | Requirement |
|----|-------------|
| FR-1.1 | Text input for searching recipes by name |
| FR-1.2 | Search triggers on button click and Enter key |
| FR-1.3 | Display results as cards in a responsive grid |
| FR-1.4 | Each card shows: thumbnail (150x150), meal name, category badge |
| FR-1.5 | Clicking a recipe card opens a detail modal or expands for assignment |
| FR-1.6 | Show "No results found" message when search returns empty |
| FR-1.7 | Show loading spinner during API calls |

### FR-2: Category Browsing

| ID | Requirement |
|----|-------------|
| FR-2.1 | Sidebar shows all categories from `/categories.php` |
| FR-2.2 | Each category shows name and meal count |
| FR-2.3 | Clicking category filters recipes using `/filter.php?c={category}` |
| FR-2.4 | "All Recipes" option clears category filter |
| FR-2.5 | Active category visually highlighted (brand color background) |

### FR-3: Weekly Calendar

| ID | Requirement |
|----|-------------|
| FR-3.1 | Display 7-day grid (Monday through Sunday) |
| FR-3.2 | Show current week with dates (e.g., "Mon 2", "Tue 3") |
| FR-3.3 | Today's column highlighted with brand color header |
| FR-3.4 | Each day has 3 slots: Breakfast, Lunch, Dinner |
| FR-3.5 | Empty slots show dashed border with "+" icon |
| FR-3.6 | Filled slots show meal thumbnail (40x40) and name |
| FR-3.7 | Hover on filled slot reveals "×" remove button |
| FR-3.8 | Week navigation buttons (previous/next week) |
| FR-3.9 | "Today" button jumps to current week |

### FR-4: Meal Assignment

| ID | Requirement |
|----|-------------|
| FR-4.1 | Click recipe card to select it for assignment |
| FR-4.2 | Then click an empty calendar slot to assign |
| FR-4.3 | Visual indicator when a recipe is selected (border glow) |
| FR-4.4 | Cancel selection by clicking elsewhere or pressing Escape |
| FR-4.5 | Alternatively: drag recipe card to calendar slot |
| FR-4.6 | When assigning from filter results, fetch full meal details via lookup |

### FR-5: Shopping List

| ID | Requirement |
|----|-------------|
| FR-5.1 | Right panel displays aggregated shopping list |
| FR-5.2 | Parse all ingredients from planned meals (strIngredient1-20) |
| FR-5.3 | Combine duplicates intelligently (e.g., "Chicken" appears once with combined quantity) |
| FR-5.4 | Group ingredients by category: Proteins, Produce, Dairy, Pantry, Spices, Other |
| FR-5.5 | Each item has checkbox to mark as purchased |
| FR-5.6 | Checked items show strikethrough and move to bottom of category |
| FR-5.7 | Show item count badge in panel header (e.g., "12 items") |
| FR-5.8 | "Clear Checked" button removes purchased items |
| FR-5.9 | "Copy List" button copies plain text to clipboard |
| FR-5.10 | List updates automatically when meals added/removed |

### FR-6: Favorites System

| ID | Requirement |
|----|-------------|
| FR-6.1 | Heart icon on each recipe card (empty/filled state) |
| FR-6.2 | Click heart to toggle favorite status |
| FR-6.3 | Favorites section in sidebar below categories |
| FR-6.4 | Show up to 10 recent favorites with small thumbnails |
| FR-6.5 | Click favorite to select for calendar assignment |
| FR-6.6 | Favorites persist in localStorage |

### FR-7: Random Recipe

| ID | Requirement |
|----|-------------|
| FR-7.1 | "🎲 Random" button in header or main area |
| FR-7.2 | Fetches from `/random.php` endpoint |
| FR-7.3 | Displays result prominently (can be added to calendar) |
| FR-7.4 | Optional: "Feeling Lucky" fills entire week with random meals |

### FR-8: Data Persistence

| ID | Requirement |
|----|-------------|
| FR-8.1 | Meal plan saves to localStorage on every change |
| FR-8.2 | Key: `mealPlanner_weekPlan` |
| FR-8.3 | Favorites save to localStorage |
| FR-8.4 | Key: `mealPlanner_favorites` |
| FR-8.5 | Shopping list checkbox state saves to localStorage |
| FR-8.6 | Key: `mealPlanner_shoppingChecked` |
| FR-8.7 | All data loads on page initialization |
| FR-8.8 | "Clear Week" button resets current week's meals |

### FR-9: Application States

| ID | Requirement |
|----|-------------|
| FR-9.1 | Loading state: Spinner with "Loading..." text |
| FR-9.2 | Empty state: Welcome message with search prompt |
| FR-9.3 | Error state: Error message with retry button |
| FR-9.4 | Success state: Recipe grid displayed |
| FR-9.5 | Only one state visible at a time in main content area |

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
    --colorBrandForeground: #0078D4;
    
    /* Neutral */
    --colorNeutralForeground1: #242424;
    --colorNeutralForeground2: #616161;
    --colorNeutralForeground3: #707070;
    --colorNeutralForegroundDisabled: #BDBDBD;
    --colorNeutralBackground1: #FFFFFF;
    --colorNeutralBackground2: #FAFAFA;
    --colorNeutralBackground3: #F5F5F5;
    --colorNeutralBackground4: #F0F0F0;
    --colorNeutralStroke1: #D1D1D1;
    --colorNeutralStroke2: #E0E0E0;
    
    /* Status */
    --colorStatusSuccess: #107C10;
    --colorStatusSuccessBackground: #DFF6DD;
    --colorStatusWarning: #FFB900;
    --colorStatusWarningBackground: #FFF4CE;
    --colorStatusDanger: #D13438;
    --colorStatusDangerBackground: #FDE7E9;
    
    /* Category Colors (for badges) */
    --colorSeafood: #0078D4;
    --colorChicken: #FFB900;
    --colorBeef: #D13438;
    --colorVegetarian: #107C10;
    --colorDessert: #881798;
    --colorPasta: #FF8C00;
    --colorPork: #E3008C;
    --colorLamb: #8E562E;
}
```

#### Typography
```css
font-family: 'Segoe UI Variable', 'Segoe UI', system-ui, -apple-system, sans-serif;
```

| Role | Size | Weight | Line Height |
|------|------|--------|-------------|
| Caption | 12px | 400 | 16px |
| Body | 14px | 400 | 20px |
| Body Strong | 14px | 600 | 20px |
| Body Large | 16px | 400 | 22px |
| Subtitle | 20px | 600 | 28px |
| Title | 28px | 600 | 36px |

#### Spacing Scale
```
4px, 8px, 12px, 16px, 20px, 24px, 32px, 40px, 48px
```

#### Border Radius
| Token | Value | Usage |
|-------|-------|-------|
| Small | 4px | Buttons, inputs, small elements |
| Medium | 8px | Cards, containers |
| Large | 12px | Panels, modals |
| Circular | 50% | Avatars, icon buttons |

#### Shadows (Elevation)
```css
--shadow2: 0 1px 2px rgba(0,0,0,0.14), 0 0 2px rgba(0,0,0,0.12);
--shadow4: 0 2px 4px rgba(0,0,0,0.14), 0 0 2px rgba(0,0,0,0.12);
--shadow8: 0 4px 8px rgba(0,0,0,0.14), 0 0 2px rgba(0,0,0,0.12);
--shadow16: 0 8px 16px rgba(0,0,0,0.14), 0 0 2px rgba(0,0,0,0.12);
--shadow28: 0 14px 28px rgba(0,0,0,0.24), 0 0 8px rgba(0,0,0,0.12);
```

#### Transitions
```css
--transitionFast: 100ms ease;
--transitionNormal: 200ms cubic-bezier(0.33, 0, 0.67, 1);
--transitionSlow: 300ms cubic-bezier(0.33, 0, 0.67, 1);
```

#### Component States
| State | Visual Change |
|-------|---------------|
| Hover | Background shifts one shade, cards lift (translateY -2px, shadow increases) |
| Active | Background darkens, transform scale(0.98) |
| Focus | 2px solid outline with brand color, 2px offset |
| Disabled | 40% opacity, cursor: not-allowed |

### NFR-2: Layout Structure

```
┌────────────────────────────────────────────────────────────────┐
│  HEADER: Logo, Search, Random Button, Settings                 │
├──────────────┬─────────────────────────────┬───────────────────┤
│              │                             │                   │
│   SIDEBAR    │      MAIN CONTENT           │   RIGHT PANEL     │
│   280px      │      flex: 1                │   320px           │
│              │                             │                   │
│  Categories  │   Week Calendar (top)       │   Shopping List   │
│  Filters     │   Recipe Grid (bottom)      │   Nutrition       │
│  Favorites   │                             │   (optional)      │
│              │                             │                   │
└──────────────┴─────────────────────────────┴───────────────────┘
```

### NFR-3: Responsive Breakpoints

| Breakpoint | Width | Adjustments |
|------------|-------|-------------|
| Desktop | > 1200px | Full 3-panel layout |
| Tablet | 768-1200px | Collapsible sidebar, 2-panel |
| Mobile | < 768px | Single column, bottom nav, swipeable calendar |

#### Mobile Specific
- Sidebar becomes slide-out drawer
- Shopping list becomes modal overlay
- Calendar scrolls horizontally
- Recipe cards stack in 1-2 columns

### NFR-4: Accessibility

| Requirement |
|-------------|
| All interactive elements focusable via keyboard |
| Focus-visible outlines (2px brand color) |
| ARIA labels on icon-only buttons |
| Role attributes on custom components |
| Color contrast meets WCAG AA (4.5:1) |
| prefers-reduced-motion: respect user preference |
| Screen reader announcements for state changes |

### NFR-5: Performance

| Requirement |
|-------------|
| Debounce search input (300ms) |
| Cache API responses in memory (5 min TTL) |
| Lazy load images (loading="lazy") |
| Minimize DOM reflows during list updates |
| No external dependencies (vanilla JS only) |

---

## HTML Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Meal Planner</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="app-container">
        <!-- Header -->
        <header class="header">
            <div class="header-left">
                <div class="logo">🍽️ <span>Meal Planner</span></div>
                <div class="search-box">
                    <span class="search-icon">🔍</span>
                    <input type="text" id="searchInput" placeholder="Search recipes...">
                </div>
            </div>
            <div class="header-actions">
                <button id="randomBtn" class="btn btn-secondary">🎲 Random</button>
                <button id="clearWeekBtn" class="btn btn-secondary">🗑️ Clear Week</button>
            </div>
        </header>

        <!-- Sidebar -->
        <aside class="sidebar" id="sidebar">
            <section class="sidebar-section">
                <h3 class="sidebar-title">Categories</h3>
                <ul id="categoryList" class="category-list">
                    <!-- Populated by JS -->
                </ul>
            </section>
            
            <section class="sidebar-section">
                <h3 class="sidebar-title">⭐ Favorites</h3>
                <div id="favoritesList" class="favorites-list">
                    <!-- Populated by JS -->
                </div>
            </section>
        </aside>

        <!-- Main Content -->
        <main class="main-content">
            <!-- Calendar Section -->
            <section class="calendar-section">
                <div class="calendar-header">
                    <h2 class="section-title">Weekly Meal Plan</h2>
                    <div class="week-nav">
                        <button id="prevWeekBtn" class="btn-icon">◀</button>
                        <span id="weekLabel" class="week-label">Dec 2 - 8, 2025</span>
                        <button id="nextWeekBtn" class="btn-icon">▶</button>
                        <button id="todayBtn" class="btn btn-secondary">Today</button>
                    </div>
                </div>
                <div id="calendarGrid" class="calendar-grid">
                    <!-- 7 day columns populated by JS -->
                </div>
            </section>

            <!-- Recipe Results Section -->
            <section class="recipes-section">
                <h2 class="section-title">Recipes</h2>
                
                <div id="loadingState" class="state-container hidden">
                    <div class="spinner"></div>
                    <p>Loading recipes...</p>
                </div>
                
                <div id="emptyState" class="state-container">
                    <p>🍳 Search for recipes or browse by category</p>
                </div>
                
                <div id="errorState" class="state-container hidden">
                    <p id="errorMessage">Something went wrong</p>
                    <button id="retryBtn" class="btn btn-primary">Retry</button>
                </div>
                
                <div id="recipeGrid" class="recipe-grid hidden">
                    <!-- Recipe cards populated by JS -->
                </div>
            </section>
        </main>

        <!-- Right Panel - Shopping List -->
        <aside class="right-panel" id="rightPanel">
            <div class="panel-header">
                <h3 class="panel-title">🛒 Shopping List</h3>
                <span id="itemCount" class="item-count">0 items</span>
            </div>
            
            <div id="shoppingList" class="shopping-list">
                <!-- Grouped ingredients populated by JS -->
            </div>
            
            <div class="panel-actions">
                <button id="clearCheckedBtn" class="btn btn-secondary">Clear Checked</button>
                <button id="copyListBtn" class="btn btn-primary">📋 Copy List</button>
            </div>
        </aside>
    </div>

    <!-- Selected Recipe Indicator (for assignment mode) -->
    <div id="selectionIndicator" class="selection-indicator hidden">
        <span>Click a calendar slot to add: </span>
        <strong id="selectedMealName"></strong>
        <button id="cancelSelectionBtn" class="btn-icon">✕</button>
    </div>

    <script src="app.js"></script>
</body>
</html>
```

---

## JavaScript Architecture

```javascript
// ================================================================
// CONFIGURATION & CONSTANTS
// ================================================================
const API_BASE = 'https://www.themealdb.com/api/json/v1/1';
const STORAGE_KEYS = {
    weekPlan: 'mealPlanner_weekPlan',
    favorites: 'mealPlanner_favorites',
    shoppingChecked: 'mealPlanner_shoppingChecked'
};
const INGREDIENT_CATEGORIES = {
    proteins: ['chicken', 'beef', 'pork', 'fish', 'salmon', 'shrimp', 'lamb', 'turkey', 'bacon', 'sausage', 'egg'],
    produce: ['onion', 'garlic', 'tomato', 'pepper', 'carrot', 'celery', 'lettuce', 'spinach', 'broccoli', 'mushroom', 'potato', 'lemon', 'lime', 'ginger', 'avocado'],
    dairy: ['milk', 'cheese', 'butter', 'cream', 'yogurt', 'sour cream'],
    pantry: ['flour', 'sugar', 'rice', 'pasta', 'oil', 'vinegar', 'soy sauce', 'bread', 'stock', 'broth'],
    spices: ['salt', 'pepper', 'paprika', 'cumin', 'oregano', 'basil', 'thyme', 'cinnamon', 'chili']
};
const DAYS = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday'];
const MEALS = ['Breakfast', 'Lunch', 'Dinner'];

// ================================================================
// STATE
// ================================================================
let state = {
    currentWeekStart: getMonday(new Date()),
    weekPlan: {},           // { 'YYYY-MM-DD': { Breakfast: meal, Lunch: meal, Dinner: meal } }
    favorites: [],          // Array of meal objects
    shoppingChecked: {},    // { 'ingredient': true }
    selectedMeal: null,     // Meal object waiting for calendar assignment
    categories: [],         // From API
    activeCategory: null,
    recipes: [],            // Current search/filter results
    mealCache: {},          // { mealId: fullMealObject }
    isLoading: false,
    error: null
};

// ================================================================
// DOM REFERENCES
// ================================================================
const elements = {
    searchInput: document.getElementById('searchInput'),
    randomBtn: document.getElementById('randomBtn'),
    clearWeekBtn: document.getElementById('clearWeekBtn'),
    categoryList: document.getElementById('categoryList'),
    favoritesList: document.getElementById('favoritesList'),
    calendarGrid: document.getElementById('calendarGrid'),
    weekLabel: document.getElementById('weekLabel'),
    prevWeekBtn: document.getElementById('prevWeekBtn'),
    nextWeekBtn: document.getElementById('nextWeekBtn'),
    todayBtn: document.getElementById('todayBtn'),
    recipeGrid: document.getElementById('recipeGrid'),
    loadingState: document.getElementById('loadingState'),
    emptyState: document.getElementById('emptyState'),
    errorState: document.getElementById('errorState'),
    errorMessage: document.getElementById('errorMessage'),
    retryBtn: document.getElementById('retryBtn'),
    shoppingList: document.getElementById('shoppingList'),
    itemCount: document.getElementById('itemCount'),
    clearCheckedBtn: document.getElementById('clearCheckedBtn'),
    copyListBtn: document.getElementById('copyListBtn'),
    selectionIndicator: document.getElementById('selectionIndicator'),
    selectedMealName: document.getElementById('selectedMealName'),
    cancelSelectionBtn: document.getElementById('cancelSelectionBtn')
};

// ================================================================
// API FUNCTIONS
// ================================================================
async function searchMeals(query) { /* /search.php?s={query} */ }
async function filterByCategory(category) { /* /filter.php?c={category} */ }
async function getMealById(id) { /* /lookup.php?i={id} - use cache */ }
async function getRandomMeal() { /* /random.php */ }
async function getCategories() { /* /categories.php */ }

// ================================================================
// RENDER FUNCTIONS
// ================================================================
function renderCategories() { /* Sidebar category list */ }
function renderFavorites() { /* Sidebar favorites */ }
function renderCalendar() { /* 7-day grid with meal slots */ }
function renderRecipes() { /* Recipe cards grid */ }
function renderShoppingList() { /* Aggregated ingredients */ }
function renderStates() { /* Show/hide loading/empty/error/content */ }

// ================================================================
// EVENT HANDLERS
// ================================================================
function handleSearch(e) { /* Debounced search */ }
function handleCategoryClick(category) { /* Filter by category */ }
function handleRecipeClick(meal) { /* Select for assignment */ }
function handleSlotClick(date, mealType) { /* Assign selected meal */ }
function handleRemoveMeal(date, mealType) { /* Remove from calendar */ }
function handleFavoriteToggle(meal) { /* Add/remove favorite */ }
function handleWeekNavigation(direction) { /* Prev/next week */ }
function handleShoppingCheck(ingredient) { /* Toggle checked */ }
function handleClearWeek() { /* Reset current week */ }
function handleCopyList() { /* Copy to clipboard */ }
function handleCancelSelection() { /* Cancel meal selection */ }

// ================================================================
// UTILITY FUNCTIONS
// ================================================================
function getMonday(date) { /* Get Monday of week */ }
function formatDate(date) { /* YYYY-MM-DD */ }
function formatDisplayDate(date) { /* Mon 2 */ }
function parseIngredients(meal) { /* Extract strIngredient1-20 */ }
function categorizeIngredient(name) { /* Match to category */ }
function aggregateIngredients(meals) { /* Combine duplicates */ }
function debounce(fn, delay) { /* Debounce helper */ }

// ================================================================
// STORAGE FUNCTIONS
// ================================================================
function saveToStorage(key, data) { /* localStorage.setItem */ }
function loadFromStorage(key) { /* localStorage.getItem + parse */ }
function loadAllData() { /* Load weekPlan, favorites, shoppingChecked */ }
function saveWeekPlan() { /* Persist week plan */ }
function saveFavorites() { /* Persist favorites */ }
function saveShoppingChecked() { /* Persist checked items */ }

// ================================================================
// INITIALIZATION
// ================================================================
async function init() {
    loadAllData();
    await getCategories();
    renderCategories();
    renderFavorites();
    renderCalendar();
    renderShoppingList();
    setupEventListeners();
}

function setupEventListeners() {
    // Search
    elements.searchInput.addEventListener('input', debounce(handleSearch, 300));
    elements.searchInput.addEventListener('keypress', (e) => e.key === 'Enter' && handleSearch());
    
    // Week navigation
    elements.prevWeekBtn.addEventListener('click', () => handleWeekNavigation(-1));
    elements.nextWeekBtn.addEventListener('click', () => handleWeekNavigation(1));
    elements.todayBtn.addEventListener('click', () => { state.currentWeekStart = getMonday(new Date()); renderCalendar(); });
    
    // Actions
    elements.randomBtn.addEventListener('click', handleRandomMeal);
    elements.clearWeekBtn.addEventListener('click', handleClearWeek);
    elements.clearCheckedBtn.addEventListener('click', handleClearChecked);
    elements.copyListBtn.addEventListener('click', handleCopyList);
    elements.cancelSelectionBtn.addEventListener('click', handleCancelSelection);
    elements.retryBtn.addEventListener('click', handleRetry);
    
    // Keyboard
    document.addEventListener('keydown', (e) => e.key === 'Escape' && handleCancelSelection());
}

document.addEventListener('DOMContentLoaded', init);
```

---

## Ingredient Categorization Logic

```javascript
function categorizeIngredient(ingredientName) {
    const name = ingredientName.toLowerCase();
    
    for (const [category, keywords] of Object.entries(INGREDIENT_CATEGORIES)) {
        if (keywords.some(keyword => name.includes(keyword))) {
            return category;
        }
    }
    return 'other';
}

function aggregateIngredients(meals) {
    const ingredientMap = {};
    
    meals.forEach(meal => {
        for (let i = 1; i <= 20; i++) {
            const ingredient = meal[`strIngredient${i}`];
            const measure = meal[`strMeasure${i}`];
            
            if (ingredient && ingredient.trim()) {
                const key = ingredient.toLowerCase().trim();
                if (!ingredientMap[key]) {
                    ingredientMap[key] = {
                        name: ingredient.trim(),
                        measures: [],
                        category: categorizeIngredient(ingredient)
                    };
                }
                if (measure && measure.trim()) {
                    ingredientMap[key].measures.push(measure.trim());
                }
            }
        }
    });
    
    return Object.values(ingredientMap);
}
```

---

## Shopping List Rendering

```javascript
function renderShoppingList() {
    // Get all meals from current week
    const plannedMeals = [];
    const weekDates = getWeekDates(state.currentWeekStart);
    
    weekDates.forEach(date => {
        const dateStr = formatDate(date);
        const dayPlan = state.weekPlan[dateStr] || {};
        MEALS.forEach(mealType => {
            if (dayPlan[mealType]) {
                plannedMeals.push(dayPlan[mealType]);
            }
        });
    });
    
    // Aggregate ingredients
    const ingredients = aggregateIngredients(plannedMeals);
    
    // Group by category
    const grouped = {
        proteins: [],
        produce: [],
        dairy: [],
        pantry: [],
        spices: [],
        other: []
    };
    
    ingredients.forEach(ing => {
        grouped[ing.category].push(ing);
    });
    
    // Render
    let html = '';
    const categoryLabels = {
        proteins: '🥩 Proteins',
        produce: '🥬 Produce',
        dairy: '🧀 Dairy',
        pantry: '🫙 Pantry',
        spices: '🌿 Spices',
        other: '📦 Other'
    };
    
    for (const [category, items] of Object.entries(grouped)) {
        if (items.length === 0) continue;
        
        html += `<div class="shopping-category">
            <h4 class="shopping-category-title">${categoryLabels[category]}</h4>`;
        
        // Sort: unchecked first, then checked
        items.sort((a, b) => {
            const aChecked = state.shoppingChecked[a.name.toLowerCase()];
            const bChecked = state.shoppingChecked[b.name.toLowerCase()];
            return aChecked === bChecked ? 0 : aChecked ? 1 : -1;
        });
        
        items.forEach(item => {
            const isChecked = state.shoppingChecked[item.name.toLowerCase()];
            const measureText = item.measures.length > 0 ? item.measures.join(', ') : '';
            
            html += `<div class="shopping-item ${isChecked ? 'checked' : ''}" data-ingredient="${item.name}">
                <div class="shopping-checkbox ${isChecked ? 'checked' : ''}">${isChecked ? '✓' : ''}</div>
                <span class="shopping-item-name">${item.name}</span>
                ${measureText ? `<span class="shopping-item-qty">${measureText}</span>` : ''}
            </div>`;
        });
        
        html += '</div>';
    }
    
    elements.shoppingList.innerHTML = html || '<p class="empty-list">No ingredients yet. Add meals to your calendar!</p>';
    
    // Update count
    const totalItems = ingredients.length;
    const checkedItems = ingredients.filter(i => state.shoppingChecked[i.name.toLowerCase()]).length;
    elements.itemCount.textContent = `${totalItems - checkedItems} of ${totalItems} items`;
    
    // Add click handlers
    document.querySelectorAll('.shopping-item').forEach(item => {
        item.addEventListener('click', () => {
            const ingredient = item.dataset.ingredient;
            handleShoppingCheck(ingredient);
        });
    });
}
```

---

## Acceptance Criteria

### Must Have (P0)
- [ ] Search recipes by name
- [ ] Browse recipes by category
- [ ] 7-day calendar with Breakfast/Lunch/Dinner slots
- [ ] Assign recipes to calendar slots
- [ ] Remove meals from calendar
- [ ] LocalStorage persistence for meal plan
- [ ] Auto-generated shopping list from planned meals
- [ ] Ingredients grouped by category
- [ ] Checkbox to mark items as purchased
- [ ] Favorites system with heart toggle
- [ ] Fluent 2.0 design tokens applied
- [ ] Loading/error/empty states
- [ ] Today's date highlighted

### Should Have (P1)
- [ ] Week navigation (prev/next)
- [ ] Random recipe button
- [ ] Copy shopping list to clipboard
- [ ] Combine duplicate ingredients
- [ ] Clear Week button
- [ ] Escape key cancels selection
- [ ] Mobile responsive layout

### Nice to Have (P2)
- [ ] Drag-and-drop meal assignment
- [ ] Nutrition summary (calories if available)
- [ ] "Fill Week Random" feature
- [ ] Export meal plan as PDF/image
- [ ] Dark mode support

---

## Testing Checklist

### API Tests
- [ ] Search "chicken" returns results
- [ ] Click "Seafood" category filters correctly
- [ ] Random button fetches new meal
- [ ] Meal details load with ingredients

### Calendar Tests
- [ ] Week displays Mon-Sun with correct dates
- [ ] Today is highlighted
- [ ] Previous/Next week navigation works
- [ ] Today button returns to current week
- [ ] Meals added appear in correct slot
- [ ] Meals persist after page refresh
- [ ] Remove button deletes meal

### Shopping List Tests
- [ ] List updates when meals added/removed
- [ ] Ingredients grouped correctly
- [ ] Checkboxes toggle and persist
- [ ] "Clear Checked" removes checked items
- [ ] "Copy List" copies to clipboard
- [ ] Duplicate ingredients combined

### Favorites Tests
- [ ] Heart toggles filled/empty
- [ ] Favorites appear in sidebar
- [ ] Favorites persist after refresh
- [ ] Can add favorite to calendar

### Design Tests
- [ ] Brand color (#0078D4) used correctly
- [ ] Cards have proper shadow and hover lift
- [ ] Smooth 200ms transitions
- [ ] Focus outlines visible
- [ ] Mobile layout works
