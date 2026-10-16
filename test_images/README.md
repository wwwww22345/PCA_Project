# Image Dataset & Input Preparation (Member 3)

ARTI 503 – Parallel Image Filtering Using Multicore Processing – Stage 1

## Test images

All members must use **these exact files** for benchmarking.

| File | Resolution | Total pixels | File size |
|---|---|---|---|
| small_256x256.png | 256 × 256 | 65,536 | 37 KB |
| medium_512x512.png | 512 × 512 | 262,144 | 136 KB |
| large_1024x1024.png | 1024 × 1024 | 1,048,576 | 401 KB |
| xlarge_2048x2048.png | 2048 × 2048 | 4,194,304 | 1,064 KB |
| xxlarge_4096x4096.png | 4096 × 4096 | 16,777,216 | 2,829 KB |

Each step up has **4× the pixels** of the previous one, so we can see how execution time scales with problem size (as required in the handout: "the input size should be adjustable").

## Agreed input format (for Members 4 and 5)

- **Format:** PNG (lossless, so no compression artifacts affect results)
- **Color:** Grayscale, 1 channel, 8-bit (values 0–255)
- **Source:** "Astronaut" image (Eileen Collins, NASA — public domain), included in the scikit-image library (`skimage.data.astronaut()`), converted to grayscale and resized with Lanczos resampling.
- **Suggested output:** same size as input, uint8 (values clipped to 0–255), saved as PNG.
- **Boundary handling:** to be confirmed with Members 4 and 5 (suggestion: zero padding or edge replication, same for both filters).

## How to load an image

```python
from PIL import Image
import numpy as np

img = np.array(Image.open("large_1024x1024.png"), dtype=np.float32)
print(img.shape)  # (1024, 1024)
```

## Note on very large images

Pure-Python nested loops on the 4096 × 4096 image may take several minutes. If it is too slow on some laptops, the group can agree to benchmark only up to 2048 × 2048 and report 4096 as optional.

## Reference

van der Walt, S. et al. (2014). *scikit-image: image processing in Python.* PeerJ 2:e453.
