# Installing Neo4j on Arch Linux (Community Edition & Graph View)

## 1. Choose the Correct Package

On Arch Linux, for most users, **neo4j-community** is recommended.  
- It is open-source, reliable, and provides the Neo4j Browser web interface with graph visualization.
- **neo4j-desktop** may be available but is mainly for Windows/Mac and less stable on Linux.

**Install neo4j-community (recommended):**
```bash
paru -S neo4j-community
# or, if using yay:
yay -S neo4j-community
```
_If you specifically want the desktop GUI app and are comfortable troubleshooting, you may try `neo4j-desktop`, but most users should use `neo4j-community`._

---

## 2. Enable and Start Neo4j Service

```bash
sudo systemctl enable neo4j
sudo systemctl start neo4j
```

Check status:
```bash
systemctl status neo4j
```

---

## 3. Access the Neo4j Browser & Graph View

Neo4j runs a web interface by default at:  
[http://localhost:7474](http://localhost:7474)

- **Default username:** `neo4j`
- **Default password:** `neo4j` (you will be prompted to change this on first login)
- **Graph view:** Available in the Neo4j Browser web interface after logging in.

You can also use the CLI tool `cypher-shell`:
```bash
cypher-shell -u neo4j -p <yourpassword>
```
If you need to set a new password after installation, follow the prompt in the browser or use:
```bash
neo4j-admin set-initial-password <newpassword>
```

---

## 4. Example Cypher Commands

Your SQL schema and data, translated into Cypher (Neo4j query language):

```cypher
// Create asset types as nodes
CREATE (pipeType:AssetType {type_name: 'Pipe'});
CREATE (roadType:AssetType {type_name: 'Road'});
CREATE (lightType:AssetType {type_name: 'Streetlight'});

// Create assets
CREATE (pipe:Asset {name: 'Main St Water Pipe', location: 'Main St & 2nd Ave'});
CREATE (road:Asset {name: 'Highway 1', location: 'Highway 1, Section B'});
CREATE (light:Asset {name: 'Corner Streetlight', location: 'Corner of Main St & 3rd Ave'});

// Relate assets to their types
MATCH (pipe:Asset {name: 'Main St Water Pipe'}), (pipeType:AssetType {type_name: 'Pipe'})
CREATE (pipe)-[:IS_TYPE]->(pipeType);

MATCH (road:Asset {name: 'Highway 1'}), (roadType:AssetType {type_name: 'Road'})
CREATE (road)-[:IS_TYPE]->(roadType);

MATCH (light:Asset {name: 'Corner Streetlight'}), (lightType:AssetType {type_name: 'Streetlight'})
CREATE (light)-[:IS_TYPE]->(lightType);

// Create maintenance requests
CREATE (mr1:MaintenanceRequest {description: 'Burst water pipe causing flooding', reported_at: datetime('2025-09-29T08:30:00'), status: 'Open'});
CREATE (mr2:MaintenanceRequest {description: 'Large pothole forming', reported_at: datetime('2025-09-28T10:00:00'), status: 'In Progress'});
CREATE (mr3:MaintenanceRequest {description: 'Streetlight out', reported_at: datetime('2025-09-27T22:00:00'), status: 'Closed'});

// Relate maintenance requests to assets
MATCH (mr1:MaintenanceRequest {description: 'Burst water pipe causing flooding'}), (pipe:Asset {name: 'Main St Water Pipe'})
CREATE (mr1)-[:FOR_ASSET]->(pipe);

MATCH (mr2:MaintenanceRequest {description: 'Large pothole forming'}), (road:Asset {name: 'Highway 1'})
CREATE (mr2)-[:FOR_ASSET]->(road);

MATCH (mr3:MaintenanceRequest {description: 'Streetlight out'}), (light:Asset {name: 'Corner Streetlight'})
CREATE (mr3)-[:FOR_ASSET]->(light);
```

---

## 5. Testing

- Paste these commands into the Neo4j Browser query bar (at http://localhost:7474), or run them via `cypher-shell`.
- To see all your nodes and relationships as a graph:
  ```cypher
  MATCH (n) RETURN n;
  ```
- The Neo4j Browser graph view will visually display the nodes and relationships.

---

## Summary Table

| MySQL/MariaDB Concept        | Neo4j Equivalent                  |
|-----------------------------|-----------------------------------|
| Database/table/row          | Graph/node                        |
| Foreign key                 | Relationship (edge)               |
| SQL                         | Cypher                            |

---

## Troubleshooting & Notes

- If you can’t connect to [http://localhost:7474](http://localhost:7474), check that the service is running with `systemctl status neo4j`.
- Use `neo4j-community` for best compatibility and support on Linux.
- For advanced users: You can try `neo4j-desktop` for a GUI manager, but it’s less commonly used and may require extra setup.

