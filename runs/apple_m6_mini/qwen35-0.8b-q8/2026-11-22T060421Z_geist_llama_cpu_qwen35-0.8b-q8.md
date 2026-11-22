# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 984.73 ± 1.40 | 923.02 ± 3.48 | +6.69% | 142.04 ± 0.13 | 133.89 ± 0.28 | +6.09% |
| 256 | 979.89 ± 0.77 | 901.52 ± 3.28 | +8.69% | 141.03 ± 0.21 | 132.14 ± 0.26 | +6.73% |
| 512 | 965.91 ± 0.66 | 879.19 ± 5.89 | +9.86% | 138.63 ± 0.20 | 130.78 ± 0.38 | +6.00% |
| 1024 | 933.04 ± 2.07 | 849.39 ± 7.60 | +9.85% | 133.85 ± 0.21 | 128.59 ± 0.36 | +4.09% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
