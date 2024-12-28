# RAG

# Document-based Question Answering System

This repository contains a simple implementation of a Document-based Question Answering (QA) system using the following key components:
- **Sentence Transformers** for document embedding and similarity search.
- **FAISS** for efficient nearest-neighbor search.
- **Hugging Face's Transformers** for generating natural language responses with a pre-trained model.

The system allows users to input a query, retrieve relevant chunks of a document, and generate a context-aware response using a language model.

## Features
- **Document Embedding**: The document is split into chunks, and embeddings for these chunks are generated using Sentence-BERT's `all-MiniLM-L6-v2` model.
- **Similarity Search**: FAISS is used to efficiently find the most similar document chunks to the user's query.
- **Response Generation**: A pre-trained T5-based model (Flan-T5) from Hugging Face's `transformers` library generates answers based on the retrieved document chunks.

## Requirements
Make sure to install the following dependencies:

```bash
pip install transformers sentence-transformers faiss-cpu

```
## How it Works

The system follows a multi-step process to generate responses based on the content of a document and a user's query. Here's a breakdown of how the system operates:

1. **Document Chunking**:
   - The document is read from a `.txt` file and is split into smaller, manageable chunks (in this case, by sentence using a period `.` as the delimiter).
   - Each chunk represents a smaller piece of information from the document, allowing for more precise retrieval during the search phase.

2. **Embedding Generation**:
   - Each document chunk is passed through a pre-trained **Sentence-BERT** model (`all-MiniLM-L6-v2`) to generate vector embeddings. These embeddings are high-dimensional numerical representations of the semantic meaning of the chunks.
   - These embeddings capture the meaning of the document chunks in a way that allows for efficient comparison and similarity measurement.

3. **Similarity Search with FAISS**:
   - When a user enters a query, it is also passed through the **Sentence-BERT** model to generate an embedding.
   - **FAISS** (Facebook AI Similarity Search) is then used to search for the most similar document chunks to the query embedding. FAISS performs efficient nearest-neighbor search on the vector space, identifying the most relevant chunks based on their similarity to the query.

4. **Response Generation**:
   - The relevant document chunks retrieved from the FAISS search are concatenated with the original query to provide context.
   - This concatenated text is passed into a pre-trained **Flan-T5** model (from Hugging Face's `transformers` library), which generates a natural language response to the query based on the retrieved document chunks.
   - The response is then returned to the user.

By combining document chunking, semantic embeddings, efficient search, and language generation, the system is able to provide context-aware responses to user queries based on the document content.

## Notes

- **Document Size**: The document is assumed to be in a `.txt` format, with each sentence split by periods (`.`). If your document uses a different format or delimiter, you may need to adjust the chunking logic.
  
- **Compute Resources**: Generating embeddings and using language models like **Flan-T5** may require significant computational resources, especially for larger documents or frequent queries. Consider using a machine with enough memory and processing power, or use cloud-based solutions if necessary.

- **Model Performance**: The quality of responses depends on the relevance of the document chunks retrieved and the performance of the language model. If the document contains highly technical or complex content, consider fine-tuning the models for better results.


