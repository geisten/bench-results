# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e4b-Q4_K_M.gguf` (`85a896a047553e842f25297ee5b031d64ff30147d9c4af17b1e4b394cd1fab87`)

geist `7765b16fc97f`; llama.cpp `d81235049384`.

Host profile `apple_m1max`: 8-thread prefill, 7-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M1 Max (8 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 174.10 ± 0.33 | 153.20 ± 2.30 | +13.64% | 32.05 ± 0.12 | 27.12 ± 0.07 | +18.21% |
| 256 | 170.25 ± 1.20 | 152.19 ± 3.73 | +11.86% | 30.77 ± 0.15 | 26.84 ± 0.06 | +14.66% |
| 512 | 156.67 ± 2.36 | 149.85 ± 5.99 | +4.56% | 28.39 ± 0.10 | 26.28 ± 0.06 | +8.03% |
| 1024 | 143.34 ± 1.42 | 142.53 ± 3.83 | +0.56% | 26.88 ± 0.07 | 26.07 ± 0.09 | +3.09% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
