# Active Handoffs

Handoffs contain temporary active working state. They are not permanent architecture and must never be the only place an important decision exists.

Use one scoped file per active workstream/task, for example:

```text
handoffs/desktop-available.md
handoffs/station-auth.md
handoffs/server-bootstrap.md
```

A handoff should contain:

- current objective;
- repository/branch/PR;
- completed work;
- current issue/blocker;
- important constraints;
- next work;
- relevant files/links.

When work finishes, move durable knowledge into `CURRENT_STATE.md`, `DECISIONS.md`, ADR/specification/interface/workstream docs, or the owning component repository. Then delete or archive the obsolete handoff.