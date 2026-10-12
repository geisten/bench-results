# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `4d6e2696a51b`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 950.50 ± 7.69 | 984.85 ± 11.79 | -3.49% | 81.41 ± 0.58 | 70.79 ± 0.45 | +15.00% |
| 256 | 898.14 ± 4.88 | 1019.70 ± 19.10 | -11.92% | 81.82 ± 0.50 | 71.43 ± 0.91 | +14.55% |
| 512 | 866.12 ± 2.80 | 1030.26 ± 5.40 | -15.93% | 82.05 ± 0.19 | 71.30 ± 0.44 | +15.08% |
| 1024 | 848.70 ± 2.24 | 1020.18 ± 5.53 | -16.81% | 81.12 ± 0.20 | 70.68 ± 0.61 | +14.78% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
