# CSC360: Computer Graphics and Image Processing

## Reflection Journal - Session 12

---

### Session Metadata

- **Course Code:** CSC360
- **Course Name:** Computer Graphics and Image Processing
- **Student ID:** AU2420150
- **Session Number:** Session 12
- **Session Date:** September 15, 2026
- **Entry Date:** October 01, 2026

---

## 1. Overview

The entire class session was dedicated to project work, with faculty circulating between groups to check progress and guide the build. For Group 7 (Taskwood), this was the session where the first working demo came together: AI-generated scaffolding, a live test, faculty approval, and the first commit to the shared repository.

Key topics covered in this session include:

- **Project Lab Format:** No new academic content - faculty check-ins replaced lecture time.
- **First Working Build:** Taskwood's initial JavaFX scaffold, generated with AI assistance and tested live.
- **Faculty Approval:** Demo shown and confirmed as heading in the right direction.
- **Shared Repository Setup:** Initial commit pushed so the whole team could branch from the same base.
- **AI-Assisted Development ("Vibe Coding"):** Where the human's role sits relative to AI-generated code.

---


## 2. First Working Build - Taskwood

Our group entered the session prepared: the concept, roles, and project idea had already been settled. Using Claude, we generated the initial source code for Taskwood - our local-first JavaFX application with a form panel for editing each node and JSON-based persistence.

- A **TreeView** on the left panel displays the full Workspace → Project → Task hierarchy and lets you navigate between nodes.
- Clicking any node opens its details in a **form panel** on the right for viewing and editing properties.
- All data auto-saves to a local JSON file and reloads on the next launch.

We tested the code on one machine, got a first working demo on screen, and showed it to the faculty.

---

## 3. Faculty Approval

The faculty confirmed the project was heading in the right direction. This checkpoint mattered beyond a simple progress update - it meant the team wasn't going to spend weeks building something that turned out to be misaligned with expectations.

> [!IMPORTANT]
> **Why Early Approval Matters:**  
> Getting a working demo in front of the faculty early is more valuable than spending longer refining a version that might be misaligned. The approval checkpoint here reduced the risk of rework later.

---

## 4. Shared Repository Setup

The source code was committed to GitHub at the end of the session so every group member could clone it and start working individually from the same base - avoiding conflicting versions or setup confusion down the line.

---

## 5. AI-Assisted Development

Using Claude for the initial scaffolding aligns with the course's AI policy, which permits AI assistance as long as students understand and can explain what they've built. The AI wrote the structure; the group's job was to understand it well enough to test it, evaluate whether it matched requirements, and defend it to the faculty.

> [!TIP]
> **Direction vs. Implementation:**  
> The most important decisions in this session were architectural - what the three levels should be, how the tree should behave, what the edit panel should contain, what the persistence format should look like. Claude wrote the implementation once the design was decided. This split (thinking through design vs. generating code) is the same pattern behind "vibe coding": the human directs what needs to exist and verifies the output matches that intent, rather than writing every line manually.

> [!NOTE]
> **Read Before You Run:**  
> The generated code was longer and more structured than expected, and it took real time to read through it and confirm it did what was planned. AI-generated code is only useful if you understand what it's doing - running code you can't explain is not a good position to be in when faculty asks how it works.

---

# Key Takeaways

1. **Architecture Over Syntax:** The most important decisions in an AI-assisted project session are architectural, not syntactic - deciding what to build and why is the real work.
2. **Understand Before You Ship:** AI-generated code must be read and understood before testing or submission; getting approval for code you can't explain isn't a valid outcome.
3. **Early Demos Reduce Risk:** Getting a working demo in front of the faculty early catches misalignment before it compounds into wasted work.
4. **Commit Immediately After Approval:** Pushing the initial source right after approval gives the whole team a clean, conflict-free starting point to branch from.
5. **AI Shifts What You Need to Understand:** AI-assisted development isn't a shortcut around understanding - it moves the required understanding from implementation syntax toward design intent, architecture, and critical review of generated output.

---

## Final Reflection

What stood out most in this session was how quickly the gap between "deciding what to build" and "having something running on screen" closed with AI assistance. That speed isn't just convenient - it changes how you allocate your time. Rather than spending the bulk of effort on typing out boilerplate, the team spent its time on the decisions that actually mattered: the hierarchy structure, the editing flow, and whether the result matched what the faculty expected. Having built something vibe-coded before, I used to think of it as a shortcut. This session reframed it for me - the shortcut isn't in the thinking, it's in the typing, and that's exactly the part that should be sped up.
