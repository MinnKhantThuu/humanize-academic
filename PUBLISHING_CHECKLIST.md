# Publishing checklist — humanize-academic

Complete these steps in order before/after pushing to GitHub.

## 1. Pre-publish (local)

- [x] Repo folder created: `/Volumes/Mac Storage/Projects/My Projects/humanize-academic-skill`
- [x] `skills/humanize/SKILL.md` + 3 reference files copied from `~/.codex/skills/humanize/`
- [x] SKILL.md bumped to v1.2.0 with light-edit guard (step 0) added
- [x] `README.md` written (positioning, honest limits, install, license, acknowledgments)
- [x] `LICENSE` (MIT with attribution to blader/humanizer and harshaneel/humanize)
- [ ] Test the skill end-to-end one more time from the repo copy:
      ```bash
      mkdir -p ~/.codex/skills && cp -R skills/humanize ~/.codex/skills/
      # restart codex, then: humanize this: <ai-flavored paragraph>
      ```
- [ ] Quick QA read of SKILL.md — no leftover references to personal paths
      (checked: frontmatter and body clean)

## 2. Repo hygiene before first commit

- [ ] `git init`, create `.gitignore` (only needs `.DS_Store`)
- [ ] First commit message: `humanize-academic v1.2.0: academic + docs + ESL-safe humanizer skill`
- [ ] Default branch: `main`

## 3. GitHub setup

- [ ] Create repo named `humanize-academic` (public)
- [ ] Description (copy-ready): `Agent skill that removes AI-writing tells from English text — with citation-preserving academic mode, docs mode, and an ESL-safe vocabulary ceiling. Works in Codex, Claude Code, and any SKILL.md agent.`
- [ ] Topics: `humanizer`, `ai-writing`, `codex`, `claude-code`, `agent-skills`, `academic-writing`, `skill`, `prompt-engineering`
- [ ] Push

## 4. Post-publish (discovery)

- [ ] Search-traffic FAQ section is already in README; consider adding a
      "Frequently compared with" section naming blader/humanizer and
      academic-humanizer for search visibility
- [ ] Open a good-first-issue on your own repo only if you plan to maintain
- [ ] Optional: submit to skills.sh / agent skill directories if they accept
      listings
- [ ] Optional: replace `YOUR_USERNAME` in README install instructions with
      the real GitHub username (2 occurrences)

## 5. Maintenance policy (decide now)

- Re-sync from personal copy when you improve `~/.codex/skills/humanize/`:
  ```bash
  cp ~/.codex/skills/humanize/SKILL.md skills/humanize/SKILL.md
  cp ~/.codex/skills/humanize/references/*.md skills/humanize/references/
  # bump metadata.version, commit
  ```
- If the light-edit guard or any mode changes behavior in a way that could
  surprise existing users, bump the minor version and note it in this file.
