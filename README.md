# Retrieval-Augmented Multi-Agent System for Rapid SOW Generation

Multi-agent system that drafts Statements of Work from a retrieval-grounded corpus,
with compliance rules and human review gates between draft and delivery.

Peer-reviewed and presented (oral) at **IEEE ICMLA 2025**.
Paper: [arXiv:2508.07569](https://arxiv.org/abs/2508.07569)

## Why this exists

SOW drafting in a services business is high-volume, template-driven, and unforgiving
about compliance language. The interesting problem is not generation — it is grounding
the generated clauses in prior approved work and refusing to emit anything the source
corpus cannot support.

## Design

| Component | File | Role |
|---|---|---|
| Agent graph | `backend/graph.py` | Orchestration and control flow |
| Retrieval | `backend/vector_rag.py` | pgvector-backed grounding over prior SOWs |
| Compliance | `backend/compliance_checker.py`, `backend/rules.py` | Rule checks before a draft is releasable |
| Prompts | `backend/prompt.py` | Prompt construction |
| Model access | `backend/llm.py` | LLM interface |
| API | `backend/app.py` | Flask service |
| UI | `src/`, `frontend/` | React + Vite review surface |

Embeddings are built with `backend/generate_embeddings.py`.

## Run it

```bash
# backend
cd backend
cp .env.example .env          # set model + database credentials
pip install -r requirements.txt
python generate_embeddings.py # build the vector index
python app.py

# frontend (repo root)
npm install
npm run dev
```

## Citation

```bibtex
@inproceedings{gupta2025sow,
  title     = {Retrieval-Augmented Multi-Agent System for Rapid Statement of Work Generation},
  author    = {Gupta, Rahul},
  booktitle = {IEEE International Conference on Machine Learning and Applications (ICMLA)},
  year      = {2025},
  eprint    = {2508.07569},
  archivePrefix = {arXiv}
}
```
