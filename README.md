# safe_store
![GitHub Repo](https://img.shields.io/badge/GitHub-Repo-brightgreen.svg)
![PyPI Version](https://img.shields.io/pypi/v/safe-store.svg)
![License](https://img.shields.io/github/license/ParisNeo/safe_store.svg)
![Python Versions](https://img.shields.io/pypi/pyversions/safe-store.svg)

`safe_store` is an open-source Python library that provides essential tools for text data management, vectorization, and document retrieval. It empowers users to work with text documents efficiently and effortlessly.

- [Introduction](#safe_store)
- [Key Features](#key-features)
  - [Text Vectorizer](#1-text-vectorizer)
  - [Generic Data Loader](#2-generic-data-loader)
- [What Can You Use `safe_store` For?](#what-can-you-use-safe_store-for)
- [Text Vectorizer](#text-vectorizer)
  - [Features](#features)
  - [Installation](#installation)
  - [Getting Started](#getting-started)
    - [Initializing the Text Vectorizer](#initializing-the-text-vectorizer)
    - [Adding and Indexing Documents](#adding-and-indexing-documents)
    - [Embedding a Query and Retrieving Similar Documents](#embedding-a-query-and-retrieving-similar-documents)
  - [Interactive Document Visualization](#interactive-document-visualization)
- [Generic Data Loader](#generic-data-loader)
  - [Features](#features-1)
  - [Usage](#usage)
  - [Supported File Types](#supported-file-types)
- [Author](#author)
- [License](#license)


## Key Features:

### 1. Text Vectorizer

- **Versatile Vectorization:** Choose between TF-IDF vectorization, model-based embeddings to convert text documents into numerical representations or use BM25 ranking for text retreival.
- **Document Similarity:** Find documents similar to a given query text, making it ideal for document retrieval tasks.
- **Interactive Visualization:** Visualize document embeddings in a scatter plot to gain insights into document relationships.
- **No Authentication Required:** Use the library without the need for API keys or authentication, making it accessible for everyone.
- **Commercially Usable:** `safe_store` is 100% open-source and free to use, even for commercial purposes, under the Apache 2.0 License.

### 2. Generic Data Loader

- **Multi-format Support:** Read various file formats, including PDF, DOCX, JSON, HTML, and more.
- **Simplified Text Extraction:** Convert file content to plain text or data structures with ease.
- **Efficient and Time-Saving:** Streamline data loading and processing tasks, reducing the need for manual extraction.

## What Can You Use `safe_store` For?

- **Text Document Analysis:** Analyze and understand the content of text documents quickly and efficiently.
- **Document Retrieval:** Retrieve documents similar to a given query text, facilitating content recommendation and search tasks.
- **Text Data Preprocessing:** Prepare text data for natural language processing (NLP) tasks, such as sentiment analysis and text classification.
- **Data Loading:** Streamline the process of reading and extracting content from various file formats.

`safe_store` is designed to be accessible, versatile, and free for all users. It's an ideal choice for developers, data scientists, and researchers who want a user-friendly and open-source solution for working with text data.

---

Explore the world of text data management and analysis with `safe_store` today!

## Text Vectorizer

### Features

- Vectorize and index text documents.
- Retrieve similar documents based on a query.
- Supports both TF-IDF vectorization and model-based embeddings.
- Interactive visualization of document embeddings.
- No authentication or API keys required.

### Installation

To install `safe_store`, you can use `pip`:

```bash
pip install safe_store
```

### Getting Started

#### Initializing the Text Vectorizer

```python
from safe_store import TextVectorizer, VectorizationMethod
from pathlib import Path

# Create an instance of TextVectorizer
vectorizer = TextVectorizer(
    vectorization_method=VectorizationMethod.TFIDF_VECTORIZER,
    database_path="database.json",
    save_db=False
)
```

#### Adding and Indexing Documents

```python
# Add documents for vectorization
documents = ["llm", "space", "submarines", "new york"]
for doc in documents:
    document_name = Path(__file__).parent / f"{doc}.txt"
    with open(document_name, 'r', encoding='utf-8') as file:
        text = file.read()
    vectorizer.add_document(document_name, text, chunk_size=100, overlap_size=20, force_vectorize=False, add_as_a_bloc=False)

# Index the documents (perform vectorization)
vectorizer.index()
```

#### Embedding a Query and Retrieving Similar Documents

```python
# Embed a query and retrieve similar documents
query_text = "what is space"
similar_texts, _ = vectorizer.recover_text(query_text, top_k=3)

# Show the interactive document visualization
vectorizer.show_document(show_interactive_form=True)

print("Similar Documents:")
for i, text in enumerate(similar_texts):
    print(f"{i + 1}: {text}")
```
The `vectorizer.show_document(show_interactive_form=True)` should yield a plot like this where you can read the text by pointing on the dots. Each dot is a chunk of the text. We can clearly see that chunks that come from the same document tend to form a cluster.
![image](https://github.com/ParisNeo/safe_store/assets/827993/5d9c59f8-656a-423d-ab8a-08ebf77595e4)

---

## Generic Data Loader

### Features

- Read various file formats including PDF, DOCX, JSON, HTML, and more.
- Convert file content to text or data structures.

### Usage

To read a file using `GenericDataLoader`, you can use the `read_file` method and provide the file path:

```python
from safe_store import GenericDataLoader
from pathlib import Path

file_path = Path("example.pdf")
file_content = GenericDataLoader.read_file(file_path)
```

### Supported File Types

- PDF
- DOCX
- JSON
- HTML
- PPTX
- TXT
- RTF
- MD
- LOG
- CPP
- Java
- JS
- Python
- Ruby
- Shell Script
- SQL
- CSS
- PHP
- XML
- YAML
- INI
- INF
- MAP
- BAT

Feel free to replace `"example.pdf"` with the path to your specific file.

---

## Author
- ParisNeo

## License
This project is licensed under the Apache 2.0 License.
