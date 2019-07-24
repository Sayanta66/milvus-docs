---
id: creating-table
title: Creating a table
sidebar_label: Creating a table
---

# Creating a table

> Note: All the following actions are executed in Python. For other languages, Milvus supports RESTful and RPC.

## Prerequisites
When you have finished the installation and basic configuration of Milvus, you may go on and create a table to insert data into. Before that, ensure you have：

1. Imported pymilvus.

   ```python
   # Import pymilvus
   >>> from milvus import Milvus, Prepare, IndexType, Status

   ```
2. Connected Milvus to your local server.

   ```
   # Connect Milvus to server
   >>> milvus = Milvus()
   >>> milvus.connect(host='0.0.0.0', port='19530')
   Status(message='connected!', code=0)

   ```
   > Note: In the above code, default values are used for *host* and *port* parameters. They shoud be the value of the *address* and *port* you set in *server_config* file in *Configuring Milvus*.
   
## Creating a table
This section shows you how to create a table in Milvus. To make it easier to understand, all task procedures are based on an example of  Table test01 creation. Here are all related parameters. You can set parameter values to your needs.

|  Parameter  |  Description  |  Type   |  Reference value   |
| ------------| --------------| --------| ---------|
| table_name  | Name of the table you want to create (Table name can only be _, number and letter. The first character must be _ or letter, not a number. The entire length can not exceed 255 characters)| String | 'table name' |
| dimension   | Vector dimensions | Integer | 0 < dimension <= 16384 (Usually set to 128, 256 or 512)
| index_type  |5 types of indexing methods: 1. 'FLAT' - Precise vector indexing; 2. 'IVFLAT' - K-means based vector indexing. Search precision may be lower, but with faster speed.  |IndexType|FLAT / IVFLAT|


1. Prepare table parameters.
  
   ```
   # Prepare param
   >>> param = {'table_name':'test01', 'dimension':256, 'index_type':IndexType.FLAT}
   ```
   
   > Note: Table name is the unique identifier of a table in Milvus. So make sure there are no duplicated names.
   
2. Create Table test01.

   ```
   # Create a table
   >>> milvus.create_table(param)
   Status(message='Table test01 created!', code=0)
   ```
   
3. Verify details of the newly created table.
   ```
   # Verify table info.
   >>> status, table = milvus.describe_table('test01')
   >>> status
   Status(message='Describe table successfully!')
   >>> table
   TableSchema(table_name='test01',dimension=256, index_type=1, store_raw_vector=False)
   
   ```                        
