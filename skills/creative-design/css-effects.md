---
description: Create CSS visual effects including glassmorphism, gradient animations, text effects, parallax, and hover transitions
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in advanced CSS techniques and visual effects. When asked to create CSS effects, follow these steps:

**Step 1: Assess the Context**
- Identify the target element or component for the effect.
- Determine the framework and CSS approach: vanilla CSS, Tailwind CSS, CSS Modules, styled-components.
- Check browser support requirements (Can I Use) for the CSS features needed.
- Consider performance impact: prefer `transform` and `opacity` for animations (GPU-accelerated).
- Ensure the effect enhances UX rather than distracting from content.

**Step 2: Glassmorphism and Blur Effects**
- Create frosted glass effect:
  ```css
  .glass {
    background: rgba(255, 255, 255, 0.1);
    backdrop-filter: blur(12px);
    -webkit-backdrop-filter: blur(12px);
    border: 1px solid rgba(255, 255, 255, 0.2);
    border-radius: 16px;
    box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
  }
  ```
- Vary the blur amount: subtle (4px), medium (12px), heavy (24px).
- Add a translucent background tint to improve text readability.
- Ensure fallback for browsers without `backdrop-filter` support (solid background).
- Combine with subtle border for depth and definition.

**Step 3: Neumorphism / Soft UI**
- Create the soft, extruded effect using dual box shadows:
  ```css
  .neumorphic {
    background: #e0e0e0;
    border-radius: 12px;
    box-shadow: 8px 8px 16px #bebebe, -8px -8px 16px #ffffff;
  }
  .neumorphic-inset {
    box-shadow: inset 8px 8px 16px #bebebe, inset -8px -8px 16px #ffffff;
  }
  ```
- Use subtle color differences for light and dark shadows.
- Create pressed/inset state for interactive elements.
- Note accessibility concerns: neumorphism can have poor contrast; use with caution.

**Step 4: Gradient Animations**
- Create animated gradient backgrounds:
  ```css
  .gradient-animate {
    background: linear-gradient(-45deg, #ee7752, #e73c7e, #23a6d5, #23d5ab);
    background-size: 400% 400%;
    animation: gradientShift 8s ease infinite;
  }
  @keyframes gradientShift {
    0% { background-position: 0% 50%; }
    50% { background-position: 100% 50%; }
    100% { background-position: 0% 50%; }
  }
  ```
- Create gradient text: `background-clip: text` with `-webkit-text-fill-color: transparent`.
- Create gradient borders using pseudo-elements or `border-image`.
- Use `conic-gradient` for spinner/loading effects.
- Use `radial-gradient` for spotlight or glow effects.

**Step 5: Text Effects**
- Glowing text: use `text-shadow` with multiple colored layers.
- Typewriter effect: animate `width` with `steps()` timing function and a blinking cursor.
- Text reveal: use `clip-path` or `overflow: hidden` with animated height/width.
- Gradient text: `background: linear-gradient(...)` with `background-clip: text`.
- Stroke/outline text: use `-webkit-text-stroke` or paint the text with `color: transparent` and stroke.
- Split text animation: wrap each character in a span and stagger the animation delay.
- Scramble/decode effect: use JavaScript to rapidly cycle through random characters.

**Step 6: Hover Transitions and Micro-Interactions**
- Card hover: lift with shadow increase:
  ```css
  .card { transition: transform 0.2s, box-shadow 0.2s; }
  .card:hover { transform: translateY(-4px); box-shadow: 0 12px 24px rgba(0,0,0,0.15); }
  ```
- Button hover: fill animation using pseudo-element scaling from left or bottom.
- Link underline: animated underline using `background-size` from 0% to 100%.
- Image hover: zoom with `transform: scale(1.05)` inside `overflow: hidden` container.
- Icon hover: rotation, bounce, or color fill transition.
- Use `transition` for triggered effects, `animation` for continuous effects.
- Respect `prefers-reduced-motion`: disable or simplify animations for accessibility.

**Step 7: Parallax and Scroll Effects**
- CSS-only parallax: use `perspective` and `translateZ` on nested layers.
- Scroll-driven animations (modern CSS): use `animation-timeline: scroll()`.
- Sticky elements with scroll-based transforms for header shrinking effects.
- Reveal on scroll: use `IntersectionObserver` in JS to add animation classes.
- Particle backgrounds: use multiple positioned pseudo-elements with different animation durations.
- Performance tips:
  - Use `will-change: transform` sparingly on animated elements.
  - Avoid animating `width`, `height`, `top`, `left` (causes layout thrashing).
  - Test on lower-end devices to ensure smooth performance.
  - Add `@media (prefers-reduced-motion: reduce)` to disable intensive animations.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
