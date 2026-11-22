# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e4b-Q4_K_M.gguf` (`85a896a047553e842f25297ee5b031d64ff30147d9c4af17b1e4b394cd1fab87`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 484.80 ± 4.62 | 315.18 ± 1.66 | +53.81% | 25.99 ± 0.12 | 23.14 ± 0.06 | +12.33% |
| 256 | 493.21 ± 3.73 | 320.52 ± 1.03 | +53.88% | 26.01 ± 0.04 | 22.95 ± 0.05 | +13.36% |
| 512 | 485.80 ± 3.06 | 326.11 ± 1.95 | +48.97% | 25.90 ± 0.04 | 22.71 ± 0.03 | +14.04% |
| 1024 | 482.50 ± 3.96 | 320.97 ± 1.70 | +50.33% | 25.80 ± 0.02 | 22.55 ± 0.07 | +14.40% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
