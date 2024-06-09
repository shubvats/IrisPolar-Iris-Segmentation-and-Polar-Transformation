# Iris Segmentation and Polar Transformation

## Project Overview

The goal of this project is to accurately segment the iris region of an eye from given images and convert it into a co-centricity invariant representation by transforming Cartesian coordinates to polar coordinates. This involves two key steps: detecting the iris boundaries using circle detection techniques and converting the segmented iris region to a polar representation.

## Objectives

### Iris Boundary Detection

- Use the Hough Transform for circle detection to locate the iris boundaries (both inner and outer).
- Implement Daugman's integrodifferential operator to refine the detection of both the inner and outer boundaries of the iris.

### Coordinate Transformation

- Convert the segmented iris region from Cartesian coordinates to polar coordinates to create a normalized, scale-invariant representation of the iris.

## Data

The project uses images provided in the eyes.zip file, which contains various eye images for processing.

## Implementation Details

### Iris Boundary Detection

#### Hough Transform for Circle Detection

The Hough Transform is a feature extraction technique used in image analysis, computer vision, and digital image processing. We will use this technique to detect circles that correspond to the inner and outer boundaries of the iris.

#### Daugman's Integrodifferential Operator

Daugman's operator is used to detect the circular boundaries of the iris more precisely. This method iterates over possible circle parameters and selects the ones that maximize the integro-differential expression, providing an accurate detection of the iris boundaries.

### Polar Coordinates Transformation

After detecting the iris boundaries, we convert the segmented iris region from Cartesian coordinates (x, y) to polar coordinates (r, θ). This transformation normalizes the iris region, making it invariant to changes in scale and rotation, which is crucial for iris recognition tasks.

## Usage

The `detectIris` function in the provided code can be used to detect the iris boundaries and perform the polar transformation. Provide the image path, parameters for circle detection, and other settings as input to the function.

```matlab
detectIris(imagePath, minRadius, maxRadius, sigma, sensitivity, outerSearchRadius, figureIndex,var)
```

## Contributing

Contributions to this project are welcome! Feel free to open issues or submit pull requests with improvements, bug fixes, or additional features.

## License

This project is licensed under the [MIT License](LICENSE).

---
