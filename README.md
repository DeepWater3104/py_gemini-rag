# NEURON Simulator RAG AI Assistant 🧠
This is an interactive AI development assistant built using the official documentation of the NEURON Simulator as its knowledge source. It leverages Google's Gemini File Search API to construct a Retrieval-Augmented Generation (RAG) system, ensuring accurate and reliable code generation and Q&A capabilities specific to this technical domain.

## ✨ Key Features
Domain-Specific Expertise: Generates accurate answers to questions about the NEURON Simulator, based on its official documentation.

High-Quality Code Generation: Accelerates development by generating ready-to-use hoc and Python code snippets for building NEURON models and running simulations, given concrete instructions.

Guardrail Functionality: Designed not to respond to questions unrelated to NEURON, maintaining its specialization.

Source Citation: Provides clear citation of the document sections that support the generated answer, ensuring information trustworthiness.

Automatic Knowledge Update: Utilizes GitHub Actions to periodically re-fetch the official documentation and keep the knowledge base up-to-date.

## 🔧 How It Works
The application is built and operated through the following steps:

Data Collection: A Python script (py_wget.py) is used to recursively download HTML files from the specified NEURON documentation site.

Data Preprocessing: The downloaded HTML is processed to generate a plain-text knowledge source suitable for RAG (local_html2text.py).

Knowledge Base Construction: The Gemini File Search API is used to upload the generated text files, constructing a vectorized, searchable "File Search Store" (setup_rag_store.py).

Conversational Interface: An interactive application is run (query_rag.py) to answer user queries by referencing the constructed store as the knowledge source.

## 🚀 Getting Started
## 1. Initial Setup
### a. Clone the Repository
```Bash
git clone https://github.com/your-username/your-repository-name.git
cd your-repository-name
```
### b. Install Required Libraries
Run the following command in a Python environment (3.9+ recommended):

```Bash
pip install -r requirements.txt
```
### c. Set API Key
Create a new file named .env in the project's root directory and set your Gemini API key.

```
# .env
GEMINI_API_KEY="YOUR_GEMINI_API_KEY_HERE"

```
## 2. Building the Knowledge Base (RAG Store)
This step trains the AI with the source documentation. This task is performed only once initially.

### a. Document Download and Text Conversion
Run the following scripts to download the official NEURON Simulator documentation and convert it into text files. (This process may take several minutes to tens of minutes)

```Bash
python py_wget.py
python local_html2text.py
```
### b. Create the RAG Store
Next, upload the textual documents to the Gemini File Search API to construct the knowledge base.

```Bash
python setup_rag_store.py
```
Upon completion, a Store Name (ID) like fileSearchStores/xxxxxxxx will be displayed in the console. Copy this ID.

## 3. Running the AI Assistant
Now you can start the conversation with the AI assistant.

### a. Configure the Store Name
Open the query_rag.py file and replace the value of FILE_SEARCH_STORE_NAME with the ID you copied.

```python
# query_rag.py

# ...
FILE_SEARCH_STORE_NAME = "fileSearchStores/xxxxxxxxxxxx" # ← Replace this
# ...
```

### b. Launch the Application
Execute the following command in your terminal to start the dialogue with the AI.

```Bash
python query_rag.py

Enter your question about NEURON (Press Enter only to quit): 
Feel free to ask any questions about the NEURON Simulator.

🤖 Automatic Knowledge Update with GitHub Actions
This repository includes a GitHub Actions workflow (.github/workflows/update-docs.yml) for automatically updating the documentation.

Execution Timing:

Manual execution from the GitHub Actions tab (workflow_dispatch).

Periodic execution is also possible (by uncommenting the schedule in update-docs.yml).

Action Details:

Executes py_wget.py and local_html2text.py to re-fetch and re-process the documentation.

If any differences are found in the generated files, it automatically commits and pushes the changes.

This ensures that the knowledge source within your repository is always current. You can get the latest knowledge simply by running git pull locally.

💡 Future Outlook
Knowledge Base Expansion: The AI's expertise can be further broadened simply by adding new documentation site URLs to py_wget.py (e.g., NEURON tutorials, documentation for related libraries).

Web UI Implementation: Developing a more user-friendly web application using tools like Streamlit, Gradio, or Flask.

Advanced Store Management: Enhancing scripts like add_docs_to_store.py to allow flexible addition, deletion, and update of documents within an existing store.

We hope this README assists you in your fantastic NEURON simulation projects.

Would you like me to elaborate on how you would typically modify py_wget.py to target the NEURON documentation website?
```
