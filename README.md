# Fraud monitoring and credit risk

Two independent analyses for a digital-banking case study:

| Notebook | Question | Dataset | Target |
|---|---|---|---|
| `fraud_monitoring.ipynb` | Which transactions should fraud operations review first? | `digital_bank_fraud_transactions.csv` | `is_fraud` |
| `credit_risk.ipynb` | Which customers are most likely to default within 90 days? | `digital_bank_default_case_study_dataset 1.csv` | `default_90d` |

The two datasets are unrelated; run the notebooks in any order.

## 1. Set up the environment (uv)

The project uses [uv](https://docs.astral.sh/uv/) and Python 3.15 (see `.python-version` and `pyproject.toml`).

Install uv if you do not have it:

```powershell
# Windows (PowerShell)
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

```bash
# macOS / Linux
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Already installed? Run `uv self update` so it can find Python 3.15.

Then, from the project folder:

```bash
uv sync
```

This downloads Python 3.15 if needed, creates `.venv`, and installs the exact versions pinned in `uv.lock`
(pandas, numpy, matplotlib, seaborn, scikit-learn, ipykernel).

## 2. Provide the datasets

By default the notebooks read the CSVs from a folder called `Interview Case Study` in the project root:

```
fraud-monitoring-credit-risk/
├── Interview Case Study/
│   ├── digital_bank_fraud_transactions.csv
│   └── digital_bank_default_case_study_dataset 1.csv
├── fraud_monitoring.ipynb
└── credit_risk.ipynb
```

The data files are not stored in the repository. Put them there, or point the notebooks to wherever you keep them.
Each notebook sets the path in one line near the top (the first code cell that loads data):

| Notebook | Variable | Default |
|---|---|---|
| `fraud_monitoring.ipynb` | `FRAUD_CSV` | `"Interview Case Study/digital_bank_fraud_transactions.csv"` |
| `credit_risk.ipynb` | `CREDIT_CSV` | `"Interview Case Study/digital_bank_default_case_study_dataset 1.csv"` |

Edit that string to your own path. Relative paths are resolved from the notebook's folder; absolute paths also work.
On Windows use forward slashes or a raw string to avoid backslash problems:

```python
FRAUD_CSV = "D:/data/digital_bank_fraud_transactions.csv"
CREDIT_CSV = r"D:\data\digital_bank_default_case_study_dataset 1.csv"
```

## 3. Run the notebooks

**VS Code:** open a notebook, click *Select Kernel* (top right), choose *Python Environments* then the `.venv` interpreter
in this folder, then *Run All*.
If `.venv` is not listed, run the command palette action *Python: Select Interpreter* and pick `.venv`, then reload the window.

**Jupyter in the browser:**

```bash
uv run --with jupyterlab jupyter lab
```

Open a notebook and choose the Python 3 kernel from this environment.

Both notebooks run top to bottom in a couple of minutes with no other setup and no random-seed surprises
(seeds are fixed). Each starts with a *Reader's guide* that marks which sections are core and which are supplementary.

## Adding packages

```bash
uv add <package>
```

This updates `pyproject.toml` and `uv.lock`.
