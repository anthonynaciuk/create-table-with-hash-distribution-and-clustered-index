# create-table-with-hash-distribution-and-clustered-index
create SQL table using hash distribution and clustered index


	• Use SQL code to choose Distribution and Indexing types for large datasets (>1,000,000 to >50,000,000 rows.)
		○ Distribution types: 
			§ Round robin, use for <60,000,000 row datasets
			§ Hash, use for <60,000,000 row datasets 
			§ Clustered, use for >60,000,000 row datasets
		○ Index methods: 
			§ Copy command, Bulk insert, Polybase.
		○ Heap:
			§ Not an index
			§ Not a distribution
			§ Mention it like a 'Distribution type' - speeds up queries in use cases of many queries on small datasets
		○ Partitions:
			§ Can be used to partition data for faster computation, get results from certain datasets sooner than other partitions
			§ Partitioning in MySQL is used to split or partition the rows of a table into separate tables in different locations, but still, it is treated as a single table. It distributes the portions of the table's data across a file system based on the rules we have set as our requirement.


	-- Note on creating Indexes
	CREATE TABLE [logdata]
	(
	    [Correlation id] [varchar](200) NULL,
	    [Operation name] [varchar](200) NULL,
	    [Status] [varchar](100) NULL,
	    [Event category] [varchar](100) NULL,
	    [Level] [varchar](100) NULL,
	    [Time] [datetime] NULL,
	    [Subscription] [varchar](200) NULL,
	    [Event initiated by] [varchar](1000) NULL,
	    [Resource type] [varchar](1000) NULL,
	    [Resource group] [varchar](1000) NULL,
	    [Resource] [varchar](2000) NULL
	)
	WITH  
	(   
	    DISTRIBUTION = HASH ([Operation name]),
	    CLUSTERED INDEX ([Resource type])
	)
	
CREATE INDEX EventCategoryIndex ON [logdata] ([Event category])![image](https://github.com/anthonynaciuk/create-table-with-hash-distribution-and-clustered-index/assets/114329733/aed2c67c-b509-4dbb-8e3c-e550f32d8895)
