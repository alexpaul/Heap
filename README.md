# Heap

A heap is a tree data structure. Generally a heap is of two types, a min heap or a max heap. Heaps work along with complete binary trees.

Heaps are implemented using arrays not pointers like in traditionaly binary trees.

## Review of types of Binary Trees 

![sketch of type of trees](https://user-images.githubusercontent.com/1819208/101498715-6e849080-393a-11eb-8978-92eae19e451d.jpg)

## Objectives 

* To create a heap from a given array, this is known as _Heapify_.
* Be able to retrieve the minimum value in constant time. 
* Understand what it is to shift up and shift down. 

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
struct MinHeap {
  private var elements = [2, 8, 21, 10, 16, 30, 36] //[Int]()
  
  public func getLeftChildIndex(_ parentIndex: Int) -> Int {
    return (parentIndex * 2) + 1
  }
  
  public func getRightChildIndex(_ parentIndex: Int) -> Int {
    return (parentIndex * 2) + 2
  }
  
  public func getParentIndex(_ childIndex: Int) -> Int {
    return (childIndex - 1) / 2
  }
  
  public func hasLeftChild(for index: Int) -> Bool {
    return getLeftChildIndex(index) < elements.count
  }
  
  public func hasRightChild(for index: Int) -> Bool {
    return getRightChildIndex(index) < elements.count
  }
  
  public func hasParent(_ childIndex: Int) -> Bool {
    return getParentIndex(childIndex) >= 0
  }
  
  public func leftChild(for index: Int) -> Int {
    return elements[getLeftChildIndex(index)]
  }
  
  public func rightChild(for index: Int) -> Int {
    return elements[getRightChildIndex(index)]
  }
  
  public func parent(for index: Int) -> Int {
    return elements[getParentIndex(index)]
  }
}


let heap = MinHeap()
heap.getLeftChildIndex(2) // 5
heap.getRightChildIndex(2) // 6

heap.leftChild(for: 2) // 30
heap.rightChild(for: 2) // 36

heap.getParentIndex(0) // -1
```

## Resources 

1. [GeeksForGeeks - Heap Data Structure](https://www.geeksforgeeks.org/heap-data-structure/)
1. [Wikipedia - Heap Data Structure](https://en.wikipedia.org/wiki/Heap_(data_structure))
1. [Interview Cake - Heap Data Structure](https://www.interviewcake.com/concept/java/heap)
