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

## Other Collection Interfaces & Abstract Classes

- `List` - Collection that maintains a particular order
- `Queue` - A Collection with the concept of order and specific "head" element
- `Set` - Collection that contains no duplicate value
- `SortedSet` - A Set whose members are sorted

## Common Collection Implementations

- `ArrayList` - A List
- `LinkedList` - A List *and* a Queue
- `HashSet` - A Set implemented as a hash table
- `TreeSet` - A SortedSet

## Sorting
Two ways to achieve this - Sorting the Types that implement Comparable Interface, or using a type that implements Comparator Interface that compares other type
