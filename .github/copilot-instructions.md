# Copilot Instructions for MEDIBOT

## Project Overview
MEDIBOT is a medical chatbot system that processes and analyzes medical documents (PDFs) to enable question answering and information retrieval. The project uses LangChain for document loading, text splitting, and filtering, and is structured for extensibility and experimentation.

## Key Components
- `app.py`: Likely the main entry point for the application or API.
- `data/`: Contains source medical documents (PDFs) for ingestion.
- `medibot/`: Contains binaries and dependencies, including a bundled Python runtime for portability.
- `research/`: Contains Jupyter notebooks for experimentation and prototyping (see `trials.ipynb`).
- `src/`: (If present) May contain core source code for the chatbot logic.

## Developer Workflows
- **Document Ingestion:**
  - Use LangChain's `DirectoryLoader` and `PyPDFLoader` to load PDFs from `data/`.
  - Use `RecursiveCharacterTextSplitter` to chunk documents for downstream processing.
  - Example pattern (see `trials.ipynb`):
    ```python
    loader = DirectoryLoader('data', glob='*.pdf', loader_cls=PyPDFLoader)
    documents = loader.load()
    splitter = RecursiveCharacterTextSplitter(...)
    chunks = splitter.split_documents(documents)
    ```
- **Filtering:**
  - Use custom filter functions to reduce document metadata to essentials (e.g., only `source` and `page_content`).
- **Experimentation:**
  - Use notebooks in `research/` for rapid prototyping and data exploration.

## Conventions & Patterns
- Prefer minimal metadata in processed documents for efficiency.
- Keep all raw data in `data/` and do not modify source PDFs.
- Notebooks should demonstrate end-to-end flows: loading, filtering, chunking, and (optionally) QA.
- Use relative paths for data access to ensure portability.

## Integration & Dependencies
- Core dependencies are managed via `requirements.txt`.
- LangChain is used for document and text processing.
- The project is designed to run with a bundled Python in `medibot/` for reproducibility.

## Examples
- See `research/trials.ipynb` for canonical data loading, filtering, and chunking code.
- Example filter function:
    ```python
    def filter_to_minimal_docs(docs):
        ... # returns docs with only 'source' in metadata
    ```

## Tips for AI Agents
- When adding new workflows, follow the notebook-driven development style.
- Reference `trials.ipynb` for idiomatic usage of LangChain and document processing.
- Place new data files in `data/` and keep code/data separation clear.
- If adding new dependencies, update `requirements.txt` and document usage in a notebook.

---
For questions or unclear conventions, review `trials.ipynb` and existing code patterns before introducing new approaches.
