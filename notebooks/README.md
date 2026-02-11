# Notebook Organization Guide

**Module-to-Notebook Mapping**

This document maps the existing Jupyter notebooks to the new module structure.

---

## Module 01: Python Fundamentals

The following notebooks from `notebooks/basic/` align with Module 01:

| Notebook | Topics Covered | Module Section |
|----------|----------------|----------------|
| `01_strings.ipynb` | String methods, formatting, slicing | Presentation slides 10-20 |
| `02_numbers.ipynb` | Arithmetic, type conversions, math operations | Presentation slides 21-28 |
| `03_lists.ipynb` | List creation, indexing, methods | Presentation slides 29-37 |
| `04_dictionaries.ipynb` | Key-value pairs, dict methods | Presentation slides 38-45 |
| `05_booleans.ipynb` | Boolean logic, comparison operators | Presentation slides 46-48 |
| `06_control_flow.ipynb` | if/elif/else, conditions | Presentation slides 49-55 |
| `07_loops.ipynb` | for/while loops, range() | Presentation slides 56-61 |
| `08_functions.ipynb` | Function definition, parameters, return | Presentation slides 62-67 |
| `09_file_io.ipynb` | Reading/writing files, with statement | Presentation slides 68-71 |

---

## Module 04: Pandas & Data Processing

The following notebooks from `notebooks/data_processing/` align with Module 04:

| Notebook | Topics Covered |
|----------|----------------|
| (TBD - analyze existing notebooks) | DataFrames, Series, cleaning |

---

## Module 05: Web Scraping & APIs

The following notebooks from `notebooks/data_retrieval/` align with Module 05:

| Notebook | Topics Covered |
|----------|----------------|
| (TBD - analyze existing notebooks) | HTTP requests, BeautifulSoup, APIs |

---

## Recommended Study Path

**For students:**

1. **Read module presentation** first for theory
2. **Work through notebooks** for interactive practice
3. **Complete module exercises** for assessment
4. **Build mini project** to integrate concepts

**Example workflow for Module 01:**
```bash
# Step 1: Study the presentation
cd modules/01_python_fundamentals
# Read 01_presentation.md (or PDF version)

# Step 2: Work through notebooks (in order)
cd ../../notebooks/basic
# Open and complete 01_strings.ipynb through 09_file_io.ipynb

# Step 3: Practice with exercises
cd ../../modules/01_python_fundamentals
# Complete 02_exercises.md
# Check your work with 03_solutions.md

# Step 4: Build the project
# Complete 04_mini_project.md
```

---

## Navigation Links

Each module README should include links to the relevant notebooks:

```markdown
## Recommended Notebooks

Work through these notebooks in order:

1. [Strings](../../notebooks/basic/01_strings.ipynb)
2. [Numbers](../../notebooks/basic/02_numbers.ipynb)
3. [Lists](../../notebooks/basic/03_lists.ipynb)
4. [Dictionaries](../../notebooks/basic/04_dictionaries.ipynb)
5. [Booleans](../../notebooks/basic/05_booleans.ipynb)
6. [Control Flow](../../notebooks/basic/06_control_flow.ipynb)
7. [Loops](../../notebooks/basic/07_loops.ipynb)
8. [Functions](../../notebooks/basic/08_functions.ipynb)
9. [File I/O](../../notebooks/basic/09_file_io.ipynb)
```

---

## File Structure

**Current structure (RECOMMENDED):**
```
data-science-project/
├── modules/
│   ├── 00_setup/
│   ├── 01_python_fundamentals/
│   └── ...
└── notebooks/
    ├── basic/           # Module 01 notebooks
    ├── data_processing/ # Module 04 notebooks
    └── data_retrieval/  # Module 05 notebooks
```

**Why this works:**
- Notebooks stay in centralized location
- Easy to find and navigate
- Modules reference notebooks via relative paths
- Students can work through notebooks independently

---

## For Instructors

### Adding New Modules

When creating new modules:

1. Create module directory: `modules/XX_name/`
2. Add README with notebook references
3. Create presentation: `01_presentation.md`
4. Create exercises: `02_exercises.md`
5. Create solutions: `03_solutions.md`
6. Create mini project: `04_mini_project.md`

