---
name: working-method
description: How to carry any task from request to report - understand the goal, surface the decisions, diagnose before fixing, attack the design, prove it, deliver, report. Load at the start of every task, before reading code.
license: MIT
compatibility: opencode
---

# Working method

Apply this to every task, whatever its size. The effort scales with the task;
the order of the steps does not.

# 1. Understand the goal, not only the instruction

- Find out what the thing is **for** before deciding how it works. Read the
  project's own description of its purpose first: spec, README, notes.
- Write the goal in one sentence. Every later decision is judged against it.
  If you cannot write that sentence, ask before writing code.
- Domain facts come from the user only: what a role does, what a game or
  business rule is, what is worth more than what. Never infer one. A guess
  that sounds right is the most expensive kind of mistake, because nobody
  checks it.
- Write each domain fact down where the next session will find it, and say
  where it overrides an older document.

# 2. List the decisions nobody stated

Every task contains decisions the request did not mention. A silent decision
never looks like a choice: it looks like the obvious way to build the thing.
So make the list on purpose, before building.

For each one, say which way you are going. Take the obvious ones without
ceremony. Raise the ones in these categories, because the user nearly always
has an opinion there:

- **Behaviour in time**: when something happens, how fast, what it
  interrupts, what waits for what. A delay chosen by the implementation is
  still a product decision.
- **Priority**: what wins when two goals conflict.
- **Who controls what**: which machine, account or person decides, and where
  it is edited from.
- **Security and trust**: who may do a thing, what crosses a network, what is
  stored in clear.
- **Shape of the data**: what belongs to which thing. The most expensive to
  change later.
- **Visibility**: what a person sees, and whether they can act on it.
- **Failure budget**: what may break, and what must never. Ask for it in the
  user's own words.

Ask in one batch, with a recommended option first. Ask a question whose
answer depends on another one only after that one is answered.

# 3. Diagnose before fixing

For a bug, the first deliverable is an explanation, not a patch.

- Read every piece of evidence in full: logs, screenshots, the exact error.
- Separate what the evidence **proves** from what you **suppose**. Write both
  down.
- Find the cause, then find its **class**: the other ways the same fault can
  happen. Fix the class when it is cheap.
- If the evidence cannot decide between two causes, say what would decide it
  and get that evidence, rather than fixing both blind. Adding the logging
  that answers the question is a valid fix.

# 4. Attack the design before building it

Answer these for any mechanism: state, a file two processes share, a socket,
a process, a cache, a timer, a decision taken between machines. Skip them for
a renamed label or a comment.

1. **Who else has a copy?** What happens when the holder disappears?
2. **Is it a state or an event?** An event that is missed is lost for good. If
   the receiver must end up right, send the state, and send it again.
3. **Can two copies be ordered?** A timestamp says when a copy was written,
   not which content is newer.
4. **What bounds it?** For anything that grows: the ceiling, and what happens
   at it.
5. **Who stops what you started?** And what if the starter dies first?
6. **Who finds out when it fails?** Every swallowed error: is the failed
   thing the one the design depends on?
7. **Can the invariant be read at runtime?** If correctness rests on a value,
   somebody must be able to see it without opening files.
8. **Does the label name exactly the set?** A setting's word must cover
   precisely what it controls.
9. **What thread is this, and what may it block?**

Then write the check for the answer you are least sure of **before** writing
the mechanism. A check written after the bug proves the fix; a check written
before finds the bug.

# 5. Build like the code around you

- Load the project's conventions and the language's traps before the first
  edit. Follow the file you are in over your own preferences.
- Do not bend shared code for one feature: add a gate or read state it
  already keeps.
- New behaviour ships off by default unless the user says otherwise.
- Keep the change as small as the goal allows. No refactor on the side.

# 6. Prove it, and say how far

Name the kind of evidence every time. They are not interchangeable, and a
reader assumes the strongest one you let them:

- passes the linter or checker;
- loads;
- a test drove it;
- somebody watched it work;
- it ran in real use.

Then:

- "Untested" hides two claims: nobody ran it, and nobody attacked it. Say
  which one is true.
- A comment that explains why is not evidence.
- Keep a ledger in the repository of what is proven and what is not, with
  checkboxes. A sentence in one commit message is lost by the next one.
- Do not commit what has not passed the checks that are available. If the
  test environment is down, wait or say so.

# 7. Deliver

- One atomic commit per feature, following the project's git rules. The body
  says what a future reader cannot reconstruct: what was tried, what was
  rejected, why a number is that number, what is not proven.
- Update the documentation the change makes wrong, in the same commit.
- Nothing is pushed, merged or published without asking.

# 8. Report

- Lead with the outcome. Then what is proven, what is not, and what the user
  must do or decide next.
- Admit a wrong assumption plainly when one is found, and correct every
  document that carried it.
- When the user asks a "what if" question, answer the instance and then the
  class it belongs to.
- End with at most one question or one proposed next step.
