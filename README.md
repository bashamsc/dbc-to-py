# dbc-to-py

Convert Databricks DBC exports into Databricks-style Python scripts (.py).

Features
- Simple and dependency-free.
- Handles JSON, base64, gzip, and zlib encoded DBC entries.
- Supports Databricks formats:
  - {"commands": [...]} (position-sorted)
  - {"cells": [...]} (Jupyter-like)
  - {"notebooks": [ ... ]} (multiple notebooks per entry)
- Writes "# Databricks notebook source" and "# COMMAND ----------" separators.
- Preserves original ZIP entry order.

Usage
- CLI:
  ```bash
  python dbc_to_py.py path/to/file.dbc [out_dir]
  # default out_dir is "<dbc_basename>_py"
  ```

- From code:
  ```python
  from converter import dbc_to_py
  py_files = dbc_to_py("your_dbc_file.dbc", "out_py")
  ```

Notes
- For non-Python notebooks (e.g., SQL), the converter adds a hint at the top of each cell (e.g., "%sql" or "# %% SQL cell").
- If an entry can't be decoded as JSON, it falls back to raw text as a single script.

License
MIT
