# Lab 1: Vibe Coding a Meal Planner

> **Duration**: 45-60 minutes  
> **Approach**: Iterative prompting ("vibe coding")  
> **Tools**: GitHub Copilot (Agent Mode) or Cline  
> **API**: TheMealDB (free, no API key required)

---

## Learning Objectives

By the end of this lab, you will:
- Experience iterative "vibe coding" with an AI coding assistant
- Build a functional meal planner through progressive refinement
- Understand the conversation overhead of unstructured prompting
- Count the iterations required to reach a polished result

---

## What You'll Build

A meal planning application with:
- Recipe search by name or category
- Weekly meal calendar (drag-drop assignment)
- Auto-generated shopping list from planned meals
- Favorites and local storage persistence
- Microsoft Fluent 2.0 design system

---

## Prerequisites

- [ ] VS Code with GitHub Copilot or Cline extension
- [ ] Empty project folder created
- [ ] Basic understanding of HTML/CSS/JavaScript

---

## The Vibe Coding Approach

In this lab, you'll start with a simple request and iteratively refine the application. This mimics real-world "vibe coding" where developers work conversationally with AI assistants.

**Track your iterations!** Note how many prompts it takes to reach the final result.

---

## Step 1: Initial Request

Start with a basic, high-level request:

```
Create a meal planner web app using HTML, CSS, and JavaScript. 
Use TheMealDB API (https://www.themealdb.com/api.php) to search for recipes.
```

### Expected Result
- Basic HTML structure
- Simple search input
- API integration (may have issues)
- Minimal styling

### What's Likely Missing
- ❌ No meal calendar
- ❌ No shopping list
- ❌ Basic/ugly styling
- ❌ No local storage
- ❌ No favorites

**Iteration count: 1**

---

## Step 2: Add Calendar View

```
Add a weekly calendar view where I can see Monday through Sunday. 
Each day should have slots for breakfast, lunch, and dinner.
```

### Expected Result
- 7-day grid layout
- Meal type labels
- Basic structure

### What's Likely Missing
- ❌ Can't add meals to calendar yet
- ❌ No visual feedback
- ❌ Doesn't match recipe search

**Iteration count: 2**

---

## Step 3: Connect Search to Calendar

```
When I click on a recipe from the search results, let me choose which day 
and meal slot (breakfast/lunch/dinner) to add it to. Show the recipe 
thumbnail and name in the calendar slot.
```

### Expected Result
- Click-to-add functionality
- Modal or dropdown for day/meal selection
- Recipes appear in calendar

### What's Likely Missing
- ❌ No way to remove meals
- ❌ Meals disappear on refresh
- ❌ Still rough styling

**Iteration count: 3**

---

## Step 4: Implement Persistence

```
Save the meal plan to localStorage so it persists when I refresh the page.
Also add a way to remove meals from the calendar by clicking an X button.
```

### Expected Result
- Meals survive page refresh
- Remove button on each meal
- localStorage read/write

### What's Likely Missing
- ❌ No shopping list yet
- ❌ No favorites
- ❌ Styling still basic

**Iteration count: 4**

---

## Step 5: Add Shopping List

```
Add a shopping list panel on the right side. When I have meals planned, 
automatically aggregate all the ingredients from those recipes and show 
them in the shopping list. Group them by category (produce, dairy, meat, etc).
```

### Expected Result
- Right sidebar with shopping list
- Ingredients pulled from recipes
- Some grouping attempt

### What's Likely Missing
- ❌ Duplicate ingredients not merged
- ❌ No quantities
- ❌ Can't check off items
- ❌ Category grouping may be wrong

**Iteration count: 5**

---

## Step 6: Fix Shopping List Issues

```
Fix the shopping list:
1. Combine duplicate ingredients (e.g., "2 onions" + "1 onion" = "3 onions")
2. Add checkboxes so I can mark items as purchased
3. Save checkbox state to localStorage
```

### Expected Result
- Smarter ingredient aggregation
- Interactive checkboxes
- Persistent checkbox state

