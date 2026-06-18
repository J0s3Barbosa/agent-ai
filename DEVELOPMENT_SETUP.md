# Development Environment Setup

```bash
# Clone the repository
git clone https://github.com/J0s3Barbosa/agent-ai.git

# Navigate to project directory
cd agent-ai

# Install dependencies
pip install -r requirements.txt

# Create .env file with environment variables
# Copy .env.example and modify as needed
```

## 🔧 Development Tools

### Required Packages

```python
# Core dependencies
pytest>=7.0.0
celery>=5.2.0
redis>=4.5.0
gunicorn>=21.0.0
psycopg2-binary>=2.9.0
requests>=2.31.0
```

### Pre-commit Hooks

```yaml
# .pre-commit-config.yaml
repos:
  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v4.5.0
    hooks:
      - id: check-yaml
      - id: end-of-file-fixer
```