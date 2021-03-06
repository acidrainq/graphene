Getting started
===============

What is GraphQL?
----------------

For an introduction to GraphQL and an overview of its concepts, please refer
to `the official introduction <http://graphql.org/learn/>`_.

Let’s build a basic GraphQL schema from scratch.

Requirements
------------

-  Python (2.7, 3.4, 3.5, 3.6, pypy)
-  Graphene (2.0)

Project setup
-------------

.. code:: bash

    pip install "graphene>=2.0.dev"

Creating a basic Schema
-----------------------

A GraphQL schema describes your data model, and provides a GraphQL
server with an associated set of resolve methods that know how to fetch
data.

We are going to create a very simple schema, with a ``Query`` with only
one field: ``hello`` and an input name. And when we query it, it should return ``"Hello {name}"``.

.. code:: python

    import graphene

    class Query(graphene.ObjectType):
        hello = graphene.String(name=graphene.String(default_value="stranger"))

        def resolve_hello(self, info, name):
            return 'Hello ' + name

    schema = graphene.Schema(query=Query)

Querying
--------

Then we can start querying our schema:

.. code:: python

    result = schema.execute('{ hello }')
    print result.data['hello'] # "Hello stranger"

Congrats! You got your first graphene schema working!
