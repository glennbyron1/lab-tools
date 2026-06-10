# Lab Tools — Eight Portfolio Projects (FROZEN)

| Folder | Name | What it does | RMF hooks |
|---|---|---|---|
| `labforge/` | **LabForge** | IaC: rebuild any node from code; drift detection | CM-2/3/6 |
| `firewatch/` | **FireWatch** | Scheduled SCAP/STIG scans + POA&M-style ConMon | CA-7, RA-5, CM-6 |
| `cauldron/` | **Cauldron** | Wazuh alerts triaged by the self-hosted LLM | AU-6, SI-4 |
| `stitch/` | **Stitch** | Backups that test-restore and prove it every run | CP-9, CP-10 |
| `ward/` | **Ward** | Pre-push DLP: blocks employer strings — tree, staged, history | AC-4, SI-12 |
| `familiar/` | **Familiar** | Network inventory vs reality: flags rogue/moved/missing devices | CM-8, SI-4 |
| `candle/` | **Candle** | Certificate expiry watcher (PKI's most common outage) | SC-12, SC-17 |
| `grimoire/` | **Grimoire** | GPO scanner: conflicts + Zero Trust pillar gaps | CM-6, CA-7 |

**FROZEN** = feature freeze: no new tools until the lab runs and at least
LabForge + Stitch execute on real hardware. Bug fixes and deployment hardening
only. The next artifact is the lab, not tool #9.

See TESTING.md — everything except Grimoire runs against included fixtures.
Honesty rule: résumé bullets track tools that actually RUN — not repos that exist.
