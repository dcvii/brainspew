---
title: "What Are Deletion Vectors (DLV)?"
source: "https://www.confessionsofadataguy.com/what-are-deletion-vectors-dlv/"
author:
  - "[[Daniel]]"
published: 2025-07-27
created: 2025-08-11
description: "Deletion Vectors are a soft‑delete mechanism in Delta Lake that enables Merge‑on‑Read (MoR) behavior, letting update/delete/merge operations mark row positions as removed without rewriting the underlying Parquet files. This contrasts with the older Copy‑on‑Write (CoW) model, where even a single deleted record triggers rewriting of entire files YouTube+8docs.delta.io+8Medium+8. Supported since Delta Lake 2.3 (read-only), full […]"
tags:
  - "clippings"
---
Deletion Vectors are a **soft‑delete** mechanism in Delta Lake that enables **Merge‑on‑Read** (MoR) behavior, letting update/delete/merge operations mark row positions as removed without rewriting the underlying Parquet files. This contrasts with the older **Copy‑on‑Write** (CoW) model, where even a single deleted record triggers rewriting of entire files [YouTube +8 docs.delta.io +8 Medium +8](https://docs.delta.io/latest/delta-deletion-vectors.html?utm_source=chatgpt.com).

Supported since Delta Lake 2.3 (read-only), full deletion vector support for DELETE/UPDATE/MERGE appeared in later versions: DELETE in 2.4, UPDATE/MERGE in Delta 3.x [Miles Cole +4 docs.delta.io +4 delta.io +4](https://docs.delta.io/latest/delta-deletion-vectors.html?utm_source=chatgpt.com).

---

## ✅ Why Use Deletion Vectors?

- **Faster small changes**: Only binary bitmap metadata is written, rather than rewriting large Parquet files.
- **Write efficiency**: Particularly efficient when changes affect sparse rows across many files [Medium +11 delta.io +11 Towards AI +11](https://delta.io/blog/2023-07-05-deletion-vectors/?utm_source=chatgpt.com).
- **ACID semantics preserved**: Readers still get the correct view by merging with DLV metadata at read time.

However:

- **Read-time overhead**: Filtering DLV metadata adds overhead during queries.
- **Maintenance needed**: Unapplied deletion markers build up until compaction or purge [Medium +6 japila-books +6 Towards AI +6](https://books.japila.pl/delta-lake-internals/deletion-vectors/?utm_source=chatgpt.com).

---

## ⚙️ How They Work Under the Hood

### Enabling

On Databricks, settings can also auto-enable deletion vectors for new tables [YouTube +8 Databricks Documentation +8 Data in Action +8](https://docs.databricks.com/aws/en/delta/deletion-vectors?utm_source=chatgpt.com).

### Write-Time

When you delete rows (e.g. `DELETE WHERE`), Delta writes a **deletion vector file or log entry** —a bitmap of row positions using RoaringBitmap—without touching Parquet data files [Databricks Documentation +8 delta.io +8 Medium +8](https://delta.io/blog/2023-07-05-deletion-vectors/?utm_source=chatgpt.com).

### Read-Time

Delta reads the base Parquet + DLV metadata, applying filters to hide soft-deleted rows during query execution.

### Physical Cleanup

To remove soft-deleted rows physically:

- Run `OPTIMIZE` to compact affected Parquet files.
- Or use `REORG TABLE ... APPLY (PURGE)` to force rewriting files with DLVs applied [Medium +8 docs.delta.io +8 Towards AI +8](https://docs.delta.io/latest/delta-deletion-vectors.html?utm_source=chatgpt.com).
- Then `VACUUM` can remove old files beyond retention threshold.

---

## 📊 Copy-on-Write vs Merge-on-Read with Deletion Vectors

| Feature | Copy‑on‑Write | Merge‑on‑Read (Deletion Vectors) |
| --- | --- | --- |
| Write/Delete cost | Rewrites entire files | Writes small metadata only |
| Read-time cost | Minimal | Additional filtering overhead |
| Best for frequent updates | ❌ | ✅ |
| Best for read-heavy workloads | ✅ | ⚠️ (needs compaction) |
| Compaction required | Less often | Yes (OPTIMIZE/REORG) |

That heatmap in the image above illustrates how deletion vectors provide faster DELETE performance as file count and changes grow [Microsoft Learn +2 docs.delta.io +2 Databricks Documentation +2](https://docs.delta.io/latest/delta-deletion-vectors.html?utm_source=chatgpt.com) [Data in Action](https://www.datainaction.dev/en/post/databricks-deletion-vector-photon-predictive-io-comparing-performance?utm_source=chatgpt.com) [Medium +6 delta.io +6 delta.io +6](https://delta.io/blog/2023-07-05-deletion-vectors/?utm_source=chatgpt.com) [Towards AI +4 delta.io +4 Medium +4](https://delta.io/blog/2023-07-05-deletion-vectors/?utm_source=chatgpt.com).

---

## 💡 Best Practices for Data Engineers

1. **Enable on high-write tables** (Bronze/Silver layers) where DML is frequent [Data in Action +7 Reddit +7 delta.io +7](https://www.reddit.com/r/MicrosoftFabric/comments/1gjvig1/blog_unlock_faster_writes_in_delta_lake_with/?utm_source=chatgpt.com).
2. **Plan regular maintenance**: schedule `OPTIMIZE`, `REORG TABLE APPLY PURGE`, and `VACUUM`.
3. **Monitor read latency**: as DLV files accumulate, query performance may degrade.
4. **Be cautious with compatibility**: older clients or Delta sharing may not support DLV-enabled tables [Medium +5 Databricks Documentation +5 Microsoft Learn +5](https://docs.databricks.com/aws/en/delta/deletion-vectors?utm_source=chatgpt.com) [Medium](https://ange-kouame.medium.com/delta-lake-deletion-vectors-a-complete-overview-bf1b2dd3a7c0?utm_source=chatgpt.com) [Databricks Documentation](https://docs.databricks.com/aws/en/admin/workspace-settings/deletion-vectors?utm_source=chatgpt.com).
5. **Enable workspace auto‑enable** options on Databricks to enforce default usage for new tables [Databricks Documentation +2 Databricks Documentation +2 Microsoft Learn +2](https://docs.databricks.com/aws/en/admin/workspace-settings/deletion-vectors?utm_source=chatgpt.com).
6. **Consider using Photon + Predictive I/O** for further acceleration of deletion/update workloads in Databricks Runtime 14.x+ [YouTube +7 Databricks Documentation +7 Microsoft Learn +7](https://docs.databricks.com/aws/en/admin/workspace-settings/deletion-vectors?utm_source=chatgpt.com).

---

## 🔧 Sample Code

---

## 🧾 Summary

Deletion Vectors mark a big leap forward in efficient data mutation workflows within Delta Lake. They give you **low-latency deletes and updates** without immediate file rewrites, ideal for high-change tables—but they need **thoughtful maintenance** to keep query performance sharp. Choose wisely: use them where writes dominate and compaction is part of your data ops routine.

### Archive

- [July 2025](https://www.confessionsofadataguy.com/2025/07/)
- [June 2025](https://www.confessionsofadataguy.com/2025/06/)
- [May 2025](https://www.confessionsofadataguy.com/2025/05/)
- [April 2025](https://www.confessionsofadataguy.com/2025/04/)
- [March 2025](https://www.confessionsofadataguy.com/2025/03/)
- [February 2025](https://www.confessionsofadataguy.com/2025/02/)
- [January 2025](https://www.confessionsofadataguy.com/2025/01/)
- [December 2024](https://www.confessionsofadataguy.com/2024/12/)
- [November 2024](https://www.confessionsofadataguy.com/2024/11/)
- [October 2024](https://www.confessionsofadataguy.com/2024/10/)
- [September 2024](https://www.confessionsofadataguy.com/2024/09/)
- [August 2024](https://www.confessionsofadataguy.com/2024/08/)
- [July 2024](https://www.confessionsofadataguy.com/2024/07/)
- [June 2024](https://www.confessionsofadataguy.com/2024/06/)
- [May 2024](https://www.confessionsofadataguy.com/2024/05/)
- [April 2024](https://www.confessionsofadataguy.com/2024/04/)
- [March 2024](https://www.confessionsofadataguy.com/2024/03/)
- [February 2024](https://www.confessionsofadataguy.com/2024/02/)
- [January 2024](https://www.confessionsofadataguy.com/2024/01/)
- [December 2023](https://www.confessionsofadataguy.com/2023/12/)
- [November 2023](https://www.confessionsofadataguy.com/2023/11/)
- [October 2023](https://www.confessionsofadataguy.com/2023/10/)
- [September 2023](https://www.confessionsofadataguy.com/2023/09/)
- [August 2023](https://www.confessionsofadataguy.com/2023/08/)
- [July 2023](https://www.confessionsofadataguy.com/2023/07/)
- [June 2023](https://www.confessionsofadataguy.com/2023/06/)
- [May 2023](https://www.confessionsofadataguy.com/2023/05/)
- [April 2023](https://www.confessionsofadataguy.com/2023/04/)
- [March 2023](https://www.confessionsofadataguy.com/2023/03/)
- [February 2023](https://www.confessionsofadataguy.com/2023/02/)
- [January 2023](https://www.confessionsofadataguy.com/2023/01/)
- [December 2022](https://www.confessionsofadataguy.com/2022/12/)
- [November 2022](https://www.confessionsofadataguy.com/2022/11/)
- [October 2022](https://www.confessionsofadataguy.com/2022/10/)
- [September 2022](https://www.confessionsofadataguy.com/2022/09/)
- [August 2022](https://www.confessionsofadataguy.com/2022/08/)
- [July 2022](https://www.confessionsofadataguy.com/2022/07/)
- [June 2022](https://www.confessionsofadataguy.com/2022/06/)
- [May 2022](https://www.confessionsofadataguy.com/2022/05/)
- [April 2022](https://www.confessionsofadataguy.com/2022/04/)
- [March 2022](https://www.confessionsofadataguy.com/2022/03/)
- [February 2022](https://www.confessionsofadataguy.com/2022/02/)
- [January 2022](https://www.confessionsofadataguy.com/2022/01/)
- [December 2021](https://www.confessionsofadataguy.com/2021/12/)
- [November 2021](https://www.confessionsofadataguy.com/2021/11/)
- [October 2021](https://www.confessionsofadataguy.com/2021/10/)
- [September 2021](https://www.confessionsofadataguy.com/2021/09/)
- [August 2021](https://www.confessionsofadataguy.com/2021/08/)
- [July 2021](https://www.confessionsofadataguy.com/2021/07/)
- [June 2021](https://www.confessionsofadataguy.com/2021/06/)
- [May 2021](https://www.confessionsofadataguy.com/2021/05/)
- [April 2021](https://www.confessionsofadataguy.com/2021/04/)
- [March 2021](https://www.confessionsofadataguy.com/2021/03/)
- [February 2021](https://www.confessionsofadataguy.com/2021/02/)
- [January 2021](https://www.confessionsofadataguy.com/2021/01/)
- [December 2020](https://www.confessionsofadataguy.com/2020/12/)
- [November 2020](https://www.confessionsofadataguy.com/2020/11/)
- [October 2020](https://www.confessionsofadataguy.com/2020/10/)
- [September 2020](https://www.confessionsofadataguy.com/2020/09/)
- [August 2020](https://www.confessionsofadataguy.com/2020/08/)
- [July 2020](https://www.confessionsofadataguy.com/2020/07/)
- [June 2020](https://www.confessionsofadataguy.com/2020/06/)
- [May 2020](https://www.confessionsofadataguy.com/2020/05/)
- [April 2020](https://www.confessionsofadataguy.com/2020/04/)
- [March 2020](https://www.confessionsofadataguy.com/2020/03/)
- [January 2020](https://www.confessionsofadataguy.com/2020/01/)
- [December 2019](https://www.confessionsofadataguy.com/2019/12/)
- [November 2019](https://www.confessionsofadataguy.com/2019/11/)
- [October 2019](https://www.confessionsofadataguy.com/2019/10/)
- [September 2019](https://www.confessionsofadataguy.com/2019/09/)
- [August 2019](https://www.confessionsofadataguy.com/2019/08/)
- [July 2019](https://www.confessionsofadataguy.com/2019/07/)
- [May 2019](https://www.confessionsofadataguy.com/2019/05/)
- [March 2019](https://www.confessionsofadataguy.com/2019/03/)
- [February 2019](https://www.confessionsofadataguy.com/2019/02/)
- [January 2019](https://www.confessionsofadataguy.com/2019/01/)
- [December 2018](https://www.confessionsofadataguy.com/2018/12/)
- [November 2018](https://www.confessionsofadataguy.com/2018/11/)
- [October 2018](https://www.confessionsofadataguy.com/2018/10/)
- [September 2018](https://www.confessionsofadataguy.com/2018/09/)
- [July 2018](https://www.confessionsofadataguy.com/2018/07/)
- [June 2018](https://www.confessionsofadataguy.com/2018/06/)
- [May 2018](https://www.confessionsofadataguy.com/2018/05/)
- [April 2018](https://www.confessionsofadataguy.com/2018/04/)
- [March 2018](https://www.confessionsofadataguy.com/2018/03/)
- [February 2018](https://www.confessionsofadataguy.com/2018/02/)