Separation of storage and compute is at the heart of lakehouse architecture. The physical data layer (parquet) upon which the logical layer (Open Table Format - Iceberg - metadata) is established to regulate queries (via index, partition, etc) requires a coordination layer or catalog. This control plane - or catalog - governs the data plane - or tables in storage - with respect to quality (schema, lineage) and access (ACL). 

I'd like to discuss the quality management aspect of Data Lakehousing and specifically that with regard to its differentiation from SCDs in Kimball Star Schema Data Warehousing. I believe there is not sufficient differentiation between the Warehouse and Lake disciplines in regards to MDM or referential integrity, so I will dismiss those aspects for the purpose of this context. 

Warehousing relies on history tables with start and end timestamps to version attributes with SCDs > Type 1. Lakehousing, on the other hand - via catalogs and metastores which are managed by catalogs - utilizes logical metadata table schema branching and copy-on-write data snapshots to preserve and manage lineage. 

In Kimball Star Schema SCD inside the Warehouse, not only is storage and compute co-located, but the attribute and its data are co-located. in the Lakehouse, the schema metadata is separate and apart from the data layer and also managed and versioned separately.

in RDBMS with compute storage schema and data co-located, if you make a schema change and want that reflected in your program, it requires a table migration involving a copy of the table data to the new version with its updated structure...

with Lakehouse there's none of that. it's zero-copy on schema change. the logical metadata layer is but an overlay transparently governing the new data without the need to physically relocate it.

Great paper and I agree with the flow and direction overall. There is one place where I think emphasis is overstated in one aspect and then in another way, you're missing a trick. I think ELT described as zero-copy transform-in-place is more representative than 'schema-on-read'.

I downloaded the source paper you cited and i suppose it has some historical importance although I don't really care about it. Your documentation of it is academically rigorous. I just have a disagreement with the convention. Have a good one.

One topic i would like to explore (collectively as an industry or sector or w/e) is the idea - in keeping with separation of storage and compute - of non-blocking read access and more or less unlimited analytical concurrency for distributed systems. We could, by a windy/jagged/tortuous path, achieve a single version of the truth again perhaps.

I'm referring to the dematerialization of the relational database for online analytical processing systems and specifically ROLAP queries of course.


