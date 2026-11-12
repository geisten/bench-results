# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `48a84627b0c5`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2634.75 ± 6.66 | 2276.95 ± 3.32 | +15.71% | 89.56 ± 0.03 | 85.95 ± 0.11 | +4.21% |
| 256 | 2723.93 ± 4.79 | 2875.73 ± 7.15 | -5.28% | 89.30 ± 0.05 | 85.62 ± 0.08 | +4.30% |
| 512 | 2706.02 ± 6.85 | 2827.48 ± 4.64 | -4.30% | 88.55 ± 0.03 | 85.04 ± 0.19 | +4.12% |
| 1024 | 2658.14 ± 6.30 | 2776.53 ± 1.93 | -4.26% | 88.04 ± 0.05 | 84.21 ± 0.19 | +4.54% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
