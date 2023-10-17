Separation of storage and compute is at the heart of lakehouse architecture. The physical data layer (parquet) upon which the logical layer (Open Table Format - Iceberg - metadata) is established to regulate queries (via index, partition, etc) requires a coordination layer or catalog. This control plane - or catalog - governs the data plane - or tables in storage - with respect to quality (schema, lineage) and access (ACL). 

I'd like to discuss the quality management aspect of Data Lakehousing and specifically that with regard to its differentiation from SCDs in Kimball Star Schema Data Warehousing. I believe there is not sufficient differentiation between the Warehouse and Lake disciplines in regards to MDM or referential integrity, so I will dismiss those aspects for the purpose of this context. 

Warehousing relies on history tables with start and end timestamps to version attributes with SCDs > Type 1. Lakehousing, on the other hand - via catalogs and metastores which are managed by catalogs - utilizes logical metadata table schema branching and copy-on-write data snapshots to preserve and manage lineage. 

In Kimball Star Schema SCD inside the Warehouse, not only is storage and compute co-located, but the attribute and its data are co-located. in the Lakehouse, the schema metadata is separate and apart from the data layer and also managed and versioned separately.

...