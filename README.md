<div align = "center">
    <img src = "https://raw.githubusercontent.com/Barath19/barath19.github.io/refs/heads/master/images/cilantro-metal.png" width="300" alt = "Logo" />
</div>

<div align = "center">
    <a href = "https://github.com/kzampog/cilantro/actions/workflows/build.yml/badge.svg">
        <img src = "https://github.com/kzampog/cilantro/actions/workflows/build.yml/badge.svg" alt = "Build Status" />
    </a>
    <a href = "http://cilantro.readthedocs.io/en/latest/?badge=latest">
        <img src = "https://readthedocs.org/projects/cilantro/badge/?version=latest" alt = "Documentation Status" />
    </a>
    <a href = "https://codedocs.xyz/kzampog/cilantro/">
        <img src = "https://codedocs.xyz/kzampog/cilantro.svg" alt = "Documentation" />
    </a>
    <a href = "https://github.com/kzampog/cilantro/blob/master/LICENSE">
        <img src = "https://img.shields.io/github/license/kzampog/cilantro" alt = "License" />
    </a>
</div>

## A Lean and Efficient Library for Point Cloud Data Processing. Now, accelerated using Metal 
`cilantro` is a lean and fast C++ library for working with point cloud data, with emphasis given to the 3D case.
It includes efficient implementations for a variety of common operations, providing a clean API and attempting to minimize the amount of boilerplate code.
The library is extensively templated, enabling operations on data of arbitrary numerical type and dimensionality (where applicable) and featuring a modular/extensible design of the more complex procedures.
At the same time, convenience aliases/wrappers for the most common cases are provided.
A high-level description of `cilantro` can be found in our [technical report](https://arxiv.org/abs/1807.00399).

## Supported functionality
#### Basic operations:
- General dimension kd-trees (using bundled [nanoflann](https://github.com/jlblancoc/nanoflann))
- Surface normal and curvature (robust) estimation from raw point clouds
- General dimension grid-based point cloud resampling
- Principal Component Analysis
- Basic I/O utilities for 3D point clouds (in PLY format, using bundled [tinyply](https://github.com/ddiakopoulos/tinyply)) and Eigen matrices
- RGBD image pair to/from point cloud conversion utilities

#### Clustering:
- General dimension k-means clustering that supports all distance metrics supported by [nanoflann](https://github.com/jlblancoc/nanoflann)
- Spectral clustering based on various graph Laplacian types (using bundled [Spectra](https://github.com/yixuan/spectra))
- Mean-shift clustering with custom kernel support
- Connected component based point cloud segmentation that supports arbitrary point-wise similarity functions
<div align = "center">
    <img src = "https://kzampog.github.io/images/conn_comp.png" width="800" />
</div>

#### Robust model estimation:
- A RANSAC estimator template and instantiations thereof for general dimension:
    - Robust hyperplane estimation
    - Rigid point cloud registration given noisy correspondences

#### Visualization:
- Classical Multidimensional Scaling (using bundled [Spectra](https://github.com/yixuan/spectra) for eigendecompositions)
- A powerful, extensible, and easy to use 3D visualizer

## Dependencies
- [Eigen](http://eigen.tuxfamily.org/index.php?title=Main_Page) (version 3.3 or newer) [**required**]
- [Pangolin](https://github.com/stevenlovegrove/Pangolin) (built with Eigen enabled) [**optional**; needed for visualization modules and most examples]

## Building
`cilantro` is developed and tested on Ubuntu variants (18.04 and newer) using [CMake](https://cmake.org/).
To clone and build the library (with bundled examples), execute the following in a terminal:

```bash
git clone https://github.com/kzampog/cilantro.git
cd cilantro
mkdir build
cd build
cmake ..
make -j
```

### Building for iOS, Simulator and OSX

```bash
cmake .. -G Xcode -DCMAKE_TOOLCHAIN_FILE=../ios.toolchain.cmake -DPLATFORM=SIMULATORARM64 -DBUILD_SHARED_LIBS=OFF -DEigen3_DIR=<path to eigen build folder>

xcodebuild -create-xcframework -library build/libcilantro.a -headers include -output cilantro.xcframework
```


## Documentation
Documentation ([readthedocs.io](http://cilantro.readthedocs.io/en/latest/?badge=latest), [Doxygen API reference](https://codedocs.xyz/kzampog/cilantro/)) is a work in progress.
The short provided examples (built by default) cover a significant part of the library's functionality.
Most of them expect a single command-line argument (path to a point cloud file in PLY format).
One such input is bundled in `examples/test_clouds` for quick testing.

## License
The library is released under the [MIT license](https://github.com/kzampog/cilantro/blob/master/LICENSE).
If you use `cilantro` in your research, please cite our [technical report](https://arxiv.org/abs/1807.00399):
```bib
@inproceedings{zampogiannis2018cilantro,
    author = {Zampogiannis, Konstantinos and Fermuller, Cornelia and Aloimonos, Yiannis},
    title = {cilantro: A Lean, Versatile, and Efficient Library for Point Cloud Data Processing},
    booktitle = {Proceedings of the 26th ACM International Conference on Multimedia},
    series = {MM '18},
    year = {2018},
    isbn = {978-1-4503-5665-7},
    location = {Seoul, Republic of Korea},
    pages = {1364--1367},
    doi = {10.1145/3240508.3243655},
    publisher = {ACM},
    address = {New York, NY, USA}
}
```
