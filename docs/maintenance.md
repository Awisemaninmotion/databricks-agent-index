# Maintenance Guide: databricks-agent-index

This document outlines how to maintain the `INDEX.md` scaffolding in your Databricks environment.

## Why Maintenance Matters
The system relies on the `INDEX.md` files being accurate. If the map does not match the territory, the agent will "wander" and lose efficiency.

## Routine Tasks

### 1. Weekly Sync (Recommended)
Run the `scripts/generate_index.py` script once a week (or after major manual changes) to ensure all manually created files are indexed.
1. Open the Databricks Notebook containing the script.
2. Update `ROOT_PATH` if necessary.
3. Run the cell.
4. Review the output log for any "Updating" messages.

### 2. Agent-Driven Updates
If your agent has file write permissions, it should update the `INDEX.md` automatically when it creates new files.
- **Verification:** After a long session, ask the agent: "Did you update the index for the new files you created?"
- **Manual Check:** Open the `INDEX.md` in the folder where you know new files were added and verify they are listed.

## Troubleshooting

### "Agent says file not found"
1. Check if the file exists in the folder.
2. Check if the `INDEX.md` lists it.
3. If the file exists but isn't listed, run the `generate_index.py` script to refresh the map.

### "Agent is confused by too many files"
If a folder has grown too large (e.g., >50 files):
1. Consider splitting the folder into subfolders (e.g., `01.Q1_Reports`, `02.Q2_Reports`).
2. Run the script to generate new `INDEX.md` files for the subfolders.
3. Update the parent `INDEX.md` to point to the new subfolders.

### "Archive Folder is cluttered"
The `06.Archived` folder should be treated differently.
- Do not let the agent actively search here unless requested.
- If the archive grows too large, consider moving old items to a separate "Cold Storage" path and updating the `INDEX.md` to point to that path instead of listing every file.

## Best Practices
- **Numbering:** Always use `01.`, `02.` prefixes for new folders/files. This ensures the agent reads them in the correct order.
- **One Concern Per Folder:** Do not mix Data, Analysis, and Strategy in the same folder.
- **No Deep Nesting:** Keep the hierarchy to 2-3 levels maximum. Deep nesting slows down the agent's navigation.