# OpenCorr Project Analysis

## Overview
**OpenCorr** is an open-source C++ library for Digital Image Correlation (DIC) and Digital Volume Correlation (DVC). It supports 2D, 3D/stereo DIC, and volumetric DIC.

**Repository**: Open-source, maintained by researchers at South China University of Technology, RIKEN, and BrookHaven National Laboratory.

---

## Project Structure

```
OpenCorr/
├── src/                    # 42 C++ source/header files
├── examples/               # Example programs (2D, 3D, DVC)
├── gpu_lib/                # GPU acceleration library
├── gui_soft/               # GUI application
├── img/                    # Documentation images
├── README.md               # Main documentation
├── 1_Get_started.md
├── 2_Framework.md
├── 3_Data_structures.md
├── 4_Processing_methods.md
├── 5_GPU_acceleration.md
├── 6_Examples.md
└── 7_Software_with_GUI.md
```

---

## Core Modules (src/)

### Data Structures
| File | Purpose |
|------|---------|
| `oc_point.h` | 2D/3D point coordinates, vector operations (dot/cross product) |
| `oc_array.h` | 2D/3D/4D array operations via Eigen matrices |
| `oc_image.h` | Image I/O (2D via OpenCV, 3D volumetric TIFF/binary) |
| `oc_subset.h` | Subset extraction with zero-mean normalization |
| `oc_deformation.h` | 1st/2nd order shape functions, warp matrices |
| `oc_poi.h` | Point of Interest with deformation, results, strain vectors |

### Processing Methods

#### Basic Processing
| Module | Description |
|--------|-------------|
| `Gradient` | 4th-order central difference gradient computation |
| `Interpolation` | Cubic B-spline interpolation (2D/3D) |
| `NearestNeighbor` | KD-tree search via nanoflann |
| `Feature` | SIFT feature extraction/matching (2D/3D) |
| `Calibration` | Camera intrinsic/extrinsic parameters, undistortion |
| `Stereovision` | 3D reconstruction from stereo pairs |

#### DIC Algorithms
| Module | Algorithm | Type |
|--------|-----------|------|
| `FFTCC` | Fast Fourier Cross-Correlation | Coarse search |
| `ICGN` | Inverse Compositional Gauss-Newton | Sub-pixel refinement |
| `ICLM` | Inverse Compositional Levenberg-Marquardt | Sub-pixel refinement |
| `NR` | Newton-Raphson | Sub-pixel refinement |
| `FeatureAffine` | Feature-based affine registration | Hybrid approach |

#### Post-Processing
| Module | Description |
|--------|-------------|
| `Strain` | 2D/3D strain computation from displacement fields |

---

## Key Technologies

- **Eigen**: Linear algebra (matrices, vectors)
- **OpenCV**: Image I/O, SIFT features
- **nanoflann**: Approximate nearest neighbor search
- **CUDA**: GPU acceleration for ICGN
- **OpenMP**: Multi-threaded CPU acceleration

---

## Example Programs

```
examples/
├── test_2d_dic_fftcc_icgn*.cpp     # 2D DIC workflow
├── test_2d_dic_self_adaptive_*.cpp  # Adaptive subset sizing
├── test_2d_dic_gpu_icgn.cpp        # GPU-accelerated 2D DIC
├── test_3d_dic_epipolar_*.cpp      # Stereo DIC with epipolar geometry
├── test_3d_reconstruction_*.cpp    # 3D point cloud reconstruction
├── test_dvc_*.cpp                  # Digital Volume Correlation
└── 2d_dic/, 3d_dic/, dvc/          # Image datasets
```

---

## Dependencies

| Dependency | Version | Purpose |
|------------|---------|---------|
| Eigen | Latest stable | Matrix operations |
| OpenCV | Latest stable | Image processing, SIFT |
| nanoflann | - | KD-tree search |
| CUDA Toolkit | - | GPU acceleration |

---

## Visual Studio Solution (opencorrsln/)

```
opencorrsln/
├── OpenCorr.sln              # Visual Studio solution
├── OpenCorr.vcxproj          # Project file (x64 Debug/Release)
├── OpenCorr.vcxproj.filters  # File organization in IDE
├── Eigen3/                   # Eigen library (header-only)
├── fftw3/                    # FFTW3 library (header+lib)
├── nanoflann/                # nanoflann library
├── opencv4/                  # OpenCV4 library
└── x64/                      # Build outputs (Build/, Debug/, Release/)
```

### Project Configuration
- **Platform**: x64 (Visual Studio 2022, toolset v143)
- **C++ Standard**: C++17
- **Debug Dependencies**: `libfftw3-3.lib`, `opencv_world4100d.lib`
- **Release Dependencies**: `libfftw3-3.lib`, `opencv_world4100.lib`
- **Active Example**: `test_2d_dic_sift_icgn2.cpp`

### Include/Library Paths
| Configuration | Additional Paths |
|--------------|------------------|
| Debug|x64 | Eigen3, fftw3, opencv4, nanoflann |
| Release|x64 | + CUDA Toolkit (cuda/, $(CUDA_PATH)) |

---

## Repository Workflow

| Folder | Purpose |
|--------|---------|
| `src/` | Git repo tracking `origin/main` (https://github.com/dylau/OpenCorr.git) |
| `opencorrsln/` | Development workspace (VS solution, modified sources) |

**Usage:**
- `src/` → sync with upstream via `git pull origin main`
- `opencorrsln/` → actual development and builds
- Compare changes: `diff src/ opencorrsln/OpenCorr/`

---

## Developers
- Dr. JIANG Zhenyu (South China University of Technology)
- Dr. ZHANG Lingqi (RIKEN)
- Dr. WANG Tianyi (BrookHaven National Laboratory)

---

## Contact
- Email: zhenyujiang@scut.edu.cn
- QQ Group: 597895040
- Website: opencorr.org