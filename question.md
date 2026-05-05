<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>React Fundamentals — DSA-style Question Sheet</title>
<style>
  :root {
    --bg: #0f1115;
    --bg-elev: #161922;
    --bg-soft: #1c2030;
    --border: #262a3a;
    --text: #e6e7ee;
    --text-dim: #9aa0b4;
    --accent: #61dafb;
    --accent-2: #7c5cff;
    --good: #4ade80;
    --warn: #facc15;
    --hover: #1f2333;
    --shadow: 0 4px 20px rgba(0,0,0,.25);
  }
  [data-theme="light"] {
    --bg: #f7f8fb;
    --bg-elev: #ffffff;
    --bg-soft: #f0f2f8;
    --border: #e4e7ef;
    --text: #1a1d29;
    --text-dim: #5c6479;
    --accent: #0aa6c7;
    --accent-2: #6244ee;
    --good: #16a34a;
    --warn: #d97706;
    --hover: #eef0f7;
    --shadow: 0 4px 20px rgba(0,0,0,.06);
  }

  * { box-sizing: border-box; }
  html, body { margin: 0; padding: 0; }
  body {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Inter, Roboto, sans-serif;
    background: var(--bg);
    color: var(--text);
    line-height: 1.55;
    -webkit-font-smoothing: antialiased;
  }

  /* Header */
  header.top {
    position: sticky;
    top: 0;
    z-index: 50;
    background: var(--bg-elev);
    border-bottom: 1px solid var(--border);
    padding: 14px 28px;
    display: flex;
    align-items: center;
    gap: 18px;
    backdrop-filter: blur(10px);
  }
  .brand {
    display: flex;
    align-items: center;
    gap: 10px;
    font-weight: 700;
    font-size: 18px;
  }
  .brand .logo {
    width: 28px; height: 28px;
    border-radius: 8px;
    background: linear-gradient(135deg, var(--accent), var(--accent-2));
    display: grid; place-items: center;
    color: #0f1115; font-weight: 900;
    font-size: 14px;
  }
  .progress-wrap {
    flex: 1;
    display: flex;
    align-items: center;
    gap: 12px;
    max-width: 500px;
  }
  .progress-bar {
    flex: 1;
    height: 8px;
    background: var(--bg-soft);
    border-radius: 99px;
    overflow: hidden;
  }
  .progress-fill {
    height: 100%;
    width: 0%;
    background: linear-gradient(90deg, var(--accent), var(--accent-2));
    transition: width .4s ease;
  }
  .progress-text { font-size: 13px; color: var(--text-dim); white-space: nowrap; min-width: 70px; text-align: right; }
  .top-actions { display: flex; gap: 8px; align-items: center; }
  .icon-btn {
    background: var(--bg-soft);
    color: var(--text);
    border: 1px solid var(--border);
    padding: 7px 12px;
    border-radius: 8px;
    cursor: pointer;
    font-size: 13px;
    transition: all .15s;
  }
  .icon-btn:hover { background: var(--hover); }

  /* Layout */
  .layout {
    display: grid;
    grid-template-columns: 260px 1fr;
    gap: 0;
    max-width: 1280px;
    margin: 0 auto;
  }
  aside.sidebar {
    position: sticky;
    top: 65px;
    height: calc(100vh - 65px);
    overflow-y: auto;
    padding: 24px 16px;
    border-right: 1px solid var(--border);
  }
  aside .side-title {
    font-size: 11px;
    font-weight: 700;
    letter-spacing: .12em;
    color: var(--text-dim);
    text-transform: uppercase;
    margin: 0 0 12px 8px;
  }
  aside ul { list-style: none; padding: 0; margin: 0; }
  aside li a {
    display: flex;
    justify-content: space-between;
    align-items: center;
    text-decoration: none;
    color: var(--text-dim);
    padding: 8px 12px;
    border-radius: 8px;
    font-size: 14px;
    margin-bottom: 2px;
    transition: all .15s;
  }
  aside li a:hover { background: var(--hover); color: var(--text); }
  aside li a.active { background: var(--bg-soft); color: var(--text); font-weight: 600; }
  aside li a .count {
    font-size: 11px;
    background: var(--bg-soft);
    color: var(--text-dim);
    padding: 2px 7px;
    border-radius: 99px;
    border: 1px solid var(--border);
  }
  aside li a.active .count { background: var(--accent); color: #0f1115; border-color: transparent; }

  main {
    padding: 32px 36px 80px;
    max-width: 900px;
  }

  /* Topic blocks */
  .topic { margin-bottom: 56px; scroll-margin-top: 90px; }
  .topic-header {
    display: flex;
    align-items: baseline;
    gap: 12px;
    margin-bottom: 6px;
  }
  .topic-num {
    font-size: 12px;
    font-weight: 700;
    color: var(--accent);
    background: var(--bg-soft);
    padding: 4px 10px;
    border-radius: 6px;
    letter-spacing: .05em;
  }
  .topic h2 {
    font-size: 26px;
    margin: 0;
    font-weight: 700;
  }
  .topic .topic-sub {
    color: var(--text-dim);
    font-size: 14px;
    margin: 6px 0 20px;
  }

  .qsection {
    background: var(--bg-elev);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 4px 0;
    margin-bottom: 16px;
    overflow: hidden;
  }
  .qsection-title {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 14px 18px;
    border-bottom: 1px solid var(--border);
    font-size: 13px;
    font-weight: 700;
    color: var(--text-dim);
    text-transform: uppercase;
    letter-spacing: .08em;
  }
  .qsection-title.theory::before { content: "📚"; font-size: 16px; }
  .qsection-title.practical::before { content: "🛠"; font-size: 16px; }

  ul.qlist { list-style: none; padding: 0; margin: 0; }
  ul.qlist li.q {
    display: flex;
    align-items: flex-start;
    gap: 12px;
    padding: 12px 18px;
    border-bottom: 1px solid var(--border);
    transition: background .15s;
  }
  ul.qlist li.q:last-child { border-bottom: none; }
  ul.qlist li.q:hover { background: var(--bg-soft); }
  ul.qlist li.q.done .qtext { text-decoration: line-through; color: var(--text-dim); opacity: .65; }

  .checkbox {
    width: 18px; height: 18px;
    margin-top: 4px;
    accent-color: var(--good);
    cursor: pointer;
    flex-shrink: 0;
  }
  .qtext { flex: 1; font-size: 15px; }
  .qactions {
    display: flex;
    gap: 6px;
    opacity: 0;
    transition: opacity .15s;
  }
  ul.qlist li.q:hover .qactions { opacity: 1; }
  .qactions button {
    background: transparent;
    color: var(--text-dim);
    border: 1px solid var(--border);
    padding: 4px 9px;
    border-radius: 6px;
    cursor: pointer;
    font-size: 11px;
    transition: all .15s;
  }
  .qactions button:hover { background: var(--accent); color: #0f1115; border-color: transparent; }

  /* Toast */
  .toast {
    position: fixed;
    bottom: 24px;
    left: 50%;
    transform: translateX(-50%) translateY(20px);
    background: var(--bg-elev);
    border: 1px solid var(--good);
    color: var(--good);
    padding: 10px 18px;
    border-radius: 10px;
    font-size: 13px;
    font-weight: 600;
    box-shadow: var(--shadow);
    opacity: 0;
    pointer-events: none;
    transition: all .25s;
    z-index: 100;
  }
  .toast.show {
    transform: translateX(-50%) translateY(0);
    opacity: 1;
  }

  /* Intro card */
  .intro {
    background: linear-gradient(135deg, rgba(97, 218, 251, .1), rgba(124, 92, 255, .1));
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 24px 28px;
    margin-bottom: 36px;
  }
  .intro h1 {
    margin: 0 0 8px;
    font-size: 28px;
  }
  .intro p {
    margin: 0;
    color: var(--text-dim);
    font-size: 14px;
  }
  .intro .how {
    margin-top: 14px;
    font-size: 13px;
    color: var(--text-dim);
    background: var(--bg-soft);
    padding: 12px 14px;
    border-radius: 8px;
    border-left: 3px solid var(--accent);
  }
  .intro .how b { color: var(--text); }

  @media (max-width: 900px) {
    .layout { grid-template-columns: 1fr; }
    aside.sidebar { display: none; }
    main { padding: 20px; }
    header.top { padding: 12px 16px; gap: 10px; flex-wrap: wrap;}
    .progress-wrap { order: 3; flex-basis: 100%; max-width: none; }
  }
</style>
</head>
<body data-theme="dark">

<header class="top">
  <div class="brand">
    <div class="logo">⚛</div>
    <span>React Fundamentals Sheet</span>
  </div>
  <div class="progress-wrap">
    <div class="progress-bar"><div class="progress-fill" id="progressFill"></div></div>
    <div class="progress-text" id="progressText">0 / 0</div>
  </div>
  <div class="top-actions">
    <button class="icon-btn" id="resetBtn" title="Reset progress">Reset</button>
    <button class="icon-btn" id="themeBtn" title="Toggle theme">🌙</button>
  </div>
</header>

<div class="layout">
  <aside class="sidebar">
    <div class="side-title">Topics</div>
    <ul id="sideNav"></ul>
  </aside>

  <main id="content">
    <div class="intro">
      <h1>React, the DSA way 🧠</h1>
      <p>A topic-by-topic checklist of theoretical + practical React questions. Solve each one in your own editor or notebook, then paste it into Claude / ChatGPT for evaluation.</p>
      <div class="how">
        <b>How to use:</b> Click <i>Copy</i> on any question to copy it as a ready-to-paste AI prompt. Tick the box once you've answered. Progress saves automatically in your browser.
      </div>
    </div>
    <div id="topics"></div>
  </main>
</div>

<div class="toast" id="toast">Copied!</div>

<script>
/* ============== DATA ============== */
const TOPICS = [
  {
    id: "components",
    title: "1. Components & Props",
    sub: "Your first taste of React — components, JSX, and passing data down.",
    theory: [
      "What is a component in React, and why do we break UI into components?",
      "Difference between functional and class components — which one is preferred today and why?",
      "What are props? Can a child modify the props it receives? Why or why not?",
      "What is JSX? Is it required to use React? What does it compile to?",
      "What is the special `children` prop and where is it useful?"
    ],
    practical: [
      "Create a `Greeting` component that takes a `name` prop and renders 'Hello, {name}'.",
      "Build a `Card` component that wraps any content using the `children` prop.",
      "Build a `Button` component that accepts a `variant` prop (`primary` | `secondary`) and styles itself accordingly.",
      "Build a `UserList` component that takes an array of users and renders a `UserCard` for each one."
    ]
  },
  {
    id: "usestate",
    title: "2. useState (in depth)",
    sub: "The hook you'll use 80% of the time. Get the mental model right here.",
    theory: [
      "Why can't we just use a normal JavaScript variable for state in a functional component?",
      "Why is `setState` asynchronous, and what problem does that cause?",
      "What is the difference between `setCount(count + 1)` and `setCount(prev => prev + 1)`? Give a case where the difference matters.",
      "Why should you never mutate state directly (e.g. `state.push(item)`)? What does React actually compare?",
      "What is automatic batching in React 18? How does it differ from older versions?",
      "What is lazy initial state, and when should you use `useState(() => expensiveCalc())`?",
      "How do you correctly update an object in state without losing other fields?",
      "How do you update a specific item inside an array in state immutably?"
    ],
    practical: [
      "Build a counter with Increment, Decrement, and Reset buttons.",
      "Build a counter that increments by 3 in a single click — using THREE `setCount(c=>c+1)` calls. Then try with `setCount(count+1)` three times and explain the difference.",
      "Build a Todo app with: add todo, delete todo, toggle complete (no external libs).",
      "Build a registration form with name, email, password fields managed in a SINGLE state object.",
      "Build a list of users where you can edit a single user's name without re-typing other users' data.",
      "Demonstrate a bug where mutating an array (e.g. `arr.push(x)` then `setArr(arr)`) does NOT trigger a re-render. Then fix it.",
      "Build a 'lazy initialiser' demo: load a heavy default value from `localStorage` only on first mount."
    ]
  },
  {
    id: "useeffect",
    title: "3. useEffect",
    sub: "Side effects, lifecycle, and the famous dependency array.",
    theory: [
      "What is `useEffect`? When does it run relative to render?",
      "Explain the three forms: no dep array, empty `[]` dep array, and `[a, b]` deps. What does each mean?",
      "What is the cleanup function in `useEffect` and when does it run?",
      "How do you replicate `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount` with `useEffect`?",
      "What is a 'stale closure' inside `useEffect`, and how do dependencies fix it?",
      "Why is using `useEffect` to derive state from props usually a code smell? What should you do instead?"
    ],
    practical: [
      "Fetch a list of posts from `https://jsonplaceholder.typicode.com/posts` on mount. Show loading and error states.",
      "Build a debounced search input — only fire the API call 500ms after the user stops typing. (Use cleanup!)",
      "Add a `window` resize listener that updates state with the current width. Clean it up properly on unmount.",
      "Build a stopwatch with Start / Stop / Reset using `setInterval` + cleanup.",
      "Sync a piece of state with `localStorage` — read on mount, write on every change."
    ]
  },
  {
    id: "router",
    title: "4. React Router v6",
    sub: "Client-side routing — nested routes, params, and navigation.",
    theory: [
      "Difference between `BrowserRouter` and `HashRouter` — when would you pick which?",
      "What changed from React Router v5 to v6 (e.g. `Switch` → `Routes`, `component` → `element`)?",
      "What is `<Outlet />` and how does it enable nested layouts?",
      "Explain `useNavigate`, `useParams`, `useLocation`, and `useSearchParams` — give one use case each.",
      "How would you implement a private/protected route in v6?"
    ],
    practical: [
      "Create an app with three routes: `/`, `/about`, `/contact`, and a top nav.",
      "Add a dynamic route `/users/:id` that shows the user id using `useParams`.",
      "Build a nested layout: `/dashboard` has a sidebar and renders `/dashboard/profile` and `/dashboard/settings` via `<Outlet />`.",
      "Build a `<ProtectedRoute>` wrapper that redirects to `/login` if the user is not authenticated.",
      "Build a search page where the query string (`?q=react`) is read and updated using `useSearchParams`.",
      "Programmatically navigate to `/dashboard` after a successful login button click."
    ]
  },
  {
    id: "context",
    title: "5. Context API",
    sub: "Solving prop drilling — and where Context shines vs hurts.",
    theory: [
      "What problem does React Context solve? Define 'prop drilling'.",
      "How do you create and consume a Context? Walk through `createContext`, `Provider`, `useContext`.",
      "Why can Context cause performance issues, and how would you mitigate them (e.g. splitting contexts, memoising the value)?",
      "When would you choose Context over Redux, and vice versa?"
    ],
    practical: [
      "Build a `ThemeContext` that toggles between light and dark mode across the whole app.",
      "Build an `AuthContext` exposing `user`, `login`, `logout`. Use it from a Navbar component.",
      "Build a `CartContext` with `items`, `addItem`, `removeItem`. Show a cart count in the header.",
      "Demonstrate a re-render issue: every consumer re-renders when context value changes. Fix by splitting into two contexts (state + dispatch)."
    ]
  },
  {
    id: "advanced-hooks",
    title: "6. useReducer, useCallback, useMemo",
    sub: "Reducers for complex state, memoisation for performance.",
    theory: [
      "When would you reach for `useReducer` over `useState`?",
      "What does `useCallback` do? When does it actually help, and when is it premature optimisation?",
      "Difference between `useMemo` and `useCallback` — give one example of each.",
      "What is referential equality and why does it matter for `React.memo` / dependency arrays?",
      "Name two cases where memoising HURTS performance instead of helping."
    ],
    practical: [
      "Convert a counter from `useState` to `useReducer` with `INCREMENT`, `DECREMENT`, `RESET` actions.",
      "Rebuild your Todo app from Section 2 using `useReducer` (`ADD`, `REMOVE`, `TOGGLE`).",
      "Build a component that computes a slow factorial — use `useMemo` so it only recomputes when input changes.",
      "Use `React.memo` on a child + `useCallback` on the parent's handler to prevent unnecessary child re-renders. Prove it with `console.log`.",
      "Build a shopping cart reducer with actions: `ADD_ITEM`, `REMOVE_ITEM`, `INCREASE_QTY`, `DECREASE_QTY`, `CLEAR`."
    ]
  },
  {
    id: "other-hooks",
    title: "7. Other Hooks (useRef, useId, custom, etc.)",
    sub: "The remaining hooks every React dev should at least recognise.",
    theory: [
      "What are the two main use cases of `useRef`? Why doesn't changing a ref trigger a re-render?",
      "Difference between `useEffect` and `useLayoutEffect`. When do you actually need `useLayoutEffect`?",
      "What is `useImperativeHandle` and when is it needed?",
      "What is `useId` and what problem does it solve in SSR apps?",
      "Quick overview of React 18's `useTransition` and `useDeferredValue`.",
      "What are the rules of hooks, and why must hooks be called at the top level of a component (not inside conditions/loops)?"
    ],
    practical: [
      "Build a custom `useFetch(url)` hook returning `{ data, loading, error }`.",
      "Build a custom `useDebounce(value, delay)` hook.",
      "Use `useRef` to focus an input automatically on mount.",
      "Use `useRef` to store the previous value of a state variable and display it.",
      "Use `useLayoutEffect` to measure the width of a DOM element after render."
    ]
  },
  {
    id: "internals",
    title: "8. Behind the Scenes — How React Works",
    sub: "Virtual DOM, reconciliation, keys, Fiber, rendering — the stuff that separates juniors from seniors.",
    theory: [
      "What is the Virtual DOM and how is it different from the real DOM?",
      "Explain the reconciliation algorithm — how does React decide what to update?",
      "Why is the `key` prop important in lists? What goes wrong if you use the array index as the key when items are reordered or deleted?",
      "What is React Fiber, and why was it introduced?",
      "What causes a component to re-render? Name all triggers.",
      "What does `<React.StrictMode>` do, and why does it sometimes call your component twice in dev?",
      "Difference between controlled and uncontrolled components — give an example of each.",
      "What is `React.memo` and when does it actually prevent re-renders (and when doesn't it)?",
      "How does React handle events? What are synthetic events and event delegation in React?",
      "Explain React 18's automatic batching, concurrent rendering, and transitions in plain English.",
      "Why must hooks always run in the same order? What does React internally use to track them?"
    ],
    practical: [
      "Build a list where deleting an item from the MIDDLE breaks state when index is used as key. Fix it with stable IDs.",
      "Build a controlled vs uncontrolled form side-by-side — show how to read values from both.",
      "Optimise a parent + 100 children component using `React.memo` + `useCallback`. Confirm via React DevTools Profiler that re-renders dropped."
    ]
  },
  {
    id: "redux",
    title: "9. Redux & Redux Toolkit",
    sub: "The classic state management library — and the modern way to write it.",
    theory: [
      "What is Redux and what problem does it solve?",
      "Explain the three principles of Redux (single source of truth, state is read-only, changes via pure reducers).",
      "Define: store, action, reducer, dispatch, selector.",
      "What is middleware in Redux? What does `redux-thunk` do?",
      "Why must reducers be pure functions?",
      "What is Redux Toolkit and which problems of plain Redux does it solve?",
      "What is `createSlice`? How does it leverage Immer to allow 'mutating' code?",
      "What is `createAsyncThunk` and how does it model `pending` / `fulfilled` / `rejected` states?",
      "What is RTK Query and when would you use it over `createAsyncThunk`?",
      "When should you choose Redux Toolkit over Context API?"
    ],
    practical: [
      "Set up a Redux Toolkit store with `configureStore` + `Provider` at the app root.",
      "Build a counter slice using `createSlice` with `increment`, `decrement`, `incrementByAmount`.",
      "Rebuild the Todo app using a Redux Toolkit slice (`addTodo`, `toggleTodo`, `removeTodo`).",
      "Fetch a list of users from an API using `createAsyncThunk` and handle loading / success / error in the slice.",
      "Build a simple auth flow with RTK: `loginSlice` storing `user` and `token`, with thunks for `login` and `logout`.",
      "Use RTK Query to fetch and cache a list of posts, then refetch on demand."
    ]
  }
];

/* ============== RENDER ============== */
const STORAGE_KEY = "react_fundamentals_progress_v1";
const stored = JSON.parse(localStorage.getItem(STORAGE_KEY) || "{}");

const sideNav = document.getElementById("sideNav");
const topicsEl = document.getElementById("topics");
let totalQs = 0;

TOPICS.forEach((t, idx) => {
  const total = t.theory.length + t.practical.length;
  totalQs += total;

  // Sidebar
  const li = document.createElement("li");
  li.innerHTML = `<a href="#${t.id}" data-topic="${t.id}">
    <span>${t.title}</span><span class="count" data-side-count="${t.id}">0/${total}</span>
  </a>`;
  sideNav.appendChild(li);

  // Topic block
  const block = document.createElement("section");
  block.className = "topic";
  block.id = t.id;
  block.innerHTML = `
    <div class="topic-header">
      <span class="topic-num">${String(idx + 1).padStart(2, "0")}</span>
      <h2>${t.title.replace(/^\d+\.\s*/, "")}</h2>
    </div>
    <p class="topic-sub">${t.sub}</p>

    <div class="qsection">
      <div class="qsection-title theory">Theoretical</div>
      <ul class="qlist">${t.theory.map((q, i) => questionItem(t.id, "t", i, q)).join("")}</ul>
    </div>
    <div class="qsection">
      <div class="qsection-title practical">Practical</div>
      <ul class="qlist">${t.practical.map((q, i) => questionItem(t.id, "p", i, q)).join("")}</ul>
    </div>
  `;
  topicsEl.appendChild(block);
});

function questionItem(topicId, kind, i, text) {
  const id = `${topicId}-${kind}-${i}`;
  const checked = stored[id] ? "checked" : "";
  const doneClass = stored[id] ? "done" : "";
  return `
    <li class="q ${doneClass}" data-id="${id}">
      <input type="checkbox" class="checkbox" ${checked} />
      <span class="qtext">${text}</span>
      <div class="qactions">
        <button data-action="copy" data-q="${escapeAttr(text)}">Copy Q</button>
        <button data-action="copy-prompt" data-q="${escapeAttr(text)}">Copy as AI prompt</button>
      </div>
    </li>
  `;
}
function escapeAttr(s) {
  return s.replace(/&/g, "&amp;").replace(/"/g, "&quot;").replace(/</g, "&lt;").replace(/>/g, "&gt;");
}

/* ============== INTERACTIONS ============== */
const toast = document.getElementById("toast");
function showToast(msg) {
  toast.textContent = msg;
  toast.classList.add("show");
  clearTimeout(toast._t);
  toast._t = setTimeout(() => toast.classList.remove("show"), 1400);
}

// Checkbox + actions delegation
document.addEventListener("click", (e) => {
  const cb = e.target.closest(".checkbox");
  if (cb) {
    const li = cb.closest("li.q");
    const id = li.dataset.id;
    stored[id] = cb.checked;
    localStorage.setItem(STORAGE_KEY, JSON.stringify(stored));
    li.classList.toggle("done", cb.checked);
    updateProgress();
    return;
  }

  const btn = e.target.closest("button[data-action]");
  if (btn) {
    const text = decodeAttr(btn.dataset.q);
    if (btn.dataset.action === "copy") {
      navigator.clipboard.writeText(text);
      showToast("Question copied!");
    } else if (btn.dataset.action === "copy-prompt") {
      const prompt = `I'm studying React. Please evaluate my answer to the following question. Be honest, point out gaps, and give a short ideal answer at the end.\n\nQuestion: ${text}\n\nMy answer:\n<paste your answer here>`;
      navigator.clipboard.writeText(prompt);
      showToast("AI prompt copied!");
    }
  }
});
function decodeAttr(s) {
  return s.replace(/&quot;/g, '"').replace(/&lt;/g, "<").replace(/&gt;/g, ">").replace(/&amp;/g, "&");
}

// Theme toggle
const themeBtn = document.getElementById("themeBtn");
const savedTheme = localStorage.getItem("react_sheet_theme") || "dark";
document.body.dataset.theme = savedTheme;
themeBtn.textContent = savedTheme === "dark" ? "☀️" : "🌙";
themeBtn.addEventListener("click", () => {
  const next = document.body.dataset.theme === "dark" ? "light" : "dark";
  document.body.dataset.theme = next;
  themeBtn.textContent = next === "dark" ? "☀️" : "🌙";
  localStorage.setItem("react_sheet_theme", next);
});

// Reset
document.getElementById("resetBtn").addEventListener("click", () => {
  if (!confirm("Reset all progress?")) return;
  localStorage.removeItem(STORAGE_KEY);
  document.querySelectorAll(".checkbox").forEach(cb => { cb.checked = false; cb.closest("li.q").classList.remove("done"); });
  Object.keys(stored).forEach(k => delete stored[k]);
  updateProgress();
  showToast("Progress reset");
});

// Progress
function updateProgress() {
  const done = Object.values(stored).filter(Boolean).length;
  document.getElementById("progressFill").style.width = (done / totalQs * 100) + "%";
  document.getElementById("progressText").textContent = `${done} / ${totalQs}`;

  TOPICS.forEach(t => {
    const total = t.theory.length + t.practical.length;
    let count = 0;
    for (let i = 0; i < t.theory.length; i++) if (stored[`${t.id}-t-${i}`]) count++;
    for (let i = 0; i < t.practical.length; i++) if (stored[`${t.id}-p-${i}`]) count++;
    const el = document.querySelector(`[data-side-count="${t.id}"]`);
    if (el) el.textContent = `${count}/${total}`;
  });
}
updateProgress();

// Active section highlight on scroll
const links = document.querySelectorAll("aside a[data-topic]");
const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      links.forEach(l => l.classList.toggle("active", l.dataset.topic === entry.target.id));
    }
  });
}, { rootMargin: "-30% 0px -60% 0px" });
TOPICS.forEach(t => {
  const el = document.getElementById(t.id);
  if (el) observer.observe(el);
});
</script>
</body>
</html>
