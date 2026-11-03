# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `57f58a18c43f`; llama.cpp `adfffbe41b2c`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.0.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 256.88 ± 0.33 | 235.57 ± 0.28 | +9.05% | 18.94 ± 0.01 | 16.01 ± 0.01 | +18.27% |
| 256 | 259.98 ± 0.21 | 236.87 ± 0.10 | +9.76% | 18.92 ± 0.01 | 16.01 ± 0.01 | +18.18% |
| 512 | 224.75 ± 0.07 | 234.15 ± 0.26 | -4.01% | 18.85 ± 0.01 | 15.93 ± 0.01 | +18.30% |
| 1024 | 222.33 ± 0.05 | 232.70 ± 0.15 | -4.46% | 18.72 ± 0.01 | 15.86 ± 0.01 | +18.03% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
