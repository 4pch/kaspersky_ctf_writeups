# Writeup 

PixelGenerator.py is a Python script that performs pixel-wise adversarial attacks on images.
It randomly selects pixels in a source image, tests different grayscale levels, and sends each modified image to a verification API.

The goal is to maximize a target probability returned by the API while maintaining visual similarity to a reference image using MSE and SSIM metrics.
The script iterates until the target probability is reached or the maximum number of attempts is completed

https://github.com/IMSHOX/CTF-Kaspersky-25-AI
