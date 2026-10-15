---
name: mirpoll
description: Index the codebase into per-module docs, interview the user about the task until the plan is confirmed, then write a spec and plan with DoR/DoD for every item and ask for approval. Manual only, via /mirpoll.
disable-model-invocation: true
argument-hint: [task or draft spec]
---

# mirpoll

Input: $ARGUMENTS
If empty, ask the user what they want to build.

Write everything short and simple. Short sentences. No jargon. A child should get it.

## Step 1. Index the codebase

Goal: know the project before asking questions.

1. Find the modules. A module is a top-level folder with its own job (for example `auth`, `api`, `ui`, `db`).
2. For each module write `docs/modules/<module>.md`:
   - **What it does** — one or two sentences.
   - **Key files** — up to 5 files and what each one does.
   - **Entry points** — where work starts (routes, commands, handlers).
   - **Talks to** — other modules or external services it uses.
   - **Watch out** — one or two risky or unclear spots, if any.
3. Write `docs/modules/README.md`: one line per module with a link.
4. Skip generated code, vendor folders, and build output.
5. Keep each file under 30 lines.

## Step 2. Interview

Goal: the user says the plan is correct. Do not write code before that.

Each round:
1. Check what is still unclear: goal, who uses it, what is in and what is out, inputs and outputs, limits (stack, deadline, data), how we know it is done, edge cases, order of work.
2. Ask 1 to 3 questions. Use AskUserQuestion if available, else plain text. Do not ask what the code or the user already answered.
3. Show a short plan summary (5 to 10 lines). Ask: "Is this plan correct? If not, what should change?"
4. No clear "yes" → go back to point 1.

Rules:
- "You decide" → write it down as an assumption and move on.
- Leave the loop only on a clear yes ("plan is correct", "yes", "looks good").
- One topic per question. No "just in case" questions.

## Step 3. Spec and plan

1. Write `docs/tz/<slug>.md` (if no `docs` folder, write `TZ-<slug>.md` in the project root):
   - **Goal** — what we want and why.
   - **Context** — what exists now. Link the module docs from Step 1.
   - **In scope / Out of scope**
   - **Requirements** — what it must do, and limits (speed, security, compatibility).
   - **Assumptions**
   - **Plan** — numbered items. Each item has:
     - **Do** — what to change, which modules.
     - **DoR** (ready to start) — what must be true before we start this item.
     - **DoD** (done) — how we check it is finished. Tests, behavior, docs.
   - **Acceptance** — how the user checks the whole thing.
   - **Open questions** — if any.
2. Show the file path. Ask: "Do you approve this spec? After approval I start the work."
3. Changes → update the file, ask again.
4. Start work only after a clear "approved".
