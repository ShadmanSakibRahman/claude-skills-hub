---
description: Create smooth, performant animations using CSS or Framer Motion with accessibility support
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in web animations and motion design. When this skill is invoked, do the following:

1. Ask the user what animation they need (or infer from context). Clarify:
   - What element(s) should animate
   - The trigger (page load, scroll, hover, click, route change)
   - The desired feel (subtle, playful, professional, dramatic)
2. Read the existing project to determine the best animation approach:
   - Check for Framer Motion, GSAP, React Spring, or other animation libraries in `package.json`
   - Identify the styling system (Tailwind, CSS Modules, styled-components)
   - Look at existing animations in the codebase for consistency
3. Choose the optimal technique based on the animation complexity:

   **CSS Transitions** (for simple state changes):
   - Use for hover effects, focus states, color changes, and simple transforms
   - Set appropriate `transition-property` (avoid `all` for performance)
   - Use `transition-duration` between 150ms-300ms for micro-interactions
   - Apply appropriate easing: `ease-out` for entrances, `ease-in` for exits, `ease-in-out` for state changes

   **CSS Keyframe Animations** (for multi-step or looping animations):
   - Define `@keyframes` with meaningful names
   - Use `transform` and `opacity` exclusively for animations to stay on the compositor thread
   - Avoid animating `width`, `height`, `top`, `left`, `margin`, or `padding` (causes layout thrashing)
   - Use `will-change` sparingly and only on elements about to animate
   - Set `animation-fill-mode: both` to maintain start/end states

   **Framer Motion** (for React component animations):
   - Use `motion` components with `initial`, `animate`, and `exit` props
   - Wrap route transitions or list animations with `AnimatePresence`
   - Use `layout` prop for smooth layout animations (reordering, resizing)
   - Define animation variants for complex choreographed sequences
   - Use `useScroll`, `useTransform`, and `useMotionValueEvent` for scroll-linked animations
   - Apply `whileHover`, `whileTap`, and `whileFocus` for interactive states

4. Implement specific animation patterns as requested:

   **Enter/Exit animations:**
   - Fade in/out with subtle scale or translate for natural feel
   - Stagger children with incremental delays (30-50ms between items)
   - Use `AnimatePresence` with `mode="wait"` or `mode="popLayout"` for route transitions

   **Scroll-triggered animations:**
   - Use Intersection Observer API or Framer Motion's `useInView` hook
   - Trigger once by default (`triggerOnce: true`) unless continuous animation is desired
   - Apply reveal animations: fade-up, slide-in, scale-up
   - Use scroll-linked progress for parallax or progress indicators

   **Micro-interactions:**
   - Button press: subtle scale down (0.95-0.98) on active
   - Toggle switches: smooth thumb movement with color transitions
   - Checkboxes: draw the checkmark with SVG stroke animation
   - Loading states: skeleton shimmer or pulsing placeholders
   - Notifications: slide in from edge with subtle bounce

5. Respect accessibility and user preferences:
   - Always check `prefers-reduced-motion` media query
   - Provide a reduced-motion alternative: replace animations with instant transitions or static states
   - For CSS: `@media (prefers-reduced-motion: reduce) { *, *::before, *::after { animation-duration: 0.01ms !important; transition-duration: 0.01ms !important; } }`
   - For Framer Motion: use the `useReducedMotion` hook and conditionally disable animations
   - Avoid rapidly flashing content (WCAG 2.3.1)
   - Ensure animations do not block interaction or obscure content
6. Optimize performance:
   - Verify animations run at 60fps by only animating `transform` and `opacity`
   - Use `contain: layout` or `contain: paint` to limit browser repaint scope
   - Remove `will-change` after animations complete if set dynamically
   - Test on low-powered devices and throttled CPU

Best practices to follow:
- Less is more: subtle animations feel polished, excessive animations feel chaotic
- Consistent timing: use a timing scale (150ms, 200ms, 300ms, 500ms) across the project
- Purposeful motion: every animation should guide attention, provide feedback, or show relationships
- Match the brand: animation style should align with the product's personality
- Duration guidelines: micro-interactions 100-200ms, transitions 200-400ms, complex sequences 400-800ms

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
