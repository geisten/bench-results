# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `f4ae43569c6a`; llama.cpp `adfffbe41b2c`.

Host profile `apple_m1max_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M1 Max, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M1 Max (8 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 160.85 ± 0.29 | 141.90 ± 0.05 | +13.35% | 21.73 ± 0.08 | 21.14 ± 0.04 | +2.79% |
| 256 | 166.03 ± 0.16 | 147.36 ± 0.13 | +12.67% | 21.65 ± 0.03 | 20.88 ± 0.27 | +3.68% |
| 512 | 162.19 ± 0.08 | 123.34 ± 9.25 | +31.50% | 21.53 ± 0.12 | 18.65 ± 1.50 | +15.43% |
| 1024 | 161.68 ± 0.06 | 113.17 ± 1.03 | +42.87% | 21.37 ± 0.05 | 17.10 ± 0.22 | +25.01% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
