# rag-chat-api

## Project Setup and Instructions
## Prerequisites
- Python 3.x
- pip (Python package installer)
- Firebase Admin SDK credentials (set up in Firebase Console)
- Pinecone API key
- Google Gemini API key
- Git

## Clone the Repository
1. Clone the GitHub repository to your local machine:
```bash
git clone https://github.com/your-repo/rag-chat-api.git
cd rag-chat-api
```

2. Create and Activate a Virtual Environment
```bash
python -m venv venv
```

3. Activate the virtual environment:
- On macOS/Linux:
``` bash
source venv/bin/activate
```
- On Windows:
```bash
venv\Scripts\activate
```

## Install Dependencies
1. Install all required Python dependencies:
```bash
pip install -r requirements.txt
```

## Environment Variables Setup
In the root directory of the project, create a file called `.env` to store your API keys and Firebase project details:
```bash
touch .env
```
Inside the `.env` file, add the following environment variables:
- PINECONE_API_KEY=your-pinecone-api-key
- GEMINI_API_KEY=your-google-gemini-api-key
- FIREBASE_PRIVATE_KEY_PATH=config/rag-chat-api-firebase-adminsdk.json

### Firebase Setup

This project uses Firebase for storing and retrieving document metadata. To configure Firebase:

1. Go to the [Firebase Console](https://console.firebase.google.com/).
2. Navigate to your project settings.
3. In the "Service accounts" tab, click "Generate new private key" and download the `json` file.
4. Place this file in the `config/` folder of the project.
5. Make sure the file is named `rag-chat-api-firebase-adminsdk.json`.


### Pinecone Setup

1. Go to [Pinecone](https://www.pinecone.io/) Dashboard.
2. Create an Index named document-index with a dimension of 768 (this matches the dimension of embeddings generated by Google Gemini).
3. Copy your API Key and the Environment details from the Pinecone Dashboard.

   
### Google Gemini Setup
1. Visit [Google AI Studio](https://aistudio.google.com/app/prompts/new_chat).
Sign in with your Google account.
2. Generate an API Key
3. Add this key to the .env file under GEMINI_API_KEY.


## Running the Project
### Flask API (Backend)
1. Start the Flask backend server:
```bash
   python app.py
```
### Streamlit (Frontend Interface)
1. Start the Streamlit application for user interaction:
```bash
streamlit run app_streamlit.py
```
- This will open a web interface where users can:
- Upload PDF documents.
- Provide a unique chat name for indexing.
- Query indexed documents using a chat-based interaction.

## Testing with curl (Optional)
Uploading a Document:
You can upload a document and index it by running the following `curl` command:
```bash
curl -X POST http://127.0.0.1:5000/upload -F "file=@/path/to/your/document.pdf" -F "chat_name=your_chat_name"
```
Querying the Document:
To query the indexed document and get responses using Google Gemini, run:
```bash
curl -X POST http://127.0.0.1:5000/query_document -F "chat_name=your_chat_name" -F "question=your_query_here"
```

## Using the Application
1. Upload a Document
Use the Drag and Drop feature or browse to upload a PDF document.
Enter a unique chat name to associate with the document.
2. Query the Document
After indexing the document, you can query it by entering the chat name and typing your question.
The system will fetch relevant sections from the document using Pinecone and generate responses using Google Gemini.


## Example Output
Sample Upload Response:
```bash
{
  "status": "success",
  "message": "Document indexed under chat name: your_chat_name"
}
```

Sample Query Response:
```bash
{
  "status": "success",
  "response": "Based on the document, the answer to your query is..."
}
```
Security Considerations
Ensure the following files are added to `.gitignore` to avoid exposing sensitive information:
```bash
config/rag-chat-api-firebase-adminsdk.json
.env
__pycache__/
venv/
```
## Final Thoughts
This project demonstrates the integration of cutting-edge technologies like Google Gemini, Pinecone, and Firebase for creating a Retrieval-Augmented Generation (RAG) based system. The solution allows users to upload documents, query relevant sections, and receive AI-generated answers. With error handling, input validation, and guardrails in place, the system ensures robust and accurate interactions. For any further improvements or questions, feel free to contribute or raise an issue in this repository.

