# Q1. Principles  
Choose any two tools to describe and explain the principles. Provide relevant screenshots and explanations to demonstrate your thorough understanding of the tools. 

---

## 1.1 MySQL

### 1.1.1 Principles

- Relational Model: Data is organised in tables (relations) made of rows and columns.
- Schema: Tables have a fixed schema (defined columns and data types).
- ACID Transactions: Ensures Atomicity, Consistency, Isolation, and Durability for reliability.
- SQL (Structured Query Language): Used for querying and managing data.
- Joins: Relationships between data are represented using foreign keys and JOIN operations.

---

### 1.1.2 Demonstration

#### 1.1.2.1 Designing the Schema

What to keep track of:
- Assets (e.g., pipes, roads, streetlights)
- Maintenance Requests (issues reported)
- Asset Types (to categorise assets)

SQL Code:
```sql
-- Create database
CREATE DATABASE CapeTownInfrastructure;
USE CapeTownInfrastructure;

-- Table for asset types
CREATE TABLE AssetTypes (
    id INT AUTO_INCREMENT PRIMARY KEY,
    type_name VARCHAR(100) NOT NULL
);

-- Table for assets
CREATE TABLE Assets (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    asset_type_id INT,
    location VARCHAR(255),
    FOREIGN KEY (asset_type_id) REFERENCES AssetTypes(id)
);

-- Table for maintenance requests
CREATE TABLE MaintenanceRequests (
    id INT AUTO_INCREMENT PRIMARY KEY,
    asset_id INT,
    description TEXT,
    reported_at DATETIME,
    status VARCHAR(50),
    FOREIGN KEY (asset_id) REFERENCES Assets(id)
);
```

Explanation:
- `AssetTypes` holds categories (e.g., Pipe, Road).
- `Assets` stores information about each asset, with a reference to its type.
- `MaintenanceRequests` are linked to specific assets via foreign keys.

---

#### 1.1.2.2 Inserting Data

SQL Code:
```sql
-- Asset types
INSERT INTO AssetTypes (type_name) VALUES ('Pipe'), ('Road'), ('Streetlight');

-- Assets
INSERT INTO Assets (name, asset_type_id, location)
VALUES
  ('Main St Water Pipe', 1, 'Main St & 2nd Ave'),
  ('Highway 1', 2, 'Highway 1, Section B'),
  ('Corner Streetlight', 3, 'Corner of Main St & 3rd Ave');

-- Maintenance Requests
INSERT INTO MaintenanceRequests (asset_id, description, reported_at, status)
VALUES
  (1, 'Burst water pipe causing flooding', '2025-09-29 08:30:00', 'Open'),
  (2, 'Large pothole forming', '2025-09-28 10:00:00', 'In Progress'),
  (3, 'Streetlight out', '2025-09-27 22:00:00', 'Closed');
```

---

#### 1.1.2.3 Querying Data
Find all open maintenance requests, and the asset/location involved:

SQL Code:
```sql
SELECT mr.id, a.name AS asset_name, at.type_name, a.location, mr.description, mr.status
FROM MaintenanceRequests mr
JOIN Assets a ON mr.asset_id = a.id
JOIN AssetTypes at ON a.asset_type_id = at.id
WHERE mr.status = 'Open';
```

Explanation:
- SQL JOINs relate maintenance requests to assets and asset types, demonstrating the relational model.

---

## 1.2 Neo4j

### 1.2.1 Principles

- Graph Model: Data is stored as nodes (entities) and relationships (edges).
- Schema-Optional: Flexible structure; nodes/relationships can have arbitrary properties.
- ACID Transactions: Ensures reliable operations.
- Cypher Query Language: Declarative language for querying and updating the graph.
- Direct Relationships: Relationships are first-class citisens, not inferred via JOINs.

---

### 1.2.2 Demonstration

#### 1.2.2.1 Creating the Graph

What to keep track of:
- Asset Types (`AssetType`)
- Assets (`Asset`)
- Maintenance Requests (`MaintenanceRequest`)
- Relationships between them

