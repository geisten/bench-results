# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `49ffbf5118ee`; llama.cpp `adfffbe41b2c`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 257.00 ± 0.36 | 235.77 ± 0.30 | +9.01% | 19.00 ± 0.00 | 16.09 ± 0.00 | +18.07% |
| 256 | 260.03 ± 0.26 | 237.16 ± 0.27 | +9.64% | 18.97 ± 0.00 | 16.08 ± 0.00 | +17.93% |
| 512 | 224.82 ± 0.07 | 234.54 ± 0.18 | -4.15% | 18.92 ± 0.01 | 16.01 ± 0.01 | +18.22% |
| 1024 | 222.26 ± 0.03 | 232.82 ± 0.08 | -4.54% | 18.79 ± 0.01 | 15.94 ± 0.01 | +17.84% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
