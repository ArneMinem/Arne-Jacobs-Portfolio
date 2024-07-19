# Digital Terain Model in C++

## Description

This project was done during my second year at ENSTA Bretagne. The goal was to create a Digital Terrain Model (DTM) using C++.
It was an individual project that contributed to 50% of the final grade of the course.
Before starting this project we had a course on C++ to learn the basics of the language.
[Here](https://simon-rohou.fr/cours/c++/index.php) you can have a look at the class distribution and [here](https://github.com/ArneMinem/Projet_Cpp) is the link to my repository. For those who are interested there is a video presentation of the project [here](https://youtu.be/AH8jv9s0MrI).

## The work done

For this project, I needed to create a 2D image that represents different altitudes of a 2.5D terrain using color levels. I started by using a Digital Terrain Model (DTM) of Guerlédan Lake, which provided the elevation data I needed.

First, I had to read the input file containing geographic coordinates and elevation information. Since the coordinates were in a geographic format, I converted them to a suitable projection, like Lambert93, to ensure accurate mapping on a 2D plane. Lambert93 is a widely used projection system in France, making it a good choice for this project.

Next, I implemented a Delaunay triangulation to create a mesh from the terrain data. This step was crucial for accurately representing the terrain, especially when dealing with irregular grids. Delaunay triangulation ensures that no point is inside the circumcircle of any triangle, resulting in a more uniform mesh.

To optimize my program, I used a binary tree structure to speed up the search for triangles corresponding to each pixel in the image. This reduced the complexity of the search from O(n) to O(log(n)), making the process much more efficient.

For the image generation, I started with the PGM format, which is a simple grayscale image format. Once I had that working, I moved on to the PPM format to add color. I implemented a color mapping system, using a gradient like the Haxby color map to visually represent the altitude variations.

I named my executable "create_raster," and it accepted parameters like the path to the input file and the desired width of the output image. The height was automatically calculated based on the DTM dimensions.

In terms of deliverables, I organized my source code neatly, created a build.sh script for compilation, and documented everything thoroughly. I also recorded a video explaining my project and the structure of my code, keeping it under 10 minutes as required.

Finally, I made sure to follow the evaluation criteria closely, focusing on code readability, proper implementation of the binary tree structure, and ensuring the correct handling of inputs and outputs. I also considered adding bonus features like generating documentation and a webpage, and adding shadows to the terrain. Thanks to these shadow effects, the terrain looked more realistic and visually appealing.

I put a lot of effort into this project, and I was proud of the final result. It was a great learning experience, and I gained valuable skills in C++ programming, data processing, optimization techniques, and computer graphics.
Moreover, I got the best grade in the class for this project, which was a testament to my hard work and dedication.

## Skills developed

- C++ programming
- Data processing
- Delaunay triangulation
- Binary tree structure
- Image generation
- Color mapping
- Optimization techniques
- Computer graphics
- Documentation
- Video presentation
- Problem-solving
- Time management
- Lamert93 projection