Cypher Code:
```cypher
// Create asset types as nodes
CREATE (pipeType:AssetType {type_name: 'Pipe'})
CREATE (roadType:AssetType {type_name: 'Road'})
CREATE (lightType:AssetType {type_name: 'Streetlight'})

// Create assets
CREATE (pipe:Asset {name: 'Main St Water Pipe', location: 'Main St & 2nd Ave'})
CREATE (road:Asset {name: 'Highway 1', location: 'Highway 1, Section B'})
CREATE (light:Asset {name: 'Corner Streetlight', location: 'Corner of Main St & 3rd Ave'})

// Relate assets to their types
CREATE (pipe)-[:IS_TYPE]->(pipeType)
CREATE (road)-[:IS_TYPE]->(roadType)
CREATE (light)-[:IS_TYPE]->(lightType)

// Create maintenance requests
CREATE (mr1:MaintenanceRequest {description: 'Burst water pipe causing flooding', reported_at: datetime('2025-09-29T08:30:00'), status: 'Open'})
CREATE (mr2:MaintenanceRequest {description: 'Large pothole forming', reported_at: datetime('2025-09-28T10:00:00'), status: 'In Progress'})
CREATE (mr3:MaintenanceRequest {description: 'Streetlight out', reported_at: datetime('2025-09-27T22:00:00'), status: 'Closed'})

// Relate maintenance requests to assets
CREATE (mr1)-[:FOR_ASSET]->(pipe)
CREATE (mr2)-[:FOR_ASSET]->(road)
CREATE (mr3)-[:FOR_ASSET]->(light)
```

Explanation:
- Each entity (asset type, asset, maintenance request) is a node.
- Relationships such as `IS_TYPE` and `FOR_ASSET` directly connect nodes, making traversals efficient and visualisations natural.

---

#### 1.2.2.2 Querying the Graph

Find all open requests with asset and type:

Cypher Code:
```cypher
MATCH (mr:MaintenanceRequest {status: 'Open'})-[:FOR_ASSET]->(a:Asset)-[:IS_TYPE]->(t:AssetType)
RETURN mr, a, t
```

Explanation:
- Pattern-matching traverses the graph to retrieve open requests and their associated assets and types, all in a single, intuitive query.

---

## 1.3 Key Differences

| Principle         | MySQL (Relational)                      | Neo4j (Graph)                                |
|-------------------|-----------------------------------------|----------------------------------------------|
| Data Model        | Tables (rows, columns)                  | Nodes and Relationships (edges)              |
| Schema            | Fixed, defined before use               | Flexible, schema-optional                    |
| Relationships     | Foreign Keys, JOINs                     | Direct, first-class relationships            |
| Query Language    | SQL                                     | Cypher                                       |
| Best For          | Structured, tabular data                | Highly connected, networked data             |

---

## 1.4 Conclusion

- MySQL is ideal for structured data and transactional workloads where relationships are simple and schema is stable.
- Neo4j excels when the domain is highly connected, and the relationships themselves are central to the data and queries, such as asset networks and maintenance tracking.

# Q2 features
 
Compare and contrast the features of any two tools. Why would one tool be chosen over the other? Use appropriate examples, screenshots and explanations.

---

## 2.1 MySQL vs. Neo4j: Feature Comparison

| Feature/Aspect  | MySQL (Relational)                        | Neo4j (Graph)                              |
| --------------- | ----------------------------------------- | ------------------------------------------ |
| Data Model      | Tables (rows and columns)                 | Nodes and Relationships (edges)            |
| Schema          | Fixed, pre-defined                        | Flexible, schema-optional                  |
| Relationships   | Foreign keys and JOINs                    | First-class, direct relationships          |
| Query Language  | SQL                                       | Cypher                                     |
| Performance     | Efficient for tabular, transactional data | Efficient for connected, networked data    |
| ACID Compliance | Yes                                       | Yes                                        |
| Visualisation   | Not native, requires external tools       | Native, intuitive graph visualisation      |
| Best for        | Structured, tabular data                  | Complex, highly connected data             |
| Scaling         | Scales well for large tables              | Scales well for deep/complex relationships |
| Learning Curve  | Well-known, widely used                   | Newer, graph concepts may be less familiar |

