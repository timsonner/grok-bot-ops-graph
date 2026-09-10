# Artifact layout

Empty on purpose. Specialists create files here when a packet says `status: needed`.

```
artifacts/
  research/     pack.md (cited pack)
  drafts/       changelog.md or other requested artifact
  checks/       findings.md
  staging/      human-packet.md
```

Rules:

- Paths in packets are relative to the job, using the convention `ops-graph/jobs/<slug>/artifacts/...`
- No secrets, no private URLs, no real names
- `checker` writes only in `checks/`
- `distribution` writes only in `staging/`
