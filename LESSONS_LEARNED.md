# Lessons Learned — Cisco Lab Skills

Patterns, bugs, and design decisions from CCNP ENCOR lab development.
Reference this when starting a new certification or extending a skill.

---

## Python Script Generation

### ❌ Bug: `SyntaxError: unterminated string literal` in generated scripts

**Cause**: Fault injection / setup scripts using multiline f-strings with embedded CLI config blocks. The AI generates a string that ends prematurely or contains an unescaped `"""`.

**Fix**:
1. Represent CLI config as a Python `list` of strings, not a heredoc or f-string.
2. After generating any Python script, validate: `python3 -m py_compile script.py`

**Affected skills**: `fault-injector`, `lab-workbook-creator` (setup_lab.py)

---

## Draw.io Diagrams

### ❌ Bug: Link visually crossing through an intermediate device

**When**: Three devices share the same X coordinate and a bypass link connects non-adjacent ones (R1→R3 when R1, R2, R3 are all at x=400).

**Fix**: Offset intermediate devices horizontally by ≥100px. See `skills/drawio/SKILL.md` Section 4.8.

### ❌ Bug: Tunnel overlays routing through devices instead of arcing above

**Fix**: Use `exitX=0.5;exitY=0` (top-center) and add two arc waypoints above both endpoints. See `skills/drawio/SKILL.md` Section 4.9.3.

---

## Netmiko / GNS3 Automation

### ⚡ Pattern: Telnet connections to GNS3 consoles

```python
ConnectHandler(
    device_type="cisco_ios_telnet",
    host="127.0.0.1",
    port=5001,
    username="",    # Must be present but empty — do NOT omit
    password="",    # Same
    secret="",      # Same
    timeout=10,
)
```

Omitting `username`, `password`, or `secret` causes `TypeError` in some Netmiko versions.

---

## Lab Design

### ⚡ Pattern: Config chaining — never remove, only add

Solutions from Lab N become initial configs for Lab N+1. Never `no` a command between labs unless that lab explicitly teaches undoing it.

### ⚡ Pattern: Always run `chapter-topics-creator` first

Starting a chapter by jumping to `lab-workbook-creator` for Lab 01 causes topology problems in later labs (interface exhaustion, no room for optional devices). `chapter-topics-creator` pre-reserves IPs and interfaces for all planned labs via `baseline.yaml`.

### ⚡ Pattern: Console Access Table is required for fault-injector

The `fault-injector` skill parses port mappings from the workbook's Console Access Table (Section 3). Without it, generated scripts use placeholder ports. Always include:

| Device | Port | Connection Command |
|--------|------|--------------------|
| R1 | 5001 | `telnet 127.0.0.1 5001` |

---

## Style Iterations (ENCOR history)

| Version | Change | Reason |
|---------|--------|--------|
| v1 | Black connection lines | Default Draw.io |
| v2 | White lines (`#FFFFFF`) | Invisible on dark backgrounds |
| v3 | Labels below icon | Default position |
| v4 | Labels left/right (empty side rule) | Overlapped connection lines |
| v5 | Added IP last-octet labels | Students couldn't identify interface ownership |
