# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `d231cb8104bc`; llama.cpp `adfffbe41b2c`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 280.83 ± 0.22 | 235.32 ± 0.33 | +19.34% | 18.94 ± 0.00 | 15.84 ± 0.01 | +19.57% |
| 256 | 279.68 ± 0.20 | 236.97 ± 0.09 | +18.02% | 18.90 ± 0.01 | 15.82 ± 0.00 | +19.44% |
| 512 | 279.76 ± 0.29 | 234.05 ± 0.24 | +19.53% | 18.86 ± 0.00 | 15.74 ± 0.01 | +19.78% |
| 1024 | 286.22 ± 0.13 | 232.75 ± 0.30 | +22.97% | 18.73 ± 0.01 | 15.68 ± 0.00 | +19.45% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
