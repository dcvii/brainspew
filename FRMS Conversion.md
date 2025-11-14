---
title: ChatGPT
source: https://chatgpt.com/g/g-p-67faf5ef2ee48191a6625794219afb1d-frms-conversion/c/67faf64e-e768-8004-bbbc-c565d909ef84
author:
  - "[[FRMS Conversion]]"
published:
created: 2025-11-13
description: ChatGPT is your AI chatbot for everyday use. Chat with the most advanced AI to explore ideas, solve problems, and learn faster.
tags:
  - clippings
---
Thanks! I now have the full structure of the Ruby code. I’ll start by converting the core logic and structure from Ruby to Python while keeping the same methods and data flow intact. Here's the Python version so far:

```python
python# Author: Michael Bowen (michael.bowen@full360.com)
# Converted from Ruby to Python
# All rights reserved - Do Not Redistribute

import os
import time
import shutil
import logging
from pathlib import Path
from datetime import datetime
from Crypto.Cipher import Blowfish

# Constants
HERE = os.getenv("STREAM_DIR", ".") + "/01_gather/"
METHOD = 'day-zero'
FULLFORCE = False
ENCRYPTED = True
TERAENV = 'TVIEW'

OUTBOX = os.getenv("OUTBOX", "/tmp/outbox")
S3_KEYFILE = os.getenv("S3_KEYFILE", "keyfile")
S3_IVFILE = os.getenv("S3_IVFILE", "ivfile")
FRYBOX = os.getenv("FRYBOX", "/tmp/frybox")

logger = logging.getLogger("FRMS")
logging.basicConfig(level=logging.INFO)

class SelectStatementError(Exception):
    pass

class GatherCurrent:
    def __init__(self, tdb, vdb, t_sequel):
        logger.info(f"-- Starting FRMS::GatherCurrent in {os.getenv('ENVIRONMENT', 'unknown')} --")
        self.tdb = tdb
        self.vdb = vdb
        self.t_sequel = t_sequel

    def cleanup(self, mess):
        for f in Path('.').glob(mess):
            os.remove(f)

    def encrypt_file(self, fspec):
        logger.info(f"-- encrypting {os.path.basename(fspec)} --")

        cipher = Blowfish.new(Path(S3_KEYFILE).read_bytes(), Blowfish.MODE_CBC, Path(S3_IVFILE).read_bytes())

        t = time.time()
        with open('enc.tmp', 'wb') as outf:
            with open(fspec, 'rb') as inf:
                while True:
                    chunk = inf.read(4096)
                    if not chunk:
                        break
                    outf.write(cipher.encrypt(chunk.ljust(4096, b'\x00')))
            outf.write(cipher.encrypt(b''))

        logger.info(f"{os.path.basename(fspec)} encrypt time: {time.time() - t} seconds")
        new_fspec = os.path.join(OUTBOX, os.path.basename(fspec))
        shutil.move('enc.tmp', new_fspec)

    def push_to_s3(self, fspec, buk):
        # Placeholder for actual S3 integration
        if ENCRYPTED:
            self.encrypt_file(fspec)

        fname = os.path.basename(fspec)
        logger.info(f"STEP THREE - send (encrypted) file to S3: {fspec}")

        today = datetime.now().strftime('%Y-%m-%d')
        year = today[:4]
        yearmo = today[:7]

        s3_object = f"{buk}/{year}/{yearmo}/{today}/{fname}"
        s3_bucket = 'dev.arms.qantas-flightops.com'
        aws_endpoint = 's3-ap-southeast-2.amazonaws.com'

        logger.info(f"Mock upload {fspec} to s3://{s3_bucket}/{s3_object}")

    def toss(self, mess):
        shutil.move(mess, FRYBOX)

    def fsize(self, fspec):
        act_fs = os.stat(fspec).st_size
        fname = os.path.basename(fspec)
        fs_kb = act_fs // 1024
        if fs_kb > 1024:
            fs_mb = fs_kb // 1024
            logger.info(f"{fname} is {fs_mb} MB")
            return f"{fs_mb} MiB"
        else:
            logger.info(f"{fname} is {fs_kb} KB")
            return f"{fs_kb} KiB"

    def file_stats(self, fspec):
        fname = os.path.basename(fspec)
        if os.path.exists(fspec):
            size = self.fsize(fspec)
            with open(fspec, 'r') as infile:
                line_count = sum(1 for _ in infile)
            return {'name': fname, 'line_count': line_count, 'status': 'OK', 'size': size}
        else:
            return {'name': fname, 'line_count': 0, 'status': 'DNE', 'size': 0}

    def get_records(self, erb, key):
        # Placeholder for sequel_erb_query
        logger.info("Running get_records (mock)")
        return {}

    def query_current(self):
        # Placeholder for actual SQL logic
        raise NotImplementedError("query_current method not yet implemented")
```

