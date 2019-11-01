# 705. Design HashSet

## 题目

实现一个HashSet并实现`add(), contains(), remove()`方法，不许使用任何`built-in Hash table libraries`. 元素范围在`[0, 1000000]` 之间。

>Design a HashSet without using any built-in hash table libraries.
>
>To be specific, your design should include these functions:
>
> - `add(value)`: Insert a value into the HashSet.
> - `contains(value)` : Return whether the value exists in the HashSet or not.
> - `remove(value)`: Remove a value in the HashSet. If the value does not exist in the HashSet, do nothing.
>
>**Example:**
>
>>```java
>>MyHashSet hashSet = new MyHashSet();
>>hashSet.add(1);
>>hashSet.add(2);
>>hashSet.contains(1);    // returns true
>>hashSet.contains(3);    // returns false (not found)
>>hashSet.add(2);
>>hashSet.contains(2);    // returns true
>>hashSet.remove(2);
>>hashSet.contains(2);    // returns false (already removed)
>>```
>
>**Note:**
>
> - All values will be in the range of [0, 1000000].
> - The number of operations will be in the range of [1, 10000].
> - Please do not use the built-in HashSet library.

## 解法

简单粗暴地做了一个`boolean[1000001]`。使用空间仅打败了33.33%的提交，运行时间也比较慢。

```java
private boolean[] table;
    /** Initialize your data structure here. */
    public MyHashSet() {
        table = new boolean[1000001];
        Arrays.fill(table, false);
    }

    public void add(int key) {
        table[key] = true;
    }

    public void remove(int key) {
        if (contains(key))
            table[key] = false;
    }

    /** Returns true if this set contains the specified element */
    public boolean contains(int key) {
        return table[key];
    }
```

更好的方法是遇到较大Key时再给数组扩容。

```java
class MyHashSet {
    private boolean[] table;
    /** Initialize your data structure here. */
    public MyHashSet() {
        table = new boolean[100];
        Arrays.fill(table, false);
    }

    public void add(int key) {
        if (key >= table.length)
            table = Arrays.copyOf(table, key + 2);
        table[key] = true;
    }

    public void remove(int key) {
        if (contains(key)) table[key] = false;
    }

    /** Returns true if this set contains the specified element */
    public boolean contains(int key) {
        return (key >= table.length) ? false : table[key];
    }
}
```
