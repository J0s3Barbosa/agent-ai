"""
Project structure for agent-ai development environment.
Contains the layout of the source code, documentation, and configuration files.
"""

from pathlib import Path


def get_project_root() -> Path:
    """Return the root path of the project."""
    return Path(__file__).resolve().parent.parent


PROJECT_ROOT = get_project_root()


def get_src_dir() -> Path:
    """Return the source directory."""
    return PROJECT_ROOT / "src"


def get_tests_dir() -> Path:
    """Return the tests directory."""
    return PROJECT_ROOT / "tests"


def get_docs_dir() -> Path:
    """Return the documentation directory."""
    return PROJECT_ROOT / "docs"


def get_config_files():
    """Return list of configuration files."""
    return [
        PROJECT_ROOT / ".env.example",
        PROJECT_ROOT / ".pre-commit-config.yaml",
        PROJECT_ROOT / "requirements.txt",
        PROJECT_ROOT / "pyproject.toml",
    ]


def get_ci_cd_dir() -> Path:
    """Return the CI/CD workflow directory."""
    return PROJECT_ROOT / ".github" / "workflows"


def get_security_doc() -> Path:
    """Return the security documentation file."""
    return PROJECT_ROOT / "SECURITY.md"


def get_docker_config() -> Path:
    """Return the Docker configuration files."""
    return [PROJECT_ROOT / "docker" / "Dockerfile", PROJECT_ROOT / "docker" / "agent-ai-compose.yml"]


def get_all_config_files() -> list[Path]:
    """Get all configuration file paths."""
    return sorted([f for f in get_config_files() if f.exists()], key=lambda x: x.parts)


def get_ci_cd_workflow_names() -> list[str]:
    """Return the names of CI/CD workflow files."""
    workflows = [w.name for w in get_ci_cd_dir().iterdir() if w.is_dir()]
    return sorted(workflows, key=lambda x: x.name)


# Example usage:
if __name__ == "__main__":
    print("Project Root:", PROJECT_ROOT)
    print("\nConfig Files:")
    for f in get_all_config_files():
        print(f"  - {f}")
    
    print("\nCI/CD Workflows:")
    for wf in get_ci_cd_workflow_names():
        print(f"  - {wf}")