# Web Performance Handbook

<img align="right" width="100" height="100" title="Logo"
src="./static/images/logo.png" />

Support the project by giving it a star! ⭐

## Metrics

This is a list of the most common metrics which may appear in articles, DevTools, Lighthouse, and other
various tools for working with web performance. Everything is sorted in the alphabetical order.

The factual data is primarily sourced from MDN, web.dev and w3c, however the short description has been rewritten and enhanced.

---

### CLS

**Cumulative Layout Shift**

Measurement Unit: Score (lower is better)

Shows how often users experience unexpected changes in the layout. It measures the 
instability of elements and their overall impact. For example, the banner element changes its height 
during the loading process, which causes a shift in the elements below.

[more details](https://web.dev/articles/cls)

---

### DCL

**DOMContentLoaded**

Measurement Unit: Milliseconds (ms)

Refers to the moment in a webpage's loading process when the DOM is completely parsed. And all deferred scripts have 
downloaded and executed. It doesn't wait for resources.

[more details](https://developer.mozilla.org/en-US/docs/Web/API/Document/DOMContentLoaded_event)

---

### FCP

**First Contentful Paint**

Measurement Unit: Milliseconds (ms)

Measures the time it takes for first bit of any actual content on a page to become visible on the screen. 
This includes text, images, background images, SVG elements, and non-white canvas elements.

[more details](https://web.dev/articles/fcp)

---

### FID

**First Input Delay**

Measurement Unit: Milliseconds (ms)

Measures the time it takes for the browser to respond to a user's first interaction. This interaction can 
include clicks, hovers, touches, and other user events.

[more details](https://web.dev/articles/fid)

---

### FP

**First Paint**

Measurement Unit: Milliseconds (ms)

Marks the first time the browser renders anything visually different from the default background color of the body.

---

### INP

**Interaction to Next Paint**

Measurement Unit: Milliseconds (ms)

Measures the time it takes for the browser to paint the next frame after a user interaction. 

[more details](https://web.dev/articles/inp)

---

### L

**On Load**

Measurement Unit: Milliseconds (ms)

Measures the time when the entire page and its resources are fully loaded. 
It includes all dependent resources: stylesheets, scripts, iframes, and images.

[more details](https://developer.mozilla.org/en-US/docs/Web/API/Window/load_event)

---

### LCP

**Largest Contentful Paint**

Measurement Unit: Milliseconds (ms)

Measures the time when the largest content block is rendered in the user viewport. The content may include images, 
background images, SVG, video, and text.

[more details](https://web.dev/articles/lcp)

---

### SI

**Speed Index**

Measurement Unit: Score (lower is better)

Measures how swiftly the contents of a page are visually populated. Technically, in a graph, it is represented 
by the area above the curve, which will approach 0 as the page loads faster.

[more details](https://developer.mozilla.org/en-US/docs/Glossary/Speed_index)

---

### TBT

**Total Blocking Time**

Measurement Unit: Milliseconds (ms)

Measures the time between [FCP](#FCP) and [TTI](#TTI) when the main thread was blocked for long enough to prevent input responsiveness. 
More specifically, it's the sum of the blocking time for each long task (>50 ms). For web frameworks, this time is 
usually consumed by virtual DOM renders and hydration.

[more details](https://web.dev/articles/tbt)

---

### TTI

**Time to Interactive**

Measurement Unit: Milliseconds (ms)

Measures the time when than at least for 5 seconds where weren't long tasks (>50ms) and
no more than two in-flight network GET requests.

[more details](https://web.dev/articles/tti)

---

### TTFB

**Time To First Byte**

Measurement Unit: Milliseconds (ms)

Measures when the first byte of data from the web server reaches the browser.

[more details](https://web.dev/articles/ttfb)

---