### What's Likely Still Rough
- ❌ Design is utilitarian
- ❌ No favorites system
- ❌ No categories/filters

**Iteration count: 6**

---

## Step 7: Add Favorites

```
Add a favorites system:
1. Heart icon on each recipe card to mark as favorite
2. Favorites saved to localStorage
3. Show my favorites in the sidebar so I can quickly add them to the calendar
```

### Expected Result
- Heart toggle on recipes
- Favorites persist
- Quick access in sidebar

**Iteration count: 7**

---

## Step 8: Add Category Browsing

```
Add category buttons or a dropdown to browse recipes by category. 
TheMealDB has categories like Seafood, Chicken, Beef, Vegetarian, Dessert, etc.
Use their /filter.php?c={category} endpoint.
```

### Expected Result
- Category navigation
- Filtered recipe results
- Multiple browse modes

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
```

### Expected Result
- Professional Microsoft-style design
- Consistent spacing and typography
- Smooth hover animations
- Card elevation effects

**Iteration count: 9**

---

## Step 10: Add Random Recipe Button

```
Add a "Random Recipe" button that fetches a random recipe from 
TheMealDB's /random.php endpoint and displays it prominently.
Make it fun - maybe add a dice icon 🎲
```

### Expected Result
- Random recipe feature
- Fun interaction
- Easy discovery

**Iteration count: 10**

---

## Step 11: Polish and Fix Issues

At this point, review your app and prompt for any fixes:

```
Fix any remaining issues:
1. Make the layout responsive for mobile
2. Ensure all buttons have proper hover states
3. Add loading spinners during API calls
4. Handle API errors gracefully with user-friendly messages
```

### Expected Result
- Responsive design
- Loading states
- Error handling
- Polished interactions

**Iteration count: 11**

---

## Step 12: Final Touches

```
Final polish:
1. Add the app title "Meal Planner" with a 🍽️ icon in the header
2. Add a "Clear Week" button to reset the calendar
3. Add an "Export Shopping List" button that copies to clipboard
4. Make sure the calendar shows the current week with today highlighted
```

### Expected Result
- Complete, polished application
- All features working
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

### API CORS Issues
TheMealDB allows direct browser requests, but if you see CORS errors:
```
Try opening the HTML file directly (file://) rather than through a local server,
or use the www.themealdb.com domain (not themealdb.com).
```

### Ingredients Not Parsing
TheMealDB stores ingredients as `strIngredient1` through `strIngredient20`:
```
The API returns ingredients in a weird format. Each recipe has strIngredient1, 
strIngredient2, etc. up to strIngredient20, with corresponding strMeasure1, 
strMeasure2, etc. Parse all of these to get the full ingredient list.
```

### Calendar Not Persisting
```
The calendar meals aren't saving properly. Make sure you're saving the 
entire meal plan object to localStorage whenever it changes, and loading 
it when the page initializes.
```

---

## Final Checklist

Before moving to Lab 2, verify your app has:

- [ ] Recipe search working
- [ ] Category browsing working
- [ ] Weekly calendar with 3 meals per day
- [ ] Click-to-add recipes to calendar
- [ ] Remove meals from calendar
- [ ] LocalStorage persistence for meal plan
- [ ] Auto-generated shopping list
- [ ] Ingredient aggregation (duplicates combined)
- [ ] Checkable shopping list items
- [ ] Favorites system
- [ ] Fluent 2.0 styling
- [ ] Responsive layout
- [ ] Loading states
- [ ] Error handling

---

## Key Takeaway

**Vibe coding works, but it's inefficient.**

You likely spent 12+ prompts and significant back-and-forth to build this app. The AI had to re-read and understand the growing codebase with each iteration, sometimes introducing regressions.

In **Lab 2**, you'll see how a comprehensive upfront specification can achieve the same result in a **single prompt** - dramatically reducing iteration overhead and improving output consistency.

---

## Next Steps

→ Proceed to **Lab 2: Spec-Driven Development** to compare approaches
