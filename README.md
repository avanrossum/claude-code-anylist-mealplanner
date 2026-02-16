# AnyList Meal Planner

AI-assisted meal planning using Claude Code and AnyList.

## What is This?

This project provides a structured environment for using Claude Code to plan weekly meals, manage recipes, and coordinate shopping lists through the AnyList app.

Claude reads your preferences, dietary restrictions, and budget constraints from the docs in this folder, then uses MCP tools to interact with your AnyList account.

## Requirements

### 1. AnyList Account

You need an [AnyList](https://www.anylist.com/) account (the meal planning features require AnyList Complete subscription).

### 2. mcp-anylist (AnyList MCP Server)

This project requires the `mcp-anylist` MCP server to communicate with AnyList.

**Option A: Install from npm** (when published)
```bash
npx mcp-anylist --setup
```

**Option B: Install from GitHub** (current)
```bash
# Clone the MCP server repo
git clone https://github.com/avanrossum/mcp-anylist.git
cd mcp-anylist
npm install

# Run setup to authenticate with AnyList
node src/index.js --setup
```

The setup will prompt for your AnyList email and password, then store your credentials securely in `~/.mcp-anylist-credentials`.

> **Note:** If you installed from GitHub, update `.mcp.json` in this project to point to your local installation:
> ```json
> {
>   "mcpServers": {
>     "anylist": {
>       "command": "node",
>       "args": ["/path/to/mcp-anylist/src/index.js"]
>     }
>   }
> }
> ```

### 3. Claude Code

Install Claude Code: [CLI](https://docs.anthropic.com/en/docs/claude-code) or [Desktop App](https://claude.ai/download).

## Setup

1. **Clone or copy this project** to your local machine

2. **Configure your preferences** by editing the files in `docs/`:
   - `dietary-restrictions.md` - Allergies, medical diets, etc.
   - `family-preferences.md` - Likes, dislikes, comfort foods
   - `budget.md` - Weekly spending limits
   - `shopping-preferences.md` - Store preferences, ingredient strategies

3. **Run Claude Code** in this project:

   **Desktop App (Recommended):**
   - Open Claude Code Desktop
   - Click "Open Project" or drag this folder into the window
   - The MCP server will connect automatically

   **CLI:**
   ```bash
   cd claude-code-anylist-mealplanner
   claude
   ```

4. **Start planning!** Try:
   - "Plan dinners for next week"
   - "What meals do I have planned?"
   - "Add ingredients for Tuesday's dinner to my shopping list"

## Project Structure

```
claude-code-anylist-mealplanner/
├── .mcp.json                    # MCP server configuration
├── CLAUDE.md                    # Instructions for Claude
├── README.md                    # This file
└── docs/
    ├── dietary-restrictions.md  # Health/medical diet needs
    ├── family-preferences.md    # Food preferences
    ├── budget.md                # Spending constraints
    ├── shopping-preferences.md  # Shopping strategies
    ├── decisions.md             # Planning history
    └── recipe-cache.md          # Frequently used recipes
```

## How It Works

1. **Claude reads your context** from the docs folder
2. **You request a meal plan** ("Plan next week's dinners")
3. **Claude proposes options** based on your constraints
4. **You approve the plan**
5. **Claude writes to AnyList** via MCP tools
6. **Decisions are logged** for future reference

## Tips

- **Start simple** - Plan a few days before doing a full week
- **Update preferences** - Add notes when you discover new likes/dislikes
- **Review decisions** - Check `docs/decisions.md` periodically
- **Be specific** - "Quick weeknight meals under 30 minutes" gets better results

## Privacy

Your AnyList credentials are stored locally in `~/.mcp-anylist-credentials` (encrypted). The docs in this folder contain your personal preferences — don't commit them to a public repo.

## License

MIT
