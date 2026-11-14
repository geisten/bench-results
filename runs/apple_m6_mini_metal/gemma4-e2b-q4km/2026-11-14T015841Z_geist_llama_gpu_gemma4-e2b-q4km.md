# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `666d971e5db2`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2630.23 ± 5.11 | 2279.51 ± 3.14 | +15.39% | 89.31 ± 0.03 | 85.90 ± 0.02 | +3.97% |
| 256 | 2714.29 ± 2.50 | 2876.39 ± 4.64 | -5.64% | 89.05 ± 0.03 | 85.45 ± 0.13 | +4.21% |
| 512 | 2698.87 ± 2.30 | 2822.05 ± 2.96 | -4.36% | 88.35 ± 0.02 | 85.06 ± 0.06 | +3.87% |
| 1024 | 2650.34 ± 0.90 | 2771.99 ± 6.90 | -4.39% | 87.81 ± 0.03 | 84.17 ± 0.15 | +4.33% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
