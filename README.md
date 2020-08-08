# Swift Coding Interview tips:

- Use guard where necessary to “force stop/return” the function 
- Use recursion where necessary
- Try avoiding algorithm with O(n^2)
- Try to add empty, out of bounds or negative input edge cases in the algorithm

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

### Hashable: (not clear yet)
Use it when keys need to be unique

### Dictionary:
```
Var dict : [Int: String]
Var dict = Dictionary<Int, string>()

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
Let arr = [“ABC”, “DEF”, “GHI”]
let flatMapped = arr.flatMap{$0}
```
## For loop:
```
for value in values {
  print(value)
}

for i in 0...values.count-1 {
  print(values[i])
}
```
