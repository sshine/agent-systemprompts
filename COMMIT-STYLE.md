## git commit style

These rules apply when:
- formulating git commit messages
- creating pull requests and issues
- commenting in issue trackers

Subject:
- Separate subject from body with a blank line.
- Use conventional commits: `feat: blah`, `fix: blah`, `chore: blah`, `docs: blah`.
- Don't be too creative with the types: Reuse the ones that are already in use.
- Always specify scope, i.e. `feat(<scope>): blah` when there is git history precedence.
- Try to achieve some kind of scope taxonomy consistency, e.g. if there is precedence for
  `fix(istio): blah` or `fix(services): istio blah`, consistency wins. It's okay to make
  new scopes as long as they fit with the existing taxonomy.

Body:
- Always use bullet points and not full paragraphs; make the bullets fit a single line.
- A single line is 90-120 characters (stay consistent within a commit), or it wraps.
- Rather break the margin by 1-2 characters than wrap a single word. Just stay consistent.
- Try to fit what you explain within a single line of that length, not multiple paragraph lines. (And not super long lines like this one. It doesn't look good by itself, it's not consistent within the commit, and breaking it into multiple wrapped lines doesn't fit with the pattern of "one big paragraph bullet at the bottom of the list if necessary".)
- Don't over-explain the what: Briefly summarize at a higher level, focus on the why.
- Don't use backticks for keywords excessively; a little is fine, but it clutters.
- Organize the body into sections with headings just like in this git commit style instruction.
- Section names only need to be consistent within a commit: They can be filenames, scopes, topics.
- When asked to move comments to commit messages, adapt the comments to this style instead of
  copying them verbatim. Don't leave out too many details this way, but don't break the format.
- Occasionally, when there is a complex why, break into prose at the bottom of a bullet list, but
  make sure the words wrap nicely at the margin so it's pleasant to read; in particular, large code
  lines can mess this up. (This bullet is an example of how the last bullet is really a paragraph.)

Scope:
- Try to limit one commit to one logical change and break many changes into separate commits.
- When a single logical change is really simple, it's okay to leave out the body entirely.

Attribution:
- Do not write "Co-authored-by:" unless the co-author is a human. Accountability, not advertising.
