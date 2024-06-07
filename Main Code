Function detectIris(imagePath, minRadius, maxRadius, sigma, sensitivity,
outerSearchRadius, figureIndex,var)
% Read the image
eyeImage = imread(imagePath);
% Check if the image is grayscale or not
if ndims(eyeImage) == 3 && size(eyeImage, 3) == 3
% Convert the image to grayscale if it's not already
grayEyeImage = rgb2gray(eyeImage);
else
% If the image is already grayscale, keep it as is
grayEyeImage = eyeImage;
end
% Apply Gaussian blur with the specified sigma value
blurredImage = imgaussfilt(grayEyeImage, sigma);
% Edge detection using Canny
edgeImage = edge(blurredImage, 'canny');
% Find circles using Hough transform
[centers, radii, metric] = imfindcircles(edgeImage, [minRadius, maxRadius],
'ObjectPolarity', 'bright', 'Sensitivity', sensitivity);
% Extract the center and radius of the detected circle
irisCenter = centers(1,:);
irisRadius = radii(1,:);
% Use Daugman's integrodifferential operator to find the outer boundary
[outerCenter, outerRadius] = findOuterBoundary(edgeImage, irisCenter,
irisRadius, outerSearchRadius);
disp(outerRadius)
disp(irisRadius)
% Display the image with the detected iris boundaries
figure(figureIndex);
imshow(eyeImage);
hold on;
viscircles(irisCenter, irisRadius, 'EdgeColor', 'g');
viscircles(outerCenter, outerRadius, 'EdgeColor', 'r');
title(['Image ', num2str(figureIndex)]);
hold off;
% Print the polar matrix for the region between the outer and inner circle
printPolarMatrix(grayEyeImage, irisCenter, irisRadius, outerRadius,var);
end
function [center, radius] = findOuterBoundary(image, innerCenter, innerRadius,
outerSearchRadius)
% Define the range of possible outer radii
minOuterRadius = innerRadius;
maxOuterRadius = minOuterRadius + outerSearchRadius;
% Define the step size for the search
stepSize = 5;
% Initialize the maximum gradient sum
maxGradientSum = -Inf;
% Initialize the outer boundary
center = innerCenter;
radius = innerRadius;
% For each possible radius...
for r = minOuterRadius:stepSize:maxOuterRadius
% Compute the circular path
theta = 0:0.01:(2*pi);
x = round(innerCenter(1) + r * cos(theta));
y = round(innerCenter(2) + r * sin(theta));
% Ensure the coordinates are within the image bounds
x = max(min(x, size(image, 2)), 1);
y = max(min(y, size(image, 1)), 1);
% Compute the gradient along the path
gradient = abs(diff(double(image(sub2ind(size(image), y, x)))));
% Compute the sum of the gradient
gradientSum = sum(gradient);
% If this sum is greater than the current maximum...
if gradientSum > maxGradientSum
% Update the maximum gradient sum
maxGradientSum = gradientSum;
% Update the outer boundary
radius = r;
end
end
end
function printPolarMatrix(image, center, innerRadius, outerRadius,var)
% Get the size of the image
[height, width] = size(image);
% Create a meshgrid for the x and y coordinates
[X, Y] = meshgrid(1:width, 1:height);
% Shift the coordinates so that the center of the iris is at (0,0)
X = X - center(1);
Y = Y - center(2);
% Convert the Cartesian coordinates to polar coordinates
[Theta, Rho] = cart2pol(X, Y);
% Create a mask for the region between the outer and inner circle
mask = (Rho >= innerRadius) & (Rho <= outerRadius);
% Apply the mask to the polar coordinates
Theta = Theta(mask);
Rho = Rho(mask);
polarmatrix=(([Rho, Theta]));
assignin('base',var,polarmatrix);
end
