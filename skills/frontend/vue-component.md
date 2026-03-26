---
description: Generate Vue 3 components with Composition API, TypeScript, proper emits/props definitions, and slot support
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert Vue 3 developer. When this skill is invoked, do the following:

1. Ask the user what component they need (or infer from context if provided).
2. Read the existing project structure to understand conventions:
   - Check for Vue 3 vs Vue 2 (look at package.json and existing components)
   - Identify styling approach (scoped CSS, SCSS, Tailwind, UnoCSS)
   - Determine if the project uses Pinia, Vuex, or other state management
   - Check for auto-imports (unplugin-auto-import, unplugin-vue-components)
3. Generate a Vue 3 Single File Component (SFC) using `<script setup lang="ts">` that includes:
   - `defineProps` with full TypeScript interface and default values using `withDefaults`
   - `defineEmits` with typed event payloads
   - `defineSlots` for typed slot definitions where applicable
   - `defineExpose` only when parent access is explicitly needed
   - Composables extracted for reusable logic (use `use` prefix convention)
   - Proper `ref`, `reactive`, `computed`, `watch`, and `watchEffect` usage
4. Structure the SFC in the correct order following Vue style guide:
   - `<script setup lang="ts">` block first
   - `<template>` block second
   - `<style scoped>` block last
5. Follow the Vue style guide strictly:
   - Multi-word component names (except for root App component)
   - PascalCase for component file names
   - Props definitions as detailed as possible with types, defaults, and validators
   - Use `v-bind` shorthand and `v-on` shorthand consistently
   - Prefix component events with descriptive verbs (e.g., `update:modelValue`, `submit`, `cancel`)
6. Include proper template directives:
   - `v-if` / `v-else-if` / `v-else` for conditional rendering
   - `v-for` with `:key` binding (never use index as key for dynamic lists)
   - `v-model` with proper modifiers where needed
7. Add accessibility attributes to the template (ARIA labels, roles, keyboard handlers).
8. If testing infrastructure exists (Vitest, Vue Test Utils), create a corresponding test file.
9. Create or update barrel exports if the project uses them.

Best practices to follow:
- Prefer `<script setup>` over Options API or plain `<script>` with `defineComponent`
- Keep templates readable; extract complex logic into computed properties or composables
- Use `toRefs` or `toRef` when destructuring reactive props in composables
- Avoid mutating props directly; emit events to the parent instead
- Use `shallowRef` for large objects that do not need deep reactivity
- Handle async operations with proper loading and error states
- Keep components focused; split into child components when the template exceeds 100 lines

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
