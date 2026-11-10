# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `29a0ce4b5937`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2626.88 ± 4.81 | 2269.43 ± 3.40 | +15.75% | 88.92 ± 0.04 | 85.35 ± 0.06 | +4.18% |
| 256 | 2713.45 ± 5.75 | 2876.62 ± 2.66 | -5.67% | 88.67 ± 0.04 | 84.94 ± 0.11 | +4.39% |
| 512 | 2700.04 ± 5.67 | 2823.03 ± 2.23 | -4.36% | 87.94 ± 0.03 | 84.46 ± 0.16 | +4.11% |
| 1024 | 2652.57 ± 3.32 | 2772.66 ± 1.45 | -4.33% | 87.47 ± 0.04 | 83.66 ± 0.14 | +4.56% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
