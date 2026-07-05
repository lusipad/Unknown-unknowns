# Use a Reference

Sometimes the user can't describe what they want — but they can point. The best
reference is **source code**: it carries the edge cases and defaults that a screenshot
or prose description loses. A reference in a different language still beats a vague spec.

## 1. Pin down the reference and the extraction target

Confirm: **where** is the reference (folder, dependency, URL — for a website component,
read the page's actual markup/CSS/JS, not just how it looks), and **what exactly** to
extract — behavior (semantics, edge cases), structure (architecture, API shape), or
appearance (markup, styling)? "All of it" is rarely true; make the user pick the
load-bearing part.

## 2. Read the source properly

The happy path, then every branch off it: error paths, retries, timeouts, limits.
**Defaults and magic numbers** — they encode the author's hard-won knowledge. The
configuration surface. Tests, if present — they document intended semantics more
honestly than the code.

## 3. Produce the semantics checklist

Before writing any code, one row per observed behavior:

| Reference behavior | Plan | Why |
|---|---|---|
| "exponential backoff, base 200ms, jitter ±20%, cap 30s" | keep | core of what user wants |
| "persists queue to disk" | drop | our client is stateless |
| "errors returned as Result<T>" | adapt → typed exceptions | idiomatic in our stack |

Every row marked **keep / adapt / drop** with a one-line reason. Get the user's
confirmation — this is where misunderstandings die cheaply.

**License check:** before carrying over code verbatim, check the reference's license.
Default to reimplementing semantics in the target stack's idiom.

## 4. Implement and verify against the checklist

For each **keep** and **adapt** row, state how the new implementation satisfies it
(test, code reference, or demo). Unverified rows are marked openly, not assumed done.

If the reference turns out to do something subtly different from what the user believed,
surface it before implementing — that discovery is the technique working as intended.
