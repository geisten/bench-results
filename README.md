# bench-results

Raw runs of geistlib's `bench-matrix` workflow: geistlib against llama.cpp under the frozen cross-engine protocol, per model and host. This repository is the archive: primary at git.geisten.net/geisten/bench-results, public mirror at https://github.com/geisten/bench-results. https://geisten.net/bench/ is a view rebuilt from it (`scripts/bench-publish.sh` and `tools/bench_matrix.py` in geistlib).

```
runs/<host column>/<model>/<UTC timestamp>_geist_llama_<cpu|gpu>_<model>.jsonl   every sample + provenance
runs/<host column>/<model>/<UTC timestamp>_geist_llama_<cpu|gpu>_<model>.md      the run's report
releases/<geistlib tag>.json                                                     newest run of every cell at that release
```

Host columns and models are defined in geistlib's `benchmark/bench_matrix.json`. The protocol is `benchmark/cross_engine_{cpu,gpu}_protocol.json`, and its SHA-256 is recorded in every run. Files are only ever added: never edit a run.
