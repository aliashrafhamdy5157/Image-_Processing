# Classical Computer Vision–Based Jigsaw Puzzle Solver

## Overview

This project investigates the problem of **automatic jigsaw puzzle assembly** using **classical computer vision techniques only**, without employing any machine learning or deep learning methods.

The goal was to segment puzzle images into individual tiles and automatically reconstruct the original image by matching and assembling tiles based on visual compatibility. The project focuses on analyzing the **limitations of hand-crafted visual descriptors and classical optimization algorithms** when applied to this problem.

---

## Problem Description

Given an image of a shuffled jigsaw puzzle:
- Segment the image into individual puzzle pieces.
- Extract meaningful visual features from each piece.
- Estimate pairwise compatibility between puzzle pieces.
- Assemble the puzzle by placing each piece in its correct position.

The solution must rely solely on **classical image processing and computer vision techniques**.

---

## Implemented Pipeline

1. **Image Preprocessing**
   - Color space conversion (RGB, Grayscale, Lab).
   - Noise reduction and normalization.
   - Cropping to enforce even grid dimensions.

2. **Tile Extraction**
   - Puzzle images were sliced into fixed-size tiles (2×2, 4×4, and 8×8 grids).
   - Each tile was treated as an independent candidate puzzle piece.

3. **Feature Extraction**
   - Grayscale intensity profiles along tile edges.
   - Edge gradients (Sobel magnitude).
   - Contour and boundary information.
   - Corner-like responses.
   - Color statistics using Lab color space.
   - Hybrid descriptors combining multiple visual cues.

4. **Pairwise Compatibility Estimation**
   - Sum of Squared Differences (SSD).
   - Normalized Cross-Correlation (NCC).
   - Gradient-based similarity.
   - Structural Similarity Index (SSIM) for evaluation.

5. **Puzzle Assembly Algorithms**
   Multiple classical assembly strategies were explored:
   - Greedy placement
   - Backtracking search
   - Beam search
   - Energy minimization approaches
   - Hungarian (assignment) algorithm
   - Exhaustive brute-force (for 2×2 puzzles)

---

## Challenges Encountered

### 1. Limitations of Grayscale, Edge, and Contour-Based Descriptors

Early approaches relied on **grayscale representations, edges, and contours** to match puzzle pieces.  
While these features capture local shape information, they were **not discriminative enough** to reliably distinguish correct from incorrect tile matches.

Key issues:
- Visually similar edges often appeared between unrelated tiles.
- Smooth or low-texture regions produced ambiguous matches.
- Contour similarity lacked sufficient contextual information.

These weaknesses caused incorrect placements early in the assembly process, which then propagated through the solution.

---

### 2. Failure of Classical Assembly Algorithms

Despite testing a wide range of classical algorithms—including greedy methods, backtracking, beam search, energy-based optimization, and the Hungarian algorithm—none were able to produce robust results at larger puzzle sizes.

This failure was **not due to algorithmic implementation**, but rather due to the **weakness of the underlying matching cost function**:
- When pairwise compatibility scores are ambiguous, even optimal global solvers converge to incorrect solutions.
- Increasing search depth or enforcing global constraints did not compensate for poor local discrimination.

This demonstrated that **algorithmic complexity cannot overcome fundamentally weak visual descriptors**.

---

### 3. Attempts to Strengthen the Descriptor Using Hybrid Features

To address descriptor limitations, several enhancements were explored, resulting in a **hybrid descriptor** that combined:

- Edge intensity profiles
- Gradient magnitude and direction
- Corner response behavior
- Color information in Lab color space
- Boundary texture statistics
- Normalized cross-correlation signals

While these additions improved local matching in some cases, they **failed to consistently resolve ambiguous matches**, particularly in regions with repeated patterns or low visual entropy.

The descriptor still lacked sufficient global context, and improvements remained incremental rather than transformative.

---

## Experimental Results

- **2×2 puzzles**  
  Exhaustive brute-force search successfully reconstructed puzzles with high accuracy.

- **4×4 puzzles**  
  Partial reconstruction was achieved, but accuracy degraded due to error propagation.

- **8×8 puzzles**  
  All classical approaches failed to produce stable global solutions, even with advanced search strategies.

These results highlight the **scaling limitations of classical feature-based puzzle assembly**.

---

## Key Insights and Lessons Learned

- Jigsaw puzzle assembly is fundamentally **descriptor-limited rather than algorithm-limited**.
- Classical hand-crafted features struggle to capture the complex visual relationships needed for large-scale reconstruction.
- Global optimization strategies cannot succeed when local matching cues are weak or ambiguous.
- Robust puzzle assembly likely requires **learned or data-driven representations**, which were intentionally excluded from this project.

---

## Future Work

Potential directions for improving performance include:
- Incorporating learned feature representations (e.g., CNN-based embeddings).
- Using probabilistic graphical models with learned compatibility scores.
- Integrating semantic context to guide global assembly.
- Hybrid classical–learning approaches for feature extraction.

---

## Technologies Used

- Python
- OpenCV
- NumPy
- Matplotlib

---



## Authors

Ali Ashraf Gomma  
Adel Waheed 
ahmed tamer 
asaad ramzy
kerollous bassem
Computer Engineering Student
