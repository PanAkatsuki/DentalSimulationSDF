\# Dental Simulation System (SDF-Based)



\## Overview

This project presents a real-time dental cutting simulation system based on Signed Distance Field (SDF) representation and haptic interaction.



The system enables physically plausible tooth drilling by updating a volumetric SDF representation in real time and reconstructing the surface dynamically using the Marching Cubes algorithm.



\---



\## Key Features



\- \*\*SDF-Based Volumetric Representation\*\*

&#x20; - Teeth are represented using a voxel-based signed distance field

&#x20; - Supports robust inside–outside queries and smooth deformation



\- \*\*Real-Time Cutting Simulation\*\*

&#x20; - Localized SDF updates simulate material removal

&#x20; - Efficient partial updates for interactive performance



\- \*\*Dynamic Mesh Reconstruction\*\*

&#x20; - Surface is reconstructed using the Marching Cubes algorithm

&#x20; - Updated in real time after each cutting operation



\- \*\*Haptic Interaction\*\*

&#x20; - Integration with haptic devices for force feedback

&#x20; - Collision handled via SDF and triangle-based structures



\- \*\*Acceleration Structures\*\*

&#x20; - BVH used for efficient collision detection

&#x20; - Optimized interaction between tool and tooth surface



\---



\## System Architecture



The system is built on Unreal Engine and consists of:



\- `ToothSDFVolume`: volumetric representation of teeth

\- `PhantomManager`: manages simulation state

\- `HapticSDFManager`: handles SDF-based interaction

\- `MarchingCubes`: surface reconstruction module

\- `BVH`: acceleration structure for collision detection



\---



\## How It Works



1\. Convert tooth mesh into SDF (voxel grid)

2\. Detect interaction between drill and tooth

3\. Apply localized SDF modification (cut operation)

4\. Reconstruct surface using Marching Cubes

5\. Render updated geometry in real time



\---



\## Requirements



\- Unreal Engine 5.x

\- Windows

\- (Optional) Haptic device



\---



\## How to Run



1\. Clone this repository

2\. Open `DentalSimu.uproject` in Unreal Engine

3\. Build the project

4\. Run the simulation



\---



\## Demo



(Add GIF / video here)



\---



\## Applications



\- Dental training simulation

\- Medical simulation systems

\- Real-time volumetric modeling



\---



\## Author



Zhang Xiaoyu

