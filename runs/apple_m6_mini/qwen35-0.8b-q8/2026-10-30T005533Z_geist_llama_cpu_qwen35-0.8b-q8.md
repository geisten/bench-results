# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `50863de30fe7`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.0.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 984.81 ± 1.22 | 923.24 ± 1.49 | +6.67% | 140.54 ± 0.15 | 135.51 ± 0.24 | +3.72% |
| 256 | 979.19 ± 3.86 | 895.91 ± 11.91 | +9.30% | 139.51 ± 0.18 | 133.62 ± 0.28 | +4.41% |
| 512 | 966.29 ± 1.17 | 889.44 ± 4.78 | +8.64% | 137.50 ± 0.08 | 132.29 ± 0.42 | +3.93% |
| 1024 | 934.83 ± 1.11 | 867.71 ± 2.53 | +7.73% | 132.77 ± 0.21 | 130.19 ± 0.34 | +1.98% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
