# JanusGraphBench
The Benchmark tool for JanusGraph performance
# How to Use:
Import as an Eclipse project. Under the project folder, there are a few pre-defined config file for benchmarker csv generator. 
###Example 1 Generate and load a tiny JanusgraphDB
	- JanusGraphBench /home/ubuntu/workspaces/JanusGraphBench/tiny_config.json /tmp
	- BatchImport <Path-to-your-janusgraph-config>/janusgraph-cassandra-es.properties /tmp/ /tmp/schema.json /tmp/datamapper.json
# Proposal 
###Populate entire graphdb with a configuration json. 
#####We should provide a default configuration that specify these elements (* is for now):  
	1. Vertices:
		* label names
		* Number of different label types
		* size (small, medium, large)
	2. Edges:
		* label names
		* Number of different label types
		* size (small, medium, large)
	3. Relation(Edge) pattern?
	4. Properties
		* Number of properties for:
		  - vertices(look at some existing data)
		  - edges(look at some existing data)
		* data types (use String and Integer first)
	5. Index
		* which key should be indexed?
		* types of index (composite or mixed)?
		* start with 2 properites first. 1 compostie and 1 mixed
	
###Performance Metric:
	1. How fast can we do these types of transactions (With pre-defined default or customized transaction scenarios):
		* Importing data
			- Use Simeon's importer
				- one csv for vertices: each line is a unique vertex
				- one csv for edges: each line is a relation
		* Concurrent Query (How to drive? See options below)
			- Define own test queries here. For example:
				- List all the edges of all vertices
				- List all vertices with certain properties
			- Drive using Simeon's despatcher through Gremlin server
		- delete?
		- update?
		- Insert(same as create vertices?)
	2. Metric to measure:
		* Avg. TPS
		* Avg. KB/sec?(A vertex can have any # of properties and edges so its size can vary)
		* Avg. latency
	3. known variables:
		- Transactions/sec VS Threads(users)
		- Number of Transactions for each commit
###Monitor:
	* nmon
	* gclog
	
	
###Hardware
####Single node:
	* 1 x cassandra + ES (1 composit index + 1 mixed inedex)
####Multiple nodes:
	* Cluster of 3 cassandra later?
	- Other data store? (hbase)
###Which interface should the driver use to generate data and send queries:
####Options:
	* Send APIs through Gremlin servers (web socket or REST)?
	* Stand alone Java Application?
###Codename:
	- Hermes?
###Ohter tests:
  1. https://github.com/njeirath/titan-perf-tester 
  2. https://www.slideshare.net/NakulJeirath/addressing-performance-issues-in-titancassandra
  3. https://aws.amazon.com/blogs/big-data/performance-tuning-your-titan-graph-database-on-aws/
  4. https://www.datastax.com/dev/blog/boutique-graph-data-with-titan
  5. http://s3.thinkaurelius.com/docs/titan/0.5.1/hadoop-performance-tuning.html
