# PCD

## Implementation

### Perf Benchmark

- [TPCH](https://www.tpc.org/tpch/default5.asp), [spec](https://www.tpc.org/TPC_Documents_Current_Versions/pdf/TPC-H_v3.0.1.pdf): demonstrate support to different queries, and perf is good

### Integration

- [Polars](https://pola.rs/)
- [Spark SQL](https://spark.apache.org/sql/)
- [Duck DB](https://duckdb.org/) _low priority_

### Exp Setup

#### Benchmark (Overhead analysis)

- TPC-H under different DBs, with or without PCD integration
- The overhead _under different policies_
  - The performance impact of each policy (on different relational operations), respectively
  - _optional_ with or without optimizations
- Metrics: throughput, exec time, different concurrency levels
- _Optional_: compare with other frameworks
  - access control-based policy enforcement framework?
  - static analysis-based approaches?

**What causes such overhead? How effective are the optimizations?**

#### How to demonstrate the policy enforcement works?

- How do related work demonstrate this?
- Expressiveness of the policy
  - Compare with other work
  - access control-based policy enforcement framework?
- Baseline: Coq proof? Verification time/version; => pass

#### Case Study

- Medical dataset?
- Policy? sources like
  - hospital
  - state laws
  - federal/EU regulations
- Task?
