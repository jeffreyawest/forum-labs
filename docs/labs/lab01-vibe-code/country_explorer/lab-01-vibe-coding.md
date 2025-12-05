# Lab 1: Vibe Coding a Country Explorer

> **Duration**: 45-60 minutes  
> **Approach**: Iterative prompting ("vibe coding")  
> **Tools**: GitHub Copilot (Agent Mode) or Cline  
> **API**: REST Countries (free, no API key required)

---

## Learning Objectives

By the end of this lab, you will:
- Experience iterative "vibe coding" with an AI coding assistant
- Build a functional country explorer through progressive refinement
- Understand the conversation overhead of unstructured prompting
- Count the iterations required to reach a polished result

---

## What You'll Build

A country exploration application with:
- Browse and search all countries
- View detailed country information
- Filter by region and subregion
- Build a travel bucket list
- Track visited countries
- View travel statistics and visualizations
- Compare countries side-by-side
- Microsoft Fluent 2.0 design system

---

## Prerequisites

- [ ] VS Code with GitHub Copilot or Cline extension
- [ ] Empty project folder created
- [ ] Basic understanding of HTML/CSS/JavaScript
- [ ] **No API key required!** REST Countries is completely free

---

## API Quick Reference

**Base URL**: `https://restcountries.com/v3.1`

| Endpoint | Returns |
|----------|---------|
| `/all` | All countries |
| `/name/{name}` | Countries by name |
| `/region/{region}` | Countries by region |
| `/subregion/{subregion}` | Countries by subregion |
| `/alpha/{code}` | Country by code (cca2, cca3, ccn3) |

---

## The Vibe Coding Approach

In this lab, you'll start with a simple request and iteratively refine the application. This mimics real-world "vibe coding" where developers work conversationally with AI assistants.

**Track your iterations!** Note how many prompts it takes to reach the final result.

---

## Step 1: Initial Request

Start with a basic, high-level request:

```
Create a country explorer web app using HTML, CSS, and JavaScript.
Use the REST Countries API (https://restcountries.com/) to fetch country data.
Let me browse and search for countries.
```

### Expected Result
- Basic HTML structure
- Search input
- API integration
- Country list display
- Minimal styling

### What's Likely Missing
- ❌ No detailed country view
- ❌ No filtering options
- ❌ Basic/ugly styling
- ❌ No bucket list feature

**Iteration count: 1**

---

## Step 2: Show Country Details

```
When I click on a country, show a detail modal with:
- Country flag (flags.svg)
- Official name and common name
- Capital city
- Population (formatted with commas)
- Region and subregion
- Languages spoken
- Currencies used
- Borders (neighboring countries)
- Google Maps link (maps.googleMaps)
```

### Expected Result
- Click-to-view functionality
- Detailed information display
- Maps link

### What's Likely Missing
- ❌ Flag may not display properly
- ❌ Languages/currencies format may be off
- ❌ Border countries show as codes, not names

**Iteration count: 2**

---

## Step 3: Fix Data Formatting

```
Fix the country detail display:
1. Languages come as an object like { eng: "English", spa: "Spanish" }
   - Show as comma-separated list of values
2. Currencies come as an object like { USD: { name: "US Dollar", symbol: "$" } }
   - Show as "US Dollar ($)"
3. Border codes (like USA, MEX) should show country names instead
   - Fetch the border country names and display them as clickable links
```

### Expected Result
- Properly formatted languages
- Currencies with symbols
- Clickable border countries

**Iteration count: 3**

---

## Step 4: Add Region Filter

```
Add a filter dropdown to browse countries by region:
- All (default)
- Africa
- Americas
- Asia
- Europe
- Oceania

When selecting a region, show only countries from that region.
Keep the search working within the filtered region.
```

### Expected Result
- Region dropdown filter
- Combined search + filter
- Region-specific results

### What's Likely Missing
- ❌ May fetch all then filter (slow)
- ❌ No loading indicator

**Iteration count: 4**

---

## Step 5: Add Bucket List

```
Add a "Bucket List" feature:
1. Each country card should have an "Add to Bucket List" button (heart icon)
2. Create a bucket list panel showing countries I want to visit
3. Save the bucket list to localStorage
4. Allow removing countries from the bucket list
5. Show the count of countries in my bucket list
```

### Expected Result
- Heart button on cards
- Bucket list panel
- Persistence
- Remove functionality

### What's Likely Missing
- ❌ No visited tracking
- ❌ No statistics

**Iteration count: 5**

---

## Step 6: Add Visited Tracking

```
Add a "Visited" feature:
1. Add a checkmark button to mark countries as visited
2. Create a "Visited Countries" panel
3. Different styling for visited vs bucket list vs neither
4. Save visited countries to localStorage
5. A country can be in bucket list OR visited, but not both
   - Moving from bucket list to visited should remove from bucket list
```

### Expected Result
- Visited tracking
- Visual distinction
- State management
- Auto-transition logic

**Iteration count: 6**

---

## Step 7: Add Statistics Dashboard

```
Add a statistics section that shows:
1. Total countries visited: X / 250
2. Progress bar showing percentage
3. Breakdown by region:
   - Africa: X / 54
   - Americas: X / 56
   - Asia: X / 50
   - Europe: X / 53
   - Oceania: X / 27
4. Total bucket list items
5. Countries remaining to visit
```

### Expected Result
- Statistics display
- Progress visualization
- Regional breakdown

### What's Likely Missing
- ❌ Numbers may be off
- ❌ Progress bars may not look good

