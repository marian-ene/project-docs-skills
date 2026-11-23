# Investigate databases through MCP

Use an available database MCP connection when database behavior matters to the current flow or story. Verify the environment and the connection's permitted scope. Prefer catalog metadata and narrowly scoped read-only queries. Inspect definitions without executing business procedures, functions, or other operations that could have side effects. Keep data and schema read-only. Read actual rows only when necessary and permitted. Request the minimum columns and rows and prefer aggregates when they can answer the question.

Record the environment, verification date, objects checked, and scope alongside the finding. Keep personal data and secrets out of documentation. An observation applies to the environment checked. Limited metadata visibility or permissions leave object existence unverified. If MCP, the database, or a required permission is unavailable, document the limit and continue from available source such as ORM mappings, migrations, SQL, and tests. Label findings based on source evidence accordingly.

## Project Mapping

Build the database map incrementally alongside the application flows. In each prioritized round, inspect the relevant tables, foreign keys, constraints, indexes, views, stored procedures, functions, triggers, and temporal or history structures. Trace readers, writers, and ownership to evidence before documenting them. Compare observed schema and definitions with ORM models, migrations, and queries. Record verified behavior, confirmed intent, and discrepancies distinctly. Carry open decisions into the existing five-question rounds and continuation notes.

## Grill Reqs

Start with the existing database documentation and recheck only the story's dependencies through MCP. Verify relevant integrity rules, cardinality, soft deletion, transaction boundaries, and indexes against the schema and application code. Treat performance as unverified unless supported by appropriate runtime evidence. Update the page that owns the information and link to it from the story or flow. Reuse the existing database map.
