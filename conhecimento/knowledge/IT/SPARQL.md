*Query language for [[RDF]].*

- Similar to [[SQL]], but for data stored in knowledge graphs instead of relational databases.
- Allows for adding, removing, retrieving data from graph databases. Queries can include optional patterns, aggregate results, and even use subqueries.
- Typical structure:
	- `PREFIX` declarations for namespaces
	- `SELECT` clause to specify variables to return
	- `WHERE` clause with graph patterns to match