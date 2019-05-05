## A brief guide to Java classes

#### Array
 - length

#### [Arrays](https://docs.oracle.com/javase/8/docs/api/java/util/Arrays.html)
```
int[] a;
Arrays.fill(a, 0);
```
```
static <T> List<T> asList(T... a)

static IntStream stream(int[] array)

static void	sort(short[] a)

static void	sort(short[] a, int fromIndex, int toIndex)

static <T> void	sort(T[] a, Comparator<? super T> c)

static <T> void	sort(T[] a, int fromIndex, int toIndex, Comparator<? super T> c)
```

#### [String](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html)

```
int length()

char charAt(int index)

char[] toCharArray()

int indexOf(int ch)

boolean isEmpty()

String substring(int beginIndex)

String substring(int beginIndex, int endIndex) //inclusive, exclusive

String replaceAll(String regex, String replacement)

boolean startsWith(String prefix)

boolean split(String regex)

String trim()

String toLowerCase()

String toUpperCase()

String valueOf(value) //overloaded
```

#### [StringBuilder](https://docs.oracle.com/javase/8/docs/api/java/lang/StringBuilder.html)
```
StringBuilder()

StringBuilder(String str)

StringBuilder append(char c)

StringBuilder append(CharSequence s)

char charAt(int index)

StringBuilder deleteCharAt(int index)

StringBuilder reverse()
```

#### [Iterable](https://docs.oracle.com/javase/8/docs/api/java/lang/Iterable.html) - interface

```
default void forEach(Consumer<? super T> action)

Iterator<T> iterator()

```

#### [Collection](https://docs.oracle.com/javase/8/docs/api/java/util/Collection.html) - interface
- --> Iterable

```
boolean add(E e)

boolean addAll(Collection<? extends E> c)

void clear()

boolean contains(Object o)

boolean containsAll(Collection<?> c)

boolean isEmpty()

boolean remove(Object o) // remove the first occurence of o

int size()

Object[] toArray()

<T> T[] toArray(T[] a)

```
#### [ArrayList](https://docs.oracle.com/javase/8/docs/api/java/util/ArrayList.html)
- --> AbstractList --> AbstractCollection
- implement Iterable<E>, Collection<E>, List<E>, RandomAccess, etc

```
ArrayList()

ArrayList(Collection<? extends E> c)

ArrayList(int initialCapacity)

E get(int index)

E set(int index, E element)

E remove(int index)

List<E> subList(int fromIndex, int toIndex) //[inclusive, exclusive)

int indexOf(Object o)

void add(int index, E element) // out of bound if index < 0 || index > size()

boolean addAll(Collection<? extends E> c)

void clear()

```
#### [Stack](https://docs.oracle.com/javase/8/docs/api/java/util/Stack.html)
```
boolean empty()

E peek() //throw EmptyStackException if empty

E pop()

E push(E item)

int search(Object o) // return 1 based position. never used before
```
#### [Queue](https://docs.oracle.com/javase/8/docs/api/java/util/Queue.html) - interface
```
/**
return true if success, throws IllegalStateException if no space is available
*/
boolean add(E e)

boolean offer(E e) //best offort, no exception throw

E remove() //throw exception if empty

E poll() // return null if empty

E peek() // return null if empty
```

#### [Deque](https://docs.oracle.com/javase/8/docs/api/java/util/Deque.html) - interface
- Superinterfaces: Iterable<E>, Queue<E>, Collection<E>

```
void add(E e) // addLast

void addFirst(E e) //throws exception if no space

void addLast(E e) //throw exception if no space

E getFirst() //throw exception if empty
 
E getLast() //throw exception if empty

boolean offerFirst(E e)

boolean offerLast(E e)

E pollFirst() //head or null

E pollLast() //tail or null

E removeFirst() //throw exception if empty

E removeLast() //throw exception if empty

E peekFirst() // head or null

E peekLast() // tail or null


E peek() // head or null

boolean offer(E e) //same as offerLast(e)

E poll() // pollFirst


E pop() // removeFirst

E push(E e) // addFirst(E e)


```
#### [LinkedList](https://docs.oracle.com/javase/8/docs/api/java/util/LinkedList.html)
implements: Iterable<E>, Collection<E>, Deque<E>, List<E>, Queue<E>

#### [PriorityQueue](https://docs.oracle.com/javase/8/docs/api/java/util/PriorityQueue.html)
implements: Iterable<E>, Collection<E>, Queue<E>

```
PriorityQueue()

PriorityQueue(Collection<? extends E> c)

PriorityQueue(Comparator<? super E> comparator) // often used

PriorityQueue(int initialCapacity) 

PriorityQueue(int initialCapacity, Comparator<? super E> comparator) //ofen used

PriorityQueue(SortedSet<? extends E> c)
```

#### [Map](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html) - interface

```
void clear()

boolean isEmpty()

int size()

boolean containsKey(Object key)

boolean containsValue(Object value)

Set<Map.Entry<K,V>> entrySet()

Set<K> keySet()

Collection<V> values()

V get(Object key)

V put(K key, V value) //return previous associated value (can be null)

default V putIfAbsent(K key, V value)

default V getOrDefault(Object key, V defaultValue)

V remove(Object key) //optional

default boolean remove(Object key, Object value)
```

