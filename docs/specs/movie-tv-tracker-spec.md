# Movie & TV Tracker Application Specification

## Overview

Build a complete movie and TV show tracking application using vanilla HTML, CSS, and JavaScript. The application uses **OMDb API** and implements **Microsoft Fluent 2.0 design system**.

### API Key
```javascript
const API_KEY = 'YOUR_API_KEY_HERE'; // Replace with your OMDb API key
```

### Target Files
```
movie-tracker/
├── index.html    # Single-page application
├── styles.css    # Fluent 2.0 styling
├── app.js        # Application logic
└── README.md     # Setup instructions
```

---

## API Reference: OMDb API

**Base URL**: `https://www.omdbapi.com/`

### Endpoints Used

| Operation | URL | Parameters |
|-----------|-----|------------|
| Search | `/?s={query}&type={type}&apikey={key}` | s=search term, type=movie\|series |
| Get by ID | `/?i={imdbID}&plot=full&apikey={key}` | i=IMDB ID, plot=short\|full |

### Search Response
```javascript
{
  Search: [
    {
      Title: "The Matrix",
      Year: "1999",
      imdbID: "tt0133093",
      Type: "movie",
      Poster: "https://..."
    }
  ],
  totalResults: "89",
  Response: "True"
}
```

### Detail Response
```javascript
{
  Title: "The Matrix",
  Year: "1999",
  Rated: "R",
  Released: "31 Mar 1999",
  Runtime: "136 min",
  Genre: "Action, Sci-Fi",
  Director: "Lana Wachowski, Lilly Wachowski",
  Writer: "Lilly Wachowski, Lana Wachowski",
  Actors: "Keanu Reeves, Laurence Fishburne, Carrie-Anne Moss",
  Plot: "When a beautiful stranger...",
  Language: "English",
  Country: "United States, Australia",
  Awards: "Won 4 Oscars...",
  Poster: "https://...",
  Ratings: [
    { Source: "Internet Movie Database", Value: "8.7/10" },
    { Source: "Rotten Tomatoes", Value: "88%" },
    { Source: "Metacritic", Value: "73/100" }
  ],
  Metascore: "73",
  imdbRating: "8.7",
  imdbVotes: "1,900,000",
  imdbID: "tt0133093",
  Type: "movie",
  totalSeasons: "N/A" // Only for series
}
```

### Error Response
```javascript
{
  Response: "False",
  Error: "Movie not found!" | "Invalid API key!" | "Request limit reached!"
}
```

---

## Functional Requirements

### FR-1: Search Functionality

| ID | Requirement |
|----|-------------|
| FR-1.1 | Text input for searching titles |
| FR-1.2 | Search triggers on button click and Enter key |
| FR-1.3 | Toggle/tabs to switch between Movies and TV Shows |
| FR-1.4 | Display results in a responsive grid of poster cards |
| FR-1.5 | Each card shows: poster, title, year, type badge |
| FR-1.6 | Handle "N/A" posters with placeholder image |
| FR-1.7 | Show "No results found" for empty searches |
| FR-1.8 | Show loading spinner during API calls |
| FR-1.9 | Debounce search input (300ms) |

### FR-2: Detail Modal

| ID | Requirement |
|----|-------------|
| FR-2.1 | Click card to open detail modal |
| FR-2.2 | Fetch full details using OMDb ID |
| FR-2.3 | Display large poster image |
| FR-2.4 | Show title, year, runtime, rated badge |
| FR-2.5 | Display IMDb rating with ⭐ icon and vote count |
| FR-2.6 | Show Rotten Tomatoes score if available (🍅 icon) |
| FR-2.7 | Display full plot summary |
| FR-2.8 | List director and main cast |
| FR-2.9 | Show genre tags as pills |
| FR-2.10 | For TV shows: display total seasons |
| FR-2.11 | Add to Watchlist buttons (see FR-3) |
| FR-2.12 | Close on × button, overlay click, or Escape key |

### FR-3: Watchlist Management

| ID | Requirement |
|----|-------------|
| FR-3.1 | Three watchlist categories: "Want to Watch", "Currently Watching", "Completed" |
| FR-3.2 | Add button in detail modal for each list |
| FR-3.3 | If already in a list, show current status and allow moving |
| FR-3.4 | Sidebar displays all three lists with item counts |
| FR-3.5 | Click list item to view details |
| FR-3.6 | Remove button (×) on each list item |
| FR-3.7 | Dropdown to move item between lists |
| FR-3.8 | Prevent duplicates (same title can only be in one list) |
| FR-3.9 | Show date added to list |

