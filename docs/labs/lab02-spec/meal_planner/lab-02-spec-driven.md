# Lab 2: Spec-Driven Development

> **Duration**: 45-60 minutes  
> **Approach**: Single-prompt with comprehensive specification  
> **Tools**: GitHub Copilot (Agent Mode) or Cline  
> **API**: TheMealDB (free, no API key required)

---

## Learning Objectives

By the end of this lab, you will:
- Use a comprehensive specification to generate a complete application
- Experience the efficiency of upfront context engineering
- Compare results with the iterative approach from Lab 1
- Understand what makes a specification "AI-complete"

---

## The Spec-Driven Approach

Instead of 12+ iterative prompts, you'll provide a **single, comprehensive specification** that contains everything the AI needs to build the complete application.

**Key Insight**: The time spent writing a detailed spec is recovered many times over through:
- Reduced iteration cycles
- Fewer regressions
- Consistent output quality
- Reproducible results

---

## Instructions

### Step 1: Create a New Project Folder

Create a fresh folder (different from Lab 1) to build the spec-driven version.

### Step 2: Copy the Complete Specification

Copy the entire specification below and paste it as your **single prompt** to the AI assistant.

### Step 3: Let It Build

Watch as the AI generates the complete application in one pass.

### Step 4: Compare Results

Compare the output with your Lab 1 result:
- Feature completeness
- Code quality
- Design consistency
- Time spent

---

## The Complete Specification

The full specification for this application is available as a standalone file:

📄 **[meal-planner-spec.md](../../../specs/meal-planner-spec.md)**

### Instructions

1. Open the specification file linked above
2. Copy the **entire contents** of the specification
3. Paste it as your single prompt to the AI assistant
4. Watch as the complete application is generated

---

## After Generation

### Testing Checklist

Verify all features work:

- [ ] Search "chicken" returns results
- [ ] Click "Seafood" category filters correctly
- [ ] Random button fetches new meal
- [ ] Meal details load with ingredients
- [ ] Week displays Mon-Sun with correct dates
- [ ] Today is highlighted
- [ ] Previous/Next week navigation works
- [ ] Today button returns to current week
- [ ] Meals added appear in correct slot
- [ ] Meals persist after page refresh
- [ ] Remove button deletes meal
- [ ] List updates when meals added/removed
- [ ] Ingredients grouped correctly
- [ ] Checkboxes toggle and persist
- [ ] "Clear Checked" removes checked items
- [ ] "Copy List" copies to clipboard
- [ ] Duplicate ingredients combined
- [ ] Heart toggles filled/empty
- [ ] Favorites appear in sidebar
- [ ] Favorites persist after refresh
- [ ] Can add favorite to calendar
- [ ] Brand color (#0078D4) used correctly
- [ ] Cards have proper shadow and hover lift
- [ ] Smooth 200ms transitions
- [ ] Focus outlines visible
- [ ] Mobile layout works

### Common Adjustments

If the AI missed something, you might need:

```
The calendar isn't showing today highlighted. Add this logic:
const today = new Date().toISOString().split('T')[0];
if (dateStr === today) {
  dayColumn.classList.add('today');
}
```

```
Shopping list ingredients aren't grouping properly. Make sure to use:
const category = categorizeIngredient(ingredient);
grouped[category].push(item);
```

---

## Comparison: Vibe Coding vs Spec-Driven

| Aspect | Vibe Coding (Lab 1) | Spec-Driven (Lab 2) |
|--------|--------------------|--------------------|
| Prompts Required | 12+ | 1 |
| Time to Complete | 45-60 min | 30-45 min |
| Consistency | Variable | High |
| Feature Completeness | Often needs fixes | Usually correct |
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
1. Start with vibe coding to explore
2. Document what works
3. Convert learnings to specification
4. Generate final version from spec
5. Iterate from solid foundation

---

## Reflection Questions

1. **How many fixes did the spec-driven version need?**
   - Likely fewer than vibe coding

2. **Which features were more complete?**
   - Compare shopping list implementation

3. **How long could you maintain each version?**
   - Spec serves as documentation

4. **What would you add to the specification?**
   - Edge cases? Animation details? Performance?

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

- 🌍 **Country Explorer**: Build a travel bucket list app with REST Countries API
- 🎬 **Movie Tracker**: Create a watchlist app with OMDb API
- ⚡ **Pokémon Team Builder**: Create a team building app with PokéAPI
