# Set

## Learning Goals

- Understand the Set interface
- Use Set implementations

## Sets in Java

Sets are like Lists but do not allow duplicates. There are 2 most commonly-used
implementations of Sets:

1. HashSet - this set is not ordered - this is the type of Set we will focus on
   in this module
2. TreeSet - this set is ordered based on the elements' natural ordering

Continuing with our student example, we might use a set to store all the
possible letter grades. We would use a set instead of a list to ensure that all
letter grades are unique, since a Set does not allow duplicates. After we
collect all the grades from all the students, we could then use the `contains()`
method of our set to check if any student got a specific letter grade.

This is more efficient (in terms of memory space) than just adding the grades to
a `List` because that list would continue to grow with the number of grades,
even when many grades would be duplicates.

Like an `ArrayList`, a `HashSet` grows dynamically and supports some of the same
methods: `clear()`, `contains()`, and `remove()`.

Notably missing from this list is the `get()` method, since a `HashSet` does not
maintain order and therefore does not let us reference its object by index
position.

We can combine an example of using a `HashSet` with the `HashMap` example from
the previous section to demonstrate how each data structure has its appropriate,
and different, uses.

In our previous `HashMap` example, we used that data structure to associate a
student name with their grade, which is very useful for being able to look up a
student's grade quickly by looking is up in the `HashMap` by key. Now, imagine
we want to be able to tell if any students got a specific grade. One way to do
this would be to go through every grade in our `studentGrades` data structure
and create another data structure where we count each grade, and then go back
through it and check if a particular grade has a count of 0. This might be
useful if we want to know _how many_ students got a particular grade, but
requires a little bit of extra work compared to addressing the specific
requirement we've been given, which is to be able to determine if _any_ student
got a particular grade.

To do that, we can simply go through the `studentGrades` and add each grade to a
`HashSet`. Since we know the `HashSet` won't allow duplicates, we know that the
data structure will only grow to be as big as the total number of possible
grades, not the total number of students, and since we will have gone through
every student in `studentGrades`, we will also know that all actual student
grades are represented in our data structure.

```java
// build a data structure to quickly determine if any student got a specific grade
Set<String> uniqueStudentGrades = new HashSet<String>();
for (Map.Entry<String, String> studentGrade: studentGrades.entrySet()) {
    uniqueStudentGrades.add(studentGrade.getValue());
}
System.out.println("Did anyone get an A+? " + (uniqueStudentGrades.contains("A+") ? "Yes" : "No"));
```

Some things to note about this sample code:

1. If we consider the list of possible grades to be the letter grades A, B, C, D
   and F, along with their +/- variations, we have a total of 15 possible grades
2. We could have 100s, 1000s or even more students in `studentGrades`, and
   `uniqueStudentGrades` would still only contain a maximum of 15 possible
   entries. This demonstrates the power of sets.
3. Using the right data structure for the job will simplify your code greatly -
   we only need 3 lines of code to fulfill the requirement of having the ability
   to determine if a specific grade has been given to any student, regardless of
   how many students we have

We also introduced an operator we haven't discussed before in the line of code
that outputs the answer to the question of whether anyone got a specific grade:

```java
System.out.println("Did anyone get an A+? " + (uniqueStudentGrades.contains("A+") ? "Yes" : "No"));
```

The expression `uniqueStudentGrades.contains("A+") ? "Yes" : "No"` returns a
`String` based on the result of the boolean expression
`uniqueStudentGrades.contains("A+")`. This is the "ternary operator" and is a
shorthand for and "if/else" statement. The statement
`uniqueStudentGrades.contains("A+") ? "Yes" : "No"` can be translated to the
following `if` statement:

```java
String answer = "";
if (uniqueStudentGrades.contains("A+")) {
    answer = "Yes";
} else {
    answer = "No";
}
```

Using the ternary operator in this case presents two advantages:

1. We've turned 5 lines of code into a single line of code
2. We can now embed the single line of code expression in a larger expression
   and do not have to use the temporary variable `answer`

Note that the ternary operator can be abused to write code that is very hard to
read and understand, so use it sparingly and carefully.