#### [HashMap](https://docs.oracle.com/javase/8/docs/api/java/util/HashMap.html)

- implement: Map<K, V>

#### [LinkedHashMap](https://docs.oracle.com/javase/8/docs/api/java/util/LinkedHashMap.html)
- extends: HashMap
- implement: Map<K, V>
- Hash table and linked list implementation of the Map interface, with predictable iteration order.

```
/**
accessOrder: true for access-order, false for insertion-order
*/
LinkedHashMap(int initCap, float loadFactor, boolean accessOrder)

protected boolean removeEldestEntry(Map.Entry<K, V> eldest)
```
```
class LRUCache {
    
    private LinkedHashMap<Integer, Integer> mMap;
    private final int mCapacity;

    public LRUCache(int capacity) {
        mCapacity = capacity;
        mMap = new LinkedHashMap(capacity, 0.75f, true) {
            @Override
            protected boolean removeEldestEntry(Map.Entry entry) {
                return size() > mCapacity;
            }
        };
    }
    
    public int get(int key) {
        return mMap.get(key) == null ? -1 : mMap.get(key);
    }
    
    public void put(int key, int value) {
        mMap.put(key, value);
    }
}
```

#### [SortedMap](https://docs.oracle.com/javase/8/docs/api/java/util/SortedMap.html) - interface
- extends: Map

```
K firstKey()

K lastKey()
```

#### [NavigableMap](https://docs.oracle.com/javase/8/docs/api/java/util/NavigableMap.html) - interface
- extends: Map<K,V>, SortedMap<K, V>

```
K lowerKey(K key) // strict less than

K higherKey(K key) // strict larger than

K floorKey(K key) // greatest key less or equal to key

K ceilingKey(K key) 

Map.Entry<K, V> lowerEntry(K key)

Map.Entry<K, V> higherEntry(K key)

Map.Entry<K, V> floorEntry(K key)

Map.Entry<K, V> ceilingEntry(K key)

Map.Entry<K, V> pollFirstEntry()

Map.Entry<K, V> pollLastEntry()

NavigableSet<K> navigableKeySet()
```

#### [TreeMap](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)
	- implements: Map, NavigableMap, SortedMap
	- A Red-Black tree based NavigableMap implementation
```
TreeMap(Comparator<? super K> comparator)
```

#### [Set](https://docs.oracle.com/javase/8/docs/api/java/util/Set.html) - interface

- implement: Collection<E>, Iterable<E>

#### [HashSet](https://docs.oracle.com/javase/8/docs/api/java/util/HashSet.html)
- implement: Iterable<E>, Collection<E>, Set<E>
- backed by HashMap

#### [LinkedHashSet](https://docs.oracle.com/javase/8/docs/api/java/util/LinkedHashSet.html)
- implement: Iterable<E>, Collection<E>, Set<E>

- Hash table and linked list implementation of the Set interface, with predictable iteration order. 
- This implementation differs from HashSet in that it maintains a doubly-linked list running through all of its entries. 
- This linked list defines the iteration ordering, which is the order in which elements were inserted into the set (insertion-order). 
- Note that insertion order is not affected if an element is re-inserted into the set. (An element e is reinserted into a set s if s.add(e) is invoked when s.contains(e) would return true immediately prior to the invocation.)


#### [SortedSet](https://docs.oracle.com/javase/8/docs/api/java/util/SortedSet.html) - interface
```
E first()

E last()

```

#### [NavigableSet](https://docs.oracle.com/javase/8/docs/api/java/util/NavigableSet.html) - interface
- extend: Collection<E>, Iterable<E>, Set<E>, SortedSet<E>

```
E ceiling(E e) // return smallest element >= e

E floor(E e) // return largest element <= e

E higher(E e)

E lower(E e)

E pollFirst()

E pollLast()
```

#### [TreeSet](https://docs.oracle.com/javase/8/docs/api/java/util/TreeSet.html) 
- implement: Iterable, Collection, NavigableSet, Set, SortedSet
- A NavigableSet implementation based on a TreeMap
- guaranteed log(n) time cost for basic operations (add, remove and contains)

#### [Collections](https://docs.oracle.com/javase/8/docs/api/java/util/Collections.html)
```
static <T extends Comparable<? super T>> void sort(List<T> list)

static <T> void sort(List<T> list, Comparator<? super T> c)

/**
return: insertPos
insertPos >= 0, found with position
insertPos < 0, represent insertion point is at index (-insertPos-1)
*/
static <T> int binarySearch(List<? extends T> list, T key, Comparator<? super T> c)
```

#### [BitSet](https://docs.oracle.com/javase/8/docs/api/java/util/BitSet.html)
```
BitSet()
BitSet(int nbits)

void set(int bitIndex)
boolean get(int bitIndex)

void and(BitSet set)
void or(BitSet set)
void xor(BitSet set)
void andNot(BitSet set)
```