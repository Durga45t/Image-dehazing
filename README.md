# Image Dehazing using Multi-Scale Fusion

A MATLAB implementation for removing haze and fog from images using fusion-based approach.

## Overview

This project enhances hazy images by intelligently combining multiple preprocessing techniques:
- Corrects color cast using white balance
- Improves contrast and visibility
- Uses weight maps to select best parts from each enhanced version
- Applies multi-scale pyramid fusion for seamless results

## Requirements

- MATLAB R2018b or later
- Image Processing Toolbox

## Usage

```matlab
% Simply run the main script
main
```

The script will:
1. Load a hazy image
2. Generate two enhanced versions (white-balanced & contrast-enhanced)
3. Calculate weight maps (luminance, chromatic, saliency)
4. Fuse them using pyramid blending
5. Display the dehazed result

## How It Works

**Step 1: Preprocessing**
- White balance removes color cast (Gray World assumption)
- Contrast enhancement improves visibility (adaptive gamma)

**Step 2: Weight Map Generation**
- Luminance map: measures color variance
- Chromatic map: measures saturation
- Saliency map: identifies important regions
- Combined via multiplication for strict selection

**Step 3: Multi-Scale Fusion**
- Creates 5-level pyramids for smooth blending
- Combines inputs based on weight maps
- Reconstructs final dehazed image

## Project Structure

```
├── main.m                    # Main dehazing pipeline
├── whiteBalance.m            # Gray World color correction
├── enhanceContrast.m         # Adaptive contrast enhancement
├── luminanceWeightmap.m      # Color variance measure
├── chromaticWeightmap.m      # Saturation measure
├── saliencyWeightmap.m       # Visual importance measure
├── genPyr.m                  # Pyramid generation
├── pyr_reduce.m              # Downsample operations
├── pyr_expand.m              # Upsample operations
└── pyrReconstruct.m          # Pyramid reconstruction
```

## Key Algorithms

### White Balance (Gray World)
Assumes natural scenes average to gray color:
```matlab
gray_value = mean([R_avg, G_avg, B_avg])
scale = gray_value / channel_avg
```

### Weight Maps
- **Luminance**: Standard deviation of RGB from mean
- **Chromatic**: Gaussian function centered at max saturation
- **Saliency**: Difference from average after Gaussian smoothing

### Fusion
Weighted combination at multiple scales prevents visible seams:
```matlab
Fused = Detail1 × Weight1 + Detail2 × Weight2
```

## Parameters

Adjustable in the code:
- `sigma = 0.3` - Saturation weighting strictness
- `levels = 5` - Number of pyramid levels
- `gamma = 2*(0.5 + avgLuminance)` - Adaptive enhancement strength

## Applications

- Landscape photography in foggy conditions
- Outdoor surveillance systems
- Autonomous vehicle vision
- Satellite and aerial imagery

## Author

[Durga Prasad] - [https://github.com/Durga45t]

---

*This project demonstrates image processing techniques including haze removal, color correction, weight map fusion, and multi-scale pyramid blending.*
