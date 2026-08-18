# 📚 GATE CS/IT DBMS Revision - Main Index

Quick reference portal and topic index for GATE DBMS preparation.

---

## 📂 Topic Directory

### 1. [ER Modeling & Table Reduction](./README.md#1-er-model--relational-schema-reduction)
* **Attributes:** Simple, Composite, Multivalued, Derived.
* **Table Reduction Rules:**
  * 1:1 (Total Participation) $\rightarrow$ 2 Tables
  * 1:N $\rightarrow$ 2 Tables (Merge on N-side)
  * M:N $\rightarrow$ 3 Tables
  * Weak Entity $\rightarrow$ 1 Combined Table

---

### 2. [Normalization & FDs](./README.md#2-normalization--functional-dependencies)
* **Closure Algorithm ($X^+$):** Finding Candidate Keys & Super Keys.
* **Normal Form Hierarchy:**
  * **1NF:** Atomic values only.
  * **2NF:** No Partial Dependency.
  * **3NF:** $X$ is Super Key OR $Y$ is Prime Attribute.
  * **BCNF:** $X$ must be Super Key.
* **Decomposition:** Lossless Join condition vs Dependency Preservation.

---

### 3. [Transactions & Concurrency Control](./README.md#3-transactions--concurrency-control)
* **ACID Properties:** Responsibility mapping.
* **Conflict Serializability:** Precedence Graph testing & cycle detection.
* **Schedules:** Strict $\subset$ Cascadeless $\subset$ Recoverable.
* **Concurrency Protocols:** Basic 2PL, Strict 2PL, Rigorous 2PL.

---

## ⚡ Quick Formula & Decision Cheatsheet

```text
[Is X -> Y in Non-Trivial FD?]
       |
       +--> Is X a Super Key? --(YES)--> [BCNF]
       |          |
       |         (NO)
       |          v
       +--> Is Y a Prime Attribute? --(YES)--> [3NF]
       |          |
       |         (NO)
       |          v
       +--> Is X a Partial Key? --(YES)--> [1NF Only]
                  |
                 (NO)
                  v
               [2NF]
