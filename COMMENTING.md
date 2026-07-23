# Commenting source code

Comments come in three forms, and the rules below apply to all of them:
- **Module-level doc comments** — exported as API documentation.
- **Function-level doc comments** — exported as API documentation.
- **Single-line comments above code blocks** — serve the reader of the source.

## Scope

These rules are for source code under version control. Code written for tutorials, books, and blog
posts follows different conventions and may deviate from these rules for didactical purposes, such
as highlighting `# <- here!`, start a code block with `# flake.nix`, etc., but should otherwise
follow them.

## Core principle

- Comment the *why*, not the *what* (just like git commit style),
- **Don't encode transient working context**.

A comment outlives the session that created it and is read later with none of that context: no
knowledge of what you just debugged, refactored, or found surprising today. Whatever feels crystal
clear right now will fade. Write only what still makes sense years from now, to a reader who has the
file and nothing else.

## Rules

1. **Consistent** — Match the file. Comment exactly the way it already does: if it has no comments,
   add none; if it only uses doc comments (`///` not `//`), stay in that register; if it uses short,
   casual, lowercase notes, do the same. The one exception: a genuinely non-obvious *why* can earn a
   comment even in an otherwise bare file.
2. **Focused** — Comment only the code at hand. Don't explain neighboring code, don't explain
   decisions, and don't explain things that happen to be in your context now but won't be in the
   reader's later.
3. **Kept in sync** — When you change code, update or delete the comments that described the old
   behavior. A stale comment is worse than none.

## Context hierarchy

Knowledge sits at tiers ordered by how reachable it is for a future reader:

1. Common knowledge among programmers.
2. Knowledge established and referenceable across this project.
3. Knowledge local to a file, plus what lives in its git history.
4. Cutting-edge knowledge just learned — from debugging, or from this session.

Tiers 1–3 are safe to *reference*: the reader can reach them. Tier 4 cannot be referenced, and
building up to it inline usually costs too much space — so explain it in full where it's essential,
and there is precedence for wordy comment sections, otherwise push it to the commit message.

## Justify your commenting style

After writing a run of comments, give a brief summary in chat, not in the diff, of why you added
them. This makes it easy to check that you held to the file's pre-existing level of commenting.
