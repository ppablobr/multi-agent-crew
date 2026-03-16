# Example: Billing Verification Automation

This is a real-world example of multi-agent collaboration using the Multi-Agent Crew framework.

## Scenario

A finance team needed to automate daily verification of partner billing charges in an e-commerce operation, ensuring each charge is communicated exactly once (zero duplicates).

## Agents Involved

1. **Process Manager** — Mapped the AS-IS and TO-BE processes, identified bottlenecks
2. **n8n Agent** — Built the automation workflow (Google Sheets → Filter → Validate → Slack)
3. **Tech Docs Writer** — Created the complete SOP documentation

## Files

| File | Description |
|---|---|
| `process-mapping.md` | AS-IS vs TO-BE process documentation |
| `process-as-is.excalidraw` | Visual flowchart of the current process |
| `process-to-be.excalidraw` | Visual flowchart of the automated process |
| `workflow.md` | n8n workflow technical documentation |
| `SOP.md` | Standard Operating Procedure for the team |

## Results

- **90% time savings** (30 min → 3 min/day)
- **95% error reduction** (20% → <1%)
- **100% coverage** (from ~70% manual verification)

## How to Reproduce

1. Use the **Process Manager** agent to map your own process
2. Hand off to the **n8n Agent** to build the automation workflow
3. Use the **Tech Docs Writer** to generate the SOP

This demonstrates the sequential handoff pattern described in `CLAUDE.md`.
