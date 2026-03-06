# JavaMem — GitHub Issues to Create

Copy-paste each one into GitHub → Issues → New Issue.
Add the specified labels after creating each issue.

---

## Issue #1
**Label:** `good first issue` `documentation`

**Title:**
Add syntax examples to the Help panel for all supported data structures

**Body:**
### Description
The `? Help` button opens a syntax reference panel, but it currently doesn't show examples for all supported data structures (e.g. BST, TreeMap, LinkedHashMap, TreeSet).

### What needs to be done
- Review all supported types listed in the README
- Add a usage example for each one inside the Help panel in `index.html`
- Keep the style consistent with existing examples

### Why this matters
New users often don't know the exact syntax to type in the editor. A complete Help panel removes that friction instantly.

### Good for first-timers because
- No complex logic needed
- Just HTML/text editing inside a clearly defined section
- Easy to test visually

---

## Issue #2
**Label:** `good first issue` `bug`

**Title:**
Mobile warning message is too generic — improve it with a redirect suggestion

**Body:**
### Description
JavaMem shows a warning on small viewports saying it's optimized for larger screens. But the message doesn't tell the user *what to do* — it just leaves them stuck.

### What needs to be done
- Update the mobile warning message in `index.html`
- Suggest the user open the link on a laptop or tablet
- Optionally add a "Continue anyway" button that dismisses the warning

### Expected behavior
User on mobile sees a friendly, actionable message instead of a dead end.

### Good for first-timers because
- Pure UI/text change
- No memory logic involved
- Easy to locate and test

---

## Issue #3
**Label:** `good first issue` `documentation`

**Title:**
Add GitHub Topics / tags to the repository

**Body:**
### Description
The repository currently has no GitHub topics set. Topics like `java`, `visualization`, `education`, `data-structures`, `memory-management`, `learning` help people discover JavaMem through GitHub search and topic pages.

### What needs to be done
- Go to the repo settings (top right of repo page → gear icon next to "About")
- Add relevant topics:
  - `java`
  - `visualization`
  - `education`
  - `data-structures`
  - `memory-management`
  - `learning`
  - `browser-based`
  - `computer-science`

### Why this matters
This is one of the easiest ways to get organic discovery on GitHub with zero code changes.

### Good for first-timers because
- No coding required — just a settings change
- Immediate visible impact

---

## Issue #4
**Label:** `enhancement` `good first issue`

**Title:**
Add a Queue data structure visualization

**Body:**
### Description
JavaMem currently supports Stack (LIFO) but not Queue (FIFO). Queue is one of the most commonly taught data structures and a natural complement to Stack.

### Proposed syntax
```
Queue<Integer> q = new Queue<>();
q.enqueue(10);
q.enqueue(20);
q.dequeue();
```

### Expected visual behavior
- Render as a horizontal row of cells (left = front, right = rear)
- `enqueue` adds to the right
- `dequeue` removes from the left
- Label: *FIFO — First In First Out*
- Show `FRONT →` and `← REAR` labels

### Why this matters
Queue is taught alongside Stack in virtually every CS curriculum. Its absence is a noticeable gap.

### Notes
- Follow the same pattern used for `Stack` in `index.html`
- Keep it self-contained — no external libraries

---

## Issue #5
**Label:** `enhancement`

**Title:**
Add a GC log / event timeline panel

**Body:**
### Description
JavaMem already simulates two-phase garbage collection (GC-eligible → collected with delay). But there's no record of what happened — the event just disappears.

### Proposed feature
Add a small collapsible **GC Log panel** (bottom of screen or sidebar) that records events like:
```
[GC] String@"Alice" → eligible (last ref removed)
[GC] String@"Alice" → collected (after 2.3s)
[GC] ArrayList@list1 → eligible
```

### Why this matters
Students often don't realize GC is happening in the background. A live log makes the two-phase process unmissable and educational.

### Acceptance criteria
- [ ] Log appears when GC events fire
- [ ] Shows object type, variable name, and event type
- [ ] Collapsible so it doesn't clutter the UI
- [ ] Cleared when user hits "Clear"

---

## Issue #6
**Label:** `enhancement`

**Title:**
Add keyboard shortcut cheatsheet overlay (Ctrl+/ or ?)

**Body:**
### Description
JavaMem has at least one keyboard shortcut (`Ctrl+Enter` to Run). As the tool grows, more shortcuts may be added. There's no way to discover them currently.

### Proposed feature
Pressing `Ctrl+/` or `?` opens a small overlay listing all available keyboard shortcuts:

| Shortcut | Action |
|----------|--------|
| `Ctrl+Enter` | Run code |
| `Ctrl+L` | Clear |
| `?` | Toggle help |

### Why this matters
Power users (especially CS students doing drills) benefit from keyboard-driven workflows. Discoverability of shortcuts also makes the tool feel more polished.

---

## Issue #7
**Label:** `bug`

**Title:**
Reference arrows don't reposition when heap cards are dragged

**Body:**
### Description
Heap object cards are draggable, but the SVG reference arrows connecting stack variables to heap objects don't update their positions when a card is moved.

### Steps to reproduce
1. Declare `String name = "Alice";`
2. Hit Run — arrow appears from stack to string pool
3. Drag the string pool card to a new position
4. Arrow stays in original position — now points to empty space

### Expected behavior
Arrows should follow the card as it's dragged and update in real time.

### Environment
Tested on Chrome 120+, macOS

---

## Issue #8
**Label:** `enhancement` `documentation`

**Title:**
Add a demo GIF / screen recording to the README

**Body:**
### Description
The README is detailed and well-written, but there's no visual demo. For a *visual tool*, this is the single biggest missing piece. Most visitors decide whether to star/use a project within 10 seconds of landing on the README.

### What needs to be done
- Record a short GIF (10–20 seconds) showing:
  - Typing a few declarations in the editor
  - Hitting Run
  - Watching stack frames, heap objects, and reference arrows appear
  - Optionally showing GC in action
- Tools you can use: [LICEcap](https://www.cockos.com/licecap/), [Kap](https://getkap.co/) (macOS), [ScreenToGif](https://www.screentogif.com/) (Windows)
- Add the GIF at the top of the README, just below the title

### Why this matters
A single GIF would likely 3-5x the star count. It's the highest-ROI change possible right now.
