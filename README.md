# Technical Writing Assignment

For guidance on setting up and submitting this assignment, refer to the Marcy lab School Docs How-To guide for [Working with Short Response and Coding Assignments](https://marcylabschool.gitbook.io/marcy-lab-school-docs/fullstack-curriculum/how-tos/working-with-assignments#how-to-work-on-assignments).

## Prompt 1

Imagine you are giving a brief lesson on Recursion to a relatively new programmer. In your lesson make sure to include the following:

- A formal definition of recursion (feel free to quote an official source like MDN)
- An example in code.
- An explanation of the code example.
- An explanation of the kinds of functions that are best solved using recursion.

### Response 1
Recursion is the act of a function calling itself, receiving two inputs: a base case, which ends recursion, and a recursive case, which resumes recursion.

```js

const countdown = (num) {
    if (num <= 0) console.log(num);
    console.log(num);
    countdown(num - 1);
}

```

This function logs statements to the console, representing a countdown from `num`, a numerical argument. Before `num` is reached, `countdown` logs `num` to the console and recurses, this time with an argument of one lesser than the current value of `num`. As the invocations continue, `num` is logged to the console with each recursive case until the base case, where `num` is equal to or less than (in case the initial value of `num` is negative or non-whole) zero. Once the base case's condition is reached, the final value of `num` is logged and the recursion concludes.

Recursion should be used when problems can be broken down into smaller, similar subproblems. Recursion is a suitable alternative for problems which, when solved iteratively, are more complex and less readable. Using recursion can simplify problems and reduce code size at the cost of memory usage and performance. Although recursive functions can significantly greaten performance time due to overhead, they are a natural fit for problems such as most sorting algorithms and tree traversals.

## Prompt 2

Imagine you are giving a brief lesson on the Tree data structure to a relatively new programmer. In your lesson make sure to include the following:

- A formal definition of a Tree (feel free to quote an official source like MDN)
- Definitions for key terms like **root**, **leaf**, **depth**, and **height** as they relate to Trees
- An example in code.
- An explanation of the code example.

### Response 2

> A Tree is a hierarchical data structure consisting of nodes connected by edges, which are connection between two nodes in a tree representing the relationship between a parent and a child node. Each node contains a value and references to its child nodes. A tree follows these properties:
>
> 1. It has a single root node (the topmost node).
> 2. Each node, except the root, has exactly one parent.
> 3. Nodes may have zero or more children.
> 4. There are no cycles in the structure (it is an acyclic graph).
>
> - **Root**: The topmost node in the tree. It serves as the starting point and has no parent.
> - **Leaf**: A node that has no children (it is at the end of a branch).
> - **Depth**: The number of edges from the root node to a given node.
> - **Height**: The number of edges on the longest path from a node to a leaf. The height of the tree is the height of the root node.
>
> ```js
> class Tree {
>   constructor(value) {
>     this.value = value;
>     this.children = [];
>   }
>
>   addChild(childNode) {
>     this.children.push(childNode);
>   }
>
>   printTree(level = 0) {
>     console.log(" ".repeat(level) + this.value);
>     this.children.forEach((child) => child.printTreet(level + 1));
>   }
> }
>
> const root = new Tree("A");
> const nodeB = new Tree("B");
> const nodeC = new Tree("C");
> const nodeD = new Tree("D");
> const nodeE = new Tree("E");
>
> root.addChild(nodeB);
> root.addChild(nodeC);
> nodeB.addChild(nodeD);
> nodeB.addChild(nodeE);
>
> root.printTree();
> // Output:
> // A
> //   B
> //     D
> //     E
> //   C
> ```
>
> Explanation:
>
> 1. **`Tree` Class**: Each node has a `value` (data) and an array of `children`. The constructor initializes the node's value and an empty list for children.
> 2. **`addChild(childNode)` Method**: This method adds a child node to the current node.
> 3. **`printTree(level = 0)` Method**: This recursively prints the tree structure with indentation. The `repeat(level)` function controls the indentation to visually represent the tree hierarchy.
> 4. **Examples**: "A" is the root node. "B" and "C" are children of "A". "D" and "E" are children of "B". `printTree()` is called to display the structure.

## Prompt 3

Any iterative function can be written recursively. Provide an example of an iterative function and the same function written recursively. Then, explain the benefits and/or drawbacks of each approach.

### Response 3
```js
    const iter = arr => {
        const double = [];
        for (let i = 0; i < arr.length, i++) {
            double.push(arr[i] * 2);
        }
        return double;
    }

    const recur = (arr, double = [], i = 0) => {
        if (i >= arr.length) return double;
        double.push(arr[i] * 2);
        recur(arr, double, i + 1);
    }
```

While these functions have the same functionality, `iter` doubles each item in the argument `arr` iteratively while `recur` does so recursively. This function is suitable for the iterative approach: it is not complicated and only requires one for loop without addition conditional statements, assuming `arr` is composed entirely of values that can be doubled as these functions lack error handling. Although `iter` uses more lines than `recur`, it is straightforward and easy to understand even without the recursive approach. Although `recur` is a shorter function, it uses extra space: `double` and `i` are extra parameters with initialized values. As the function is simple, recursion does not provide any significant benefit as the stacked invocations increase performance time and memory.

## Prompt 4

Depth-first-search is an algorithm of traversing through a tree that explores as far as possible along a single branch before backtracking and exploring other branches. The three approaches for depth-first-search are "inorder", "preorder", and "postorder".

Using this tree as an example, explain the differences between these three approaches, providing implementations of each (recursive or iterative, its up to you but one of them is definitely cleaner).

```
    A
   / \
  B   C
 / \   \
D   E   F
```

### Response 4

> 1. Preorder (Root -> Left -> Right)
>
> - Visit the root first. Traverse left subtree. Traverse right subtree.
> - Order: `A B D E C F`
>
> ```js
> // Recursive
> function preorder(node) {
>   if (!node) return;
>   console.log(node.value);
>   preorder(node.left);
>   preorder(node.right);
> }
> ```
>
> 2. Inorder (Left -> Root -> Right)
>
> - Traverse left subtree. Visit the root. Traverse right subtree.
> - Order: `D B E A C F`
>
> ```js
> // Recursive
> function inorder(node) {
>   if (!node) return;
>   inorder(node.left);
>   console.log(node.value);
>   inorder(node.right);
> }
> ```
>
> 3. Postorder (Left -> Right -> Root)
>
> - Traverse left subtree. Traverse right subtree. Visit the root.
> - Order: `D E B F C A`
>
> ```js
> // Recursive
> function postorder(node) {
>   if (!node) return;
>   postorder(node.left);
>   postorder(node.right);
>   console.log(node.value);
> }
> ```
