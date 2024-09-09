# ERP System Using Neo4j and Python

This project demonstrates a basic **Enterprise Resource Planning (ERP)** system using a **graph database (Neo4j)** in Python. The ERP system models entities like Suppliers, Customers, and Products, and their relationships using the graph data model, allowing for efficient querying and management of complex business relationships.

## Features

- **Supplier Management**: Add, retrieve, and manage supplier information.
- **Product Management**: Add, retrieve, and manage product details.
- **Customer Management**: Add, retrieve, and manage customer information.
- **Relationship Management**:
  - Suppliers supplying products.
  - Customers purchasing products.
- **Query Support**: 
  - Retrieve products supplied by a particular supplier.
  - Retrieve products purchased by a specific customer.

## Prerequisites

Before you start, ensure you have the following:

- Python 3.x installed on your machine.
- **Neo4j** database installed and running locally or remotely. Download Neo4j from the [official site](https://neo4j.com/download/).
- `neo4j` Python driver installed: 

  Install the required packages using:
  ```bash
  pip install neo4j
  ```

## Getting Started

### 1. Neo4j Setup

Start Neo4j server either locally or in a cloud instance. Make sure it's running on the default `bolt` port (7687).

#### Sample Connection:

```plaintext
Bolt URL: bolt://localhost:7687
Username: neo4j
Password: password
```

### 2. Clone the Repository

```bash
git clone https://github.com/matt7salomon/Enterprise_Resource_Planning_Graph_Database
cd erp-neo4j
```

### 3. Modify Connection Details

In the `erp_neo4j.py` file, update the connection string, username, and password to match your Neo4j configuration:

```python
erp = ERPNeo4j("bolt://localhost:7687", "neo4j", "password")
```

### 4. Run the Program

To run the ERP system example:

```bash
python erp_neo4j.py
```

## Code Overview

The code is structured around a class `ERPNeo4j`, which contains methods to interact with the Neo4j database. Each method is responsible for creating or querying data about suppliers, customers, products, and their relationships.

### Core Methods:

- **add_supplier**: Add a new supplier node.
- **add_product**: Add a new product node.
- **add_customer**: Add a new customer node.
- **create_supply**: Create a relationship indicating which supplier supplies which product.
- **create_purchase**: Create a relationship indicating which customer purchased which product.
- **get_supplier_products**: Query the products supplied by a specific supplier.
- **get_customer_purchases**: Query the products purchased by a specific customer.

## Example Use Cases

- **Suppliers Supplying Products**:
  ```python
  erp.create_supply("SUP001", "PROD001")
  ```
  
- **Customers Purchasing Products**:
  ```python
  erp.create_purchase("CUST001", "PROD001")
  ```

- **Query Products Supplied by Supplier**:
  ```python
  erp.get_supplier_products("SUP001")
  ```

## Neo4j Query Explanation

The project uses Cypher, Neo4j's query language, to manage nodes and relationships. For example:
- To create a new supplier:
  ```cypher
  CREATE (s:Supplier {supplier_id: $supplier_id, name: $name, country: $country})
  RETURN s
  ```

- To create a supplier-product relationship:
  ```cypher
  MATCH (s:Supplier {supplier_id: $supplier_id}), (p:Product {product_id: $product_id})
  CREATE (s)-[:SUPPLIES]->(p)
  RETURN s, p
  ```

## Future Enhancements

- Add support for managing more entities like **orders**, **warehouses**, and **invoices**.
- Improve querying with more complex relationships and properties.
- Implement front-end integration for better user interaction.

## Dependencies

- **Python 3.x**
- **Neo4j** (Database)
- **Neo4j Python Driver** (`neo4j`)

Install dependencies using:
```bash
pip install neo4j
```

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Contributing

Contributions are welcome! Please feel free to submit a pull request.
