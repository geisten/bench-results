# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.8-27b-q4_0.gguf` (`ede16c7b36e578ca87a8c70e011e4b4633a32c831c0ce76d0f474582384e671d`)

geist `6642260d55a1`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.0.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 251.19 ± 0.15 | 248.46 ± 0.21 | +1.10% | 9.06 ± 0.00 | 9.18 ± 0.00 | -1.35% |
| 256 | 253.51 ± 0.16 | 256.49 ± 0.14 | -1.17% | 9.05 ± 0.00 | 9.18 ± 0.00 | -1.40% |
| 512 | 219.92 ± 0.21 | 252.16 ± 0.21 | -12.78% | 9.04 ± 0.00 | 9.16 ± 0.00 | -1.37% |
| 1024 | 218.10 ± 0.09 | 252.21 ± 0.44 | -13.53% | 9.00 ± 0.00 | 9.13 ± 0.00 | -1.40% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
