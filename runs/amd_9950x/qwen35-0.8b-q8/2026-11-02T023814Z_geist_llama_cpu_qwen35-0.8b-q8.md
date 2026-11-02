# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `f83e03b37679`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1699.21 ± 13.05 | 992.26 ± 15.27 | +71.25% | 81.84 ± 0.33 | 68.78 ± 0.23 | +18.99% |
| 256 | 1730.60 ± 17.55 | 1043.13 ± 9.69 | +65.90% | 81.96 ± 0.30 | 70.46 ± 0.52 | +16.32% |
| 512 | 1738.36 ± 12.03 | 1012.64 ± 21.71 | +71.67% | 81.48 ± 0.31 | 69.85 ± 0.92 | +16.65% |
| 1024 | 1736.92 ± 5.12 | 988.07 ± 31.49 | +75.79% | 80.96 ± 0.34 | 68.59 ± 0.53 | +18.03% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
