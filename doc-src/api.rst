Useful APIs
============

Add the import declaration to use `treelib` in your project:

    from treelib import Node, Tree

This module `treelib` mainly contains two data structures: `Node` and `Tree`.


treelib.Node
------------

The structure `Node` defines basic properties such as node identifier 
(unique ID in the environment of a tree), node tag (readable name for human), 
parent node, children nodes etc., and some public operations on a node. 
(e.g., `a` in the description below):

    # To create a new node object.
    a = Node([tag[, identifier[, expanded]]])
    
    # To get or set the ID of the node
    a.identifier [=nid]
    
    # To get or set the ID of a's parent node
    a.bpointer [=value]
    a.update_bpointer(nid) # for set only
    
    # As a getting operator, ID list of a's SON nodes is obtained.
    # As a setting operator, the value can be list, set, or dict.
    # For list or set, it is converted to a list type by the packeage;
    # For dict, the keys are treated as the node IDs
    a.fpointer [=value]

    # Update the children list with different modes
    a.update_fpointer(identifier, mode=[Node.ADD, Node.DELETE, Node.INSERT])

    # Check if it's a leaf node
    a.is_leaf()



treelib.Tree
------------

The class `Tree` defines the tree-like structure based on the node structure.
Public methods are also available to make operations on the tree, e.g. a Tree object `t`:

    # Create a new object of tree structure
    t = Tree()
    
    # Get or set the ID of the root
    t.root [=nid]

    # Get the number of nodes in this tree
    t.size()

    # Check if the tree contains given node
    t.contains(nid)

    # Obtain node's parent (Node instance)
    # Return None if the parent is None or does not exist in the tree
    t.parent(nid)
    
    # Get the list of all the nodes randomly belonging to this tree
    t.all_nodes()

    # Get depth of the tree
    t.depth()

    # Get leaves of give root
    t.leaves([nid])

    # Add a new node object to the tree and make the parent as the root by default
    t.add_node(node[,parent])
    
    # Create a new node and add it to this tree
    t.create_node(tag[,identifier[,parent]])
    
    # Traverse the tree nodes with different modes; NOTE:
    # `nid` refers to the expanding point to start;
    # `mode` refers to the search mode (Tree.DEPTH, Tree.WIDTH);
    # `filter` refers to the function of one varible to act on the **node object**;
    # `key`, `reverse` are present to sort **node objects** in the same level.
    t.expand_tree([nid[,mode[,filter[,key[,reverse]]]]]]) 
    
    # Get the object of the node with ID of nid
    # An alternative way is using '[]' operation on the tree.
    # But small difference exists between them:
    # the get_node() will return None if nid is absent, whereas '[]' will raise KeyError.
    t.get_node(nid)
    
    # Get the children (only sons) list of the node with ID == nid.
    t.is_branch(nid)

    # Get all the siblings of given nid.
    t.siblings(nid)
    
    # Move node (source) from its parent to another parent (destination).
    t.move_node(source, destination)
    
    # Paste a new tree to an existing tree, with `nid` becoming the parent of the root of this new tree.
    t.paste(nid, new_tree) 
    
    # Remove a node and free the memory along with its successors.
    t.remove_node(nid)

    # Remove a node and link its children to its parent (root is not allowed)
    t.link_past_node(nid)
 
    # Search the tree from `nid` to the root along links reversedly
    # Note: `filter` refers to the function of one varible to act on the **node object**.
    t.rsearch(nid[,filter]) 
    
    # Print the tree structure in hierarchy style;
    # Note:
    # `nid` refers to the expanding point to start;
    # `level` refers to the node level in the tree (root as level 0);
    # `idhidden` refers to hiding the node ID when priting;
    # `filter` refers to the function of one varible to act on the **node object**;
    # `key`, `reverse` are present to sort **node objects** in the same level.
    t.show([nid[,level[,idhidden[,filter[,key[,reverse]]]]]]])

    # Return a soft copy of the subtree with `nid` being the root; The softness 
    # means all the nodes are shared between subtree and the original.
    t.subtree(nid)

    # Return a subtree with `nid` being the root, and
    # remove all nodes in the subtree from the original one
    t.remove_subtree(nid)

    # Save the tree into file for offline analysis.
    t.save2file(filename[,nid[,level[,idhidden[,filter[,key[,reverse]]]]]]])
    
    # To format the tree in a json format.
    t.to_json()
    