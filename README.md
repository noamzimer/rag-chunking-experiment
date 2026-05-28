# Experimental RAG Project – Chunking Comparison

Submitted by:
- Noam Z.

Track: Experimental / Research RAG – Track 2

---

## Abstract

This project presents a simple experimental Retrieval-Augmented Generation (RAG) pipeline.

The main goal of the experiment is to examine how different chunking configurations affect retrieval quality in a RAG system. The experiment compares three chunking configurations: small chunks, medium chunks, and large chunks.

All configurations use the same dataset, the same test questions, and the same TF-IDF retriever. The only variables that change are the chunk size and overlap.

The results show that all chunking configurations achieved perfect Top-1 Accuracy and Top-3 Accuracy on the selected test questions. However, a qualitative analysis shows that the medium chunking configuration provides the best balance between focused retrieval and enough useful context.

---

## 1. Introduction

Retrieval-Augmented Generation (RAG) is a method that combines information retrieval with text generation. Instead of relying only on the internal knowledge of a language model, a RAG system first retrieves relevant information from an external knowledge source and then uses this information as context for generating an answer.

A typical RAG pipeline includes document loading, chunking, indexing, retrieval, and answer generation.

One important component in a RAG system is chunking. Chunking is the process of splitting documents into smaller text segments. The choice of chunk size can affect retrieval quality, because small chunks may be more focused, while large chunks may preserve more context.

This project focuses on one important RAG component: the chunking strategy.

---

## 2. Research Question

The main research question of this project is:

**How do different chunking configurations affect retrieval quality in a simple RAG pipeline?**

More specifically, the experiment checks whether small, medium, or large chunks provide better retrieved context for answering questions.

---

## 3. Dataset

The dataset contains six short educational text documents related to Artificial Intelligence and Information Retrieval.

The documents are:

1. `doc1_machine_learning.txt`
2. `doc2_information_retrieval.txt`
3. `doc3_rag.txt`
4. `doc4_chunking.txt`
5. `doc5_embeddings.txt`
6. `doc6_vector_databases.txt`

Each document represents one topic in the knowledge base.

---

## 4. Methodology

The project implements a simple experimental RAG pipeline.

The pipeline includes the following stages:

1. Loading the document collection.
2. Splitting the documents into chunks.
3. Building a TF-IDF retriever for each chunking configuration.
4. Retrieving the most relevant chunks for each test question using cosine similarity.
5. Evaluating retrieval quality using Top-1 Accuracy and Top-3 Accuracy.
6. Generating simple answers based on the retrieved context.

The experiment keeps the dataset, test questions, and retrieval method fixed. Only the chunking configuration changes.

---

## 5. Chunking Configurations

The experiment compares three chunking configurations:

| Configuration | Chunk Size | Overlap |
|---|---:|---:|
| small_chunks | 300 characters | 50 characters |
| medium_chunks | 500 characters | 100 characters |
| large_chunks | 800 characters | 150 characters |

The purpose of comparing these configurations is to understand how chunk size and overlap affect retrieval results.

---

## 6. Retrieval Method

The retrieval stage uses:

- TF-IDF vector representation
- Cosine similarity
- Top-k retrieval with `k = 3`

Each chunk is represented as a TF-IDF vector.  
Each test question is also converted into a TF-IDF vector.  
Cosine similarity is then used to rank the chunks according to their relevance to the question.

---

## 7. Test Questions

The system was evaluated using the following test questions:

1. What is Retrieval-Augmented Generation?
2. Why is chunking important in RAG systems?
3. What is the role of embeddings in semantic search?
4. How does an inverted index help in information retrieval?
5. What is a vector database used for?

Each question has an expected source document.

---

## 8. Evaluation Metrics

The experiment uses two automatic evaluation metrics:

### Top-1 Accuracy

Top-1 Accuracy checks whether the first retrieved chunk comes from the expected source document.

### Top-3 Accuracy

Top-3 Accuracy checks whether at least one of the top 3 retrieved chunks comes from the expected source document.

These metrics help evaluate whether the retriever finds relevant information for each question.

---

## 9. Results

All three chunking configurations achieved the following results:

| Configuration | Top-1 Accuracy | Top-3 Accuracy |
|---|---:|---:|
| small_chunks | 1.0 | 1.0 |
| medium_chunks | 1.0 | 1.0 |
| large_chunks | 1.0 | 1.0 |

The results show that all configurations successfully retrieved the expected source document for every test question.

---

## 10. Discussion

Although all configurations achieved the same automatic accuracy scores, the retrieved chunks were not identical.

Small chunks were usually focused and precise, but they sometimes provided too little context or cut sentences.

Large chunks preserved more context, but sometimes included additional information that was not directly needed for answering the question.

Medium chunks provided the best balance between focused retrieval and enough useful context.

Therefore, even though the automatic scores were identical, the qualitative analysis suggests that the medium chunking configuration is the most balanced option for this dataset.

---

## 11. Answer Generation

The project also includes a simple answer generation step.

The system uses the best chunking configuration, `medium_chunks`, retrieves the most relevant chunk, and presents it as the generated answer.

This generation method does not use an external LLM. Instead, it uses the retrieved context directly.

This keeps the generated answer grounded in the retrieved document and avoids using external knowledge.

---

## 12. Limitations

This experiment has several limitations.

First, the dataset is small and clean. It contains only six short educational documents.

Second, each test question is strongly connected to one specific document. Because of this, all chunking configurations achieved perfect automatic accuracy.

Third, the chunking method is character-based. As a result, some chunks may end in the middle of a word or sentence.

In a larger or noisier dataset, the differences between chunking strategies would probably become more significant.

Future work could include:

- More documents
- Longer documents
- Noisier text
- More ambiguous questions
- Sentence-based chunking
- Additional retrieval methods such as BM25 or embeddings
- Comparison between local LLMs and external LLM APIs

---

## 13. Conclusion

This project implemented a simple experimental RAG pipeline and compared three chunking configurations.

The automatic evaluation showed that all configurations achieved perfect Top-1 and Top-3 Accuracy on the selected test questions.

However, the qualitative analysis showed that medium chunks provided the best balance between precision and context.

For this small RAG experiment, the medium chunking configuration was selected as the most balanced option.

---

## Project Files

```text
rag-chunking-experiment/
│
├── README.md
├── rag_chunking_experiment.ipynb
│
├── data/
│   ├── doc1_machine_learning.txt
│   ├── doc2_information_retrieval.txt
│   ├── doc3_rag.txt
│   ├── doc4_chunking.txt
│   ├── doc5_embeddings.txt
│   └── doc6_vector_databases.txt
│
└── outputs/
    ├── evaluation_results.csv
    └── summary_results.csv
```

---

## How to Run

1. Open `rag_chunking_experiment.ipynb` in Google Colab or Jupyter Notebook.
2. Run the notebook cells in order.
3. Upload the six text documents when requested.
4. The notebook will:
   - Load the documents
   - Split them into chunks
   - Build TF-IDF retrievers
   - Retrieve relevant chunks
   - Evaluate retrieval quality
   - Generate simple answers from retrieved context
   - Save the results to the `outputs/` folder

---

## Technologies Used

- Python
- Google Colab / Jupyter Notebook
- pandas
- NumPy
- scikit-learn
- TF-IDF
- Cosine Similarity
