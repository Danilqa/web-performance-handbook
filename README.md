# Web Performance Handbook

<img align="right" width="100" height="100" title="Logo"
src="./static/images/logo.png" />

This handbook helps to quickly understand the topic and start improving performance. It contains a metrics glossary, 
a compilation of useful tools, and a catalog of necessary materials.

Support and bookmark the project by giving it a star! ⭐

## Table of Contents

- [Web Performance Handbook](#web-performance-handbook)
  - [Table of Contents](#table-of-contents)
  - [Tools](#tools)
    - [Treo — Site Speed](#treo--site-speed)
    - [Web Vitals (extension)](#web-vitals-extension)
    - [PageSpeed Insights](#pagespeed-insights)
    - [WebPageTest](#webpagetest)
    - [Lighthouse](#lighthouse)
    - [DevTools Performance (with experimental features)](#devtools-performance-with-experimental-features)
  - [Monitoring](#monitoring)
    - [LHCI Server (open-source)](#lhci-server-open-source)
    - [DebugBear (paid)](#debugbear-paid)
  - [Optimizing Bundle](#optimizing-bundle)
    - [Tools to Analyze](#tools-to-analyze)
      - [Statoscope](#statoscope)
      - [Bundle Analyzer](#bundle-analyzer)
      - [Why?](#why)
    - [Webpack Alias: Remove 3-rd Party Code from Bundle](#webpack-alias-remove-3-rd-party-code-from-bundle)
    - [Lazy Code Loading: On Viewport, on Interaction](#lazy-code-loading-on-viewport-on-interaction)
    - [Deduplication](#deduplication)
    - [Webpack: Magic Comments on Imports](#webpack-magic-comments-on-imports)
  - [React Tools](#react-tools)
    - [Why Did You Render](#why-did-you-render)
    - [React DevTools Profiler](#react-devtools-profiler)
  - [Learning Resources](#learning-resources)
    - [Browser Rendering Optimization Course](#browser-rendering-optimization-course)
    - [Web App Performance Course](#web-app-performance-course)
  - [Metrics](#metrics)
    - [CLS](#cls)
    - [DCL](#dcl)
    - [FCP](#fcp)
    - [FID](#fid)
    - [FP](#fp)
    - [INP](#inp)
    - [L](#l)
    - [LCP](#lcp)
    - [SI](#si)
    - [TBT](#tbt)
    - [TTI](#tti)
    - [TTFB](#ttfb)

---

## Tools

### Treo — Site Speed

How to view historical performance data of real users?

Allows viewing annual reports for websites based on Light House and CrUX (Chrome User Experience Report) metrics. 
Filters can also be set, such as internet connection speed, location, and device. Uses real user data. Very useful for observing trends 
and metrics specific to certain user types.

[link](https://treo.sh/sitespeed)

### Web Vitals (extension)

Collect metrics such as [**INP**](#INP), [LCP](#LCP), [CLS](#CLS), [FIP](#FIP), [FCP](#FCP), and [TTFB](#TTFB) in real-time and easily view them in a popup. 
Enabling logging in options can assist in debugging [INP](#INP).

[link](https://chrome.google.com/webstore/detail/web-vitals/ahfhijdlegdabablpippeagghigmibma/)

### PageSpeed Insights

Allows you to conduct Lighthouse performance tests remotely, in a more realistic environment. Can be used for taking 
more objective measurements, as computer powers vary among teammates. Especially, developers tend to have significantly 
more powerful computers than the general market. Also, for popular websites, it provides data from the CrUX report.

[link](https://pagespeed.web.dev)

### WebPageTest

The same as previous, but on steroids. Allows you to set up a testing environment: location, browser, its available 
functionality, connection speed, etc. Can record a video of the loading process, providing more understandable and 
detailed reports on the webpage loading process and requests.

[link](https://www.webpagetest.org/)

### Lighthouse

A tool designed for assessing the quality of a web page, focusing on core vitals metrics, SEO, and accessibility.
It is built into Chrome DevTools and can be also used as a CLI tool, making it especially useful for measuring 
performance during CI processes. Additionally, it offers practical suggestions to enhance the quality and loading 
speed of the page.

### DevTools Performance (with experimental features)

Record and analyze the performance of a page. It allows you to see the loading process in detail, including the
loading, scripting, rendering, and painting phases. It also provides a timeline of events, which can be used to
understand what is happening under the hood. For instance, you can see how long the hydration takes.

Hint:\
Enable the experimental "timeline-*" features in DevTools settings to see more information about events. It's especially 
useful for React apps. By default, it's challenging to understand what's really happening because of tons of anonymous
events.

---

## Monitoring

### LHCI Server (open-source)

Allows you to store historical performance data and see differences between builds. It integrates with CI/CD processes.

[GitHub link](https://github.com/GoogleChrome/lighthouse-ci/blob/main/docs/server.md)

### DebugBear (paid)

A tool for monitoring web performance and Lighthouse metrics. It can be used to set up alerts for performance regressions.

[link](https://www.debugbear.com/)

---

## Optimizing Bundle

### Tools to Analyze

#### Statoscope

Built elaborated report of your bundle. Separates scripts from initial loading and asynchronous loading.

[Github Link](https://github.com/statoscope/statoscope)

#### Bundle Analyzer

[Github Link](https://github.com/webpack-contrib/webpack-bundle-analyzer)

#### Why?

Identifies why a package has been installed. Especially useful for transitive dependencies.

```sh
yarn why
pnpm why
```

### Webpack Alias: Remove 3-rd Party Code from Bundle

```js
const mockEmptyModule = path.resolve('./mock-empty-module.js');
// ...
config.resolve.alias['reactstrap/lib/Carousel.js'] = mockEmptyModule;
```

### Lazy Code Loading: On Viewport, on Interaction

The key principle is to avoid including code in the initial load that can be downloaded later. Instead, download it when a user is about to view it in their viewport, during idle time, or at the start of an interaction. 

For React, combine dynamic module import with Suspense.

[real world example](https://dev.to/dsitdikov/my-journey-to-accelerate-load-times-in-heavy-frontend-30c7/)

### Deduplication

If it's safe, align the minor versions of installed modules that are duplicated.

```sh
yarn dedupe
npm dedupe
pnpm dedupe
```

### Webpack: Magic Comments on Imports

Allows you to rename chunks, regroup, prefetch lazy chunks and more.

[link](https://webpack.js.org/api/module-methods/#magic-comments)

---

## React Tools

### Why Did You Render

A tool for detecting unnecessary re-renders. It can be used to find components that are re-rendered too often. Write 
messages to the console.

[link](https://github.com/welldone-software/why-did-you-render)

### React DevTools Profiler

Shows the time spent rendering each component and how many times it was rendered. To observe why it was rendered, 
enable the "Record why each component rendered while profiling" flag in the settings.

[link](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi)

---

## Learning Resources

### Browser Rendering Optimization Course

Provides a solid basis for understanding how a browser renders a document and what happens behind the scenes.

[link](https://www.udacity.com/course/browser-rendering-optimization--ud860)

### Web App Performance Course

Reveals many subtleties and working practices about optimization that are not usually written about. 

[link](https://frontendmasters.com/courses/web-app-performance/)

---

## Metrics

This is a list of the most common metrics which may appear in articles, DevTools, Lighthouse, and other
various tools for working with web performance. Everything is sorted in the alphabetical order.

The factual data is primarily sourced from MDN, web.dev and w3c, however the short description has been rewritten and enhanced.


### CLS

**Cumulative Layout Shift**

Measurement Unit: Score (lower is better)

Shows how often users experience unexpected changes in the layout. It measures the 
instability of elements and their overall impact. For example, the banner element changes its height 
during the loading process, which causes a shift in the elements below.

[more details](https://web.dev/articles/cls)

### DCL

**DOMContentLoaded**

Measurement Unit: Milliseconds (ms)

Refers to the moment in a webpage's loading process when the DOM is completely parsed. And all deferred scripts have 
downloaded and executed. It doesn't wait for resources.

[more details](https://developer.mozilla.org/en-US/docs/Web/API/Document/DOMContentLoaded_event)

### FCP

**First Contentful Paint**

Measurement Unit: Milliseconds (ms)

Measures the time it takes for first bit of any actual content on a page to become visible on the screen. 
This includes text, images, background images, SVG elements, and non-white canvas elements.

[more details](https://web.dev/articles/fcp)

### FID

**First Input Delay**

Measurement Unit: Milliseconds (ms)

Measures the time it takes for the browser to respond to a user's first interaction. This interaction can 
include clicks, hovers, touches, and other user events.

[more details](https://web.dev/articles/fid)

### FP

**First Paint**

Measurement Unit: Milliseconds (ms)

Marks the first time the browser renders anything visually different from the default background color of the body.

### INP

**Interaction to Next Paint**

Measurement Unit: Milliseconds (ms)

Measures the time it takes for the browser to paint the next frame after a user interaction. 

[more details](https://web.dev/articles/inp)

### L

**On Load**

Measurement Unit: Milliseconds (ms)

Measures the time when the entire page and its resources are fully loaded. 
It includes all dependent resources: stylesheets, scripts, iframes, and images.

[more details](https://developer.mozilla.org/en-US/docs/Web/API/Window/load_event)

### LCP

**Largest Contentful Paint**

Measurement Unit: Milliseconds (ms)

Measures the time when the largest content block is rendered in the user viewport. The content may include images, 
background images, SVG, video, and text.

[more details](https://web.dev/articles/lcp)

### SI

**Speed Index**

Measurement Unit: Score (lower is better)

Measures how swiftly the contents of a page are visually populated. Technically, in a graph, it is represented 
by the area above the curve, which will approach 0 as the page loads faster.

[more details](https://developer.mozilla.org/en-US/docs/Glossary/Speed_index)

### TBT

**Total Blocking Time**

Measurement Unit: Milliseconds (ms)

Measures the time between [FCP](#FCP) and [TTI](#TTI) when the main thread was blocked for long enough to prevent input responsiveness. 
More specifically, it's the sum of the blocking time for each long task (>50 ms). For web frameworks, this time is 
usually consumed by virtual DOM renders and hydration.

[more details](https://web.dev/articles/tbt)

### TTI

**Time to Interactive**

Measurement Unit: Milliseconds (ms)

Measures the time when than at least for 5 seconds where weren't long tasks (>50ms) and
no more than two in-flight network GET requests.

[more details](https://web.dev/articles/tti)

### TTFB

**Time To First Byte**

Measurement Unit: Milliseconds (ms)

Measures when the first byte of data from the web server reaches the browser.

[more details](https://web.dev/articles/ttfb)
