# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `666d971e5db2`; llama.cpp `adfffbe41b2c`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 256.93 ± 0.23 | 235.23 ± 0.34 | +9.22% | 18.90 ± 0.01 | 15.94 ± 0.01 | +18.59% |
| 256 | 259.86 ± 0.22 | 236.80 ± 0.23 | +9.74% | 18.87 ± 0.01 | 15.92 ± 0.01 | +18.51% |
| 512 | 224.72 ± 0.19 | 234.22 ± 0.40 | -4.05% | 18.82 ± 0.01 | 15.84 ± 0.01 | +18.80% |
| 1024 | 222.21 ± 0.09 | 232.43 ± 0.24 | -4.40% | 18.68 ± 0.01 | 15.76 ± 0.03 | +18.57% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
