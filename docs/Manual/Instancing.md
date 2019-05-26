# Instancing Unlit Shader

We are using a custom shader to offload as much work as possible to the gpu rather than the cpu to create the 3d isometric effect.

## Instancing  

Sprites are rotated towards the camera in such a way that viewed from a certain angle by the camera they appear to be 3d objects. That rotation must happen individually on each sprite around its center position. While we could have simply set the `Transform.rotation` on each GameObject that would have also effected any physics colliders attached.   
So to disrupt your workflow as little as possible and stick to standard Unity components we perform the rotation in our custom shader.
Unity optimizes rendering performance using a technique called [dynamic batching](https://docs.unity3d.com/Manual/DrawCallBatching.html). Batching sprites unfortunately loses any information about a sprite's center position and we therefore cannot rotate the sprite around its center anymore.   
So to perform our rotation and still profit from Unity build in rendering optimization we use [instancing](https://docs.unity3d.com/Manual/GPUInstancing.html).  

GPU Instancing however is not available on older devices. Desktops, modern browsers and most mobile devices today support GPU instancing. As of May 7th, 2019 just under 80% of Android devices support the required OpenGL es 3.0 standard or higher [[1]](https://developer.android.com/about/dashboards#OpenGL) as well as all devices running iOS 7 and higher [[2]](https://developer.apple.com/library/archive/documentation/3DDrawing/Conceptual/OpenGLES_ProgrammingGuide/OpenGLESApplicationDesign/OpenGLESApplicationDesign.html#//apple_ref/doc/uid/TP40008793-CH6-SW2).

!!! summary
    * WebGL 2.0, OpenGL es 3.0+ or DirectX11+ is required on your target platform to use all features of this asset.
    * close to 80% of Android devices, Apple devices running iOS 7+, modern browser and pretty much all desktops support one of the required standards.