### FR-4: Personal Ratings & Reviews

| ID | Requirement |
|----|-------------|
| FR-4.1 | 5-star rating component (clickable stars) |
| FR-4.2 | Stars highlight on hover to indicate selection |
| FR-4.3 | Click star to set rating (1-5) |
| FR-4.4 | Show personal rating next to IMDb rating |
| FR-4.5 | Notes/review textarea (max 500 characters) |
| FR-4.6 | Character count display |
| FR-4.7 | Ratings and reviews save to localStorage |
| FR-4.8 | Edit rating/review from watchlist item |

### FR-5: Filtering & Sorting

| ID | Requirement |
|----|-------------|
| FR-5.1 | Filter dropdown: All, Movies, TV Shows |
| FR-5.2 | Sort dropdown: Date Added, Title A-Z, Title Z-A, My Rating ↓, IMDb Rating ↓ |
| FR-5.3 | Search box to filter watchlist by title |
| FR-5.4 | Filters apply to currently selected list |
| FR-5.5 | Show count of filtered results |
| FR-5.6 | Clear filters button |

### FR-6: Statistics Dashboard

| ID | Requirement |
|----|-------------|
| FR-6.1 | Total items in each watchlist |
| FR-6.2 | Total movies vs TV shows (completed) |
| FR-6.3 | Average personal rating |
| FR-6.4 | Total watch time (sum of runtimes for completed) |
| FR-6.5 | Most common genre |
| FR-6.6 | Display as card grid at top of watchlist section |
| FR-6.7 | Stats update in real-time when lists change |

### FR-7: View Toggle

| ID | Requirement |
|----|-------------|
| FR-7.1 | Grid view: Poster cards in responsive grid |
| FR-7.2 | List view: Compact rows with thumbnail, title, year, ratings |
| FR-7.3 | Toggle buttons with icons (grid/list) |
| FR-7.4 | Remember preference in localStorage |

### FR-8: Data Persistence

| ID | Requirement |
|----|-------------|
| FR-8.1 | All watchlists save to localStorage |
| FR-8.2 | Key: `movieTracker_watchlists` |
| FR-8.3 | Ratings and reviews save to localStorage |
| FR-8.4 | Key: `movieTracker_ratings` |
| FR-8.5 | View preference saves to localStorage |
| FR-8.6 | Key: `movieTracker_viewMode` |
| FR-8.7 | Load all data on page initialization |
| FR-8.8 | "Clear All" button per list (with confirmation dialog) |

### FR-9: Additional Features

| ID | Requirement |
|----|-------------|
| FR-9.1 | "Random Pick" button on "Want to Watch" list |
| FR-9.2 | Highlights a random title with animation |
| FR-9.3 | Empty state messages for each list |
| FR-9.4 | Keyboard shortcuts: Escape closes modal |

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
    --colorStatusWarning: #FFB900;
    --colorStatusDanger: #D13438;
    
    /* Ratings */
    --colorStarFilled: #FFB900;
    --colorStarEmpty: #E0E0E0;
    --colorImdb: #F5C518;
    --colorRottenTomatoes: #FA320A;
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
| Small | 4px | Buttons, inputs, badges |
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

### NFR-2: Layout Structure