---

### 2.2 Why Choose MySQL?

- Best for: Applications with structured data, strong schema requirements, and simple or moderate relationships (e.g., accounting systems, inventory, traditional business apps).
- Strengths: Mature, widely supported, easy to find tooling and expertise, optimised for transactions and reporting.

---

### 2.3 Why Choose Neo4j?

- Best for: Applications with complex, interconnected data (e.g., social networks, recommendation engines, asset management with interdependencies).
- Strengths: Efficient for traversing multi-level relationships, dynamic schemas, and visualising connections.

---

## 2.4 Demonstration

### 2.4.1 Finding All Connected Maintenance Issues

#### Scenario:  
Suppose you want to find all maintenance requests that are related because they involve assets of the same type. For example, all open requests for "Pipes".

---

#### A. MySQL Solution

SQL Code:
```sql
-- Find all open maintenance requests for assets of the same type (e.g., 'Pipe')
SELECT mr.id, a.name AS asset_name, at.type_name, a.location, mr.description, mr.status
FROM MaintenanceRequests mr
JOIN Assets a ON mr.asset_id = a.id
JOIN AssetTypes at ON a.asset_type_id = at.id
WHERE mr.status = 'Open'
  AND at.type_name = 'Pipe';
```

Explanation:  
- Uses SQL JOINs to connect tables.
- Filtering is done on asset type and status.
- As relationships become more complex (e.g., finding all assets connected via multiple intermediate relationships), queries become more complex and performance may degrade.

---

#### B. Neo4j Solution

Cypher Code:
```cypher
// Find all open maintenance requests for assets of type 'Pipe'
MATCH (mr:MaintenanceRequest {status: 'Open'})-[:FOR_ASSET]->(a:Asset)-[:IS_TYPE]->(t:AssetType {type_name: 'Pipe'})
RETURN mr, a, t;
```

Explanation:  
- Pattern matching in Cypher naturally expresses traversals.
- As relationships become more complex (e.g., assets connected via multiple hops), the query remains concise and efficient.

---

### 2.4.2 Finding Connections Between Assets

#### A. MySQL: Finding Indirect Relationships
Suppose you want to find all other assets that share the same type as a given asset.

SQL Code:
```sql
SELECT a1.name AS asset_1, a2.name AS asset_2, at.type_name
FROM Assets a1
JOIN AssetTypes at ON a1.asset_type_id = at.id
JOIN Assets a2 ON a2.asset_type_id = at.id
WHERE a1.id <> a2.id
  AND a1.name = 'Main St Water Pipe';
```
Explanation:  
- Requires multiple JOINs and careful filtering.
- Indirect relationships (multi-hop) require increasingly complex queries.

---

#### B. Neo4j: Finding Indirect Relationships

Cypher Code:
```cypher
// Find all assets connected by the same type as 'Main St Water Pipe'
MATCH (a1:Asset {name: 'Main St Water Pipe'})-[:IS_TYPE]->(t:AssetType)<-[:IS_TYPE]-(a2:Asset)
WHERE a1 <> a2
RETURN a1, a2, t;
```
Explanation:  
- Relationship traversals are direct and intuitive.
- Cypher naturally expresses multi-hop and network queries.

---

## 2.5 Summary Table: When to Choose Each Tool

| Use Case / Requirement                 | MySQL                               | Neo4j                                    |
|----------------------------------------|-------------------------------------|------------------------------------------|
| Highly structured, tabular data        | ✓                                   |                                          |
| Strict schema required                 | ✓                                   |                                          |
| Simple relationships                   | ✓                                   |                                          |
| Complex, interconnected data           |                                     | ✓                                        |
| Multi-hop, recursive queries           |                                     | ✓                                        |
| Need for visualising relationships     |                                     | ✓                                        |
| Mature ecosystem and wide support      | ✓                                   |                                          |

