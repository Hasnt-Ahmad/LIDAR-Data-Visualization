# KITTI 3D Detection & Tracking Viewer

A practical computer vision project for exploring **KITTI 3D object detection data** through LiDAR point-cloud visualization, camera projection, Bird's-Eye View (BEV) representations, and 3D bounding-box rendering.

The project focuses on understanding how autonomous-driving datasets connect **LiDAR coordinates, camera coordinates, image pixels, calibration matrices, and 3D object annotations**.

---

## Project Overview

3D perception for autonomous vehicles requires understanding multiple coordinate systems and sensor representations.

In this project, I worked with the **KITTI 3D Object Detection dataset** and implemented a visualization pipeline that:

* Loads KITTI LiDAR `.bin` point clouds.
* Reads KITTI camera calibration files.
* Applies LiDAR-to-camera coordinate transformations.
* Projects 3D LiDAR points into the camera image.
* Reads KITTI 3D object annotations.
* Converts KITTI bounding-box representations into a common format.
* Visualizes LiDAR point clouds.
* Generates Bird's-Eye View (BEV) representations.
* Projects 3D bounding boxes onto camera images.
* Renders 3D bounding boxes using `vedo`.
* Displays object IDs and class information.
* Generates 3D scene screenshots for portfolio visualization.

The project helped me move from conventional 2D computer vision toward **3D perception for autonomous driving**.

---

## What I Practiced

### 3D Perception

* LiDAR point-cloud processing
* 3D coordinate systems
* Camera-LiDAR transformations
* Homogeneous coordinates
* 3D bounding-box representation
* Object orientation / yaw
* Point-cloud visualization
* Bird's-Eye View representations

### Camera-LiDAR Calibration

* KITTI `P2` projection matrix
* `Tr_velo_to_cam` transformation
* `R0_rect` rectification matrix
* LiDAR → camera transformation
* Camera → LiDAR transformation
* 3D → 2D image projection

### Visualization

* LiDAR scatter visualization
* 3D bounding-box rendering
* BEV visualization
* Camera-image overlays
* 3D scene rendering with `vedo`
* Offscreen rendering and screenshot generation

---

# Dataset

This project uses the **KITTI 3D Object Detection dataset**.

The relevant training directory contains:

```text
training/
├── velodyne/
├── image_2/
├── calib/
└── label_2/
```

### Directory contents

| Directory   | Description                               |
| ----------- | ----------------------------------------- |
| `velodyne/` | LiDAR point clouds stored as `.bin` files |
| `image_2/`  | Left camera images                        |
| `calib/`    | Camera/LiDAR calibration files            |
| `label_2/`  | 3D object annotations                     |

Each sample is identified using a six-digit frame ID.
---

# KITTI LiDAR Point Clouds

Each KITTI Velodyne file contains points represented as:

```text
[x, y, z, reflectance]
```

Therefore, every LiDAR point contains four floating-point values:

| Value         | Meaning                       |
| ------------- | ----------------------------- |
| `x`           | X coordinate                  |
| `y`           | Y coordinate                  |
| `z`           | Z coordinate                  |
| `reflectance` | LiDAR intensity / reflectance |

The visualization primarily uses the first three values to construct the 3D point cloud.

---

The visualization can include:

* 3D box surfaces
* Box edges
* Corner spheres
* Heading arrows
* Object IDs
* Class labels
* Object-specific colors

---

# Point Cloud Visualization

LiDAR points are visualized using `vedo`.

```

The point color can be determined from the point's depth coordinate.

This produces a colored 3D representation of the LiDAR scene.

---

# Bird's-Eye View

The project also generates a simplified **Bird's-Eye View representation**.

The BEV visualization maps the spatial coordinates of points onto a 2D image:

```text
LiDAR Point Cloud
       │
       ▼
Select X/Y coordinates
       │
       ▼
Normalize coordinates
       │
       ▼
Map to image pixels
       │
       ▼
     BEV Image
```

The implementation uses the X and Y coordinates of the point cloud to construct the 2D representation.

3D object boxes can also be projected into this representation.

---

# Camera Visualization

Several visualization functions are implemented for examining the relationship between the camera and LiDAR data.

### Point projection

```python
visualize_points(index)
```
<img width="1204" height="358" alt="image" src="https://github.com/user-attachments/assets/7fa2c4d0-e34f-4379-b233-286d0cdb79d2" />


Projects LiDAR points onto a blank camera-sized image.

### BEV

```python
visualize_bev(index)
```
<img width="1028" height="365" alt="image" src="https://github.com/user-attachments/assets/cd205bc3-0450-4cd0-a2d2-7db79afcf627" />


Creates a Bird's-Eye View representation of the LiDAR scene.

### Camera image with 3D boxes

```python
visualize_image_box(index)
```
<img width="1189" height="361" alt="image" src="https://github.com/user-attachments/assets/c1e0d9ff-128e-40b0-af8c-1ef6db2dd478" />


Projects 3D object bounding boxes onto the camera image.

### Combined camera visualization

```python
visualize(index)
```
<img width="1208" height="364" alt="image" src="https://github.com/user-attachments/assets/c4038b48-343a-41ef-9713-6762e01dbff7" />


Combines:

* LiDAR points
* 3D bounding boxes
* Camera projection

into a single visualization.

---

