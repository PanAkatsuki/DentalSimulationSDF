# 🦷 Dental Simulation System – SDF-Based Cutting

A real-time dental cutting simulation system based on **Signed Distance Fields (SDF)** and **haptic interaction**, designed for interactive dental training and medical simulation research.

> 🎯 Goal: Simulate tooth drilling through volumetric SDF deformation, real-time mesh reconstruction, and haptic force feedback.

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
* [Performance & Evaluation](#performance--evaluation)
* [Known Dependencies](#known-dependencies)
* [Limitations](#limitations)
* [Future Work](#future-work)
* [Author](#author)
* [License](#license)

---

# Overview

This project implements a real-time dental drilling simulation framework using a voxel-based **Signed Distance Field (SDF)** representation.

Unlike traditional mesh deformation methods, the system directly modifies volumetric distance fields to simulate material removal during drilling. This approach enables stable volumetric cutting behavior and efficient local deformation updates.

The system supports:

* Real-time tooth drilling simulation
* Volumetric material removal
* Dynamic surface reconstruction
* Haptic force feedback interaction
* Spatial acceleration structures
* Interactive beginner-level dental training

The project is implemented in **Unreal Engine 5** and integrates **OpenHaptics** devices for real-time force feedback.

---

# Features

## ✅ SDF-Based Volumetric Representation

* Tooth geometry represented using voxelized Signed Distance Fields
* Robust inside–outside queries
* Stable volumetric cutting behavior

---

## ✅ Real-Time Cutting Simulation

* Localized SDF modification
* Drill-based volumetric material removal
* Incremental deformation updates for interactive performance

---

## ✅ Dynamic Mesh Reconstruction

* Surface extraction using Marching Cubes
* Dynamic geometry updates after cutting
* Partial reconstruction of modified regions

---

## ✅ Haptic Interaction

* Phantom / Touch haptic device integration
* Force feedback based on SDF gradient information
* Real-time drill-to-surface interaction

---

## ✅ Spatial Acceleration Structures

* BVH acceleration for spatial queries
* Optimized interaction handling
* Efficient triangle-based collision support

---

## ✅ Real-Time Performance

* Interactive real-time rendering performance
* Localized volumetric updates for efficiency
* Tested under multiple voxel resolutions

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
│   └── DentalSimu/
│
│       ├── Actor/                        # Scene actors and simulation entities
│       │   ├── Arch                      # Combined dental arch
│       │   ├── Drill                     # Dental drill actor
│       │   ├── Gum                       # Gum representation
│       │   └── Tooth                     # Tooth representation
│       │
│       ├── BVH/                          # Spatial acceleration structures
│       │   └── BVH
│       │
│       ├── EnumType/                     # Enumerations and type definitions
│       │   └── MeshType
│       │
│       ├── Haptic/                       # Haptic interaction system
│       │   ├── HapticSDFManager
│       │   └── HapticTriangleManager
│       │
│       ├── Phantom/                      # Phantom/OpenHaptics device integration
│       │   ├── PhantomManager
│       │   └── PhantomSubsystem
│       │
│       ├── StructType/                   # Core data structures
│       │   ├── BVHNode
│       │   ├── MeshTriangle
│       │   ├── SnapshotMeshTriangles
│       │   ├── SnapshotSDFVolume
│       │   ├── ToothMeshData
│       │   ├── ToothProceduralMeshData
│       │   └── ToothSDFVolume
│       │
│       ├── Table/                        # Lookup tables
│       │   └── MarchingCubesTables
│       │
│       └── Test/                         # Experimental / debugging utilities
│           ├── HapticTriangle
│           └── HapticBox
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
* Localized SDF deformation
* Dynamic Marching Cubes reconstruction
* Haptic interaction using Phantom device
* Real-time geometry updates

---

# Installation & Setup

## 1. Clone the Repository

```bash
git clone https://github.com/PanAkatsuki/DentalSimulationSDF.git
```

---

## 2. Install Haptic Device Drivers

⚠️ Hardware Requirement

A compatible Phantom / Touch haptic device is currently required to run the project.

The current implementation assumes that a valid haptic device is connected and successfully initialized during startup.

If no compatible device is connected, the application may fail to launch or crash due to missing device initialization and null-pointer access in the haptic subsystem.

At the current stage of development:

Haptic interaction is tightly integrated into the simulation loop
Device fallback handling has not yet been implemented
Running the project without a connected Phantom/OpenHaptics device is not supported

Supported devices include:

Phantom Premium
Touch
Touch X

This project requires a supported **3D Systems Phantom / Touch** haptic device.

Download and install the official drivers:

https://support.3dsystems.com/s/article/Haptic-Device-Drivers?language=en_US

Supported devices include:

* Phantom Premium
* Touch
* Touch X

After installation, verify that the device is correctly recognized by the operating system.

---

## 3. Configure the Haptic Device

After installing the drivers, launch the provided configuration utility and complete calibration.

Recommended checks:

* Device calibration
* Workspace setup
* Stylus verification
* Button input test
* Force feedback test

Ensure the haptic device functions correctly before launching the project.

---

## 4. Install OpenHaptics SDK

This project depends on the **OpenHaptics SDK**.

Download the SDK here:

https://support.3dsystems.com/s/article/OpenHaptics-for-Windows-Developer-Edition-v35?language=en_US&redirect=yes

The SDK is required for compiling the project and accessing the HD/HL APIs.

Example installation paths:

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

Example configuration:

```cpp
using System.IO;
using UnrealBuildTool;

public class DentalSimu : ModuleRules
{
    public DentalSimu(ReadOnlyTargetRules Target) : base(Target)
    {
        PCHUsage = PCHUsageMode.UseExplicitOrSharedPCHs;

        PublicDependencyModuleNames.AddRange(
            new string[]
            {
                "Core",
                "CoreUObject",
                "Engine",
                "InputCore",
                "ProceduralMeshComponent"
            }
        );

        // OpenHaptics SDK path
        string PhantomSDKPath = "C:\\OpenHaptics\\Developer\\3.5.0";

        // Include paths
        PublicIncludePaths.Add(
            Path.Combine(PhantomSDKPath, "include")
        );

        PublicIncludePaths.Add(
            Path.Combine(PhantomSDKPath, "utilities\\include")
        );

        // HD library
        PublicAdditionalLibraries.Add(
            Path.Combine(PhantomSDKPath, "lib\\x64\\Release\\hd.lib")
        );

        PublicDelayLoadDLLs.Add("hd.dll");

        // HL library
        PublicAdditionalLibraries.Add(
            Path.Combine(PhantomSDKPath, "lib\\x64\\Release\\hl.lib")
        );

        PublicDelayLoadDLLs.Add("hl.dll");

        // HDU utility library
        PublicAdditionalLibraries.Add(
            Path.Combine(PhantomSDKPath, "utilities\\lib\\x64\\Release\\hdu.lib")
        );
    }
}
```

Modify the SDK path according to your local installation directory.

### Runtime DLL Requirements

Make sure the required OpenHaptics DLL files are accessible at runtime.

Depending on your system configuration, you may need to:

* Add the OpenHaptics SDK `bin` directory to the system `PATH`
* Or copy the required DLL files next to the Unreal executable

Common required DLLs include:

```text
hd.dll
hl.dll
```

If the DLLs are not found at runtime, Unreal Engine may fail to launch the project correctly.

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

| Component     | Version         | Notes               |
| ------------- | --------------- | ------------------- |
| Unreal Engine | 5.x             | Required            |
| OS            | Windows         | Tested              |
| Language      | C++17+          | Core implementation |
| IDE           | Visual Studio   | Recommended         |
| Haptic SDK    | OpenHaptics     | Required            |
| Device        | Phantom / Touch | Required            |

---

# How It Works

## 1. Tooth Voxelization

The input tooth mesh is converted into a voxel-based Signed Distance Field representation.

---

## 2. Interaction Detection

The drill position and orientation are sampled against the SDF volume.

Collision and interaction information are computed in real time.

---

## 3. SDF Modification

Material removal is simulated by modifying local SDF values near the drill region.

The cutting operation is spatially restricted to nearby voxels for efficiency.

---

## 4. Surface Reconstruction

The updated SDF volume is converted into a polygon mesh using Marching Cubes.

Only modified regions are reconstructed to maintain interactive performance.

---

## 5. Haptic Feedback

Force feedback is computed using SDF gradient information and stiffness parameters.

The haptic device provides tactile resistance during drilling interaction.

---

# Performance & Evaluation

The system was evaluated under different voxel resolutions.

Experimental results indicate:

* Stable real-time rendering performance
* Increased initialization cost at finer voxel resolutions
* A voxel size of `0.5f` provides a practical balance between geometric detail and computational cost

A preliminary user study involving 8 participants was also conducted.

Key findings include:

* High usability and learnability
* Positive feedback on haptic realism
* Strong educational value for beginner training
* Average overall evaluation score: **8.5 / 10**

The results support the feasibility of SDF-based volumetric modeling for interactive dental simulation.

---

# Known Dependencies

* Unreal Engine 5
* OpenHaptics SDK
* Visual Studio C++ Toolchain
* Phantom / Touch Device Drivers

---

# Limitations

Current limitations include:

* High memory usage at fine voxel resolutions
* Simplified force feedback model
* Limited user study sample size
* Lack of clinical validation by professional dentists

---

# Future Work

Potential future improvements include:

* GPU-accelerated SDF updates
* Adaptive or hierarchical SDF structures
* Material-aware force modeling
* Expanded user studies
* Improved calibration and interaction refinement
* Undo/redo interaction refinement
* Left-handed mode support
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

Third-party SDKs and dependencies may be subject to their own licenses.
