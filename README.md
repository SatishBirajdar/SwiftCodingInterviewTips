# Swift Coding Interview Revision/tips:

- Solve the problem on the paper first.
- Choose datastructure appropraitely.
- Try to add empty, out of bounds or negative input edge cases in the algorithm. Use guard where necessary to “force stop/return” the function. 
- Use recursion where necessary
- Try avoiding algorithm with O(n^2)

## Some Concepts:
### Enumerated:
```
let array = ["Apples", "Peaches", "Plums"]
for (index, item) in array.enumerated() {
    print("Found \(item) at position \(index)")
}
```

### Generic Types:
```
Struct Pair<T1, T2>{
	var first: T1
	var second: T2
}
Let floatFloatPair = Pair<Float, Float>(first: 0.3, second: 0.5)
Let stringStringPair = Pair(first: “first string”, second: “second string”)
```

### Generic Functions / Equatable:
```
Func isEqual<T: Equatable> (left: T, right: T) -> Bool {
	return left == right
}
Struct Contact: Equatable{
	let name: string
	let address: String
	init(name: String, address: String){
		self.name = name
		self.address = address
	}
	static func == (lhs: Contact, rhs: Contact) -> Bool {
		return lhs.name == rhs.name && lhs.address == rhs.address 
	}
}
Let oldCampus = Contact(name: “A”, address: “Address 1”)
Let newCampus = Contact(name: “B”, address: “Address 2”)
print(isEqual(left:oldCampus, right:newCampus))
```

### Complexity:
- Constant time = O(1)
- Linear time = O(n)
- Logarithmic = O(log n)
- Quadratic time = O(n^2)
- Triplatic time = O(n^3)

## Datastructure:
### Array:
Use array only when order and if items has to be of same type. And if the items need to be accessed repeatedly
```
Arr.insert(“new element”, at: 2)
Arr.remove(at:2)
```

### Set:
Use it, if the items need to be unique and unordered. Or when we need Union or Intersection

```
Set.insert(“new element”)
Set.remove(”element”)
Set.sorted()
Set1.union(set2)
Set1.intersect(set2)
Set1.subtracting(set2)

Set1 = [3,4,5]
Set2 = [2,3,4]
Let output = Set1.symmetricDifference(set2) = [2,5]
```

### Dictionary:
```
Var dict : [Int: String]
Var dict = Dictionary<Int, string>()
```


### Hashable: (not clear yet)
Use it when keys need to be unique
```
Var dict = Dictionary<AnyHasable, Any>().           === recommended for JSON

for(key, value) in dict {
	print(“\(key): \(value)”)
}

For value in dict.values {
	print(value)
}

dict[2]= “new value”.     -> update an existing value for an index ‘2’
dict[3] = nil   -> remove value for index ‘3’
```

### Stack:
```
struct Stack {
  fileprivate var array: [String] = []
  
  mutating func push(_ element: String) {
    array.append(element)
  }

  mutating func pop() -> String? {
    return array.popLast()
  }
}

var rwBookStack = Stack()
rwBookStack.push("3D Games by Tutorials")
rwBookStack.pop()

```