---

## 2.6 Conclusion

- MySQL is ideal for projects requiring structured data, strong consistency, and simple relationships.
- Neo4j excels in scenarios with complex relationships, dynamic structures, and where traversing or visualising data connections is central to the application.

- Choose MySQL for traditional business data and reporting.  
- Choose Neo4j for modern, networked, or graph-centric domains like infrastructure network management, social relationships, or recommendation systems.

Therefore city maintenance involves complex interconnected data, which is Neo4j's core strength. Assets (like roads, pipes, traffic lights) are not just items in a table; they are highly dependent on location and each other. A pipe breaking might affect the road above it, which in turn affects traffic lights. Neo4j excels at multi-hop queries (e.g., "Find all maintenance crews, roads, and scheduled events that will be affected if this specific bridge component fails"), and its native visualisation makes managing and analysing the city's complex network and infrastructure dependencies intuitive. MySQL would struggle with the complexity and performance of these highly relational, deep-traversal queries.

This is why Neo4j would be chosen over mySql

# Q3 Neo4J Database

City of Cape Town Infrastructure Maintenance Neo4j demonstration

---

## 3.1 Example: Creating the Graph

### **3.1.1 Create Asset Types**
```cypher
CREATE (:AssetType {type_name: 'Pipe'});
CREATE (:AssetType {type_name: 'Road'});
CREATE (:AssetType {type_name: 'Streetlight'});
```

---

### **3.1.2 Create Locations**
```cypher
CREATE (:Location {name: 'Main St & 2nd Ave'});
CREATE (:Location {name: 'Highway 1, Section B'});
CREATE (:Location {name: 'Corner of Main St & 3rd Ave'});
```

---

### **3.1.3 Create Assets and Connect to Types and Locations**
```cypher
// Pipes
MATCH (t:AssetType {type_name: 'Pipe'}), (loc:Location {name: 'Main St & 2nd Ave'})
CREATE (a:Asset {name: 'Main St Water Pipe', install_date: date('2010-05-01')})
CREATE (a)-[:IS_TYPE]->(t)
CREATE (a)-[:LOCATED_AT]->(loc);

// Roads
MATCH (t:AssetType {type_name: 'Road'}), (loc:Location {name: 'Highway 1, Section B'})
CREATE (a:Asset {name: 'Highway 1', install_date: date('1990-01-01')})
CREATE (a)-[:IS_TYPE]->(t)
CREATE (a)-[:LOCATED_AT]->(loc);

// Streetlights
MATCH (t:AssetType {type_name: 'Streetlight'}), (loc:Location {name: 'Corner of Main St & 3rd Ave'})
CREATE (a:Asset {name: 'Corner Streetlight', install_date: date('2015-03-15')})
CREATE (a)-[:IS_TYPE]->(t)
CREATE (a)-[:LOCATED_AT]->(loc);
```

---

### **3.1.4 Create Maintenance Crews**
```cypher
CREATE (:MaintenanceCrew {name: 'Team Alpha'});
CREATE (:MaintenanceCrew {name: 'Team Beta'});
```

---

