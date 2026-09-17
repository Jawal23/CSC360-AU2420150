# CSC360: Computer Graphics and Image Processing

## Reflection Journal - Session 11

---

### Session Metadata

- **Course Code:** CSC360
- **Course Name:** Computer Graphics and Image Processing
- **Student ID:** AU2420150
- **Session Number:** Session 11
- **Session Date:** September 10, 2026
- **Entry Date:** September 12, 2026

---

## 1. Overview

Session 11 marked the course's transition from computer graphics (generating images from code) into image processing (working with and improving images that already exist). Before diving into that shift, the session covered a preview of Core Java Volume II, a statistics primer motivated by video streaming quality, the connection between XML and vector graphics, Server-Side vs. Client-Side Rendering, graphics storage at scale, and AWT's role as an abstraction layer.

Key topics covered in this session include:

- **Course Direction Shift:** Moving from graphics generation to image processing; Core Java Volume II preview.
- **Streaming vs. Downloading:** Why variance in delivery, not just average speed, determines playback quality.
- **Statistics Primer:** Mean, mode, median, variance, and standard deviation — population vs. sample.
- **SVG as XML:** Vector graphics stored as structured, human-readable markup.
- **SSR vs. CSR:** Where rendering work happens and the trade-offs of each.
- **Graphics Storage at Scale:** Relational databases vs. object storage (S3, GCS).
- **AWT:** Why it's called the "Abstract" Window Toolkit.
- **Group 7 Project Kickoff:** Taskwood - a three-level, JSON-persisted JavaFX task tree.

---

## 2. Course Direction: Graphics -> Image Processing

The professor framed the shift plainly: the first half of the course was about generating images from code (shapes, coordinates, mathematical descriptions). The second half is about working with images that already exist - extracting meaning from them or improving them. Core Java Volume II was previewed as the next reading, covering streams, networking, database connectivity, and concurrency.

---

## 3. Streaming vs. Downloading - Why Variance Matters

- **Downloading:** The entire file arrives before playback starts. Quality is consistent because everything is already local.
- **Streaming:** Content arrives in chunks; playback starts almost immediately, but experience quality depends on how reliably those chunks arrive.

> [!IMPORTANT]
> **Variance, Not Average Speed, Drives Buffering:**  
> If packet arrival times are consistent (low variance), the buffer stays full and playback is smooth. If delivery is erratic (high variance), the buffer empties before the next chunk arrives - causing buffering or a quality drop, even if the average speed is fast.

---

## 4. Statistics Primer

### Mean
- **Population Mean:** $$\mu = \frac{x_1 + x_2 + \dots + x_N}{N} = \frac{\sum_{i=1}^{N} x_i}{N}$$
- **Sample Mean:** $$\bar{x} = \frac{x_1 + x_2 + \dots + x_n}{n} = \frac{\sum_{i=1}^{n} x_i}{n}$$

### Mode
The most frequently occurring value. A dataset can be unimodal, multimodal, or have no mode at all.

### Median
The middle value in sorted order:
- If $n$ is odd: $$\text{Median} = \text{value at position } \frac{n + 1}{2}$$
- If $n$ is even: $$\text{Median} = \text{average of values at positions } \frac{n}{2} \text{ and } \left(\frac{n}{2} + 1\right)$$

*Example:* `[3, 7, 7, 9, 12]` $\rightarrow$ median = `7`. `[3, 7, 9, 12]` $\rightarrow$ median = $\frac{7 + 9}{2} = 8$.

### Variance
- **Population Variance:** $$\sigma^2 = \frac{\sum_{i=1}^{N} (x_i - \mu)^2}{N}$$
- **Sample Variance:** $$s^2 = \frac{\sum_{i=1}^{n} (x_i - \bar{x})^2}{n - 1}$$

> [!NOTE]
> **Bessel's Correction:**  
> Sample variance divides by $(n - 1)$ instead of $n$ because the sample mean is already the best estimate of the population mean — dividing by $n$ would slightly underestimate the true variance.

### Standard Deviation
- **Population SD:** $$\sigma = \sqrt{\sigma^2}$$
- **Sample SD:** $$s = \sqrt{s^2}$$

In the streaming context: high standard deviation in packet delivery times means an inconsistent network - even a fast average delivery speed still causes buffering if variability is high.

---

## 5. SVG as XML

