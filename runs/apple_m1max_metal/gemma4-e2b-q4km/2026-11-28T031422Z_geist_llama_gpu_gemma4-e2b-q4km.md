# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `0b0ee998e552`; llama.cpp `d81235049384`.

Host profile `apple_m1max_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M1 Max, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M1 Max (8 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 3411.24 ± 7.76 | 1403.47 ± 1.45 | +143.06% | 122.07 ± 0.45 | 99.79 ± 0.29 | +22.33% |
| 256 | 4205.31 ± 9.43 | 1523.49 ± 0.33 | +176.03% | 121.27 ± 0.26 | 99.65 ± 0.24 | +21.70% |
| 512 | 4463.86 ± 8.56 | 1550.36 ± 1.61 | +187.93% | 120.02 ± 0.29 | 99.37 ± 0.25 | +20.78% |
| 1024 | 4548.43 ± 4.15 | 1487.56 ± 0.77 | +205.77% | 117.75 ± 0.37 | 96.56 ± 0.43 | +21.95% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
