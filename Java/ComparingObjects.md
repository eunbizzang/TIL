Reference : https://www.baeldung.com/java-comparing-objects

1. == and != operators

* Primitive types
```
assertThat(1 == 1).isTrue();
```


Thanks to auto-unboxing, this also works when comparing a primitive value with its wrapper type counterpart:

```
Integer a = new Integer(1);
assertThat(1 == a).isTrue();
````


* Objects
```
Integer a = new Integer(1);
Integer b = new Integer(1);

assertThat(a == b).isFalse();
```

By comparing two objects, the value of those objects isn't 1. Rather, it's their memory addresses in the stack that are different, since both objects are created using the new operator. If we assigned a to b, then we would have a different result:

```
Integer a = new Integer(1);
Integer b = a;

assertThat(a == b).isTrue();
```

Integer#valueOf factory method:
```
Integer a = Integer.valueOf(1);
Integer b = Integer.valueOf(1);

assertThat(a == b).isTrue();
```
The valueOf() method stores the Integer in a cache to avoid creating too many wrapper objects with the same value. Therefore, the method returns the same Integer instance for both calls.


```
assertThat("Hello!" == "Hello!").isTrue();
```
If they're created using the new operator, then they won't be the same.

Finally, two null references are considered the same, while any non-null object is considered different from null:

```
assertThat(null == null).isTrue();

assertThat("Hello!" == null).isFalse();
```


2. Object#equals Method

This method is defined in the Object class so that every Java object inherits it. By default, its implementation compares object memory addresses, so it works the same as the == operator. However, we can override this method in order to define what equality means for our objects.

```ex.java
Integer a = new Integer(1);
Integer b = new Integer(1);

assertThat(a.equals(b)).isTrue();
```
The method still returns true when both objects are the same.

We should note that we can pass a null object as the argument of the method, but not as the object we call the method upon.

We can also use the equals() method with an object of our own. Let's say we have a Person class:
```
public class Person {
    private String firstName;
    private String lastName;

    public Person(String firstName, String lastName) {
        this.firstName = firstName;
        this.lastName = lastName;
    }
}
```
We can override the equals() method for this class so that we can compare two Persons based on their internal details:

```
@Override
public boolean equals(Object o) {
    if (this == o) return true;
    if (o == null || getClass() != o.getClass()) return false;
    Person that = (Person) o;
    return firstName.equals(that.firstName) &&
      lastName.equals(that.lastName);
}
```
For more information, check out our article about this topic.


3. Objects#equals Static Method
We mentioned earlier that we can't use null as the value of the first object, otherwise a NullPointerException will be thrown.

The equals() method of the Objects helper class solves that problem. It takes two arguments and compares them, also handling null values.

Let's compare Person objects again:
```
Person joe = new Person("Joe", "Portman");
Person joeAgain = new Person("Joe", "Portman");
Person natalie = new Person("Natalie", "Portman");

assertThat(Objects.equals(joe, joeAgain)).isTrue();
assertThat(Objects.equals(joe, natalie)).isFalse();
```
As we explained, this method handles null values. Therefore, if both arguments are null, it'll return true, and if only one of them is null, it'll return false.

This can be really handy. Let's say we want to add an optional birth date to our Person class:

```
public Person(String firstName, String lastName, LocalDate birthDate) {
    this(firstName, lastName);
    this.birthDate = birthDate;
}
```

Then we have to update our equals() method, but with null handling. We can do this by adding the condition to our equals() method:

```
birthDate == null ? that.birthDate == null : birthDate.equals(that.birthDate);
```

However, if we add too many nullable fields to our class, it can become really messy. Using the Objects#equals method in our equals() implementation is much cleaner, and improves readability:

```
Objects.equals(birthDate, that.birthDate);
```

4. Comparable Interface
Comparison logic can also be used to place objects in a specific order. The Comparable interface allows us to define an ordering between objects by determining if an object is greater, equal, or lesser than another.

The Comparable interface is generic and has only one method, compareTo(), which takes an argument of the generic type and returns an int. The returned value is negative if this is lower than the argument, 0 if they're equal, and positive otherwise.

Let's say, in our Person class, we want to compare Person objects by their last name:
```
public class Person implements Comparable<Person> {
    //...

    @Override
    public int compareTo(Person o) {
        return this.lastName.compareTo(o.lastName);
    }
}
```

The compareTo() method will return a negative int if called with a Person having a greater last name than this, zero if the same last name, and positive otherwise.


5. Comparator Interface

The Comparator interface is generic and has a compare method that takes two arguments of that generic type and returns an integer. We already saw this pattern earlier with the Comparable interface.

Comparator is similar; however, it's separated from the definition of the class. Therefore, we can define as many Comparators as we want for a class, where we can only provide one Comparable implementation.

Let's imagine we have a web page displaying people in a table view, and we want to offer the user the possibility to sort them by first names rather than last names. This isn't possible with Comparable if we also want to keep our current implementation, but we can implement our own Comparators.

Let's create a Person Comparator that will compare them only by their first names:

```
Comparator<Person> compareByFirstNames = Comparator.comparing(Person::getFirstName);
```
Now let's sort a List of people using that Comparator:

```
Person joe = new Person("Joe", "Portman");
Person allan = new Person("Allan", "Dale");

List<Person> people = new ArrayList<>();
people.add(joe);
people.add(allan);

people.sort(compareByFirstNames);

assertThat(people).containsExactly(allan, joe);
```
There are also other methods on the Comparator interface we can use in our compareTo() implementation:

```
@Override
public int compareTo(Person o) {
    return Comparator.comparing(Person::getLastName)
      .thenComparing(Person::getFirstName)
      .thenComparing(Person::getBirthDate, Comparator.nullsLast(Comparator.naturalOrder()))
      .compare(this, o);
}
```
In this case, we're first comparing last names, then first names. Next we compare birth dates, but as they're nullable, we must say how to handle that. To do this, we give a second argument to say that they should be compared according to their natural order, with null values going last.

