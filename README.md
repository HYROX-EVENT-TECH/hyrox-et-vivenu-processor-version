# hyrox-et-vivenu-processor-version

Minimum-version pointer for the **HYROX Vivenu Processor** force-upgrade gate.

The app reads `version.csv` on startup (see `vv_converter/version_gate.py`). It is
a two-column key/value file:

| key | value |
|-----|-------|
| `min_version` | the lowest version allowed to run (blank = gate disabled) |
| `download_url` | where blocked users are sent to update |
| `message` | *(optional)* custom text on the block screen |

**Do not hand-edit `min_version` casually.** The app's release workflow
(`update-version-pointer` job) rewrites this file automatically on every `v*`
tag, setting `min_version` to the version just released — so every release
becomes mandatory for older builds with nothing to update by hand.

Current state: `min_version` is blank, so the gate is **disabled** (dormant).
The next tagged release will set it and activate the gate. The gate also
fail-opens: if this file is ever unreachable, the app runs normally.
