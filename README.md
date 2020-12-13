# Heap

A heap is a tree data structure. Generally a heap is of two types, a min heap or a max heap. Heaps work along with complete binary trees.

Heaps are implemented using arrays not pointers like in traditionaly binary trees.

## Review of types of Binary Trees 

![sketch of type of trees](https://user-images.githubusercontent.com/1819208/102018865-f48b4780-3d3d-11eb-99a5-a648873e4374.jpg)

## Objectives 

* Be able to insert values in a Heap. 
* Be able to retrieve the minimum value from a Heap. 
* Understand how to keep true to the heap property by using `shiftDown` or `shiftUp` heap functions. 

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
```

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

```swift 
func mutating func insert(_ item: Int) {
  elements.append(item)
  shiftUp(elements.count - 1)
}
``` 

## `shiftUp` function in order to swap nodes as needed when inserting

```swift 
func mutating func shiftUp(_ index: Int) {
  // code here
}
```

## `removeMin` function  

```swift 
``` 

## `shiftDown` function in `heapify` back in place after removing a node

```swift 
```

## Resources 

1. [GeeksForGeeks - Heap Data Structure](https://www.geeksforgeeks.org/heap-data-structure/)
1. [Wikipedia - Heap Data Structure](https://en.wikipedia.org/wiki/Heap_(data_structure))
1. [Interview Cake - Heap Data Structure](https://www.interviewcake.com/concept/java/heap)
