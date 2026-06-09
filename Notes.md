# Notes to sort through



```
conf/               # WHAT to run        (Hydra)
  config.yaml
  model/ data/ training/
src/                # HOW to run it
  train.py  data.py
sweeps/             # a W&B sweep definition (you'll launch it on the cluster in S2)
  sweep_bayes.yaml
outputs/            # the immutable record of what happened (auto-created)
```


    project/
    ├── conf/
    │   ├── config.yaml
    │   ├── model/
    │   │   ├── baseline.yaml
    │   │   └── lightgbm.yaml
    │   ├── data/
    │   │   └── dataset.yaml
    │   └── jobs/
    │       ├── train.yaml
    │       └── evaluate.yaml
    │
    ├── data/
    │   ├── raw/
    │   ├── interim/
    │   ├── processed/
    │   └── external/
    │
    ├── notebooks/
    │   ├── exploratory/
    │   └── reports/
    │
    ├── src/
    │   ├── __init__.py
    │   ├── data/
    │   │   ├── load.py
    │   │   └── preprocess.py
    │   ├── features/
    │   │   └── build_features.py
    │   ├── models/
    │   │   ├── train.py
    │   │   ├── predict.py
    │   │   └── evaluate.py
    │   ├── visualization/
    │   │   └── plots.py
    │   └── utils/
    │       └── io.py
    │
    ├── scripts/
    │   ├── train_model.py
    │   ├── evaluate_model.py
    │   └── run_pipeline.py
    │
    ├── models/
    │   ├── checkpoints/
    │   └── final/
    │
    ├── reports/
    │   ├── figures/
    │   └── tables/
    │
    ├── tests/
    │   ├── test_data.py
    │   ├── test_features.py
    │   └── test_models.py
    │
    ├── outputs/
    │   ├── predictions/
    │   ├── metrics/
    │   └── logs/
    │
    ├── requirements.txt
    ├── pyproject.toml
    ├── README.md
    ├── .gitignore
    └── Makefile

---

sweeps with `--multirun`

    python train.y --multirun
    	training.lr=1e-5,2e-5,5e-5
    	model=bert_base,roberta_large

* runs sequentially 
---
What are sweep searches: hyperparameter search ove the same rum
* grid
* random
* bayesian
* early stopping (hyperband)

---
composable libraries for hugging face:
* transformers : models, tokens
* datasets
* evaluate
* accelerate

> from transformers import ( AutoTokenizer, AutoModel...

---
* keep code , config, and results separate

----
HPC cluster
* login nodes
* compute noes
* sjared filesystem

----
* literature exploration - extract methods, draft a reading plan, find papers
* boilerplating - configs, data loaders, sweep scripts, logging
* debugging
	* give access to repo - dont just paste 
	`The eval script crashes on the last batch. Fix it`
	runs the script
	reads traceback
	finds ragged final batch
	edits the collate function
	rereuns the check`

* first-pass plots - get a draft before refining
* writing support -- tables, captions, latex, error messages, docstrings
* managing jobs on the cluster -- check logs, relaunch failed jobs, summarize content

---
* decompose ! do not dump
* Do: give it steps. and tell it to draft a plan.

---
Clean the context often.

> Exhaustively list all the potential failure modes that fould impact the scientific validity of our conclusions

---
MCP vs Skill
* skill: reusable expertise: files that will ground its output. Bundle skills and knowledge and load on demand
* format results table
* 
**Core concept:** A skill is a directory containing a _SKILL.md_ file (with YAML frontmatter and instructions) plus optional _scripts/_, _references/_, and _assets/_ folders. This design supports **progressive disclosure** — agents first see a short description, then load full instructions, and finally fetch resources on demand.


---
consolidate memory at the end of each session
* update documentation

 can you get your overleaf onto vscode and give claude access to look for broken references.
 * how would we do this? is it renderable?
 * make a lsit of the claims to then use it as a guideline fo the supplimentary materials
 * create a list 
 * make an architecture for the appendix withplaceholders with missing information


---
academic papers
* make a skill for the paper guidelines that are found for paper writin per conference
* verify that i am complying with all the requirements
 * [ ] List item
