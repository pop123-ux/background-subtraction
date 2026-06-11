# Background Subtraction Algorithms

A comparative study of three background subtraction algorithms from OpenCV, applied to video surveillance footage. Each algorithm isolates moving objects (foreground) from a static background using different statistical approaches.

This project is the theoretical companion to [motion-detector](https://github.com/pop123-ux/motion-detector), which applies MOG2 in a real-time webcam-based motion detection system.

![Python](https://img.shields.io/badge/Python-3.8+-blue?logo=python&logoColor=white)
![OpenCV](https://img.shields.io/badge/OpenCV-4.x-5C3EE8?logo=opencv&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter&logoColor=white)

---

## Algorithms Compared

| Algorithm | Method | Shadow Detection | Init Frames | Best For |
|-----------|--------|:---:|:---:|---------|
| **MOG2** | Mixture of Gaussians (adaptive K) | Yes | None | General-purpose, dynamic scenes |
| **MOG** | Mixture of Gaussians (fixed K) | No | None | Simpler scenes, lower compute |
| **GMG** | Bayesian segmentation | No | ~120 | Stable cameras, long-running feeds |

### MOG2 (Mixture of Gaussians v2)

Models each pixel as a mixture of Gaussians with an adaptive number of components. Includes built-in shadow detection — shadows appear gray in the foreground mask rather than white, allowing you to distinguish actual moving objects from their shadows.

### MOG (Mixture of Gaussians v1)

The original Gaussian Mixture Model approach. Uses a fixed number of Gaussian distributions per pixel. Simpler and faster than MOG2 but less robust to lighting changes and lacks shadow detection.

### GMG (Geometric Multigrid)

Uses Bayesian inference over the first N frames to build a background model, then applies probabilistic foreground detection. Requires an initialization period (~120 frames) before producing valid masks. Best combined with morphological operations to reduce noise.

## Project Structure

```
background-subtraction/
├── code.ipynb        # Jupyter notebook comparing all three algorithms
├── sample_vid.mp4    # Sample surveillance video for testing
└── README.md
```

## Usage

```bash
pip install opencv-python opencv-contrib-python numpy jupyter
jupyter notebook code.ipynb
```

Run each cell to see the foreground mask and original video side by side. Press `q` to stop playback.

## Key Takeaways

- **MOG2** is the best default choice — adaptive, handles shadows, works out of the box
- **MOG** is lighter but less accurate in complex scenes
- **GMG** needs a warm-up period but produces cleaner masks for long-running surveillance feeds
- Morphological operations (opening, dilation) significantly improve mask quality across all methods

## Related

- [motion-detector](https://github.com/pop123-ux/motion-detector) — Real-time webcam motion detection using MOG2 with contour detection and bounding boxes

## License

MIT
