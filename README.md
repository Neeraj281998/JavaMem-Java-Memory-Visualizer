# 🧠 JavaMem – Java Memory Visualizer

> **A live, browser-based tool that visualizes how Java manages memory — stack, heap, and string pool — in real time.**

JavaMem parses simplified Java code you type and renders an animated, interactive diagram showing exactly where each variable lives, how references point to objects, and how different data structures look in memory. Built as a single self-contained HTML file — no install, no build step, no backend.

---

## 🚀 Live Demo

Open `newVisualIndex.html` directly in any modern browser on a laptop or tablet. That's it.

> ⚠️ Optimized for larger screens (laptop/tablet). A mobile warning is shown on small viewports.

---

## 🎯 What It Does

When you type Java-like declarations into the code editor and press **▶ Run**, JavaMem:

1. **Parses** your code line by line
2. **Renders stack cards** for every variable declared
3. **Spawns heap objects** for reference types, positioned in the correct memory region
4. **Draws animated arrows** from stack variables to their heap objects
5. **Lets you manipulate** each data structure live using Add and Remove controls embedded in each heap card

---

## 🖥️ UI Layout

```
┌──────────────────────────────────────────────────────────────────┐
│  Header: JavaMem logo · Stack / Heap / Pool counts · Zoom        │
├───────────────┬──────────────┬───────────────────────────────────┤
│               │              │                                   │
│  Code Editor  │  Stack Panel │         Heap Region               │
│               │              │   (draggable object cards)        │
│  [▶ Run]      │  (variable   ├───────────────────────────────────┤
│  [Clear]      │   cards,     │                                   │
│  [Scope Pop]  │   bottom-up) │       String Pool Region          │
│  [Arrays]     │              │   (interned strings, int cache)   │
│  [Help]       │              │                                   │
└───────────────┴──────────────┴───────────────────────────────────┘
```

**Animated SVG arrows** float over the entire layout, connecting each stack reference variable to its corresponding heap object.

---

## 📦 Supported Java Types & Data Structures

Every supported type has exactly **two interactive operations: `add` and `remove`** (labeled contextually per type). The code editor also supports declaring and pre-populating them inline.

---

### 🔷 Primitive Types — Stack Only

Primitive values are stored directly on the stack card. No heap object is created.

| Type | Example | Stack Value |
|---|---|---|
| `int` | `int age = 25;` | `25` |
| `double` | `double gpa = 9.2;` | `9.2` |
| `float` | `float pi = 3.14;` | `3.14` |
| `long` | `long big = 100L;` | `100` |
| `boolean` | `boolean flag = true;` | `true` |
| `char` | `char c = 'A';` | `'A'` |
| `byte` | `byte b = 8;` | `8` |
| `short` | `short s = 32;` | `32` |

**Add:** Not applicable — primitives are declared with a value in code.  
**Remove:** Use **Scope Pop** to pop individual primitive variables off the stack.

---

### 🔷 String — String Pool

`String` objects are placed in the **String Pool** region. JavaMem simulates Java's string interning: two variables with identical string values point to the same pool object.

```java
String name  = "Neeraj";
String name2 = "Neeraj"; // → same pool object, two references
```

The stack card shows the pool address; an arrow connects the variable to the interned object.

| Operation | Label | Behavior |
|---|---|---|
| **Add** | — | Declare a new `String` variable in the editor |
| **Remove** | Scope Pop | Remove the variable; if no other references exist, the pool entry is GC'd |

---

### 🔷 Integer Cache

Integers in the range **−128 to 127** are cached (per Java spec). When you declare a boxed integer in this range, JavaMem places the object in the **String Pool region** with a `⚑ CACHE` badge instead of the heap.

---

### 🔷 LinkedList — Visual Node Chain

`LinkedList<T>` is rendered as a visual **node chain** with boxes connected by arrows, simulating a singly-linked list. Each node shows its value and its `next` pointer (or `null` at the tail). The chain is scrollable if it grows long.

```java
LinkedList<Integer> ll = new LinkedList<>();
ll.add(10);
ll.add(20);
ll.add(30);
```

Renders as:

```
HEAD
[10 | next] → [20 | next] → [30 | null] → ∅
```

| Operation | Label | Behavior |
|---|---|---|
| **Add** | `add (tail)` | Appends the entered value to the end of the list |
| **Remove** | `remove (val)` | Removes the first node matching the entered value; if input is blank, removes the tail node |

---

### 🔷 BST — Binary Search Tree

`BST` is rendered as a **canvas-drawn tree diagram** — nodes as yellow-bordered circles, edges as lines, with the root labeled. The canvas resizes dynamically based on tree depth. In-order traversal is shown as a sorted sequence below the tree.

```java
BST tree = new BST();
tree.add(50);
tree.add(30);
tree.add(70);
```

BST enforces **no duplicates**. Only numeric values are accepted.

| Operation | Label | Behavior |
|---|---|---|
| **Add** | `insert` | Inserts a numeric value following BST rules (left < root < right) |
| **Remove** | `delete` | Deletes the node; handles all cases including nodes with two children via in-order successor replacement |

---

### 🔷 ArrayList

`ArrayList<T>` is a dynamic list shown as an index → value table inside the heap card.

```java
ArrayList<String> list = new ArrayList<>();
list.add(Alice);
list.add(Bob);
```

