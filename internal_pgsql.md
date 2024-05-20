### Before beginning

#### Page layout of a heap table file
![image](https://github.com/Eric0329/ePlus/assets/3777869/7ead3fc5-dc01-4791-b744-823197c90f4b)

*Page layout of a heap table file from [Notes on Postgresql Internals](https://muatik.medium.com/notes-on-postgresql-internals-4050340c9f4f)*

#### Terminology
- heap file: every table and index is stored as an array of pages of a fixed size (usually 8 kB)
- block/page
- tuple/item/row 

#### Ref
- [Notes on Postgresql Internals](https://muatik.medium.com/notes-on-postgresql-internals-4050340c9f4f)
- [SQL and PostgreSQL: The Complete Developer's Guide, Section 22, 23](https://www.udemy.com/course/sql-and-postgresql/?couponCode=LEADERSALE24A)  
- [73.1. Database File Layout](https://www.postgresql.org/docs/current/storage-file-layout.html)
- [73.6. Database Page Layout](https://www.postgresql.org/docs/current/storage-page-layout.html) 


#### 3.2. COST ESTIMATION IN SINGLE-TABLE QUERY
The primary cost factors:
- I/O Cost
  - [seq_page_cost](https://www.postgresql.org/docs/current/runtime-config-query.html#GUC-SEQ-PAGE-COST): 1.0
  - [random_page_cost](https://www.postgresql.org/docs/current/runtime-config-query.html#GUC-RANDOM-PAGE-COST): 4.0 
- Cpu Cost
  - [cpu_tuple_cost](https://www.postgresql.org/docs/current/runtime-config-query.html#GUC-CPU-TUPLE-COST): 0.01
  - [cpu_operator_cost](https://www.postgresql.org/docs/current/runtime-config-query.html#GUC-CPU-OPERATOR-COST): 0.0025
  - [cpu_index_tuple_cost](https://www.postgresql.org/docs/current/runtime-config-query.html#GUC-CPU-INDEX-TUPLE-COST): 0.005

#### Selectivity: the proportion of the search range of the index that satisfies the `WHERE` clause
- Most Common Value (MCV)
- histogram_bounds
