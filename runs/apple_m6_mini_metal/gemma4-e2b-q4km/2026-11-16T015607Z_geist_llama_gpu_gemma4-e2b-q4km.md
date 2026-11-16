# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `99e847f1c898`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2592.38 ± 3.65 | 2248.97 ± 5.52 | +15.27% | 88.22 ± 0.08 | 84.67 ± 0.11 | +4.19% |
| 256 | 2692.12 ± 2.97 | 2853.83 ± 4.54 | -5.67% | 87.98 ± 0.03 | 84.25 ± 0.21 | +4.43% |
| 512 | 2676.22 ± 1.53 | 2803.74 ± 2.37 | -4.55% | 87.15 ± 0.16 | 83.71 ± 0.22 | +4.10% |
| 1024 | 2627.35 ± 2.26 | 2757.32 ± 3.05 | -4.71% | 86.70 ± 0.14 | 82.83 ± 0.35 | +4.68% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