```
┌─────────────────────────────────────────────────────────────────┐
│  HEADER: Logo, Search Input, Type Toggle, Search Button         │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │  SEARCH RESULTS (when searching)                         │   │
│  │  Responsive grid of poster cards                         │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │  STATISTICS CARDS (4 cards in a row)                     │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  ┌────────────┬────────────────────────────────────────────┐   │
│  │  SIDEBAR   │  WATCHLIST CONTENT                          │   │
│  │  240px     │  flex: 1                                    │   │
│  │            │                                              │   │
│  │  • Want    │  Filters & Sort Bar                         │   │
│  │  • Watch   │  ─────────────────                          │   │
│  │  • Done    │  Grid or List of items                      │   │
│  │            │                                              │   │
│  └────────────┴────────────────────────────────────────────┘   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### NFR-3: Responsive Breakpoints

| Breakpoint | Width | Adjustments |
|------------|-------|-------------|
| Desktop | > 1024px | Full layout with sidebar |
| Tablet | 768-1024px | Collapsible sidebar |
| Mobile | < 768px | Sidebar becomes tabs, single column content |

### NFR-4: Accessibility

| Requirement |
|-------------|
| All interactive elements focusable via keyboard |
| Focus-visible outlines (2px brand color) |
| ARIA labels on icon-only buttons |
| Color contrast meets WCAG AA (4.5:1) |
| Star rating keyboard accessible (arrow keys) |

---

## HTML Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Movie & TV Tracker</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="app-container">
        <!-- Header -->
        <header class="header">
            <div class="logo">🎬 <span>My Watchlist</span></div>
            <div class="search-container">
                <div class="type-toggle">
                    <button class="type-btn active" data-type="movie">Movies</button>
                    <button class="type-btn" data-type="series">TV Shows</button>
                </div>
                <div class="search-box">
                    <input type="text" id="searchInput" placeholder="Search movies or TV shows...">
                    <button id="searchBtn">🔍</button>
                </div>
            </div>
        </header>

        <!-- Search Results (hidden by default) -->
        <section id="searchResults" class="search-results hidden">
            <div class="section-header">
                <h2>Search Results</h2>
                <button id="closeSearch" class="btn-icon">✕</button>
            </div>
            <div id="loadingSearch" class="loading hidden">
                <div class="spinner"></div>
                <p>Searching...</p>
            </div>
            <div id="resultsGrid" class="results-grid"></div>
        </section>

        <!-- Main Content -->
        <main class="main-content">
            <!-- Statistics -->
            <section class="stats-section">
                <div class="stats-grid">
                    <div class="stat-card">
                        <div class="stat-value" id="statTotal">0</div>
                        <div class="stat-label">Total Tracked</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-value" id="statCompleted">0</div>
                        <div class="stat-label">Completed</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-value" id="statAvgRating">-</div>
                        <div class="stat-label">Avg Rating</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-value" id="statWatchTime">0h</div>
                        <div class="stat-label">Watch Time</div>
                    </div>
                </div>
            </section>

            <!-- Watchlist Section -->
            <section class="watchlist-section">
                <aside class="sidebar">
                    <nav class="list-nav">
                        <button class="list-btn active" data-list="wantToWatch">
                            <span class="list-icon">📋</span>
                            <span class="list-name">Want to Watch</span>
                            <span class="list-count" id="countWant">0</span>
                        </button>
                        <button class="list-btn" data-list="watching">
                            <span class="list-icon">▶️</span>
                            <span class="list-name">Watching</span>
                            <span class="list-count" id="countWatching">0</span>
                        </button>
                        <button class="list-btn" data-list="completed">
                            <span class="list-icon">✅</span>
                            <span class="list-name">Completed</span>
                            <span class="list-count" id="countCompleted">0</span>
                        </button>
                    </nav>
                </aside>

                <div class="watchlist-content">
                    <!-- Filters Bar -->
                    <div class="filters-bar">
                        <div class="filter-group">
                            <input type="text" id="filterSearch" placeholder="Search in list...">
                            <select id="filterType">
                                <option value="all">All Types</option>
                                <option value="movie">Movies</option>
                                <option value="series">TV Shows</option>
                            </select>
                            <select id="sortBy">
                                <option value="dateAdded">Date Added</option>
                                <option value="titleAsc">Title A-Z</option>
                                <option value="titleDesc">Title Z-A</option>
                                <option value="myRating">My Rating ↓</option>
                                <option value="imdbRating">IMDb Rating ↓</option>
                            </select>
                        </div>
                        <div class="view-toggle">
                            <button class="view-btn active" data-view="grid" title="Grid view">▦</button>
                            <button class="view-btn" data-view="list" title="List view">☰</button>
                        </div>
                    </div>

                    <!-- Random Pick (for Want to Watch) -->
                    <div id="randomPick" class="random-pick hidden">
                        <button id="randomBtn" class="btn btn-secondary">🎲 Random Pick</button>
                    </div>

                    <!-- Watchlist Items -->
                    <div id="watchlistItems" class="watchlist-items grid-view">
                        <!-- Populated by JS -->
                    </div>

                    <!-- Empty State -->
                    <div id="emptyState" class="empty-state hidden">
                        <div class="empty-icon">🎬</div>
                        <p class="empty-message">No titles in this list yet</p>
                        <p class="empty-hint">Search for movies or TV shows to add them</p>
                    </div>
                </div>
            </section>
        </main>
    </div>

    <!-- Detail Modal -->
    <div id="detailModal" class="modal-overlay hidden">
        <div class="modal detail-modal">
            <button class="modal-close" id="closeDetailModal">✕</button>
            <div id="modalContent" class="modal-content">
                <!-- Populated by JS -->
            </div>
        </div>
    </div>

    <script src="app.js"></script>
</body>
</html>
```

