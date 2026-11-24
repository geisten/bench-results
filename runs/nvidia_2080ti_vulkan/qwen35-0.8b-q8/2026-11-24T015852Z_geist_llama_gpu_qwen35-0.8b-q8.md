# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `acaed04bf0f2`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 8903.11 ± 34.19 | 8529.20 ± 172.11 | +4.38% | 328.74 ± 1.69 | 310.81 ± 1.04 | +5.77% |
| 256 | 11926.67 ± 81.40 | 11592.55 ± 40.85 | +2.88% | 329.30 ± 0.31 | 285.57 ± 3.38 | +15.31% |
| 512 | 15252.17 ± 21.10 | 12111.85 ± 11.20 | +25.93% | 328.51 ± 0.45 | 292.04 ± 1.60 | +12.49% |
| 1024 | 15051.52 ± 21.22 | 11851.30 ± 19.45 | +27.00% | 327.04 ± 0.16 | 288.83 ± 2.20 | +13.23% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
