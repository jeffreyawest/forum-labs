# Lab 1: Vibe Coding a Pokémon Team Builder

> **Duration**: 45-60 minutes  
> **Approach**: Iterative prompting ("vibe coding")  
> **Tools**: GitHub Copilot (Agent Mode) or Cline  
> **API**: PokéAPI (free, no API key required)

---

## Learning Objectives

By the end of this lab, you will:
- Experience iterative "vibe coding" with an AI coding assistant
- Build a functional Pokémon team builder through progressive refinement
- Understand the conversation overhead of unstructured prompting
- Count the iterations required to reach a polished result

---

## What You'll Build

A Pokémon team building application with:
- Search and browse all Pokémon
- View detailed stats, types, and abilities
- Build teams of up to 6 Pokémon
- Type effectiveness analysis
- Save multiple teams to localStorage
- Compare Pokémon stats
- Microsoft Fluent 2.0 design system

---

## Prerequisites

- [ ] VS Code with GitHub Copilot or Cline extension
- [ ] Empty project folder created
- [ ] Basic understanding of HTML/CSS/JavaScript
- [ ] **No API key required!** PokéAPI is completely free

---

## API Quick Reference

**Base URL**: `https://pokeapi.co/api/v2`

| Endpoint | Returns |
|----------|---------|
| `/pokemon/{name or id}` | Pokémon details (stats, types, sprites) |
| `/pokemon?limit=151` | List of Pokémon (paginated) |
| `/type/{name}` | Type details with damage relations |
| `/ability/{name}` | Ability description |

---

## The Vibe Coding Approach

In this lab, you'll start with a simple request and iteratively refine the application. This mimics real-world "vibe coding" where developers work conversationally with AI assistants.

**Track your iterations!** Note how many prompts it takes to reach the final result.

---

## Step 1: Initial Request

Start with a basic, high-level request:

```
Create a Pokémon team builder web app using HTML, CSS, and JavaScript.
Use the PokéAPI (https://pokeapi.co/) to fetch Pokémon data.
Let me search for Pokémon and see their details.
```

### Expected Result
- Basic HTML structure
- Search input
- API integration
- Minimal styling

### What's Likely Missing
- ❌ No team building feature
- ❌ No type information
- ❌ Basic/ugly styling
- ❌ Only shows basic info

**Iteration count: 1**

---

## Step 2: Show Pokémon Details

```
When I click on a Pokémon from the search results, show a detailed card with:
- Official artwork (sprites.other.official-artwork.front_default)
- Name and Pokédex number
- Types with colored badges
- Base stats (HP, Attack, Defense, Sp.Atk, Sp.Def, Speed) as bars
- Height and weight
```

### Expected Result
- Click-to-view functionality
- Stats visualization
- Type badges

### What's Likely Missing
- ❌ Stat bars may not be proportional
- ❌ Type colors may be wrong
- ❌ No team building yet

**Iteration count: 2**

---

## Step 3: Add Type Colors

```
Use the correct Pokémon type colors for the badges:
- Normal: #A8A878
- Fire: #F08030
- Water: #6890F0
- Electric: #F8D030
- Grass: #78C850
- Ice: #98D8D8
- Fighting: #C03028
- Poison: #A040A0
- Ground: #E0C068
- Flying: #A890F0
- Psychic: #F85888
- Bug: #A8B820
- Rock: #B8A038
- Ghost: #705898
- Dragon: #7038F8
- Dark: #705848
- Steel: #B8B8D0
- Fairy: #EE99AC
```

### Expected Result
- Proper type colors
- Visually distinct badges

**Iteration count: 3**

---

## Step 4: Add Team Building

```
Add a team builder section:
1. Show "My Team" panel that can hold up to 6 Pokémon
2. Add an "Add to Team" button on each Pokémon card
3. Show small sprites for team members
4. Allow removing Pokémon from the team by clicking an X
5. Show a message when the team is full (6 Pokémon)
```

### Expected Result
- Team panel with 6 slots
- Add/remove functionality
- Team limit enforcement

### What's Likely Missing
- ❌ Team doesn't persist
- ❌ No type coverage analysis
- ❌ Can add duplicates

**Iteration count: 4**

---

## Step 5: Prevent Duplicates and Add Persistence

```
Fix the team builder:
1. Prevent adding the same Pokémon twice to a team
2. Save the team to localStorage so it persists on refresh
3. Show a warning message if trying to add a duplicate
```

### Expected Result
- Duplicate prevention
- localStorage persistence
- User feedback

**Iteration count: 5**

---

## Step 6: Add Browse by Generation

```
Add a way to browse Pokémon by generation instead of just searching:
- Gen 1 (Kanto): #1-151
- Gen 2 (Johto): #152-251
- Gen 3 (Hoenn): #252-386
- Gen 4 (Sinnoh): #387-493
- Gen 5 (Unova): #494-649
- Gen 6 (Kalos): #650-721
- Gen 7 (Alola): #722-809
- Gen 8 (Galar): #810-905
- Gen 9 (Paldea): #906-1010

Show generation buttons and load that generation's Pokémon when clicked.
```

