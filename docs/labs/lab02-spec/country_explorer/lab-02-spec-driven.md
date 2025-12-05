# Lab 2: Spec-Driven Country Explorer

> **Duration**: 30-45 minutes  
> **Approach**: Single comprehensive prompt  
> **Tools**: GitHub Copilot (Agent Mode) or Cline  
> **API**: REST Countries (free, no API key required)

---

## Learning Objectives

By the end of this lab, you will:
- Experience the power of comprehensive upfront specification
- Generate a complete application in a single prompt
- Compare output quality vs iterative "vibe coding"
- Understand the time savings of spec-driven development

---

## The Spec-Driven Approach

Instead of iterating through 12+ prompts, we'll provide a complete specification that:
- Defines all features upfront
- Specifies exact API endpoints and response handling
- Includes the complete design system
- Provides data transformation logic
- Details all UI components and interactions

**Goal**: One prompt → working application

---

## Instructions

1. Create a new empty project folder
2. Open it in VS Code
3. Copy the entire specification from the linked file
4. Paste it into your AI assistant as a single prompt
5. Wait for generation to complete
6. Test the application

---

## Complete Application Specification

The full specification for this application is available as a standalone file:

📄 **[country-explorer-spec.md](../../../specs/country-explorer-spec.md)**

### Instructions

1. Open the specification file linked above
2. Copy the **entire contents** of the specification
3. Paste it as your single prompt to the AI assistant
4. Watch as the complete application is generated

---

## After Generation

### Testing Checklist

Verify all features work:

- [ ] Countries load on page open
- [ ] Search filters in real-time
- [ ] Region filter works
- [ ] Sorting options work
- [ ] Clicking card opens detail modal
- [ ] Flag displays correctly
- [ ] Languages formatted correctly
- [ ] Currencies formatted correctly
- [ ] Border countries are clickable
- [ ] Google Maps link opens new tab
- [ ] Add to bucket list works
- [ ] Mark as visited works
- [ ] Can't be in both lists
- [ ] Statistics update correctly
- [ ] Regional breakdown shows progress
- [ ] Compare feature works
- [ ] Random country button works
- [ ] Dark mode toggle works
- [ ] Data persists on refresh
- [ ] Share stats copies to clipboard
- [ ] Works on mobile viewport

### Common Adjustments

If the AI missed something, you might need:

```
The flags aren't displaying. Make sure the img src uses country.flags.svg 
and add onerror fallback to flags.png:
<img src="${country.flags.svg}" 
     onerror="this.src='${country.flags.png}'"
     alt="${country.name.common} flag">
```

```
Border countries show as codes (USA, MEX) instead of names. Fetch each:

async renderBorderCountries(borders) {
  if (!borders || !borders.length) {
    return '<p>Island nation - no land borders</p>';
  }
  const names = await Promise.all(
    borders.map(code => 
      this.getCountryByCode(code)
        .then(c => ({ code, name: c.name.common }))
    )
  );
  return names.map(b => 
    `<button class="border-btn" data-code="${b.code}">${b.name}</button>`
  ).join('');
}
```

```
Statistics count is wrong. Make sure to count the actual array lengths:
const visitedCount = this.state.visited.length;
const bucketCount = this.state.bucketList.length;
```

---

## Comparison: Vibe Coding vs Spec-Driven

| Aspect | Vibe Coding (Lab 1) | Spec-Driven (Lab 2) |
|--------|--------------------|--------------------|
| Prompts Required | 12+ | 1 |
| Time to Complete | 45-60 min | 30-45 min |
| Consistency | Variable | High |
| Data Formatting | Often needs fixes | Usually correct |
| Design System | Gradual refinement | Complete from start |
| Reproducibility | Low | High |
| Context Loss | Yes, over iterations | No |
| Learning Value | High (exploration) | Moderate |

---

## Key Insights

### When to Use Spec-Driven Development

✅ **Use specs when:**
- Requirements are well-understood
- Design system is established
- API contracts are known
- Reproducibility matters
- Working with teams

### When Vibe Coding Works

✅ **Vibe code when:**
- Exploring new APIs
- Prototyping ideas
- Learning a new technology
- Requirements are unclear
- Personal projects

### The Sweet Spot

**Hybrid approach:**
1. Start with vibe coding to explore the API
2. Document what works (data transformations)
3. Convert learnings to specification
4. Generate final version from spec
5. Iterate from solid foundation

---

## Extending the Application

Ideas for further development:

1. **Interactive Map**
   - Use Leaflet.js to show world map
   - Color countries by visited/bucket list status
   - Click countries on map to view details

2. **Trip Planner**
   - Create trips combining multiple countries
   - Show travel route on map
   - Calculate total population visited

3. **Country Quizzes**
   - "Guess the flag" game
   - "Guess the capital" game
   - Track quiz scores

4. **Social Features**
   - Share profile link
   - Compare with friends
   - Global leaderboard

5. **Offline Support**
   - Cache country data in IndexedDB
   - PWA with service worker
   - Work without internet

---

## Reflection Questions

1. **How many fixes did the spec-driven version need?**
   - Likely fewer than vibe coding

2. **Which features were more complete?**
   - Compare data formatting between approaches

3. **How would you document the vibe-coded version?**
   - Much harder after the fact

4. **What would you add to the specification?**
   - Edge cases? Animation details? Error states?

---

## Summary

This lab demonstrated that **investing time in specification** pays dividends:

- **One prompt** replaced 12+ iterations
- **Complete features** from the start  
- **Consistent quality** across generations
- **Reproducible results** for team collaboration
- **Self-documenting** through the spec itself

The specification approach treats AI assistants as **code generators** rather than **conversation partners**, leading to more predictable and efficient development.

---

## Next Lab Options

- 🎬 **Movie Tracker**: Build a watchlist app with OMDb API
- ⚡ **Pokémon Team Builder**: Create a team building app with PokéAPI
- 🍳 **Meal Planner**: Build a recipe and meal planning app with TheMealDB
