# 🚀 DBMS Quick Revision for GATE CS/IT

High-yield revision notes covering **ER Modeling**, **Normalization (1NF–BCNF)**, and **Transactions & Concurrency Control** tailored for GATE CS/IT preparation.

---

## 📌 Table of Contents
1. [ER Model & Relational Schema Reduction](#1-er-model--relational-schema-reduction)
2. [Normalization & Functional Dependencies](#2-normalization--functional-dependencies)
3. [Transactions & Concurrency Control](#3-transactions--concurrency-control)

---

## 1. ER Model & Relational Schema Reduction

### Attribute Types
* **Simple / Atomic:** Cannot be divided further (e.g., `Age`).
* **Composite:** Can be split into sub-parts (e.g., `Name` $\rightarrow$ `First_Name`, `Last_Name`).
* **Multivalued:** Double oval; holds multiple values (e.g., `Phone_Number`). Requires a separate table during reduction.
* **Derived:** Dashed oval; calculated from other attributes (e.g., `DOB` $\rightarrow$ `Age`). Omitted in relational schema.

### Minimum Relational Tables Required
| Entity / Relationship Structure | Minimum Tables | Key Reduction Rule |
| :--- | :--- | :--- |
| **1 : 1 (Total participation on one side)** | 2 | Merge relationship table into total participation entity table. |
| **1 : N (One-to-Many)** | 2 | Merge relationship table into the **N-side** entity table. |
| **M : N (Many-to-Many)** | 3 | Dedicated table needed for relationship with PK = $(PK_A + PK_B)$. |
| **Weak Entity Set** | 1 (combined) | Combine weak entity with identifying relationship. PK = $(\text{Strong PK} + \text{Discriminator})$. |

---

## 2. Normalization & Functional Dependencies

### Candidate Key Closure Algorithm ($X^+$)
1. Start with attribute set $X$.
2. Add attributes determined by dependencies in $F$ until no new attributes can be added.
3. If $X^+$ contains all attributes in $R$, then $X$ is a **Super Key**.
4. If no proper subset of $X$ is a Super Key, $X$ is a **Candidate Key**.

### Normal Form Identification Rules
For every non-trivial Functional Dependency $X \rightarrow Y$:

| Normal Form | Allowed Condition ($X \rightarrow Y$) | Key Rule |
| :--- | :--- | :--- |
| **1NF** | Atomic values only | No multivalued or composite attributes allowed. |
| **2NF** | No Partial Dependency | Proper subset of Candidate Key cannot derive a Non-prime attribute. |
| **3NF** | No Transitive Dependency | Either **$X$ is a Super Key** OR **$Y$ is a Prime Attribute**. |
| **BCNF** | Determinant = Super Key | **$X$ must strictly be a Super Key**. |

### Decomposition Properties
* **Lossless Join:** Decomposition of $R$ into $R_1$ and $R_2$ is lossless iff:
  $$(R_1 \cap R_2) \rightarrow R_1 \quad \text{OR} \quad (R_1 \cap R_2) \rightarrow R_2$$
* **Dependency Preservation:** Preserved if $F^+ = (F_1 \cup F_2)^+$.
* *GATE Note:* 3NF guarantees both Lossless Join and Dependency Preservation. BCNF guarantees Lossless Join, but Dependency Preservation is not guaranteed.

---

## 3. Transactions & Concurrency Control

### ACID Properties
* **Atomicity:** All-or-nothing execution (Handled by *Transaction/Recovery Manager*).
* **Consistency:** Database remains valid before and after transaction (Handled by *Programmer/User*).
* **Isolation:** Concurrent execution produces same result as serial execution (Handled by *Concurrency Control Subsystem*).
* **Durability:** Committed updates survive system crashes (Handled by *Recovery Manager*).

### Conflict Serializability & Precedence Graph
Two operations conflict if they belong to different transactions, access the same item, and at least one operation is a **Write ($W$)**.

1. Create a node for each transaction $T_i$.
2. Draw directed edge $T_i \rightarrow T_j$ for conflicting operations where $T_i$ executes first.
3. **No Cycle $\implies$ Conflict Serializable** (and View Serializable).
4. Use Topological Sort on acyclic graphs to find the equivalent serial order.

### Schedule Hierarchy
* **Recoverable:** If $T_j$ reads data written by $T_i$, $T_i$ must commit **before** $T_j$.
* **Cascadeless (ACA):** Transaction reads $X$ only after the writing transaction has **committed**.
* **Strict:** Transaction cannot read or write $X$ until the writing transaction has **committed**.

$$\text{Strict} \subset \text{Cascadeless} \subset \text{Recoverable}$$

### Lock-Based Protocols (2PL)
* **Basic 2PL:** Growing phase (acquire locks) $\rightarrow$ Shrinking phase (release locks). Guarantees Conflict Serializability; allows Deadlocks and Cascading Aborts.
* **Strict 2PL:** Holds **Exclusive (X) locks** until Commit/Abort. Guarantees Cascadeless schedules.
* **Rigorous 2PL:** Holds **Shared (S) and Exclusive (X) locks** until Commit/Abort.
