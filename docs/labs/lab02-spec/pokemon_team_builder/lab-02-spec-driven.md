# Lab 2: Spec-Driven Pokémon Team Builder

> **Duration**: 30-45 minutes  
> **Approach**: Single comprehensive prompt  
> **Tools**: GitHub Copilot (Agent Mode) or Cline  
> **API**: PokéAPI (free, no API key required)

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
- Provides type effectiveness calculation logic
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

📄 **[pokemon-team-builder-spec.md](../../../specs/pokemon-team-builder-spec.md)**

### Instructions

1. Open the specification file linked above
2. Copy the **entire contents** of the specification
3. Paste it as your single prompt to the AI assistant
4. Watch as the complete application is generated

---

## After Generation

### Testing Checklist

Verify all features work:

- [ ] Generation buttons load Pokémon
- [ ] Search filters results in real-time
- [ ] Clicking card opens detail modal
- [ ] Stats show as proportional bars
- [ ] Type badges have correct colors
- [ ] "Add to Team" adds Pokémon to team panel
- [ ] Can't add duplicates (toast warning)
- [ ] Can remove Pokémon from team
- [ ] Type effectiveness updates for team
- [ ] "Save Team" stores team with custom name
- [ ] Saved teams can be loaded
- [ ] Compare feature shows side-by-side stats
- [ ] "Random Team" fills with 6 random Pokémon
- [ ] Refresh preserves current team
- [ ] Shiny toggle works in modal
- [ ] Play Cry plays audio
- [ ] Works on mobile viewport

### Common Adjustments

If the AI missed something, you might need:

```
The sprites aren't loading for some Pokémon. Add fallback logic:
const sprite = pokemon.sprites.other?.['official-artwork']?.front_default 
            || pokemon.sprites.front_default;
```

```
The type effectiveness is calculating wrong for dual-types. Make sure to:
1. Fetch type data for BOTH types
2. MULTIPLY the effectiveness values (not add)
3. 0x always wins (immunity)
```

```
The generation buttons aren't styled. Add these styles for the active state:
.gen-btn.active {
  background: var(--brand-primary);
  color: white;
}
```

---

## Comparison: Vibe Coding vs Spec-Driven

| Aspect | Vibe Coding (Lab 1) | Spec-Driven (Lab 2) |
|--------|--------------------|--------------------|
| Prompts Required | 12+ | 1 |
| Time to Complete | 45-60 min | 30-45 min |
| Consistency | Variable | High |
| Type Effectiveness | Often needs fixes | Usually correct |
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

## Extending the Application

Ideas for further development:

1. **Move animations**
   - Fetch moves from `/pokemon/{id}` 
   - Show move type coverage

2. **Evolution chains**
   - Use `/evolution-chain/{id}`
   - Show evolutionary path

3. **Team export**
   - Export team as shareable link
   - Import teams from others

4. **Competitive formats**
   - Filter by tier (OU, UU, etc.)
   - Show usage statistics

5. **Battle simulator**
   - Calculate damage against opponent
   - Type matchup predictor

---

## Reflection Questions

1. **How many fixes did the spec-driven version need?**
   - Likely fewer than vibe coding

2. **Which features were more complete?**
   - Compare type effectiveness implementation

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
- 🍳 **Meal Planner**: Build a recipe and meal planning app with TheMealDB
