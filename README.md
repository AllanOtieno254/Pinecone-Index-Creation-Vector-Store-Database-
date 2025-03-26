# Pinecone Index Creation (Vector Store Database)

## Overview
This project demonstrates how to create an index in **Pinecone**, a vector database optimized for similarity search and machine learning applications. The notebook covers setting up a Pinecone client, creating an index, and managing vector data efficiently.

## Features
- **Pinecone Client Setup**: Install and initialize the Pinecone client.
- **Index Creation**: Define an index with a specified dimension, metric, and serverless configuration.
- **Index Management**: List, check status, and delete indexes.
- **Handling Errors**: Address common API exceptions like region restrictions and duplicate indexes.

## Requirements
Before running the notebook, ensure you have the following dependencies installed:

```bash
pip install pinecone-client
```

## Getting Started
### 1. Import Necessary Libraries
```python
from pinecone import Pinecone, ServerlessSpec
```

### 2. Initialize Pinecone Client
```python
pc = Pinecone(api_key="YOUR_PINECONE_API_KEY")
```
> **Note**: Replace `YOUR_PINECONE_API_KEY` with your actual Pinecone API key.

### 3. List Available Indexes
```python
print(pc.list_indexes())
```

### 4. Create a New Index
```python
pc.create_index(
    name="example-index",
    dimension=128,
    metric="euclidean",
    spec=ServerlessSpec(
        cloud="aws",
        region="us-east-1"
    )
)
```
> **Important**: Free-tier Pinecone accounts may be limited to specific regions (e.g., `us-east-1`).

### 5. Handle Index Creation Errors
#### a) Region Not Supported Error
If you receive an error about region restrictions, adjust your region to one supported by the free tier.

#### b) Index Already Exists Error
If the index already exists, you can delete it before re-creating it:
```python
pc.delete_index("example-index")
```

### 6. Delete an Index
```python
pc.delete_index("example-index")
```

## Common Issues & Solutions
| Error | Cause | Solution |
|--------|--------|------------|
| `INVALID_ARGUMENT` | Region not supported | Use a free-tier supported region (e.g., `us-east-1`). |
| `ALREADY_EXISTS` | Index name already taken | Delete the existing index or use a different name. |
| `AttributeError: delete_index is no longer a top-level attribute` | Incorrect deletion method | Use `pc.delete_index("index-name")` instead of `pinecone.delete_index("index-name")`. |

## File Structure
```
📂 Create_an_index_in_pinecone
│── 📝 Create_an_index_in_pinecone.ipynb  # Jupyter Notebook with implementation
│── 📄 README.md  # Project documentation
```

## Resources
- [Pinecone Documentation](https://docs.pinecone.io/)
- [Pinecone Free Tier Limits](https://www.pinecone.io/pricing/)

## Author
**Allan Otieno Akumu**

---
This README provides a detailed overview of the project, helping users understand and implement Pinecone vector search efficiently.
