# CSC360: Computer Graphics and Image Processing

## Reflection Journal - Session 14

---

### Session Metadata

- **Course Code:** CSC360
- **Course Name:** Computer Graphics and Image Processing
- **Student ID:** AU2420150
- **Session Number:** Session 14
- **Session Date:** September 29, 2026
- **Entry Date:** October 05, 2026

---

## 1. Overview

Session 14 was the last in-class session dedicated to project work. There was no lecture; the professor moved between groups to review visual interfaces, check progress, and clear up doubts before final submission. For our group, the project was nearly complete, so the session went into settling one last feature (a splash screen) and starting the README and Wiki.

Key topics covered in this session include:

- **Design-Review Style Check-Ins:** Group-by-group walkthroughs instead of a lecture.
- **Final Feature Decision:** Agreeing on a splash screen as the last addition.
- **Splash Screen in JavaFX:** The `Preloader` approach and the simpler separate-`Stage` alternative.
- **UI Rework Now Visible:** The redesign planned in Session 13 appearing in the running app.
- **Documentation Split:** README as the quick pitch, Wiki as the depth.

---

## 2. Project Review and Final Feature Decision

The professor's visit to our group was short because little remained to sort out. What followed was a brief internal ideation round: is there anything still worth adding? The group agreed on one final feature, a splash screen.

> [!TIP]
> **Why a Small Feature Still Matters:**  
> Functionally a splash screen is a minor addition, but it shapes the first impression of the application. Most polished desktop apps greet the user with something before the main window appears, and the app stops feeling abrupt once it does the same.

Remaining work was then split: part of the group implemented the splash screen, while the rest began writing the README and the Wiki on the GitHub repository.

---

## 3. The Redesigned UI

The UI rework planned in Session 13 was now fully visible. The earlier version was utilitarian: flat, white, and functional with little visual thought, closer to software from the 1990s. The redesigned version is cleaner, better proportioned, and noticeably more pleasant to use.

![Redesigned UI Preview](https://github.com/user-attachments/assets/9a021f06-4185-4f53-9b3a-505b1d394fd0)

*The reworked interface as shown in this session.*

> [!NOTE]
> **Polish Changes Perception:**  
> Functionality did not change between the two versions, yet the redesign made the project feel finished in a way the earlier build did not.

---

## 4. Splash Screen in JavaFX

A splash screen appears briefly when the application launches, before the main window is shown.

```
App launch --> Splash window (name / logo / loading state) --> Main window (tree editor)
```

| Approach | How It Works | Best For |
|---|---|---|
| `Preloader` class | A separate class JavaFX runs *before* the main `Application`, shows a lightweight window, then hands over control | Splash screens tied to real startup work |
| Separate `Stage` + fade | Open a small `Stage`, fade it out, then show the main `Scene` | Simple branding moments |

For our project the splash screen is mainly a branding moment: the project name and a brief loading state before the tree editor appears. It is not technically complex, but it gives the app a proper entry point.

---

## 5. README vs. Wiki

> [!IMPORTANT]
> **Two Documents, Two Jobs:**  
> - **README:** The elevator pitch. A first-time visitor should understand in a couple of minutes what the project is, what it does, and how to run it.
> - **Wiki:** The depth. Architecture decisions, feature explanations, known limitations, and contribution steps.

Writing both without this boundary in mind produces a README that is too long and a Wiki that merely repeats it.

---

# Key Takeaways

1. **Last Project Session:** Our group was nearly done and used the time to confirm the plan and settle on a splash screen as the final feature.
2. **Splash Screens Complete the Experience:** JavaFX's `Preloader` pattern lets the app have a clean entry point without complicating the main application logic.
3. **UI Redesign Changes How a Project Feels:** A well-designed interface makes software feel finished in a way functionality alone cannot.
4. **Documentation Is Part of the Product:** A clear README and Wiki are what make a project understandable to people outside the team.
5. **Outside-In Thinking Exposes Gaps:** Writing documentation forces you to view the project as a newcomer would, which often reveals what is still unclear even to the builders.
6. **Knowing When to Stop:** Deciding when a feature is good enough to ship, especially close to submission, is a judgement skill in its own right.

---

## Final Reflection

Session 14 made it clear that the finishing stage of a project is mostly about presentation: how it looks on launch, how it reads on GitHub, and how easily a stranger can understand it. Writing the README pushed me to switch from the inside-out view I use while building to an outside-in view, asking what someone who has never seen the project needs to know first. That shift was uncomfortable at times, but it highlighted the parts of the project that were still fuzzy even to me. The discussion about whether the splash screen needed more branding also reminded me that "done enough" is a real engineering decision, especially when submission is close.
