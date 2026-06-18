# CI/CD Configuration

```yaml
# .github/workflows/test.yml
global:
  name: "Test Workflow"

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  test:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        python-version: ["3.9", "3.10", "3.11"]
    steps:
      - uses: actions/checkout@v3
      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: ${{ matrix.python-version }}
      - name: Install dependencies
        run: pip install --upgrade pip && pip install -r requirements.txt
      - name: Run tests
        run: pytest tests/ -v --tb=short
```

```yaml
# .github/workflows/deploy.yml
global:
  name: "Deploy Workflow"

on:
  push:
    branches:
      - main
  workflow_dispatch:
    inputs:
      environment:
        description: "Target deployment environment"
        required: true
        default: "production"
        choices:
          - staging
          - production

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Deploy to ${{ inputs.environment }}
        run: |
          echo "Deploying to ${{ inputs.environment }} environment"
          # Your deployment commands go here
```