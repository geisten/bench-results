# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `6642260d55a1`; llama.cpp `adfffbe41b2c`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.0.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 256.61 ± 0.45 | 235.24 ± 0.35 | +9.08% | 19.05 ± 0.01 | 16.24 ± 0.02 | +17.27% |
| 256 | 259.94 ± 0.23 | 237.12 ± 0.14 | +9.63% | 19.01 ± 0.01 | 16.23 ± 0.01 | +17.08% |
| 512 | 224.80 ± 0.08 | 234.32 ± 0.21 | -4.06% | 18.97 ± 0.01 | 16.16 ± 0.01 | +17.32% |
| 1024 | 222.23 ± 0.06 | 232.71 ± 0.07 | -4.51% | 18.83 ± 0.00 | 16.09 ± 0.01 | +17.04% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
