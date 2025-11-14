# **✈️ Smart Travel Planner Agent**

This project implements a **Smart Travel Planner Agent**, a core application within the **Concierge Agents** track of the Google AI Agents Intensive Capstone Project. It showcases a robust multi-agent architecture designed to handle complex, multi-step personal planning tasks.

The agent takes unstructured requests from a user (e.g., destination, dates, budget) and orchestrates a series of specialized sub-agents and tools to generate a final, structured itinerary.

## **🌟 Key Features & Course Concepts Demonstrated**

This project fulfills the competition requirement by demonstrating **three essential AI Agent concepts**:

| Concept | Implementation Details |
| :---- | :---- |
| **1\. Multi-Agent System** | The solution uses a **Sequential Graph** orchestrated by LangGraph, involving three specialized nodes: Planner Agent (user interface/data collection), Tool Executor (API integration), and Itinerary Builder Agent (final output generation). |
| **2\. Tools (Function Calling)** | The system defines and uses three **Custom Tools** (search\_flights, Google Hotels, search\_activities) using Pydantic schemas. This simulates real-world API interaction and allows the LLM to perform external actions. |
| **3\. Sessions & Memory** | The TravelPlanState class acts as the centralized **session memory**, tracking the ongoing conversation history (messages), collected user constraints (plan\_criteria), and the raw data from tools (plan\_data) to maintain context across turns. |
| **Bonus:** **Effective Use of Gemini** | The core reasoning and conversational intelligence of all three agents are powered by the gemini-2.5-flash-preview-09-2025 model. |

## **🛠️ Agent Architecture**

The planning process follows a specific, goal-oriented flow, ensuring all criteria are met before the final itinerary is built.

### **Component Breakdown**

| Component | Type / Role in Graph | Primary Function |
| :---- | :---- | :---- |
| **Planner Agent** | Conversational Node (planner\_node) | **Gathers Criteria:** Handles initial user dialogue, validates input, collects missing details, and decides when all necessary data is ready to initiate tool calls. |
| **Tool Executor Node** | Function Node (call\_tool) | **Executes Tools:** Runs simulated API calls (search\_flights, Google Hotels, search\_activities) and stores the resulting data in the shared state (plan\_data). |
| **Itinerary Builder Agent** | Synthesis Agent (itinerary\_builder\_agent) | **Generates Output:** Takes all collected criteria and tool outputs and synthesizes them into the final, structured, day-by-day travel plan. |

### **Workflow Sequence**

1. **Input & Planning:** User provides input $\\rightarrow$ **Planner Agent** collects criteria.  
2. **Action:** Criteria are complete $\\rightarrow$ **Planner Agent** generates tool calls.  
3. **Execution:** Tool calls are generated $\\rightarrow$ **Tool Executor Node** executes functions.  
4. **Synthesis:** Tool outputs are collected $\\rightarrow$ **Itinerary Builder Agent** creates the final plan.  
5. **End:** The process terminates when the final plan is delivered.

## **🚀 Setup and Run Instructions**

This agent is implemented entirely within a single Python file, ready to run in any environment where Python and the required libraries are installed (e.g., Kaggle Notebook, Google Colab, or local terminal).

### **Prerequisites**

1. **API Key:** You must have a **Gemini API Key**.  
2. **Python:** Python 3.9+ is required.

### **Installation**

Run the following command in your notebook or terminal to install all necessary dependencies:

\!pip install \-q google-genai langchain-google-genai langgraph pydantic

### **Configuration**

Set your Gemini API key in your environment or directly within the Python script (replace GEMINI\_API\_KEY \= os.getenv("GEMINI\_API\_KEY", "") with your actual key).

### **Execution**

1. Copy the entire Python code from the file (smart\_travel\_planner.md).  
2. Paste it into your Python environment (Kaggle Notebook code cell or a .py script).  
3. Execute the script to start the interactive loop:  
   run\_agent\_loop()

### **Recommended Test Data**

To test the full capability of the multi-agent orchestration, enter this single, comprehensive command when the agent asks for input:

I want to go to Rome from 2026-06-15 to 2026-06-22. My maximum budget is $2500, and I'm really interested in history, food, and culture.

This single input should successfully trigger the entire three-agent, three-tool workflow and deliver the final itinerary.
