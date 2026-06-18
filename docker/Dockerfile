FROM python:3.11-slim

# Set environment variables
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1
ENV DEBIAN_FRONTEND=noninteractive

# Install system dependencies
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        build-essential \
        python3-dev \
        && rm -rf /var/lib/apt/lists/*

# Set Python version
RUN pip install --no-cache-dir --upgrade pip \
    && pip install --no-cache-dir -r requirements.txt

WORKDIR /app

# Copy requirements and package files
COPY .env.example .env.example

# Create virtual environment
RUN python -m venv /opt/venv
ENV PATH="/opt/venv/bin:$PATH"

# Install dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Copy project files
COPY . .

# Set up pre-commit hooks
RUN echo "git init" > /tmp/.git-init && chmod +x /tmp/.git-init
RUN echo "git add ." >> /tmp/.git-add && chmod +x /tmp/.git-add
RUN echo "git commit -m 'Initial commit'" >> /tmp/.git-commit && chmod +x /tmp/.git-commit

# Copy pre-commit config
COPY .pre-commit-config.yaml /tmp/.pre-commit-config.yaml

# Install pre-commit hooks
RUN pip install pre-commit
RUN pre-commit install

# Create .gitignore file
RUN echo ".env" >> .gitignore
RUN echo "venv/*" >> .gitignore

# Copy additional configuration files
COPY docker/agent-ai-compose.yml /opt/compose/

# Set working directory
WORKDIR /app

# Expose port 8000
EXPOSE 8000

# Health check
CMD ["python", "main.py"]