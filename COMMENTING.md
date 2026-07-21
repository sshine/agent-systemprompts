# Commenting source code

There are three kinds of comments in source code:

1. Module-level doc comments: They get exported as API documentation.
2. Function-level doc comments: They also get exported as API documentation.
3. Single-line comments above code blocks: They serve the reader of the source code.

These rules mainly apply when changing source code for version control.

There are different rules for comments in source code intended for tutorials, books and blog posts.

## Commenting rules

1. Consistent: Add comments in exactly the same way as the file already has. If the file has no
   comments, don't add any comments. If the file only has doc comments (e.g. `///` instead of `//`),
   only add doc comments. If the file has short, casual, lowercase sentences, go with that.
2. Durable: Imagine the context of the comment spanning years, not just the single session that
   brought it into existence. We know things now that are hard to relay and things that don't matter
   long-term. Comments are read in the context of the file without knowledge of our current working
   context.
2. Don't explain other code, and don't explain random things that happen to be in your context that
   aren't in the context of the reader some time later. Whatever seems to be crystal clear will fade,
   and the comment has to be durable over time.

## Context hierarchies

When writing comments, refer to the following hierarchies of context:

1. Common knowledge among programmers
2. Knowledge established and referencable in this project
3. Knowledge about a specific part of this project, known only in the file and in git comments
4. Cutting-edge knowledge learned from debugging, or from 

The reader cannot jump to cutting-edge knowledge we learned just now, just by referencing it, and
building to a conclusion often requires too much space. Leave such comments for git commit messages.

## Justification

When writing many comments in a sequence, please provide in summary afterwards why.

This helps assess if you stayed true to the pre-existing level of comments.

-------

# Commenting source code

Comments come in three forms, and the rules below apply to all of them:
- **Module-level doc comments** — exported as API documentation.
- **Function-level doc comments** — exported as API documentation.
- **Single-line comments above code blocks** — serve the reader of the source.

Scope: these rules are for source code under version control. Code written for tutorials, books,
and blog posts follows different conventions and is out of scope here.

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
2. **Focused** — Comment only the code at hand. Don't explain neighboring code, and don't explain
   things that happen to be in your context now but won't be in the reader's later.
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
otherwise push it to the commit message.

## Justify your commenting style

After writing a run of comments, give a brief summary in chat — not in the diff — of why you added
them. This makes it easy to check that you held to the file's pre-existing level of commenting.
