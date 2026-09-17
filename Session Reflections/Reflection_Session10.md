# CSC360: Computer Graphics and Image Processing

## Reflection Journal - Session 10

---

### Session Metadata

- **Course Code:** CSC360
- **Course Name:** Computer Graphics and Image Processing
- **Student ID:** AU2420150
- **Session Number:** Session 10
- **Session Date:** September 08, 2026
- **Entry Date:** September 10, 2026

---

## 1. Overview

Session 10 opened with a roadmap of the course's five prescribed textbooks, then moved through several Core Java Volume I chapters (exceptions, generics, collections) before diving into the hardest topic of the session: how events propagate through JavaFX's scene graph. The session closed with CSS-driven layout behavior, the design intent behind common UI components, and Groups 9-12.

Key topics covered in this session include:

- **Course Textbook Roadmap:** Which of the five prescribed books to consult for which topic.
- **Exceptions, Generics, and Collections:** Core Java Volume I, Chapters 7-9.
- **View-Only Access:** Unmodifiable wrappers as a read/write separation pattern.
- **Event Propagation in JavaFX:** Capturing and bubbling phases through the scene graph.
- **Responsive Layouts:** GridPane, VBox, and HBox behavior under window resizing.
- **UI Component Design Intent:** Checkboxes vs. radio buttons, sliders, and dialog boxes as affordances.
- **Group Projects 9-12:** Mixed Swing/JavaFX UI, Master-Detail layout, real-time object styling, and JavaFX-to-DOM bridging via WebView.

---

## 2. Core Java Volume I - Chapters 7-9

- **Chapter 7 (Exceptions, Assertions, Logging):** Exceptions are how Java signals a runtime failure - thrown, caught, and handled before they crash the program.
- **Chapter 8 (Generic Programming):** Enables code that works across different types while preserving compile-time type safety. The angle-bracket syntax in `ArrayList<T>` comes directly from generics.
- **Chapter 9 (Java Collections Framework):** The standard toolbox of ready-made data structures - lists, sets, queues, and maps.

> [!TIP]
> **View-Only Access:**  
> Java supports exposing data as read-only through unmodifiable wrappers, which throw an exception the moment any code attempts to modify them. This is a direct library-level implementation of separating read operations from write operations - a concern that shows up constantly in data structures and algorithms design.

---

## 3. Event Propagation in JavaFX

Every user interaction - a click, key press, or scroll - generates an event. In JavaFX, that event does not go directly to its target. It travels through the scene graph in two distinct phases:

```
        CAPTURING (down)        BUBBLING (up)
Stage        |                       ^
  |          v                       |
Scene        |                       ^
  |          v                       |
Parent       |                       ^
  |          v                       |
Target ------+-----------------------+
        (event happens here)
```

- **Capturing phase:** The event travels from the root down to the target node. **Event filters** intercept during this downward pass.
- **Bubbling phase:** The event travels back up from the target to the root. **Event handlers** respond during this upward pass.

> [!IMPORTANT]
> **Why This Matters:**  
> Without a formal event hierarchy, every interaction in a complex, nested GUI would need to be wired manually - an approach that quickly becomes unmanageable. Understanding which phase a filter versus a handler operates in, and what happens when a node consumes an event mid-chain, is essential once a UI has overlapping or nested components.

---

## 4. Responsive Layouts (CSS & Layout Containers)

A well-designed layout reorganizes itself when a window is resized, shrunk, or stretched, rather than overflowing or breaking. JavaFX layout containers are built specifically around this:

| Container | Behavior |
|---|---|
| `GridPane` | Arranges children in a configurable row/column grid that adapts to available space |
| `VBox` | Stacks children vertically, redistributing space as the container resizes |
| `HBox` | Arranges children horizontally with the same responsive redistribution |

---

## 5. UI Components as Designed Affordances

Different UI widgets are not interchangeable - each signals a distinct interaction model before the user even reads a label:

- **Checkbox:** Independent, binary choices - any combination can be selected.
- **Radio button:** Mutually exclusive selection within a group - only one option at a time.
- **Slider:** Used when approximation matters more than precision (e.g., volume control - you want it to *sound right*, not read exactly 67%).
- **Dialog box:** Deliberately blocks user attention to force a response before a significant action proceeds.

> [!NOTE]
> **Affordance, Not Just Widget:**  
> Each component encodes a different mental model for the user. Choosing the wrong one for the task - a checkbox where a radio button belongs, or a numeric field where a slider belongs - creates friction even if the interface is otherwise functional.

---

## 6. Group Projects 9–12

| Group | Project | Core Concept |
|---|---|---|
| 9 | JavaFX UI mixing Swing and JavaFX components | Cross-toolkit UI integration |
| 10 | Master-Detail layout (click item → detail panel) | Progressive disclosure, avoiding loading everything at once |
| 11 | Real-time styling UI for a single geometric object | Live property binding (sliders, color pickers) |
| 12 | JavaFX button modifying a browser DOM via WebView/WebEngine | Embedding a browser engine inside a desktop app |

> [!TIP]
> **Master-Detail Rationale:**  
> A library website with ten million articles doesn't load all of them at once - it shows a few, with the rest reachable through search. Master-Detail applies the same principle: show a list, reveal detail on demand. Gmail's inbox-plus-reading-pane layout and most file managers follow this exact pattern.

---

## Key Takeaways

1. **Collections Framework Structure:** `Iterable` sits at the root, branching into `Collection` (-> `List`, `Set`, `Queue`) with `Map` as a separate key-value branch.
2. **View-Only Access Is a Design Pattern:** Unmodifiable wrappers give a concrete Java-library implementation of separating read and write access to shared data.
3. **Two-Phase Event Propagation:** JavaFX events travel down via capturing (filters intercept) and back up via bubbling (handlers respond) - getting this model wrong in a nested UI causes events to misfire or not fire at all.
4. **Layouts Should Adapt, Not Break:** `GridPane`, `VBox`, and `HBox` are built to reorganize children dynamically as window size changes.
5. **Sliders Suit Approximation:** Any interaction where the user cares about "does it feel right" rather than an exact value (volume, brightness, seek position) calls for a slider over a numeric input.
6. **UI Widgets Encode Affordances:** Checkboxes, radio buttons, sliders, and dialogs each signal a distinct interaction model before any text is read - matching the right widget to the task matters as much as functionality.

---

## Final Reflection

Session 10 was the point where JavaFX moved from "a listener responds to a click" to a formal, hierarchical model of how interaction actually flows through a UI. The capturing/bubbling structure was the hardest concept of the session precisely because my prior experience with event listeners had been flat — a button fires, a handler catches it, nothing more. Realizing that every event I'd already used (like the arrow-drawing mouse listener from Session 8) was secretly traveling through this two-phase scene-graph journey reframed a lot of earlier, simpler-seeming code. The UI components discussion reinforced a similar idea: what looks like a simple choice between a checkbox and a radio button is really a choice about what mental model you're handing the user, and that design intent doesn't show up until you look past the widget's surface behavior.
