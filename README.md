# 🤖 AI Study Buddy (RAG Project)

This is a simple Generative AI (GenAI) application that allows you to "chat" with your own documents.

It uses a **RAG (Retrieval-Augmented Generation)** pipeline to find the most relevant parts of your notes and then uses the Gemini API to generate a natural language answer.

## 🚀 Tech Stack

* **Python**
* **Google Colab:** The environment where this project is built and run.
* **Pandas:** Used for data cleaning and organizing the text chunks.
* **Sentence-Transformers:** A powerful local AI model (`all-MiniLM-L6-v2`) used to create vector embeddings (turning "meaning" into numbers) for free.
* **Numpy & Scipy:** Used to perform the high-speed mathematical "Vector Search" (calculating cosine similarity).
* **Google Gemini API:** The final "Generative" AI (`gemini-pro-latest`) that summarizes the retrieved information and answers the user's question.

## ⚙️ How It Works: The RAG Pipeline

This project demonstrates the five core steps of a RAG system:

1.  **Read & Clean:** The `notes.txt` file is read, cleaned of junk characters (`\n`, `\t`), and split into meaningful paragraphs ("chunks").
2.  **Embeddings:** The `SentenceTransformer` model reads every *chunk* and converts its semantic "meaning" into a 384-dimension mathematical vector.
3.  **Vector Search:** When you ask a "Query" (e.g., "What is KNN?"), your query is *also* converted into a vector. We then use `scipy.spatial.distance.cosine` to calculate the mathematical "distance" between your query and *every* note chunk.
4.  **Retrieval:** We retrieve the Top-K (e.g., top 3) chunks that are mathematically "closest" in meaning to your query.
5.  **Generation:** We send these 3 retrieved chunks *and* your original query to the Gemini API (`gemini-pro-latest`) with a specific prompt, telling it to "answer the query *only* using the provided context."

## 🏃‍♀️ How to Run

1.  Open the `AI_Study_Buddy.ipynb` file directly in Google Colab.
2.  On the left-hand sidebar, click the **"Secrets" (🔑)** icon.
3.  Create a new secret named `GEMINI_API_KEY` and paste your Google AI Studio API key into the value field.
4.  In the top menu, click **Runtime -> Run all**. The notebook will execute all the steps, and you will see the final AI-generated answer at the bottom.