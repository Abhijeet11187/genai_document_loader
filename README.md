# 📄 LangChain Document Loaders

A hands-on collection of Jupyter notebooks demonstrating how to load and process various document types using **LangChain's document loaders**. This project covers everything from web pages and plain text files to PDFs, CSVs, JSON, and Markdown — making it a practical reference for building LLM-ready data pipelines.

---

## 📚 Table of Contents

- [Overview](#overview)
- [Notebooks](#notebooks)
- [Document Loaders Covered](#document-loaders-covered)
- [Installation](#installation)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [Requirements](#requirements)

---

## Overview

When building LLM applications, the first step is always ingesting data from different sources. This repository explores LangChain's `document_loaders` module and demonstrates how to load data from multiple formats — all formatted as `Document` objects ready for downstream processing like splitting, embedding, and retrieval.

---

## Notebooks

| Notebook | Description |
|---|---|
| `document_loaders.ipynb` | Web, Text (.srt), Directory, and CSV loaders |
| `document_loader_two.ipynb` | Markdown, CSV, JSON, and PDF loaders |

---

## Document Loaders Covered

### 🌐 Web Loader
Load live content from any URL using `WebBaseLoader` with `BeautifulSoup4`.

```python
from langchain_community.document_loaders import WebBaseLoader

loader = WebBaseLoader("https://docs.langchain.com/")
data = loader.load()
```

---

### 📝 Text Loader
Load plain text files such as `.srt` subtitle files.

```python
from langchain_community.document_loaders import TextLoader

loader = TextLoader('data/subtitles/Friends_2x01.srt')
data = loader.load()
```

---

### 📁 Directory Loader
Bulk-load all files matching a glob pattern from a folder.

```python
from langchain_community.document_loaders import DirectoryLoader

loader = DirectoryLoader('data/subtitles', glob="*.srt", show_progress=True, loader_cls=TextLoader)
data = loader.load()
```

---

### 📊 CSV Loader
Load tabular data row-by-row from `.csv` files.

```python
from langchain_community.document_loaders import CSVLoader

loader = CSVLoader("data/csv_data/movies_data.csv")
data = loader.load()
```

---

### 🔖 Markdown Loader
Parse and load Markdown documents using `UnstructuredMarkdownLoader`.

```python
from langchain_community.document_loaders import UnstructuredMarkdownLoader

loader = UnstructuredMarkdownLoader("README.md", mode="single")
doc = loader.load()
```

---

### 🗂️ JSON Loader
Extract specific fields from JSON files using `jq` schema filters.

```python
from langchain_community.document_loaders import JSONLoader

loader = JSONLoader("chat_data.json", jq_schema=".messages[]", text_content=False)
data = loader.load()
```

---

### 📕 PDF Loader (PyMuPDF)
Load structured PDF documents page-by-page with metadata.

```python
from langchain_community.document_loaders import PyMuPDFLoader

loader = PyMuPDFLoader("layoutparser_paper.pdf")
data = loader.load()
```

---

### 📄 Unstructured PDF Loader
Handle messy or scanned PDFs using `UnstructuredPDFLoader` with OCR support via Tesseract.

```python
from langchain_community.document_loaders import UnstructuredPDFLoader

loader = UnstructuredPDFLoader("document.pdf")
data = loader.load()
```

---

## Installation

```bash
pip install langchain-community langchain-core
pip install beautifulsoup4
pip install unstructured[all-docs]
pip install pymupdf
pip install jq
```

For OCR support (scanned PDFs):
```bash
# Ubuntu/Debian
sudo apt-get install tesseract-ocr
sudo apt-get install poppler-utils

# macOS (via conda)
conda install -c conda-forge tesseract
```

---

## Project Structure

```
📦 langchain-document-loaders
 ┣ 📓 document_loaders.ipynb       # Web, Text, Directory, CSV loaders
 ┣ 📓 document_loader_two.ipynb    # Markdown, CSV, JSON, PDF loaders
 ┣ 📁 data/
 ┃ ┣ 📁 subtitles/                 # .srt subtitle files
 ┃ ┗ 📁 csv_data/                  # Sample CSV files
 ┗ 📄 README.md
```

---

## Requirements

- Python 3.8+
- LangChain Community
- BeautifulSoup4
- PyMuPDF (`pymupdf`)
- `jq` (for JSON loader)
- `unstructured[all-docs]` (for unstructured loaders)
- `nltk` (for Markdown parsing)
- `pandas` (for CSV creation)
- Tesseract OCR *(optional, for scanned PDFs)*

---

## 🙌 Acknowledgements

- [LangChain](https://github.com/langchain-ai/langchain) for the powerful document loading ecosystem.
- [Unstructured.io](https://unstructured.io/) for OCR and unstructured document parsing.
