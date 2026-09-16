# CoreDNS certification gate

[![CNTi cert](https://github.com/martin-mat/coredns-gate/raw/badges/cnti-badge.svg)](https://github.com/martin-mat/coredns-gate/actions/workflows/cnti.yml)

The smallest possible use of the [CNTi Test Suite GitHub Action](https://github.com/lfn-cnti/testsuite-action):
the upstream [CoreDNS Helm chart](https://github.com/coredns/helm), unmodified, certified on
every change.

- [`cnti-testsuite.yaml`](cnti-testsuite.yaml) — the CNF: chart `coredns/coredns` at a pinned version.
- [`.github/workflows/cnti.yml`](.github/workflows/cnti.yml) — one step: the action runs
  `cnti-testsuite cert` on a kind cluster. The job **passes if the certification criterion is met
  and fails if it is not** — nothing else.
- [`renovate.json`](renovate.json) — Renovate opens a PR for every new upstream chart release; the
  certification run on that PR is the gate, so the repository history is a record of which CoreDNS
  releases were certified.

The workflow also runs weekly, so a new `cnti-testsuite` release re-certifies the unchanged chart.

The badge is published by the action to the [`badges`](https://github.com/martin-mat/coredns-gate/tree/badges)
branch after every run on `main` - no secrets involved; it links to the workflow runs.

Results (per-test table, annotations for failed tests, the results YAML as an artifact) are on
each run's summary page.
