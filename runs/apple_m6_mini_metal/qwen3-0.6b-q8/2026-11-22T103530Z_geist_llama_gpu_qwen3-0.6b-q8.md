# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `7765ee2a075d`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 7982.29 ± 50.87 | 8244.50 ± 27.93 | -3.18% | 201.47 ± 0.67 | 194.65 ± 0.40 | +3.51% |
| 256 | 9421.98 ± 17.32 | 10178.60 ± 15.75 | -7.43% | 197.35 ± 0.06 | 189.38 ± 0.68 | +4.21% |
| 512 | 9183.28 ± 14.09 | 9942.43 ± 20.02 | -7.64% | 189.80 ± 0.02 | 182.84 ± 0.55 | +3.81% |
| 1024 | 8434.06 ± 12.68 | 9277.09 ± 6.40 | -9.09% | 175.91 ± 0.11 | 170.77 ± 0.99 | +3.01% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
