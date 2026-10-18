# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e4b-Q4_K_M.gguf` (`85a896a047553e842f25297ee5b031d64ff30147d9c4af17b1e4b394cd1fab87`)

geist `c993379b0746`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 492.90 ± 6.07 | 318.66 ± 1.58 | +54.68% | 26.17 ± 0.05 | 22.97 ± 0.05 | +13.92% |
| 256 | 499.90 ± 6.02 | 324.42 ± 1.90 | +54.09% | 26.17 ± 0.07 | 22.84 ± 0.04 | +14.58% |
| 512 | 492.44 ± 5.58 | 331.76 ± 2.12 | +48.43% | 26.11 ± 0.04 | 22.59 ± 0.09 | +15.56% |
| 1024 | 486.08 ± 5.92 | 327.80 ± 1.07 | +48.29% | 25.98 ± 0.06 | 22.42 ± 0.04 | +15.91% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
