# 703. Kth Largest Element in a Stream

## 题目

给定一个数组和整数K。设计并实现一个类`KthLargest`，其构造函数接受数组和k作为参数，并可通过调用`add()`方法向里面添加元素并返回当前数组中第k大的元素值。

>Design a class to find the kth largest element in a stream. Note that it is the kth largest element in the sorted order, not the kth distinct element.
>
>Your `KthLargest` class will have a constructor which accepts an integer k and an integer array nums, which contains initial elements from the stream. For each call to the method KthLargest.add, return the element representing the kth largest element in the stream.
>
>Example:
>
>>```java
>>int k = 3;
>>int[] arr = [4,5,8,2];
>>KthLargest kthLargest = new KthLargest(3, arr);
>>kthLargest.add(3);   // returns 4
>>kthLargest.add(5);   // returns 5
>>kthLargest.add(10);  // returns 5
>>kthLargest.add(9);   // returns 8
>>kthLargest.add(4);   // returns 8
>>```
>
>**Note:**
>You may assume that `nums`' length `≥ k-1` and `k ≥ 1`.

## 解法

使用了`java.util`中的优先级队列`PriorityQueue`，队列中的元素是有序的，元素值最小的总是在队头。这样我们可以new一个容量为k的优先级队列，则队头就是我们需要返回的元素。

```java
    private int k;
    private PriorityQueue<Integer> q;
    public KthLargest(int k, int[] nums) {
        this.k = k;
        q = new PriorityQueue<>(k);
        for (int num : nums) {
            q.add(num);
            if (q.size() > k) q.poll();
        }
    }

    public int add(int val) {
        q.add(val);
        if (q.size() > k) q.poll();
        return q.peek();
    }
```

这题有一个`heap`的tag。所以Submission里，击败了99%的样例代码是自己手写一个堆。

```java
private int[] heap;
  private int size = 0;

  public KthLargest(int k, int[] nums) {
    heap = new int[k];
    for (int num : nums) {
      addAnItem(num);
    }
  }

  private void addAnItem(int item) {
    // add to end of the array until array is full and heapifyUp
    if (size < heap.length) {
      heap[size++] = item;
      heapifyUp();
    } else {
      // add to the top only if less than the least and heapifyDown
      if (item < heap[0]) return;
      heap[0] = item;
      heapifyDown();
    }
  }

  public int add(int val) {
    addAnItem(val);
    return heap[0];
  }

  private void swap(int parentNodeIndex, int i) {
    int temp = heap[i];
    heap[i] = heap[parentNodeIndex];
    heap[parentNodeIndex] = temp;
  }

  private void heapifyUp() {
    int indexToStartWith = size - 1;
    while(indexToStartWith > 0) {
      int parentIndex = (indexToStartWith - 1) / 2; // best way to find parent
      if (heap[indexToStartWith] < heap[parentIndex]) {
        swap(indexToStartWith, parentIndex);
        indexToStartWith = parentIndex;
      } else {
        break;
      }
    }
  }

  private void heapifyDown() {
    if (size == 1) return;
    int largest = 0;
    int startIndex = 0;
    while(startIndex < size ) {
      int leftChildIndex = 2*startIndex + 1;
      int rightChildIndex = 2*startIndex + 2;
      if (leftChildIndex < size && heap[largest] > heap[leftChildIndex]) {
        largest = leftChildIndex;
      }
      if (rightChildIndex < size && heap[largest] > heap[rightChildIndex]) {
        largest = rightChildIndex;
      }
      if (startIndex != largest) {
        swap(largest, startIndex);
        startIndex = largest;
      } else {
        break;
      }
    }
  }
```