| Operation | Label | Behavior |
|---|---|---|
| **Add** | `add` | Appends the entered value to the end |
| **Remove** | `remove(last)` | Removes the last element |

---

### 🔷 Stack

`Stack<T>` is a LIFO structure. The add operation pushes to the top; remove pops from the top.

```java
Stack<Integer> s = new Stack<>();
s.add(1);
s.add(2);
```

| Operation | Label | Behavior |
|---|---|---|
| **Add** | `push` | Pushes the entered value onto the top of the stack |
| **Remove** | `pop` | Removes and displays the top element |

---

### 🔷 HashMap / TreeMap / LinkedHashMap

Map types display a **key → value** table inside the heap card.

```java
HashMap<String, String> map = new HashMap<>();
map.put(name, Neeraj);
map.put(city, Delhi);
```

| Operation | Label | Behavior |
|---|---|---|
| **Add** | `put` | Inserts or updates an entry with the given key and value |
| **Remove** | `remove` | Deletes the entry with the given key |

---

### 🔷 HashSet / TreeSet

Set types display elements as a `{a, b, c}` list. Duplicates are rejected.

```java
HashSet<String> set = new HashSet<>();
```

| Operation | Label | Behavior |
|---|---|---|
| **Add** | `add` | Adds the value if not already present |
| **Remove** | `remove` | Removes the specified value |

---

### 🔷 Arrays (primitive and object)

Fixed-size arrays are allocated on the heap. The index `[i]` and value are shown per row.

```java
int[] nums = new int[5];
String[] words = new String[3];
```

| Operation | Label | Behavior |
|---|---|---|
| **Add** | `set[i]` | Sets the value at the given index |
| **Remove** | `reset` | Resets the value at the given index to `0` |

---

## 🧰 Editor Controls

| Button | Action |
|---|---|
| **▶ Run** (`Ctrl+Enter`) | Parses the editor code and renders the memory diagram |
| **Clear** | Clears all variables, heap objects, and resets the diagram |
| **Scope Pop** | Opens a panel to select individual stack variables to pop; orphaned heap objects are GC-animated and removed |
| **Arrays** | Inserts a sample array declaration snippet into the editor |
| **Help** | Opens a syntax reference guide |

---

## 🔍 Memory Regions

| Region | Color | What Lives Here |
|---|---|---|
| **Stack** | Blue | All declared variables (primitives as values, references as addresses) |
| **Heap** | Green | All non-pooled reference objects (LinkedList, BST, ArrayList, etc.) |
| **String Pool** | Orange | Interned `String` objects, Integer cache entries |

---

## ⚡ Memory Mechanics Simulated

- **String interning** — identical string literals share one pool object; reference count is tracked
- **Integer cache** — boxed integers −128 to 127 reuse cached heap objects
- **Garbage collection** — when a Scope Pop removes the last reference to a heap object, the object fades out with a GC animation
- **Reference arrows** — animated dashed bezier curves connect each reference variable on the stack to its heap object, color-coded by type
- **Zoom** — each memory region (heap/pool) can be zoomed in or out independently
- **Drag** — heap object cards are freely draggable within their region

---

## 📝 Supported Syntax (Editor)

```java
// Primitive
int x = 10;
double d = 3.14;
boolean flag = true;

// String
String s = "hello";

// Data Structures
ArrayList<String> list = new ArrayList<>();
list.add(Alice);
list.remove();

LinkedList<Integer> ll = new LinkedList<>();
ll.add(10);
ll.add(20);
ll.remove(10);

BST tree = new BST();
tree.add(50);
tree.add(30);
tree.remove(30);

HashMap<String, String> map = new HashMap<>();
map.put(key, value);
map.remove(key);

Stack<Integer> s = new Stack<>();
s.add(1);
s.remove();

HashSet<String> set = new HashSet<>();
set.add(hello);
set.remove(hello);

int[] nums = new int[5];
String[] words = new String[3];
```

> Note: String and identifier values in method calls do not need quotes in the editor syntax.

---



## 🚧 Current Status — Demo / Prototype

> **This is a demo.** The entire application — UI, parser, visualizer, and all data structure logic — lives in a single raw HTML file with vanilla JavaScript. It was built this way to move fast, validate the idea, and get something visual working quickly.

This prototype proves the concept works well. The next step is a proper migration.

### 🔜 Planned: Rebuild with Proper Tools

Right now everything — the buttons, the logic, the visuals — is crammed into one big HTML file. It works, but as the project grows it gets harder to manage and add new things to.

The plan is to rewrite JavaMem in a cleaner, more organized way:

- **Break it into proper pieces** — instead of one giant file, each part of the UI (editor, stack panel, heap cards) will be its own separate, reusable component
- **Keep the data in one place** — right now all the memory state is scattered around; the rewrite will have one central place that holds everything, making it easier to track and update
- **Make the code easier to read and debug** — adding clearer structure so anyone (including future me) can understand what each part does
- **Separate the "parsing" from the "drawing"** — the part that reads your Java code and the part that draws the diagram will be split up, making both easier to fix and improve
- **Add tests** — so if something breaks, it's caught immediately instead of discovered later

Everything that makes this tool fun and useful — the live arrows, the animations, dragging cards around, the add/remove buttons — will stay exactly the same. The rewrite is just about making the code behind it cleaner and easier to build on top of.

** ⭐💡 Have ideas or want to help? Feel free to open an issue or start a discussion.**
