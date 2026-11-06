# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `406a3c0519ec`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1711.88 ± 24.66 | 990.59 ± 8.00 | +72.82% | 82.07 ± 0.21 | 69.20 ± 0.32 | +18.59% |
| 256 | 1732.00 ± 9.82 | 1043.58 ± 7.74 | +65.97% | 81.93 ± 0.10 | 69.59 ± 0.68 | +17.74% |
| 512 | 1734.34 ± 9.83 | 1044.62 ± 11.35 | +66.03% | 81.65 ± 0.22 | 69.39 ± 1.03 | +17.66% |
| 1024 | 1727.11 ± 8.29 | 1035.84 ± 11.16 | +66.73% | 81.33 ± 0.18 | 69.39 ± 0.70 | +17.20% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