---

## JavaScript Architecture

```javascript
// ================================================================
// CONFIGURATION
// ================================================================
const API_KEY = 'YOUR_API_KEY_HERE'; // Replace with your key
const API_BASE = 'https://www.omdbapi.com/';
const STORAGE_KEYS = {
    watchlists: 'movieTracker_watchlists',
    ratings: 'movieTracker_ratings',
    viewMode: 'movieTracker_viewMode'
};
const LISTS = {
    wantToWatch: 'Want to Watch',
    watching: 'Currently Watching',
    completed: 'Completed'
};
const PLACEHOLDER_POSTER = 'data:image/svg+xml,...'; // Gray placeholder

// ================================================================
// STATE
// ================================================================
let state = {
    searchType: 'movie',        // 'movie' | 'series'
    activeList: 'wantToWatch',  // Current watchlist tab
    viewMode: 'grid',           // 'grid' | 'list'
    watchlists: {
        wantToWatch: [],
        watching: [],
        completed: []
    },
    ratings: {},                // { imdbID: { stars: 4, review: '...' } }
    searchResults: [],
    filters: {
        search: '',
        type: 'all',
        sort: 'dateAdded'
    }
};

// ================================================================
// DOM REFERENCES
// ================================================================
const elements = {
    searchInput: document.getElementById('searchInput'),
    searchBtn: document.getElementById('searchBtn'),
    searchResults: document.getElementById('searchResults'),
    resultsGrid: document.getElementById('resultsGrid'),
    loadingSearch: document.getElementById('loadingSearch'),
    watchlistItems: document.getElementById('watchlistItems'),
    emptyState: document.getElementById('emptyState'),
    detailModal: document.getElementById('detailModal'),
    modalContent: document.getElementById('modalContent'),
    // ... all other elements
};

// ================================================================
// API FUNCTIONS
// ================================================================
async function searchTitles(query, type) {
    // GET /?s={query}&type={type}&apikey={key}
}

async function getTitleDetails(imdbID) {
    // GET /?i={imdbID}&plot=full&apikey={key}
}

// ================================================================
// RENDER FUNCTIONS
// ================================================================
function renderSearchResults(results) { }
function renderWatchlist() { }
function renderDetailModal(title) { }
function renderStats() { }
function renderStarRating(imdbID, currentRating) { }

// ================================================================
// WATCHLIST FUNCTIONS
// ================================================================
function addToList(title, listName) { }
function removeFromList(imdbID) { }
function moveToList(imdbID, newList) { }
function findTitleInLists(imdbID) { }
function getFilteredList() { }

// ================================================================
// RATING FUNCTIONS
// ================================================================
function setRating(imdbID, stars) { }
function setReview(imdbID, review) { }
function getRating(imdbID) { }

// ================================================================
// STATS FUNCTIONS
// ================================================================
function calculateStats() {
    // Total tracked
    // Total completed
    // Average rating
    // Total watch time (parse "136 min" to minutes)
    // Most common genre
}

// ================================================================
// FILTER & SORT FUNCTIONS
// ================================================================
function applyFilters(list) { }
function sortList(list, sortBy) { }

// ================================================================
// STORAGE FUNCTIONS
// ================================================================
function saveWatchlists() { }
function saveRatings() { }
function saveViewMode() { }
function loadAllData() { }

// ================================================================
// UTILITY FUNCTIONS
// ================================================================
function debounce(fn, delay) { }
function formatRuntime(runtime) { }
function getPosterUrl(poster) { }
function formatDate(isoDate) { }

// ================================================================
// EVENT HANDLERS
// ================================================================
function handleSearch() { }
function handleTypeToggle(type) { }
function handleCardClick(imdbID) { }
function handleAddToList(listName) { }
function handleRemoveFromList(imdbID) { }
function handleMoveToList(imdbID, newList) { }
function handleStarClick(imdbID, stars) { }
function handleReviewChange(imdbID, text) { }
function handleFilterChange() { }
function handleViewToggle(mode) { }
function handleRandomPick() { }
function handleClearList(listName) { }

// ================================================================
// INITIALIZATION
// ================================================================
function init() {
    loadAllData();
    renderWatchlist();
    renderStats();
    setupEventListeners();
}

function setupEventListeners() {
    // Search
    elements.searchBtn.addEventListener('click', handleSearch);
    elements.searchInput.addEventListener('keypress', e => e.key === 'Enter' && handleSearch());
    
    // Type toggle
    document.querySelectorAll('.type-btn').forEach(btn => {
        btn.addEventListener('click', () => handleTypeToggle(btn.dataset.type));
    });
    
    // List navigation
    document.querySelectorAll('.list-btn').forEach(btn => {
        btn.addEventListener('click', () => handleListChange(btn.dataset.list));
    });
    
    // Filters
    elements.filterSearch.addEventListener('input', debounce(handleFilterChange, 300));
    elements.filterType.addEventListener('change', handleFilterChange);
    elements.sortBy.addEventListener('change', handleFilterChange);
    
    // View toggle
    document.querySelectorAll('.view-btn').forEach(btn => {
        btn.addEventListener('click', () => handleViewToggle(btn.dataset.view));
    });
    
    // Modal close
    elements.closeDetailModal.addEventListener('click', closeModal);
    elements.detailModal.addEventListener('click', e => e.target === elements.detailModal && closeModal());
    document.addEventListener('keydown', e => e.key === 'Escape' && closeModal());
    
    // Random pick
    elements.randomBtn.addEventListener('click', handleRandomPick);
}

document.addEventListener('DOMContentLoaded', init);
```

