# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `a4d332c604a2`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2622.04 ± 5.92 | 2255.10 ± 8.84 | +16.27% | 88.74 ± 0.12 | 85.18 ± 0.11 | +4.18% |
| 256 | 2711.29 ± 5.80 | 2869.36 ± 3.30 | -5.51% | 88.51 ± 0.05 | 84.81 ± 0.15 | +4.36% |
| 512 | 2697.31 ± 1.87 | 2819.65 ± 1.76 | -4.34% | 87.81 ± 0.03 | 84.34 ± 0.09 | +4.11% |
| 1024 | 2648.76 ± 0.60 | 2770.65 ± 3.93 | -4.40% | 87.31 ± 0.04 | 83.38 ± 0.19 | +4.71% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
