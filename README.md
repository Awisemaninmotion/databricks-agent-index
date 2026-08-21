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

- ## 📜 Licensing & Usage

This project is **dual-licensed** to support community innovation while protecting commercial interests. The legal terms are defined in the **[LICENSE](LICENSE)** file (PolyForm Noncommercial 1.0.0).

# Please review the summary below to determine which license applies to your use case.

### 1. Non-Commercial Use (Free)
You may use this software for **free** if your use is strictly for **non-commercial purposes**. This explicitly includes:
*   **Personal Use**: Individual study, hobby projects, private entertainment, or amateur pursuits.
*   **Education**: Academic research, classroom teaching, or student projects.
*   **Non-Profits & Government**: Charitable organizations, public research institutions, government agencies, and public safety organizations (even if funded by grants).

**Requirements:**
*   ✅ You must give appropriate credit (attribution) to the original author.
*   ✅ You must include a copy of the license or a link to it.
*   ❌ **Restricted**: You **cannot** use this for any for-profit business operations, internal corporate workflows, or to generate revenue. If you are using it in a commercial setting, see the details outlined in the next section.

📄 *See the full [LICENSE](LICENSE) file for the complete legal text.*

### 2. Commercial Use (Paid License Required)
**You must purchase a Commercial License** if you are a **for-profit corporation, organization, or individual** intending to use this software for any business purpose.

This includes, but is not limited to:
*   **Corporate Integration**: Using the software within a company's internal Databricks environment, data vaults, or AI agent workflows to optimize business operations.
*   **Commercial Products**: Embedding this code into a software product, SaaS platform, or service that you sell, license, or offer to customers.
*   **Redistribution**: Copying, modifying, or distributing the software (or derivative works) to third parties for a fee or as part of a commercial offering.
*   **Cost Savings**: Using the software to reduce internal operational costs, increase efficiency, or generate indirect revenue for a for-profit entity.

> **Why this matters for Databricks Users:**
> If you are deploying this agent workflow in a **corporate Databricks workspace** (e.g., to manage your company's data, automate internal pipelines, or power a customer-facing feature), this is considered **Commercial Use**. The free version of this license does not cover for-profit business operations.

### 3. How to Get a Commercial License
If your use case falls under the **Commercial Use** section, we offer a **Commercial License** that grants you:
*   Full rights to use the software in commercial environments.
*   The right to integrate the software into your corporate Databricks environment.
*   The right to redistribute the software as part of your commercial offerings.
*   Optional support, warranty, and indemnification terms.

📩 **Contact Us for a License:**
To obtain a commercial license for your organization, please contact us:
*   **Email**: [adam@onlineworkflow.io]
*   **Website**: [https://www.onlineworkflow.io]
*   **Company**: [ONLINEWORKFLOW]

---

## 🤝 Contributing
We welcome contributions from the community! By submitting a pull request, you agree to release your contribution under the **PolyForm Noncommercial License** and grant the project maintainer the right to include your work in our **Commercial License** offerings. This ensures the project can remain sustainable for all users.

---

## ⚠️ Disclaimer
This software is provided "as is", without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose, and noninfringement. In no event shall the authors or copyright holders be liable for any claim, damages, or other liability, whether in an action of contract, tort, or otherwise, arising from, out of, or in connection with the software or the use or other dealings in the software.

## 📄 License
PolyForm Noncommercial 1.0.0
