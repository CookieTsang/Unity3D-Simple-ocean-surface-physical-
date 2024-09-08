![wave](https://github.com/user-attachments/assets/bffe38fe-7aa4-4934-9405-a761f74f839d)
# Simple-ocean-surface-physical-A summary of online learning.
简单的Wave
每个类和方法协同工作，创建了一个动态且交互的海面效果，确保物体能够根据水面高度正确漂浮，且性能损耗并不大
主要代码分为三部分：Floater、WaterManager和WaveManager

1. Floater
这个类负责模拟物体在水中的漂浮效果。`Floater`类使用Unity的`Rigidbody`组件来处理物体的物理运动，并通过力的作用模拟物体受到的浮力和水的阻力。代码中的关键变量包括：
- `depthBeforeSubmerged`：控制物体在完全淹没前的深度。
- `displacementAmount`：用于计算位移的乘数，模拟浮力的大小。
- `floaterCount`：决定浮点数量，用于分配浮力。
- `waterDrag`和`waterAngularDrag`：模拟水的阻力和角阻力。

在`FixedUpdate`方法中，每帧都会对物体施加重力，并根据物体在水中的位置计算浮力。如果物体低于水面高度（`waveHeight`），则根据物体的深度和水面的波动计算浮力和阻力。`AddForceAtPosition`用于在物体上某一点施加浮力，而`AddForce`和`AddTorque`则用来应用水的线性和角阻力。

2.WaterManager
这个类负责动态地更新水面网格的高度，以显示波动的效果。每帧通过`Update`方法遍历水面网格的顶点，调用`WaveManager`提供的波浪高度数据更新水面的形状。
具体实现中，水面的每个顶点都会依据其世界坐标的x和z位置，应用波浪高度更新，使得水面呈现波动效果。更新完成后，网格法线也会重新计算，以确保渲染效果。

3.WaveManager
`WaveManager`类是核心的波浪生成器，负责计算水面的波浪高度。其属性包括波幅（`amplitude`）、波长（`length`）、宽度（`wide`）、波速（`speed`）和偏移量（`offset`）。
每帧通过`Update`方法更新波浪的偏移量，从而模拟波浪的运动。

波浪高度通过`GetWaveHeight`方法计算，使用了正弦和余弦函数的组合，基于顶点的x和z位置，以及波浪的长度和宽度来生成变化的波动效果。
偏移量的引入使得波浪会随着时间的推移不断变化，模拟出水面的自然波动效果。


总结
该水面物理模拟系统结合了物理和图形处理
通过计算波浪高度和作用于物体的浮力，成功模拟了物体在动态波动水面上的漂浮效果。
`Floater`类处理物体的浮动和阻力，
`WaterManager`负责更新水面的形状，
`WaveManager`则生成了波浪的动态效果。



Each class and method works together to create a dynamic and interactive ocean surface effect, ensuring that objects can correctly float according to the water surface height with minimal performance loss. The main code is divided into three parts: Floater, WaterManager, and WaveManager.

1. **Floater**

   This class is responsible for simulating the floating effect of objects in water. The `Floater` class uses Unity's `Rigidbody` component to handle the physical motion of objects and simulates the buoyancy and water resistance acting on the objects through forces. Key variables in the code include:
   - `depthBeforeSubmerged`: Controls the depth before the object is fully submerged.
   - `displacementAmount`: A multiplier used to calculate displacement, simulating the magnitude of buoyancy.
   - `floaterCount`: Determines the number of floaters used to distribute buoyancy.
   - `waterDrag` and `waterAngularDrag`: Simulates the linear and angular resistance of water.

   In the `FixedUpdate` method, gravity is applied to the object each frame, and buoyancy is calculated based on the object's position in the water. If the object is below the water surface height (`waveHeight`), buoyancy and drag are calculated based on the object's depth and water surface fluctuations. `AddForceAtPosition` is used to apply buoyancy at a specific point on the object, while `AddForce` and `AddTorque` are used to apply the water's linear and angular resistance.

2. **WaterManager**

   This class is responsible for dynamically updating the heights of the water surface mesh to display wave effects. Each frame, the `Update` method traverses the vertices of the water surface mesh, updating the shape of the water surface by calling wave height data provided by `WaveManager`.

   In the specific implementation, each vertex of the water surface is updated according to its world coordinate x and z positions, applying wave height updates to create a fluctuating effect on the water surface. After the update, the mesh normals are recalculated to ensure rendering quality.

3. **WaveManager**

   The `WaveManager` class is the core wave generator, responsible for calculating the wave heights on the water surface. Its properties include amplitude (`amplitude`), wavelength (`length`), width (`wide`), wave speed (`speed`), and offset (`offset`).

   Each frame, the offset of the waves is updated via the `Update` method to simulate wave movement.

   Wave height is calculated using the `GetWaveHeight` method, which uses a combination of sine and cosine functions, generating varying wave effects based on the x and z positions of the vertices and the length and width of the waves. The introduction of the offset allows waves to continuously change over time, simulating the natural fluctuation of the water surface.

**Summary**

This water surface physics simulation system combines physical and graphical processing. By calculating wave heights and the buoyancy acting on objects, it successfully simulates the buoyant effect of objects on a dynamically fluctuating water surface. The `Floater` class handles object buoyancy and resistance, `WaterManager` updates the shape of the water surface, and `WaveManager` generates the dynamic wave effects.
