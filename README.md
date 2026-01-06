# Video Frame Interpolation with Lightweight U-Net

A simple yet effective U-Net model for video frame interpolation, trained on the Vimeo-90K dataset. It generates high-quality intermediate frames to smoothly upsample video frame rates (e.g., 30 → 60 FPS) while preserving motion continuity and minimizing artifacts.

**Key Results**
- Validation PSNR: **28.5 dB**
- Loss: L1 + 0.2×LPIPS (perceptual)
- Mixed-precision training with gradient clipping for stable convergence

## Live Demo
Try the CPU-only Gradio app deployed on Hugging Face Spaces:  
[https://huggingface.co/spaces/your-username/video-frame-interpolation-demo](https://huggingface.co/spaces/your-username/video-frame-interpolation-demo)  
*(Replace with your actual Space link)*

Upload any video, interpolate frames, and download the smoother version with original audio preserved.

## Demo Comparison

### Original (30 FPS) vs Interpolated (60 FPS)

| Original Video | Interpolated Video (2× smoother) |
|---------------|--------------------------------|
| <video src="original_video.mp4" controls muted width="400"></video> | <video src="interpolated_video_with_audio.mp4" controls width="400"></video> |

*(Embed your actual video files or use side-by-side GIFs/embedded videos here)*

## Model Architecture
- Lightweight U-Net with double convolutions (GELU activation)
- Input: Concatenated frame1 + frame2 (6 channels)
- Output: Predicted middle frame (3 channels)
- Skip connections and transpose convolutions for precise alignment

## Training Details
- Dataset: Vimeo-90K triplet (subsets used for faster iteration)
- Optimizer: Adam (lr=1e-4)
- Scheduler: ReduceLROnPlateau
- Early stopping + best model checkpointing

## Inference Usage
The provided script includes:
- Loading a video
- Interpolating frames pairwise
- Doubling FPS while keeping original speed
- Re-adding original audio via ffmpeg

Perfect for creating buttery-smooth slow-motion or frame-rate upsampling effects.

Enjoy smoother videos! 🚀