**Iteration count: 7**

---

## Step 8: Add Sorting Options

```
Add sorting options for the country list:
- Name (A-Z)
- Name (Z-A)
- Population (highest first)
- Population (lowest first)
- Area (largest first)
- Area (smallest first)

Add a dropdown to select the sort option.
```

### Expected Result
- Sort dropdown
- Multiple sort options
- Instant re-sorting

**Iteration count: 8**

---

## Step 9: Add Country Comparison

```
Add a compare feature:
1. Add a "Compare" button/checkbox on country cards
2. Can select 2-4 countries to compare
3. Show comparison view with:
   - Flags side by side
   - Population bar chart
   - Area bar chart
   - Languages comparison
   - Currencies comparison
4. "Clear comparison" button
```

### Expected Result
- Multi-select for comparison
- Side-by-side comparison
- Visual charts

### What's Likely Missing
- ❌ Charts may not scale correctly
- ❌ Layout may break with 4 countries

**Iteration count: 9**

---

## Step 10: Apply Fluent 2.0 Design

```
Restyle the entire application using Microsoft Fluent 2.0 design system:
- Use Segoe UI Variable font
- Brand color #0078D4 (Microsoft blue)
- Proper shadow tokens (shadow2, shadow4, shadow8, shadow16)
- Border radius: 4px small, 8px medium, 12px large
- Spacing scale: 4px, 8px, 12px, 16px, 20px, 24px, 32px
- Hover states with smooth 200ms transitions
- Cards should lift on hover with increased shadow
```

### Expected Result
- Professional Microsoft-style design
- Consistent spacing and typography
- Smooth hover animations

**Iteration count: 10**

---

## Step 11: Polish and Fix Issues

```
Fix any remaining issues:
1. Add loading spinner when fetching country data
2. Handle API errors gracefully
3. Make the layout responsive for mobile
4. Add empty state messages for empty lists
5. Add smooth animations when adding/removing countries from lists
6. Add a world map visualization showing visited countries (use simple colored dots)
```

### Expected Result
- Loading states
- Error handling
- Responsive design
- Animations
- Map visualization

**Iteration count: 11**

---

## Step 12: Final Touches

```
Final polish:
1. Add app title "Country Explorer" with a globe icon 🌍
2. Add a "Random Country" button to discover new places
3. Add timezone information to country details
4. Add driving side (left/right)
5. Add a "Share My Progress" button that copies stats to clipboard
6. Add dark mode toggle
```

### Expected Result
- Complete, polished application
- Fun features (random, share)
- Dark mode support
- Professional appearance

**Iteration count: 12**

---

## Reflection Questions

After completing the lab, consider:

1. **How many prompts did it take?** 
   - Typical: 10-15 iterations
   - Your count: ___

2. **How many "fix this" prompts were needed?**
   - Count prompts that corrected previous output: ___

3. **Did the data formatting work correctly the first time?**
   - Languages, currencies, and borders often need fixes

4. **How would you describe the conversation efficiency?**
   - Lots of back-and-forth?
   - Context getting lost?

5. **What if you needed to rebuild this app?**
   - Would you remember all the prompts?
   - Could someone else replicate your result?

---

## Common Issues & Fixes

### Flag Not Displaying
```
The flags.svg URL should work directly in an <img> tag:
<img src="${country.flags.svg}" alt="${country.name.common} flag">

If it doesn't load, try flags.png as fallback.
```

### Languages/Currencies Object Format
```
// Languages: { eng: "English", spa: "Spanish" }
Object.values(country.languages).join(', ')

// Currencies: { USD: { name: "US Dollar", symbol: "$" } }
Object.values(country.currencies)
  .map(c => `${c.name} (${c.symbol})`)
  .join(', ')
```

### Border Country Codes
```
// borders: ["USA", "GTM", "BLZ"]
// Need to fetch each country to get the name
const borderCountries = await Promise.all(
  country.borders.map(code => 
    fetch(`https://restcountries.com/v3.1/alpha/${code}`)
      .then(r => r.json())
      .then(data => data[0].name.common)
  )
);
```

### Missing Data
```
Some countries don't have all fields. Add fallbacks:
const capital = country.capital?.[0] || 'N/A';
const languages = country.languages 
  ? Object.values(country.languages).join(', ') 
  : 'N/A';
```

---

## Final Checklist

Before moving to Lab 2, verify your app has:

- [ ] Browse all countries
- [ ] Search by name
- [ ] Filter by region
- [ ] Country detail modal
- [ ] Properly formatted languages
- [ ] Properly formatted currencies  
- [ ] Clickable border countries
- [ ] Bucket list feature
- [ ] Visited countries tracking
- [ ] LocalStorage persistence
- [ ] Statistics dashboard
- [ ] Regional breakdown
- [ ] Sorting options
- [ ] Country comparison
- [ ] Fluent 2.0 styling
- [ ] Responsive layout
- [ ] Loading states
- [ ] Error handling
- [ ] Dark mode

---

## Key Takeaway

**Vibe coding works, but it's inefficient.**

You likely spent 12+ prompts and significant back-and-forth to build this app. The data formatting (languages, currencies, borders) alone probably required multiple iterations to get right.

In **Lab 2**, you'll see how a comprehensive upfront specification can achieve the same result in a **single prompt** - dramatically reducing iteration overhead and improving output consistency.

---

## Next Steps

→ Proceed to **Lab 2: Spec-Driven Development** to compare approaches