### Queue:
```
struct Queue<T> {
  private var elements: [T] = []

  mutating func enqueue(_ value: T) {
    elements.append(value)
  }

  mutating func dequeue() -> T? {
    guard !elements.isEmpty else {
      return nil
    }
    return elements.removeFirst()
  }

  var head: T? {
    return elements.first
  }

  var tail: T? {
    return elements.last
  }
}
var queue = Queue<String>()
queue.enqueue("Adam")
queue.enqueue("Julia")
queue.enqueue("Ben")

// we have 3 customers to serve, we're going to serve them in order of arrived
let serving = queue.dequeue() // { Ben -> Julia -> Adam }   removed Adam
let nextToServe = queue.head // { Ben -> Julia }
```
### Linked List:
```
class Node {
  var data: String
  var next: Node?
  init(data: String){
    self.data = data
  }
}

let node1 = Node(data: "A")
let node2 = Node(data: "B")
let node3 = Node(data: "C")
node1.next = node2
node2.next = node3
node3.next = nil

func parseNodes(fromNode: Node?){
  guard let validNode = fromNode else {
    return
  }
  print(validNode.data)
  parseNodes(fromNode: validNode.next)
}

parseNodes(fromNode: node1)
```
### Tree (includes Root, Node, Leaf)
```
class Node {
  var value: String
  var children: [Node] = []
  weak var parent: Node?

  init(value: String) {
    self.value = value
  }

  func add(child: Node) {
    children.append(child)
    child.parent = self
  }
}
let beverages = Node(value: "beverages")

let hotBeverages = Node(value: "hot")
let coldBeverages = Node(value: "cold")

beverages.add(child: hotBeverages)
beverages.add(child: coldBeverages)
print(coldBeverages.parent?.value)      // "beverages"
```
### Binary Tree: {Left, Node, Right} -> where Left is smaller than Node and Right is greater than Node
```
class TreeNode<T> {
    
    var data: T
    var leftNode: TreeNode?
    var rightNode: TreeNode?
    
    init(data: T,
         leftNode: TreeNode? = nil,
         rightNode: TreeNode? = nil) {
        self.data = data
        self.leftNode = leftNode
        self.rightNode = rightNode
    }
}

class BinaryTree<T: Comparable & CustomStringConvertible> {
    
    private var rootNode: TreeNode<T>?
    
    func insert(element: T) {
        let node = TreeNode(data: element)
        if let rootNode = self.rootNode {
            self.insert(rootNode, node)
        } else {
            self.rootNode = node
        }
    }
    
    // RECURSIVE FUNCTION
    private func insert(_ rootNode: TreeNode<T>, _ node: TreeNode<T>) {
        if rootNode.data > node.data {
            if let leftNode = rootNode.leftNode {
                self.insert(leftNode, node)
            } else {
                rootNode.leftNode = node
            }
        } else {
            if let rightNode = rootNode.rightNode {
                self.insert(rightNode, node)
            } else {
                rootNode.rightNode = node
            }
        }
    }
}

extension BinaryTree {

   func traverse() {
       print("\nPRE-ORDER TRAVERSE")
       self.preorder(self.rootNode)
       print("\n\nIN-ORDER TRAVERSE")
       self.inorder(self.rootNode)
       print("\n\nPOST-ORDER TRAVERSE")
       self.postorder(self.rootNode)
       print("\n")
   }
  
  // LNR : LEFT NODE RIGHT
  private func inorder(_ node: TreeNode<T>?) {
      guard let _ = node else { return }
      self.inorder(node?.leftNode)
      print("\(node!.data)", terminator: " ")
      self.inorder(node?.rightNode)
  }
  
  // NLR : NODE LEFT RIGHT
  private func preorder(_ node: TreeNode<T>?) {
      guard let _ = node else { return }
      print("\(node!.data)", terminator: " ")
      self.preorder(node?.leftNode)
      self.preorder(node?.rightNode)
  }
  
  // LRN :  LEFT RIGHT NODE
  private func postorder(_ node: TreeNode<T>?) {
      guard let _ = node else { return }
      self.postorder(node?.leftNode)
      self.postorder(node?.rightNode)
      print("\(node!.data)", terminator: " ")
  }
}

let tree = BinaryTree<String>()

tree.insert(element: "F")
tree.insert(element: "G")
tree.insert(element: "H")
tree.insert(element: "D")
tree.insert(element: "E")
tree.insert(element: "I")
tree.insert(element: "J")
tree.insert(element: "A")
tree.insert(element: "B")
tree.insert(element: "C")

tree.traverse()

/*
 Output:
 PRE-ORDER TRAVERSE
 F D A B C E G H I J

 IN-ORDER TRAVERSE
 A B C D E F G H I J

 POST-ORDER TRAVERSE
 C B A E D J I H G F
 
 */

```

### Binary Search Tree:
For above algorithm, add following code:
```
extension BinaryTree {
    
    func search(element: T) {
        self.search(self.rootNode, element)
    }
    
    private func search(_ rootNode: TreeNode<T>?, _ element: T) {
        
        guard let rootNode = rootNode else {
            print("INVALID NODE : \(element)")
            return
        }
        
        print("ROOT NODE \(rootNode.data)")
        if element > rootNode.data {
            self.search(rootNode.rightNode, element)
        } else if element < rootNode.data {
            self.search(rootNode.leftNode, element)
        } else {
           print("NODE FOUND : \(rootNode.data)")
        }
    }
}
```

## Swap:
```
Swap(&a, &b)
```

## Sorting
Selection Sort: (http://sorting.at/) Select the smaller forward item in the array and swap with the current item. With 2 for loops

### Insertion Sort: (also is lil time consuming) (Fastest sort for smaller array)
Items are sorted while inserting item from unsorted array to sorted array.

### Bubble Sort: 
Smaller item comes to the top, where the comparison happens between two consecutive numbers. Needs 2 for loops.

### Merge Sort: (2nd best)
Split the array in 2
Split the subarray, till you get single item array
Merge single items while sorting 2 items at a time. Complex : n(Log n)

### Quick Sort: (Fastest sort for bigger array)
PivotIndex = n/2
Split the array in 3 groups (<, = , >) of pivot item, quicksort each group and merge them
![Image of Quicksort snippet](https://github.com/SatishBirajdar/SwiftCodingInterviewTips/blob/master/import%20Foundation.png)

## Functional programming
### Reduce:
Reduce can be used on array or sets to calculate the sum of all items.
- Array: let reducedNumberSum = numbers.reduce(0) { $0 + $1 }
- Set: let reducedSet = numbers.reduce(0) { $0 + $1 }

### FlatMap:
```
let arr = ["ABC", "DEF", "GHI"]
let flatMapped = arr.flatMap{$0}
print(flatMapped)        // ["A", "B", "C", "D", "E", "F", "G", "H", "I"]
```
## Some basics and tricks
### For loop:
```
for value in values {
  print(value)
}

for i in 0...values.count-1 {
  print(values[i])
}
```
### Convert decimal to binary:
```
let num = 22
let str = String(num, radix: 2)
print(str)
```

### String to chars:
```
let characters = Array(string)    // or use flatMap
```
### Largest number of Array:
```
let largest = binaryGaps.reduce(Int.min, { max($0, $1) })
```
### Array is empty
```
binaryGaps.isEmpty  ==> checks if empty
```
