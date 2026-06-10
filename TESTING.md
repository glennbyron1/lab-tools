# Testing Without the Lab

Every tool here can be exercised on any laptop (or this sandbox) with fake data.
Fixtures included under each project's test/ or scans/ folder.

## FireWatch (scanner)
No lab needed at all for the reporting half:
  cd firewatch && python3 report.py
Parses the included fake XCCDF in scans/ -> reports/summary.md + findings.csv.
For scan.sh itself: any Ubuntu VM/WSL2 with `apt install openscap-scanner ssg-base`
— scan localhost. A laptop IS a valid SCAP target.

## Cauldron (AI triage)
  cd cauldron && python3 triage.py --alerts test/alerts.json --out /tmp/r.md
Parses fake Wazuh alerts; without Ollama it degrades gracefully ("unreachable").
To test the AI half with NO lab: install Ollama on any PC (your 4070 Ti box),
`ollama pull llama3.1:8b`, then:
  OLLAMA_URL=http://localhost:11434 python3 triage.py --alerts test/alerts.json

## LabForge (Ansible)
  ansible-playbook playbooks/site.yml --syntax-check
  ansible-playbook -i "localhost," -c local playbooks/site.yml --check --diff
--check = dry run: shows what WOULD change on your own machine, changes nothing.
Any Linux VM, WSL2, or a free cloud shell works as a guinea pig.

## Stitch (backups)
Works against any directory + any disk — no lab concept involved:
  export RESTIC_REPOSITORY=/tmp/test-repo RESTIC_PASSWORD=test
  restic init
  # edit PATHS to something small like (~/Documents), then:
  ./backup-verify.sh
Check backup-log.md for the PASS line. Delete /tmp/test-repo when done.

## GUIs (FireWatch / Cauldron / Stitch)
Each has a Streamlit dashboard testable with the fixtures:
  pip install streamlit pandas requests --break-system-packages
  cd firewatch && python3 report.py && streamlit run gui.py
  cd stitch && streamlit run gui.py   # sample backup-log.md included
  cd cauldron && streamlit run gui.py # reports tab offline; live tab needs Ollama
LabForge intentionally has no GUI — deploy Ansible Semaphore for that.

## Ward (pre-push DLP)
No lab needed at all:
  cd ward && cp ward-rules.example.txt ward-rules.txt
  python3 ward.py --path /some/repo            # tree + staged
  python3 ward.py --path /some/repo --history  # catches deleted-but-committed files
  ./install-hook.sh /some/repo                 # make git push enforce it
Tested: a file committed then deleted passes the tree scan but is caught by --history.

## Familiar
  cd familiar && cp inventory.example.csv inventory.csv
  python3 familiar.py --scan-file test/scan-with-rogue.txt   # flags the planted rogue, exit 1

## Candle
  cd candle && cp candle-targets.example.txt candle-targets.txt
  python3 candle.py   # CRIT on the included 3-day cert, exit 2 (regenerate certs if stale)

## Grimoire
Needs a DC + RSAT GroupPolicy module — untestable without the lab by nature.
First run: Phase 2+, on the domain.
