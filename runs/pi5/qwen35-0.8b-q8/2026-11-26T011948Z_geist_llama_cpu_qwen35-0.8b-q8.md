# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `002ea9d90274`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 117.49 ± 0.28 | 128.09 ± 1.05 | -8.27% | 13.33 ± 0.09 | 12.02 ± 0.15 | +10.90% |
| 256 | 110.22 ± 0.33 | 101.46 ± 0.87 | +8.64% | 13.33 ± 0.04 | 12.03 ± 0.21 | +10.76% |
| 512 | 105.42 ± 0.40 | 94.98 ± 0.72 | +11.00% | 13.26 ± 0.08 | 11.65 ± 0.13 | +13.89% |
| 1024 | 100.31 ± 0.21 | 92.40 ± 0.24 | +8.56% | 13.06 ± 0.09 | 11.13 ± 0.02 | +17.25% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
