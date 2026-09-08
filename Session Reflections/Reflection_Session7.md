# CSC360: Computer Graphics and Image Processing
## Reflection Journal — Session 7

---

### Session Metadata
- **Course Code:** CSC360
- **Course Name:** Computer Graphics and Image Processing
- **Student ID:** AU2420150
- **Session Number:** Session 07
- **Session Date:** August 27, 2026
- **Entry Date:** August 31, 2026

---

## 1. Overview

Session 7 shifted focus away from graphics math and toward the infrastructure layer that supports real software projects: how Java source becomes a distributable artifact, how automated pipelines take that artifact from a commit to a deployment, and how text itself is represented at the byte level.

Key topics covered in this session include:
- **Java Build Artifact Pipeline:** The transformation chain from `.java` source to `.class` bytecode to a packaged `.jar` file, and what belongs in version control versus what doesn't.
- **`pom.xml` as Build Orchestrator:** How Maven's configuration file drives compilation, testing, and packaging without producing bytecode itself.
- **CI/CD Pipelines:** The distinction between Continuous Integration (build + test on every push) and Continuous Delivery/Deployment (packaging and release automation).
- **Character Encoding — UTF-8 vs. UTF-16:** Why these are not "versions" of one another but differently optimized variable-length encodings for different script profiles.
- **Security-First Application Design:** Why login and access-control systems are foundational rather than incidental features.

---

## 2. Java Build Artifact Pipeline

The build chain follows a strict, one-directional transformation:

```
+-------------------+       javac       +-------------------+       Maven        +-------------------+
|   .java source    |  ----------------> |   .class bytecode |  ----------------> |     .jar file      |
| (human-readable)  |                    | (JVM instructions) |                    | (distributable unit)|
+-------------------+                    +-------------------+                    +-------------------+
```

- **`.java` files:** Human-written source code.
- **`.class` files:** Output of `javac`. Not human-readable and not machine-specific binary — they are portable bytecode meant to be executed by any JVM.
- **`.jar` file:** The final distributable package assembled by Maven from the compiled `.class` files.

> [!TIP]
> **What Belongs on Git:**  
> Source code (`.java`) and build descriptors (`pom.xml`) should always be version-controlled. The `target/` directory, `.class` files, and the packaged JAR are generated outputs and should never be committed — doing so causes repository bloat, merge conflicts on machine-generated files, and environment-specific build discrepancies for other developers.

---

## 3. pom.xml as Build Orchestrator

Maven uses `pom.xml` to drive the full build lifecycle rather than to generate bytecode directly:

$$\text{compile } (.java \to .class) \longrightarrow \text{test} \longrightarrow \text{package } (.class \to .jar)$$

- **Plugins declared in `pom.xml`** — such as `maven-jar-plugin` — control exactly how the JAR is assembled: which classes are included, where the manifest lives, and which class serves as the entry point for an executable JAR.
- **Indirect Relationship:** `pom.xml` does not compile code itself. It configures Maven, which in turn configures `javac` and the packaging plugins — making it the blueprint that lets a build be reproduced identically by anyone who clones the repository.

> [!IMPORTANT]
> **Reproducibility Without Guesswork:**  
> Without `pom.xml`, replicating a build on a different machine requires manual scripting and trial-and-error. With it, the entire compile-test-package sequence is deterministic and portable across machines and CI servers.

---

## 4. CI/CD Pipelines

CI/CD stands for Continuous Integration and Continuous Delivery/Deployment.

- **CI (Continuous Integration):** Frequently pushing code to a shared repository, triggering an automated pipeline that builds and tests on every push — catching integration bugs before they compound.
- **CD (Continuous Delivery/Deployment):** Extends the pipeline past testing by automating packaging, publishing, and deployment to staging or production.

A typical pipeline flows as follows:

```
Git Push/PR --> Checkout Code --> mvn compile --> mvn test --> Package JAR --> Publish Artifact --> Deploy to Staging/Production
```

Tools like **GitHub Actions**, **GitLab CI**, and **Jenkins** execute these pipelines. The underlying goal is to replace error-prone manual release steps with a consistent, repeatable process regardless of who pushed the change.

---

## 5. Character Encoding — UTF-8 vs. UTF-16

Both are Unicode standards, not sequential versions of each other — a distinction that is easy to misread from their names.

| Encoding | Minimum Unit | ASCII Cost | CJK Script Cost | Dominant Use |
| :--- | :--- | :--- | :--- | :--- |
| **UTF-8** | 1 byte | 1 byte/char | ~3 bytes/char | Web, most modern systems |
| **UTF-16** | 2 bytes | 2 bytes/char | 2 bytes/char (BMP) | Internal to Java, JavaScript, Windows |

- **UTF-8:** Variable-length; ASCII characters cost 1 byte, characters outside that range cost 2–4 bytes. This backward compatibility with ASCII is a major reason it became the web's dominant standard.
- **UTF-16:** Also variable-length, but its minimum code unit is 2 bytes; most Basic Multilingual Plane (BMP) characters cost 2 bytes, with characters outside it costing 4 bytes.

> [!NOTE]
> **The "16" Is Not a Version Number:**  
> The numbers in UTF-8/UTF-16 refer to the bit-width of the minimum code unit, not a release cycle. A natural first assumption is that the higher number means "newer and better," but UTF-16 is actually more expensive for ASCII-heavy text since it can never go below 2 bytes per character. Neither encoding is universally superior — the right choice depends on the script profile of the text being processed.

---

## 6. Security-First Application Design

A login and access-control system was framed as the single most important component to get right before building anything else in a web application. This ties directly to CI/CD and testing discipline:
- **Unit tests** verify individual components in isolation.
- **Integration tests** verify that components work correctly together.
- Both matter more, not less, when the component being tested is the access-control layer that everything else depends on.

---

# Key Takeaways

1. **Build Artifact Chain:** `.java` $\to$ `.class` (via `javac`) $\to$ `.jar` (via Maven). Source and `pom.xml` belong on Git; `target/`, `.class` files, and JARs do not.
2. **`pom.xml`'s Indirect Role:** It configures Maven, which configures `javac` and packaging plugins — it is a blueprint, not a compiler.
3. **CI vs. CD:** CI automates build-and-test on every push; CD automates packaging and release once tests pass.
4. **UTF-8 vs. UTF-16 Are Not Versions:** UTF-8 minimizes cost for ASCII-heavy text; UTF-16 minimizes cost for CJK-heavy text. The digit in each name denotes minimum code-unit width, not superiority.
5. **Security as Foundation:** Access control (e.g., RBAC) is not an add-on feature — it is the layer every other feature's safety depends on.

---

## Final Reflection

Session 7 connected two areas that initially seemed unrelated: build infrastructure and text encoding. Both turned out to hinge on the same underlying lesson — surface-level assumptions (that generated files are harmless to commit, or that a bigger version-like number means a strictly better standard) break down once you understand what is actually happening underneath. Tracing `.java` through to a deployable JAR, and rebuilding my mental model of UTF-8/UTF-16 around code-unit width rather than version hierarchy, both reinforced the same habit: check the mechanism before trusting the naming convention.
