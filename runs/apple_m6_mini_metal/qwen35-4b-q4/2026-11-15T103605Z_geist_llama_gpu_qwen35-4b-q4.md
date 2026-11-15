# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-4b-q4_0.gguf` (`298fcb5fe7a77ccc79745ae24751560c5ac56874caff4bb39b1f2055bd72b8bb`)

geist `9287d0c3734e`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1388.66 ± 1.58 | 1381.16 ± 1.85 | +0.54% | 50.06 ± 0.01 | 50.29 ± 0.03 | -0.46% |
| 256 | 1523.42 ± 2.14 | 1470.74 ± 0.43 | +3.58% | 49.96 ± 0.01 | 49.99 ± 0.03 | -0.06% |
| 512 | 1535.90 ± 0.52 | 1427.45 ± 4.62 | +7.60% | 49.79 ± 0.03 | 49.69 ± 0.03 | +0.20% |
| 1024 | 1532.75 ± 0.77 | 1430.28 ± 2.85 | +7.16% | 49.42 ± 0.01 | 49.44 ± 0.03 | -0.05% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
