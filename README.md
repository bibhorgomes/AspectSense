# AspectSense: Multi-Criteria Product Intelligence via Metadata-Gated Hybrid RAG

**AspectSense** is an aspect-based product intelligence engine designed to analyze large-scale customer review datasets without falling into common retrieval traps. Instead of relying solely on standard vector search—which often overemphasizes isolated negative reviews—AspectSense uses a **dual-stream architecture** that pairs exact relational statistical baselines with filtered semantic retrieval, synthesizing grounded product reports with 100% verified citations.

---

## 💡 What Problem Does This Solve?

When standard Retrieval-Augmented Generation (RAG) is applied to thousands of e-commerce reviews, two common issues arise:

1. **Sampling Bias:** If an LLM is given only 3 retrieved negative reviews about a phone's camera, it will claim the camera is terrible—even if 90% of verified buyers gave it 5 stars.
2. **Cross-Product Contamination:** Review phrasing is often identical across models (e.g., *"Camera quality is very poor indoors"*). Pure vector search lacks entity boundaries and frequently pulls reviews from the wrong phone brand or model.

**AspectSense resolves both problems** by fetching exact macro statistics from an indexed SQL database while strictly gating semantic vector retrieval to the target device and rating criteria before generating answers with **Gemma 3 4B**.

---


## 🔍 How to Explore This Project

* **View the Complete Code & Pre-Rendered Outputs:** Open [`notebooks/aspectsense-pipeline-eval.ipynb`](notebooks/aspectsense-pipeline-eval.ipynb) directly on GitHub. All cells, UI screenshots, benchmark tables, and generated Gemma 3 outputs are pre-rendered and viewable without running code.
* **Read the Technical Report:** Open [`docs/AspectSense_Technical_Report.pdf`](docs/AspectSense_Technical_Report.pdf) for the complete methodology, mathematical formulations, and detailed ablation discussions.
* **Inspect the Precomputed Artifacts:** Explore [`artifacts/`](artifacts/) to see the indexed SQLite schema and FAISS mapping structure used for local deployment.

---

## 📁 Repository Structure & Contents

```text
AspectSense/
├── artifacts/
│   ├── aspectsense.db               # SQLite database of 50,000 reviews with multi-aspect ratings
│   ├── aspectsense.index            # Precomputed FAISS index (IndexFlatIP, d=384)
│   └── index_to_review_id.json      # Mapping dictionary linking vector index IDs to database review IDs
├── benchmarks/
│   ├── benchmark_metrics.json       # Quantitative evaluation results across 50 multi-aspect test queries
│   └── retrieval_benchmark.png      # High-resolution benchmark comparison charts (MRR, Precision, Latency)
├── docs/
│   ├── architectural_diagram.png   # Full system workflow diagram (Router -> SQL / Hybrid RRF -> Gemma 3)
│   └── AspectSense_Technical_Report.pdf # Complete technical report covering methodology, math, and ablation studies
├── notebooks/
│   └── aspectsense-pipeline-eval.ipynb # End-to-end executable notebook containing pipeline code and pre-rendered outputs
├── .gitignore                       # Git ignore file for Python environments and temporary files
└── README.md                        # Project overview and documentation




