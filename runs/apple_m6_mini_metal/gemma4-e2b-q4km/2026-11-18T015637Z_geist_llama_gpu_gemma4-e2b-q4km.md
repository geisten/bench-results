# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `372846765fa0`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2577.85 ± 7.26 | 2247.01 ± 5.70 | +14.72% | 87.63 ± 0.04 | 83.89 ± 0.05 | +4.46% |
| 256 | 2685.13 ± 5.67 | 2855.57 ± 1.50 | -5.97% | 87.36 ± 0.04 | 83.61 ± 0.09 | +4.49% |
| 512 | 2669.73 ± 4.09 | 2803.34 ± 1.20 | -4.77% | 86.68 ± 0.06 | 83.10 ± 0.11 | +4.30% |
| 1024 | 2624.21 ± 5.46 | 2756.65 ± 1.52 | -4.80% | 86.18 ± 0.06 | 82.34 ± 0.10 | +4.66% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
