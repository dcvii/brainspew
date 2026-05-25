---
title: "Manage RustFS Objects with MinIO Client"
source: "https://docs.rustfs.com/developer/mc.html"
author:
  - "[[RustFS]]"
published: 2026-04-27
created: 2026-05-24
description: "Manage RustFS objects using the MinIO Client."
tags:
  - "brain_spew"
---
## MinIO Client (mc)

The MinIO Client (`mc`) is a command-line tool for managing object storage services. It supports MinIO, Amazon S3, and other S3-compatible services. As RustFS is S3-compatible, you can use `mc` to manage RustFS objects.

Prerequisites:

- An available RustFS instance. Refer to the [Installation Guide](https://docs.rustfs.com/installation/).
- The `mc` tool is installed.
- Available [access keys](https://docs.rustfs.com/administration/iam/access-token.html).

## Using mc with RustFS

First, configure an alias for RustFS using the `mc alias` command:

```bash
mc alias set rustfs http://12.34.56.78:9000 ACCESS_KEY SECRET_KEY
```

Output:

```bash
Added \`rustfs\` successfully.
```

You can now use `mc` with the `rustfs` alias to create/delete buckets, upload/download files, etc.

### List Buckets

List all buckets:

```bash
mc ls rustfs
```

Output:

```bash
[2025-08-01 10:46:24 CST]     0B bucket-creation-by-api/
[2025-07-29 09:15:35 CST]     0B rustfs-demo/
[2025-08-03 09:44:45 CST]     0B bucket-creation-by-ui/
```

### Create Bucket

Create a bucket:

```bash
mc mb rustfs/bucket-creation-by-mc
```

Output:

```bash
Bucket created successfully \`rustfs/bucket-creation-by-mc\`.
```

### Delete Bucket

Delete a bucket:

```bash
mc rb rustfs/bucket-creation-by-mc
```

Output:

```bash
Removed \`rustfs/bucket-creation-by-mc\` successfully.
```

### Upload File

Upload a file to a bucket:

```bash
mc cp file_name rustfs/bucket-creation-by-mc
```

Output:

```bash
...path/to/file_name: 4 B / 4 B  ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓  12 B/s 0s%
```

### Delete File

Delete a file from a bucket:

```bash
mc rm rustfs/bucket-creation-by-mc/file_name
```

Output:

```bash
Removed \`rustfs/bucket-creation-by-mc/1.txt\`.
```

### Download File from Storage

Use `mc get` command to download a file from a bucket:

```bash
mc get rustfs/bucket-creation-by-mc/file_name ./file_name
```

Response:

```bash
...eation-by-mc/file_name: 4 B / 4 B  ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓  18 B/s 0s%
```