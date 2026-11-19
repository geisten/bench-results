# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `f261cadcf982`; llama.cpp `adfffbe41b2c`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 256.19 ± 0.28 | 234.34 ± 0.20 | +9.33% | 18.92 ± 0.01 | 16.11 ± 0.02 | +17.47% |
| 256 | 258.91 ± 0.24 | 235.75 ± 0.23 | +9.82% | 18.88 ± 0.01 | 16.09 ± 0.01 | +17.32% |
| 512 | 223.88 ± 0.21 | 232.49 ± 0.41 | -3.70% | 18.82 ± 0.02 | 16.02 ± 0.01 | +17.50% |
| 1024 | 221.50 ± 0.08 | 230.84 ± 0.29 | -4.05% | 18.69 ± 0.01 | 15.96 ± 0.00 | +17.15% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
