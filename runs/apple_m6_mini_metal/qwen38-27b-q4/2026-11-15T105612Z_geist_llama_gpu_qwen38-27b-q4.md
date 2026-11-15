# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.8-27b-q4_0.gguf` (`ede16c7b36e578ca87a8c70e011e4b4633a32c831c0ce76d0f474582384e671d`)

geist `9287d0c3734e`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 250.54 ± 0.54 | 247.43 ± 0.32 | +1.26% | 8.89 ± 0.03 | 9.08 ± 0.01 | -2.02% |
| 256 | 252.35 ± 0.30 | 254.87 ± 0.24 | -0.99% | 8.90 ± 0.02 | 9.07 ± 0.01 | -1.85% |
| 512 | 219.04 ± 0.26 | 249.28 ± 0.69 | -12.13% | 8.93 ± 0.01 | 9.06 ± 0.00 | -1.39% |
| 1024 | 217.17 ± 0.19 | 248.61 ± 0.66 | -12.65% | 8.90 ± 0.01 | 9.03 ± 0.00 | -1.44% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