### **3.1.5 Create Maintenance Requests and Assign to Assets and Crews**
```cypher
// Burst water pipe (Open, assigned to Team Alpha)
MATCH (a:Asset {name: 'Main St Water Pipe'}), (crew:MaintenanceCrew {name: 'Team Alpha'})
CREATE (mr:MaintenanceRequest {
    description: 'Burst water pipe causing flooding',
    reported_at: datetime('2025-09-29T08:30:00'),
    status: 'Open'
})
CREATE (mr)-[:FOR_ASSET]->(a)
CREATE (mr)-[:ASSIGNED_TO]->(crew);

// Large pothole (In Progress, assigned to Team Beta)
MATCH (a:Asset {name: 'Highway 1'}), (crew:MaintenanceCrew {name: 'Team Beta'})
CREATE (mr:MaintenanceRequest {
    description: 'Large pothole forming',
    reported_at: datetime('2025-09-28T10:00:00'),
    status: 'In Progress'
})
CREATE (mr)-[:FOR_ASSET]->(a)
CREATE (mr)-[:ASSIGNED_TO]->(crew);

// Streetlight out (Closed, assigned to Team Alpha)
MATCH (a:Asset {name: 'Corner Streetlight'}), (crew:MaintenanceCrew {name: 'Team Alpha'})
CREATE (mr:MaintenanceRequest {
    description: 'Streetlight out',
    reported_at: datetime('2025-09-27T22:00:00'),
    status: 'Closed'
})
CREATE (mr)-[:FOR_ASSET]->(a)
CREATE (mr)-[:ASSIGNED_TO]->(crew);
```

---

## 3.2 Example Queries

### **3.2.1 Find All Open Maintenance Requests and Their Assets, Locations, Types, and Crews**
```cypher
MATCH (mr:MaintenanceRequest {status: 'Open'})-[:FOR_ASSET]->(a:Asset)-[:IS_TYPE]->(t:AssetType),
      (a)-[:LOCATED_AT]->(loc:Location),
      (mr)-[:ASSIGNED_TO]->(crew:MaintenanceCrew)
RETURN mr.description, mr.reported_at, a.name AS asset, t.type_name AS type, loc.name AS location, crew.name AS crew;
```

---

### **3.2.2 List All Maintenance Requests for Assets of Type 'Pipe'**
```cypher
MATCH (mr:MaintenanceRequest)-[:FOR_ASSET]->(a:Asset)-[:IS_TYPE]->(t:AssetType {type_name: 'Pipe'})
RETURN mr.description, mr.status, a.name;
```

---

### **3.2.3 Find All Maintenance Requests at a Specific Location**
```cypher
MATCH (loc:Location {name: 'Main St & 2nd Ave'})<-[:LOCATED_AT]-(a:Asset)<-[:FOR_ASSET]-(mr:MaintenanceRequest)
RETURN mr.description, mr.status, a.name;
```

---

### **3.2.4 Find Assets with Multiple Open Maintenance Requests**
```cypher
MATCH (a:Asset)<-[:FOR_ASSET]-(mr:MaintenanceRequest {status: 'Open'})
WITH a, COUNT(mr) AS open_requests
WHERE open_requests > 1
RETURN a.name, open_requests;
```

---

### **3.2.5 Visualise the Entire Network**
```cypher
MATCH (n)
OPTIONAL MATCH (n)-[r]->(m)
RETURN n, r, m;
```
*This will visualise all nodes and relationships in the Neo4j Browser UI.*

---

# Q4 Tool evaluation

This section discusses commonly used tools in database design, management, and visualisation, considering their application in the City of Cape Town infrastructure maintenance scenario. For each tool, we describe its purpose, limitations, and underlying assumptions.

- MongoDB
    
- MySQL Workbench
    
- Lucidchart / Draw.io
    
- Neo4j
    
- phpMyAdmin
    
- Microsoft Visio

---

## 1. MongoDB

**Purpose:**  
A NoSQL, document-oriented database that stores data in flexible, JSON-like documents.

**Limitations:**  
- **Joins:** No native support for complex JOIN operations like relational databases. Modeling relationships between assets, requests, and locations may require data duplication or manual referencing.
- **Transactions:** Historically limited transaction support; multi-document ACID transactions added only in later versions.
- **Schema Management:** Flexible schema can lead to inconsistent data if not carefully managed.
- **Aggregation Complexity:** Complex analytics may require elaborate aggregation pipelines, which can be harder to manage and optimise.

**Underlying Assumptions:**  
- Data is best represented as documents with varying structures.
- Relationships between entities are either simple or can be embedded, not deeply interconnected.

---

## 2. MySQL Workbench

**Purpose:**  
A graphical tool for MySQL database modeling, design, and administration.

