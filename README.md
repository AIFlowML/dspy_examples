# DSPy Learning Notebooks

This repository contains DSPy learning notebooks for building and optimizing AI agents and programs.

## Quick Setup with UV

### 1. Install UV (Python Package Manager)

UV is a fast Python package manager and environment manager. Choose your installation method:

#### macOS/Linux:

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

#### Windows:

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

#### Alternative (via pip):

```bash
pip install uv
```

#### Homebrew (macOS):

```bash
brew install uv
```

### 2. Setup Project Environment

Clone the repository and set up the environment:

```bash
# Clone the repository
git clone <git@github.com:AIFlowML/dspy_examples.git>
cd dspy

# Create virtual environment with Python 3.13
uv venv --python 3.12

# Activate the virtual environment
source .venv/bin/activate  # On macOS/Linux
# or
.venv\Scripts\activate     # On Windows

# Install dependencies
uv sync
```

### 3. Environment Variables Setup

Create a `.env` file in the project root:

```bash
# Copy the example or create new .env file
cp .env.example .env  # if available
# or create manually:
touch .env
```

Add your API keys to the `.env` file:

```env
OPENAI_API_KEY=your_openai_api_key_here
DLAI_LOCAL_URL=http://localhost:{port}
```

### 4. Running MLflow (for Lesson 3)

For lesson 3, you'll need to run MLflow UI locally:

```bash
# Make sure your virtual environment is activated
source .venv/bin/activate

# Start MLflow UI on port 8080
mlflow ui --port 8080
```

Keep this terminal window open while working with Lesson 3. MLflow UI will be available at `http://localhost:8080`

### 5. Running Jupyter Notebooks

Start Jupyter Lab or Notebook:

```bash
# Make sure your virtual environment is activated
source .venv/bin/activate

# Start Jupyter Lab (recommended)
jupyter lab

# or Jupyter Notebook
jupyter notebook
```

## Project Structure

```
dspy/
├── .env                    # Environment variables (create this)
├── .venv/                  # Virtual environment (auto-created by uv)
├── pyproject.toml          # Project dependencies
├── uv.lock                 # Lockfile for exact versions
├── Lesson_2.ipynb         # Sentiment Classification
├── Lesson_3.ipynb         # MLflow Tracing & Debugging
├── Lesson_4.ipynb         # Advanced DSPy Features
├── dspy_program/           # DSPy program modules
└── README.md               # This file
```

## Lessons Overview

- **Lesson 2**: Building a sentiment classifier with DSPy
- **Lesson 3**: Debugging DSPy agents with MLflow tracing
- **Lesson 4**: Advanced DSPy optimization and evaluation

## Troubleshooting

### Environment Activation

If you forget to activate the environment, you'll see import errors. Always run:

```bash
source .venv/bin/activate  # macOS/Linux
.venv\Scripts\activate     # Windows
```

### MLflow Connection Issues

If MLflow can't connect, ensure:

1. MLflow UI is running: `mlflow ui --port 8080`
2. Your `.env` file has the correct `DLAI_LOCAL_URL`
3. The port 8080 is not being used by another service

### Missing Dependencies

If packages are missing:

```bash
uv sync  # Sync all dependencies
uv add package_name  # Add specific package
```

## Requirements

- Python 3.10+
- OpenAI API Key
- Internet connection for package installation

## Quick Commands Reference

```bash
# Setup (one-time)
uv venv --python 3.13
source .venv/bin/activate
uv sync

# Daily workflow
source .venv/bin/activate  # Always activate first
mlflow ui --port 8080      # For Lesson 3 (separate terminal)
jupyter lab                # Run notebooks
```

## Support

If you encounter issues:

1. Ensure UV is properly installed: `uv --version`
2. Check virtual environment is activated: `which python`
3. Verify dependencies are installed: `uv sync`
4. Check your `.env` file contains the required API keys
