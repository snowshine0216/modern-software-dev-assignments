# CS146S: Building a Coding Agent Recap

## 🏛️ The Four Pillars of Coding Agents

| Pillar | Concept | Implementation Detail |
| :--- | :--- | :--- |
| **1. Reasoning 🧠** | The ReAct Loop | A cycle of Thought → Action → Observation that allows the agent to process feedback. |
| **2. Capability 🛠️** | Dynamic Tool Registry | Using `inspect.signature` to automatically tell the LLM what tools are available. |
| **3. Communication 🌉** | The Parsing Bridge | Using Regex to translate the LLM's text into executable Python function calls. |
| **4. Security 🛡️** | Guardrails & Safety | Using sandboxes, "human-in-the-loop," and declarative changes to protect the system. |

## 🔄 The Lifecycle of a Fix

When our agent encounters a bug, it follows a specific sequence within its control loop:

1.  **Analyze**: The agent receives an error (e.g., an `AssertionError`) as an Observation. 🧐
2.  **Act**: It uses `read_file` to see the code and `write_file` to apply a hypothesized fix. ✍️
3.  **Verify**: It uses a tool like `run_command` to execute tests and ensure the fix works without breaking other things. ✅

## 🛡️ Best Practices for Robust Agents

*   **High-Signal Feedback**: Tools should return specific error messages (line numbers, expected vs. actual values) so the agent doesn't get stuck in an infinite loop. 📡
*   **Environment Integrity**: Avoid "Environment Drift" by having the agent modify dependency files (like `requirements.txt`) rather than running raw install commands. 🏗️
*   **Version Control**: Always run agents on a branch or worktree so that changes can be easily reverted if something goes wrong. 🕒