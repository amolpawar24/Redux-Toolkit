# Redux Toolkit — Complete Learning Guide

<p align="center">
  <img src="https://img.shields.io/badge/Redux%20Toolkit-State%20Management-764ABC?style=for-the-badge&logo=redux&logoColor=white" alt="Redux Toolkit"/>
  <img src="https://img.shields.io/badge/React-UI%20Library-61DAFB?style=for-the-badge&logo=react&logoColor=black" alt="React"/>
  <img src="https://img.shields.io/badge/JavaScript-ES6+-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black" alt="JavaScript"/>
  <img src="https://img.shields.io/badge/Learning-In%20Progress-DC2626?style=for-the-badge" alt="Learning in Progress"/>
</p>

<p align="center">
  <b>Learn • Understand • Practice • Build</b>
</p>

<p align="center">
  A structured learning repository dedicated to Redux Toolkit, covering modern Redux concepts, store configuration, slices, reducers, actions, asynchronous logic, React integration, and practical projects.
</p>

---

## 📌 About This Repository

This repository documents my learning journey with **Redux Toolkit (RTK)**, the official recommended approach for writing Redux logic in modern Redux applications.

It contains organized notes, code examples, practice exercises, and small projects to help developers understand state management and apply it in React applications.

### 🎯 Learning Objectives

- Understand Redux and Redux Toolkit.
- Learn centralized state management.
- Configure a Redux store using `configureStore()`.
- Create slices using `createSlice()`.
- Understand actions and reducers.
- Access state using `useSelector()`.
- Dispatch actions using `useDispatch()`.
- Connect React applications using `Provider`.
- Handle asynchronous operations using `createAsyncThunk()`.
- Learn API data fetching and caching with RTK Query.
- Organize multiple slices in scalable applications.
- Build practical projects using Redux Toolkit.

---

## 📚 Table of Contents

