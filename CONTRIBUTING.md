# Adding a skill

## Format

Every skill lives at `skills/<category>/<skill-name>/SKILL.md` — lowercase,
hyphenated directory name, matching `name` in the frontmatter exactly.
`<category>` is one of `dixscript`, `languages`, or `workflow` — add a new
top-level category deliberately, not per-skill.

```markdown
---
name: skill-name
description: One line — what it covers and when it should be pulled in.
origin: <"first-party" | "adapted: <source-repo>" | "community">
---

# Skill Title

Brief overview (1-2 sentences).

## When to Activate

- Concrete scenario
- Concrete scenario

## Core Concepts / Reference

The actual content — patterns, syntax, tables, whatever the skill needs.

## Common Mistakes

What goes wrong in practice, and the fix.
```

This is plain markdown plus YAML frontmatter — nothing Claude-specific and
nothing that assumes one particular AI tool's plugin format. It should read
the same whether it's pasted straight into a chat, pointed at by an agent
that reads local files, or dropped into another tool's own rules/skills
folder.

## Rules for this repo specifically

1. **DixScript content is the priority.** If a DixScript skill and a general
   skill would both need updating, the DixScript one goes first.
2. **Keep it small and correct over broad and stale.** Don't port a skill
   from `everything-claude-code` (or anywhere else) unless it's actually
   going to get used. A skill nobody reads is worse than no skill — it's
   stale advice waiting to mislead later.
3. **Attribute adapted content.** If a skill is adapted from another repo,
   say so in its `origin` field and add a row to `NOTICE.md`. DixScript-Rust
   / mdix-scaffold content is first-party (mine) and just needs
   `origin: first-party`.
4. **No sensitive data.** No API keys, tokens, absolute local paths, or
   anything that shouldn't be public — this repo is meant to be shareable.
5. **Verify before porting — don't trust a source's own docs about itself.**
   Read the actual file in full before adapting it into a skill here. Example
   of why this matters: `everything-claude-code`'s own skill-development guide
   documents `origin` as a flat frontmatter key, but the real skill files that
   set it at all (7 out of ~700) use nested `metadata.origin` instead. Its own
   docs drifted from its own shipped format — check the source, not the
   source's description of itself.
6. **New category folders go through the structure template, not by hand.**
   Add the directory group (with a `gitkeep()`) to
   `.mdix/project_structure/project_structure.mdix` and re-run it — see
   `skills/dixscript/dixscript-scaffold/SKILL.md`. Real skill content still
   goes through `.mdix/replacements/replacements.mdix`, same as everything
   else here.

## Validation checklist

- [ ] Frontmatter parses (valid YAML; `name`, `description`, `origin` present)
- [ ] Directory name matches `name` exactly
- [ ] "When to Activate" is concrete, not vague ("writing Rust code" not "Rust")
- [ ] Code/syntax examples are correct — for DixScript skills, check against
      `references/dixscript/midx.ebnf`
- [ ] No secrets, tokens, or local absolute paths

## Candidate skills (not started yet)

### `languages/`
- `rust` — ownership, error handling, traits, concurrency
- `csharp_unity` — Unity-specific C# patterns
- `typescript_svelte` — SvelteKit conventions
- `dotnet_blazor` — Blazor component/render patterns

### `workflow/`
- `git-workflow` — branching, commit conventions, conflict resolution
- `testing-patterns` — TDD / general testing, language-agnostic
- `code-review` — review checklist patterns

None of these are pulled in yet. Each needs the same "read the real file in
full before adapting" treatment as everything else in this repo — see rule 5
above.
