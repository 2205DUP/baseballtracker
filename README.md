# Baseball Vision Tracking System
A computer vision + physics based analytics system for baseball. This project takes video input (single-camera or multi-camera) and calculates:
- Ball trajectory
- Exit velocity (speed off the bat)
- Estimated carry distance
- Pitch spin rate
- Release point clustering
- Pitch delivery repeatability and mechanics consistency

This is a work-in-progress tool aimed at coaches, players, and player development groups that want real tracking data without paying thousands for commercial systems.

## Core Features
- **Ball Tracking:** Frame-by-frame detection and tracking of the baseball in flight.
- **Trajectory Calculation:** Uses calibrated camera geometry + motion modeling to compute the ball flight path.
- **Exit Velocity Estimation:** Estimates speed off the bat using pixel velocity → real-world conversion.
- **Distance Projection:** Predicts projected carry distance based on launch angle, speed, and drag model.
- **Spin Measurement:** Tracks rotational cue patterns on the baseball to estimate RPM.
- **Release Point Mapping:** Builds release-point heatmaps for pitchers to diagnose consistency.
- **Pitch Form Consistency:** Tracks key body/arm markers (optional) to evaluate repeatable mechanics.

## Requirements
- Python 3.10+
- OpenCV
- NumPy
- SciPy
- (Optional) PyTorch or ONNX Runtime if using ML-based ball/hand/keypoint detectors

Install using:
pip install -r requirements.txt


## Recommended Camera Setup
- **Frame Rate:** 120 FPS minimum (to resolve rotation and contact timing).
- **Shutter Speed:** As fast as possible to reduce motion blur.
- **Mounting:** Fixed and stable, preferably elevated behind home plate or down the line.
- **Calibration:** Use included calibration script + checkerboard to convert pixel distances to real dimensions.

## How It Works (Technical Overview)
1. **Video Input** → Raw frames loaded.
2. **Object Detection** → Ball localized in each frame using CV model.
3. **Ball Path Tracking** → Positions smoothed, noise filtered, trajectory curve fit.
4. **Physics Fitting** → Ball flight modeled with gravity + drag to estimate real velocity.
5. **Spin Estimation** → Visible surface pattern or seam movement analyzed per rotation cycle.
6. **Release Point / Form** → Hand position across frames extracted and clustered.

## Output Data
| Metric | Description |
|-------|-------------|
| Exit Velocity (mph) | Speed off the bat |
| Launch Angle (deg) | Initial angle of ball flight |
| Carry Distance (ft) | Estimated landing distance |
| Spin Rate (RPM) | Ball rotation speed |
| Spin Axis (optional) | Calculated if camera resolution allows |
| Release Variance (inches) | Pitcher mechanics repeatability |

Outputs can be exported to:
- CSV
- JSON
- Graphs & Visual Overlays

## Example Use

python analyze_video.py --input sample_pitch.mp4 --calibration camera.yaml --output results.csv

## Roadmap
- Multiple camera triangulation for full 3D tracking
- Player skeleton tracking for biomechanics metrics
- Real-time mode for live batting practice feedback

## License
MIT License. Use it, modify it, just don’t pretend you invented baseball physics.

## Contributing
Pull requests welcome. If you submit sloppy code, it will be judged accordingly. No participation trophy nonsense.



