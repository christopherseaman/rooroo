# 🚀 rooroo (如如): Minimalist AI Orchestration with Specialist Agents 🚀

**Version: v0.6.3** | [Changelog](changelog.md) | [v0.6.0 Details](v0.6.0.md) | [v0.5.0 Details](v0.5.0.md)

`rooroo` is a **minimalist AI orchestration framework** for VS Code, designed to streamline software development using a team of specialized Rooroo agents. It emphasizes a clear, Navigator-led workflow, efficient task management, and robust communication, all while incorporating advanced prompting techniques for enhanced reliability.

## 🤔 The Philosophy: "rooroo (如如)" - Thusness

Inspired by Buddhist philosophy, "如如" (rú rú) or "Thusness" reflects the idea of an underlying, consistent nature. This informs `rooroo`'s minimalist approach, focusing on the essential, specialized role of each agent.

![img](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQeUmsB4LIHLErFEbei5g8PfIFG-XQntgqLyA&s)

## ⚙️ Core Principles
*   **Navigator-Led Orchestration:** The **🧭 Rooroo Navigator** is your central guide, managing task flows, user interactions, and expert agent coordination with concise communication.
*   **Specialized Agent Team:** A lean team of focused AI agents:
    *   **🗓️ Rooroo Planner:** Decomposes complex goals.
    *   **🧑‍💻 Rooroo Developer:** Crafts code and UIs.
    *   **📊 Rooroo Analyzer:** Investigates and delivers insights.
    *   **✍️ Rooroo Documenter:** Creates clear documentation.
    *   **💡 Rooroo Idea Sparker:** Acts as a Strategic Foresight Facilitator, guiding users through a structured process to explore problems, evaluate solutions, and produce a detailed **Handoff Document**. This document serves as a comprehensive blueprint, ready for delegation to execution agents. Its outputs are stored in `.rooroo/brainstorming/`.
*   **Structured Workflow & Communication:**
    *   **Task Management:** Uses `.rooroo/queue.jsonl` for pending tasks.
    *   **Detailed Briefings:** Tasks are detailed in `.rooroo/tasks/TASK_ID/context.md`, prioritizing links over embedded content.
    *   **Organized Artifacts:** Outputs are stored in `.rooroo/tasks/TASK_ID/`.
    *   **Clear Reporting:** Agents use a structured JSON "Output Envelope" to report to the Navigator.
    *   **Event Logging:** Key events are logged with severity in `.rooroo/logs/activity.jsonl`.
