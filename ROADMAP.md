# AnyList Meal Planner - Roadmap

## What is this?

AI-assisted meal planning using Claude Code and AnyList. Claude reads your preferences and constraints, then manages your meal calendar and shopping lists.

## Current Status: MVP

Basic structure in place with control documents. Waiting on mcp-anylist recipe CRUD tools for full functionality.

## Current Sprint

### Done

- [x] Project structure
- [x] MCP configuration (`.mcp.json`)
- [x] CLAUDE.md with planning workflow
- [x] Control documents (dietary, preferences, budget, shopping)
- [x] Decision tracking template
- [x] Recipe cache template

### Blocked / Waiting

- [ ] **Recipe CRUD in mcp-anylist** - Need `anylist_create_recipe` to upload AI-generated recipes
- [ ] Test with real AnyList account

### Up Next

- [ ] Recipe sync system (pull from AnyList, cache locally, detect changes)
- [ ] First-run initialization workflow
- [ ] Recipe generation guidelines in CLAUDE.md

## Feature Backlog

### Recipe Management

- [ ] Local recipe cache (format TBD: JSON? Markdown? SQLite?)
- [ ] Change detection (hash comparison or timestamps)
- [ ] Sync strategy (full sync vs incremental)
- [ ] AI recipe generation format/template
- [ ] Upload generated recipes to AnyList

### Planning Intelligence

- [ ] Ingredient overlap optimization
- [ ] Seasonal recipe suggestions
- [ ] Budget tracking per meal
- [ ] Leftover utilization planning
- [ ] "Haven't made this in a while" suggestions

### Shopping Integration

- [ ] Auto-generate shopping list from meal plan
- [ ] Pantry/staples awareness (don't add what you have)
- [ ] Store section grouping

## Architecture Decisions Needed

1. **Recipe cache format** - How to store synced recipes locally?
   - JSON file (simple, single file)
   - Markdown files (human-readable, git-friendly)
   - SQLite (queryable, but heavier)

2. **Change detection** - How to know if AnyList recipes changed?
   - Hash the recipe content
   - Track `lastModified` timestamps
   - Full re-sync each session (simplest)

3. **Recipe generation format** - What structure for AI-generated recipes?
   - Match AnyList's internal format exactly
   - Use a template that maps to AnyList fields

## Dependencies

| Dependency | Status | Notes |
|------------|--------|-------|
| mcp-anylist | ✅ Ready | Meal planning, labels, shopping lists work |
| Recipe read | ✅ Ready | `anylist_get_recipes` exists |
| Recipe write | ❌ Needed | `anylist_create_recipe` not yet implemented |
| anylist-api PR | ⏳ Pending | Label CRUD submitted, awaiting merge |

## Version History

| Version | Date | Highlights |
|---------|------|------------|
| 0.1.0 | 2026-02-15 | Initial structure with control documents |
