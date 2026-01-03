# Nano Banana Pro - Photo Editing & Restoration

**Source Repository:** https://github.com/ZeroLu/awesome-nanobanana-pro

## Description

Prompts for photo editing tasks including composition adjustment, object removal, and surveillance simulation.

## Table of Contents

1. [Composition Rescue (Smart Outpainting)](#61-composition-rescue-smart-outpainting)
2. [Smart Crowd Removal](#62-smart-crowd-removal)
3. [Face Detection CCTV Simulation](#63-face-detection-cctv-simulation)

---

## 6.1. Composition Rescue (Smart Outpainting)

**Description:** Expands image ratios (e.g., to 16:9) by intelligently generating matching scenery.

**Prompt:**
```text
Zoom out and expand this image to a 16:9 aspect ratio (computer wallpaper size). Context Awareness : Seamlessly extend the scenery on both left and right sides. Match the original lighting, weather, and texture perfectly. Logical Completion : If there are cut-off objects (like a shoulder, a tree branch, or a building edge) on the borders, complete them naturally based on logical inference. Do not distort the original center image.
```

**Source:** [WeChat Article](https://mp.weixin.qq.com/s/lrYNbs4rGs3KOqewoZ6aNQ)

---

## 6.2. Smart Crowd Removal

**Description:** Removes unwanted people from backgrounds and fills the space with logical textures.

**Prompt:**
```text
Remove all the tourists/people in the background behind the main subject. Intelligent Fill : Replace them with realistic background elements that logically fit the scene (e.g., extend the cobblestone pavement, empty park benches, or grass textures). Consistency : Ensure no blurry artifacts or 'smudges' remain. The filled area must have the same grain, focus depth, and lighting as the rest of the photo.
```

**Source:** [WeChat Article](https://mp.weixin.qq.com/s/lrYNbs4rGs3KOqewoZ6aNQ)

---

## 6.3. Face Detection CCTV Simulation

**Description:** Create a high angle CCTV surveillance shot with face detection.

**Prompt:**
```text
Create a high angle CCTV surveillance shot using the uploaded image as the source. Detect every visible person in the image and automatically draw a white rectangular bounding box around each face. For the most prominent person, add a large zoom in inset: a sharp, enhanced close-up of their face displayed in a floating rectangular frame connected with a thin white line.Keep the main image slightly noisy and security camera like (soft grain, slight distortion, muted colors), while the zoom in face box should be clearer, brighter, and more detailed. No text, no timestamps, no overlays except the boxes and connecting line. Maintain the original scene layout, angle, and environment of the uploaded image.
```

**Source:** [@egeberkina](https://x.com/egeberkina/status/1994804061024010628)
