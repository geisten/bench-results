# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e4b-Q4_K_M.gguf` (`85a896a047553e842f25297ee5b031d64ff30147d9c4af17b1e4b394cd1fab87`)

geist `6642260d55a1`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 501.04 ± 3.17 | 319.95 ± 2.33 | +56.60% | 26.31 ± 0.02 | 22.99 ± 0.05 | +14.46% |
| 256 | 498.56 ± 6.18 | 328.79 ± 1.74 | +51.63% | 26.21 ± 0.02 | 22.80 ± 0.02 | +14.96% |
| 512 | 499.62 ± 2.21 | 333.52 ± 2.17 | +49.80% | 26.10 ± 0.03 | 22.52 ± 0.05 | +15.91% |
| 1024 | 493.88 ± 2.23 | 329.02 ± 1.93 | +50.11% | 26.04 ± 0.03 | 22.40 ± 0.03 | +16.27% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
