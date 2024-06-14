#### Before beginning
##### Page layout of a heap table file
![image](https://github.com/Eric0329/ePlus/assets/3777869/7ead3fc5-dc01-4791-b744-823197c90f4b)

*Page layout of a heap table file from [Notes on Postgresql Internals](https://muatik.medium.com/notes-on-postgresql-internals-4050340c9f4f)*

##### Terminology
- heap file: every table and index is stored as an array of pages of a fixed size (usually 8 kB)
- block/page
- tuple/item/row 

##### Notes
- Setting the `Page Fill Factor` to Optimize Hot Update Table, 

##### Ref
- [Notes on Postgresql Internals](https://muatik.medium.com/notes-on-postgresql-internals-4050340c9f4f)
- [SQL and PostgreSQL: The Complete Developer's Guide, Section 22, 23](https://www.udemy.com/course/sql-and-postgresql/?couponCode=LEADERSALE24A)  
- [73.1. Database File Layout](https://www.postgresql.org/docs/current/storage-file-layout.html)
- [73.6. Database Page Layout](https://www.postgresql.org/docs/current/storage-page-layout.html)
- [Postgres Performance Boost: HOT Updates and Fill Factor](https://www.crunchydata.com/blog/postgres-performance-boost-hot-updates-and-fill-factor)


#### [3.2. COST ESTIMATION IN SINGLE-TABLE QUERY](https://www.interdb.jp/pg/pgsql03/02.html)
##### The cost formula and its factors:
- Total cost formula
  - `start-up cost + run cost`
- I/O Cost factors
  - [seq_page_cost](https://www.postgresql.org/docs/current/runtime-config-query.html#GUC-SEQ-PAGE-COST): 1.0
  - [random_page_cost](https://www.postgresql.org/docs/current/runtime-config-query.html#GUC-RANDOM-PAGE-COST): 4.0 
- CPU Cost factors
  - [cpu_tuple_cost](https://www.postgresql.org/docs/current/runtime-config-query.html#GUC-CPU-TUPLE-COST): 0.01
  - [cpu_operator_cost](https://www.postgresql.org/docs/current/runtime-config-query.html#GUC-CPU-OPERATOR-COST): 0.0025
  - [cpu_index_tuple_cost](https://www.postgresql.org/docs/current/runtime-config-query.html#GUC-CPU-INDEX-TUPLE-COST): 0.005

##### Number of Tuples, Pages, Index_tuples, and Index_tuples
- query from `pg_class` 

##### [Sequential Scan](https://www.interdb.jp/pg/pgsql03/02.html#321-sequential-scan)
![image](https://github.com/Eric0329/ePlus/assets/3777869/7a98263c-2f89-4fc6-9989-35240529b047)

##### [Index Scan](https://www.interdb.jp/pg/pgsql03/02.html#322-index-scan) 
![image](https://github.com/Eric0329/ePlus/assets/3777869/3c33d8cf-edc8-4779-be69-ed532e9e91df)
![image](https://github.com/Eric0329/ePlus/assets/3777869/3ea6a4f2-0709-4713-a2c0-69a2b93ffb30)
![image](https://github.com/Eric0329/ePlus/assets/3777869/58ec056d-44fa-4275-a4bc-e59f25141ab6)
![image](https://github.com/Eric0329/ePlus/assets/3777869/ea2c15e6-299a-4e6b-af8b-062b09141642)
![image](https://github.com/Eric0329/ePlus/assets/3777869/e7577fb3-c0f3-4ff5-81ce-c335ab1869c1)

- Selectivity: the proportion of the search range of the index that satisfies the `WHERE` clause
  - Most Common Value (MCV), categorizable data
![image](https://github.com/Eric0329/ePlus/assets/3777869/902caad9-94f3-4bd6-b19a-f7c40ad6ea92)

  - Histogram bounds, real numbers data
![image](https://github.com/Eric0329/ePlus/assets/3777869/36447fa0-3a47-44e2-8af3-6f12597ffba3)

#### 3.5. JOIN OPERATIONS
- Materialized Nested Loop Join
  - writes the inner table tuples to the work_mem or a temporary file [tuplestore.c] before running a nested loop join (https://github.com/postgres/postgres/blob/master/src/backend/utils/sort/tuplestore.c)
- Materialized Merge Join
  - materializes the result of the sorted inner table before merge join
  ![image](https://github.com/Eric0329/ePlus/assets/3777869/5c99d064-7dd0-466d-aa77-3e9ccdec9e81)

- Hybrid Hash Join with Skew
 

  
