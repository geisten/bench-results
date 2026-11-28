# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `0b0ee998e552`; llama.cpp `adfffbe41b2c`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 279.29 ± 0.53 | 234.30 ± 0.35 | +19.21% | 18.74 ± 0.01 | 15.62 ± 0.01 | +19.91% |
| 256 | 278.66 ± 0.32 | 235.74 ± 0.32 | +18.21% | 18.70 ± 0.01 | 15.61 ± 0.00 | +19.79% |
| 512 | 278.54 ± 0.06 | 232.53 ± 0.11 | +19.78% | 18.66 ± 0.01 | 15.54 ± 0.00 | +20.05% |
| 1024 | 284.84 ± 0.08 | 231.03 ± 0.18 | +23.29% | 18.54 ± 0.00 | 15.47 ± 0.01 | +19.80% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
