# Contributing to JavaMem 🧠

Thanks for your interest in contributing! JavaMem is a browser-based Java memory visualizer built to correct the mental models that textbooks get wrong. Every contribution — big or small — helps developers learn better.

---

## 📌 Before You Start

- Check the [open issues](https://github.com/Neeraj281998/JavaMem-Java-Memory-Visualizer/issues) to see what needs work
- Issues labeled `good first issue` are great starting points if you're new to the project
- If you want to work on something, **comment on the issue first** so we don't duplicate effort

---

## 🛠️ How to Set Up Locally

JavaMem has zero dependencies — no npm, no build step, no backend.

```bash
# 1. Fork the repo and clone it
git clone https://github.com/YOUR_USERNAME/JavaMem-Java-Memory-Visualizer.git

# 2. Open the file directly in your browser
open index.html   # macOS
start index.html  # Windows
xdg-open index.html  # Linux
```

That's it. Edit `index.html`, refresh the browser, see changes instantly.

---

## 🔄 Submitting a Pull Request

1. **Fork** the repository
2. **Create a branch** with a descriptive name:
   ```bash
   git checkout -b fix/hashmap-bucket-rendering
   git checkout -b feature/queue-visualization
   ```
3. **Make your changes** in `index.html`
4. **Test manually** — open in Chrome, Firefox, and Safari if possible
5. **Commit** with a clear message:
   ```bash
   git commit -m "fix: correct LinkedList node spacing on small screens"
   git commit -m "feat: add Queue data structure visualization"
   ```
6. **Push** and open a Pull Request against `main`

---

## ✅ PR Checklist

Before submitting, please make sure:

- [ ] The visualizer renders correctly in a modern browser
- [ ] No existing feature is broken
- [ ] New syntax (if added) is documented in the README's **Supported Syntax** section
- [ ] Code is readable — add a comment if something isn't obvious

---

## 💡 Types of Contributions Welcome

| Type | Examples |
|------|---------|
| 🐛 Bug fixes | Rendering glitches, broken interactions, wrong memory behavior |
| ✨ New data structures | Queue, PriorityQueue, Deque, Graph |
| 📖 Documentation | Clearer explanations, fixing typos, adding examples |
| 🎨 UI improvements | Better colors, responsive layout, accessibility |
| ⚡ Performance | Smoother animations, faster rendering |
| 🧪 Edge cases | Unusual inputs, boundary conditions |

---

## 🚫 What to Avoid

- Don't add external libraries or npm dependencies — JavaMem must stay a single self-contained HTML file
- Don't change the core educational intent — every visual choice is deliberate (see the README's "Why I Built This" section)
- Don't submit AI-generated code dumps without testing and understanding them

---

## 🗣️ Questions or Ideas?

Open a [GitHub Discussion](https://github.com/Neeraj281998/JavaMem-Java-Memory-Visualizer/discussions) or comment on an existing issue. All skill levels welcome.

---

## 📜 License

By contributing, you agree that your contributions will be licensed under the [MIT License](LICENSE).
