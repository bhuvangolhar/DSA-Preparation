<a id="readme-top"></a>

# Arrays Class

> **The `Arrays` class is a toolbox of ready-made static methods for arrays — print, sort, search, copy, fill and compare them without writing the loops yourself.**

![Language](https://img.shields.io/badge/Language-Java-orange?logo=openjdk&logoColor=white)
![Topic](https://img.shields.io/badge/Topic-Arrays_Class-blue)
![Level](https://img.shields.io/badge/Level-Beginner-green)

| Quick Facts | Details |
|---|---|
| **Category** | Array — utility class (`java.util.Arrays`) |
| **Prerequisites** | 1D arrays, `for` loops, calling static methods |
| **Key keywords** | `import java.util.Arrays;` · `toString` · `sort` · `binarySearch` · `copyOf` · `fill` · `equals` |
| **Works with** | Java 8 and above |
| **At a glance** | every method is `static` — call it as `Arrays.method(array)` · `sort` is `O(n log n)` · `binarySearch` is `O(log n)` on a sorted array |

## 🔰 Table of Contents

| Level | Sections |
|---|---|
| 🟢 **Level 1 — Understand** | [Definition](#-definition) · [Key Points](#-key-points) · [How It Works](#-how-it-works) |
| 🟡 **Level 2 — Use It** | [Syntax & Variations](#-syntax--variations) · [Common Patterns](#-common-patterns) · [When to Use](#-when-to-use) · [Example](#-example) · [Code](#-code) |
| 🔴 **Level 3 — Wrap-up** | [Time Complexity](#-time-complexity) · [Common Mistakes](#-common-mistakes) · [Interview Questions](#-interview-questions) · [Summary](#-summary) |

## 📍 Definition

An array knows very little about itself — it only has `length` (and `clone()`). It cannot sort itself, print itself or search itself. The **`Arrays` class** closes that gap: it is a **utility class** in `java.util` full of **static methods** that do the common array jobs for you.

You never create an `Arrays` object. You call the methods on the class name — `Arrays.sort(arr)` — after adding `import java.util.Arrays;`. Some methods **change the array you pass in** (`sort`, `fill`); the others **return** something new — a String, a number, a boolean or a new array.

| Term | Meaning | Example |
|---|---|---|
| **Utility class** | A class that is just a collection of helper methods | `Arrays` |
| **Static method** | A method called on the class name — no object is needed | `Arrays.toString(arr)` |
| **In place** | The method changes the very array you pass in | `Arrays.sort(arr)` |
| **New array** | The method returns a separate copy | `Arrays.copyOf(arr, 5)` |
| **Sorted** | In ascending order, smallest first | `{1, 3, 7}` |
| **Binary search** | A fast search that works only on a sorted array | `Arrays.binarySearch(arr, 7)` |
| **Shallow / deep** | For nested arrays, the "deep" methods look inside the inner arrays | `Arrays.deepToString(table)` |

**In place or new?**

| Method | Changes the array? | Returns |
|---|---|---|
| `sort` | **yes** | nothing (`void`) |
| `fill` | **yes** | nothing (`void`) |
| `toString` | no | a `String` |
| `copyOf` · `copyOfRange` | no | a **new** array |
| `equals` | no | a `boolean` |
| `binarySearch` | no | an `int` |
| `asList` | no | a `List` that is a window onto the array |

> [!TIP]
> **Real-life analogy:** a toolbox that stands next to the array. The array itself only knows how long it is; the toolbox holds the sorting tool (`sort`), the tape measure that finds things fast (`binarySearch`), the photocopier (`copyOf`), the paint roller that sets every slot (`fill`) and the label printer (`toString`).

## 📌 Key Points

1. **Import it, then call it on the class** — `import java.util.Arrays;` and `Arrays.method(array)`; all methods are `static`.
2. **Print with `Arrays.toString(arr)`** — `System.out.println(arr)` only prints a hash such as `[I@6d06d69c`; for a 2D array use `Arrays.deepToString`.
3. **`Arrays.sort(arr)` sorts in place** — ascending, it returns nothing, and it changes the array you gave it; Strings are sorted alphabetically (capital letters first).
4. **`binarySearch` needs a sorted array** — it returns the index when the value is found and a **negative** number when it is not; on an unsorted array the answer cannot be trusted.
5. **`copyOf(arr, n)` returns a new array** — longer than the original it is padded with `0` / `false` / `null`, shorter it is cut; `copyOfRange(arr, from, to)` excludes `to`.
6. **`fill(arr, value)` sets every element** — `fill(arr, from, to, value)` sets a range (`to` is not included).
7. **`Arrays.equals(a, b)` compares the contents** — `a == b` and `a.equals(b)` compare references; use `deepEquals` for nested arrays.
8. **`Arrays.asList(...)` is a fixed-size window** — you can read and replace elements but not add or remove, and it works as expected only on object arrays like `Integer[]`, not on `int[]`.

> [!IMPORTANT]
> **`Arrays.sort` rearranges the very array you give it.** If the original order still matters, copy first — `int[] sorted = Arrays.copyOf(marks, marks.length);` — and sort the copy. `int[] b = a;` is **not** a copy: both names point to the same array.

## ⚙️ How It Works

### `sort` — in place

```text
int[] a = {42, 7, 19, 3};

Arrays.sort(a);          // a is now {3, 7, 19, 42} — the SAME array, now in order
```

### `binarySearch` — halve the range every step

```text
a = {3, 7, 19, 42, 56, 80}              (sorted)       Arrays.binarySearch(a, 56)

Step 1  low = 0, high = 5   middle = index 2 → 19    19 < 56 → the key is in the right half   low = 3
Step 2  low = 3, high = 5   middle = index 4 → 56    found → returns 4
```

When the value is **not** there, the answer is `-(insertion point) - 1`, where the insertion point is the index at which the value would have to be inserted to keep the order:

```text
Arrays.binarySearch(a, 20)    20 would go between 19 (index 2) and 42 (index 3) → insertion point 3
                              returns -(3) - 1 = -4        (any negative number means "not found")
```

### `copyOf` — a new array of the length you ask for

```text
int[] a = {1, 2, 3};

Arrays.copyOf(a, 5)   → {1, 2, 3, 0, 0}     longer: padded with the default value
Arrays.copyOf(a, 2)   → {1, 2}              shorter: cut off
```

> [!NOTE]
> Binary search can skip half of the array at every step only because the array is sorted — that is why it is so fast, and why it gives wrong answers on unsorted data. The basics of arrays are in array.md, and tables of rows and columns in 2d-array.md; for text there is the matching toolbox in string-methods.md.

## 🔄 Syntax & Variations

The examples use arrays such as `int[] arr = {5, 2, 9, 1};`.

### Print

| Method | Example | Result |
|---|---|---|
| **`Arrays.toString(arr)`** | `Arrays.toString(arr)` | `"[5, 2, 9, 1]"` |
| **`Arrays.deepToString(arr)`** | `Arrays.deepToString(new int[][]{{1, 2}, {3, 4}})` | `"[[1, 2], [3, 4]]"` |

### Sort

| Method | Example | Result |
|---|---|---|
| **`Arrays.sort(arr)`** | `Arrays.sort(arr)` | `arr` becomes `[1, 2, 5, 9]` |
| **`Arrays.sort(arr, from, to)`** | `Arrays.sort(arr, 1, 3)` | sorts only the indexes `1` and `2` — `to` is not included |
| **Strings** | `Arrays.sort(names)` | alphabetical; capital letters come before small ones |
| **Descending** | `Arrays.sort(boxed, Collections.reverseOrder())` | needs an `Integer[]` — it does not work on `int[]` |

### Search

| Method | Example | Result |
|---|---|---|
| **`Arrays.binarySearch(arr, key)`** | `Arrays.binarySearch(sorted, 90)` | the index if found, otherwise `-(insertion point) - 1` |

For an **unsorted** array that you search only once, a simple loop is better than sorting first.

### Copy and resize

| Method | Example | Result |
|---|---|---|
| **`Arrays.copyOf(arr, n)`** | `Arrays.copyOf(small, 5)` | a new array of length `n` — padded or cut |
| **`Arrays.copyOfRange(arr, from, to)`** | `Arrays.copyOfRange(marks, 1, 4)` | the elements `1` to `3` — `to` is not included |
| **`arr.clone()`** | `arr.clone()` | a copy of the same length |
| **`System.arraycopy(src, srcPos, dest, destPos, length)`** | `System.arraycopy(src, 1, dest, 0, 3)` | copies a range into an existing array (a method of `System`, not `Arrays`) |
| **Not a copy** | `int[] b = a;` | both names point to the **same** array |

### Fill and compare

| Method | Example | Result |
|---|---|---|
| **`Arrays.fill(arr, value)`** | `Arrays.fill(arr, -1)` | every element becomes `-1` |
| **`Arrays.fill(arr, from, to, value)`** | `Arrays.fill(arr, 1, 3, 7)` | indexes `1` and `2` become `7` |
| **`Arrays.equals(a, b)`** | `Arrays.equals(x, y)` | `true` when both have the same length and the same elements |
| **`Arrays.deepEquals(a, b)`** | `Arrays.deepEquals(t1, t2)` | the same for nested arrays |

### Lists and streams

| Method | Example | Result |
|---|---|---|
| **`Arrays.asList(...)`** | `Arrays.asList(boxedNums)` | a fixed-size `List` view — `add` and `remove` throw `UnsupportedOperationException` |
| **A list you can change** | `new ArrayList<>(Arrays.asList(boxedNums))` | a real, growable list |
| **`Arrays.stream(arr).sum()`** | `Arrays.stream(marks).sum()` | the sum of an `int[]` (Java 8) |
| **`Arrays.stream(arr).max()`** | `Arrays.stream(marks).max().getAsInt()` | the largest value |

### Not in the `Arrays` class

Beginners often look for these — there is no ready-made method, so do this instead:

| Need | Do this |
|---|---|
| Add or remove an element | arrays have a fixed size — copy into a bigger or smaller array with `copyOf`, or use an `ArrayList` |
| Check whether a value is in the array | a loop; or sort first and use `binarySearch(...) >= 0` |
| Reverse the array | a loop with two indexes that swap and move inwards |
| Find the largest or smallest value | a loop, or `Arrays.stream(arr).max()` / `.min()` |

## 🧩 Common Patterns

| Pattern | Idea | Code |
|---|---|---|
| **Print an array** | one call instead of a loop | `System.out.println(Arrays.toString(arr));` |
| **Sort a copy** | keep the original order | `int[] s = Arrays.copyOf(arr, arr.length); Arrays.sort(s);` |
| **Smallest and largest** | sort, then look at the two ends | `s[0]` and `s[s.length - 1]` |
| **Fast repeated lookup** | sort once, then use binary search many times | `Arrays.binarySearch(s, key) >= 0` |
| **Grow an array** | copy it into a bigger one | `arr = Arrays.copyOf(arr, arr.length * 2);` |
| **Start with a default value** | fill instead of a loop | `Arrays.fill(arr, -1);` |
| **Find duplicates** | sort, then compare neighbors | `if (s[i] == s[i + 1]) …` |
| **Are two arrays the same?** | compare the content | `Arrays.equals(a, b)` |

## 🎯 When to Use

| Need | Use | Watch out |
|---|---|---|
| See what is inside an array | **`toString`** · `deepToString` | never `println(arr)` |
| Put the values in order | **`sort`** | it changes the array — copy first if the order matters |
| Find a value in a **sorted** array | **`binarySearch`** | on an unsorted array the result is unreliable |
| Find a value once in an **unsorted** array | **a loop** | sorting first costs `O(n log n)` — more than one pass |
| Make a copy, grow or shrink an array | **`copyOf`** · `copyOfRange` | the result is a new array; `to` is not included |
| Give every element the same value | **`fill`** | for a table, fill each row separately |
| Check whether two arrays hold the same values | **`equals`** · `deepEquals` | never `==` |
| A list you can add to and remove from | **`new ArrayList<>(Arrays.asList(...))`** | `Arrays.asList` alone has a fixed size |

## 🎲 Example

**Problem:** the marks `{85, 90, 78, 92, 66}` must stay in their original order, but you also need them sorted, the lowest and highest mark, and a quick check whether `90` and `80` are among them.

**Dry run — step by step**

| Step | Code | Result |
|---|---|---|
| 1 | `int[] sorted = Arrays.copyOf(marks, marks.length);` | `sorted` = `[85, 90, 78, 92, 66]` — a separate array |
| 2 | `Arrays.sort(sorted);` | `sorted` = `[66, 78, 85, 90, 92]`, `marks` is unchanged |
| 3 | `sorted[0]` and `sorted[sorted.length - 1]` | `66` lowest, `92` highest |
| 4 | `Arrays.binarySearch(sorted, 90)` | `3` — found at index `3` |
| 5 | `Arrays.binarySearch(sorted, 80)` | `-3` — not found; `-(2) - 1`, so it would be inserted at index `2` |
| 6 | `Arrays.equals(marks, sorted)` | `false` — the same values, but in a different order |

✅ Sorting a **copy** kept the original order; one sort made the lowest and highest values instant and made `binarySearch` possible.

## 💻 Code

> Save it as `ArraysClassDemo.java`, then run `javac ArraysClassDemo.java` followed by `java ArraysClassDemo`.

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collections;
import java.util.List;

public class ArraysClassDemo {

    // Helper: prints "label : value" in neat columns
    static void show(String label, Object value) {
        System.out.printf("%-30s: %s%n", label, value);
    }

    public static void main(String[] args) {

        int[] marks = {85, 90, 78, 92, 66};

        // ----- Print: println(array) shows a hash, Arrays.toString shows the values -----
        show("Arrays.toString(marks)", Arrays.toString(marks));
        show("Arrays.deepToString(2D)", Arrays.deepToString(new int[][]{{1, 2}, {3, 4}}));

        // ----- Sort a COPY, so the original order is kept -----
        int[] sorted = Arrays.copyOf(marks, marks.length);
        Arrays.sort(sorted);                                    // sorts IN PLACE and returns nothing
        show("marks (original)", Arrays.toString(marks));
        show("sorted (the copy)", Arrays.toString(sorted));
        show("lowest / highest", sorted[0] + " / " + sorted[sorted.length - 1]);

        // ----- Sort only a part: index 1 up to, but NOT including, 4 -----
        int[] part = {9, 8, 7, 6, 5};
        Arrays.sort(part, 1, 4);
        show("sort(part, 1, 4)", Arrays.toString(part));

        // ----- Sort Strings, and descending order -----
        String[] names = {"banana", "Apple", "cherry"};
        Arrays.sort(names);                                     // capital letters come before small ones
        show("sorted Strings", Arrays.toString(names));
        Integer[] boxed = {5, 2, 9, 1};                         // descending needs Integer[], not int[]
        Arrays.sort(boxed, Collections.reverseOrder());
        show("descending (Integer[])", Arrays.toString(boxed));

        // ----- Binary search: the array must be SORTED -----
        show("binarySearch(sorted, 90)", Arrays.binarySearch(sorted, 90));
        int pos = Arrays.binarySearch(sorted, 80);             // not found: -(insertion point) - 1
        show("binarySearch(sorted, 80)", pos);
        show("insertion point for 80", -pos - 1);
        show("binarySearch on UNSORTED", Arrays.binarySearch(marks, 90) + " (90 IS in marks!)");

        // ----- Copy: copyOf pads or cuts, copyOfRange takes from .. to - 1 -----
        int[] small = {1, 2, 3};
        show("copyOf(small, 5)", Arrays.toString(Arrays.copyOf(small, 5)));
        show("copyOf(small, 2)", Arrays.toString(Arrays.copyOf(small, 2)));
        show("copyOfRange(marks, 1, 4)", Arrays.toString(Arrays.copyOfRange(marks, 1, 4)));
        show("grow: copyOf(small, 6)", Arrays.toString(Arrays.copyOf(small, small.length * 2)));
        int[] src = {1, 2, 3, 4, 5};
        int[] dest = new int[5];
        System.arraycopy(src, 1, dest, 0, 3);                   // 3 elements, from src[1] into dest[0]
        show("System.arraycopy", Arrays.toString(dest));
        int[] alias = marks;                                    // NOT a copy: the same array
        alias[0] = 100;
        show("marks[0] after alias[0]=100", marks[0]);
        marks[0] = 85;                                          // put it back

        // ----- Fill -----
        int[] scores = new int[5];
        Arrays.fill(scores, -1);
        show("fill(scores, -1)", Arrays.toString(scores));
        Arrays.fill(scores, 1, 3, 7);                           // index 1 up to, but NOT including, 3
        show("fill(scores, 1, 3, 7)", Arrays.toString(scores));

        // ----- Compare the CONTENT -----
        int[] x = {1, 2, 3};
        int[] y = {1, 2, 3};
        show("x == y", x == y);
        show("x.equals(y)", x.equals(y));
        show("Arrays.equals(x, y)", Arrays.equals(x, y));
        show("Arrays.equals(marks, sorted)", Arrays.equals(marks, sorted));
        show("deepEquals on 2D", Arrays.deepEquals(new int[][]{{1}, {2}}, new int[][]{{1}, {2}}));

        // ----- Arrays and lists -----
        Integer[] boxedNums = {3, 1, 2};
        List<Integer> view = Arrays.asList(boxedNums);          // a fixed-size list backed by the array
        show("Arrays.asList(Integer[])", view);
        try {
            view.add(4);
        } catch (UnsupportedOperationException e) {
            show("view.add(4)", "UnsupportedOperationException");
        }
        List<Integer> real = new ArrayList<>(Arrays.asList(boxedNums));
        real.add(4);
        show("new ArrayList<>(asList(...))", real);
        show("asList(int[]).size()", Arrays.asList(new int[]{1, 2, 3}).size());   // ONE element: the whole array

        // ----- Streams (Java 8): sum, max and average of an int[] -----
        show("stream: sum / max", Arrays.stream(marks).sum() + " / " + Arrays.stream(marks).max().getAsInt());
        show("stream: average", Arrays.stream(marks).average().getAsDouble());
    }
}
```

**Output**

```text
Arrays.toString(marks)        : [85, 90, 78, 92, 66]
Arrays.deepToString(2D)       : [[1, 2], [3, 4]]
marks (original)              : [85, 90, 78, 92, 66]
sorted (the copy)             : [66, 78, 85, 90, 92]
lowest / highest              : 66 / 92
sort(part, 1, 4)              : [9, 6, 7, 8, 5]
sorted Strings                : [Apple, banana, cherry]
descending (Integer[])        : [9, 5, 2, 1]
binarySearch(sorted, 90)      : 3
binarySearch(sorted, 80)      : -3
insertion point for 80        : 2
binarySearch on UNSORTED      : -4 (90 IS in marks!)
copyOf(small, 5)              : [1, 2, 3, 0, 0]
copyOf(small, 2)              : [1, 2]
copyOfRange(marks, 1, 4)      : [90, 78, 92]
grow: copyOf(small, 6)        : [1, 2, 3, 0, 0, 0]
System.arraycopy              : [2, 3, 4, 0, 0]
marks[0] after alias[0]=100   : 100
fill(scores, -1)              : [-1, -1, -1, -1, -1]
fill(scores, 1, 3, 7)         : [-1, 7, 7, -1, -1]
x == y                        : false
x.equals(y)                   : false
Arrays.equals(x, y)           : true
Arrays.equals(marks, sorted)  : false
deepEquals on 2D              : true
Arrays.asList(Integer[])      : [3, 1, 2]
view.add(4)                   : UnsupportedOperationException
new ArrayList<>(asList(...))  : [3, 1, 2, 4]
asList(int[]).size()          : 1
stream: sum / max             : 411 / 92
stream: average               : 82.2
```

> [!NOTE]
> Three lines are worth a second look. `binarySearch on UNSORTED` returns `-4` ("not found") although `90` **is** in `marks` — the search relied on an order that was not there. `marks[0] after alias[0]=100` is `100` because `alias` is the same array, not a copy. And `asList(int[]).size()` is `1`: for a primitive `int[]` the whole array becomes **one** element of the list — use an `Integer[]` instead.

## ⏳ Time Complexity

| Method | Time | Note |
|---|---|---|
| `toString`, `fill`, `equals`, `copyOf` | **O(n)** | each touches every element once |
| `sort` | **O(n log n)** | about this many steps for `n` elements |
| `binarySearch` | **O(log n)** | the array must already be sorted |
| a loop that searches an unsorted array | **O(n)** | the alternative to sorting first |
| `Arrays.asList(...)` | **O(1)** | wraps the array — nothing is copied |

Space: `copyOf` creates a new array of `O(n)` extra space; `sort` works on the array you give it (primitives need very little extra space).

**Feel the difference** — steps to find a value among `n` items:

| n | loop — `O(n)` | `binarySearch` — `O(log n)` |
|---|---|---|
| 10 | 10 | about 4 |
| 1,000 | 1,000 | about 10 |
| 1,000,000 | 1,000,000 | about 20 |

> [!TIP]
> **Rule of thumb:** sorting costs `O(n log n)` **once**. If you will search the same array many times, sort it once and use `binarySearch` each time; for a single search, a plain loop is cheaper than sorting.

## 🚨 Common Mistakes

| # | Mistake | Why it is a problem | Fix |
|---|---|---|---|
| 1 | `System.out.println(arr);` | it prints a hash such as `[I@6d06d69c`, not the values | `Arrays.toString(arr)` — or `Arrays.deepToString` for a table |
| 2 | `Arrays.binarySearch(arr, key)` on an unsorted array | the result cannot be trusted — the demo returns "not found" for a value that is there | `Arrays.sort(arr)` first |
| 3 | `int[] b = a;` and then sorting `b` | `b` is the same array as `a`, so `a` is sorted too | `int[] b = Arrays.copyOf(a, a.length);` |
| 4 | `a == b` or `a.equals(b)` to compare contents | both compare references | `Arrays.equals(a, b)` |
| 5 | `Arrays.sort(intArray, Collections.reverseOrder())` | does not compile — a comparator works only on object arrays: "no suitable method found for sort(int[],Comparator<Object>)" | use an `Integer[]`, or sort ascending and read it backwards |
| 6 | `Arrays.asList(intArray)`, then `list.add(...)` | for an `int[]` the list has **one** element (the array), and `asList` has a fixed size anyway → `UnsupportedOperationException` | use an `Integer[]` and `new ArrayList<>(Arrays.asList(...))` |

## 🎤 Interview Questions

<details>
<summary><b>1. What is the difference between <code>Array</code> and <code>Arrays</code>?</b></summary>

An **array** (`int[]`, `String[]`) is the data structure that holds the values. **`Arrays`** (`java.util.Arrays`) is a **utility class** with static helper methods that work on arrays — `sort`, `toString`, `copyOf`, `binarySearch`, `fill`, `equals` and more. The array has only `length`; the `Arrays` class provides the rest.

</details>

<details>
<summary><b>2. How do you print the contents of an array?</b></summary>

Use `Arrays.toString(arr)` for a 1D array and `Arrays.deepToString(arr)` for a table of arrays, or a loop. `System.out.println(arr)` prints only the type and a hash code, because an array does not override `toString()`.

</details>

<details>
<summary><b>3. How does <code>Arrays.sort</code> work, and what is its complexity?</b></summary>

It sorts the array you pass **in place**, in ascending order, and returns nothing. The time is about `O(n log n)`. Strings are sorted alphabetically (capital letters before small ones); for an object array you can supply your own order with a `Comparator`, for example `Collections.reverseOrder()` for descending.

</details>

<details>
<summary><b>4. How does <code>binarySearch</code> work, and what does it return when the value is missing?</b></summary>

It looks at the middle element and, because the array is sorted, throws away the half that cannot contain the key — repeating until it finds the value or runs out of range: `O(log n)`. It returns the **index** when the value is found and `-(insertion point) - 1` — a negative number — when it is not. The array **must** be sorted, otherwise the result is unreliable.

</details>

<details>
<summary><b>5. How do you copy an array?</b></summary>

`Arrays.copyOf(arr, arr.length)` (or `arr.clone()`) gives a new, independent array; `Arrays.copyOfRange(arr, from, to)` copies a part, and `System.arraycopy(...)` copies a range into an existing array. `int[] b = a;` is **not** a copy — both variables point to the same array. For an array of objects these copies are shallow: the objects themselves are shared.

</details>

<details>
<summary><b>6. How can you "resize" an array?</b></summary>

You cannot — an array has a fixed length. You create a **new** array of the length you want and copy the old values into it: `arr = Arrays.copyOf(arr, newLength);` pads with default values when it is longer and cuts when it is shorter. If the size changes often, use an `ArrayList`, which does this for you.

</details>

## 🏁 Summary

- The **`Arrays` class** (`java.util.Arrays`) is a toolbox of **static** methods for arrays — import it and call `Arrays.method(array)`.
- **Print** with `toString` / `deepToString`; **sort** in place with `sort`; **search** a sorted array with `binarySearch`; **copy** with `copyOf` / `copyOfRange`; **fill** with `fill`; **compare** with `equals`.
- **`sort` and `fill` change the array** you pass in; the others return a new value — so copy first when the original order matters.
- **`binarySearch`** needs a **sorted** array and returns a negative number when the value is missing.
- **`Arrays.asList`** gives a fixed-size list view that works as expected only on object arrays; wrap it in `new ArrayList<>(...)` to get a list you can change.
- `sort` is **O(n log n)**, `binarySearch` **O(log n)**, and the rest are **O(n)**.

### 📝 Cheat Sheet

| Question | Answer |
|---|---|
| Print | `Arrays.toString(arr)` · `Arrays.deepToString(table)` |
| Sort (in place) | `Arrays.sort(arr)` · `Arrays.sort(arr, from, to)` — `to` is not included |
| Search (sorted array only) | `Arrays.binarySearch(arr, key)` — negative when missing |
| Copy or resize | `Arrays.copyOf(arr, n)` · `Arrays.copyOfRange(arr, from, to)` |
| Fill | `Arrays.fill(arr, value)` |
| Compare contents | `Arrays.equals(a, b)` · `Arrays.deepEquals(a, b)` |
| To a list / sum | `Arrays.asList(objectArray)` (fixed size) · `Arrays.stream(arr).sum()` |
| Descending order | an `Integer[]` with `Collections.reverseOrder()` |
| Time | `sort` `O(n log n)` · `binarySearch` `O(log n)` · the others `O(n)` |

> [!IMPORTANT]
> **Copy before you sort, sort before you search:** `Arrays.sort` rearranges the very array you pass it, and `binarySearch` only works on a sorted array — so keep a copy if the original order matters, and sort once before searching many times.