1. [Introduction to Redux Toolkit](#-introduction-to-redux-toolkit)
2. [Why Redux Toolkit?](#-why-redux-toolkit)
3. [Core Concepts](#-core-concepts)
4. [Project Setup](#-project-setup)
5. [Configure Store](#-configurestore)
6. [Create Slice](#-createslice)
7. [React Integration](#-react-integration)
8. [Basic Counter Example](#-basic-counter-example)
9. [Asynchronous Logic](#-asynchronous-logic)
10. [RTK Query](#-rtk-query)
11. [Recommended Folder Structure](#-recommended-folder-structure)
12. [Learning Roadmap](#-learning-roadmap)
13. [Practice Projects](#-practice-projects)
14. [Best Practices](#-best-practices)
15. [Useful Resources](#-useful-resources)
16. [Author](#-author)

---

## 🔰 Introduction to Redux Toolkit

**Redux Toolkit (RTK)** is the official, recommended toolset for writing Redux logic. It simplifies store configuration, reducer creation, immutable state updates, and common Redux development patterns.

Redux Toolkit builds on Redux rather than replacing its core concepts.

It helps reduce repetitive code and makes Redux applications easier to maintain.

### What Is State Management?

State management is the process of storing, updating, and accessing application data.

Examples include:

- Counter values.
- Shopping cart items.
- User authentication status.
- Product lists.
- Theme preferences.
- Notifications and application settings.

```javascript
const initialState = {
  count: 0,
  username: "Amol",
  isLoggedIn: false,
};
```

Redux Toolkit provides a structured way to manage shared application state.

---

## 🤔 Why Redux Toolkit?

Redux Toolkit simplifies several tasks that would otherwise require more manual Redux setup.

| Traditional Redux approach | Redux Toolkit approach |
|---|---|
| Manually configure the store | `configureStore()` |
| Define action types and creators separately | `createSlice()` generates them |
| Write immutable update logic manually | Immer supports mutation-style reducer code |
| Configure Redux DevTools manually | DevTools integration is enabled by default |
| Set up common middleware separately | Useful default middleware is included |
| Build data-fetching infrastructure manually | RTK Query provides data-fetching and caching tools |

### Key Benefits

- Less repetitive code.
- Simpler store configuration.
- Convenient action and reducer creation.
- Safer immutable state updates through Immer.
- Integrated Redux DevTools support.
- Built-in support for common Redux middleware.
- Better organization for growing applications.

---

## 🧩 Core Concepts

### 1. Store

The Redux store holds the application state.

With Redux Toolkit, use `configureStore()` to create the store.

```javascript
import { configureStore } from "@reduxjs/toolkit";

const store = configureStore({
  reducer: {},
});

export default store;
```

### 2. Slice

A slice contains a section of application state, its reducer logic, and the actions generated from its reducers.

```javascript
import { createSlice } from "@reduxjs/toolkit";

const counterSlice = createSlice({
  name: "counter",
  initialState: { count: 0 },
  reducers: {
    increment: (state) => {
      state.count += 1;
    },
  },
});

export const { increment } = counterSlice.actions;
export default counterSlice.reducer;
```

### 3. Actions

Actions describe events that should update the state.

When you use `createSlice()`, Redux Toolkit automatically generates action creators for the defined reducers.

```javascript
import { increment } from "./counterSlice";

dispatch(increment());
```

### 4. Reducers

Reducers determine how the state changes in response to actions.

Redux Toolkit uses Immer internally for `createSlice()` reducers, allowing mutation-style syntax while producing immutable state updates.

```javascript
increment: (state) => {
  state.count += 1;
}
```

This syntax is safe inside Redux Toolkit's Immer-powered reducer logic. It should not be copied into an ordinary Redux reducer that must return immutable updates manually.

### 5. useSelector()

The `useSelector()` hook reads data from the Redux store.

```javascript
const count = useSelector((state) => state.counter.count);
```

### 6. useDispatch()

The `useDispatch()` hook provides the store's dispatch function.

```javascript
const dispatch = useDispatch();

dispatch(increment());
```

### 7. Provider

The `Provider` component makes the Redux store available to React components.

```jsx
import { Provider } from "react-redux";
import store from "./app/store";

<Provider store={store}>
  <App />
</Provider>
```

---

## ⚙️ Project Setup

### Prerequisites

Before starting, make sure you have:

- Node.js installed.
- npm installed.
- Basic JavaScript knowledge.
- Basic React knowledge.
- Familiarity with functions, objects, arrays, and ES modules.

### Step 1: Create a React Project

Using Vite:

```bash
npm create vite@latest redux-toolkit-app -- --template react
cd redux-toolkit-app
npm install
```

### Step 2: Install Dependencies

```bash
npm install @reduxjs/toolkit react-redux
```

### Step 3: Start the Development Server

```bash
npm run dev
```

Open the local URL displayed in your terminal.

---

## 🏪 configureStore()

`configureStore()` creates and configures the Redux store.

It automatically sets up useful defaults, including Redux DevTools integration and development checks.

### Example: `src/app/store.js`

```javascript
import { configureStore } from "@reduxjs/toolkit";
import counterReducer from "../features/counter/counterSlice";

const store = configureStore({
  reducer: {
    counter: counterReducer,
  },
});

export default store;
```

### Explanation

- `configureStore()` creates the Redux store.
- `reducer` specifies the reducer or reducer map.
- `counter` becomes the state key for the counter slice.
- `counterReducer` handles counter-related actions.
- The exported store is provided to React using `Provider`.

The state can then be accessed using:

```javascript
state.counter.count
```

---

## 🍰 createSlice()

`createSlice()` is one of the most important Redux Toolkit APIs.

It accepts a slice name, initial state, and reducer functions. It generates the slice reducer and corresponding action creators.

### Example: `src/features/counter/counterSlice.js`

```javascript
import { createSlice } from "@reduxjs/toolkit";

const initialState = {
  count: 0,
};

const counterSlice = createSlice({
  name: "counter",
  initialState,

  reducers: {
    increment: (state) => {
      state.count += 1;
    },

    decrement: (state) => {
      state.count -= 1;
    },

    incrementByAmount: (state, action) => {
      state.count += action.payload;
    },

    reset: (state) => {
      state.count = 0;
    },
  },
});

export const {
  increment,
  decrement,
  incrementByAmount,
  reset,
} = counterSlice.actions;

export default counterSlice.reducer;
```

### What Does This Generate?

- `counterSlice.reducer` — the reducer function.
- `increment()` — an action creator.
- `decrement()` — an action creator.
- `incrementByAmount(amount)` — an action creator carrying a payload.
- `reset()` — an action creator.

Example:

```javascript
dispatch(incrementByAmount(5));
```

This dispatches an action whose payload is `5`.

---

## ⚛️ React Integration

Redux Toolkit is commonly used with React through the separate `react-redux` package.

### Recommended Project Structure

```text
src/
├── app/
│   └── store.js
│
├── features/
│   └── counter/
│       └── counterSlice.js
│
├── App.jsx
└── main.jsx
```

### Step 1: Configure the Store

Create `src/app/store.js` as shown in the `configureStore()` section.

### Step 2: Connect the Store

Create or update `src/main.jsx`:

```jsx
import { StrictMode } from "react";
import { createRoot } from "react-dom/client";
import { Provider } from "react-redux";
import store from "./app/store";
import App from "./App";

createRoot(document.getElementById("root")).render(
  <StrictMode>
    <Provider store={store}>
      <App />
    </Provider>
  </StrictMode>
);
```

### Step 3: Read and Update State

Create or update `src/App.jsx`:

```jsx
import { useDispatch, useSelector } from "react-redux";
import {
  increment,
  decrement,
  incrementByAmount,
  reset,
} from "./features/counter/counterSlice";

function App() {
  const count = useSelector((state) => state.counter.count);
  const dispatch = useDispatch();

  return (
    <main>
      <h1>Redux Toolkit Counter</h1>

      <h2>Count: {count}</h2>

      <button onClick={() => dispatch(increment())}>
        Increment
      </button>

      <button onClick={() => dispatch(decrement())}>
        Decrement
      </button>

      <button onClick={() => dispatch(incrementByAmount(5))}>
        Add 5
      </button>

      <button onClick={() => dispatch(reset())}>
        Reset
      </button>
    </main>
  );
}

export default App;
```

### How It Works

1. `Provider` makes the store available to the React component tree.
2. `useSelector()` reads the current counter value.
3. `useDispatch()` provides the dispatch function.
4. A button dispatches an action generated by `createSlice()`.
5. The slice reducer calculates the next state.
6. React-Redux detects relevant state changes and updates the component.

---

## ⏳ Asynchronous Logic

Redux Toolkit supports asynchronous workflows through `createAsyncThunk()`.

It generates lifecycle actions for pending, fulfilled, and rejected operations.

### Example: Fetching Users

```javascript
import {
  createAsyncThunk,
  createSlice,
} from "@reduxjs/toolkit";

export const fetchUsers = createAsyncThunk(
  "users/fetchUsers",
  async () => {
    const response = await fetch(
      "https://jsonplaceholder.typicode.com/users"
    );

    if (!response.ok) {
      throw new Error("Failed to fetch users");
    }

    return response.json();
  }
);

const usersSlice = createSlice({
  name: "users",

  initialState: {
    items: [],
    status: "idle",
    error: null,
  },

  reducers: {},

  extraReducers: (builder) => {
    builder
      .addCase(fetchUsers.pending, (state) => {
        state.status = "loading";
        state.error = null;
      })

      .addCase(fetchUsers.fulfilled, (state, action) => {
        state.status = "succeeded";
        state.items = action.payload;
      })

      .addCase(fetchUsers.rejected, (state, action) => {
        state.status = "failed";
        state.error = action.error.message;
      });
  },
});

export default usersSlice.reducer;
```

### Lifecycle Actions

| Action | Meaning |
|---|---|
| `fetchUsers.pending` | The request has started. |
| `fetchUsers.fulfilled` | The request completed successfully. |
| `fetchUsers.rejected` | The request failed. |

Register `usersSlice.reducer` in the store before using this example.

---

## 🌐 RTK Query

RTK Query is Redux Toolkit's data-fetching and caching solution.

It helps manage API requests, loading states, errors, caching, and request deduplication.

### Key Features

- API request management.
- Automatic caching.
- Loading and error states.
- Cache invalidation and refetching.
- Generated React hooks.
- Support for query and mutation endpoints.

RTK Query is included with Redux Toolkit and is particularly useful for applications that communicate with REST APIs.

Learn more in the [official RTK Query documentation](https://redux-toolkit.js.org/rtk-query/overview).

---

## 📁 Recommended Folder Structure

```text
redux-toolkit/
│
├── README.md
│
├── 01-introduction/
├── 02-configure-store/
├── 03-create-slice/
├── 04-actions-and-reducers/
├── 05-use-selector/
├── 06-use-dispatch/
├── 07-provider/
├── 08-multiple-slices/
├── 09-create-async-thunk/
├── 10-rtk-query/
├── 11-typescript/
│
├── practice-projects/
│   ├── counter-app/
│   ├── todo-app/
│   ├── shopping-cart/
│   └── user-management/
│
└── notes/
    ├── redux-toolkit-basics.md
    ├── redux-toolkit-apis.md
    └── react-redux.md
```

This is a suggested learning structure. Each topic can contain its own code examples, notes, and exercises.

---

## 🗺️ Learning Roadmap

Use this checklist to track your progress.

### Fundamentals

- [ ] Introduction to Redux Toolkit
- [ ] Understanding application state
- [ ] Redux data flow
- [ ] Redux Toolkit versus classic Redux
- [ ] Installing Redux Toolkit and React-Redux

### Store and Slices

- [ ] `configureStore()`
- [ ] `createSlice()`
- [ ] Initial state
- [ ] Actions and action creators
- [ ] Reducers
- [ ] Action payloads
- [ ] Multiple slices
- [ ] `combineReducers()` when needed

### React Integration

- [ ] `Provider`
- [ ] `useSelector()`
- [ ] `useDispatch()`
- [ ] Sharing state across components
- [ ] Organizing feature-based state

### Advanced Concepts

- [ ] `createAsyncThunk()`
- [ ] `extraReducers`
- [ ] Loading and error states
- [ ] RTK Query
- [ ] API caching and invalidation
- [ ] Redux DevTools
- [ ] TypeScript integration
- [ ] Testing reducers and components

### Projects

- [ ] Counter App
- [ ] Todo App
- [ ] Shopping Cart
- [ ] User Management App
- [ ] API Data Fetching App

---

## 🚀 Practice Projects

| Level | Project | Concepts |
|---|---|---|
| Beginner | Counter App | Store, slice, actions |
| Beginner | Theme Switcher | Shared state |
| Beginner | Todo App | Arrays, add, delete, update |
| Intermediate | Shopping Cart | Products, quantities, totals |
| Intermediate | User Management | Multiple slices |
| Intermediate | API Users App | `createAsyncThunk()` |
| Advanced | Product Dashboard | RTK Query, caching |
| Advanced | TypeScript App | Typed state and actions |

Build each project yourself and commit your progress to GitHub.

---

## ✅ Best Practices

- Use `configureStore()` for store setup.
- Use `createSlice()` to organize related reducers and actions.
- Keep slices focused on specific features.
- Keep reducers predictable and free from side effects.
- Use Immer's mutation-style syntax only within supported Redux Toolkit reducer logic.
- Use `useSelector()` to select the state a component needs.
- Avoid unnecessary duplication of state.
- Handle asynchronous loading and error states.
- Use RTK Query when it fits your API data-fetching needs.
- Keep API logic and UI components organized.
- Use Redux DevTools to inspect actions and state changes.
- Add tests as application logic becomes more complex.

---

## 📖 Useful Resources

- [Redux Toolkit — Official Documentation](https://redux-toolkit.js.org/)
- [Redux Essentials Tutorial](https://redux.js.org/tutorials/essentials/part-1-overview-concepts)
- [Redux Fundamentals Tutorial](https://redux.js.org/tutorials/fundamentals/part-1-overview)
- [React-Redux Documentation](https://react-redux.js.org/)
- [RTK Query Documentation](https://redux-toolkit.js.org/rtk-query/overview)
- [Redux DevTools](https://github.com/reduxjs/redux-devtools)

---

## 👨‍💻 Author

**Amol Pawar**

Full Stack Developer | React.js Developer

Learning, practicing, and building projects to strengthen my frontend and full-stack development skills.

- GitHub: [@amolpawar24](https://github.com/amolpawar24)
- Portfolio: [amolpawar24.vercel.app](https://amolpawar24.vercel.app/)

---

## ⭐ Support

If this repository helps you learn Redux Toolkit, consider giving it a star ⭐.

Explore the examples, practice the concepts, and build your own projects to strengthen your understanding of modern Redux state management.

<p align="center">
  <b>Learn • Build • Grow</b>
</p>

<p align="center">
  Made with ❤️ by Amol Pawar
</p>