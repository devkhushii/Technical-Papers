# Python Virtual Environment – Quick Revision Cheat Sheet

## 1. What is a Virtual Environment?

A virtual environment creates an isolated Python environment for a project, keeping its packages separate from other projects.

## 2. Create a Virtual Environment

```bash
$ python3 -m venv .venv
```

- `-m` — Run a Python module as a script.
- `venv` — Module used to create virtual environments.
- `.venv` — Environment directory name.

## 3. Activate the Environment

**Linux / macOS:**

```bash
$ source .venv/bin/activate
(.venv) $
```

**Windows (Command Prompt):**

```cmd
> .venv\Scripts\activate
(.venv) >
```

## 4. Install Packages

```bash
(.venv) $ pip install requests
```

**Important flags:**

| Flag | Purpose |
|---|---|
| `-r` | Install packages from a requirements file |
| `--upgrade` | Upgrade a package |
| `--version` | Show pip version |

```bash
(.venv) $ pip install -r requirements.txt
(.venv) $ pip install --upgrade requests
(.venv) $ pip --version
```

## 5. Save and Install Dependencies

```bash
(.venv) $ pip freeze > requirements.txt
(.venv) $ pip install -r requirements.txt
```


## 6. Deactivate the Environment

```bash
(.venv) $ deactivate
$
```

## 7. Delete a Virtual Environment

First deactivate it, then remove its directory.

```bash
$ rm -rf .venv
```

- `-r` — Delete directories recursively.
- `-f` — Force deletion without prompting.


