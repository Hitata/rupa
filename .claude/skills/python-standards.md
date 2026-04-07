---
name: python-standards
description: Python coding standards for this project — invoke when writing, reviewing, or modifying Python code
---

Follow these conventions for all Python code in this project:

## File-level docstrings
- **Required at the top of every module** — brief description of purpose
- One-line summary for simple modules, multi-line for complex ones
- Place after shebang (if present) and before imports

```python
"""Pose extraction pipeline for martial arts video decomposition.

This module provides frame-by-frame skeleton extraction using MediaPipe,
with configurable keypoint filtering and movement segmentation.
"""
```

## Import organization
- **Three sections separated by blank lines:**
  1. Standard library imports
  2. External library imports (third-party packages)
  3. Internal library imports (local modules)
- Alphabetize within each section
- One import per line for `from` imports

```python
"""Frame extraction utilities for source videos."""

# Standard library
import json
from pathlib import Path
from typing import Optional

# External libraries
import cv2
import numpy as np
from mediapipe.python.solutions import pose as mp_pose

# Internal libraries
from .config import DEFAULT_FPS
from .skeleton import SkeletonRenderer
```

## Method organization within classes
- **Use section separators with heavy comment blocks**
- Order: Public methods -> Private methods -> Static methods
- Two blank lines between sections
- Separator format: 69 equals signs (fits within 88-char line limit with 4-space indent)

```python
class PoseExtractor:
    """Extract pose keypoints from video frames."""

    def __init__(self, model_complexity: int = 2) -> None:
        """Initialize the pose extraction model."""
        self.pose = mp_pose.Pose(model_complexity=model_complexity)

    # =====================================================================
    # PUBLIC METHODS
    # =====================================================================

    def extract_from_video(self, video_path: Path) -> list[dict]:
        """Extract poses from all frames in a video."""
        pass

    def extract_from_frame(self, frame: np.ndarray) -> dict:
        """Extract pose from a single frame."""
        pass


    # =====================================================================
    # PRIVATE METHODS
    # =====================================================================

    def _validate_frame(self, frame: np.ndarray) -> None:
        """Validate input frame dimensions and type."""
        pass

    def _normalize_landmarks(self, landmarks: list) -> list[dict]:
        """Normalize landmark coordinates to [0, 1] range."""
        pass


    # =====================================================================
    # STATIC METHODS
    # =====================================================================

    @staticmethod
    def calculate_joint_angle(p1: dict, p2: dict, p3: dict) -> float:
        """Calculate angle between three keypoints."""
        pass
```

## Type hints
- **Required on all function signatures** — parameters and return types
- Use `None` for functions with no return value
- Use union types with `|` (Python 3.10+) or `Optional[T]` for nullable types

## Function docstrings
- **Required for all public functions** — use reStructuredText (reST) style
- First line: brief summary (imperative mood, no period)
- Use `:param name:` for parameter descriptions
- Use `:return:` and `:rtype:` for return value
- Use `:raises ExceptionType:` for expected exceptions

## PEP 8 compliance
- **Line length:** 88 characters (Black formatter default)
- **Naming:**
  - `snake_case` for functions, variables, modules
  - `PascalCase` for classes
  - `SCREAMING_SNAKE_CASE` for constants
- **Strings:** prefer double quotes `"text"` for consistency
- **Spacing:** 2 blank lines between top-level definitions, 1 within classes

## Tools
- Format with **Black** before committing
- Type-check with **mypy** in strict mode
- Lint with **ruff** (replaces flake8 + isort)
