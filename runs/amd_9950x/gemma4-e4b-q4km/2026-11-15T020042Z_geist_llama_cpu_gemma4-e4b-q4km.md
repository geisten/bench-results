# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e4b-Q4_K_M.gguf` (`85a896a047553e842f25297ee5b031d64ff30147d9c4af17b1e4b394cd1fab87`)

geist `7765b16fc97f`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 498.47 ± 3.57 | 320.18 ± 1.57 | +55.68% | 26.21 ± 0.04 | 22.88 ± 0.04 | +14.53% |
| 256 | 500.90 ± 2.61 | 327.02 ± 1.36 | +53.17% | 26.16 ± 0.06 | 22.78 ± 0.02 | +14.80% |
| 512 | 497.11 ± 3.42 | 331.72 ± 2.77 | +49.86% | 26.10 ± 0.08 | 22.53 ± 0.04 | +15.86% |
| 1024 | 492.07 ± 4.07 | 327.49 ± 1.98 | +50.25% | 26.01 ± 0.08 | 22.36 ± 0.07 | +16.33% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
