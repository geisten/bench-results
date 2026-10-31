# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `93817e73fce2`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.0.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1026.80 ± 1.15 | 2293.99 ± 2.46 | -55.24% | 91.58 ± 0.05 | 88.76 ± 0.07 | +3.18% |
| 256 | 1040.69 ± 0.62 | 2884.18 ± 2.67 | -63.92% | 91.28 ± 0.02 | 88.52 ± 0.12 | +3.12% |
| 512 | 1034.16 ± 0.20 | 2828.15 ± 1.67 | -63.43% | 90.54 ± 0.02 | 88.01 ± 0.12 | +2.88% |
| 1024 | 1020.27 ± 0.23 | 2782.65 ± 0.94 | -63.33% | 89.99 ± 0.05 | 87.14 ± 0.13 | +3.28% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
