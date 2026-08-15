# Analysis of Coursework: AI-Assisted Full-Stack Java Application (CSC 508)

## 1. Overview

This coursework (15% of the course grade, Weeks 8–15, teams of three) requires building a three-layer desktop application in Java using JavaFX, a relational database via JDBC, and an explicit SDLC process. The distinguishing feature is that AI coding tools are a *mandatory, assessed* part of the workflow rather than an optional aid — teams are graded as much on how they directed, verified, and corrected AI output as on the resulting code.

## 2. What Is Actually Being Assessed

Stripping away the surface requirements, the coursework tests four separate competencies at once:

- **Software engineering fundamentals**: layered architecture (presentation / business logic / data access), OOP principles (encapsulation, inheritance, polymorphism, abstraction), normalised database design (3NF), and parameterised, transactional data access.
- **SDLC discipline**: producing and revising signed-off artefacts (SRS, design doc, test plan, defect log, retrospective) rather than just code.
- **Team process**: branch protection, mandatory peer-reviewed pull requests, individual commit accountability, issue tracking, and weekly meeting records.
- **AI governance**: a mandatory, ongoing AI Interaction Log (15+ entries) documenting what was asked, what was accepted/modified/rejected, and why — with higher marks for entries that show a caught AI mistake than entries where "everything worked first time."

This last point is the most novel element and the one most likely to be underestimated: the coursework explicitly rewards *catching AI errors*, not just using AI tools.

## 3. Structural Breakdown

| Area | Weight | Key risk if mishandled |
|---|---|---|
| Requirements & analysis | 10% | Vague, untestable acceptance criteria |
| System design (arch/UML/ERD/3NF) | 15% | Design and code diverge during implementation |
| Backend (schema, DAO, transactions) | 15% | Concatenated SQL strings — automatic forfeiture of backend marks |
| Logic (business rules, complexity) | 15% | Business rules leaking into the JavaFX controller |
| Frontend (JavaFX layering, UX) | 15% | SQL or business logic inside a controller |
| Testing & quality | 10% | Fabricated or unrun test results/defect logs |
| AI usage | 10% | Log reconstructed after the fact instead of maintained live; entries with no verification |
| Process & defence | 10% | Single end-of-term commit; unread/self-approved pull requests; can't explain own code in the viva |

Two rules carry outsized, near-automatic penalties: **any concatenated (non-parameterised) SQL forfeits backend marks**, and **any SQL/business logic inside a controller** violates the mandatory layering rule in Section 5. Both are exactly the kind of shortcut an AI coding assistant will produce by default if not explicitly constrained.

## 4. The Central Challenge: Timing

Section 7 flags this directly — teams that build the three layers separately across Weeks 10–12 and only integrate in Week 13 "do not finish." The Week 11 vertical slice checkpoint (one feature working end-to-end: screen → service → DAO → database) is a structural forcing function, not a formality. The practical implication: the team should get one thin feature fully wired through all three layers *before* fleshing out remaining functionality, even if that first feature is trivial.

## 5. Working With AI Tools: The Real Requirement

The brief permits any AI tool (Claude, Claude Code, Copilot, Cursor, Gemini, ChatGPT, JetBrains AI) but sets five required practices:

1. Direct with specific requirements/constraints/context — not vague prompts like "write a library app."
2. Review every diff line-by-line before commit; agents cannot push to `main`.
3. Verify generated code against the Section 5 layering rules specifically (AI tends to violate these).
4. Any accepted business-logic suggestion must have a corresponding test.
5. Check AI-suggested API/method signatures against real documentation, since hallucinated JavaFX/JDBC calls are a known failure mode.

Prohibited: submitting unexplainable code, fabricating test/defect evidence, pasting real personal/medical data into external tools, agents committing to `main`, and presenting AI-generated prose as unreviewed original analysis.

**Practical consequence**: the AI Interaction Log should be treated as a live engineering journal updated after every substantive AI interaction, not a document written retroactively — reconstructed logs are easy for a lecturer to spot (uniform tone, no messy back-and-forth, no dead ends) and are explicitly worth fewer marks than logs showing real corrections.

## 6. Process Requirements That Double as Marking Evidence

The repository itself is the evidence base: protected `main`, feature branches, peer-reviewed (not self-approved) pull requests, small frequent commits under each member's own account, one GitHub issue per requirement/defect closed by the resolving commit, and a lightweight weekly meeting log. This mirrors the marking scheme's "Process and defence" line (10%) and is designed so that contribution and diligence are verifiable from commit history alone, independent of the final demo.

## 7. Recommended Approach for This Team

1. **Week 8**: Confirm option (A–D), get all three members added as repo contributors, set up the `docs/`, `db/`, `src/main/java/app/{model,dao,service,ui}`, `src/test/java` structure from Appendix A immediately, and start the AI Interaction Log from the first prompt used.
2. **Week 9**: Freeze the ERD (3NF) and layered architecture diagram before writing implementation code; the schema script must run by the Week 9 checkpoint.
3. **Weeks 10–11**: Build the thin vertical slice first — one screen, one service method, one DAO method, one table — fully wired, tested, and demoable by the Week 11 checkpoint, before dividing into parallel layer work.
4. **Weeks 12–13**: Widen the slice across remaining features; write JUnit 5 tests for the service layer (including boundary/failure cases) as each feature lands, not at the end.
5. **Continuously**: Log every non-trivial AI interaction with outcome and judgement; enforce PR review by a non-author; keep commits small and attributed.
6. **Weeks 14–15**: Package a runnable artefact, verify the README on a machine other than the developer's, implement one post-release change request, and prepare each member to defend their own layer individually in the viva.

## 8. Summary

This coursework is less about producing a working Java app — which is a fairly standard three-layer CRUD system — and more about producing *evidence of disciplined engineering judgement under AI assistance*: a clean layered architecture, a defensible design, a verifiable process trail, and a log proving the team caught and corrected AI mistakes rather than rubber-stamping them. The two highest-risk failure modes are (a) integrating too late instead of slicing vertically early, and (b) letting AI-generated shortcuts (string-concatenated SQL, logic-in-controller) slip through review.
