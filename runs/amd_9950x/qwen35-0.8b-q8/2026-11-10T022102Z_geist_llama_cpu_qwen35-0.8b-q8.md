# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `29a0ce4b5937`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1702.13 ± 7.99 | 995.72 ± 11.58 | +70.94% | 82.10 ± 0.35 | 69.47 ± 0.45 | +18.18% |
| 256 | 1738.09 ± 12.50 | 1031.32 ± 7.49 | +68.53% | 82.19 ± 0.14 | 69.51 ± 0.78 | +18.24% |
| 512 | 1737.28 ± 9.15 | 1046.98 ± 6.00 | +65.93% | 81.95 ± 0.28 | 70.25 ± 0.65 | +16.66% |
| 1024 | 1731.32 ± 6.79 | 1045.35 ± 8.29 | +65.62% | 81.62 ± 0.15 | 68.83 ± 0.57 | +18.59% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
