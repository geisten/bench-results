# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e4b-Q4_K_M.gguf` (`85a896a047553e842f25297ee5b031d64ff30147d9c4af17b1e4b394cd1fab87`)

geist `7458b37b9531`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 493.68 ± 4.73 | 321.15 ± 1.13 | +53.72% | 26.33 ± 0.04 | 22.93 ± 0.04 | +14.79% |
| 256 | 493.62 ± 4.14 | 328.98 ± 1.89 | +50.05% | 26.25 ± 0.04 | 22.77 ± 0.03 | +15.29% |
| 512 | 490.54 ± 1.64 | 334.20 ± 2.41 | +46.78% | 26.15 ± 0.05 | 22.56 ± 0.01 | +15.93% |
| 1024 | 485.84 ± 3.14 | 329.68 ± 2.01 | +47.37% | 26.02 ± 0.05 | 22.39 ± 0.03 | +16.19% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
