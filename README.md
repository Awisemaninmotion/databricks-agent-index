# databricks-agent-index
Tired of your Databricks AI agents losing context during sessions? Optimize them with this structured workflow using numbered folders and INDEX.md maps for rapid 30s context retrieval. Includes Python scripts to auto-generate maps and system prompts to prevent agent "wandering." Ensures consistent, session-aware navigation across your data vault.

# TLDR
A Databricks-native workflow to optimize AI agent navigation and context retrieval using a structured `INDEX.md` scaffolding system.

## 🚀 Overview
AI agents often waste time and tokens "wandering" through file systems to find context. This repository implements a **concern-based hierarchy** with numbered folders and root-level `INDEX.md` maps. 

This system ensures your Databricks agent:
1.  **Retrieves context in <30 seconds** by reading a map first.
2.  **Maintains consistency** across sessions by updating the index dynamically.
3.  **Avoids hallucination** by strictly adhering to the defined "Canonical Files."

## 📦 What's Inside
- **`prompts/system_prompt.txt`**: The system instruction set for your Databricks agent.
- **`scripts/generate_index.py`**: A Databricks Notebook script to auto-scan and build/update `INDEX.md` files.
- **`examples/sample_vault/`**: A demo folder structure showing the pattern in action.
- **`docs/maintenance.md`**: Guide on how to keep the index fresh.

## 🛠️ Quick Start

### Step 1: Initialize the Structure
1.  Copy the `examples/sample_vault` folder to your Databricks workspace (e.g., `dbfs:/Workspace/Shared/MyProject`).
2.  Or, create your own folder structure following the `01.<Concern>` numbering convention.

### Step 2: Generate Initial Index
1.  Open a new **Databricks Notebook**.
2.  Copy the contents of `scripts/generate_index.py` into a cell.
3.  Update the `ROOT_PATH` variable to your project root.
4.  Run the cell. This will create `INDEX.md` files in all major folders.

### Step 3: Configure Your Agent
1.  Open your Databricks Agent configuration (or your LLM chat interface).
2.  Paste the contents of `prompts/system_prompt.txt` into the **System Prompt** field.
3.  Ensure the agent has **file write permissions** (via `dbutils.fs`) if you want it to update the index automatically.

## 🧠 How It Works
1.  **The Map:** Every major folder has an `INDEX.md` that lists subfolders, canonical files, and the "Where to Go" starting point.
2.  **The Cage:** The agent is instructed to read the `INDEX.md` *before* opening any other file. This constrains the search space.
3.  **The Update:** When the agent creates a new file, it updates the `INDEX.md`. When you add files manually, run the script to sync the map or trigger it with a /skill.

## 📚 Documentation
- See `docs/maintenance.md` for a guide on handling sync issues and manual updates.
- See `examples/sample_vault` to see the expected file naming convention.

## 📄 License
MIT License.
