# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e4b-Q4_K_M.gguf` (`85a896a047553e842f25297ee5b031d64ff30147d9c4af17b1e4b394cd1fab87`)

geist `af6689407a1d`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 358.51 ± 3.47 | 279.04 ± 4.14 | +28.48% | 25.77 ± 0.02 | 22.55 ± 0.14 | +14.31% |
| 256 | 361.86 ± 2.51 | 284.12 ± 1.80 | +27.36% | 25.67 ± 0.05 | 22.42 ± 0.05 | +14.47% |
| 512 | 362.52 ± 3.56 | 290.73 ± 3.42 | +24.69% | 25.58 ± 0.04 | 22.25 ± 0.01 | +14.97% |
| 1024 | 357.46 ± 4.45 | 288.87 ± 6.19 | +23.74% | 25.53 ± 0.03 | 22.14 ± 0.13 | +15.29% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
