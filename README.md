# 📝 English-to-Dutch Neural Machine Translation

This project implements a Neural Machine Translation (NMT) system that translates from English to Dutch using a sequence-to-sequence (seq2seq) model with Bahdanau attention. The model is trained on the Europarl parallel corpus and leverages an LSTM-based encoder-decoder architecture with attention mechanisms to handle long sequences effectively.

---

## 🚀 Key Features

✅ **Seq2Seq with Attention**  
Uses an encoder-decoder architecture with Bahdanau attention to improve translation quality by focusing on relevant parts of the input sentence during decoding.

✅ **Teacher Forcing**  
Employs teacher forcing during training, where the decoder receives the correct previous target word, accelerating convergence.

✅ **BLEU Score Evaluation**  
Measures translation performance using the BLEU (Bilingual Evaluation Understudy) metric.

✅ **Preprocessing Pipeline**  
Handles text cleaning, tokenization, padding, and adding start/end tokens.

✅ **Interactive Translation Demo**  
Allows users to input English sentences and receive Dutch translations.

---

## 📂 Implementation Details

### 1️⃣ Data Preparation

- **Dataset**: Europarl parallel corpus (English-Dutch).
- **Preprocessing**:
  - Lowercasing
  - Removing punctuation
  - Adding `<start>` and `<end>` tokens
- **Train-Test Split**: 80% training, 20% testing.

---

### 2️⃣ Model Architecture

#### 🔹 Encoder
- **Embedding Layer**: Converts words into dense vectors.
- **LSTM Layer**: Processes input sequences and produces hidden states.

#### 🔹 Decoder with Bahdanau Attention
- **Embedding + LSTM**: Processes the target sequence during decoding.
- **Attention Mechanism**:
  - Computes alignment scores between encoder outputs and decoder hidden states.
  - Generates a context vector that focuses on relevant input words for each decoding step.
- **Dense Layer**: Predicts the next word in the target language.

---

### 3️⃣ Training

- **Optimizer**: Adam (`learning_rate=0.001`)
- **Loss Function**: Sparse Categorical Crossentropy
- **Callbacks**:
  - `ModelCheckpoint`: Saves the best-performing model during training.
  - `EarlyStopping`: Stops training when validation performance stops improving to prevent overfitting.

---

### 4️⃣ Inference & Evaluation

- **Greedy Decoding**: Translates sentences word by word by choosing the most probable next word at each step.
- **BLEU Score**: Evaluates translation quality against reference translations.
- **Interactive Demo**: Accepts user-provided English sentences and returns Dutch translations.

---

## 📌 Usage

After training the model:
```python
translator = Translator(encoder, decoder, en_vectorizer, nl_vectorizer, nl_idx2word, nl_word2idx)
translation = translator.translate("Hello, how are you?")
print("Dutch translation:", translation)
