# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `9287d0c3734e`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 8062.74 ± 6.09 | 8361.70 ± 13.91 | -3.58% | 204.81 ± 0.17 | 196.39 ± 1.94 | +4.29% |
| 256 | 9563.13 ± 33.11 | 10335.15 ± 6.75 | -7.47% | 199.78 ± 0.05 | 185.28 ± 0.55 | +7.82% |
| 512 | 9330.73 ± 17.51 | 10073.45 ± 31.40 | -7.37% | 192.21 ± 0.14 | 180.34 ± 0.91 | +6.58% |
| 1024 | 8562.56 ± 23.34 | 9388.04 ± 24.44 | -8.79% | 178.23 ± 0.26 | 168.77 ± 0.71 | +5.60% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
