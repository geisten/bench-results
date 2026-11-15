# Current CPU head-to-head: geist vs llama.cpp

Model: `llama-3.2-3b-Q4_K_M.gguf` (`6c1a2b41161032677be168d354123594c0e6e67d2b9227c84f296ad037c728ff`)

geist `7765b16fc97f`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 249.99 ± 0.09 | 213.48 ± 0.03 | +17.10% | 53.53 ± 0.03 | 56.75 ± 0.15 | -5.67% |
| 256 | 245.52 ± 0.14 | 212.98 ± 0.10 | +15.28% | 52.09 ± 0.02 | 52.53 ± 0.17 | -0.83% |
| 512 | 235.64 ± 0.10 | 211.36 ± 0.51 | +11.49% | 49.43 ± 0.04 | 49.84 ± 0.22 | -0.83% |
| 1024 | 217.62 ± 0.19 | 202.10 ± 0.98 | +7.68% | 44.39 ± 0.05 | 44.19 ± 0.55 | +0.45% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
