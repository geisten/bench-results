# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.8-27b-q4_0.gguf` (`ede16c7b36e578ca87a8c70e011e4b4633a32c831c0ce76d0f474582384e671d`)

geist `ff31d42364e1`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 251.21 ± 0.61 | 247.90 ± 0.08 | +1.33% | 8.89 ± 0.02 | 9.11 ± 0.00 | -2.33% |
| 256 | 252.63 ± 0.22 | 256.20 ± 0.18 | -1.40% | 8.90 ± 0.02 | 9.10 ± 0.00 | -2.22% |
| 512 | 219.42 ± 0.39 | 251.39 ± 0.16 | -12.72% | 8.96 ± 0.00 | 9.08 ± 0.00 | -1.34% |
| 1024 | 217.71 ± 0.41 | 251.58 ± 0.29 | -13.46% | 8.93 ± 0.00 | 9.05 ± 0.00 | -1.39% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
