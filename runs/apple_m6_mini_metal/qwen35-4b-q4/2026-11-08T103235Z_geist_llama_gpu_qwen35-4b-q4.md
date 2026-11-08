# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-4b-q4_0.gguf` (`298fcb5fe7a77ccc79745ae24751560c5ac56874caff4bb39b1f2055bd72b8bb`)

geist `ff31d42364e1`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1386.41 ± 1.71 | 1379.76 ± 1.63 | +0.48% | 49.60 ± 0.02 | 49.65 ± 0.05 | -0.10% |
| 256 | 1526.19 ± 1.20 | 1471.83 ± 1.57 | +3.69% | 49.53 ± 0.01 | 49.46 ± 0.03 | +0.14% |
| 512 | 1539.38 ± 1.91 | 1433.49 ± 4.46 | +7.39% | 49.34 ± 0.02 | 49.21 ± 0.03 | +0.27% |
| 1024 | 1535.78 ± 1.95 | 1431.88 ± 2.32 | +7.26% | 48.96 ± 0.04 | 48.93 ± 0.02 | +0.08% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
