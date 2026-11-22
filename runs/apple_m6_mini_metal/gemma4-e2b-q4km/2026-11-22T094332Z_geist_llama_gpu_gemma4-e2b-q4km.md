# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `7765ee2a075d`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2610.06 ± 6.58 | 2269.53 ± 3.11 | +15.00% | 89.88 ± 0.07 | 86.29 ± 0.06 | +4.16% |
| 256 | 2700.21 ± 5.29 | 2864.10 ± 3.43 | -5.72% | 89.60 ± 0.04 | 85.98 ± 0.07 | +4.22% |
| 512 | 2688.50 ± 4.16 | 2810.47 ± 1.62 | -4.34% | 88.88 ± 0.05 | 85.54 ± 0.08 | +3.90% |
| 1024 | 2637.17 ± 1.69 | 2758.37 ± 1.56 | -4.39% | 88.35 ± 0.08 | 84.62 ± 0.09 | +4.41% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
