# PDF-Based Text Generation using Variational Autoencoder (VAE) with Gradio

## Overview

This project builds an end-to-end pipeline that generates new text from a PDF document using a Variational Autoencoder (VAE). It integrates PDF text extraction, natural language preprocessing, deep generative modeling, and a Gradio-based user interface.

The system learns patterns from the uploaded PDF and generates similar text using a latent space representation.

---

## System Architecture

The pipeline consists of four main components:

1. PDF Text Extraction
2. Text Preprocessing and Tokenization
3. Variational Autoencoder (VAE) Model
4. Text Generation and Gradio Interface

---

## 1. PDF Text Extraction

The function:

```python
extract_text_from_pdf(path)
```

* Uses PyMuPDF (fitz) to read PDF files
* Iterates through pages and extracts raw text

Note: There is a small issue in your code:

```python
text = "/content/Bound_by_Alpha_and_Omega.pdf"
```

This should be initialized as an empty string:

```python
text = ""
```

---

## 2. Text Preprocessing

The function:

```python
process_text(raw_text)
```

### Steps:

* Removes extra whitespace using regex
* Splits text into sentences
* Filters very short sentences
* Tokenizes sentences using Keras Tokenizer
* Converts text to integer sequences
* Applies padding

### Output:

* Padded sequences
* Tokenizer
* Vocabulary size
* Input dimension

---

## 3. Variational Autoencoder (VAE)

### Concept

A VAE is a generative model that:

* Encodes input into a latent distribution
* Samples from this distribution
* Decodes it back to generate new data

---

### Encoder

* Embedding layer converts tokens to vectors
* LSTM captures sequence information
* Outputs:

  * Mean (z_mean)
  * Variance (z_log_var)

---

### Latent Space Sampling

[
z = \mu + \sigma \cdot \epsilon
]

* Adds randomness for generation
* Enables smooth interpolation in latent space

---

### Decoder

* Repeats latent vector
* Uses LSTM to reconstruct sequences
* Outputs probability distribution over vocabulary

---

### Loss Function

VAE loss combines two parts:

1. Reconstruction Loss

* Measures how well output matches input

2. KL Divergence Loss

* Regularizes latent space

[
Loss = Reconstruction + KL Divergence
]

---

## 4. Text Generation

Steps:

1. Sample random vector from latent space
2. Pass through decoder
3. Generate probability distribution for each token
4. Sample words based on probabilities
5. Convert sequence back to text

---

## 5. Gradio Interface

The interface allows users to:

* Upload a PDF file
* Automatically train the VAE
* Generate new text

```python
iface = gr.Interface(...)
```

### Inputs:

* PDF file

### Outputs:

* Generated text

---

## Key Features

* End-to-end pipeline from PDF to generated text
* Uses deep learning for unsupervised text generation
* Interactive UI with Gradio
* Latent space sampling for creativity

---

## Limitations

* Training occurs every time a PDF is uploaded (slow)
* Generated text may lack coherence
* No pretrained embeddings used
* Small dataset reduces quality

---

## Improvements

* Save and reuse trained models
* Use pretrained embeddings (GloVe, BERT)
* Replace VAE with Transformer-based generator
* Add beam search instead of random sampling
* Increase dataset size for better learning

---

## Applications

* Story generation
* Document summarization (with modifications)
* Content creation tools
* Research on generative NLP

---

## Summary

This project demonstrates how a Variational Autoencoder can learn patterns from raw text extracted from PDFs and generate new sequences. By combining NLP preprocessing, sequence modeling, and a user-friendly interface, it provides a practical example of generative AI applied to text data.
