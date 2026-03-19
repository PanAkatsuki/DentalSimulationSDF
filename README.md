# 🦷 Dental Simulation System – SDF-Based Cutting

A real-time **dental cutting simulation system** based on **Signed Distance Fields (SDF)** and **haptic interaction**, designed for interactive medical simulation and training.

> 🎯 Goal: Simulate realistic tooth drilling with real-time volumetric updates and dynamic surface reconstruction.

---

## 📖 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [System Architecture](#system-architecture)
- [Demo](#demo)
- [Environment & Requirements](#environment--requirements)
- [How It Works](#how-it-works)
- [Author](#author)
- [License](#license)

---

## Overview

This project implements a **real-time dental simulation system** using a voxel-based **Signed Distance Field (SDF)** representation.

Instead of traditional mesh deformation, the system directly modifies volumetric data to simulate material removal, enabling stable and robust cutting behavior.

With this system, you can:

- Perform real-time tooth drilling simulation  
- Dynamically update geometry using SDF  
- Reconstruct surfaces using Marching Cubes  
- Support interactive input and haptic feedback  

---

## Features

✅ SDF-based volumetric representation  
- Voxel grid stores signed distance values  
- Robust inside–outside queries  

✅ Real-time cutting simulation  
- Localized SDF updates simulate material removal  
- Efficient partial updates for interactive performance  

✅ Dynamic mesh reconstruction  
- Surface extracted using Marching Cubes  
- Updated in real time after each operation  

✅ Haptic interaction  
- Supports force feedback devices  
- Interaction based on SDF and triangle geometry  

✅ Acceleration structures  
- BVH for efficient collision detection  
- Optimized tool–surface interaction  

---

## System Architecture

```
DentalSimulationSDF/
├── Source/
│ ├── Tooth/ # Tooth representation
│ │ └── ToothSDFVolume # SDF volume data
│ ├── Haptic/ # Haptic interaction system
│ │ ├── HapticSDFManager
│ │ └── HapticTriangleManager
│ ├── Simulation/ # Core simulation logic
│ │ ├── PhantomManager
│ │ ├── Drill
│ │ └── SnapshotSDFVolume
│ ├── Geometry/ # Geometry processing
│ │ ├── MarchingCubes
│ │ └── MeshTriangle
│ └── Acceleration/ # Spatial structures
│ └── BVH
├── Content/
├── Config/
├── DentalSimu.uproject
└── README.md
```

---

## Demo

> 📺 (Add your demo video or GIF here)

Example:
- Tooth before cutting  
- Real-time drilling interaction  
- Reconstructed mesh surface  

---

## Environment & Requirements

| Component | Version | Notes |
|------------|----------|-------|
| Unreal Engine | 5.x | Required |
| OS | Windows | Tested |
| C++ | C++17+ | Core language |
| IDE | Visual Studio | Recommended |

---

## How It Works

1. Convert tooth mesh into a voxel-based SDF representation  
2. Detect interaction between drill and tooth surface  
3. Apply localized SDF modification (cut operation)  
4. Reconstruct surface using Marching Cubes  
5. Render updated mesh in real time  

---

## Author

**Xiaoyu Zhang**

🔗 GitHub: https://github.com/PanAkatsuki

---

## License

MIT License

Copyright (c) 2026 PanAkatsuki

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files...