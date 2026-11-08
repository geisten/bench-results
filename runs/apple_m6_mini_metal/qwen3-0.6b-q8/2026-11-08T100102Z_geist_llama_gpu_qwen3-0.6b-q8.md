# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `ff31d42364e1`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 8111.28 ± 18.76 | 8374.48 ± 22.92 | -3.14% | 204.74 ± 0.27 | 197.63 ± 0.30 | +3.60% |
| 256 | 9579.23 ± 14.72 | 10312.20 ± 17.00 | -7.11% | 200.09 ± 0.12 | 190.09 ± 0.69 | +5.26% |
| 512 | 9325.45 ± 7.13 | 10094.25 ± 19.10 | -7.62% | 192.73 ± 0.09 | 185.48 ± 0.14 | +3.91% |
| 1024 | 8569.58 ± 8.07 | 9395.56 ± 19.39 | -8.79% | 178.97 ± 0.19 | 172.88 ± 1.02 | +3.52% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
