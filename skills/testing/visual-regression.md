---
description: Set up visual regression testing with Playwright screenshots or Percy for UI consistency
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in visual regression testing. Your goal is to set up automated visual comparison testing that catches unintended UI changes while minimizing false positives from dynamic content.

## Step-by-step instructions:

1. **Choose the visual regression tool**:
   - **Playwright screenshots**: Built-in, free, runs locally, good for most projects
   - **Percy (BrowserStack)**: Cloud-based, cross-browser, smart diffing, paid
   - **Chromatic**: Designed for Storybook, visual review workflow
   - **BackstopJS**: Docker-based, configurable viewports, free
   - Check existing dependencies and recommend the best fit

2. **Set up Playwright visual testing** (recommended default):
   - Configure `expect(page).toHaveScreenshot()` in test files
   - Set up `playwright.config.ts` with snapshot settings:
     - `snapshotPathTemplate`: organize screenshots by test/browser/platform
     - `maxDiffPixels` or `maxDiffPixelRatio`: tolerance for acceptable differences
     - `threshold`: per-pixel color difference tolerance (0-1)
   - Configure consistent viewport sizes (1280x720 desktop, 375x667 mobile)

3. **Create visual test specs**:
   - **Full page screenshots**: Key pages in default state
   - **Component screenshots**: Individual components via `locator.screenshot()`
   - **Interactive states**: Hover, focus, active, disabled, expanded/collapsed
   - **Responsive layouts**: Test at mobile, tablet, and desktop breakpoints
   - **Theme variants**: Light mode, dark mode, high contrast if applicable
   - **Data states**: Empty, loading skeleton, populated, error, overflow

4. **Handle dynamic content** to prevent false failures:
   - Mask or hide elements with dynamic content (timestamps, avatars, ads)
   - Use `page.evaluate()` to freeze animations and transitions
   - Set `animations: 'disabled'` in Playwright config
   - Mock API responses to return consistent data
   - Use CSS to hide or replace elements: `page.addStyleTag({content: '.dynamic { visibility: hidden }'})`
   - Wait for fonts and images to load before capturing

5. **Establish baseline images**:
   - Generate initial baseline screenshots on a consistent environment (CI preferred)
   - Review each baseline manually before committing
   - Store baselines in version control (git-lfs for large files) or cloud storage
   - Document the baseline generation process for the team

6. **Configure CI integration**:
   - Run visual tests in a Docker container for consistent rendering
   - Use the same OS and browser versions across all environments
   - Set up artifact upload for diff images on failure
   - Configure the pipeline to block merges on visual regression failures
   - Add a manual approval step for intentional visual changes

7. **Set up the review workflow**:
   - On failure, generate side-by-side comparison images (actual vs expected vs diff)
   - Provide a command to update baselines: `npx playwright test --update-snapshots`
   - Require visual change approval in PR reviews
   - Maintain a changelog of intentional visual changes
   - Periodically review and clean up obsolete baselines

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
