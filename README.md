# Set

## Learning Goals

- Understand the Set interface.
- Review commonly used methods of the HashSet.

## Sets in Java

`Set` is another interface in Java that implements the `Collection` interface.
Sets are like lists but do not allow duplicates. There are 2 most commonly-used
implementations of the `Set` interface:

1. HashSet - this set is not ordered and is the type of Set we will focus on
   in this module.
2. TreeSet - this set is ordered based on the elements' natural ordering.

## HashSet in Action

Let's think about our last lab. Every `Book` object has a genre associated with
it. But we would never have two genres both called "Fiction". Each genre is
unique, and we only need it to be in a collection once. This is a perfect example
to use a `Set`!

This is more efficient (in terms of memory space) than just adding the genres to
a `List` because that list would continue to grow with the number of genres,
even when many genres would be duplicates.

Like an `ArrayList`, a `HashSet` grows dynamically and supports some of the same
methods: `clear()`, `contains()`, and `remove()`. We will also import the `Set`
interface and the `HashSet` class from the `java.util` package, just like the
`List` and `ArrayList`.

```java
import java.util.Set;
import java.util.HashSet;

public class Example {
    public static void main(String[] args) {
        Set<String> genres = new HashSet<String>();

        genres.add("Fiction");
        genres.add("Non-fiction");
        genres.add("Poetry");
        genres.add("Drama");
        genres.add("Folktale");

        System.out.println(genres);
    }
}
```

Notably missing is the `get()` method, since a `HashSet` does not maintain
order and therefore does not let us reference its object by index position.

Some things to note about this sample code:

1. If we consider the list of possible genres to be just the genres we defined
   above, then we only have those 5 genres to concern ourselves with.
2. We could have 100s, 1000s or even more `Book` objects in our `Library`
   instance. But we would still only contain a maximum of 5 possible genres.
   This demonstrates the power of sets.
3. Using the right data structure for the job will simplify the code greatly.

### HashSet Constructors

Another way we could have written the above example is to define the set as a
`HashSet` from the start like so:

```java
HashSet<String> genres = new HashSet<String>();
```

If we know about how many items we will be putting in our set, we could
also specify the `HashSet` size like so:

```java
HashSet<String> genres = new HashSet<String>(3);
```

In the above line of code, we are saying we are expecting there to be about 3
items in the `HashSet`.

## Commonly Used Methods

Here are the key methods of the `HashSet` class:

| Method                   | Return Type | Description                                         |
|--------------------------|-------------|-----------------------------------------------------|
| `add(Element item)`      | boolean     | Adds an item to a set                               |
| `remove(Element item)`   | boolean     | Removes an item from a set                          |
| `clear()`                | void        | Removes all items from a set                        |
| `size()`                 | int         | Gets the current size of the set                    |
| `contains(Element item)` | boolean     | Checks to see if a set contains a specific item     |
| `isEmpty()`              | boolean     | Checks to see if a list is empty or has a size of 0 |
