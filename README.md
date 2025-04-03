


# Multi-modal Retrieval with SDEN & BLIP2

This project implements a **multi-modal retrieval** system using **SDEN (Symmetric Dynamic Emergence Network)** and **BLIP2** as the model backbone. It is designed for **evaluating multi-modal retrieval tasks** on datasets such as **Flickr30k**, **ViQuAE**, and **Infoseek**.

## 🔥 Features

- **SDEN-based embeddings** for both text and image encoding
- **BLIP2** for vision and language interaction
- Support for **multi-modal retrieval** (text → image or image → text)
- Retrieval metrics including **Recall@K**, **MRR**, **MAP**, **NDCG**, **R-Precision**, **Hit@K**
- **Caching of embeddings** for efficient evaluation
- **Evaluation pipeline** with automatic result saving (CSV/JSON)
- Easy to extend with more datasets and models

## ⚙️ Installation

Clone the repository and install the necessary dependencies:

```bash
git clone https://github.com/yourusername/qa_sden_agent.git
cd qa_sden_agent
pip install -r requirements.txt
```

Ensure that your **OpenAI API key** is set in your environment:

```bash
export OPENAI_API_KEY="sk-xxxxxxxxxxxxxx"
```

## 📂 Project Structure

```
qa_sden_agent/
├── sden/                      # SDEN model implementation
├── encoder/                   # BLIP2 encoder for multi-modal input
├── metrics/                   # Retrieval evaluation metrics
├── benchmarks/                # Datasets like F30K, Infoseek, ViQuAE
├── embeddings_cache/           # Cached query and image embeddings
├── results/                   # Evaluation results (CSV/JSON)
├── scripts/                   # Evaluation and retrieval scripts
├── config/                    # Configuration files (settings.yaml)
└── README.md                  # This file
```

## 🧑‍💻 Usage

### 1. Data Preparation

Download or prepare datasets in the following format:

```json
{
  "query": "A man playing guitar",
  "candidates": [
    {"id": "1", "image": "image1.jpg"},
    {"id": "2", "image": "image2.jpg"}
  ],
  "gt_id": "1"
}
```

Place datasets in the `benchmarks/` folder (e.g., `f30k/`, `viquae/`).

### 2. Run Evaluation

To evaluate the retrieval performance on **Flickr30k**, run:

```bash
python scripts/evaluate.py
```

This will:
- Load the dataset (e.g., `f30k`)
- Compute embeddings using SDEN and BLIP2
- Calculate retrieval metrics (Recall@K, MRR, etc.)
- Save results to `results/`

### 3. Evaluation Metrics

The following metrics will be computed and saved:
- **Recall@1, Recall@5, Recall@10**
- **Mean Reciprocal Rank (MRR)**
- **Mean Average Precision (MAP)**
- **Normalized Discounted Cumulative Gain (NDCG)**
- **R-Precision**
- **Hit@K**

You can view the results in the saved `eval.csv` file.

## 🧑‍🔬 Extending the System

### Add a New Dataset
To add a new dataset:
1. Place it in `benchmarks/`.
2. Update `config/settings.yaml` with the path.
3. Run `evaluate.py` for that dataset.

### Add a New Model
To use a different encoder model (e.g., `CLIP`, `BERT`):
1. Modify the `sden/` folder to implement your model.
2. Adjust `encoder/blip2_adapter.py` to use the new model.
3. Update the evaluation scripts accordingly.

## 🛠 Requirements

- Python >= 3.8
- PyTorch >= 1.9.0
- `transformers` (for BLIP2)
- `faiss-cpu` (optional for future indexing)
- `openai`
- `pyyaml`

Install the dependencies by running:

```bash
pip install -r requirements.txt
```

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🔗 References

- [Flickr30K Entities Dataset](https://github.com/BryanPlummer/flickr30k_entities)
- [SDEN Paper](link_to_paper)

