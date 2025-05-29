# Java Collections and Core Utilities

---

## String, StringBuilder, StringBuffer

| Feature        | String                       | StringBuilder                  | StringBuffer                     |
|----------------|------------------------------|--------------------------------|----------------------------------|
| Mutability     | Immutable                    | Mutable                        | Mutable                          |
| Thread-Safety  | ❌ Not Thread-Safe           | ❌ Not Thread-Safe             | ✅ Thread-Safe                   |
| Performance    | Slow (new object on change)  | Fast (no sync overhead)        | Slower (synchronization overhead)|
| Use Case       | Constant strings             | Single-threaded modifications  | Multi-threaded modifications     |

**Common Examples:**
```java
str1.substring(0, a);                         // Substring from 0 to a (not inclusive)
String[] news = s.trim().split("\\s+");     // Split by whitespace
String numStr = Integer.toString(count);      // Cast int to string
for (char digit : numStr.toCharArray())       // Convert string to char array
char tmp = x.charAt(i); x.setCharAt(i,x.charAt(j)); x.setCharAt(j,tmp); // Swap
sb.deleteCharAt(sb.length() - 1);             // Delete last character (O(1))
String lower = s.toLowerCase();               // Lowercase conversion
```

---

## List Interface

```java
public interface List<E> extends Collection<E> {
    int size();
    boolean isEmpty();
    boolean contains(Object o);
    boolean add(E e);
    boolean remove(Object o);
    E get(int index);
    E set(int index, E element);
    void clear();
    List<E> subList(int fromIndex, int toIndex);
}
```

**Implementations:**
```java
List<String> arrayList = new ArrayList<>();
List<String> vector = new Vector<>();
List<String> linkedList = new LinkedList<>();
```

### ArrayList vs Vector

| Use When                          | ArrayList                         | Vector                            |
|-----------------------------------|-----------------------------------|-----------------------------------|
| Threading                         | Single-threaded                   | Multi-threaded                    |
| Speed                             | Faster (no sync)                  | Slower (sync overhead)            |
| Access                            | Fast random access                | Synchronized access               |

```java
List<Integer> arrayList = new ArrayList<>();
List<Integer> vector = new Vector<>();

Runnable task = () -> {
    for (int i = 0; i < 1000; i++) {
        arrayList.add(i); // Not Thread-Safe
        vector.add(i);    // Thread-Safe
    }
};
```

---

## Set Interface

- No duplicates allowed
- Unordered (no index access)

```java
Set<String> set = new HashSet<>();        // Fastest
Set<String> linked = new LinkedHashSet<>(); // Maintains insertion order
Set<String> sorted = new TreeSet<>();     // Sorted set
Set<Character> vowels = Set.of('a','e','i','o','u','A','E','I','O','U');
```

---

## Map Interface

```java
Map<String, Integer> map = new HashMap<>();
Map<Character, List<Integer>> map2 = new HashMap<>();
```

**Iterating:**
```java
for (String key : map.keySet()) {
    System.out.println("Key: " + key + ", Value: " + map.get(key));
}

for (Integer value : map.values()) {
    System.out.println("Value: " + value);
}

for (Map.Entry<String, Integer> entry : map.entrySet()) {
    System.out.println("Key: " + entry.getKey() + ", Value: " + entry.getValue());
}
```

---

## Stack (LIFO)

```java
Stack<String> stack = new Stack<>();
stack.push("a");
stack.pop();
stack.peek();
stack.isEmpty();
```

Use Deque for better performance if thread-safety isn't needed:
```java
Deque<String> stack = new ArrayDeque<>();
```

---

## Queue

```java
Queue<Integer> q = new ArrayDeque<>();
q.offer(10);   // Insert
q.peek();      // View front
q.poll();      // Remove front
```

---

## Heap / PriorityQueue

```java
PriorityQueue<Integer> minHeap = new PriorityQueue<>();
PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());

PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> Integer.compare(a[0], b[0]));
```

| Method     | Description                        |
|------------|------------------------------------|
| offer()    | Insert element                     |
| peek()     | View the top element               |
| poll()     | Remove and return the top element  |
| isEmpty()  | Check if empty                     |
| size()     | Number of elements                 |

---

## Pair Examples

```java
Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0])); // Sort by start
Arrays.sort(intervals, (a, b) -> Integer.compare(a[1], b[1])); // Sort by end

List<List<Integer>> result = new ArrayList<>();
result.add(Arrays.asList(nums1[i], nums2[j])); // Add pair to result

PriorityQueue<int[]> minHeap = new PriorityQueue<>((a, b) -> Integer.compare(a[0], b[0]));
```

---
