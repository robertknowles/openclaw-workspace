# Skill: brave-search

This skill documents how to use the Brave Search API for research tasks within OpenClaw.

## 1. When to Use This Skill

Use this skill for:
- Any task requiring internet research
- Finding companies, contacts, or business information
- Market research or competitor analysis
- Discovering industry trends or news
- Verifying business details (websites, locations, services)

## 2. How to Use Brave Search API

### Authentication
The Brave Search API key is stored in the OpenClaw config at `env.BRAVE_API_KEY`.

### Using the web_search Tool

Call the `web_search` tool with the following parameters:

| Parameter | Type | Description |
|-----------|------|-------------|
| `query` | string | Search query string |
| `count` | number | Number of results to return (1-10) |
| `country` | string | 2-letter country code (e.g., 'AU', 'US') |
| `freshness` | string | Filter by time: 'pd' (day), 'pw' (week), 'pm' (month), 'py' (year) |

### Example Query

```
web_search(
  query: "investment buyers agents Sydney",
  count: 5,
  country: "AU"
)
```

### Query Formatting Tips
- Use specific, targeted keywords
- Include location for local searches (e.g., "Sydney", "Melbourne")
- Add qualifiers like "top", "best", "reviews" for ranked results
- Use quotes for exact phrase matching

## 3. Output Format

### Required Fields
Always extract and include:
- **Company/Entity Name**: The name of the business or organization
- **Website URL**: The primary website link
- **Description**: A brief summary of what they do

### File Naming Convention
Save results to `memory/research/` with descriptive filenames:
- `memory/research/companies/<location>-<industry>.md`
- `memory/research/competitors/<company-name>-analysis.md`
- `memory/research/market/<topic>-research.md`

### Markdown Table Format

```markdown
# [Research Topic] - Search Results

Search performed: [DATE]
Source: Brave Search API
Query: "[SEARCH QUERY]"

## Results

| Company | Website | Description |
|---------|---------|-------------|
| Company A | https://example.com | Brief description... |
| Company B | https://example2.com | Brief description... |
```

## 4. Example Workflow

### Step 1: Receive Research Request
Example: "Find investment buyers agents in Brisbane"

### Step 2: Format Search Query
```
query: "investment buyers agents Brisbane Australia"
count: 5
country: "AU"
```

### Step 3: Call Brave API
Use the `web_search` tool with the formatted query.

### Step 4: Parse Results
Extract from each result:
- `title` → Company name
- `url` → Website
- `description` → Brief description (clean up HTML tags)

### Step 5: Save to File
Write results to `memory/research/companies/brisbane-buyers-agents.md`

### Step 6: Update Google Sheet (if applicable)
Use the sheet-tracker skill to update the PropPath Tracker with:

## 5. Common Mistakes to Avoid

- **Don't** skip saving results to memory - always persist research
- **Don't** return raw API output - clean and format the data
- **Don't** forget to include the search date for freshness context
- **Don't** use overly broad queries - be specific

## 6. Integration with Other Skills

This skill works well with:
- **company-research-ranking**: After finding companies, use this skill to rank them
- **sheet-tracker**: For updating the PropPath Tracker Google Sheet
- **browser-automation**: For deeper research on specific companies found

## 7. Troubleshooting

### API Key Issues
If you get authentication errors:
1. Check `env.BRAVE_API_KEY` is set in config
2. Verify the key is valid and active
3. Restart the gateway after config changes

### No Results
If search returns no results:
1. Simplify the query
2. Remove location qualifiers
3. Try alternative keywords
