https://www.baeldung.com/java-convert-iterator-to-list


Loop
```
List<Integer> actualList = new ArrayList<Integer>();
while (iterator.hasNext()) {
    actualList.add(iterator.next());
}
```

Iterator.forEachRemaining
```
List<Integer> actualList = new ArrayList<Integer>();
iterator.forEachRemaining(actualList::add);
```

Java8 Streams
```
Iterable<Integer> iterable = () -> iterator;

List<Integer> actualList = StreamSupport
  .stream(iterable.spliterator(), false)
  .collect(Collectors.toList());
```

Guava
```
List<Integer> actualList = ImmutableList.copyOf(iterator);

assertThat(actualList, containsInAnyOrder(1, 2, 3));

or

List<Integer> actualList = Lists.newArrayList(iterator);

assertThat(actualList, containsInAnyOrder(1, 2, 3));
```

