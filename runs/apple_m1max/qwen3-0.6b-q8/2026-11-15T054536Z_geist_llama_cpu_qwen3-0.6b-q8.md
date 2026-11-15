# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `7765b16fc97f`; llama.cpp `d81235049384`.

Host profile `apple_m1max`: 8-thread prefill, 7-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M1 Max (8 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1297.94 ± 0.97 | 1633.39 ± 1.73 | -20.54% | 135.36 ± 1.31 | 136.92 ± 0.75 | -1.14% |
| 256 | 1216.26 ± 0.98 | 1600.26 ± 5.74 | -24.00% | 125.61 ± 1.07 | 129.28 ± 0.46 | -2.84% |
| 512 | 1067.68 ± 1.23 | 1465.43 ± 8.47 | -27.14% | 110.52 ± 1.06 | 119.47 ± 0.32 | -7.49% |
| 1024 | 840.31 ± 7.32 | 1259.20 ± 4.78 | -33.27% | 87.84 ± 0.72 | 97.88 ± 1.22 | -10.26% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
