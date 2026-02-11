# Data Science Project

This repo contains material for the course **Data Science Project** at Aarhus University.

In the repo there is the following

- four folders:
  - notebooks: teaching material for the course
  - data_science_project: this is where you could start building your packages, scripts, logic etc. *(folder for the uv project)*
  - tests: folder where you would write tests for your code *(folder for the uv project)*
  - guides: guides on installing python 

- README.md: this file
- uv.lock: keeps track of the exact versions used *(folder for the uv project)*
- pyproject.toml: orchestrate your project dependencies *(folder for the uv project)*

## Notebooks

For the teaching in this course we will be using [jupyter notebooks](https://docs.jupyter.org/en/latest/) which requires the students to either:

1. Use [google colab](https://colab.google/) as the environment for editing and executing the notebooks. __NB__ this is what will be used in the Machine Learning course.

2. Install jupyter in your local environment or in a [virtual environment](#virtual-environments). Once jupyter is installed you can run the code `jupyter notebook` in your command line or terminal. This will initialize a jupyter session.

__Note__ notebooks are great for teaching/learning, and therefore very useful for the current purpose, however, once you have learned the basics and wish to start developing actual applications, packages etc. you should no longer be using the notebook format.

## Virtual environments

A virtual environment is an isolation of python interpreter, libraries and scripts for your projects.

It is useful to use virtual environments

- If you need different packages or versions in your projects.
- Using a single environment, you might break existing projects when doing new installations for new projects
- Good practice to use a virtual environments for all your projects

We will use `uv` as virtual environment handler.

### uv

>a tool for dependency management and packaging in Python. uv allows you to declare the libraries your project depends on and manages their installation and updates. It also provides a lockfile to ensure repeatable installs.

- A tool for dependency management and packaging in Python.
- Allows you to declare the libraries your project depends on, and it will manage (install/update) them for you.
- Offers a lockfile to ensure repeatable installs

__NOTE:__ you need have python and uv installed and if you have not already have a look at the [guide in the guides-folder](guides/setup.md)

Jupyter is preinstalled in the uv project, hence, by following the steps [get started on the current project (data_science_project)](#get-started-on-the-current-project-data_science_project) you will have jupyter installed.

Once it installed you can run the command:

```bash
uv run jupyter notebook
```

#### get started on the current project (data_science_project)

1. open a command prompt or terminal window.
2. navigate to the `data-science-project` folder (the folder that holds this README.md)
3. run the command

```bash
uv sync
```

Now you are ready to start working :-)

#### basics of uv

**Creating a project (new)**

Creating a new project by calling the command `uv init <project-name>`, eg called python-project:

this will create the following:

```bash
python-project
├── README.md
├── python_project
│   └── __init__.py
├── pyproject.toml
└── tests
    └── __init__.py
```

Initialize a pre-existing project by running uv init.  This let you interactively create a pyproject.toml file in the current directory

**Dependencies**

Add package to environment:

- On the first installation a virtual env is created.

```bash
uv add <package_name>
```

Run using your dependencies:

```bash
uv run python <file.py>
```

**Pyproject.toml and uv.lock**

- pyproject.toml orchestrate your project dependencies
- uv.lock keeps track of the exact versions used.

- Running uv sync will install all dependencies from pyproject.toml and update uv.lock with the exact versions installed.