*   **Key Operational Guidelines:**
    *   **Minimalism & Specialization:** Focused roles for clarity.
    *   **Concise Context (Link, Don't Embed):** Efficient briefings.
    *   **Principle of Least Assumption:** Agents clarify ambiguities, don't guess.
    *   **Consistent Task IDs:** `ROO#` prefixes for easy tracking.
    *   **Cost-Effectiveness:** Uses appropriate LLM tiers per agent.
    *   **Workspace-Relative Paths:** Simplifies file referencing.
    *   **Customizable Agent Behavior (Optional):** Utilize the `.roo/rules/` directory for workspace-wide custom instructions to tailor agent behavior, aligning with Roo Code best practices for organization and potential performance improvements.

## Installation

RooRoo supports both **project-specific** and **global** installation approaches.
- **Project-Specific Installation:** applies only to one specific project
- **Global Installation:** will apply to ALL projects where you use Roo Code

### Prerequisites

1. **Install Roo Code Extension**: Ensure the [Roo Code VS Code extension](https://marketplace.visualstudio.com/items?itemName=RooVeterinaryInc.roo-cline) is installed
2. **API Keys**: Configure your preferred LLM provider API keys or CLI tools (e.g., Claude Code) in Roo Code settings

#### Download rooroo

Start by downloading or cloning this repository. Both local and global installation options require the same core files from the rooroo repository:
- `.roomodes` file (can be YAML or JSON format for local install)
- `.roo/` directory with custom rules and instructions

### Installation Options

#### Option 1: Project-Specific Installation

Install RooRoo for a single project. The configuration only applies to the current project.

Copy the following files to your project root:
- `.roomodes` or `.roomodes.json` (RooRoo mode definitions - can be YAML or JSON format)
- `.roo/` directory (custom rules and instructions)


**File Structure:**
```
your-project/
├── .roomodes              # RooRoo mode definitions
├── .roo/                  # Custom rules and instructions
│   └── rules/             # Agent-specific rules
└── ... (your project files)
```

#### Option 2: Global Installation

Install RooRoo globally. The same configuration applies to all projects automatically.

Copy the `.roomodes` file to your global Roo Code settings directory as `custom_modes.yaml`:

**Windows:**
`%APPDATA%/Code/User/globalStorage/rooveterinaryinc.roo-cline/settings/custom_modes.yaml`

**macOS:**
`~/.vscode/User/globalStorage/rooveterinaryinc.roo-cline/settings/custom_modes.yaml`

**Linux:**
`~/.vscode/User/globalStorage/rooveterinaryinc.roo-cline/settings/custom_modes.yaml`

**Note**: #FIXME:wrong https://docs.roocode.com/features/custom-instructions?_highlight=rules#rules-about-rules-files ; Global installation only includes the mode definitions. The `.roo/rules/` directory contains workspace-level and mode-specific custom instructions that are project-specific and should be copied to individual projects where needed.


### Verify Installation

After installation:

1. **Open Roo Code panel** (click the Roo icon in the Activity Bar)
2. **Check available modes** - you should see RooRoo agents like:
   - 🧭 Rooroo Navigator (Your Project Coordinator!)
   - 🗓️ Rooroo Planner
   - 🧑‍💻 Rooroo Developer
   - 📊 Rooroo Analyzer
   - ✍️ Rooroo Documenter
   - 💡 Rooroo Idea Sparker

## 🚀 Quick Start & Core Workflow

Using `rooroo` involves these main steps:

1.  **Setup:** Install [Roo Code VS Code extension](https://marketplace.visualstudio.com/items?itemName=RooVeterinaryInc.roo-cline).
    *   Load your `.roomodes` file.
        *   **For Roo Code v3.18.0 and later:** You can use the YAML format for `.roomodes`.
        *   **For Roo Code versions earlier than v3.18.0:** You must use the JSON format for `.roomodes` (e.g., `.roomodes.json`).
    *   Reload VS Code.
    *   (Optional: For advanced customization, create a `.roo/rules/` directory and add custom instruction files to tailor agent behavior across your workspace.)
2.  **Initiate:** Select **🧭 Rooroo Navigator** and state your goal.
3.  **Navigator Triage:** The Navigator assesses your request:
    *   For *complex/uncertain tasks*, it engages the **🗓️ Rooroo Planner** to break it down into sub-tasks with `context.md` briefings. These go into the `.rooroo/queue.jsonl`.
    *   For *simple, clear single-expert tasks* (Developer, Analyzer, Documenter only), it prepares `context.md` and may execute directly or queue the task.
    *   If *ambiguous*, it asks you for clarification.
4.  **Execution:** The Navigator dispatches tasks from the queue to the assigned Rooroo expert. The expert uses its `context.md` and stores outputs in `.rooroo/tasks/TASK_ID/`.
5.  **Reporting:** The expert returns a JSON **Output Envelope** (status, message, artifacts) to the Navigator.
6.  **Processing & Iteration:** The Navigator parses the envelope:
    *   `NeedsClarification`: Relays question to you.
    *   `Done`/`Failed`: Logs event, updates queue, informs you. Auto-proceeds with plans if applicable.
7.  **Monitor:** Track progress via `.rooroo/queue.jsonl` and `.rooroo/logs/activity.jsonl`.

*(Refer to the Workflow Diagram below for a visual representation.)*

## 🤖 The Agent Team at a Glance

Each Rooroo agent adheres to core principles like the **Principle of Least Assumption** and **Concise Context File Preparation** (linking over embedding).

*   **🧭 Rooroo Navigator (⚡ Cheap/Fast Recommended):** Your primary interface. Manages interactions, triages tasks, dispatches from the queue, processes expert reports, and logs events. Prioritizes concise communication.
*   **🗓️ Rooroo Planner (🧠 Smart/Expensive Recommended):** Decomposes complex goals into sub-tasks for the Developer, Analyzer, or Documenter. Creates their `context.md` briefings and can flag ambiguous expert choices for the Navigator to resolve.
*   **🧑‍💻 Rooroo Developer (Custom / Varies):** Executes coding tasks based on `context.md`. Stores outputs in its task folder or modifies project files.
*   **📊 Rooroo Analyzer (⚡ Cheap/Fast Recommended):** Performs analysis based on `context.md`. Generates reports in its task folder.
*   **✍️ Rooroo Documenter (⚡ Cheap/Fast Recommended):** Creates/updates documentation based on `context.md`. Stores outputs in its task folder.
*   **💡 Rooroo Idea Sparker (🧠 Smart/Expensive Recommended):** Acts as a Strategic Foresight Facilitator, guiding users through a structured process to explore problems, evaluate solutions, and produce a detailed **Handoff Document**. This document serves as a comprehensive blueprint, ready for delegation to execution agents. Its outputs are stored in `.rooroo/brainstorming/`.

*Balance LLM tiers per agent for optimal cost and capability.*

## 📁 Directory Structure at a Glance

`rooroo` uses a clear, workspace-relative structure under the `.rooroo/` directory for all its operations and artifacts.

```
<Project Root>/
├── .rooroo/                  # Core rooroo operational directory
│   ├── queue.jsonl           # Pending Tasks (JSON objects, one per line, ROO# IDs, strictly parsable)
│   ├── logs/
│   │   └── activity.jsonl    # Activity Log (JSON objects, one per line, written by Navigator with escaped JSON)
│   ├── rules/                # Optional: Workspace-wide custom instruction files (e.g., 01-general.md)
│   ├── tasks/                # Directory for all task-specific data
│   │   ├── ROO#PLAN_20240101120000_initial_project/ # Example Planner Task Directory
│   │   │   └── context.md      # Briefing FOR the Planner (concise, uses links)
│   │   ├── ROO#SUB_initial_project_S001/ # Example Sub-Task Directory (ROO#SUB_... ID from Planner)
│   │   │   ├── context.md      # Task briefing FOR the expert (Created by Planner, concise, uses links)
│   │   │   ├── feature_component.py # Example artifact directly in task folder
│   │   │   └── data_analysis_report.md # Another example artifact
│   │   ├── ROO#TASK_20240101130000_fix_login/ # Example Direct Task Directory (ROO#TASK_... ID from Navigator)
│   │   │   ├── context.md      # Task briefing FOR the expert (Created by Navigator, concise, uses links)
│   │   │   └── login_fix.diff    # Example artifact directly in task folder
│   │   └── ...
│   ├── plans/                # Optional: High-level plan overview documents from Rooroo Planner
│   │   └── ROO#PLAN_20240101120000_initial_project_plan_overview.md
│   └── brainstorming/        # Optional: Summaries from Rooroo Idea Sparker sessions
│       └── brainstorm_summary_ROO#IDEA_20240101140000.md
│
└── src/                      # Example source code directory (Potentially modified by Rooroo Developer)
    └── ...
```

## 📊 Core Data Files Explained

Key files driving `rooroo` operations:

*   **`.rooroo/queue.jsonl`:** Ordered list of tasks (JSON objects per line).
    *   *Defines:* What needs to be done, by which expert, with what goal and context.
    *   *Example Task:* `{"taskId": "ROO#SUB_...", "suggested_mode": "rooroo-developer", "context_file_path": ".rooroo/tasks/ROO#SUB_.../context.md", "goal_for_expert": "Build feature X..."}`
*   **`.rooroo/logs/activity.jsonl`:** Append-only log of key events with severity (INFO, ERROR, etc.).
    *   *Tracks:* What actions agents take and their outcomes.
    *   *Example Log:* `{"timestamp": "...", "agent_slug": "rooroo-navigator", "severity": "INFO", "task_id": "ROO#...", "event_type": "EXPERT_REPORT", "details": {"status": "Done"}}`
*   **`.rooroo/tasks/TASK_ID/context.md`:** The comprehensive Markdown briefing for an assigned agent.
    *   *Provides:* Detailed goals, requirements, and **links** to relevant files/artifacts (prioritizing links over embedding content).
*   **Output Artifacts:** Generated by experts (code, reports, docs) are stored directly in their respective task folders: `.rooroo/tasks/TASK_ID/` (e.g., `output.py`, `analysis_report.md`).

---

### Workflow Diagram (Visual)

```text
+----------------------------------------------------------------------+ Phase 0: Optional Brainstorming +----------------------------------------------------------------------+

[User Initiates Brainstorming with 💡 Rooroo Idea Sparker]

+----------------------------------------------------------------------+ Phase 1: User Interaction & Task Triage (Navigator) +----------------------------------------------------------------------+

[User Input (Goal)] -> [🧭 Rooroo Navigator] -> {Triage}
    |
    |--- (Complex/Uncertain) --> [Planner: Sub-tasks & context.md] --> [Navigator: Add to Queue]
    |
    |--- (Simple, Clear for Dev/Analyzer/Doc) --> [Navigator: Task & context.md] --> [Direct Exec or Queue]
    |
    |--- (Ambiguous) --> [Navigator: Clarify with User]
    |
    +--- ("Proceed"/Auto) --> [Phase 2] / (Needs Input) --> [Phase 4]

+----------------------------------------------------------------------+ Phase 2: Queued Task Dispatch (Navigator) +----------------------------------------------------------------------+

[Navigator: Check Queue] --(Not Empty)--> [Navigator: Read Task, Call Expert]
    |                                                               |
   (Empty) --> [Inform User, Phase 4]                             v
                                                      [Expert: Execute (uses context.md, creates artifacts)]
                                                                    | (Expert returns JSON Output Envelope)
                                                                    v
                                                                [Phase 3]

+----------------------------------------------------------------------+ Phase 3: Expert Report Processing (Navigator) +----------------------------------------------------------------------+

[Navigator: Receives JSON Output Envelope]
    |
    |--- ("NeedsClarification") --> [Navigator: Ask User] --> [Relay to Expert]
    |
    |--- ("Done"/"Failed") --> [Log, Update Queue, Inform User]
    |                             |
    |                             +-- (If "Failed") --> [Phase 4]
    |                             +-- (If "Done" & Queue Not Empty) --> [Phase 2]
    |                             +-- (If "Done" & Queue Empty) --> [Phase 4]

+----------------------------------------------------------------------+ Phase 4: User Decision Point (Navigator) +----------------------------------------------------------------------+

[Navigator: Prompts User for Decision/Next Steps] --> [Loop to Relevant Phase or Await New Input]
```

