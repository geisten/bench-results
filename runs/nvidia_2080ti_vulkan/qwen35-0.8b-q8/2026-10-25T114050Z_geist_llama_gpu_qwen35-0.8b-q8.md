# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `d95bf356d2f7`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on AMD Ryzen 9 9950X 16-Core Processor (RADV RAPHAEL_MENDOCINO), same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 103.85 ± 0.02 | 325.31 ± 0.02 | -68.08% | 47.00 ± 0.03 | 42.98 ± 0.06 | +9.34% |
| 256 | 100.92 ± 0.02 | 329.28 ± 0.03 | -69.35% | 48.11 ± 0.03 | 42.73 ± 0.04 | +12.60% |
| 512 | 94.35 ± 0.03 | 300.14 ± 0.03 | -68.56% | 47.53 ± 0.03 | 42.62 ± 0.04 | +11.53% |
| 1024 | 82.99 ± 0.06 | 297.62 ± 0.03 | -72.11% | 46.50 ± 0.05 | 42.23 ± 0.03 | +10.13% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
