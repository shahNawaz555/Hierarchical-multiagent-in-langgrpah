Hierarchical multiagent


Research Team:
Uses Tavily Search to find relevant web sources.
Scrapes web pages for detailed information using WebBaseLoader.


Paper Writing Team:
Creates outlines for reports or poems.
Writes and edits text documents.
Generates charts using Python REPL and Matplotlib.


Supervisor Agent:
Manages workflow between the Research and Paper Writing teams.
Routes tasks based on the current state and user request.


Modular Design:
Built with LangGraph for flexible state management and task orchestration.
Supports custom prompts and extensible tools.



Requirements

Python 3.8+
Dependencies (install via pip):pip install langchain langchain-community langchain-openai langgraph requests beautifulsoup4 matplotlib numpy


Tavily API key for search functionality (set as environment variable TAVILY_API_KEY).
OpenAI API key for LLM integration (set as environment variable OPENAI_API_KEY).

Installation

Clone the repository:
git clone https://github.com/your-username/north-american-sturgeon-report.git
cd north-american-sturgeon-report


Install dependencies:
pip install -r requirements.txt


Set up environment variables:
export TAVILY_API_KEY='your-tavily-api-key'
export OPENAI_API_KEY='your-openai-api-key'



Usage
Run the main script to generate a research report on North American sturgeons:
python main.py

The script will:

Use the Research Team to gather information from the web.
Pass the collected data to the Paper Writing Team to create an outline, write the report, and generate a chart.
Save the output files (outline, report, and chart) to a temporary working directory.

Example Input
from super_graph import super_graph

for s in super_graph.stream(
    {
        "messages": [
            HumanMessage(
                content="Write a brief research report on the North American sturgeon. Include a chart."
            )
        ],
    },
    {"recursion_limit": 150},
):
    if "__end__" not in s:
        print(s)

Output

Text Files: Outline and report saved as .txt files in the working directory.
Chart: A Matplotlib-generated chart (e.g., population trends) saved as a .png file.

Project Structure
north-american-sturgeon-report/
├── main.py                 # Main script to run the report generator
├── research_team.py        # Research Team logic (search and web scraping)
├── paper_writing_team.py   # Paper Writing Team logic (outline, writing, charts)
├── super_graph.py          # Top-level graph orchestrating both teams
├── requirements.txt        # Python dependencies
└── README.md               # This file

How It Works

Super Graph:

A top-level LangGraph orchestrates the Research and Paper Writing teams.
A supervisor node routes tasks between teams or signals completion (FINISH).


Research Team:

Search Agent: Uses Tavily to find relevant URLs.
WebScraper Agent: Scrapes content from provided URLs using WebBaseLoader.
Controlled by a supervisor that decides whether to search or scrape next.


Paper Writing Team:

NoteTaker Agent: Creates outlines.
DocWriter Agent: Writes and edits documents.
ChartGenerator Agent: Generates charts using Python REPL.
A supervisor routes tasks among these agents.


State Management:

Both teams maintain their own state (messages, current files, next steps).
The super graph ensures states don't intermingle.



Contributing
Contributions are welcome! To contribute:

Fork the repository.
Create a feature branch (git checkout -b feature/your-feature).
Commit your changes (git commit -m 'Add your feature').
Push to the branch (git push origin feature/your-feature).
Open a pull request.
