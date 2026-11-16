# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `99e847f1c898`; llama.cpp `adfffbe41b2c`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 255.90 ± 0.32 | 234.82 ± 0.51 | +8.97% | 18.88 ± 0.00 | 16.05 ± 0.01 | +17.65% |
| 256 | 258.81 ± 0.24 | 235.77 ± 0.18 | +9.77% | 18.85 ± 0.01 | 16.03 ± 0.01 | +17.57% |
| 512 | 223.84 ± 0.06 | 232.50 ± 0.53 | -3.72% | 18.80 ± 0.00 | 15.96 ± 0.00 | +17.82% |
| 1024 | 221.22 ± 0.02 | 231.19 ± 0.20 | -4.31% | 18.66 ± 0.00 | 15.89 ± 0.01 | +17.47% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