### Expected Result
- Generation selector buttons
- Paginated Pokémon loading
- Grid of Pokémon cards

### What's Likely Missing
- ❌ May be slow loading all at once
- ❌ No loading indicator

**Iteration count: 6**

---

## Step 7: Add Type Effectiveness

```
Add a type effectiveness section that shows:
1. My team's defensive weaknesses (what types deal 2x damage)
2. My team's resistances (what types deal 0.5x damage)
3. My team's immunities (what types deal 0x damage)

Calculate this based on the types of all Pokémon in my team.
Highlight any types that are a "gap" (4x weakness or multiple weaknesses).
```

### Expected Result
- Weakness analysis
- Resistance display
- Gap warnings

### What's Likely Missing
- ❌ Dual-type calculations may be wrong
- ❌ Display may be cluttered

**Iteration count: 7**

---

## Step 8: Add Multiple Teams

```
Let me save multiple teams with custom names:
1. Add a "Save Team" button that prompts for a team name
2. Show a list of saved teams
3. Click a saved team to load it
4. Add a delete button for saved teams
5. Store all teams in localStorage
```

### Expected Result
- Team saving with names
- Team list
- Load/delete functionality

**Iteration count: 8**

---

## Step 9: Add Stat Comparison

```
Add a compare feature:
1. Button to "Compare" on Pokémon cards
2. Can select 2-3 Pokémon to compare
3. Show their stats side-by-side in a comparison view
4. Highlight which Pokémon has the best stat in each category
```

### Expected Result
- Multi-select for comparison
- Side-by-side stats
- Best stat highlighting

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
- Keep the Pokémon type colors for badges
```

### Expected Result
- Professional Microsoft-style design
- Consistent spacing and typography
- Smooth hover animations
- Pokémon colors preserved

**Iteration count: 10**

---

## Step 11: Polish and Fix Issues

```
Fix any remaining issues:
1. Add loading spinners when fetching Pokémon data
2. Handle API errors gracefully
3. Make the layout responsive for mobile
4. Add empty state for team slots
5. Add smooth animations when adding/removing from team
```

### Expected Result
- Loading states
- Error handling
- Responsive design
- Animations

**Iteration count: 11**

---

## Step 12: Final Touches

```
Final polish:
1. Add app title "Pokémon Team Builder" with a Pokéball icon in the header
2. Add a "Random Team" button that fills the team with 6 random Pokémon
3. Add total base stats for each Pokémon and team average
4. Show shiny sprite toggle (sprites.front_shiny)
5. Add Pokémon cry sound when clicking on them (cries.latest from API)
```

### Expected Result
- Complete, polished application
- Fun features (random team, shiny, cries)
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

3. **Did the type effectiveness calculations work correctly the first time?**
   - Dual-type calculations are often tricky

4. **How would you describe the conversation efficiency?**
   - Lots of back-and-forth?
   - Context getting lost?

5. **What if you needed to rebuild this app?**
   - Would you remember all the prompts?
   - Could someone else replicate your result?

---

## Common Issues & Fixes

### API Rate Limiting
```
PokéAPI is free but requests should be reasonable. If you're loading many
Pokémon at once, add a small delay between requests or use Promise.all
with batching.
```

### Sprites Not Loading
```
Some Pokémon don't have all sprite variants. Add fallback logic:
sprite = pokemon.sprites.other['official-artwork'].front_default 
      || pokemon.sprites.front_default 
      || '/placeholder.png'
```

### Type Effectiveness Wrong
```
Type effectiveness for dual-types multiplies. Fire/Flying vs Ground:
- Fire is weak to Ground (2x)
- Flying is immune to Ground (0x)
- Result: 0x (immunity wins)

Make sure to multiply the effectiveness values, not add them.
```

### Stats Bars Not Proportional
```
Base stats range from ~1 to 255. Use max stat of 255 for the progress bar:
width: (stat / 255) * 100%
```

---

## Final Checklist

Before moving to Lab 2, verify your app has:

- [ ] Search Pokémon by name
- [ ] Browse by generation
- [ ] Detailed Pokémon card with stats
- [ ] Correct type colors (18 types)
- [ ] Stat bars visualization
- [ ] Team panel (6 slots)
- [ ] Add to team functionality
- [ ] Remove from team
- [ ] Duplicate prevention
- [ ] LocalStorage persistence
- [ ] Type effectiveness analysis
- [ ] Multiple saved teams
- [ ] Stat comparison view
- [ ] Fluent 2.0 styling
- [ ] Responsive layout
- [ ] Loading states
- [ ] Error handling
- [ ] Random team feature

---

## Key Takeaway

**Vibe coding works, but it's inefficient.**

You likely spent 12+ prompts and significant back-and-forth to build this app. The type effectiveness calculations alone probably required multiple iterations to get right.

In **Lab 2**, you'll see how a comprehensive upfront specification can achieve the same result in a **single prompt** - dramatically reducing iteration overhead and improving output consistency.

---

## Next Steps

→ Proceed to **Lab 2: Spec-Driven Development** to compare approaches
