# Linked Lists, Stacks & Queues

Three classic problems solved with linked structures built from scratch in Java.
No `java.util` collections are used — every queue, stack, and list in this
repository is implemented by hand so the underlying mechanics stay visible.

I/O goes through Princeton's `algs4` standard library.

---

## 🚀 Problems Solved

### 🔹 Josephus Problem

`N` people stand in a circle and every `M`-th person is eliminated until nobody
is left. The program prints the elimination order.

Implemented with a **custom linked queue** (`LinkedQueue`) holding `IntNode`
elements. Each round rotates the circle by dequeuing and re-enqueuing `M - 1`
people, then dequeues the `M`-th and prints it. Rotating the queue rather than
indexing a list is what makes the circular structure fall out naturally.

Runs in O(N · M) time and O(N) space.

```bash
java Josephus 7 2
# 1 3 5 0 4 2 6
```

### 🔹 Balanced Parentheses

Checks whether a string of brackets is correctly balanced, supporting `()`,
`[]`, and `{}`. Any other character is ignored.

Implemented with a **resizing array-backed stack** (`ResizingCharStack`).
Opening brackets are pushed; a closing bracket pops the top and fails if the
pair doesn't match. A string is balanced only if nothing is left on the stack
at the end, which catches unclosed openers as well as mismatches.

The stack doubles its capacity when full and halves it when it drops to a
quarter, so the array never sits mostly empty and push stays O(1) amortized.

```bash
echo "{[()]}" | java Parentheses
# true
```

### 🔹 Remove Duplicates from a Sorted List

Removes repeated values from a singly linked list, reading several test cases
in one run.

Implemented with a **hand-written linked list** (`IntLinkedList` over
`IntNode`) supporting append, print, and in-place duplicate removal. The removal
walks the list once and unlinks a node whenever it equals its successor, so it
targets *consecutive* duplicates and assumes the input is sorted. Nothing is
copied — the original nodes are relinked in place.

Runs in O(n) time and O(1) extra space.

```bash
# first line: number of test cases, then length + values per case
echo "1
6
1 1 2 3 3 4" | java RemoveDuplicates
# 1 2 3 4
```

---

## 🧠 Technical Highlights

- **No built-in collections.** `Queue`, `Stack`, and `LinkedList` are all
  implemented from scratch rather than imported.
- **Amortized resizing.** The character stack grows by doubling and shrinks by
  halving, keeping memory proportional to actual use.
- **In-place list surgery.** Duplicate removal relinks existing nodes instead of
  allocating a new list.
- **Defensive edge cases.** Queue and stack underflow throw explicit exceptions;
  empty inputs and invalid arguments are handled rather than left to crash.

---

## 🛠️ Build & Run

Requires Java 17+ and the `algs4` library on the classpath.

```bash
./gradlew build
```

Each class has its own `main`, so run whichever problem you want directly.