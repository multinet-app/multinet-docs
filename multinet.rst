Using Multinet
==============

This chapter is all about how to make use of a running Multinet system. Along
the way, you will also learn how Multinet structures data into tables and
networks, collected in different workspaces, and how Multinet thinks of
multivariate data and multivariate networks.

Getting Started
---------------

To begin, you will need access to a running Multinet instance (either the
official instance hosted at https://multinet.app, or a local instance you have
built and run; see :ref:`quickstart` for help). We will follow some steps to
illustrate the basic mode of using the system.

**1. Create a Workspace**

Multinet structures all the data it hosts into *workspaces*. A workspace can
hold several tables of data, as well as several networks assembled from those
tables. Think of a workspace as a dedicated area for related data to be stored.

In this tutorial sequence we will be recreating the `Paul Revere dataset
<https://kieranhealy.org/blog/archives/2013/06/09/using-metadata-to-find-paul-revere/>`_
as a social network connecting the various Revolutionary War figures to the
social clubs they belonged to.

The first step for any session where you're modifying data, is to log in using
Google OAuth. Click the person icon next to the multinet logo and then click 
'Sign in with Google'. Follow the prompts until you're back on the multinet site.
Authenticating allows you to upload data into certain workspaces (this is based 
on your permissions level).

To create a workspace to hold the materials for this dataset, use the ``NEW
WORKSPACE`` button appearing near the top of the left sidebar. A dialog box will
appear asking for the name of the new workspace. Fill this in with ``boston``
and click on the ``CREATE WORKSPACE`` button. This will create the workspace and
activate it.

In the main panel, you should see two empty columns, headed by ``Networks`` and
``Tables`` respectively. These columns will track all of the data that comes to
live in this workspace.

**2. Upload Node Tables**

Multinet largely thinks of attribute data in tabular terms. That is, Multinet
can ingest data formatted as (among other thigns) CSV files, storing it as a
*table* of *rows*, each row containing the same types of attributes in the same
order. Every node table must have a special attribute called ``_key``, which
contains a value unique to that row within the table it is part of.

We will begin by uploading separate tables to account for the *people* and
*clubs* represented in this dataset. First, download :download:`members.csv
</files/members.csv>`; this file contains the names of several historical
figures important during the American Revolution, along with some attributes.
Next, click on the plus icon to the right of the ``Tables`` column to upload a
file and create a table. Specify the ``members.csv`` file, note that the system
autofills in the name of the table to create, and then click the ``CREATE``
button.

This network contains two *node types*---one to encode the people, and another
for the clubs they belong to. Multinet recognizes nodes encoded in different
tables as being of different node types, so download :download:`clubs.csv
</files/clubs.csv>` and upload it to a ``clubs`` table, using the same procedure
as above.

You should now see both a ``members`` and a ``clubs`` table listed. You can
click on each of these to see the rows of each table. Return to the workspace
view by clicking on boston in the top bar.

**3. Upload an Edge Table**

Next we want to specify the topology of this network---that is, the relationship
between clubs and members as specified by membership. We need a special table
that encodes these memberships, using special attributes ``_from`` and ``_to``.
These attributes will always refer to rows from other tables in the workspace,
using a *node ID*, which is formed by joining the name of the table and the key
of the row with a slash. For instance, the John Adams row has a key value of
``7``; its node ID is therefore ``members/7``.

You can think of the rows of such a table as a directed links connecting two of
the nodes from somewhere in the workspace. To see this in action, download
:download:`membership.csv </files/membership.csv>`, and upload it as a table.
Because this table has properly formatted ``_from`` and ``_to`` attributes,
Multinet recognizes it as an *edge table*. If you click on the newly uploaded
table, you can explore what the rows look like. Note that while edge tables can
also have other attributes, this one does not.

**4. Create a Network**

Creating a network in Multinet is a matter of specifying an edge table that
defines that network's topology and implicitly (via the ``_from`` and ``_to``
values of its edge table rows, the nodes involved as) its nodes as well. To
create the Paul Revere network, click on the plus icon to the right of the
Networks column. When the dialog box appears, click on the ``CREATE`` tab at the
top, then select the ``membership`` table from the dropdown. Note that Multinet
already knows which tables are edge tables, due to the presence of ``_from`` and
``_to`` attributes. Fill in the name of the network with ``boston``, and then
click on the ``CREATE NETWORK`` button. You should see the new network appear in
the Networks column.

If you click on the new network, you will be taken to the network view, which
aggregates various pieces of information about this network, and provides links
to visualization applications. Note that the main panel displays some
characeristic information such as the number of nodes and edges, and the drawer
at the bottom displays information about the node types comprising this network,
the edge table that provides the connectivity, and a paged view of the nodes
themselves, identified by their node IDs. Clicking on these items will bring you
to dedicated views providing specific information; you can return to the network
view using the browser back button.

**5. Visualize the Network**

Now that the Paul Revere network is known to Multinet, its component data is now
available via the Multinet API to be consumed by different analysis and
visualization applications. To demonstrate, we will launch an interactive
node-link diagram to see what this particular network looks like.

In the network view, note that the right-hand sidebar contains a list of
external applications it can open. Click on ``Nodelink`` to open the node-link
diagram in a new tab. This application works by sending REST requests for the
specified network to the Multinet API server (which is the same server that
provides the file-browser-like view of the data that we have been learning about
in the Multinet client). As data about the nodes and links arrives in this
application, it can construct an interactive visual model of the network as a
collection of physical nodes connected by physically springlike links. Play with
the network in this application and explore the various options available in the
control panel.