---

## Star Rating Component

```javascript
function renderStarRating(imdbID, currentRating = 0, interactive = true) {
    const stars = [1, 2, 3, 4, 5].map(n => {
        const filled = n <= currentRating;
        const className = `star ${filled ? 'filled' : ''} ${interactive ? 'interactive' : ''}`;
        return `<span class="${className}" data-value="${n}" ${interactive ? `onclick="handleStarClick('${imdbID}', ${n})"` : ''}>★</span>`;
    }).join('');
    
    return `<div class="star-rating" data-id="${imdbID}">${stars}</div>`;
}

// CSS for stars
/*
.star-rating {
    display: inline-flex;
    gap: 2px;
}
.star {
    font-size: 20px;
    color: var(--colorStarEmpty);
    transition: var(--transitionFast);
}
.star.filled {
    color: var(--colorStarFilled);
}
.star.interactive {
    cursor: pointer;
}
.star.interactive:hover,
.star-rating:hover .star.interactive {
    color: var(--colorStarFilled);
}
.star-rating:hover .star.interactive:hover ~ .star {
    color: var(--colorStarEmpty);
}
*/
```

---

## Detail Modal Content Template

```javascript
function renderDetailModal(title, existingRating = null) {
    const inList = findTitleInLists(title.imdbID);
    const rating = getRating(title.imdbID);
    
    return `
        <div class="detail-header">
            <img class="detail-poster" src="${getPosterUrl(title.Poster)}" alt="${title.Title}">
            <div class="detail-info">
                <h2 class="detail-title">${title.Title}</h2>
                <div class="detail-meta">
                    <span class="badge ${title.Type}">${title.Type === 'series' ? 'TV Show' : 'Movie'}</span>
                    <span>${title.Year}</span>
                    ${title.Runtime !== 'N/A' ? `<span>${title.Runtime}</span>` : ''}
                    <span class="rated-badge">${title.Rated}</span>
                </div>
                
                <div class="ratings-row">
                    <div class="rating imdb">
                        <span class="rating-icon">⭐</span>
                        <span class="rating-value">${title.imdbRating}</span>
                        <span class="rating-label">IMDb</span>
                    </div>
                    ${title.Ratings.find(r => r.Source === 'Rotten Tomatoes') ? `
                    <div class="rating rt">
                        <span class="rating-icon">🍅</span>
                        <span class="rating-value">${title.Ratings.find(r => r.Source === 'Rotten Tomatoes').Value}</span>
                        <span class="rating-label">RT</span>
                    </div>
                    ` : ''}
                </div>
                
                ${title.Type === 'series' ? `<p class="seasons">${title.totalSeasons} Seasons</p>` : ''}
                
                <div class="genres">
                    ${title.Genre.split(', ').map(g => `<span class="genre-tag">${g}</span>`).join('')}
                </div>
            </div>
        </div>
        
        <div class="detail-body">
            <div class="plot">
                <h3>Plot</h3>
                <p>${title.Plot}</p>
            </div>
            
            <div class="credits">
                <p><strong>Director:</strong> ${title.Director}</p>
                <p><strong>Cast:</strong> ${title.Actors}</p>
            </div>
            
            <div class="my-rating">
                <h3>My Rating</h3>
                ${renderStarRating(title.imdbID, rating?.stars || 0, true)}
            </div>
            
            <div class="my-review">
                <h3>My Notes</h3>
                <textarea 
                    id="reviewText" 
                    placeholder="Write your thoughts..."
                    maxlength="500"
                    onchange="handleReviewChange('${title.imdbID}', this.value)"
                >${rating?.review || ''}</textarea>
                <div class="char-count"><span id="charCount">${(rating?.review || '').length}</span>/500</div>
            </div>
        </div>
        
        <div class="detail-actions">
            ${inList ? `
                <div class="current-status">
                    <span>In: ${LISTS[inList]}</span>
                    <select onchange="handleMoveToList('${title.imdbID}', this.value)">
                        ${Object.entries(LISTS).map(([key, name]) => 
                            `<option value="${key}" ${key === inList ? 'selected' : ''}>${name}</option>`
                        ).join('')}
                    </select>
                </div>
                <button class="btn btn-danger" onclick="handleRemoveFromList('${title.imdbID}')">Remove</button>
            ` : `
                <button class="btn btn-secondary" onclick="handleAddToList('wantToWatch')">📋 Want to Watch</button>
                <button class="btn btn-secondary" onclick="handleAddToList('watching')">▶️ Watching</button>
                <button class="btn btn-primary" onclick="handleAddToList('completed')">✅ Completed</button>
            `}
        </div>
    `;
}
```

