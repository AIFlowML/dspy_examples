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

# Create virtual environment with Python 3.12 (recommended for compatibility)
uv venv --python 3.12

# Activate the virtual environment
source .venv/bin/activate  # On macOS/Linux
# or
.venv\Scripts\activate     # On Windows

# Install dependencies
uv sync
```

### 3. Environment Variables Setup

**Step 1: Create `.env.example` template (if it doesn't exist)**

```bash
# Create .env.example template
cat > .env.example << 'EOF'
# OpenAI API Configuration
OPENAI_API_KEY=your_openai_api_key_here

# MLflow Configuration for Local Development
DLAI_LOCAL_URL=http://localhost:{port}

# Optional: Other AI Provider Keys (uncomment if needed)
# ANTHROPIC_API_KEY=your_anthropic_key_here
# GOOGLE_API_KEY=your_google_key_here
EOF
```

**Step 2: Copy and customize your environment file**

```bash
# Duplicate .env.example to create your .env file
cp .env.example .env
```

**Step 3: Add your actual API keys to `.env`**

Edit the `.env` file with your real API keys:

```env
# Required: OpenAI API Key (get from https://platform.openai.com/api-keys)
OPENAI_API_KEY=sk-your-actual-openai-api-key-here

# Required for MLflow Integration (Lesson 3)
DLAI_LOCAL_URL=http://localhost:{port}
```

**⚠️ Important:** Never commit your actual `.env` file to version control!

### 4. Running MLflow for Testing and Debugging

MLflow is essential for tracing and debugging DSPy programs, especially in Lesson 3.

**Start MLflow UI locally during tests:**

```bash
# Terminal 1: Start MLflow UI (keep this running during lessons)
source .venv/bin/activate
mlflow ui --host 127.0.0.1 --port 8080

# You should see output like:
# [INFO] Starting gunicorn 20.1.0
# [INFO] Listening at: http://127.0.0.1:8080
```

**In Terminal 2: Run your notebooks**

```bash
source .venv/bin/activate
jupyter lab
```

**Test MLflow connection:**

```bash
# Check if MLflow is running
curl -I http://localhost:8080
# Should return: HTTP/1.1 200 OK
```

MLflow UI will be available at: `http://localhost:8080`

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

### Package Build Issues (sentencepiece, arbor-ai, vllm)

If you encounter build errors with packages like `arbor-ai` that depend on `sentencepiece`:

**Solution 1: Use Python 3.12 (Recommended)**

```bash
# Remove current environment and recreate with Python 3.12
rm -rf .venv
uv venv --python 3.12
source .venv/bin/activate
uv sync
uv add arbor-ai
```

**Solution 2: Install System Dependencies (macOS)**

```bash
# Install required build dependencies
brew install cmake pkg-config protobuf sentencepiece

# Set environment variables
export PKG_CONFIG_PATH="/opt/homebrew/lib/pkgconfig:$PKG_CONFIG_PATH"
export CMAKE_PREFIX_PATH="/opt/homebrew:$CMAKE_PREFIX_PATH"

# Try installation again
uv add arbor-ai
```

**Solution 3: Use Binary Packages Only**

```bash
# Force use of pre-built wheels
uv add arbor-ai --only-binary=all
```

**Solution 4: Alternative Packages**

If you only need core AI functionality:

```bash
# Install essential packages without heavy dependencies
uv add openai anthropic transformers torch
```

## Requirements

- Python 3.10+
- OpenAI API Key
- Internet connection for package installation

## Quick Commands Reference

```bash
# Setup (one-time)
uv venv --python 3.12
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
