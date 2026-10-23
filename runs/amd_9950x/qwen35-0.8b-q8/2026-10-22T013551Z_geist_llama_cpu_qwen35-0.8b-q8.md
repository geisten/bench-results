# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `f19377734f16`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1683.04 ± 19.85 | 982.36 ± 5.92 | +71.33% | 81.09 ± 0.39 | 69.78 ± 0.31 | +16.22% |
| 256 | 1718.45 ± 10.44 | 1005.85 ± 13.46 | +70.85% | 81.35 ± 0.64 | 70.39 ± 0.24 | +15.57% |
| 512 | 1725.64 ± 8.58 | 1023.94 ± 11.08 | +68.53% | 81.24 ± 0.48 | 69.63 ± 1.12 | +16.68% |
| 1024 | 1722.15 ± 8.40 | 1017.23 ± 5.60 | +69.30% | 81.23 ± 0.58 | 68.80 ± 0.58 | +18.08% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