Would you like me to:

1. Fully implement the placeholders like `etl_stream` and `sequel_erb_query`?
2. Package this into a callable script or module?
3. Continue translating the rest of the Ruby file if there’s more?

Let me know how deep you want to go!

Got it — we'll use Jinja for SQL templating instead of Ruby's `etl_stream` or `sequel_erb_query`. I’ll revise the `get_records` method accordingly to render and optionally execute the Jinja SQL.

Here's the updated version of that method in Python:

```python
pythonfrom jinja2 import Environment, FileSystemLoader

def render_sql_template(template_path, context):
    env = Environment(loader=FileSystemLoader(os.path.dirname(template_path)))
    template = env.get_template(os.path.basename(template_path))
    return template.render(context)

def get_records(self, erb, key, context=None, db_conn=None):
    """
    Renders a SQL query from a Jinja template and executes it using the provided DB connection.
    
    Parameters:
        erb (str): Path to the Jinja SQL template file
        key (str): Optional key identifier (not used yet)
        context (dict): Variables to be used in Jinja rendering
        db_conn: A live DB-API 2.0 connection object
    """
    context = context or {}
    sql = render_sql_template(erb, context)
    logger.info(f"Executing SQL from {erb} with context {context}")

    if db_conn:
        with db_conn.cursor() as cursor:
            cursor.execute(sql)
            rows = cursor.fetchall()
            # You could use key here to structure the results if needed
            return rows
    else:
        logger.warning("No DB connection provided. Returning rendered SQL only.")
        return sql
```

Would you like the Jinja templates to reside in a fixed directory (like `templates/sql/`) and should I mock up an example template or SQL structure as well?

Perfect — I’ll assume the templates live alongside the Python code unless you specify otherwise.

Here’s the `get_records` method refined with that in mind:

```python
pythonfrom jinja2 import Environment, FileSystemLoader

def render_sql_template(template_filename, context):
    env = Environment(loader=FileSystemLoader(os.path.dirname(__file__)))
    template = env.get_template(template_filename)
    return template.render(context)

def get_records(self, erb, key, context=None, db_conn=None):
    """
    Renders and optionally executes a SQL query from a Jinja template.

    Args:
        erb (str): Jinja SQL template filename (in the same directory as the script).
        key (str): Placeholder for structuring the result (not used yet).
        context (dict): Variables passed to the template.
        db_conn: Optional DB connection object.

    Returns:
        If db_conn is provided, returns query results; otherwise returns the rendered SQL.
    """
    context = context or {}
    sql = render_sql_template(erb, context)
    logger.info(f"Executing SQL from template: {erb} with context: {context}")

    if db_conn:
        with db_conn.cursor() as cursor:
            cursor.execute(sql)
            return cursor.fetchall()
    else:
        return sql
```

Let me know when you're ready to hook up the database layer, or if you'd like to see how to log or cache the rendered SQL for later inspection!

Great — I’ll finish converting the rest of the Ruby code into Python now, preserving the logic and style but fitting it into our new Python ecosystem with Jinja SQL templates.

Here’s the remainder of the class `GatherCurrent`, picking up where we left off:

---

### 🔁 Continued GatherCurrent class (Python)

---

### 🧱 Optional: Sample usage

To help you see the overall flow, here’s a rough sketch of how it might be invoked:

