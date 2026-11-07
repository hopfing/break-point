# 0001: A lakehouse for the data layer

Date: 2026-11-07

## Chose
Object storage (S3 API) holding raw files and Iceberg tables, a REST
catalog, and separate compute engines (Spark for loads and merges, Trino
for interactive SQL, DuckDB/PyIceberg in-process from Python). Runs locally
in Docker first; a cloud twin on S3 + Glue + Athena follows for comparison.

## Alternatives
- Parquet files on disk read with DuckDB/Polars (v1's approach): simplest,
  fast at today's size; no transactions, no schema evolution, no shared
  catalog, and every machine reads its own copy of the files.
- A database (Postgres/DuckDB file): fine for reference data; the raw
  estate is 300+ GB of semi-structured and tick-shaped data, which is not
  what a row store is for, and a single file does not serve three machines.
- Cloud-only from the start: pay-per-scan compute; egress makes local
  iteration expensive, and nothing works offline.

## Why this
Primarily to build the data layer the way an enterprise data platform is
built — object storage, an open table format, a shared catalog, and
engines chosen per workload — rather than the single-machine shortcuts a
personal project usually takes, on a dataset large enough that the
differences show. The design is also a reasonable fit for the project,
which is what makes it worth building here rather than on a toy:

- Scalability tenet: incremental `MERGE` into tables with snapshots and
  partition pruning, instead of full rebuilds, as the data grows.
- Observability tenet: raw lands in the store with an arrival manifest;
  every load is a tracked job; writes can be audited before publish.
- Point-in-time: Iceberg snapshots give "what did we know at time T" for
  free, which the backtesting requirements need.
- One store, many machines: the PC hosts storage; the Mac and Beelink run
  engines against it over the network.
- Engine independence: the same tables serve Spark, Trino, DuckDB and
  Python, so the engine can change without a data migration.

## Costs accepted
Several services to run; two JVM engines that are oversized for 300 GB
today; a serving story for the 16 GB Beelink that is not yet designed.

## Revisit when
- The parity/footprint comparison against plain Parquet + DuckDB shows no
  benefit at the real workload.
- Operating the stack takes more time than the research it supports.