# Heap

A heap is a tree data structure. Generally a heap is of two types, a min heap or a max heap. Heaps work along with complete binary trees.

Heaps are implemented using arrays not pointers like in traditionaly binary trees.

#### Some use cases 
* Priority Queues - a Heap can be used to implement a Priority Queue, a Heap ordered by highest priority for example, the node at the top would serve to be the highest prioirty. 
* Sorting and Graph algorithms.

## Review of types of Binary Trees 

![sketch of type of trees](https://user-images.githubusercontent.com/1819208/102018865-f48b4780-3d3d-11eb-99a5-a648873e4374.jpg)

## Objectives 

- [x] Understand the Heap Data Structure and its implementation. 
- [x] Know the formula to retrieve the given parent, left child or right child. 
- [x] Be able to retrieve the minimum value from a Heap. 
- [x] Be able to insert values in a Heap. 
- [x] Understand how we keep the _Heap Property_ satisfied using `shiftDown` or `shiftUp` Heap functions. 
- [x] Be able to remove the minimum element from a Heap. 
- [ ] Be able to create a Heap from a given array. 

[Heap Implementation](https://repl.it/@alexpaul/Heap#main.swift)

## Common functions 

* Get min 
* Remove min 
* Insert 
* Heapify 

## Formula for getting index position of any node 

| node | formula |
|:----:|:----:|
| parent | (index - 1) / 2 |
| left child |  (index * 2) + 1 |
| right child | (index * 2) + 2 |

## Implementation of a `MinHeap` to test out retrieving nodes using fomular above 

```swift 
/*
          2
       /    \
      8      21
     / \    /  \
    10  16  30   36
*/

struct Heap {
  // data structue to hold the nodes of the Heap is an array
  private var nodes = [2, 8, 21, 10, 16, 30, 36]//[Int]()
  
  // this Heap can be a min Heap or a max Heap so we will use a closure to determine Heap type
  private var orderCriteria: (Int, Int) -> Bool
  
  // initializer
  public init(sort: @escaping (Int, Int) -> (Bool)) {
    self.orderCriteria = sort
  }
  
  // get left child index using formula => index * 2 + 1
  public func leftChildIndex(_ index: Int) -> Int {
    return index * 2 + 1
  }
  
  // get right child index using formula => index * 2 + 2
  public func rightChildIndex(_ index: Int) -> Int {
    return index * 2 + 2
  }
  
  // get parent index using formula => (index - 1) / 2
  public func parentIndex(_ index: Int) -> Int {
    return (index - 1) / 2
  }
  
  // get left child
  public func leftChild(for index: Int) -> Int {
    return nodes[leftChildIndex(index)]
  }
  
  // get right child
  public func rightChild(for index: Int) -> Int {
    return nodes[rightChildIndex(index)]
  }
  
  // get parent
  public func parent(for index: Int) -> Int {
    return nodes[parentIndex(index)]
  }
}

/*
          2
       /    \
      8      21
     / \    /  \
    10  16  30   36
*/

let minHeap = Heap(sort: <) // min Heap

minHeap.leftChildIndex(0) // 1
minHeap.rightChildIndex(0) // 2

minHeap.parentIndex(6) // 2
```

## Retrieve the minimum from the `Heap`

```swift 
public func peek() -> Int? {
  return nodes.first
}
```

## Insert a value into the `Heap`

![sketch to insert into a heap](https://user-images.githubusercontent.com/1819208/102020380-e2fa6d80-3d46-11eb-8ea7-3097a3a1d512.jpg)

```swift 
// insert
public mutating func insert(_ item: Int) {
  nodes.append(item)
  shiftUp(nodes.count - 1)
}
``` 

## `shiftUp` function in order to swap nodes as needed when inserting and satisfying the `Heap Property`

```swift 
// shift up
public mutating func shiftUp(_ index: Int) {
  let child = nodes[index]
  var childIndex = index
  var parentIndex = self.parentIndex(index)
  // while the child is not the root and the child node is smaller than the parent, continue shifting up
  while childIndex > 0 && orderCriteria(child, nodes[parentIndex]) {
    nodes[childIndex] = nodes[parentIndex]
    childIndex = parentIndex
    parentIndex = self.parentIndex(childIndex)
  }
  // insert the new child
  nodes[childIndex] = child
}
```

## Remove the top value from a `Heap`

![sketch - remove top](https://user-images.githubusercontent.com/1819208/104138866-37f4c800-5375-11eb-971b-8ea30953c960.jpg)

```swift 
public mutating func removeTop() -> Int? {
  guard !nodes.isEmpty else { return nil }

  if nodes.count == 1 {
    return nodes.removeLast()
  }

  let value = nodes[0]

  nodes[0] = nodes.removeLast() 

  shiftDown(from: 0, to: nodes.count)

  return value
}
```

## `shiftDown` function needed to satisfy the `Heap property` when removing a node

```swift 
private mutating func shiftDown(from index: Int, to endIndex: Int) {
  let leftChildIndex = self.leftChildIndex(index)
  let rightChildIndex = self.rightChildIndex(index)

  var currentIndex = index 

  if leftChildIndex < endIndex && orderingCriteria(nodes[leftChildIndex], nodes[currentIndex] {
    currentIndex = leftChildIndex
  }

  if rightChildIndex < endIndex && orderingCriteria(nodes[rightChildIndex], nodes[currentIndex] {
    currentIndex = rightChildIndex
  }

  if currentIndex == index { // no swapping needed
    return 
  }

  nodes.swapAt(currentIndex, index)

  shiftDown(from: currentIndex, to: endIndex)

}
```

## Challenge 

> Languages like C++ have built-in PriorityQueues (Reminder: a Heap can be used as a PriorityQueue, minHeap or maxHeap as needed), for this LeetCode challenge use our Heap implementation to solve this challenge [Heap Implementation](https://repl.it/@alexpaul/Heap#main.swift).

Design a class to find the kth largest element in a stream. Note that it is the kth largest element in the sorted order, not the kth distinct element.

```swift 
struct Heap {
  // implementation from in class implementation https://repl.it/@alexpaul/Heap#main.swift
}

class KthLargest {
  // decalare an instance of the Heap data structure here 

  init(_ k: Int, _ nums: [Int]) {
    // code here
  }

  func add(_ val: Int) -> Int {
    // code here
  }
}

/**
 * Your KthLargest object will be instantiated and called as such:
 * let obj = KthLargest(k, nums)
 * let ret_1: Int = obj.add(val)
 */
```

[LeetCode - 703. Kth Largest Element in a Stream
](https://leetcode.com/problems/kth-largest-element-in-a-stream/)

[Solution using our built Heap](https://repl.it/@alexpaul/Kth-Largest-Element-in-a-Stream#main.swift)

## Resources 

1. [GeeksForGeeks - Heap Data Structure](https://www.geeksforgeeks.org/heap-data-structure/)
1. [Wikipedia - Heap Data Structure](https://en.wikipedia.org/wiki/Heap_(data_structure))
1. [RW - Heap](https://github.com/raywenderlich/swift-algorithm-club/blob/master/Heap/Heap.swift)
1. [Interview Cake - Heap Data Structure](https://www.interviewcake.com/concept/java/heap)
1. [Uses of Hepas](https://webdocs.cs.ualberta.ca/~holte/T26/heap-uses.html)
1. [Video - HackerRank](https://www.youtube.com/watch?v=t0Cq6tVNRBA)
1. [Swift.org - Where is a default PriorityQueue? - Adding more data structures to the stnadard library](https://forums.swift.org/t/adding-more-data-structures-to-the-standard-library/23651)
