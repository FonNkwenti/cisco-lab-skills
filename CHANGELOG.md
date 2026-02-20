# Changelog

All notable changes to the cisco-lab-skills hub are documented here.

---

## [1.0.0] — 2026-02-20

### Initial Release — Extracted from ccnp-encor-labs-conductor

**Skills included:**
- `chapter-builder` — Multi-lab generation with config chaining
- `chapter-topics-creator` — Chapter planning with `baseline.yaml` generation
- `lab-workbook-creator` — Full lab artifact generation
- `fault-injector` — Automated troubleshooting fault script generation
- `drawio` — Visual style guide + `generate_topo.py` automation
- `gns3` — Apple Silicon GNS3 constraints and hardware reference
- `cisco-troubleshooting-1` — Structured 4-phase troubleshooting methodology

**Memory system introduced:**
- `memory/CLAUDE.md` — Shared Claude Code context (Tier 2)
- `memory/skills-index.md` — Quick reference for all skills
- `memory/gns3-constraints.md` — Hardware platform facts
- `memory/lab-standards.md` — DeepSeek Standard specification

**Key bugs fixed during ENCOR development (see LESSONS_LEARNED.md):**
- Python multiline strings causing `SyntaxError: unterminated string literal`
- Draw.io bypass links crossing through intermediate devices
- GNS3 tunnel overlays requiring top-center exit points to arc correctly
- Netmiko requiring explicit empty string fields (not omitted)

---

<!-- Template for future entries:

## [X.Y.Z] — YYYY-MM-DD

### Skills changed: [skill-name]

**What changed**: Brief description
**Why**: Reason
**Affected projects**: Update submodule ref in all cert repos

-->
