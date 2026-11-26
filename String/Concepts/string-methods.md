<a id="readme-top"></a>

# String Methods

> **Strings come with a toolbox of ready-made methods — measure, search, cut, compare, clean and convert text without writing the loops yourself.**

![Language](https://img.shields.io/badge/Language-Java-orange?logo=openjdk&logoColor=white)
![Topic](https://img.shields.io/badge/Topic-String_Methods-blue)
![Level](https://img.shields.io/badge/Level-Beginner-green)

| Quick Facts | Details |
|---|---|
| **Category** | String — built-in methods (`java.lang.String`) |
| **Prerequisites** | What a String is, variables, loop basics |
| **Key keywords** | `length()` · `charAt()` · `substring()` · `indexOf()` · `equals()` · `split()` |
| **Works with** | Java 8 and above (a few methods are marked "Java 11+") |
| **At a glance** | indexes start at `0` · methods **return** a result, they never change the String · compare text with `equals()` |

## 🔰 Table of Contents

| Level | Sections |
|---|---|
| 🟢 **Level 1 — Understand** | [Definition](#-definition) · [Key Points](#-key-points) · [How It Works](#-how-it-works) |
| 🟡 **Level 2 — Use It** | [Syntax & Variations](#-syntax--variations) · [Common Patterns](#-common-patterns) · [When to Use](#-when-to-use) · [Example](#-example) · [Code](#-code) |
| 🔴 **Level 3 — Wrap-up** | [Time Complexity](#-time-complexity) · [Common Mistakes](#-common-mistakes) · [Interview Questions](#-interview-questions) · [Summary](#-summary) |

## 📍 Definition

**String methods** are the ready-made operations that every `String` object offers. You call them with a dot — `s.length()`, `s.toUpperCase()` — and they let you **ask** questions about the text, **find** things in it, **cut** pieces out of it, **compare** it, **clean** it up and **convert** it.

A String is **immutable**, so no method ever changes the String itself. A method either **answers a question** (a number, a `true` / `false`) or **returns a new String** that you can keep.

| Term | Meaning | Example with `String s = "Hello World";` |
|---|---|---|
| **Index** | The position of a character, counting from `0` | `s.charAt(0)` → `'H'` |
| **Length** | The number of characters | `s.length()` → `11` |
| **Substring** | A part of the String | `s.substring(0, 5)` → `"Hello"` |
| **Delimiter** | The separator used to cut text into pieces | `s.split(" ")` → `["Hello", "World"]` |
| **Return value** | What a method gives back | `s.indexOf("o")` → `4` |
| **Empty String** | A String with zero characters — not the same as `null` | `"".length()` → `0` |
| **`null`** | No String object at all — calling a method on it throws an exception | `String t = null;` |

**What kind of answer a method gives**

| Group | Returns | Methods |
|---|---|---|
| **Ask a yes / no question** | `boolean` | `contains`, `startsWith`, `endsWith`, `equals`, `isEmpty` |
| **Measure or find a position** | `int` | `length`, `indexOf`, `lastIndexOf`, `compareTo` |
| **Read a part** | `char` or `String` | `charAt`, `substring` |
| **Make a changed copy** | a new `String` | `toUpperCase`, `toLowerCase`, `trim`, `replace`, `concat` |
| **Break into pieces** | `String[]` or `char[]` | `split`, `toCharArray` |

> [!TIP]
> **Real-life analogy:** a String is a row of numbered lockers, and the numbering starts at `0`. The methods let you read a locker, find which locker holds a letter, or photocopy a range of lockers — but they never rearrange the original row. You always get a copy back.

## 📌 Key Points

1. **Indexes start at `0`** — the first character is `charAt(0)` and the last is `charAt(length() - 1)`; anything outside that range throws `StringIndexOutOfBoundsException`.
2. **`length()` has parentheses** — it is a method on a String (an array uses `arr.length` without parentheses).
3. **Methods return results** — a String never changes, so assign the result: `s = s.trim();`.
4. **`substring(start, end)`** — the `start` index is included, the `end` index is **not**; `substring(start)` runs to the end.
5. **Compare text with `equals()`** — or `equalsIgnoreCase()`; never use `==` for text.
6. **`indexOf` gives `-1` when nothing is found** — check for `-1` before you use the position.
7. **`split` takes a regular expression** — so characters such as `.` and `|` must be escaped (`"\\."`), and the result is an array.
8. **`null` is not the same as `""`** — a method called on `null` throws `NullPointerException`; an empty String is fine.

> [!IMPORTANT]
> **Methods do not change the String — they return a result.** `s.toUpperCase();` on its own line does nothing useful. Write `s = s.toUpperCase();` (or use the value directly) to keep the result.

## ⚙️ How It Works

Every character in a String has an index, starting at `0`:

```text
String s = "Hello World";

index   0   1   2   3   4   5   6   7   8   9   10
char    H   e   l   l   o   ␣   W   o   r   l   d        (␣ marks the space at index 5)

s.length()            → 11              the last index is 10
s.charAt(6)           → 'W'
s.indexOf("o")        → 4               the first "o"
s.lastIndexOf("o")    → 7               the last "o"
s.indexOf("z")        → -1              not found
s.substring(0, 5)     → "Hello"         index 0 up to, but NOT including, 5
s.substring(6)        → "World"         index 6 to the end
```

Methods are often **chained**, because each one returns a new String that the next one works on. A realistic clean-up of a line of text:

```text
String line = "  red, green ,blue ";

Step 1  line.trim()                  → "red, green ,blue"           the spaces at both ends are removed
Step 2  .split(",")                  → ["red", " green ", "blue"]   cut at every comma
Step 3  trim each piece              → ["red", "green", "blue"]     the spaces around "green" are removed

The original line is still "  red, green ,blue " — nothing was changed in place.
```

> [!NOTE]
> Why Strings behave this way — immutability and the String pool — is explained in string-pool-and-immutability.md. If you build text in a loop, use the builder from stringbuilder-and-stringbuffer.md instead of repeating `+`.

## 🔄 Syntax & Variations

All examples use `String s = "Hello World";` unless they show their own text.

### Measure and read

| Method | Example | Result | Note |
|---|---|---|---|
| **`length()`** | `s.length()` | `11` | number of characters |
| **`charAt(i)`** | `s.charAt(4)` | `'o'` | exception if `i` is out of range |
| **`isEmpty()`** | `"".isEmpty()` | `true` | `true` when the length is `0` |
| **`toCharArray()`** | `"abc".toCharArray()` | `{'a', 'b', 'c'}` | handy for looping over characters |

### Search

| Method | Example | Result | Note |
|---|---|---|---|
| **`indexOf(x)`** | `s.indexOf("o")` | `4` | the first position, `-1` if missing |
| **`indexOf(x, from)`** | `s.indexOf("o", 5)` | `7` | start looking at index `from` |
| **`lastIndexOf(x)`** | `s.lastIndexOf("o")` | `7` | the last position |
| **`contains(x)`** | `s.contains("World")` | `true` | case-sensitive |
| **`startsWith(x)`** | `s.startsWith("Hello")` | `true` | |
| **`endsWith(x)`** | `s.endsWith("d")` | `true` | |

### Compare

| Method | Example | Result | Note |
|---|---|---|---|
| **`equals(x)`** | `s.equals("hello world")` | `false` | same characters, case-sensitive |
| **`equalsIgnoreCase(x)`** | `s.equalsIgnoreCase("hello world")` | `true` | ignores upper / lower case |
| **`compareTo(x)`** | `"a".compareTo("b")` | `-1` | negative if before, `0` if equal, positive if after (alphabetical order) |
| **`compareToIgnoreCase(x)`** | `"a".compareToIgnoreCase("B")` | negative | the same, ignoring case |

### Cut and change (each returns a new String)

| Method | Example | Result | Note |
|---|---|---|---|
| **`substring(start)`** | `s.substring(6)` | `"World"` | from `start` to the end |
| **`substring(start, end)`** | `s.substring(0, 5)` | `"Hello"` | the `end` index is **not** included |
| **`toUpperCase()`** | `"Hello".toUpperCase()` | `"HELLO"` | |
| **`toLowerCase()`** | `"Hello".toLowerCase()` | `"hello"` | |
| **`trim()`** | `"  hi  ".trim()` | `"hi"` | removes spaces at both ends |
| **`replace(old, new)`** | `"banana".replace("a", "o")` | `"bonono"` | replaces **all** matches |
| **`concat(x)`** | `"Hi".concat("!")` | `"Hi!"` | the same as `"Hi" + "!"` |

### Split and join

| Method | Example | Result | Note |
|---|---|---|---|
| **`split(delimiter)`** | `"a,b,c".split(",")` | `["a", "b", "c"]` | the delimiter is a regular expression |
| **`String.join(sep, items)`** | `String.join("-", "a", "b", "c")` | `"a-b-c"` | Java 8 |

**Splitting on special characters** — in a regular expression some characters have a special meaning:

| To split on | Write | Why |
|---|---|---|
| a comma | `split(",")` | no special meaning |
| one or more spaces | `split("\\s+")` | `\s` means "a space-like character", `+` means "one or more" |
| a dot | `split("\\.")` | a plain `.` means "any character" |
| a pipe | `split("\\|")` | a plain `\|` means "or" |

### Convert

| Need | Use | Example | Result |
|---|---|---|---|
| Number → String | `String.valueOf(x)` | `String.valueOf(42)` | `"42"` |
| String → `int` | `Integer.parseInt(s)` | `Integer.parseInt("42")` | `42` (`NumberFormatException` if it is not a number) |
| String → `double` | `Double.parseDouble(s)` | `Double.parseDouble("3.5")` | `3.5` |
| String → `char[]` | `s.toCharArray()` | `"abc".toCharArray()` | `{'a', 'b', 'c'}` |
| `char[]` → String | `new String(chars)` | `new String(new char[]{'a', 'b'})` | `"ab"` |

### Format

```java
String.format("%s is %d, score %.2f", "Asha", 20, 88.456);    // "Asha is 20, score 88.46"
```

| Code | Meaning | Example |
|---|---|---|
| `%s` | a String | `"Asha"` |
| `%d` | a whole number | `20` |
| `%.2f` | a decimal number with 2 digits after the point | `88.46` |
| `%n` | a new line | — |

### Newer methods (Java 11 or newer)

| Method | Example | Result | Note |
|---|---|---|---|
| **`isBlank()`** | `"   ".isBlank()` | `true` | `true` when empty or only spaces |
| **`strip()`** | `"  hi  ".strip()` | `"hi"` | like `trim()`, also handles Unicode spaces |
| **`repeat(n)`** | `"ab".repeat(3)` | `"ababab"` | |

## 🧩 Common Patterns

| Task | Idea | Code |
|---|---|---|
| **Reverse a String** | use a builder's `reverse()` | `new StringBuilder(s).reverse().toString()` |
| **Check a palindrome** | compare the text with its reverse, ignoring case | `s.equalsIgnoreCase(reversed)` |
| **Count one character** | loop with `charAt` and count the matches | `if (s.charAt(i) == 'a') count++;` |
| **Count vowels** | look the character up in a list of vowels | `"aeiouAEIOU".indexOf(ch) >= 0` |
| **Count words** | trim, then split on spaces | `s.trim().split("\\s+").length` |
| **Capitalize the first letter** | take the first letter and the rest apart | `s.substring(0, 1).toUpperCase() + s.substring(1)` |
| **Remove all spaces** | replace the space with nothing | `s.replace(" ", "")` |
| **Safe empty check** | test `null` first, then the content | `s == null \|\| s.trim().isEmpty()` |
| **Clean up a list** | trim, split, trim every piece | `for (String p : s.trim().split(",")) { p.trim(); }` |

## 🎯 When to Use

| Need | Use | Watch out |
|---|---|---|
| Is the text the same? | **`equals()`** · `equalsIgnoreCase()` | never `==` for text |
| Does it contain, start or end with something? | **`contains`** · `startsWith` · `endsWith` | case-sensitive — lower-case both sides to ignore case |
| Where is something? | **`indexOf`** · `lastIndexOf` | `-1` means "not found" |
| Take a part of it | **`substring`** | the end index is not included, and both indexes must be in range |
| Break it into pieces | **`split`** | special characters need `\\`; the result is an array |
| Clean it up | **`trim`** · `replace` · `toLowerCase` | they return a new String — assign it |
| Turn a number into text, or text into a number | **`String.valueOf`** · **`Integer.parseInt`** | `parseInt` throws `NumberFormatException` for bad input |
| Build text from several parts | **`+`** · `String.join` · `String.format` | many `+` in a loop is slow — use a `StringBuilder` |

## 🎲 Example

**Problem:** the user typed `"  hello, java world  "`. Clean the text, count its words, check whether it mentions `java` (in any case) and capitalize its first word.

**Dry run — step by step**

| Step | Code | Result |
|---|---|---|
| 1 | `String clean = line.trim();` | `"hello, java world"` |
| 2 | `clean.length()` | `17` |
| 3 | `String[] words = clean.split("\\s+");` | `["hello,", "java", "world"]` |
| 4 | `words.length` | `3` words |
| 5 | `clean.toLowerCase().contains("java")` | `true` |
| 6 | `String first = words[0].replace(",", "");` | `"hello"` |
| 7 | `first.substring(0, 1).toUpperCase() + first.substring(1)` | `"Hello"` |

✅ Each step used the result of the one before — and `line` itself is still `"  hello, java world  "`, because no String method changes the original.

## 💻 Code

> Save it as `StringMethodsDemo.java`, then run `javac StringMethodsDemo.java` followed by `java StringMethodsDemo`.

```java
import java.util.Arrays;

public class StringMethodsDemo {

    // Helper: prints "label : value" in neat columns
    static void show(String label, Object value) {
        System.out.printf("%-30s: %s%n", label, value);
    }

    public static void main(String[] args) {

        String s = "Hello World";

        // ----- Measure and read -----
        show("length()", s.length());
        show("charAt(0) / charAt(6)", s.charAt(0) + " / " + s.charAt(6));
        show("last character", s.charAt(s.length() - 1));
        show("isEmpty() on \"\"", "".isEmpty());

        // ----- Search -----
        show("indexOf(\"o\")", s.indexOf("o"));                 // the first o
        show("indexOf(\"o\", 5)", s.indexOf("o", 5));           // start looking at index 5
        show("lastIndexOf(\"o\")", s.lastIndexOf("o"));
        show("indexOf(\"z\")", s.indexOf("z"));                 // -1 means "not found"
        show("contains(\"World\")", s.contains("World"));
        show("startsWith / endsWith", s.startsWith("Hello") + " / " + s.endsWith("d"));

        // ----- Compare -----
        show("equals(\"hello world\")", s.equals("hello world"));
        show("equalsIgnoreCase(...)", s.equalsIgnoreCase("hello world"));
        show("\"a\".compareTo(\"b\")", "a".compareTo("b"));     // negative: "a" comes first
        show("\"b\".compareTo(\"a\")", "b".compareTo("a"));     // positive: "b" comes later
        show("\"a\".compareTo(\"a\")", "a".compareTo("a"));     // 0: equal

        // ----- Cut and change: every method returns a NEW String -----
        show("substring(0, 5)", s.substring(0, 5));             // the end index is NOT included
        show("substring(6)", s.substring(6));
        show("toUpperCase()", s.toUpperCase());
        show("toLowerCase()", s.toLowerCase());
        show("\"  hi  \".trim()", "[" + "  hi  ".trim() + "]");
        show("replace(\"o\", \"0\")", s.replace("o", "0"));     // replaces ALL matches
        show("concat(\"!\")", s.concat("!"));
        show("s is still", s);                                   // the original never changes

        // ----- Split and join -----
        String[] parts = "red,green,blue".split(",");
        show("split(\",\") length / first", parts.length + " / " + parts[0]);
        show("String.join(\"-\", parts)", String.join("-", parts));
        show("split on many spaces", Arrays.toString("a   b  c".split("\\s+")));

        // ----- Characters: loop over a String -----
        int vowels = 0;
        for (int i = 0; i < s.length(); i++) {
            if ("aeiouAEIOU".indexOf(s.charAt(i)) >= 0) {
                vowels++;
            }
        }
        show("vowels in \"Hello World\"", vowels);

        // ----- Convert -----
        show("String.valueOf(42) + 1", String.valueOf(42) + 1);           // text: "421"
        show("Integer.parseInt(\"42\") + 1", Integer.parseInt("42") + 1); // number: 43
        show("\"abc\".toCharArray().length", "abc".toCharArray().length);

        // ----- Format -----
        show("String.format(...)", String.format("%s is %d, score %.2f", "Asha", 20, 88.456));

        // ----- Common tasks -----
        String word = "Racecar";
        String reversed = new StringBuilder(word).reverse().toString();
        show("palindrome \"Racecar\"?", word.equalsIgnoreCase(reversed));
        String name = "java";
        show("capitalize \"java\"", name.substring(0, 1).toUpperCase() + name.substring(1));
        String line = "  Hello, Java World  ";
        String clean = line.trim();
        show("trimmed / word count", "[" + clean + "] / " + clean.split("\\s+").length);
        show("contains java (any case)", clean.toLowerCase().contains("java"));

        // ----- Traps -----
        show("\"a.b.c\".split(\".\").length", "a.b.c".split(".").length);        // "." means "any character" in a regex
        show("\"a.b.c\".split(\"\\\\.\").length", "a.b.c".split("\\.").length);   // escape it
        String t = "  hi  ";
        t.trim();                                                              // the result is thrown away
        show("t after t.trim() alone", "[" + t + "]");
        try {
            s.charAt(11);                                                      // valid indexes are 0 .. 10
        } catch (StringIndexOutOfBoundsException e) {
            show("charAt(11)", "StringIndexOutOfBoundsException");
        }
        String nothing = null;
        try {
            nothing.length();
        } catch (NullPointerException e) {
            show("null.length()", "NullPointerException");
        }
        try {
            Integer.parseInt("abc");
        } catch (NumberFormatException e) {
            show("parseInt(\"abc\")", "NumberFormatException");
        }
    }
}
```

**Output**

```text
length()                      : 11
charAt(0) / charAt(6)         : H / W
last character                : d
isEmpty() on ""               : true
indexOf("o")                  : 4
indexOf("o", 5)               : 7
lastIndexOf("o")              : 7
indexOf("z")                  : -1
contains("World")             : true
startsWith / endsWith         : true / true
equals("hello world")         : false
equalsIgnoreCase(...)         : true
"a".compareTo("b")            : -1
"b".compareTo("a")            : 1
"a".compareTo("a")            : 0
substring(0, 5)               : Hello
substring(6)                  : World
toUpperCase()                 : HELLO WORLD
toLowerCase()                 : hello world
"  hi  ".trim()               : [hi]
replace("o", "0")             : Hell0 W0rld
concat("!")                   : Hello World!
s is still                    : Hello World
split(",") length / first     : 3 / red
String.join("-", parts)       : red-green-blue
split on many spaces          : [a, b, c]
vowels in "Hello World"       : 3
String.valueOf(42) + 1        : 421
Integer.parseInt("42") + 1    : 43
"abc".toCharArray().length    : 3
String.format(...)            : Asha is 20, score 88.46
palindrome "Racecar"?         : true
capitalize "java"             : Java
trimmed / word count          : [Hello, Java World] / 3
contains java (any case)      : true
"a.b.c".split(".").length     : 0
"a.b.c".split("\\.").length   : 3
t after t.trim() alone        : [  hi  ]
charAt(11)                    : StringIndexOutOfBoundsException
null.length()                 : NullPointerException
parseInt("abc")               : NumberFormatException
```

> [!NOTE]
> Three lines are worth a second look. `String.valueOf(42) + 1` gives `421` — text plus a number is **joined**, while `Integer.parseInt("42") + 1` gives `43` — a real addition. `"a.b.c".split(".")` finds **0** pieces because `.` matches every character in a regular expression, so every piece is empty; the escaped `"\\."` finds the **3** real pieces. And `t.trim();` on its own leaves `t` unchanged because the result was thrown away.

## ⏳ Time Complexity

| Method | Time | Note |
|---|---|---|
| `length()`, `charAt(i)`, `isEmpty()` | **O(1)** | the answer is already stored |
| `equals`, `compareTo`, `startsWith` | **O(n)** | compare the characters one by one |
| `contains`, `indexOf`, `lastIndexOf` | **O(n)** | look through the text |
| `substring`, `toUpperCase`, `trim`, `replace`, `concat` | **O(n)** | build a new String of that size |
| `split` | **O(n)** | scans the text once and builds the pieces |
| a loop over the characters with `charAt` | **O(n)** | `n` steps of `O(1)` |
| `indexOf` called inside a loop over the characters | **O(n²)** | a loop of `n` steps, each one scanning up to `n` characters |

> [!TIP]
> **Rule of thumb:** most String methods look through the text once, so they take time proportional to its length. A method call **inside** a loop multiplies the cost — so do not scan the whole String again for every character if you can avoid it.

## 🚨 Common Mistakes

| # | Mistake | Why it is a problem | Fix |
|---|---|---|---|
| 1 | `s.toUpperCase();` or `s.trim();` on its own | a String never changes — the result is thrown away | assign it: `s = s.toUpperCase();` |
| 2 | `if (answer == "yes")` | `==` compares references, not the text | `"yes".equals(answer)` |
| 3 | `s.charAt(s.length())`, or `i <= s.length()` in a loop | the last index is `length() - 1` → `StringIndexOutOfBoundsException` | use `i < s.length()` |
| 4 | `"Hello".substring(1, 3)` expecting `"ell"` | the end index is **not** included — you get `"el"` | `substring(1, 4)` for `"ell"`; remember `[start, end)` |
| 5 | `"a.b.c".split(".")` | `.` means "any character" in a regular expression → the result is empty | escape it: `split("\\.")` |
| 6 | calling a method on `null` (`nothing.length()`) | `NullPointerException` — and an empty `""` is **not** `null` | check first: `s != null && !s.isEmpty()` |

## 🎤 Interview Questions

<details>
<summary><b>1. What is the difference between <code>length</code>, <code>length()</code> and <code>size()</code>?</b></summary>

| Where | What you write | Example |
|---|---|---|
| **Array** | `length` — a field, no parentheses | `arr.length` |
| **String** | `length()` — a method | `s.length()` |
| **Collection** (`ArrayList`, …) | `size()` — a method | `list.size()` |

</details>

<details>
<summary><b>2. How do you compare two Strings?</b></summary>

Use `equals()` to compare the characters (case-sensitive) and `equalsIgnoreCase()` to ignore case. Use `compareTo()` for alphabetical order. Do **not** use `==`: it compares references and can give `false` for equal text. The reason is explained in string-pool-and-immutability.md.

</details>

<details>
<summary><b>3. What does <code>"programming".substring(2, 5)</code> return?</b></summary>

`"ogr"`. The characters are `p0 r1 o2 g3 r4 a5 …`, and `substring(2, 5)` takes the index `2` up to — but **not including** — index `5`: that is `o`, `g`, `r`. The result has `5 - 2 = 3` characters.

</details>

<details>
<summary><b>4. What is the difference between <code>""</code> and <code>null</code>, and between <code>isEmpty()</code> and <code>isBlank()</code>?</b></summary>

`""` is a real String with zero characters — you can call methods on it (`"".length()` is `0`). `null` means there is no String object — any method call throws `NullPointerException`. `isEmpty()` is `true` only for a String of length `0`; `isBlank()` (Java 11 and newer) is also `true` for a String that contains only spaces.

</details>

<details>
<summary><b>5. How do you reverse a String or check whether it is a palindrome?</b></summary>

Reverse with a builder: `new StringBuilder(s).reverse().toString()`, or with a loop that walks from `length() - 1` down to `0`. A String is a **palindrome** when it equals its reverse (use `equalsIgnoreCase` to ignore case): `"Racecar"` reversed is `"racecaR"`, so the check is `true`.

</details>

<details>
<summary><b>6. How do you split a String on a dot or a pipe?</b></summary>

`split` takes a **regular expression**, where `.` means "any character" and `|` means "or". Escape them with two backslashes: `s.split("\\.")` and `s.split("\\|")`. Two more details: trailing empty pieces are dropped — `"a,b,,".split(",")` gives `["a", "b"]` — and splitting an empty String gives an array with **one** empty String.

</details>

<details>
<summary><b>7. How do you convert between a String and a number?</b></summary>

String → number: `Integer.parseInt("42")` or `Double.parseDouble("3.5")` — both throw `NumberFormatException` when the text is not a number. Number → String: `String.valueOf(42)`, or `Integer.toString(42)`. Remember that `"42" + 1` is the text `"421"`, while `Integer.parseInt("42") + 1` is the number `43`.

</details>

## 🏁 Summary

- **String methods** measure, search, cut, compare, clean and convert text — and because a String is immutable, they **return** a result instead of changing the String.
- **Indexes start at `0`**; the last valid index is `length() - 1`, and `substring(start, end)` does **not** include `end`.
- Compare text with **`equals()`** / `equalsIgnoreCase()`, never with `==`; `indexOf` returns **`-1`** when nothing is found.
- **`split`** takes a regular expression — escape `.` and `|` with `\\` — and returns an array.
- Convert with **`Integer.parseInt`** and **`String.valueOf`**; build text with `+`, `String.join` or `String.format`.
- A call on **`null`** throws an exception, an empty `""` does not; most methods take **O(n)** time.

### 📝 Cheat Sheet

| Question | Answer |
|---|---|
| Length / one character | `s.length()` · `s.charAt(i)` — valid indexes `0` … `length() - 1` |
| Find | `s.indexOf("x")` — `-1` if missing · `s.contains("x")` · `s.startsWith("x")` |
| Compare | `s.equals(t)` · `s.equalsIgnoreCase(t)` · `s.compareTo(t)` — never `==` |
| Part of a String | `s.substring(start, end)` — `end` is not included |
| Change a copy | `s.toUpperCase()` · `s.trim()` · `s.replace("a", "b")` — assign the result |
| Split / join | `s.split(",")` · `String.join("-", parts)` |
| To a number / to text | `Integer.parseInt(s)` · `String.valueOf(n)` |
| Format | `String.format("%s %d %.2f", text, whole, decimal)` |
| Newer (Java 11+) | `isBlank()` · `strip()` · `repeat(n)` |

> [!IMPORTANT]
> **Methods return, they do not change:** a String is never edited in place — always use or assign the value a method returns, and compare text with `equals()`.
