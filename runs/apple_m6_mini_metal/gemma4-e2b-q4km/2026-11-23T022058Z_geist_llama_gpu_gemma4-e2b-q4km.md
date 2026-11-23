# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `a1751c84f0d4`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2531.02 ± 7.86 | 2212.84 ± 3.58 | +14.38% | 85.25 ± 0.06 | 81.41 ± 0.09 | +4.71% |
| 256 | 3748.58 ± 5.16 | 2803.72 ± 7.02 | +33.70% | 85.00 ± 0.06 | 81.06 ± 0.10 | +4.87% |
| 512 | 4983.96 ± 7.04 | 2741.00 ± 9.09 | +81.83% | 84.21 ± 0.04 | 80.64 ± 0.10 | +4.43% |
| 1024 | 5959.27 ± 3.61 | 2697.46 ± 6.57 | +120.92% | 83.77 ± 0.06 | 79.80 ± 0.14 | +4.97% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
