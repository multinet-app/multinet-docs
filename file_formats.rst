.. _File formats:

File Formats
====================================

Multinet requires specific file formats for uploaded data. These file formats allow MultiNet to read the data and create the appropriate tables, and networks. 

Nodes
------------------------------------

We support CSV and JSON file formats for node tables. The required structure is described below.

**CSV**

For a CSV node file, there are no required fields, but there are some fields that are recommended. We recommend that you include an `_key` field that acts as a unique identifier for the row that we can reference from the links table. If it is not included, it will be automatically generated, but that is not guaranteed to be idempotent across uploads.

For example, a CSV file with the following structure would be valid:

.. code-block::

  _key,developer,language
  1,Jack,JavaScript
  2,Roni,Python
  3,Jake,TypeScript


**JSON**

For a JSON node file, there are no required fields, but there are some fields that are recommended. We recommend that you include an `_key` field that acts as a unique identifier for the row that we can reference from the links table. If it is not included, it will be automatically generated, but that is not guaranteed to be idempotent across uploads.

For example, a JSON file with the following structure would be valid:

.. code-block:: json

  [
    {
      "_key": "1",
      "developer": "Jack",
      "language": "JavaScript"
    },
    {
      "_key": "2",
      "developer": "Roni",
      "language": "Python"
    },
    {
      "_key": "3",
      "developer": "Jake",
      "language": "TypeScript"
    }
  ]

Edges
------------------------------------

We support CSV and JSON file formats for edge tables. The required structure is described below.

**CSV**

For a CSV edge file, there are two required fields: `_from` and `_to`. These fields are used to reference the nodes that are connected by the edge.

For example, a CSV file with the following structure would be valid:

.. code-block::

  _from,_to,edge_weight
  node_table_name/1,node_table_name/2,10
  node_table_name/2,node_table_name/3,20
  node_table_name/3,node_table_name/1,30

**JSON**

For a JSON edge file, there are two required fields: `_from` and `_to`. These fields are used to reference the nodes that are connected by the edge.

For example, a JSON file with the following structure would be valid:

.. code-block:: json

  [
      {
          "_from": "node_table_name/1",
          "_to": "node_table_name/2",
          "edge_weight": 10
      },
      {
          "_from": "node_table_name/2",
          "_to": "node_table_name/3",
          "edge_weight": 20
      },
      {
          "_from": "node_table_name/3",
          "_to": "node_table_name/1",
          "edge_weight": 30
      }
  ]

Networks
------------------------------------

We support JSON file format for networks. Uploading networks files requires that we define both the nodes and edges at once. The required structure is described below.

**JSON**

For a JSON network file, there are two required fields: `nodes` and `edges`. These fields are used to reference the nodes and edges that are connected by the network. Nodes must have either an `id` or `_key` field. Edges must have `_from` and `_to` or `source` and `target` fields.

For example, a JSON file with the following structure would be valid:

.. code-block:: json

  {
    "nodes": [
      {
        "_key": "1",
        "developer": "Jack",
        "language": "JavaScript"
      },
      {
        "_key": "2",
        "developer": "Roni",
        "language": "Python"
      },
      {
        "_key": "3",
        "developer": "Jake",
        "language": "TypeScript"
      }
    ],
    "edges": [
      {
        "_from": "node_table_name/1",
        "_to": "node_table_name/2",
        "edge_weight": 10
      },
      {
        "_from": "node_table_name/2",
        "_to": "node_table_name/3",
        "edge_weight": 20
      },
      {
        "_from": "node_table_name/3",
        "_to": "node_table_name/1",
        "edge_weight": 30
      }
    ]
  }

As another example, a JSON file with the following structure would also be valid:

.. code-block:: json

  {
    "nodes": [
      {
        "id": "1",
        "developer": "Jack",
        "language": "JavaScript"
      },
      {
        "id": "2",
        "developer": "Roni",
        "language": "Python"
      },
      {
        "id": "3",
        "developer": "Jake",
        "language": "TypeScript"
      }
    ],
    "edges": [
      {
        "source": "1",
        "target": "2",
        "edge_weight": 10
      },
      {
        "source": "2",
        "target": "3",
        "edge_weight": 20
      },
      {
        "source": "3",
        "target": "1",
        "edge_weight": 30
      }
    ]
  }

UpSet
------------------------------------

