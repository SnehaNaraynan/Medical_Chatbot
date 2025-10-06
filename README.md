# Medical RAG Chatbot

## DataSource: 
- Gale Encyclopedia of Medicine (PDF format)

## Data Preprocessing (database.py)
- Text Chunking: Applied RecursiveCharacterTextSplitter
- Embedding Generation:Model: sentence-transformers/all-MiniLM-L6-v2
- Vector Store:Used FAISS (Facebook AI Similarity Search) for efficient similarity search
Stored embeddings locally for fast retrieval during inference

## Retrieval & Generation (medical_chatbot.py)
-### Retrieval:

* Semantic search using FAISS vectorstore
* Top-k retrieval (k=3) to find most relevant context chunks
* Uses cosine similarity between query and document embeddings

-LLM Integration:

*Model: Claude 3 Sonnet via AWS Bedrock
*Custom ClaudeLLM wrapper for LangChain integration
*Temperature: 0.5 (balanced between creativity and consistency)
*Max tokens: 1000

- Prompt Engineering:

Custom prompt template that:

*Grounds responses strictly in retrieved context
*Prevents hallucination by instructing model to say "I don't know" when uncertain
*Ensures concise, direct answers

- Chain Architecture:

*RetrievalQA chain with "stuff" method
*Combines retrieved documents into single context window
*Returns both answer and source documents for transparency
