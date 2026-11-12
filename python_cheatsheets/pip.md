# Pip – Quick Revision Cheat Sheet

## 1. What is pip?

`pip` is Python’s package installer. It helps install, update, and remove Python packages.

## 2. Check pip

```bash
$ pip --version
pip x.x.x from ... (python x.x)
```

```bash
$ python -m pip --version
pip x.x.x from ... (python x.x)
```

## 3. Install Packages

```bash
$ pip install requests
```

**Install a specific version:**

```bash
$ pip install requests==2.31.0
```

**Install a minimum version:**

```bash
$ pip install "requests>=2.31.0"
```

**Important operators:**

| Operator | Purpose |
|---|---|
| `==` | Exact version |
| `>=` | Minimum version |
| `<=` | Maximum version |
| `!=` | Exclude a version |

## 4. Install from Requirements File

```bash
$ pip install -r requirements.txt
```

- `-r` — Install packages listed in a file.

## 5. Upgrade and Uninstall Packages

```bash
$ pip install --upgrade requests
$ pip uninstall requests
```

| Command | Purpose |
|---|---|
| `--upgrade` | Upgrade package |
| `uninstall` | Remove package |
| `-y` | Automatically confirm prompts |

```bash
$ pip uninstall -y requests
```

## 6. View Installed Packages

```bash
$ pip list
```

```bash
$ pip show requests
```

```bash
$ pip freeze
```

| Command | Purpose |
|---|---|
| `pip list` | List installed packages |
| `pip show package` | Show package details |
| `pip freeze` | List installed packages with exact versions |

## 7. Save Dependencies

```bash
$ pip freeze > requirements.txt
```

Save installed packages and their versions to `requirements.txt`.

## 8. Install Dependencies in a New Environment

```bash
$ python3 -m venv .venv
$ source .venv/bin/activate
(.venv) $ pip install -r requirements.txt
```

## 9. Important Commands at a Glance

| Command | Purpose |
|---|---|
| `pip install package` | Install package |
| `pip install package==1.0` | Install exact version |
| `pip install --upgrade package` | Upgrade package |
| `pip uninstall package` | Remove package |
| `pip list` | List installed packages |
| `pip show package` | Show package information |
| `pip freeze` | List packages with versions |
| `pip freeze > requirements.txt` | Save dependencies |
| `pip install -r requirements.txt` | Install dependencies from file |
| `python -m pip install package` | Install using the selected Python interpreter |

