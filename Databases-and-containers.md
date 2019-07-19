# IMPORTANT

In this solution's current configuration for a development environment, the SQL databases are automatically deployed with sample data into a single SQL Server container (a single shared Docker container for SQL databases) so the whole solution can be up and running without any dependency to any cloud or a specific server. Each database could also be deployed as a single Docker container, but then you'd need much more than 8GB of RAM assigned to Docker in your development machine, just to be able to run five SQL Server Docker containers.

A similar case is defined in regard to Redis cache running as a container for the development environment. Or a No-SQL database (MongoDB) running as a container.

However, in a real production environment it is recommended to have your databases (SQL Server, Redis, and the NO-SQL database, in this case) in HA (High Availability) services like Azure SQL Database, Redis as a service and Azure CosmosDB instead the MongoDB container (as both systems share the same access protocol). If you want to change to a production configuration, you'll just need to change the connection strings once you have set up the servers in an HA cloud or on-premises.
