# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `acaed04bf0f2`; llama.cpp `adfffbe41b2c`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 259.61 ± 0.25 | 235.23 ± 0.49 | +10.36% | 18.94 ± 0.00 | 15.82 ± 0.01 | +19.71% |
| 256 | 260.17 ± 0.10 | 237.04 ± 0.25 | +9.76% | 18.90 ± 0.01 | 15.80 ± 0.00 | +19.60% |
| 512 | 225.12 ± 0.11 | 234.38 ± 0.23 | -3.95% | 18.86 ± 0.01 | 15.72 ± 0.01 | +19.92% |
| 1024 | 222.69 ± 0.11 | 232.77 ± 0.13 | -4.33% | 18.72 ± 0.01 | 15.66 ± 0.00 | +19.54% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
