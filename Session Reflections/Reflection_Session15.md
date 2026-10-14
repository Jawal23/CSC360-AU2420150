# CSC360: Computer Graphics and Image Processing

## Reflection Journal - Session 15

---

### Session Metadata

- **Course Code:** CSC360
- **Course Name:** Computer Graphics and Image Processing
- **Student ID:** AU2420150
- **Session Number:** Session 15
- **Session Date:** October 01, 2026
- **Entry Date:** October 07, 2026

---

## 1. Overview

Session 15 opened with mock evaluation presentations by a few selected groups, then moved into generic programming and JavaFX shape abstraction. The mock round clarified what the final evaluation looks like, and the programming material tied directly back to code reuse and to the project itself.

Key topics covered in this session include:

- **Mock Presentations:** A live, interactive feedback round showing what the project evaluation will look like.
- **Functionality vs. Features:** Why a reliable core outweighs a long feature list.
- **Generic Programming and Reusable Code:** Making the type a parameter so logic lives in one place.
- **JavaFX Shape Hierarchy:** An abstract `Shape` class with concrete subclasses.
- **Two Drawing Models:** Scene graph shapes (retained mode) vs. `Canvas` + `GraphicsContext` (immediate mode).

---

## 2. Mock Presentations and Evaluation Format

A few groups presented to show everyone what the real evaluation would feel like. It was an active feedback round: the presenting group, the faculty, and the class all contributed. The discussion covered assumptions groups had made about the format, what the faculty actually expects, and how to make a presentation communicate the project clearly rather than demoing features one after another.

### Functionality vs. Features

| Term | Meaning |
|---|---|
| **Functionality** | What the software *does*: whether it works correctly and fulfils its core purpose |
| **Features** | Extras built on top of that core |

> [!IMPORTANT]
> **Evaluation Weight:**  
> Functionality carries more weight than features. A project that does fewer things reliably is judged more favourably than one with many features that break during the demo. This reframes what "done" means: not how much it can do, but how well the core works end to end.

---

## 3. Generic Programming and Reusable Code

If you are writing nearly the same class or method twice just because the types differ, the approach needs fixing. Generics are Java's solution: make the type itself a parameter, write the logic once, and let the compiler adapt it for each type used.

```java
// Without generics: one box per type
class IntBox    { int value;    }
class StringBox { String value; }

// With generics: one definition for every type
class Box<T> { T value; }

Box<Integer> a = new Box<>();
Box<String>  b = new Box<>();
```

The Java Collections Framework (`List`, `Set`, `Map`) is the clearest example: the logic for adding, removing, and traversing is identical regardless of what the collection holds.

> [!TIP]
> **Why Reuse Matters Beyond Line Count:**  
> Keeping logic in one place means a fix or improvement applies everywhere the code is used, instead of having to track down every near-identical copy. It is also easier to test and maintain.

---

## 4. JavaFX Shape Abstraction

`Shape` in JavaFX is an abstract class. Concrete types such as `Rectangle`, `Circle`, `Line`, and `Ellipse` extend it and inherit common properties: `fill`, `stroke`, `strokeWidth`, and `opacity`.

```
              Shape (abstract)
                    |
   +----------+-----+------+----------+
   |          |            |          |
Rectangle   Circle        Line     Ellipse
```

Because all shapes share the same base type, a single `List<Shape>` can hold different shapes, and a loop can apply a property change to all of them without knowing each concrete type. This is polymorphism from the earlier OOP sessions applied directly to a visual context.

### Two Separate Drawing Models

| Aspect | Scene Graph Shapes | `Canvas` + `GraphicsContext` |
|---|---|---|
| Mode | Retained | Immediate |
| What exists | Persistent objects in the scene tree | A pixel buffer; nothing retained as an object |
| How you use it | Set properties; JavaFX handles rendering | Issue commands like `fillRect`, `strokeOval` |
| Observable properties | Yes | No |
| Closest older equivalent | New model | Resembles `Graphics2D` from Sessions 4 and 5 |

> [!NOTE]
> **The Confusing Part:**  
> The `Shape` hierarchy itself is a plain inheritance tree. The difficulty is that JavaFX supports two independent drawing models, and the session alone did not fully explain when to use which. As a rule of thumb, scene graph shapes suit interactive, selectable, individually animated objects, while `Canvas` suits large numbers of primitives or pixel-level drawing where per-object overhead would hurt.

---

## 5. Real-World Context

- **Generics:** The whole Collections framework is built on them, and frameworks such as Spring use generic type parameters throughout their data-access and dependency-injection layers. A sorting algorithm written once as a generic method beats ten type-specific copies.
- **Shape abstraction:** Game engines, vector editors, and CAD tools share a common base type for drawable objects (position, rotation, opacity), so a render loop can iterate over them without knowing their concrete types.

---

# Key Takeaways

1. **Functionality Over Features:** For evaluation, a reliably working core matters more than the number of features.
2. **Generics Remove Duplication:** Making the type a parameter lets one implementation cover all cases, so fixes apply everywhere.
3. **Reuse Is About Maintenance:** Keeping logic in one place makes it easier to test, maintain, and improve.
4. **Shape Is an Abstract Base:** Concrete shapes inherit `fill`, `stroke`, `strokeWidth`, and `opacity`, enabling polymorphic handling through a `List<Shape>`.
5. **Two Drawing Models Coexist:** Scene graph shapes are retained and property-based; `Canvas` with `GraphicsContext` is immediate-mode with no persistent objects.
6. **Documentation Helps Evaluation:** Good documentation lets an evaluator understand the project without reading the source.

---

## Final Reflection

The most useful moment of this session was the functionality-versus-features distinction. I had been judging our project by the list of things it can do, but the professor reframed it as whether it works correctly from start to finish. That changed what I want to check before the evaluation: reliability first, extras second. On the technical side, generics clicked because the problem is easy to picture (one container written per type), while the two JavaFX drawing models were the real struggle. Linking `GraphicsContext` back to the `Graphics2D` approach from Sessions 4 and 5 helped, and I plan to experiment with both models in small test programs to build a feel for when each is the better choice.