SVG (Scalable Vector Graphics) is literally an XML text document: shapes become elements (`<circle>`, `<rect>`), their properties become attributes (position, size, color), and a renderer reads those tags to draw on screen.

> [!TIP]
> **Why This Matters:**  
> Because SVG is plain text, it can be transmitted over a network, stored in version control, indexed by search engines, and edited directly — none of which is possible with a raster image. This is a major reason SVG dominates icons, logos, and UI graphics on the web. It's the same "shapes as math, not pixels" idea from earlier in the course, just written out in a real file format.

---

## 6. SSR vs. CSR

- **SSR (Server-Side Rendering):** Client requests $\rightarrow$ Server renders everything $\rightarrow$ Sends complete content $\rightarrow$ Browser displays
- **CSR (Client-Side Rendering):** Client requests $\rightarrow$ Server sends HTML + JS $\rightarrow$ Browser runs JS $\rightarrow$ JS builds the UI

| Factor | SSR (Server-Side Rendering) | CSR (Client-Side Rendering) |
|---|---|---|
| **First-load speed** | Faster — complete HTML arrives ready | Slower — browser must download and run JS first |
| **SEO** | Better — content is pre-rendered and crawlable | Weaker — search engines may not execute JS |
| **Server costs** | Higher — server renders every request | Lower — server only sends static files |
| **Interactivity** | Lower — page reloads needed for updates | Higher — JS updates the UI without reloading |
| **Subsequent navigation** | Slower — each page needs a new server render | Faster — JS handles transitions locally |
| **Best suited for** | Content sites, news, landing pages | Web apps, dashboards, interactive tools |

---

## 7. Graphics Storage at Scale

- **Small volumes of small images:** A relational database works fine - either storing the image as binary data or a file path to disk.
- **Large volumes of high-resolution images:** Object storage systems (Amazon S3, Google Cloud Storage) are the standard, built for scale, high availability, and cost-effective large-file handling that relational databases can't match.

---

## 8. AWT — Abstract Window Toolkit

AWT provides a Java programming interface that abstracts over each OS's native windowing system. Creating an AWT button delegates the actual rendering to the OS - a Windows button looks like a Windows button, a macOS button looks like a macOS button. The "Abstract" layer is what hides those OS-specific details from the programmer.

---

## 9. Group 7 Project — Taskwood

This session marked the start of actual project work for my group. We defined Taskwood: a local-first JavaFX desktop application organizing personal and academic work into a three-level tree - **Workspaces $\rightarrow$ Projects $\rightarrow$ Tasks**.

- Every node (Workspace, Project, or Task) is fully editable through a dedicated form panel.
- All data auto-persists to a local JSON file and reloads on the next launch.
- This session's contribution was planning: naming the app, agreeing on the hierarchy, and mapping each course requirement (tree structure, editing, persistence) to a concrete design decision.

---

## Key Takeaways

1. **Course Pivot:** Graphics (generating images) is giving way to image processing (working with existing images) as the course's second half.
2. **Variance Drives Streaming Quality:** Inconsistent packet delivery causes buffering even when average speed is fast - the statistical measure that matters is variance, not the mean.
3. **SVG = XML for Shapes:** Vector graphics stored as SVG are plain-text, structured documents - lightweight, scalable, and transmittable like any other file.
4. **SSR vs. CSR Is a Trade-off, Not a Winner:** SSR favors fast first loads and SEO; CSR favors fast subsequent interactions. The right choice depends on the use case.
5. **Object Storage for Scale:** Large volumes of high-resolution images belong in systems like S3 or GCS, not relational databases.
6. **AWT Abstracts the OS:** The "Abstract" in Abstract Window Toolkit refers to the Java layer that hides OS-specific rendering details from the programmer.

---

## Final Reflection

Session 11 was full of connections that weren't obvious until the professor drew them out explicitly. The variance discussion gave formal vocabulary to something I already understood intuitively from competitive gaming (jitter causing lag spikes even with good average ping). The SVG-as-XML explanation retroactively clarified the raster-vs-vector distinction from much earlier in the course - the "mathematical description" of a shape isn't an abstract idea, it's a literal XML tag with attributes. And realizing that SSR is essentially what a headless server does - process everything remotely and hand over a finished result - tied two previously separate topics (networking and rendering architecture) into one coherent idea. Starting the actual build for Taskwood also made the tree-of-objects requirement concrete for the first time: what had been an abstract assignment description is now a specific three-level hierarchy with a name and a persistence plan behind it.
