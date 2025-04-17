
# ForensicVision: GPU-Accelerated Image Enhancement

ForensicVision is a CUDA-based application designed to enhance degraded images using GPU acceleration for forensic analysis. This system implements several image processing techniques to improve the quality of images captured from CCTV footage, crime scenes, or fingerprint scans.

## Problem Statement

Crime investigations often rely on images that are frequently degraded by noise, low resolution, motion blur, or poor lighting, making it difficult to extract crucial details. Traditional image processing techniques on CPUs can be slow and inefficient for large datasets, especially when time is critical in investigations.

## Solution

ForensicVision leverages parallel computing power through NVIDIA CUDA to significantly reduce processing time compared to conventional CPU-based approaches. The system provides multiple image enhancement techniques that can be applied to forensic images to improve their clarity and extract more details.

## Features

### 1. Image Rotation
- Rotates images by a user-defined angle
- Uses trigonometric transformations for accurate pixel repositioning
- Preserves image quality during rotation
- Implementation leverages GPU parallelism by assigning each pixel to a separate thread

### 2. Gaussian Blur
- Smooths images to reduce noise
- Uses a customizable Gaussian kernel for convolution
- Adjustable sigma value to control blur intensity
- Optimized through parallel convolution on GPU

### 3. Edge Detection (Sobel Operator)
- Detects edges using horizontal and vertical gradient calculations
- Utilizes Sobel kernels to highlight image contours
- Enhances visibility of details and boundaries
- Parallel processing of image gradients

### 4. Median Filter (Noise Reduction)
- Removes salt-and-pepper noise effectively
- Uses a sliding window to replace each pixel with the median of its neighbors
- Customizable window size
- Parallel implementation significantly speeds up the typically slow median filter operation

### 5. Morphological Dilation
- Expands bright regions in binary or grayscale images
- Enhances object visibility and fills small gaps
- Customizable structuring element size
- Parallel processing for each pixel

### 6. Morphological Erosion
- Shrinks bright regions in images
- Removes small noise particles and refines edges
- Customizable structuring element size
- Efficient parallel implementation

## Performance Optimization

### Parallel Processing Benefits

ForensicVision delivers significant performance improvements over traditional CPU-based image processing through several key optimizations:

#### Computational Speedup
- **Processing Time Reduction**: Achieves up to 50-100x speedup compared to sequential CPU implementations, particularly for larger images
- **Real-time Processing**: Enables near real-time processing of high-resolution forensic images, critical for time-sensitive investigations

#### Scalability Advantages
- **Image Size Scalability**: Performance scales efficiently with larger images due to the parallel architecture
- **Kernel Size Independence**: Processing time remains relatively stable even with larger convolution kernels (for operations like Gaussian blur)
- **Resolution Flexibility**: Handles images of varying resolutions with consistent performance characteristics

#### Resource Utilization
- **Thread Organization**: Optimized thread block dimensions (16x16) maximize GPU occupancy
- **Memory Coalescing**: Structured access patterns improve memory bandwidth utilization
- **Dynamic Resource Allocation**: Adapts to available GPU resources for optimal performance

#### Algorithm-Specific Optimizations
- **Rotation**: Parallel transformation of all pixels simultaneously instead of sequential processing
- **Convolution Operations**: 2D thread blocks process multiple pixels concurrently, dramatically accelerating filtering operations
- **Median Filtering**: Parallel window operations eliminate the sequential bottleneck typical in CPU implementations
- **Morphological Operations**: Simultaneous processing of all pixels with local neighborhood operations

### Implementation Efficiency
- **Memory Management**: Efficient host-to-device and device-to-host transfers minimize data movement overhead
- **Thread Divergence Minimization**: Carefully designed branching logic reduces warp divergence
- **Shared Memory Utilization**: Optimized data sharing between threads in the same block

## Input and Output

- **Input**: PGM (Portable Gray Map) images with user-defined parameters (e.g., rotation angle, kernel size)
- **Output**: Enhanced images saved in PGM format

## Use Cases

1. **CCTV Footage Enhancement**: Improve low-quality surveillance footage to identify suspects or vehicles
2. **Fingerprint Processing**: Enhance fingerprint scans for better ridge detection and matching
3. **Document Examination**: Improve readability of degraded or damaged documents
4. **Crime Scene Photography**: Enhance details in photographs taken under poor lighting conditions
5. **Ballistics Imaging**: Improve images of ballistic markings for more accurate comparison and analysis

## Future Work

- Implementation of additional image enhancement techniques such as contrast enhancement and deblurring
- Support for additional image formats beyond PGM
- Integration with machine learning algorithms for automated feature detection
- Development of a user-friendly GUI for non-technical investigators
- Extension to multi-GPU environments for handling extremely large images or batch processing
