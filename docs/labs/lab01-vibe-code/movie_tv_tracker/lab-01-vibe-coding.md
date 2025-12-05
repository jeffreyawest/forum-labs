# Lab 1: Vibe Coding a Movie & TV Tracker

> **Duration**: 45-60 minutes  
> **Approach**: Iterative prompting ("vibe coding")  
> **Tools**: GitHub Copilot (Agent Mode) or Cline  
> **API**: OMDb API (free tier, requires API key)

---

## Learning Objectives

By the end of this lab, you will:
- Experience iterative "vibe coding" with an AI coding assistant
- Build a functional movie/TV tracker through progressive refinement
- Understand the conversation overhead of unstructured prompting
- Count the iterations required to reach a polished result

---

## What You'll Build

A movie and TV show tracking application with:
- Search movies and TV shows by title
- View detailed information (poster, plot, ratings, cast)
- Create watchlists (Want to Watch, Currently Watching, Completed)
- Rate and review titles you've watched
- Filter and sort your collection
- Microsoft Fluent 2.0 design system

---

## Prerequisites

- [ ] VS Code with GitHub Copilot or Cline extension
- [ ] Empty project folder created
- [ ] OMDb API key (free at https://www.omdbapi.com/apikey.aspx)
- [ ] Basic understanding of HTML/CSS/JavaScript

### Getting Your API Key

1. Go to https://www.omdbapi.com/apikey.aspx
2. Select "FREE! (1,000 daily limit)"
3. Enter your email
4. Check your email and click the verification link
5. Save your API key (e.g., `a1b2c3d4`)

---

## The Vibe Coding Approach

In this lab, you'll start with a simple request and iteratively refine the application. This mimics real-world "vibe coding" where developers work conversationally with AI assistants.

**Track your iterations!** Note how many prompts it takes to reach the final result.

---

## Step 1: Initial Request

Start with a basic, high-level request:

```
Create a movie tracker web app using HTML, CSS, and JavaScript.
Use the OMDb API (https://www.omdbapi.com/) to search for movies.
My API key is: [YOUR_API_KEY]
```

### Expected Result
- Basic HTML structure
- Simple search input
- API integration (may have issues)
- Minimal styling

### What's Likely Missing
- ❌ No watchlist functionality
- ❌ No TV shows (movies only)
- ❌ Basic/ugly styling
- ❌ No local storage
- ❌ No ratings/reviews

**Iteration count: 1**

---

## Step 2: Add Detailed Movie View

```
When I click on a movie from search results, show a modal with full details:
- Large poster image
- Title, year, and runtime
- IMDb rating with star icon
- Plot summary
- Director and main cast
- Genre tags
```

### Expected Result
- Click-to-view functionality
- Modal with movie details
- API fetches full details by ID

### What's Likely Missing
- ❌ No watchlist buttons yet
- ❌ Can't distinguish movies from TV shows
- ❌ Modal styling may be rough

**Iteration count: 2**

---

## Step 3: Support TV Shows

```
Update the search to also find TV shows. The OMDb API uses type=movie or type=series.
Add tabs or toggle buttons to switch between searching Movies and TV Shows.
For TV shows, also display the total seasons and years aired.
```

### Expected Result
- Tab/toggle for Movies vs TV Shows
- Different display for series info
- Type indicator on cards

### What's Likely Missing
- ❌ Still no watchlist
- ❌ Can't save anything
- ❌ Basic styling

**Iteration count: 3**

---

## Step 4: Add Watchlist Feature

```
Add a watchlist feature with three lists:
1. "Want to Watch" - titles I plan to watch
2. "Currently Watching" - titles I'm in the middle of
3. "Completed" - titles I've finished

Add buttons in the movie detail modal to add to each list.
Show a sidebar or section that displays my watchlists.
```

### Expected Result
- Three watchlist categories
- Add buttons in detail modal
- Sidebar showing lists

### What's Likely Missing
- ❌ Lists disappear on refresh
- ❌ No way to move between lists
- ❌ No remove functionality

**Iteration count: 4**

---

## Step 5: Implement Persistence

```
Save all watchlists to localStorage so they persist when I refresh the page.
Also add:
- A way to remove titles from lists
- A way to move titles between lists (e.g., from "Want to Watch" to "Currently Watching")
```

### Expected Result
- Watchlists survive page refresh
- Remove button on each item
- Move/status dropdown

### What's Likely Missing
- ❌ No personal ratings yet
- ❌ No sorting/filtering
- ❌ Styling still basic

**Iteration count: 5**

---

## Step 6: Add Personal Ratings

```
Let me rate titles I've watched with a 1-5 star rating.
Show my personal rating next to the IMDb rating.
Add a small review/notes text field where I can write my thoughts.
Save ratings and reviews to localStorage.
```

### Expected Result
- Star rating component
- Notes textarea
- Personal ratings display
- Persistent storage

### What's Likely Missing
- ❌ Stars may not be interactive
- ❌ No filter by rating
- ❌ Review editing may be clunky

**Iteration count: 6**

---

## Step 7: Add Filtering and Sorting

```
Add filtering and sorting options for my watchlists:
- Filter by: All, Movies only, TV Shows only
- Sort by: Date added, Title (A-Z), My rating (high to low), IMDb rating
- Add a search box to search within my watchlists
```

### Expected Result
- Filter dropdown
- Sort dropdown
- Local search input

### What's Likely Missing
- ❌ May not remember filter state
- ❌ Performance issues with large lists
- ❌ UI getting cluttered

**Iteration count: 7**

---

## Step 8: Add Statistics Dashboard

```
Add a statistics section that shows:
- Total titles in each list
- Total movies vs TV shows watched
- Average rating I give
- Most watched genre
- Total watch time (sum of runtimes)
Display this as cards at the top of the watchlist section.
```

### Expected Result
- Stats cards with numbers
- Calculated totals
- Visual indicators

### What's Likely Missing
- ❌ Genre data may be incomplete
- ❌ Calculations may be wrong
- ❌ Not updating in real-time

**Iteration count: 8**

---

## Step 9: Apply Fluent 2.0 Design

```
Restyle the entire application using Microsoft Fluent 2.0 design system:
- Use Segoe UI Variable font
- Brand color #0078D4 (Microsoft blue)
- Proper shadow tokens (shadow2, shadow4, shadow8, shadow16)
- Border radius: 4px small, 8px medium, 12px large
- Spacing scale: 4px, 8px, 12px, 16px, 20px, 24px, 32px
- Hover states with smooth 200ms transitions
- Cards should lift on hover with increased shadow
- Star ratings in gold (#FFB900)
```

### Expected Result
- Professional Microsoft-style design
- Consistent spacing and typography
- Smooth hover animations
- Card elevation effects

**Iteration count: 9**

---

## Step 10: Add View Toggle

```
Add a toggle to switch between:
- Grid view: Shows poster cards in a responsive grid (current layout)
- List view: Shows items in a compact list with poster thumbnail, title, year, and rating

Remember the user's preference in localStorage.
```

### Expected Result
- Grid/List toggle buttons
- Two different layouts
- Persisted preference

**Iteration count: 10**

---

## Step 11: Polish and Fix Issues

At this point, review your app and prompt for any fixes:

```
Fix any remaining issues:
1. Make the layout responsive for mobile (stack sidebar below main content)
2. Add loading spinners during API calls
3. Handle API errors gracefully with user-friendly messages
4. Add empty state messages when lists are empty
5. Ensure all buttons have proper hover states
```

### Expected Result
- Responsive design
- Loading states
- Error handling
- Empty states
- Polished interactions

**Iteration count: 11**

---

## Step 12: Final Touches

```
Final polish:
1. Add the app title "My Watchlist" with a 🎬 icon in the header
2. Add a "Clear All" button for each watchlist (with confirmation)
3. Show the date when I added each title to a list
4. Add keyboard shortcuts: Escape closes modals, Enter submits search
5. Add a "Random Pick" button that suggests a random title from my "Want to Watch" list
```

### Expected Result
- Complete, polished application
- All features working
- Professional appearance
- Fun "Random Pick" feature

**Iteration count: 12**

---

## Reflection Questions

After completing the lab, consider:

1. **How many prompts did it take?** 
   - Typical: 10-15 iterations
   - Your count: ___

2. **How many "fix this" prompts were needed?**
   - Count prompts that corrected previous output: ___

3. **Did the AI ever break something while adding a feature?**
   - This is common in iterative development

4. **How would you describe the conversation efficiency?**
   - Lots of back-and-forth?
   - Repeated explanations?
   - Context getting lost?

5. **What if you needed to rebuild this app?**
   - Would you remember all the prompts?
   - Could someone else replicate your result?

---

## Common Issues & Fixes

### API Key Issues
```
I'm getting "Invalid API key" or "Request limit reached" errors.
Make sure to use your actual API key and check you haven't exceeded the 1,000 daily limit.
```

### Poster Images Not Loading
```
Some posters show "N/A" from the API. Add a fallback placeholder image 
when poster is "N/A" or undefined.
```

### TV Show Runtime Issues
```
TV shows don't have a single runtime like movies. Either hide runtime for series
or show "per episode" runtime if available.
```

### Star Rating Not Clickable
```
The star rating display is not interactive. Make it so clicking a star 
sets my rating to that value. Highlight stars up to the clicked star.
```

---

## Final Checklist

Before moving to Lab 2, verify your app has:

- [ ] Search working for movies
- [ ] Search working for TV shows
- [ ] Movie/TV toggle or tabs
- [ ] Detailed view modal
- [ ] Three watchlists (Want to Watch, Watching, Completed)
- [ ] Add to watchlist buttons
- [ ] Move between lists
- [ ] Remove from lists
- [ ] LocalStorage persistence
- [ ] Personal star ratings (1-5)
- [ ] Notes/review field
- [ ] Filter by type (Movie/TV)
- [ ] Sort options
- [ ] Search within watchlists
- [ ] Statistics cards
- [ ] Grid/List view toggle
- [ ] Fluent 2.0 styling
- [ ] Responsive layout
- [ ] Loading states
- [ ] Error handling
- [ ] Empty states

---

## Key Takeaway

**Vibe coding works, but it's inefficient.**

You likely spent 12+ prompts and significant back-and-forth to build this app. The AI had to re-read and understand the growing codebase with each iteration, sometimes introducing regressions.

In **Lab 2**, you'll see how a comprehensive upfront specification can achieve the same result in a **single prompt** - dramatically reducing iteration overhead and improving output consistency.

---

## Next Steps

→ Proceed to **Lab 2: Spec-Driven Development** to compare approaches
