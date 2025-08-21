AI-Powered SEC Filing Analysis
This project automates the analysis of SEC filings using a Retrieval-Augmented Generation (RAG) pipeline. It fetches financial data directly from the SEC, processes it, and leverages a large language model to provide insightful answers to complex financial questions.

Features
Automated Data Retrieval: Fetches SEC filings (10-K, 10-Q) for any given company ticker.

Intelligent Text Processing: Cleans and parses HTML content, converting tables to a markdown format for better readability and analysis.

Advanced AI-Powered Analysis: Utilizes a RAG pipeline with a Gemini model to generate context-aware and accurate financial analysis.

Efficient Data Indexing: Employs Vertex AI Vector Search and Firestore to store and index filing data for rapid retrieval.

Comprehensive Outputs: Generates detailed analysis reports in markdown format, complete with sources for full transparency.

How It Works
The project follows a systematic pipeline to deliver high-quality financial analysis:

Data Scraping: The process begins by fetching a company's CIK and name using its stock ticker. It then retrieves recent 10-K and 10-Q filings from the SEC's EDGAR database.

Data Cleaning and Chunking: The raw HTML of the filings is cleaned to remove extraneous elements like scripts and styles. Tables are converted into markdown format. The cleaned text is then segmented into logical sections based on "ITEM" headings.

Data Storage and Indexing: Each text chunk is stored in Firestore. Embeddings are generated for each chunk using Gemini and are indexed in Vertex AI Vector Search to enable efficient similarity searches.

Retrieval-Augmented Generation (RAG):

Retrieval: When a question is posed, an embedding is created for the query. This embedding is used to find the most relevant text chunks from the indexed SEC filings in Vertex AI Vector Search.

Augmentation & Generation: The retrieved chunks are combined with the user's query and a system prompt to create a comprehensive prompt. This is then passed to a Gemini model, which generates a detailed and context-aware response.

Output: The final analysis, including the sources used to generate it, is saved as a markdown file in the output directory.

Technologies Used
Cloud Platform: Google Cloud Platform (GCP)

AI/ML:

Google Generative AI (Gemini)

Vertex AI (Vector Search, Matching Engine)

Database: Firestore

Python Libraries:

requests

beautifulsoup4

google-generativeai

google-cloud-aiplatform

google-cloud-firestore

python-dotenv

jupyter

Setup and Usage
Follow these steps to set up and run the project:

Prerequisites
Python 3.9+

A Google Cloud Project with the following APIs enabled:

Vertex AI API

Firestore API

Authentication configured for your GCP account.

Installation
Clone the repository and install the required dependencies:

git clone https://github.com/honcyeung/ai-powered-sec-filing-analysis.git
cd ai-powered-sec-filing-analysis
pip install -r requirements.txt

Configuration
Create a .env file in the root directory of the project and add the following environment variables:

PROJECT_ID="your-gcp-project-id"
REGION="your-gcp-region"
GEMINI_API_KEY="your-gemini-api-key"
COLLECTION_NAME="your-firestore-collection-name"
INDEX_NAME="your-vertex-ai-index-name"
INDEX_ENDPOINT_NAME="your-vertex-ai-index-endpoint-name"
PROMPTLAYER_API_KEY="your-promptlayer-api-key"
PROMPT_TEMPLATE_IDENTIFIER="your-prompt-template-identifier"

Running the Analysis
Open main.ipynb in a Jupyter Notebook environment.

Set the TICKER variable to the stock ticker of the company you wish to analyze.

Execute all the cells in the notebook to run the full analysis pipeline.

Project Structure
main.ipynb: The primary notebook that orchestrates the entire workflow from data scraping to analysis generation.

data_scraping.ipynb: Contains all functions related to scraping, cleaning, and chunking SEC filings.

data_retrieval.ipynb: Manages the storage of data in Firestore and the deployment of the Vertex AI Vector Search index.

data_augmentation.ipynb: Implements the retrieval component of the RAG pipeline, identifying relevant text chunks for a given query.

output/: The directory where the final analysis files are saved.

.gitignore: Specifies files and directories to be ignored by Git.

Example Output
The output is a markdown file containing a detailed financial analysis based on the user's query. An example is provided in the output/ directory, such as SBET_summarize_sharplink_gaming_incs_strategy_2025_08_21.md.
