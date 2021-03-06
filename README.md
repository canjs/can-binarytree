# can-binarytree

[![Build Status](https://travis-ci.org/canjs/can-binarytree.svg?branch=master)](https://travis-ci.org/canjs/can-binarytree)

**can-binarytree** extends the very well written JavaScript binary tree
implementations provided by [@vadimg](https://github.com/vadimg/js_bintrees)
and mixes in features of CanJS that make the data structures observable.

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [Install](#install)
- [Use](#use)
- [Data Structures](#data-structures)
- [API](#api)
  - [can.RBTreeList](#canrbtreelist)
    - [.attr()](#attr)
    - [.batchSet()](#batchset)
    - [.deleteAttr()](#deleteattr)
    - [.each()](#each)
    - [.eachNode()](#eachnode)
    - [.filter()](#filter)
    - [.indexOf()](#indexof)
    - [.indexOfNode()](#indexofnode)
    - [.map()](#map)
    - [.push()](#push)
    - [.removeAttr()](#removeattr)
    - [.replace()](#replace)
    - [.splice()](#splice)
    - [.unshift()](#unshift)
  - [can.RBTreeList.Node](#canrbtreelistnode)
  - [can.RBTree](#canrbtree)
  - [can.BinTree](#canbintree)
  - [can.Tree](#cantree)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->




## Install

Use npm to install `can-binarytree`:

```
npm install can-binarytree --save
```


## Use

Use `require` in Node/Browserify workflows to import `can-binarytree` like:

```js
require('can');
require('can-binarytree');
```

Use `define`, `require` or `import` in [StealJS](http://stealjs.com)
workflows to import `can-binarytree` like:

```js
import 'can';
import 'can-binarytree';
```

Once you've imported `can-binarytree` into your project, use it to
create observable binary tree data structures. The following example
`console.log`'s some metadata about each node that's added to a
`can.RBTreeList`:

```js
var tree = new can.RBTreeList();

tree.bind('add', function (ev, nodes) {
    console.log(node[0]);
})

tree.push('Hop'); // Node {id: 0, parent: null, data: "Hop", left: null, right: null...}
tree.push('Skip'); // Node {id: 2, parent: Node, data: "Skip", left: null, right: null...}
tree.push('Jump'); // Node {id: 4, parent: Node, data: "Jump", left: null, right: null...}
```


## Data Structures

- RBTreeList - A red-black tree implementation that meets the specifications of
  a can.List
- RBTree - A self-balancing binary tree that serves as a key-value store
- BinTree - A binary tree that is not balanced

Note: Currently the only data structure in the package that is observable is
the `can.RBTreeList`.


## API


### can.RBTreeList

A red-black tree that uses a numeric "index" as the "key" in the same way
a `can.List` or native Javascript array might, yet still performs insert and
remove operations in `O(log n)` time.

#### .attr()

`rbTreeList.attr() -> Array`

Returns an array of all the nodes' `data` property value in the
`can.RBTreeList`.

`rbTreeList.attr(index) -> Object`

Returns the `data` stored on the node in the `can.RBTreeList` at
the specified index.

`rbTreeList.attr(index, value) -> can.RBTreeList`

Creates a node, sets its `data` property, and inserts it into the
`can.RBTreeList` at the specified index. If a node already exists at
the specified index its `data` property is overwritten with the
specified value.

Returns the `can.RBTreeList`.

`rbTreeList.attr('length') -> can.RBTreeList`

Returns the `length` of the `can.RBTreeList`.


#### .batchSet()

`rbTreeList.batchSet(array, setFn) -> can.RBTreeList`

Populates an empty `can.RBTreeList` in `O(n)` time - compared
to `O(mlogn)` time - from an array of values.

The `setFn` is invoked for each insert with two arguments:
(insertIndex, createdNode)

Returns the `can.RBTreeList`.


#### .deleteAttr()

`rbTreeList.deleteAttr(index) -> Object`

Removes the node at the specified `index` without affecting the `length` of
the `RBTreeList` in the same way that the [delete operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/delete#Deleting_array_elements)
affects a Javascript array. The resulting `index` will not
be iterable with `.each()` until it is set or removed.


Returns the value of the node's `data` property that was removed.


#### .each()

`rbTreeList.each(callbackFn) -> can.RBTreeList`

Iterates over the nodes in the `can.RBTreeList` invoking `callbackFn` for each
node's `data` property. The `callbackFn` is invoked with two arguments:
(value, index). If the callback returns `false`, the iteration will stop.


#### .eachNode()

`rbTreeList.eachNode(callbackFn) -> can.RBTreeList`

Iterates over the nodes in the `can.RBTreeList` invoking `callbackFn` for each
node. The `callbackFn` is invoked with two arguments: (node, index).
If the callback returns `false`, the iteration will stop.


#### .filter()

`rbTreeList.filter(predicateFn, context) -> can.RBTreeList`

Iterates the elements in the `can.RBTreeList` returning a new
`can.RBTreeList` instance of all elements `prediateFn` returns truthy for.
The `predicateFn` is invoked in the specified `context` with the arguments:
(value, index, rbTreeList).

Returns a new `can.RBTreeList` instance.


#### .indexOf()

`rbTreeList.indexOf(value) -> Number`

Returns the first index at which the specified `value` can be found in
the `can.RBTreeList`, or -1 if it is not present.


#### .indexOfNode()

`rbTreeList.indexOfNode(node, useCache) -> Number`

Returns the first index at which the specified `node` can be found in
the `can.RBTreeList`, or -1 if it is not present.


#### .map()

`rbTreeList.map(mapFn, context) -> can.RBTreeList`

Creates an `can.RBTreeList` of values by running each element in the
`can.RBTreeList` through `mapFn`. The iteratee is invoked in the specified
`context` with three arguments: (value, index, rbTreeList).

Returns a new `can.RBTreeList` instance.


#### .push()

`rbTreeList.push(value) -> Number`

Inserts the specified value at the end of the `can.RBTreeList`.

Returns the `length` of the `can.RBTreeList`.


#### .removeAttr()

`rbTreeList.removeAttr(index) -> Object`

Removes the node at the specified `index` and decrements the `length` of
the `RBTreeList` by 1.

Returns the value of the node's `data` property that was removed.


#### .replace()

`rbTreeList.replace(newValues) -> can.RBTreeList`

Changes the content of a `can.RBTreeList` by removing all of the existing nodes
and inserting new nodes with the values supplied in the `newValues` array.

Returns the `can.RBTreeList`.


#### .splice()

`rbTreeList.splice(startIndex, removeCount, nodes...) -> Array`

Changes the content of a `can.RBTreeList` by removing existing nodes
and/or adding new nodes.

Returns an array of nodes removed from the `can.RBTreeList`.


#### .unshift()

`rbTreeList.unshift(value) -> Number`

Inserts the specified value at the beginning of the `can.RBTreeList`.

Returns the `length` of the `can.RBTreeList`.


### can.RBTreeList.Node

A reference to the `Node` constructor used internally by `can.RBTreeList` to
create nodes.


### can.RBTree

*Coming soon*

### can.BinTree

*Coming soon*

### can.Tree

*Coming soon*