**Limitations:**  
- **Database Specific:** Only supports MySQL/MariaDB, not suitable for other database types (e.g., NoSQL or graph).
- **Visualisation Scope:** ER diagrams are limited to relational models; cannot intuitively represent networks or multi-hop relationships.
- **Scalability:** Not designed for large or complex schema visualisations; diagrams can become unwieldy.

**Underlying Assumptions:**  
- The data fits a strictly relational model.
- Users are comfortable with MySQL and SQL.

---

## 3. Lucidchart / Draw.io

**Purpose:**  
Online diagramming tools for creating entity-relationship diagrams, flowcharts, and system designs.

**Limitations:**  
- **Static Nature:** Diagrams are not interactive or connected to live data; require manual updates if the underlying schema changes.
- **Complexity Management:** Large, complex systems can result in cluttered diagrams.
- **Database Integration:** No direct integration with databases for reverse engineering or live updates.

**Underlying Assumptions:**  
- Visual modeling is sufficient for understanding and designing systems.
- Manual upkeep of diagrams is manageable.

---

## 4. Neo4j

**Purpose:**  
A graph database for storing and querying interconnected data.

**Limitations:**  
- **Tabular Operations:** Not optimised for tabular reporting or aggregate-heavy operations.
- **Learning Curve:** Requires understanding of graph concepts and Cypher query language.
- **Tooling:** Fewer third-party tools and less mature ecosystem compared to relational databases.
- **Scaling Writes:** Large-scale write operations can be less performant than some NoSQL or sharded relational systems.

**Underlying Assumptions:**  
- Data is highly connected; relationships are as important as the data itself (e.g., assets, locations, and requests form a network).
- Traversals and pattern matching are common queries.

---

## 5. phpMyAdmin

**Purpose:**  
A web-based interface for managing MySQL databases.

**Limitations:**  
- **Database Specific:** Only for MySQL/MariaDB.
- **Visualisation:** ER diagrams and schema design features are basic compared to desktop tools.
- **Performance:** Not optimised for very large databases or complex operations.

**Underlying Assumptions:**  
- Administrative tasks are performed via a browser.
- Users are familiar with MySQL.

---

## 6. Microsoft Visio

**Purpose:**  
Desktop software for creating detailed diagrams, including ER diagrams and system architectures.

**Limitations:**  
- **Static Diagrams:** Manual updates needed if the schema changes.
- **Database Integration:** Reverse engineering is possible but not as seamless as dedicated database tools.
- **Collaboration:** Desktop-based, so real-time collaboration is not as strong as cloud-based tools.

**Underlying Assumptions:**  
- Visual representation suffices for planning and documentation.
- Manual synchronisation with actual database schema.

---

## 7. Summary Table: Suitability for City Maintenance Scenario

| Tool                  | Best Use                        | Limitations                                    | Assumptions                            |
|-----------------------|---------------------------------|------------------------------------------------|----------------------------------------|
| **MongoDB**           | Flexible, document data         | No native JOINs, schema drift                  | Data is semi-structured, relationships are simple |
| **MySQL Workbench**   | SQL schema design, ER diagrams  | MySQL-only, relational-only                    | Data is strictly relational            |
| **Lucidchart/Draw.io**| Visual modeling, diagrams       | Static, not data-driven                        | Manual update of diagrams              |
| **Neo4j**             | Complex relationships, graphs   | Not for tabular data, learning curve           | Data is highly interconnected          |
| **phpMyAdmin**        | Web MySQL admin                 | MySQL-only, basic visualisation                | Web-based admin, simple needs          |
| **Microsoft Visio**   | Detailed static diagrams        | Manual updates, desktop only                   | Visual planning/documentation          |

---

## 8. Conclusion

Each tool comes with assumptions about data structure, user expertise, and system requirements. The choice should be based on the complexity of relationships, need for live data integration, and the team's workflow. For city infrastructure maintenance, tools like Neo4j excel in handling interconnected data, while MySQL Workbench and Lucidchart are valuable for planning and communicating system structure.