# 🦷 Dental Simulation System – SDF-Based Cutting

A real-time dental cutting simulation system based on **Signed Distance Fields (SDF)** and **haptic interaction**, designed for interactive medical simulation and training.

> 🎯 Goal: Simulate realistic tooth drilling with real-time volumetric updates, dynamic surface reconstruction, and force-feedback interaction.

---

# 📖 Table of Contents

* [Overview](#overview)
* [Features](#features)
* [Technical Pipeline](#technical-pipeline)
* [System Architecture](#system-architecture)
* [Demo](#demo)
* [Installation & Setup](#installation--setup)
* [Environment & Requirements](#environment--requirements)
* [How It Works](#how-it-works)
* [Known Dependencies](#known-dependencies)
* [Future Work](#future-work)
* [Author](#author)
* [License](#license)

---

# Overview

This project implements a **real-time dental drilling simulation system** using a voxel-based **Signed Distance Field (SDF)** representation.

Unlike traditional mesh deformation approaches, the system directly modifies volumetric distance fields to simulate material removal. This enables stable topology changes and robust cutting behavior during interactive drilling operations.

The simulation supports:

* Real-time tooth drilling
* Volumetric material removal
* Dynamic surface reconstruction
* Haptic force feedback
* Efficient collision handling
* Interactive medical simulation workflows

The project is built with **Unreal Engine 5** and integrates **OpenHaptics** devices for force-feedback interaction.

---

# Features

## ✅ SDF-Based Volumetric Representation

* Tooth geometry stored as voxelized Signed Distance Fields
* Robust inside/outside queries
* Stable topology modification during cutting

---

## ✅ Real-Time Cutting Simulation

* Localized SDF modification
* Interactive drilling operations
* Incremental updates for real-time performance

---

## ✅ Dynamic Surface Reconstruction

* Surface extraction using Marching Cubes
* Real-time mesh regeneration
* Smooth geometry updates after cutting

---

## ✅ Haptic Interaction

* Integrated Phantom / Touch haptic device support
* Force feedback based on volumetric interaction
* Real-time drill-to-surface response

---

## ✅ Acceleration Structures

* BVH acceleration for collision queries
* Optimized triangle interaction
* Reduced update overhead

---

# Technical Pipeline

```text
Tooth Mesh
    ↓
Voxelization
    ↓
Signed Distance Field (SDF)
    ↓
Drill Interaction Detection
    ↓
Localized SDF Modification
    ↓
Marching Cubes Reconstruction
    ↓
Dynamic Mesh Update
    ↓
Haptic Force Feedback
```

---

# System Architecture

```text
DentalSimulationSDF/
├── Source/
│
├── Tooth/                     # Tooth representation
│   └── ToothSDFVolume
│
├── Haptic/                    # Haptic interaction system
│   ├── HapticSDFManager
│   └── HapticTriangleManager
│
├── Simulation/                # Core simulation logic
│   ├── PhantomManager
│   ├── Drill
│   └── SnapshotSDFVolume
│
├── Geometry/                  # Geometry processing
│   ├── MarchingCubes
│   └── MeshTriangle
│
├── Acceleration/              # Spatial acceleration structures
│   └── BVH
│
├── Content/
├── Config/
└── DentalSimu.uproject
```

---

# Demo

🎥 Demo Video:

https://drive.google.com/file/d/1yQHWmkJB8WkXfQdYmGiesBFoSdt2YlQD/view?usp=sharing

The demo showcases:

* Real-time tooth drilling
* SDF-based volumetric cutting
* Dynamic Marching Cubes reconstruction
* Haptic interaction with Phantom device
* Real-time surface updates

You may also add preview GIFs or screenshots:

```md
![demo](Docs/demo.gif)
```

---

# Installation & Setup

## 1. Clone the Repository

```bash
git clone https://github.com/PanAkatsuki/DentalSimulationSDF.git
```

---

## 2. Install Haptic Device Drivers

This project requires a supported **3D Systems Phantom / Touch haptic device**.

Download and install the official drivers:

https://support.3dsystems.com/s/article/Haptic-Device-Drivers?language=en_US

Supported devices include:

* Phantom Premium
* Touch
* Touch X

After installation, verify that the device is correctly recognized by the operating system.

---

## 3. Configure the Haptic Device

After installing the drivers, launch the provided device configuration utility and complete calibration.

Recommended checks:

* Device calibration
* Workspace setup
* Stylus verification
* Button input test
* Force feedback test

Make sure the haptic device functions correctly before launching the project.

---

## 4. Install OpenHaptics SDK

This project depends on the **OpenHaptics SDK**.

Download the SDK here:

https://support.3dsystems.com/s/article/OpenHaptics-for-Windows-Developer-Edition-v35?language=en_US&redirect=yes

The SDK is required for compiling the project and accessing the HD/HL APIs.

After installation, verify that the SDK directory exists.

Example:

```text
C:\OpenHaptics\
```

or

```text
C:\Program Files\3D Systems\OpenHaptics\
```

The SDK should contain directories similar to:

```text
include/
lib/
utilities/
```

---

## 5. Configure SDK Path in Unreal Build Files

Edit the corresponding `.Build.cs` file and configure the OpenHaptics SDK path.

Example:

```cpp
string OpenHapticsPath = "C:/OpenHaptics";

PublicIncludePaths.Add(
    Path.Combine(OpenHapticsPath, "include")
);

PublicAdditionalLibraries.Add(
    Path.Combine(OpenHapticsPath, "lib", "HD.lib")
);

PublicAdditionalLibraries.Add(
    Path.Combine(OpenHapticsPath, "lib", "HL.lib")
);
```

Modify the path according to your local installation.

---

## 6. Build the Project

1. Open `DentalSimu.uproject`
2. Generate Visual Studio project files
3. Build the project in Visual Studio
4. Launch Unreal Engine 5
5. Connect and enable the haptic device
6. Start the simulation

---

# Environment & Requirements

| Component     | Version         | Notes                    |
| ------------- | --------------- | ------------------------ |
| Unreal Engine | 5.x             | Required                 |
| OS            | Windows         | Tested                   |
| Language      | C++17+          | Core implementation      |
| IDE           | Visual Studio   | Recommended              |
| Haptic SDK    | OpenHaptics     | Required                 |
| Device        | Phantom / Touch | Optional but recommended |

---

# How It Works

## 1. Tooth Voxelization

The input tooth mesh is converted into a voxel-based Signed Distance Field representation.

---

## 2. Interaction Detection

The drill position and orientation are sampled against the SDF volume.

Collision and contact information are computed in real time.

---

## 3. SDF Modification

Material removal is simulated by modifying local SDF values near the drill region.

This directly changes the volumetric representation of the tooth.

---

## 4. Surface Reconstruction

The updated SDF volume is converted back into a polygon mesh using Marching Cubes.

Only modified regions are reconstructed for performance optimization.

---

## 5. Haptic Feedback

Force feedback is computed based on drill penetration depth and contact constraints.

The haptic device provides real-time tactile interaction.

---

# Known Dependencies

* Unreal Engine 5
* OpenHaptics SDK
* Visual Studio C++ Toolchain
* Phantom / Touch Device Drivers

---

# Future Work

* GPU-based SDF updates
* Sparse voxel data structures
* Multi-resolution simulation
* Improved tooth material models
* Thermal drilling simulation
* Fluid and debris simulation
* Networked collaborative training
* XR / VR integration

---

# Author

**Xiaoyu Zhang**

GitHub:
https://github.com/PanAkatsuki

---

# License

MIT License

Copyright (c) 2026 Xiaoyu Zhang

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files...