---

## Watchlist Item Data Structure

```javascript
// Item stored in watchlist
{
    imdbID: "tt0133093",
    title: "The Matrix",
    year: "1999",
    type: "movie",
    poster: "https://...",
    imdbRating: "8.7",
    runtime: "136 min",
    genre: "Action, Sci-Fi",
    dateAdded: "2025-12-03T10:30:00.000Z"
}

// Item stored in ratings
{
    "tt0133093": {
        stars: 5,
        review: "One of the best sci-fi movies ever made!"
    }
}
```

---

## Acceptance Criteria

### Must Have (P0)
- [ ] Search movies by title
- [ ] Search TV shows by title
- [ ] Toggle between Movies and TV Shows
- [ ] Display search results as poster cards
- [ ] Click card to view full details in modal
- [ ] Three watchlists (Want to Watch, Watching, Completed)
- [ ] Add titles to any watchlist
- [ ] Remove titles from watchlists
- [ ] Move titles between lists
- [ ] LocalStorage persistence for watchlists
- [ ] 5-star personal rating system
- [ ] Notes/review field
- [ ] LocalStorage persistence for ratings
- [ ] Statistics cards (total, completed, avg rating, watch time)
- [ ] Microsoft Fluent 2.0 design tokens applied

### Should Have (P1)
- [ ] Filter by type (Movie/TV)
- [ ] Sort by various criteria
- [ ] Search within watchlists
- [ ] Grid/List view toggle
- [ ] Placeholder for missing posters
- [ ] Loading spinners
- [ ] Error messages
- [ ] Empty state messages
- [ ] Date added display

### Nice to Have (P2)
- [ ] Random Pick feature
- [ ] Clear All with confirmation
- [ ] Rotten Tomatoes score display
- [ ] Keyboard accessibility
- [ ] Mobile responsive layout
- [ ] Most common genre stat

---

## Testing Checklist

### API Tests
- [ ] Search "Matrix" returns movies
- [ ] Search "Breaking Bad" with TV toggle returns series
- [ ] Invalid API key shows error message
- [ ] Empty search shows "No results"

### Watchlist Tests
- [ ] Add movie to "Want to Watch"
- [ ] Add TV show to "Watching"
- [ ] Move item from "Want to Watch" to "Completed"
- [ ] Remove item from list
- [ ] Refresh page - lists persist
- [ ] Same title cannot be in multiple lists

### Rating Tests
- [ ] Click 4 stars sets rating to 4
- [ ] Stars highlight on hover
- [ ] Write review and save
- [ ] Refresh page - rating persists
- [ ] Character count updates

### Filter Tests
- [ ] Filter shows only movies
- [ ] Sort by Title A-Z works
- [ ] Search "matrix" in list filters results
- [ ] Clear filters resets view

### View Tests
- [ ] Grid view shows poster cards
- [ ] List view shows compact rows
- [ ] Toggle persists after refresh

### Design Tests
- [ ] Brand color (#0078D4) used correctly
- [ ] Cards have proper shadow and hover lift
- [ ] Stars are gold when filled (#FFB900)
- [ ] Smooth 200ms transitions
- [ ] Focus outlines visible
