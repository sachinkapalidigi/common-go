### 1. **Stack**
- **Go Equivalent:** Go does not have a built-in stack, but you can use a slice to implement it.

```go
// Stack operations using a slice
stack := []int{}

// Push
stack = append(stack, 10)

// Pop
top := stack[len(stack)-1]
stack = stack[:len(stack)-1]

// Peek (Top element)
top := stack[len(stack)-1]
```

- **Generic Implementation:** 
```go
type Stack[T any] struct {
    values []T 
}

func (s *Stack[T]) Push(value T) {
    s.values = append(s.values, value)
}

func (s *Stack[T]) Pop() (T, bool) {
    n := len(s.values)
    if n == 0 {
        var zero T
        return zero, false
    }
    popped := s.values[n-1]
    s.values = s.values[:n-1]
    return popped, true
}

func (s *Stack[T]) Empty() bool {
    return len(s.values) == 0
}

func (s *Stack[T]) Peek() (T, bool) {
    n := len(s.values)
    if n == 0 {
        var zero T
        return zero, false
    }
    return s.values[n-1], true
}

func (s *Stack[T]) Size() int {
    return len(s.values)
}
```

### 2. **Queue**
- **Go Equivalent:** Like with stacks, queues can be implemented using slices.

```go
// Queue operations using a slice
queue := []int{}

// Enqueue
queue = append(queue, 10)

// Dequeue
front := queue[0]
queue = queue[1:]

// Peek (Front element)
front := queue[0]
```

### 3. **PriorityQueue**
- **Go Equivalent:** `container/heap` package can be used to implement a priority queue.

```go
import (
    "container/heap"
)

// Item is a custom type that implements heap.Interface
type Item struct {
    value    string
    priority int
    index    int
}

// PriorityQueue implementation using container/heap
type PriorityQueue []*Item

func (pq PriorityQueue) Len() int { return len(pq) }

func (pq PriorityQueue) Less(i, j int) bool {
    return pq[i].priority < pq[j].priority
}

func (pq PriorityQueue) Swap(i, j int) {
    pq[i], pq[j] = pq[j], pq[i]
    pq[i].index = i
    pq[j].index = j
}

func (pq *PriorityQueue) Push(x interface{}) {
    n := len(*pq)
    item := x.(*Item)
    item.index = n
    *pq = append(*pq, item)
}

func (pq *PriorityQueue) Pop() interface{} {
    old := *pq
    n := len(old)
    item := old[n-1]
    item.index = -1 // for safety
    *pq = old[0 : n-1]
    return item
}

// Example usage:
pq := make(PriorityQueue, 0)
heap.Init(&pq)
heap.Push(&pq, &Item{value: "task1", priority: 1})
top := heap.Pop(&pq).(*Item)
```

### 4. **HashMap**
- **Go Equivalent:** `map` (built-in)

```go
// HashMap operations using a map
hashMap := make(map[string]int)

// Insert
hashMap["key1"] = 10

// Get
value := hashMap["key1"]

// Delete
delete(hashMap, "key1")

// Check existence
_, exists := hashMap["key1"]
```

### 5. **HashSet**
- **Go Equivalent:** A `map[T]struct{}` can be used to implement a set.

```go
// HashSet operations using a map
hashSet := make(map[string]struct{})

// Insert
hashSet["value1"] = struct{}{}

// Check existence
_, exists := hashSet["value1"]

// Delete
delete(hashSet, "value1")
```

### 6. **TreeMap**
- **Go Equivalent:** `github.com/emirpasic/gods/maps/treemap` (Third-party package)

```go
import "github.com/emirpasic/gods/maps/treemap"

// TreeMap operations using gods TreeMap
treeMap := treemap.NewWithStringComparator()

// Insert
treeMap.Put("key1", 10)

// Get
value, exists := treeMap.Get("key1")

// Delete
treeMap.Remove("key1")

// Iteration
it := treeMap.Iterator()
for it.Next() {
    fmt.Printf("%s: %v\n", it.Key(), it.Value())
}
```

### 7. **TreeSet**
- **Go Equivalent:** `github.com/emirpasic/gods/sets/treeset` (Third-party package)

```go
import "github.com/emirpasic/gods/sets/treeset"

// TreeSet operations using gods TreeSet
treeSet := treeset.NewWithStringComparator()

// Insert
treeSet.Add("value1")

// Check existence
exists := treeSet.Contains("value1")

// Delete
treeSet.Remove("value1")

// Iteration
it := treeSet.Iterator()
for it.Next() {
    fmt.Println(it.Value())
}
```

### Summary

- **Stack & Queue:** Use slices for basic operations.
- **PriorityQueue:** Use `container/heap`.
- **HashMap:** Use the built-in `map`.
- **HashSet:** Use a `map[T]struct{}`.
- **TreeMap & TreeSet:** Use third-party packages like `gods` for balanced tree structures.