**Link to notebooks:**
```markdown
## Recommended Notebooks

Complete these notebooks before attempting exercises:
- [Notebook Name](../../notebooks/category/notebook.ipynb)
```

### Updating Module README Files

Each module should have clear references to its notebooks:

```markdown
# Module XX: Topic Name

## Learning Objectives
...

## Prerequisites
...

## Recommended Notebooks

**Required:**
1. [Notebook 1](../../notebooks/basic/01_example.ipynb) - Core concepts
2. [Notebook 2](../../notebooks/basic/02_example.ipynb) - Advanced topics

**Optional:**
- [Bonus Notebook](../../notebooks/exercises/bonus.ipynb) - Extra practice

## Module Materials

1. **Presentation:** [01_presentation.md](01_presentation.md)
   - Theory and concepts
   - Code examples
   - Best practices

2. **Exercises:** [02_exercises.md](02_exercises.md)
   - Practice problems
   - Progressive difficulty (⭐ to ⭐⭐⭐)

3. **Solutions:** [03_solutions.md](03_solutions.md)
   - Complete solutions with explanations
   - Alternative approaches

4. **Mini Project:** [04_mini_project.md](04_mini_project.md)
   - Applied learning
   - Build a complete tool

## Study Path

1. Read presentation (1-2 hours)
2. Complete notebooks (2-4 hours)
3. Attempt exercises (2-3 hours)
4. Build mini project (3-8 hours)

Total time: ~10-15 hours
```

---

## Notebook Integration Scripts

### Check Broken Links

```python
# check_links.py
import os
from pathlib import Path

def check_markdown_links(root_dir):
    """Check if all notebook links in markdown files exist."""
    broken_links = []
    
    for md_file in Path(root_dir).rglob("*.md"):
        with open(md_file, 'r') as f:
            content = f.read()
            
        # Simple regex to find markdown links
        import re
        links = re.findall(r'\[.*?\]\((.*?\.ipynb)\)', content)
        
        for link in links:
            # Resolve relative path
            link_path = (md_file.parent / link).resolve()
            if not link_path.exists():
                broken_links.append({
                    'file': str(md_file),
                    'link': link,
                    'resolved': str(link_path)
                })
    
    return broken_links

# Usage
if __name__ == "__main__":
    broken = check_markdown_links("modules")
    if broken:
        print("Broken links found:")
        for link in broken:
            print(f"  In {link['file']}: {link['link']}")
    else:
        print("All links valid! ✅")
```

### List All Notebooks

```python
# list_notebooks.py
from pathlib import Path
import json

def list_all_notebooks(notebooks_dir):
    """List all notebooks with metadata."""
    notebooks = []
    
    for nb_file in Path(notebooks_dir).rglob("*.ipynb"):
        # Read notebook to get title
        with open(nb_file, 'r') as f:
            nb_data = json.load(f)
        
        # Extract title from first markdown cell
        title = "Untitled"
        for cell in nb_data.get('cells', []):
            if cell['cell_type'] == 'markdown':
                first_line = ''.join(cell['source']).split('\n')[0]
                if first_line.startswith('#'):
                    title = first_line.lstrip('#').strip()
                break
        
        notebooks.append({
            'path': str(nb_file),
            'relative': str(nb_file.relative_to(notebooks_dir)),
            'title': title
        })
    
    return notebooks

# Usage
if __name__ == "__main__":
    nbs = list_all_notebooks("notebooks")
    print(f"Found {len(nbs)} notebooks:\n")
    for nb in sorted(nbs, key=lambda x: x['relative']):
        print(f"{nb['relative']}: {nb['title']}")
```

---

## Summary

**Current approach:**
- ✅ Keep notebooks in centralized `notebooks/` folder
- ✅ Modules reference notebooks via relative links
- ✅ Clear mapping between modules and notebooks
- ✅ Easy for students to navigate

**Alternative approaches NOT used:**
- ❌ Moving notebooks into each module (creates duplication)
- ❌ Copying notebooks to multiple locations (hard to maintain)
- ❌ Separate notebook repo (adds complexity)

---

*Last updated: 2026-02-09*
