# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.8-27b-q4_0.gguf` (`ede16c7b36e578ca87a8c70e011e4b4633a32c831c0ce76d0f474582384e671d`)

geist `d46135a24bb6`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 250.27 ± 0.45 | 247.78 ± 0.26 | +1.01% | 8.92 ± 0.01 | 9.11 ± 0.00 | -2.08% |
| 256 | 252.07 ± 0.54 | 255.05 ± 0.33 | -1.17% | 8.89 ± 0.01 | 9.10 ± 0.00 | -2.28% |
| 512 | 218.90 ± 0.11 | 249.34 ± 0.69 | -12.21% | 8.94 ± 0.00 | 9.09 ± 0.00 | -1.59% |
| 1024 | 216.94 ± 0.09 | 249.27 ± 0.70 | -12.97% | 8.92 ± 0.00 | 9.06 ± 0.00 | -1.53% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
