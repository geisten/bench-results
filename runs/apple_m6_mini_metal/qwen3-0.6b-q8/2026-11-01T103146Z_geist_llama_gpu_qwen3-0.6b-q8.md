# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `6642260d55a1`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.0.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 8113.59 ± 11.06 | 8403.74 ± 15.36 | -3.45% | 205.83 ± 0.37 | 200.40 ± 1.78 | +2.71% |
| 256 | 9597.54 ± 9.18 | 10342.50 ± 5.95 | -7.20% | 201.24 ± 0.14 | 190.23 ± 2.50 | +5.79% |
| 512 | 9336.08 ± 10.89 | 10058.15 ± 7.75 | -7.18% | 193.67 ± 0.07 | 183.16 ± 0.43 | +5.74% |
| 1024 | 8572.98 ± 9.57 | 9384.17 ± 10.48 | -8.64% | 179.59 ± 0.14 | 171.37 ± 0.65 | +4.80% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
