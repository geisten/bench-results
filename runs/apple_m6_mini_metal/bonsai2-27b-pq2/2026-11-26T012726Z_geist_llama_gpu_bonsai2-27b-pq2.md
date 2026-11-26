# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `002ea9d90274`; llama.cpp `adfffbe41b2c`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 280.74 ± 0.33 | 235.62 ± 0.31 | +19.15% | 18.93 ± 0.01 | 15.79 ± 0.01 | +19.87% |
| 256 | 279.48 ± 0.39 | 236.99 ± 0.07 | +17.93% | 18.89 ± 0.01 | 15.78 ± 0.01 | +19.74% |
| 512 | 280.00 ± 0.14 | 234.31 ± 0.21 | +19.50% | 18.84 ± 0.01 | 15.70 ± 0.00 | +20.01% |
| 1024 | 286.52 ± 0.06 | 232.76 ± 0.10 | +23.10% | 18.72 ± 0.01 | 15.63 ± 0.01 | +19.73% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
