# Collections

## Collection Interface
Extends **`Iterable<E>`**
- `size()`
- `clear()`
- `isEmpty()`
- `add(E element)`
- `addAll(Collection<E> elements)`

The following methods uses Equality-based comparison:
- `contains(E element)`
- `containsAll(Collection<E> elements)`
- `remove(E element)`
- `removeAll(Collection<E> elements)`
- `retainAll(Collection<E> elements)`

### Converting Collections from/to Arrays

- from array to list - `Arrays.asList(T[] T)`
- from list to array
  - `.toArray()` returns an object array
  - `.toArray(T[] array)`
    - passing in zero sized array will return a new array internally
    - passing in an array with enough room to hold all the members of the list will return that particular array filled with the members of the list




### Other Collection Interfaces & Abstract Classes

- `List` - Collection that maintains a particular order
- `Queue` - A Collection with the concept of order and specific "head" element
- `Set` - Collection that contains no duplicate value
- `SortedSet` - A Set whose members are sorted

### Common Collection Implementations

- `ArrayList` - A List
- `LinkedList` - A List *and* a Queue
- `HashSet` - A Set implemented as a hash table
- `TreeSet` - A SortedSet

## Sorting
Two ways to achieve this - Sorting the Types that implement Comparable Interface, or using a type that implements Comparator Interface that compares other type

## Maps
Key Value pairs. Keys need to be unique. Values can be duplicated and also be null.

TODO: Add common map methods

### Map Interfaces

- `Map` - Basic Map operations
- `HashMap` - A Map where the Keys are sorted

### Map Implementations

- `HashMap` - Efficient General Purpose Map Implementations
- `TreeMap` - A SortedMap implemented as a self-balancing tree