---

### ✅ Recap of Completed Components:

- ✅ File encryption with Blowfish
- ✅ File S3 mock upload logic
- ✅ File cleanup, size, and stats
- ✅ Jinja-based SQL rendering and optional execution
- ✅ Full `GatherCurrent` class ported from Ruby

Would you like me to:

1. Create a simple Jinja SQL template to match your context structure?
2. Scaffold out the YAML configuration handling you may have had in the Ruby version?
3. Add error-handling/logging enhancements or S3 integration using `boto3`?

Let me know how you'd like to proceed.

Here's the Ruby ERB version you provided:

And here is the equivalent **Jinja2** SQL template version:

### Notes:

- `{{ source_table }}` replaces `<%= $source_table %>`
- `{{ last_time }}` replaces `<%= $last_time %>`
- The `~t.*` syntax might be dialect-specific or a placeholder; Jinja doesn't evaluate that—it just passes it through to the rendered SQL. If it's a real SQL dialect thing, keep it. If it's ERB-specific, you might just need `t.*`.

Let me know if you want a loader to validate all your Jinja SQL templates!

The most common file extension for Jinja templates is:

So for SQL templates, you might name your files like:

- `my_query.sql.j2`
- `incremental_load.sql.j2`
- `select_customers.sql.j2`

This helps clearly indicate both the content type (`.sql`) and the templating engine (`.j2`). Let me know if you want to set up a loader that scans all `.sql.j2` files in a directory.

In Python, using the `os` module, here are the equivalents:

### ✅ Ruby vs. Python Equivalents

| Ruby | Python (using `os`) |
| --- | --- |
| `File.basename(path)` | `os.path.basename(path)` |
| `File.stat(path).size` | `os.stat(path).st_size` |

### ✅ Example in Python:

Let me know if you want to get other file metadata (like creation or modification times) too!

The Ruby method:

is equivalent in Python to:

### ✅ Full Example in Python:

Note: `os.path.exists()` works for both files and directories. If you want to check only for files (not directories), use:

Let me know if you also want to check for symbolic links, directories, or permission checks.

In a Python REPL, you can print the type of a variable `h` using:

### Example:

This will output:

Let me know if you want a pretty-printed type analysis or structure inspection too!

To isolate and work with the `stat_result` object from `os.stat()`, you can assign it directly to a variable like this:

### Bonus: Pretty-print with field names

You can see all available fields using `dir()` or unpack it into a dictionary:

If you're curious about specific fields, here’s a common subset of `stat_result` attributes:

- `st_size`: size in bytes
- `st_mtime`: last modification time
- `st_ctime`: creation time on Windows / metadata change time on Unix
- `st_uid`: user ID of owner
- `st_gid`: group ID of owner
- `st_mode`: protection bits

Let me know if you want to convert timestamps into human-readable times too!

Here's the equivalent Python code, preserving the structure and logic of your Ruby snippet:

### Key Translations:

- Ruby's `Time.now` → Python's `time.time()`
- Encoding scrubber (`:invalid => :replace`, etc.) → `errors='replace'` in Python's file handling
- `gsub` calls → simple `str.replace` in Python
- Backticks for shell `mv` → `shutil.move()` in Python
- `$inbox` → `inbox_dir` passed in as an argument

Let me know if `inbox_dir` should come from a global or environment variable instead!

Yes — in Python, the equivalent of a **Ruby `begin...rescue` block inside a `proc`** is a `try...except` block inside a function (or lambda, though lambdas can only contain expressions, not blocks).

Here’s a clean way to do it using a `try` block within a function or callable:

### ✅ Example

### ✅ If you want to return something on error:

### ✅ Assigning the function to a variable (like a Ruby proc/lambda)

Let me know if you want to define a reusable decorator to wrap any block with error trapping too!

To get a list of files in a directory using a path and a wildcard in Python, use the `glob` module:

### ✅ Example using glob

### 🔁 Alternative using pathlib

Both approaches return a list of matching files. `pathlib` returns `Path` objects, while `glob` gives you strings.

Let me know if you want to recursively search subdirectories too!