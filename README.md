# 🌎 Local Perplexity Clone

A locally-hosted alternative to Perplexity AI that uses LangGraph to create a research workflow with multiple LLMs for query generation, web search, and response synthesis.

## 📋 Overview

This project implements a research assistant similar to Perplexity AI but running locally with open-source models. It uses a multi-step workflow to:

1. Generate search queries based on user questions
2. Search the web for relevant information
3. Synthesize search results into a comprehensive answer

The system is built using LangGraph, which enables the creation of a directed graph for orchestrating the research workflow.

## 🏗️ Architecture

The application follows a multi-agent architecture using LangGraph:

```
User Input → Query Generation → Web Search → Response Synthesis → Final Answer
```

### Components

- **Query Generator**: Analyzes the user's question and generates 3-5 search queries to gather relevant information
- **Web Searcher**: Executes searches using Tavily API and extracts content from web pages
- **Content Synthesizer**: Summarizes and extracts relevant information from search results
- **Response Writer**: Compiles all synthesized information into a comprehensive answer with citations

### Technologies Used

- **LangGraph**: For orchestrating the multi-step workflow
- **LangChain**: For LLM integration and structured outputs
- **Ollama**: For running local LLMs (Llama 3.1 and DeepSeek)
- **Tavily**: For web search capabilities
- **Streamlit**: For the user interface
- **Optional APIs**: Perplexity API and OpenPerplex for alternative search methods

## 🚀 Getting Started

### Prerequisites

- Python 3.10 or higher
- [Ollama](https://ollama.ai/) installed locally with the following models:
  - `llama3.1:8b-instruct-q4_K_S`
  - `deepseek-r1:8b`
- Tavily API key

### Installation

1. Clone the repository

```bash
git clone https://github.com/yourusername/perplexity-clone.git
cd perplexity-clone
```

2. Install dependencies using Poetry

```bash
pip install poetry
poetry install
```

3. Create a `.env` file with your API keys

```
TAVILY_API_KEY=your_tavily_api_key
# Optional APIs
PERPLEXITY_API_KEY=your_perplexity_api_key
OPENPERPLEX_API_KEY=your_openperplex_api_key
```

## 💻 Usage

Run the application with Streamlit:

```bash
poetry run streamlit run perplexity.py
```

Or directly with Python:

```bash
poetry run python perplexity.py
```

The application will open in your browser, where you can:

1. Enter your research question in the text input
2. Click "Pesquisar" (Search) to start the research process
3. View the progress as the system generates queries, searches the web, and synthesizes information
4. See the final response with citations and references
5. Optionally expand the "Reflexão" (Reflection) section to see the system's thinking process

## 🔄 Workflow Details

1. **Query Generation**: The `build_first_queries` function uses an LLM to generate multiple search queries based on the user's question.

2. **Researcher Spawning**: The `spawn_researchers` function creates parallel search tasks for each generated query.

3. **Web Search**: The `single_search` function uses Tavily to search the web and extract content from relevant pages.

4. **Content Synthesis**: Each search result is processed by an LLM to extract and summarize relevant information.

5. **Response Writing**: The `final_writer` function compiles all synthesized information into a comprehensive answer with proper citations.

## 🔧 Customization

You can customize the LLMs used by modifying the model selection in `perplexity.py`:

```python
# Choose one of these options or add your own
# llm = ChatOpenAI(model="gpt-4o")  # OpenAI model
# llm = ChatOllama(model="llama3.2:latest")  # Latest Llama model
llm = ChatOllama(model="llama3.1:8b-instruct-q4_K_S")  # Smaller quantized model
reasoning_llm = ChatOllama(model="deepseek-r1:8b")  # For final response synthesis
```

You can also modify the search providers in `utils.py` to use different search APIs:

- `tavily_search`: Uses Tavily API (default)
- `perplexity_search`: Uses Perplexity API
- `openperplex_search`: Uses OpenPerplex API

## 📝 License

This project is open source and available under the [MIT License](LICENSE).

## 🙏 Acknowledgements

- [LangChain](https://github.com/langchain-ai/langchain) for LLM integration
- [LangGraph](https://github.com/langchain-ai/langgraph) for workflow orchestration
- [Ollama](https://ollama.ai/) for local LLM hosting
- [Tavily](https://tavily.com/) for search API
- [Streamlit](https://streamlit.io/) for the user interface