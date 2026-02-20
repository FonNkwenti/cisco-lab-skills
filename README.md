# cisco-lab-skills

Central hub for Cisco certification lab skills, Claude Code memory, and project scaffolding.
Used as a **Git submodule** (at `.agent/skills/`) inside each certification lab project.

## Structure

| Directory | Purpose |
|-----------|---------|
| `skills/` | 7 AI agent skills for lab generation and troubleshooting |
| `memory/` | Shared Claude Code memory — imported by all cert projects |
| `conductor-template/` | Parameterized conductor config templates |
| `scaffolding/` | gitignore, requirements.txt, shared lab tools |
| `bootstrap.sh` | One-command project creation for a new certification |

## Skills

| Skill | What It Does |
|-------|-------------|
| `chapter-topics-creator` | Plans a chapter — generates `baseline.yaml` + README |
| `chapter-builder` | Generates all labs in a chapter with config chaining |
| `lab-workbook-creator` | Generates a single lab (workbook, configs, diagram, scripts) |
| `fault-injector` | Creates automated fault injection scripts |
| `drawio` | Visual style guide + `generate_topo.py` for topology diagrams |
| `gns3` | Apple Silicon GNS3 constraints and hardware reference |
| `cisco-troubleshooting-1` | Structured 4-phase network troubleshooting methodology |

## Starting a New Certification Lab Project

```bash
# Push this repo to GitHub first, then:
./bootstrap.sh ccnp-enarsi-labs "CCNP ENARSI" "300-410"
```

Creates a fully structured project with submodule wired, conductor configs filled in, and `CLAUDE.md` memory set up.

## Using in an Existing Project

```bash
git submodule add https://github.com/YOU/cisco-lab-skills.git .agent/skills
# Update to latest:
git submodule update --remote .agent/skills
git add .agent/skills && git commit -m "chore: sync skills"
```

## Memory Cascade (Claude Code)

```
~/.claude/CLAUDE.md                  ← Tier 1: Global (your machine)
[cert-project]/CLAUDE.md             ← Tier 3: Project-specific
  @imports .agent/skills/memory/CLAUDE.md  ← Tier 2: This repo
    @imports each skill's SKILL.md   ← detail on demand
[cert-project]/labs/[ch]/CLAUDE.md   ← Tier 3b: Chapter context (optional)
```

See [CHANGELOG.md](CHANGELOG.md) and [LESSONS_LEARNED.md](LESSONS_LEARNED.md) for history and patterns.
