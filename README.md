# Web Performance Handbook

<img align="right" width="100" height="100" title="Logo"
src="./static/images/logo.png" />

This handbook helps to quickly understand the topic and start improving performance. It contains a metrics glossary, 
a compilation of useful tools, and a catalog of necessary materials. 

I really want to share proven knowledge to make the web even better and faster. Support and bookmark the project by giving it a star! ⭐

## Table of Contents

- [Web Performance Handbook](#web-performance-handbook)
  - [Table of Contents](#table-of-contents)
  - [Tools](#tools)
    - [Global Stats](#global-stats)
    - [Treo — Site Speed](#treo--site-speed)
    - [CrUX Vis](#crux-vis)
    - [PageSpeed Insights](#pagespeed-insights)
    - [WebPageTest](#webpagetest)
    - [Lighthouse](#lighthouse)
    - [DevTools Performance](#devtools-performance)
  - [Monitoring](#monitoring)
    - [LHCI Server (open-source)](#lhci-server-open-source)
    - [DebugBear (paid)](#debugbear-paid)
    - [web-vitals (library)](#web-vitals-library)
  - [AI Tools](#ai-tools)
    - [MCP Servers](#mcp-servers)
      - [Chrome DevTools MCP (Google)](#chrome-devtools-mcp-google)
    - [AI in Browser DevTools](#ai-in-browser-devtools)
      - [Chrome DevTools AI Assistance (Gemini)](#chrome-devtools-ai-assistance-gemini)
  - [Optimizing Hydration](#optimizing-hydration)
      - [Disable Hydration](#disable-hydration)
      - [Server Components](#server-components)
  - [Optimizing Page Load Speed](#optimizing-page-load-speed)
    - [Image Proxy: Use avif / webp / progressive jpeg](#image-proxy-use-avif--webp--progressive-jpeg)
    - [Data Compression with brotli and zstd](#data-compression-with-brotli-and-zstd)
    - [Fetch Priority](#fetch-priority)
    - [Speculation Rules: Prefetch and Prerender Next Pages](#speculation-rules-prefetch-and-prerender-next-pages)
    - [Back/Forward Cache](#backforward-cache)
  - [Optimizing Bundle](#optimizing-bundle)
    - [Tools to Analyze](#tools-to-analyze)
      - [Statoscope](#statoscope)
      - [Bundle Analyzer](#bundle-analyzer)
      - [Rsdoctor](#rsdoctor)
      - [Rollup Plugin Visualizer](#rollup-plugin-visualizer)
      - [Why?](#why)
    - [Webpack Alias: Remove 3-rd Party Code from Bundle](#webpack-alias-remove-3-rd-party-code-from-bundle)
    - [Lazy Code Loading: On Viewport, on Interaction](#lazy-code-loading-on-viewport-on-interaction)
    - [Deduplication](#deduplication)
    - [Webpack: Magic Comments on Imports](#webpack-magic-comments-on-imports)
  - [React Tools](#react-tools)
    - [Why Did You Render](#why-did-you-render)
    - [React Scan](#react-scan)
    - [React Compiler](#react-compiler)
    - [React Performance Tracks](#react-performance-tracks)
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
    - [LoAF](#loaf)
    - [LCP](#lcp)
    - [SI](#si)
    - [Soft Navigations](#soft-navigations)
    - [TBT](#tbt)
    - [TTI](#tti)
    - [TTFB](#ttfb)

---

## Tools

### Global Stats

Browser market share worldwide. This allows you to see device and browser usage in specific regions.

[link](https://gs.statcounter.com/browser-market-share/)

### Treo — Site Speed

How to view historical performance data of real users?

Allows viewing annual reports for websites based on Lighthouse and CrUX (Chrome User Experience Report) metrics. 
Filters can also be set, such as internet connection speed, location, and device. Uses real user data. Very useful for observing trends 
and metrics specific to certain user types.

[link](https://treo.sh/sitespeed)

### CrUX Vis

The official Google tool to view CrUX data for an origin or a URL. Shows how [LCP](#lcp), [INP](#inp), [CLS](#cls) 
and other metrics changed over time, split by device. It replaced the CrUX Dashboard (Looker Studio), which was 
retired at the end of November 2025.

[link](https://cruxvis.withgoogle.com/)

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

Since Lighthouse 13 (October 2025), most performance audits are replaced by "insights". They are the same insights 
that you see in the DevTools Performance panel.

[link](https://developer.chrome.com/docs/lighthouse/overview)

### DevTools Performance

Record and analyze the performance of a page. It allows you to see the loading process in detail, including the
loading, scripting, rendering, and painting phases. It also provides a timeline of events, which can be used to
understand what is happening under the hood. For instance, you can see how long the hydration takes.

When you open the panel, it shows live metrics: [LCP](#lcp), [INP](#inp), and [CLS](#cls) of your local session. 
You can compare them with real user data from CrUX. It replaced the Web Vitals extension, which is no longer supported 
since Chrome 132 (January 2025).

[link](https://developer.chrome.com/docs/devtools/performance/overview)

Hint:\
By default, it's challenging to understand what's really happening because of tons of anonymous events. 
Add your own tracks to the timeline with the [extensibility API](https://developer.chrome.com/docs/devtools/performance/extension). 
For React apps, use [React Performance Tracks](#react-performance-tracks).

---

## Monitoring

### LHCI Server (open-source)

Allows you to store historical performance data and see differences between builds. It integrates with CI/CD processes.

[GitHub link](https://github.com/GoogleChrome/lighthouse-ci/blob/main/docs/server.md)

### DebugBear (paid)

A tool for monitoring web performance and Lighthouse metrics. It can be used to set up alerts for performance regressions.

[link](https://www.debugbear.com/)

### web-vitals (library)

A small library from Google to collect [LCP](#lcp), [INP](#inp), [CLS](#cls), [FCP](#fcp) and [TTFB](#ttfb) from 
real users. Send them to your analytics and build your own monitoring. The attribution build shows what caused a 
bad score. Version 6 (July 2026) can also report metrics for [soft navigations](#soft-navigations) with the 
`reportSoftNavs: true` option.

```js
import { onLCP, onINP, onCLS } from 'web-vitals';

onLCP(console.log);
onINP(console.log);
onCLS(console.log);
```

[GitHub link](https://github.com/GoogleChrome/web-vitals)

---

## AI Tools

### MCP Servers

Tools that let AI coding agents (Claude, Cursor, Copilot, Gemini) run performance audits via 
[Model Context Protocol](https://modelcontextprotocol.io/).

#### Chrome DevTools MCP (Google)

Official Google MCP server. Lets AI agents control a live Chrome browser: record performance traces, 
analyze Core Web Vitals (LCP, CLS, INP), inspect network requests, take screenshots, and fetch CrUX 
field data. The most comprehensive option for AI-driven performance analysis.

[GitHub link](https://github.com/ChromeDevTools/chrome-devtools-mcp)

```json
{
  "mcpServers": {
    "chrome-devtools": {
      "command": "npx",
      "args": ["-y", "chrome-devtools-mcp@latest"]
    }
  }
}
```

### AI in Browser DevTools

#### Chrome DevTools AI Assistance (Gemini)

Google's Gemini integrated directly into Chrome DevTools. Helps investigate page performance, analyze 
traces, debug LCP/CLS/INP issues, explain network request failures, and suggest fixes. Works across 
Performance, Network, Sources, and Elements panels. Requires Chrome with a Google account.

[link](https://developer.chrome.com/docs/devtools/ai-assistance)

## Optimizing Hydration

#### Disable Hydration

React has a trick that allows you to disable hydration for a component. The server will render it once, then send an HTML that won't be hydrated. Perfect for static content.

```jsx
<div suppressHydrationWarning dangerouslySetInnerHTML={{ __html: "" }}/>
```

#### Server Components

Server Components render only on the server. Their code is not sent to the browser and they are not hydrated.

[more about them](https://nextjs.org/docs/app/getting-started/server-and-client-components)

---

## Optimizing Page Load Speed

### Image Proxy: Use avif / webp / progressive jpeg

To improve LCP and reduce traffic volume, you can use image proxies or CDNs. They will reformat, resize, and optimize your images on the fly, and cache them immediately.

Possible solutions:
1. Cloudflare Images
2. Uploadcare
3. [imgproxy](https://github.com/imgproxy/imgproxy)
4. Implement manually: [Good starting point](https://github.com/Danilqa/image-proxy-service).

JPEG XL is back. It works in Chrome 155+, Firefox 158+ and Safari 17+. Serve it with a fallback to avif / webp 
for older browsers.

[JPEG XL in Chrome](https://developer.chrome.com/blog/jpeg-xl-in-chrome)

### Data Compression with brotli and zstd

Reduce the size of static files by 15-17% (the exact number is better to calculate using your own resources). The best results can be achieved using brotli with compression level 11. However, the compression time is longer than with gzip (level 9). Avoid using it on-the-fly and only use pre-compressed or cached versions.

[Comparison table](https://www.gstatic.com/b/brotlidocs/brotli-2015-09-22.pdf)

zstd is another option. It compresses fast, which makes it a good fit for on-the-fly compression. It works in 
all major browsers since Safari 26.3 (February 2026).

Compression dictionaries go even further. The browser keeps the old version of a file, and the server uses it as 
a dictionary to compress the new version. The response becomes much smaller. It's still experimental and works by 
default only in Chromium-based browsers.

[Compression dictionary transport](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/Compression_dictionary_transport)

### Fetch Priority

Tell the browser which resources are more important. For example, raise the priority of the [LCP](#lcp) image 
and lower it for images that are not visible yet. Works in all major browsers since October 2024.

```html
<img src="hero.avif" fetchpriority="high" alt="">
```

[link](https://web.dev/articles/fetch-priority)

### Speculation Rules: Prefetch and Prerender Next Pages

Load the next page before the user clicks a link. With prerender, the browser renders the whole page in the 
background, and the navigation feels instant. Prerender works only in Chromium-based browsers for now. Safari and 
Firefox are adding prefetch. Browsers without support ignore the rules.

```html
<script type="speculationrules">
{
  "prerender": [{ "where": { "href_matches": "/*" }, "eagerness": "moderate" }]
}
</script>
```

[link](https://developer.mozilla.org/en-US/docs/Web/API/Speculation_Rules_API)

### Back/Forward Cache

The browser can keep a page in memory when the user leaves it. When the user goes back, the page shows instantly. 
Some things block it, for example `unload` event handlers. Use `pagehide` instead. To see what blocks it on your 
page, open DevTools → Application → Back/forward cache.

[link](https://web.dev/articles/bfcache)

---

## Optimizing Bundle

### Tools to Analyze

#### Statoscope

Builds a detailed report of your bundle. Separates scripts from initial loading and asynchronous loading.

[Github Link](https://github.com/statoscope/statoscope)

#### Bundle Analyzer

[Github Link](https://github.com/webpack-contrib/webpack-bundle-analyzer)

#### Rsdoctor

A build analyzer for Rspack. Shows the bundle content, duplicated packages, and which loaders and plugins slow down 
the build. For webpack, use Rsdoctor 1.x.

[link](https://rsdoctor.rs/)

#### Rollup Plugin Visualizer

A bundle analyzer for Vite and Rollup. Shows the bundle as a treemap, sunburst, flamegraph, or network graph.

[Github Link](https://github.com/btd/rollup-plugin-visualizer)

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

### React Scan

Finds unnecessary re-renders and highlights them right on the page. Works without code changes: add a script tag 
or set it up with `npx react-scan@latest init`.

[link](https://github.com/aidenybai/react-scan)

### React Compiler

Memoizes components and values automatically at build time. You don't need to write `useMemo`, `useCallback` 
and `memo` by hand. Most unnecessary re-renders go away. Stable since version 1.0 (October 2025).

[link](https://react.dev/blog/2025/10/07/react-compiler-1)

### React Performance Tracks

React 19.2 adds its own tracks to the DevTools Performance panel. The Scheduler track shows what React is working 
on and with which priority. The Components track shows which components render and how long it takes. Available 
in development and profiling builds.

[link](https://react.dev/reference/dev-tools/react-performance-tracks)

### React DevTools Profiler

Shows the time spent rendering each component and how many times it was rendered. To observe why it was rendered, 
enable the "Record why each component rendered while profiling" flag in the settings.

[link](https://chromewebstore.google.com/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi)

---

## Learning Resources

### Browser Rendering Optimization Course

Provides a solid basis for understanding how a browser renders a document and what happens behind the scenes.

[link](https://www.udacity.com/course/browser-rendering-optimization--ud860)

### Web App Performance Course

Reveals many subtleties and working practices about optimization that are not usually written about. 

[link](https://master.dev/courses/web-app-performance/)

---

## Metrics

This is a list of the most common metrics which may appear in articles, DevTools, Lighthouse, and other
various tools for working with web performance. Everything is sorted in the alphabetical order.

The factual data is primarily sourced from MDN, web.dev and w3c, however the short description has been rewritten and enhanced.

Core Web Vitals are [LCP](#lcp), [INP](#inp) and [CLS](#cls). Good values (for 75% of page visits):

| Metric | Good | Poor |
|--------|------|------|
| LCP | ≤ 2.5 s | > 4 s |
| INP | ≤ 200 ms | > 500 ms |
| CLS | ≤ 0.1 | > 0.25 |

LCP and INP work in all major browsers since Safari 26.2 (December 2025). CLS still works only in Chromium-based 
browsers.


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

**First Input Delay** (Deprecated)

> Deprecated: FID was replaced by [INP](#inp) as a Core Web Vital on March 12, 2024. Chrome stopped reporting 
> FID in September 2024, including the Web Vitals extension, PageSpeed Insights, and CrUX.

Measurement Unit: Milliseconds (ms)

Measures the time it takes for the browser to respond to a user's first interaction. This interaction can 
include clicks, hovers, touches, and other user events. Unlike [INP](#inp), FID only measured the delay of the 
first interaction, not all interactions throughout the page lifecycle.

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

### LoAF

**Long Animation Frames**

Measurement Unit: Milliseconds (ms)

Detects frames that take longer than 50ms, providing script-level attribution for what caused the delay. 
It is the successor to the Long Tasks API and the primary tool for debugging [INP](#inp) issues. Unlike Long Tasks, 
LoAF shows which scripts ran, how long each took, and includes rendering phases. Supported in Chrome 123+ and Edge 123+.

[more details](https://developer.chrome.com/docs/web-platform/long-animation-frames)

### LCP

**Largest Contentful Paint**

Measurement Unit: Milliseconds (ms)

Measures the time when the largest content block is rendered in the user viewport. The content may include images, 
background images, SVG, video, and text.

LCP can be broken down into four sub-parts for targeted optimization:
1. [TTFB](#ttfb) — time to first byte of HTML
2. Resource Load Delay — time from TTFB until the browser starts loading the LCP resource
3. Resource Load Duration — time to download the LCP resource itself
4. Element Render Delay — time from when the resource is loaded until the LCP element is painted

[more details](https://web.dev/articles/lcp) | [optimizing sub-parts](https://web.dev/articles/optimize-lcp)

### SI

**Speed Index**

Measurement Unit: Score (lower is better)

Measures how swiftly the contents of a page are visually populated. Technically, in a graph, it is represented 
by the area above the curve, which will approach 0 as the page loads faster.

[more details](https://developer.mozilla.org/en-US/docs/Glossary/Speed_index)

### Soft Navigations

**Soft Navigations and Interaction Contentful Paint**

Measurement Unit: Milliseconds (ms)

In single-page apps, the URL changes without a full page load. Before, [LCP](#lcp), [INP](#inp) and [CLS](#cls) 
were tied to the first page load. Since Chrome 151 (July 2026), the browser detects these "soft navigations". 
Now you can measure metrics for each of them. The new `interaction-contentful-paint` entry shows when new content is 
painted after an interaction. Works only in Chromium-based browsers.

[more details](https://developer.chrome.com/docs/web-platform/soft-navigations)

### TBT

**Total Blocking Time**

Measurement Unit: Milliseconds (ms)

Measures the time between [FCP](#FCP) and [TTI](#TTI) when the main thread was blocked for long enough to prevent input responsiveness. 
More specifically, it's the sum of the blocking time for each long task (>50 ms). For web frameworks, this time is 
usually consumed by virtual DOM renders and hydration.

[more details](https://web.dev/articles/tbt)

### TTI

**Time to Interactive** (Deprecated)

> Deprecated: TTI was removed from Lighthouse scoring in Lighthouse 10 (February 2023). It was too sensitive 
> to outliers and long tasks. Use [TBT](#tbt) as the lab proxy for main-thread blocking instead.

Measurement Unit: Milliseconds (ms)

Measures the time when the page starts a quiet window of at least 5 seconds: no long tasks (>50ms) and
no more than two in-flight network GET requests.

[more details](https://web.dev/articles/tti)

### TTFB

**Time To First Byte**

Measurement Unit: Milliseconds (ms)

Measures when the first byte of data from the web server reaches the browser.

[more details](https://web.dev/articles/ttfb)
