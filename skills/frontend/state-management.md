---
description: Set up and organize state management with stores, selectors, and async operations
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in frontend state management. When this skill is invoked, do the following:

1. Ask the user what state needs to be managed, or infer from context.
2. Read the project to determine the framework and existing state management:
   - Check `package.json` for React, Vue, Angular, or Svelte
   - Identify any existing state management library (Redux, Zustand, Jotai, Recoil, Pinia, Vuex, NgRx)
   - Look at existing store patterns, naming conventions, and folder structure
   - Understand the data flow: what APIs are called, what data is shared across components

3. Recommend the right tool if no state management exists yet:
   - **Zustand:** Best for React apps needing simple, lightweight global state with minimal boilerplate
   - **Redux Toolkit:** Best for large React apps with complex state, many developers, and need for strict patterns
   - **Jotai:** Best for React apps with fine-grained atomic state that avoids unnecessary re-renders
   - **Recoil:** Best for React apps needing derived state and async selectors with Suspense integration
   - **Pinia:** The standard for Vue 3 applications with Composition API support
   - **Context + useReducer:** Sufficient for small React apps with limited shared state
   - Explain the tradeoff to the user and let them decide, or proceed with the best fit

4. Create the store structure based on the chosen library:

   **For Zustand:**
   - Create a store file with typed state interface and actions
   - Use slices pattern for organizing related state (e.g., `createUserSlice`, `createCartSlice`)
   - Implement `immer` middleware for complex nested state updates
   - Add `persist` middleware for state that survives page reloads
   - Create typed selector hooks to prevent unnecessary re-renders
   - Use `subscribeWithSelector` for reacting to specific state changes outside React

   **For Redux Toolkit:**
   - Create feature slices using `createSlice` with typed state, reducers, and actions
   - Set up the store with `configureStore` and proper TypeScript types (`RootState`, `AppDispatch`)
   - Create typed hooks (`useAppSelector`, `useAppDispatch`) in a hooks file
   - Use `createAsyncThunk` for async operations with loading/success/error states
   - Implement `createEntityAdapter` for normalized collections (lists of items with IDs)
   - Add RTK Query for API data fetching with caching, polling, and optimistic updates
   - Use `createSelector` from `reselect` for memoized derived state

   **For Jotai:**
   - Create atoms for each piece of state with TypeScript types
   - Use `atomWithStorage` for persisted state
   - Create derived atoms with `atom((get) => ...)` for computed values
   - Use `atomWithQuery` or `atomWithObservable` for async data
   - Group related atoms in feature-specific files
   - Use `selectAtom` for fine-grained subscriptions to object properties

   **For Pinia (Vue):**
   - Create stores using `defineStore` with the Composition API style (setup function)
   - Define state as `ref`/`reactive`, getters as `computed`, and actions as functions
   - Use `storeToRefs` for destructuring reactive state in components
   - Add plugins for persistence (`pinia-plugin-persistedstate`)
   - Type the store with TypeScript interfaces for state shape

5. Implement async data management:
   - Create async actions/thunks for API calls
   - Track loading state (`idle`, `loading`, `succeeded`, `failed`) per operation
   - Store error information with enough detail for UI display
   - Implement optimistic updates for better UX (update UI immediately, rollback on error)
   - Add request deduplication to prevent duplicate concurrent fetches
   - Cache responses where appropriate with TTL-based invalidation

6. Set up proper TypeScript typing throughout:
   - Type the entire state tree with interfaces
   - Type all action payloads
   - Type selectors with return types
   - Export types for use in components
   - Use discriminated unions for state that has different shapes based on status

7. Add devtools integration:
   - Enable Redux DevTools or Zustand devtools middleware
   - Add meaningful action names for debugging
   - Configure Vue DevTools for Pinia stores

Best practices to follow:
- Keep state minimal: derive what you can, store only source data
- Normalize nested data: use flat structures with ID references for collections
- Colocate state: keep component-local state local; only lift to global store when shared
- Never put UI state (form inputs, toggles) in global stores unless multiple components need it
- Separate server state (API data) from client state (UI preferences); consider React Query/TanStack Query for server state
- Write selectors for all store access; never access raw state shape in components
- Handle all async states: loading, error, success, and idle

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
