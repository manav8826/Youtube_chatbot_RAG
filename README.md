# YouTube Video RAG Pipeline

This project demonstrates a Retrieval-Augmented Generation (RAG) pipeline using LangChain and Gemini for answering questions based on the transcript of a YouTube video.

## Features

- Fetches transcript from a YouTube video using `youtube-transcript-api`
- Splits transcript into manageable text chunks
- Generates embeddings using Google Generative AI
- Stores embeddings in a FAISS vector store
- Retrieves relevant chunks for a given question
- Uses Gemini LLM to answer questions based on retrieved context
- Supports chaining for end-to-end question answering

## Setup

1. **Install dependencies**  
   Run the following command in your notebook or terminal:
   ```sh
   pip install youtube-transcript-api faiss-cpu tiktoken python-dotenv
   ```

2. **Environment Variables**  
   Add your Google Generative AI API key to a `.env` file:
   ```
   GOOGLE_API_KEY=your_api_key_here
   ```

## Usage

1. **Fetch Transcript**
   - Set the `video_id` to the YouTube video you want to process.
   - The notebook fetches and prints the transcript.

2. **Text Splitting**
   - Transcript is split into chunks using `RecursiveCharacterTextSplitter`.

3. **Embedding & Vector Store**
   - Chunks are embedded and stored in FAISS for similarity search.

4. **Retrieval**
   - Retrieve relevant chunks for a user question.

5. **Augmentation & Generation**
   - Use a prompt template and Gemini LLM to answer the question using retrieved context.

6. **Chaining**
   - The pipeline can be run as a chain for single-step invocation.

## Example

```python
question = "is the topic of nuclear fusion discussed in this video? if yes then what was discussed"
retrieved_docs = retriever.invoke(question)
context_text = "\n\n".join(doc.page_content for doc in retrieved_docs)
final_prompt = promt.invoke({"context": context_text, "question": question})
answer = llm.invoke(final_prompt)
print(answer.content)
```

## File Structure

- [`11_RAG/1.ipynb`](11_RAG/1.ipynb): Main notebook implementing the pipeline.

## Notes

- Make sure your API key is valid and you have access to Gemini and embedding models.
- The pipeline can be extended to support other sources and more advanced retrieval/generation strategies.

## References

- [LangChain Documentation](https://python.langchain.com/)
- [youtube-transcript-api](https://github.com/jdepoix/youtube-transcript-api)
- [FAISS](https://github.com/facebookresearch/faiss)
