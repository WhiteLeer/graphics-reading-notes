# GPU Gems 1 读书笔记

> 📚 《GPU Gems: Programming Techniques, Tips and Tricks for Real-Time Graphics》
>
> 编辑：Randima Fernando (NVIDIA)
> 出版社：Addison-Wesley | 出版年份：2004
> 在线免费版本：https://developer.nvidia.com/gpugems

---

## 📖 关于本笔记

GPU Gems是NVIDIA出版的图形编程技巧合集，**完全免费在线提供**。本书汇集了来自ILM、Pixar、游戏工作室和NVIDIA的顶级图形程序员的实战经验。

### ✨ 特点

- **实战导向**：来自真实项目的技术经验
- **代码示例**：包含完整的shader代码和实现细节
- **前沿技术**：2004年GPU编程的最佳实践
- **多领域覆盖**：从自然效果到GPU通用计算

### 📚 阅读进度

- ✅ Part I - Natural Effects（自然效果，8章）
- ✅ Part II - Lighting and Shadows（光照与阴影，7章）
- ✅ Part III - Materials（材质，5章）
- ✅ Part IV - Image Processing（图像处理，7章）
- ✅ Part V - Performance and Practicalities（性能与实践，9章）
- ✅ Part VI - Beyond Triangles（超越三角形，6章）
- 🎉 **全书完成！（42章）**

### 🔗 相关资源

- 📘 在线版本：https://developer.nvidia.com/gpugems
- 💻 示例代码和Demo可下载
- 📚 GPU Gems 2 和 GPU Gems 3 也在线提供

---

## 📑 目录

### Part I - Natural Effects 自然效果
- [Chapter 1: Effective Water Simulation from Physical Models](#chapter-1-effective-water-simulation-from-physical-models)
- [Chapter 2: Rendering Water Caustics](#chapter-2-rendering-water-caustics)
- [Chapter 3: Skin in the "Dawn" Demo](#chapter-3-skin-in-the-dawn-demo)
- [Chapter 4: Animation in the "Dawn" Demo](#chapter-4-animation-in-the-dawn-demo)
- [Chapter 5: Implementing Improved Perlin Noise](#chapter-5-implementing-improved-perlin-noise)
- [Chapter 6: Fire in the "Vulcan" Demo](#chapter-6-fire-in-the-vulcan-demo)
- [Chapter 7: Rendering Countless Blades of Waving Grass](#chapter-7-rendering-countless-blades-of-waving-grass)
- [Chapter 8: Simulating Diffraction](#chapter-8-simulating-diffraction)

### Part II - Lighting and Shadows 光照与阴影
- [Chapter 9: Efficient Shadow Volume Rendering](#chapter-9-efficient-shadow-volume-rendering)
- [Chapter 10: Cinematic Lighting](#chapter-10-cinematic-lighting)
- [Chapter 11: Shadow Map Antialiasing](#chapter-11-shadow-map-antialiasing)
- [Chapter 12: Omnidirectional Shadow Mapping](#chapter-12-omnidirectional-shadow-mapping)
- [Chapter 13: Generating Soft Shadows Using Occlusion Interval Maps](#chapter-13-generating-soft-shadows-using-occlusion-interval-maps)
- [Chapter 14: Perspective Shadow Maps](#chapter-14-perspective-shadow-maps)
- [Chapter 15: Managing Visibility for Per-Pixel Lighting](#chapter-15-managing-visibility-for-per-pixel-lighting)

### Part III - Materials 材质
- [Chapter 16: Real-Time Approximations to Subsurface Scattering](#chapter-16-real-time-approximations-to-subsurface-scattering)
- [Chapter 17: Ambient Occlusion](#chapter-17-ambient-occlusion)
- [Chapter 18: Spatial BRDFs](#chapter-18-spatial-brdfs)
- [Chapter 19: Image-Based Lighting](#chapter-19-image-based-lighting)
- [Chapter 20: Texture Bombing](#chapter-20-texture-bombing)

### Part IV - Image Processing 图像处理
- [Chapter 21: Real-Time Glow](#chapter-21-real-time-glow)
- [Chapter 22: Color Controls](#chapter-22-color-controls)
- [Chapter 23: Depth of Field](#chapter-23-depth-of-field)
- [Chapter 24: High-Quality Filtering](#chapter-24-high-quality-filtering)
- [Chapter 25: Fast Filter-Width Estimates](#chapter-25-fast-filter-width-estimates)
- [Chapter 26: The OpenEXR Image File Format](#chapter-26-the-openexr-image-file-format)
- [Chapter 27: A Framework for Image Processing](#chapter-27-a-framework-for-image-processing)

### Part V - Performance and Practicalities 性能与实践
- [Chapter 28: Graphics Pipeline Performance](#chapter-28-graphics-pipeline-performance)
- [Chapter 29: Efficient Occlusion Culling](#chapter-29-efficient-occlusion-culling)
- [Chapter 30-31: FX Composer](#chapter-30-31-fx-composer)
- [Chapter 32: Shader Interfaces](#chapter-32-shader-interfaces)
- [Chapter 33: Converting Production RenderMan Shaders](#chapter-33-converting-production-renderman-shaders)
- [Chapter 34-36: Shader Integration](#chapter-34-36-shader-integration)

### Part VI - Beyond Triangles 超越三角形
- [Chapter 37: GPU Programming Toolkit](#chapter-37-gpu-programming-toolkit)
- [Chapter 38: Fast Fluid Dynamics on the GPU](#chapter-38-fast-fluid-dynamics-on-the-gpu)
- [Chapter 39: Volume Rendering Techniques](#chapter-39-volume-rendering-techniques)
- [Chapter 40: Real-Time 3D Ultrasound Visualization](#chapter-40-real-time-3d-ultrasound-visualization)
- [Chapter 41: Real-Time Stereograms](#chapter-41-real-time-stereograms)
- [Chapter 42: Deformers](#chapter-42-deformers)

---

## Part I - Natural Effects 自然效果

### Chapter 1: Effective Water Simulation from Physical Models
**作者**: Mark Finch (Cyan Worlds)

#### 核心概念

基于物理的实时水面模拟，结合几何形变和动态法线贴图，适用于从池塘到海洋的各种水体。

#### 技术要点

**1. Gerstner波模型**
- 波函数：正弦波叠加，每个波包含波长(L)、振幅(A)、速度(S)、方向(D)
- 物理基础：色散关系 `ω = √(gk)`，g为重力常数，k为波数
- 陡峭参数Q：控制波峰尖锐度（0=光滑，接近1/ωA时形成尖峰）

**2. 双层实现策略**
- **几何波**（4条）：顶点着色器中实现，产生网格起伏
- **纹理波**（~15条）：像素着色器中实现，生成动态法线贴图

**3. 优化技术**
- 基于网格边长的自适应波长过滤
- 深度衰减：波高随水深减小
- 查找表：优化三角函数和插值计算
- 球面环境映射修正：仅5次算术运算

**4. 应用场景**
- 《Uru: Ages Beyond Myst》游戏中的实时水体
- 最低要求：vs_1_0 和 ps_1_0

> [!tip] 关键技巧
> 将波分为几何层和纹理层，前者产生大尺度形变，后者提供细节，避免过度细分网格。

---

### Chapter 2: Rendering Water Caustics
**作者**: Daniel Sánchez-Crespo, Juan Guardado

#### 核心概念

实时渲染水面焦散效果，采用简化的光线追踪近似，优先美学效果而非物理精确。

#### 技术要点

**1. 焦散原理**
- 光线通过波浪表面折射
- Snell定律：`η₁sinθ₁ = η₂sinθ₂`（水的折射率1.33）
- 垂直光线假设（正午场景）

**2. 实现流程**
```
步骤1: 渲染海底纹理基础层
步骤2: 添加焦散叠加层（逆向光线追踪）
步骤3: 渲染波面表面与环境映射
```

**3. 数学工具**
- 波函数偏导数：`∂z/∂x`, `∂z/∂y` → 表面法线
- 直线与平面交点：确定光线到达海底的位置
- 距离编码：产生深度衰减

**4. 优化策略**
- 纹理空间渲染：计算量恒定
- 环境映射替代完整Snell定律
- GPU像素着色器实现

> [!warning] 简化假设
> 为了实时性能，采用美学驱动而非物理精确的方法，垂直光线假设可能不适用所有场景。

---

### Chapter 3: Skin in the "Dawn" Demo
**作者**: Curtis Beeson, Kevin Bjorke (NVIDIA)

#### 核心概念

NVIDIA Dawn演示中的高质量皮肤渲染，结合HDR环境光照和次表面散射近似。

#### 技术要点

**1. 多层光照模型**
- **漫反射层**：皮肤纹理 × 预卷积漫反射立方体贴图 × 遮挡
- **镜面反射层**：法线贴图alpha通道控制 × 镜面立方体贴图
- **边缘高光**：背光环境采样 × 视线方向衰减
- **反射层**：0.02权重的镜面反射

**2. HDR环境光照**
- iPIX工具：183度鱼眼影像采集
- HDRShop：生成预卷积立方体贴图
- 存储余弦加权的入射光平均值

**3. 次表面散射近似**
- 剪影边缘采样视线后方的环境光
- 混合皮肤基础色调
- 模拟光线穿透薄组织的效果

**4. 顶点着色器优化**
- 98根骨骼的加权蒙皮
- 5个blend shape变形
- 预计算 N·V 点积

**5. Shader架构**
- 单通道渲染，无需多Pass
- 程序化着色器生成器：自动优化骨骼数量

> [!tip] 美术可控性
> 更复杂的光照方案往往牺牲美术可控性。建议混合环境光与定向光源，保持可调节性。

---

### Chapter 4: Animation in the "Dawn" Demo
**作者**: Curtis Beeson (NVIDIA)

#### 核心概念

Dawn演示中的高级角色动画系统，结合变形目标(Morph Targets)和骨骼蒙皮(Skeletal Skinning)。

#### 技术要点

**1. 两种变形技术**

**变形目标(Morph Targets)**：
- 用于复杂面部表情动画
- Dawn角色：27,000三角形的中性头部
- 50个变形副本：~30个情绪（快乐、悲伤等）+ ~20个修饰符（眉毛上升等）
- 并行应用：使用差异向量方法，权重1.0完全应用偏移

**骨骼蒙皮(Skeletal Skinning)**：
- 每个顶点由加权矩阵数组影响
- Dawn演示：98根骨骼驱动超过180,000个三角形

**2. GPU实现优化**

**寄存器限制解决方案**：
- 顶点输入最多16个寄存器
- 5个变形目标影响位置和法线
- 正交归一化中性切线，通过叉积计算副法线
- 节省寄存器空间用于其他数据

**累积矩阵蒙皮**：
- 先将加权矩阵求和：`M = w₁M₁ + w₂M₂ + ... + wₙMₙ`
- 再执行单次矩阵乘法
- 显著降低计算成本（相比对每个矩阵分别进行4次点积）

**3. 工程技巧**

- 每帧动态重命名顶点输入属性，激活所需的5个变形目标
- 在`.w`分量中存储自遮挡项，利用未使用空间
- 将头部网格与身体分离，避免对整体网格应用不必要计算
- 允许人工截断骨骼数量，重新缩放权重保持总和为1

> [!tip] 性能优化
> 累积矩阵蒙皮是关键优化——将N个矩阵变换的开销从O(N)降到O(1)+预处理。

---

### Chapter 5: Implementing Improved Perlin Noise
**作者**: Ken Perlin (New York University)

#### 核心概念

Ken Perlin对其经典噪声算法的改进版本，消除了原版中的视觉伪影。

#### 改进内容

**1. 插值函数升级**
- **原版**：3阶 `3t² - 2t³`
- **新版**：5阶 `6t⁵ - 15t⁴ + 10t³`
- **原因**：原版在边界处二阶导数不连续，导致凹凸贴图出现明显伪影
- **效果**：新版保证一阶和二阶导数在边界处均为零

**2. 梯度向量优化**
- **原版**：256个随机梯度向量
- **新版**：12个均匀分布的向量
- **分布**：立方体边中心 `(0,±1,±1)`, `(±1,0,±1)`, `(±1,±1,0)`
- **效果**：消除不规则分布导致的高频伪影

#### 实现技术

**1. 纹理采样方案**
- 8×8×8 toroidal平铺体积纹理
- 复数旋转相位结合高频和低频
- 低频实部调制高频纹理

**2. 优化技巧**
- 查找表替代数学计算（256长度，16位精度）
- 简化梯度内积（如 `(1,1,0)·(x,y,z) = x+y`）
- 像素着色器实现bump映射

**3. 应用场景**
- 程序化纹理生成
- 自然材质模拟（云、大理石、木纹）
- 实时凹凸贴图
- 分辨率无关的细节纹理

> [!success] 学术贡献
> Ken Perlin因程序化纹理技术获得奥斯卡技术成就奖。此改进版本是对原版的重要升级。

---

### Chapter 6: Fire in the "Vulcan" Demo
**作者**: Hubert Nguyen (NVIDIA)

#### 核心概念

基于视频纹理精灵的火焰渲染系统，结合体积纹理和粒子技术实现真实火焰效果。

#### 技术要点

**1. 渲染方案选择**

**三种方案对比**：
- **完全程序化**：内存占用少，但需处理数千粒子
- **屏幕空间2D扭曲**：对相机角度敏感
- **视频素材驱动**（选用）：电影级特效仍使用的方案

**2. 粒子系统实现**

**发射器配置**：
- 可调整：大小、密度、纹理、生命周期
- 动画帧限制：256帧3D纹理总量
- 分配：火焰动画192帧 + 其他效果64帧

**多样性策略**：
- 随机调整：粒子大小、位置、衰减率
- 起始帧随机化
- 透明度变化
- 自定义精灵（非硬件点精灵），支持纹理坐标U/V轴翻转

**3. 体积纹理技术**

**数据存储**：
- 256×256×256 B8G8R8A8格式：16MB
- 帧间混合补偿低帧数
- Z纹理坐标递增播放动画
- 备选方案：64×64×256分辨率（低端设备）

**4. Shader实现**

**多层合成**（Example 6-1）：
```
热扭曲偏移采样 → 模糊场景混合 → 火焰/烟雾Alpha混合 → 发光效果叠加
```
- 使用Alpha通道选择性模糊对象

**5. 性能优化**

**分层合成**：
- 256×256火焰源 → 1/4屏幕分辨率缓冲
- 混合操作减少4倍

**自定义精灵几何**：
- 用矩形替代正方形
- 减少未使用纹素读取

**混合方式**：
- 从加法混合切换至Alpha混合
- 排序数百粒子性能开销可忽略

> [!warning] 权衡
> 视频纹理提供逼真效果但内存密集（16MB）。可通过降低分辨率支持低端设备。

---

### Chapter 7: Rendering Countless Blades of Waving Grass
**作者**: Kurt Pelzer

#### 核心概念

通过几何实例化和顶点着色器动画实现大规模草地的实时渲染。

#### 技术要点

**1. 核心几何结构**

**星形配置**：
- 3个相交四边形构成单个草簇对象
- 禁用背面剔除实现双侧可见
- 法向量与多边形竖边平行（保证斜坡上正确光照）
- 通过alpha混合和深度测试实现密集视觉效果

**2. 纹理优化**

**单张纹理方案**：
- 承载多个草叶
- 透明度通道：绘制草茎轮廓
- 颜色通道：绿/黄混合区分草叶状态
- 用少量多边形代表许多草叶

**3. 三种动画方案**

| 方案 | 计算位置 | 优势 | 劣势 |
|------|--------|------|------|
| **按簇** | CPU | 支持复杂风模拟 | 需多次绘制调用 |
| **按顶点** | 顶点着色器 | 绘制调用少 | 纹理扭曲可见 |
| **按对象** | 对象中心 | 无扭曲+局部混沌 | 需额外顶点数据 |

**4. LOD管理**

- 动态添加/移除距离草对象
- 保持堆积排序+alpha混合渲染顺序
- 确保视觉一致性

**5. 性能优化**

- 顶点着色器框架统一，仅改变动画部分
- 通过纹理坐标识别上部顶点（`v < 0.1`）
- 避免不必要计算
- 单次绘制调用覆盖完整草地区域

> [!tip] 实现建议
> 按对象动画方案是最佳平衡：无纹理扭曲、绘制调用少、支持局部风场变化。

---

### Chapter 8: Simulating Diffraction
**作者**: Jos Stam (Alias)

#### 核心概念

基于物理的光学衍射实时模拟，适用于CD、全息图等表面效果。

#### 技术要点

**1. 光学衍射原理**

**物理基础**：
- 光的波动特性导致衍射现象
- 平行反射条纹（间距*d*）产生衍射光栅
- 每条纹产生球面波，接收点的波是所有球面波的叠加

**干涉条件**：
```
d(sin θ₁ - sin θ₂) = nλ
```
- *n*: 整数（衍射级数）
- *λ*: 波长
- 相位相同时产生最大干涉强度

**2. 顶点着色器实现**

**所需顶点属性**：
- 法向量（表面朝向）
- 位置信息
- 切线向量（条纹方向，如CD轨道方向）

**计算管线**：
1. 半向量投影到切线方向得到参数*u*
2. 遍历有效*n*值范围（固定循环8次）
3. 计算公式：`y = 2u/n - 1`
4. 累加对应波长的颜色贡献

**3. 着色实现**

**双部分着色**：

**衍射图案**：
- 用3个高斯凸函数近似彩虹色映射
- 覆盖可见光谱范围

**各向异性高光**：
- 模拟*u=0*情况下的表面粗糙度
- 使用Greg Ward模型

**4. 性能考虑**

**限制**：
- 编译器限制：固定循环8次
- 未动态计算有效*n*范围
- 预定义迭代次数平衡精度与性能

**优化建议**：
- 纹理查找表替代计算
- 可变循环（支持时）
- 根据视角动态调整*n*范围

> [!success] 应用场景
> CD表面、全息效果、鸟类羽毛、昆虫翅膀等自然界iridescence（虹彩）效果。

---

## Part II - Lighting and Shadows 光照与阴影

### Chapter 9: Efficient Shadow Volume Rendering
**作者**: Morgan McGuire

#### 核心概念

模板阴影体（Stencil Shadow Volume）的高效实现技术，支持实时动态阴影。

#### 算法原理

**1. 核心思想**

构造3D几何体"包围物体投射的所有阴影"。使用模板缓冲计数光线与阴影体表面的交点。

**判断规则**：
```
点P在阴影中 ⟺ 射向无穷远的光线进入交点数 > 退出交点数
```

**2. 模板缓冲实现**

**渲染设置**：
- 禁用深度写入
- 渲染阴影体到模板缓冲

**计数规则**：
- 正面多边形深度测试失败时：模板值递减
- 背面多边形深度测试失败时：模板值递增
- 结果：区分阴影/光照像素

#### 优化技术

**3. Depth-Pass vs. Depth-Fail**

| 方法 | 计数方向 | Cap要求 | 优势 |
|------|--------|---------|------|
| **Depth-Pass (z-pass)** | 向观察者 | 无需（"uncapped"优化） | 更快 |
| **Depth-Fail (z-fail)** | 远离观察者 | 需要light和dark cap | 更稳定 |

**4. 性能优化技术**

**方向光优化**：
- 阴影边成为三角形（非四边形）
- 因为光线在无穷远处收敛

**XY裁剪**：
- 限制渲染到投影光范围
- 使用scissor测试
- 减少填充率开销

**深度边界**：
- 使用`glDepthBoundsEXT`
- 跳过光范围外的像素

**有限体积**：
- 阴影几何仅扩展到光源半径
- 而非无穷远

**5. 实现要求**

**数据结构**：
- 双顶点缓冲：标准顶点 + 无穷远扩展副本（w=0）
- 边邻接信息（一致的缠绕顺序）

**投影矩阵**：
- 无限远投影矩阵
- 防止远平面裁剪

**轮廓检测**：
- 每帧通过 N·L 点积判断朝光面
- 确定阴影体边缘

> [!tip] 实战建议
> Depth-pass + uncapped优化是最优组合，除非相机可能进入阴影体。

---

### Chapter 10: Cinematic Lighting
**作者**: Fabio Pellacini, Kiril Vidimce (Pixar)

#### 核心概念

基于Pixar生产经验的"Uberlight"着色器，将电影级光照控制引入实时渲染。

#### 技术要点

**1. Uberlight概念**

**来源**：Ronen Barzel的光照模型，Pixar在多部动画电影中使用：
- 《玩具总动员》
- 《虫虫特工队》
- 《怪兽公司》
- 《海底总动员》

**简化版本**：适应实时GPU限制的电影光照着色器。

**2. Pixar光照模型**

**两阶段处理**：

**阶段1 - 表面着色**：
- 纹理查询
- 插值
- 程序纹理

**阶段2 - 光源遍历**：
- 评估每个光源颜色
- 与表面反应

**3. 美术控制参数**

| 参数类别 | 功能 | 用途 |
|---------|------|------|
| **选择性** | 对象响应特定光源 | 精确控制光照影响 |
| **色彩** | 独立环境光/漫反射/镜面反射 | 艺术化调整 |
| **塑形** | 全向光/谷仓门塑形 | 超椭圆锥体控制 |
| **阴影** | 控制密度/色调/反射 | 柔和阴影效果 |
| **纹理投影** | "Cookie"效果 | 幻灯机/离镜阴影 |

**全向光控制**：
- 近/远截断距离
- 距离衰减

**谷仓门塑形**：
- 超椭圆锥体定义光照范围
- 模拟实际灯光设备

**4. Cg实现**

**顶点着色器**：
- 坐标变换
- 光空间计算

**片段着色器**：
- 超椭圆评估
- 距离衰减
- 阴影映射查询

**优化策略**：
- 预生成纹理替代复杂计算
- 可提速3倍

> [!success] 电影级控制
> Uberlight将电影制作中的灯光师控制参数引入实时渲染，兼顾美术表现力和实时性能。

---

### Chapter 11: Shadow Map Antialiasing
**作者**: Mike Bunnell, Fabio Pellacini

#### 核心概念

通过百分比渐近过滤（PCF）解决阴影贴图放大时的锯齿问题。

#### 技术要点

**1. 走样问题**

阴影贴图投影到几何体时，放大导致"大而丑陋的锯齿"出现在阴影边界，严重影响实时渲染质量。

**2. PCF原理**

**核心思想**：
- 不预过滤阴影纹理
- 每像素执行多次深度比较
- 平均结果

**计算内容**：
```
表面更接近光源的百分比 = 非阴影覆盖率
```

**3. 优化策略**

**16采样方案**：
- 使用硬件内置PCF
- 4×4纹素采样
- 偏移：(-1.5, -0.5, 0.5, 1.5)

**4采样抖动**：
- 减少到每像素4个采样
- 使用位置相关模式
- 通过空间分布达到相似视觉质量

**4. 实现要点**

**固定采样区域**：
- 4×4纹素区域
- 不对齐纹素边界（产生抗锯齿效果）

**硬件深度比较**：
- 利用GPU加速
- 提高效率

**采样重叠**：
- 相邻像素采样区域重叠
- 放大时自然平滑过渡
- 无需大量采样开销

**精度考虑**：
- 8位精度
- 防止高对比度阴影中的条带伪影

> [!tip] 关键洞察
> 放大阴影贴图时，相邻像素的采样区域重叠，自然产生平滑过渡而无需过多采样。

---

### Chapter 12: Omnidirectional Shadow Mapping
**作者**: Philipp S. Gerasimov

#### 核心概念

点光源的全向阴影贴图（Omnidirectional Shadow Mapping），解决单一深度贴图只能覆盖方向光源的局限。

#### 我的理解

**问题**：标准Shadow Map只能从单一方向投影，点光源需要全向覆盖。

#### 解决方案：Cube Map Shadow

**核心思路**：使用立方体贴图（6个面）存储全向深度。

```cpp
// 1. 生成阶段（从点光源渲染6次）
for (int face = 0; face < 6; face++) {
    // 设置立方体贴图面的视角
    Matrix4 view = GetCubeFaceView(lightPos, face);
    Matrix4 proj = PerspectiveProj(90, 1.0, nearPlane, farPlane);  // 90°FOV覆盖一个面

    SetRenderTarget(shadowCubeMap, face);
    SetViewProj(view, proj);

    // 渲染场景深度
    RenderSceneDepthOnly();
}
```

**立方体面方向**：
```
Face 0: +X (right)
Face 1: -X (left)
Face 2: +Y (up)
Face 3: -Y (down)
Face 4: +Z (forward)
Face 5: -Z (back)
```

#### Shader实现

```hlsl
// 顶点着色器：计算世界空间位置
struct VS_OUTPUT {
    float4 pos : POSITION;
    float3 worldPos : TEXCOORD0;
};

VS_OUTPUT VS_Main(float3 position : POSITION) {
    VS_OUTPUT output;
    output.pos = mul(float4(position, 1.0), WorldViewProj);
    output.worldPos = mul(float4(position, 1.0), World).xyz;
    return output;
}

// 像素着色器：采样立方体阴影贴图
samplerCUBE shadowCube : register(s0);
float3 lightPos;
float lightFarPlane;

float4 PS_Main(VS_OUTPUT input) : COLOR {
    // 1. 计算从光源到片元的向量
    float3 lightToFrag = input.worldPos - lightPos;

    // 2. 采样立方体贴图获取存储的深度
    float closestDepth = texCUBE(shadowCube, lightToFrag).r;

    // 3. 计算当前片元深度
    float currentDepth = length(lightToFrag);

    // 4. 深度比较
    float shadow = (currentDepth - bias > closestDepth) ? 0.0 : 1.0;

    // 5. 应用光照
    float3 lighting = ComputeLighting(...) * shadow;
    return float4(lighting, 1.0);
}
```

#### 性能优化

**1. 多Pass渲染开销**：
```
标准Shadow Map：1次场景渲染
Cube Shadow Map：6次场景渲染（6个面）
→ 渲染开销增加6倍
```

**优化策略**：
- 降低立方体贴图分辨率（512×512 vs 2048×2048平面阴影）
- 仅在点光源附近物体渲染
- 多个点光源共享立方体贴图池
- 使用几何着色器一次性渲染到6个面（GeForce 8+）

**2. 深度存储**：
```hlsl
// 线性化深度存储（而非透视深度）
float depth = length(worldPos - lightPos);
depth = depth / lightFarPlane;  // 归一化到[0,1]
return float4(depth, depth, depth, depth);
```

#### 与Dual-Paraboloid对比

| 特性 | **Cube Map** | **Dual-Paraboloid** |
|------|--------------|---------------------|
| **采样面数** | 6 | 2 |
| **渲染开销** | 高（6个Pass） | 中（2个Pass） |
| **接缝问题** | 轻微（边缘） | ⚠️ 明显（赤道） |
| **采样简单性** | ✅ texCUBE | ❌ 需要特殊计算 |
| **视口变形** | ✅ 无 | ⚠️ 抛物面变形 |
| **现代支持** | ✅ 主流选择 | ⚠️ 较少使用 |

#### 现代应用

```
现代引擎中：
- Cube Shadow Map仍是点光源阴影标准方案
- 结合PCF/VSM实现软阴影
- 使用Geometry Shader优化渲染（一个Pass输出6个面）
- Unity/Unreal的点光源阴影默认使用Cube Shadow Map
```

---

### Chapter 13: Generating Soft Shadows Using Occlusion Interval Maps
**作者**: Will Donnelly, Joe Demers

#### 核心概念

使用遮挡区间贴图（Occlusion Interval Maps）实现静态场景中动态面光源的软阴影。

#### 我的理解

**软阴影原理**：
- 面光源（Area Light）产生半影（Penumbra）
- 每个表面点被光源的不同部分遮挡
- 需要对光源表面积分

**传统方法问题**：
- 光线追踪：每个像素数百条光线，实时不可行
- Shadow Map：只能产生硬阴影

#### Occlusion Interval Maps原理

**核心思路**：预计算遮挡信息，运行时快速查询。

**1. 遮挡区间定义**：

```
对于表面点P和线性光源L（1D）：
- 遍历遮挡物边界
- 记录光源上被遮挡的区间

示例：
光源：[0.0, 1.0]
遮挡物A遮挡：[0.2, 0.4]
遮挡物B遮挡：[0.6, 0.8]
→ 可见区间：[0.0, 0.2], [0.4, 0.6], [0.8, 1.0]
→ 可见度 = 0.2 + 0.2 + 0.2 = 0.6（60%光照）
```

**2. 区间贴图存储**：

```cpp
struct OcclusionInterval {
    float start;   // 区间起点
    float end;     // 区间终点
};

// 每个纹素存储遮挡区间链表
// 使用多个纹理通道或链表结构
```

#### 算法流程

**预计算阶段**（静态场景）：

```cpp
void PrecomputeOcclusionIntervals() {
    for (each surface point P) {
        List<OcclusionInterval> intervals;

        // 1. 投影场景到光源空间
        for (each occluder edge E) {
            // 计算E在光源上的投影
            float2 proj = ProjectEdgeOntoLight(P, E, lightPlane);

            // 添加遮挡区间
            intervals.Add({proj.x, proj.y});
        }

        // 2. 合并重叠区间
        intervals = MergeIntervals(intervals);

        // 3. 存储到纹理
        StoreIntervalsToTexture(P, intervals);
    }
}
```

**实时渲染阶段**：

```hlsl
// 像素着色器：查询遮挡区间
sampler2D occlusionMap : register(s0);

float4 PS_SoftShadow(float2 texCoord : TEXCOORD0, float3 worldPos : TEXCOORD1) : COLOR {
    // 1. 从纹理读取遮挡区间
    float4 interval1 = tex2D(occlusionMap, texCoord);  // [start1, end1, start2, end2]

    // 2. 计算可见区间长度
    float visible = 0.0;
    float totalLength = 1.0;  // 光源归一化长度

    // 排除遮挡区间
    visible = totalLength - (interval1.y - interval1.x) - (interval1.w - interval1.z);

    // 3. 可见度 = 可见区间 / 总长度
    float visibility = saturate(visible / totalLength);

    // 4. 应用光照
    float3 lighting = ComputeLighting(worldPos, lightPos);
    return float4(lighting * visibility, 1.0);
}
```

#### 扩展到2D面光源

**方法**：将面光源分解为多个线性光源。

```
矩形光源分解：
- 水平方向：N条线性光源
- 每条线应用1D遮挡区间算法
- 结果沿垂直方向积分

visibility_2D = (1/N) * Σ visibility_1D(i)
```

```hlsl
float ComputeSoftShadow2D(float2 texCoord, float3 worldPos) {
    float totalVisibility = 0.0;
    int numSamples = 8;  // 光源细分数量

    for (int i = 0; i < numSamples; i++) {
        // 采样光源的不同位置
        float u = (i + 0.5) / numSamples;
        float3 sampleLightPos = lightPosMin + u * (lightPosMax - lightPosMin);

        // 查询该位置的遮挡区间
        float visibility = QueryOcclusionInterval(texCoord, sampleLightPos);
        totalVisibility += visibility;
    }

    return totalVisibility / numSamples;
}
```

#### 优缺点分析

**优点**：
```
✅ 静态场景预计算，运行时非常快
✅ 动态光源位置（在预定义范围内移动）
✅ 软阴影质量高（准确的半影）
✅ 无需多次采样Shadow Map
```

**缺点**：
```
❌ 仅适用于静态场景（遮挡物不能移动）
❌ 预计算存储开销大（每个表面点的区间链表）
❌ 动态物体需要其他技术补充
❌ 复杂场景遮挡区间过多（纹理容量限制）
```

#### 存储优化

**压缩策略**：
```cpp
// 1. 限制最大区间数量（丢弃小区间）
const int MAX_INTERVALS = 4;

// 2. 使用浮点纹理存储
R32G32B32A32_FLOAT: [start1, end1, start2, end2]

// 3. 区间链表（使用间接纹理）
struct IntervalNode {
    float2 interval;
    uint next;  // 链表指针
};
```

#### 与其他软阴影技术对比

| 技术 | **实时性** | **动态场景** | **质量** | **复杂度** |
|------|-----------|-------------|---------|-----------|
| **Ray Tracing** | ❌ 慢 | ✅ | ⭐⭐⭐⭐⭐ | 高 |
| **PCSS** | ⚠️ 中 | ✅ | ⭐⭐⭐⭐ | 中 |
| **VSM** | ✅ 快 | ✅ | ⭐⭐⭐ | 低 |
| **Occlusion Intervals** | ✅ 最快 | ❌ 静态 | ⭐⭐⭐⭐ | 高（预计算） |

#### 适用场景

```
理想应用：
- 建筑可视化（静态建筑 + 动态光照）
- 室内场景（日光模拟）
- 预渲染背景 + 动态角色（混合技术）

不适用：
- 开放世界游戏（大量动态物体）
- 破坏系统（场景结构改变）
```

---

### Chapter 14: Perspective Shadow Maps (PSM)
**作者**: Simon Kozlov

#### 核心概念

透视阴影贴图（Perspective Shadow Maps, PSM）通过后透视变换优化深度贴图分辨率分配，减少透视走样。

#### 我的理解

**标准Shadow Map的问题**：

```
透视走样（Perspective Aliasing）：
- 近处物体占据更多屏幕像素
- 远处和近处使用相同的Shadow Map分辨率
- 导致近处阴影块状化（undersampling）

示例：
        相机
         |
    近处 |         远处
    ████ |         ▓
    ████ |         ▓

阴影贴图分辨率分配：
    近处: 10 texels → 锯齿严重！
    远处: 10 texels → 浪费分辨率
```

#### PSM核心思想

**关键洞察**：从相机视角变换阴影贴图，使分辨率分配与屏幕空间像素密度匹配。

**变换流程**：

```
标准Shadow Map：
World Space → Light View Space → Light Proj Space → Shadow Map

PSM：
World Space → Light View Space → Camera View Space → Camera Proj Space → Shadow Map
                                   ↑
                              关键创新！
```

#### 算法详解

**1. 标准Shadow Map渲染**：

```cpp
// 从光源视角渲染
Matrix4 lightView = LookAt(lightPos, sceneCenter, up);
Matrix4 lightProj = Ortho(bounds);  // 正交投影

Matrix4 lightMatrix = lightProj * lightView;
RenderDepth(lightMatrix);
```

**2. PSM渲染**：

```cpp
// 从光源视角变换到相机空间
Matrix4 lightView = LookAt(lightPos, sceneCenter, up);

// ⭐ 关键：应用相机的透视变换
Matrix4 cameraView = GetCameraView();
Matrix4 cameraProj = GetCameraProj();  // 相机的透视矩阵

// 复合变换
Matrix4 psmMatrix = cameraProj * cameraView * Inverse(lightView);

RenderDepth(psmMatrix);
```

**几何意义**：
```
1. 将场景从光源空间变换到相机空间
2. 应用相机的透视变换
   → 近处物体被"放大"
   → 远处物体被"缩小"
3. 阴影贴图分辨率自动匹配屏幕空间密度
```

#### Shader实现

```hlsl
// 顶点着色器（PSM深度渲染）
float4x4 psmMatrix;  // lightView^-1 * cameraView * cameraProj

struct VS_OUTPUT {
    float4 pos : POSITION;
    float depth : TEXCOORD0;
};

VS_OUTPUT VS_PSM(float3 position : POSITION) {
    VS_OUTPUT output;

    // 应用PSM变换
    float4 posLightSpace = mul(float4(position, 1.0), lightView);
    output.pos = mul(posLightSpace, psmMatrix);

    // 存储线性深度
    output.depth = output.pos.z / output.pos.w;

    return output;
}

float4 PS_PSM(VS_OUTPUT input) : COLOR {
    return float4(input.depth, input.depth, input.depth, 1.0);
}
```

```hlsl
// 像素着色器（阴影采样）
sampler2D psmShadowMap : register(s0);
float4x4 psmMatrix;

float4 PS_Main(float3 worldPos : TEXCOORD0) : COLOR {
    // 1. 变换到PSM空间
    float4 posLightSpace = mul(float4(worldPos, 1.0), lightView);
    float4 posPSM = mul(posLightSpace, psmMatrix);

    // 2. 透视除法
    float3 projCoords = posPSM.xyz / posPSM.w;

    // 3. 变换到纹理坐标[0,1]
    projCoords = projCoords * 0.5 + 0.5;
    projCoords.y = 1.0 - projCoords.y;  // 翻转Y

    // 4. 采样深度
    float closestDepth = tex2D(psmShadowMap, projCoords.xy).r;
    float currentDepth = projCoords.z;

    // 5. 深度测试
    float shadow = (currentDepth - bias > closestDepth) ? 0.0 : 1.0;

    // 应用光照
    float3 lighting = ComputeLighting(worldPos, lightPos);
    return float4(lighting * shadow, 1.0);
}
```

#### 优缺点分析

**优点**：
```
✅ 近处阴影质量显著提升
✅ 无需额外内存开销
✅ 算法简单，易于实现
✅ 适合第三人称游戏（角色周围高分辨率）
```

**缺点**：
```
❌ 远处阴影质量下降（分辨率被"偷"给近处）
❌ 仅在光源和相机方向接近时效果好
❌ 边界裁剪问题（相机背后物体投影到无穷远）
❌ 需要处理特殊情况（光源在相机后方）
```

#### 边界裁剪问题

**问题描述**：
```
相机背后的物体通过透视变换投影到无穷远
→ 阴影贴图需要覆盖无限范围
→ 分辨率严重浪费或裁剪错误
```

**解决方案**：
```cpp
// 1. 裁剪相机视锥背后的物体
if (Dot(lightDir, cameraForward) < 0) {
    // 光源在相机后方，使用标准Shadow Map
    return StandardShadowMap();
}

// 2. 限制近平面（避免极端变形）
float nearClip = max(cameraNear, minNearPlane);
Matrix4 clippedProj = PerspectiveProj(fov, aspect, nearClip, cameraFar);

// 3. 使用裁剪平面
// 仅渲染相机可见物体到阴影贴图
```

#### 与其他技术对比

| 技术 | **近处质量** | **远处质量** | **复杂度** | **适用场景** |
|------|------------|------------|-----------|-------------|
| **标准Shadow Map** | ⭐⭐ | ⭐⭐⭐ | 低 | 通用 |
| **PSM** | ⭐⭐⭐⭐⭐ | ⭐ | 低 | 角色周围 |
| **CSM** | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | 中 | 大场景⭐ |
| **PSSM** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | 中 | 现代标准⭐ |

#### 现代改进：LiSPSM

**Light-Space Perspective Shadow Maps**（后续研究）：

```
改进：
1. 考虑光源和相机的相对位置
2. 自适应调整透视变换强度
3. 解决边界裁剪问题

核心公式：
n' = lerp(n_uniform, n_perspective, weight)

weight基于光源-相机夹角：
- 夹角小（平行）：更多透视
- 夹角大（垂直）：更少透视
```

#### 实际应用建议

```cpp
// 混合策略（现代引擎常用）
if (IsCloseupScene() && IsLightInFront()) {
    // 近景使用PSM
    return PSM();
} else {
    // 其他情况使用CSM
    return CascadedShadowMap();
}

// 或使用PSSM（结合CSM和PSM优点）
return ParallelSplitShadowMaps();
```

---

### Chapter 15: Managing Visibility for Per-Pixel Lighting
**作者**: John O'Rorke

#### 核心概念

使用可见性管理技术优化多光源逐像素光照的性能，避免对不可见或不受影响的像素进行昂贵的光照计算。

#### 我的理解

**多光源问题**：

```
场景：100个动态光源
传统Forward Rendering：
- 每个像素计算100次光照
- 大量像素不受特定光源影响
- 浪费计算资源

示例：
像素P在角落：
- 距离光源L50: 100米（超出衰减范围）
- 仍然计算光照 → 结果为0 → 浪费！

性能：
100个光源 × 1920×1080像素 = 2亿次光照计算/帧
60 FPS → 120亿次/秒（不可行！）
```

#### 解决方案：光体积（Light Volumes）

**核心思路**：仅对光源影响范围内的像素进行光照计算。

**1. 光源包围体定义**：

```cpp
// 计算光源影响半径
float ComputeLightRadius(PointLight light) {
    // 基于衰减公式反推半径
    // Attenuation = 1 / (constant + linear*d + quadratic*d²)
    // 当Attenuation < threshold (如0.01)时截断

    float threshold = 0.01;  // 1%亮度
    float maxIntensity = max(light.color.r, light.color.g, light.color.b);

    // 求解二次方程
    float radius = (-light.linear + sqrt(light.linear * light.linear
                    - 4 * light.quadratic * (light.constant - maxIntensity / threshold)))
                   / (2 * light.quadratic);

    return radius;
}

// 创建光源包围球
Sphere lightVolume;
lightVolume.center = light.position;
lightVolume.radius = ComputeLightRadius(light);
```

**2. 使用模板缓冲（Stencil Buffer）标记**：

```cpp
// Multi-pass光照渲染
void RenderLights(Scene scene, Camera camera) {
    // Pass 1: 渲染场景几何（仅环境光）
    glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT | GL_STENCIL_BUFFER_BIT);
    RenderSceneAmbient(scene);

    // Pass 2+: 为每个光源添加光照
    glEnable(GL_BLEND);
    glBlendFunc(GL_ONE, GL_ONE);  // 累加光照
    glDepthMask(GL_FALSE);        // 不写入深度

    for (Light light : scene.lights) {
        // ⭐ 关键：渲染光源包围球
        // 仅影响球内的像素

        // 2a. 使用模板缓冲标记受影响像素
        glEnable(GL_STENCIL_TEST);
        glStencilFunc(GL_ALWAYS, 1, 0xFF);
        glStencilOp(GL_KEEP, GL_KEEP, GL_REPLACE);
        glColorMask(GL_FALSE, GL_FALSE, GL_FALSE, GL_FALSE);

        RenderLightVolume(light);  // 渲染球体，标记模板

        // 2b. 仅在标记像素执行光照计算
        glStencilFunc(GL_EQUAL, 1, 0xFF);
        glStencilOp(GL_KEEP, GL_KEEP, GL_KEEP);
        glColorMask(GL_TRUE, GL_TRUE, GL_TRUE, GL_TRUE);

        RenderSceneWithLight(scene, light);  // 仅计算模板标记的像素

        glClear(GL_STENCIL_BUFFER_BIT);
    }
}
```

#### Shader实现

```hlsl
// 顶点着色器：渲染光源包围球
float4x4 WorldViewProj;

float4 VS_LightVolume(float3 position : POSITION) : POSITION {
    // 将光源包围球顶点变换到屏幕空间
    return mul(float4(position, 1.0), WorldViewProj);
}

// 像素着色器：空（仅标记模板）
float4 PS_LightVolume() : COLOR {
    return float4(0, 0, 0, 0);  // 不写入颜色
}
```

```hlsl
// 像素着色器：逐像素光照（仅在模板标记区域执行）
sampler2D normalMap : register(s0);
sampler2D depthMap : register(s1);

float3 lightPos;
float3 lightColor;
float lightRadius;

float4 PS_PerPixelLight(float2 texCoord : TEXCOORD0, float3 viewRay : TEXCOORD1) : COLOR {
    // 1. 从G-Buffer重建世界位置
    float depth = tex2D(depthMap, texCoord).r;
    float3 worldPos = cameraPos + viewRay * depth;

    // 2. 计算光照方向和距离
    float3 L = lightPos - worldPos;
    float distance = length(L);
    L = normalize(L);

    // 3. 提前退出（在影响范围外）
    if (distance > lightRadius) {
        discard;  // 或return 0
    }

    // 4. 读取法线
    float3 N = tex2D(normalMap, texCoord).xyz * 2.0 - 1.0;
    N = normalize(N);

    // 5. 计算光照
    float NdotL = saturate(dot(N, L));
    float attenuation = 1.0 / (1.0 + 0.1 * distance + 0.01 * distance * distance);

    float3 lighting = lightColor * NdotL * attenuation;

    return float4(lighting, 1.0);
}
```

#### 优化策略对比

**1. 无优化（Brute Force）**：
```
for each pixel:
    for each light:
        compute lighting  // 即使光照贡献为0

成本：O(Pixels × Lights)
```

**2. 光源包围体（Light Volumes）**：
```
for each light:
    mark affected pixels (stencil)
    for each marked pixel:
        compute lighting

成本：O(Lights × AffectedPixels)
AffectedPixels << TotalPixels
```

**3. 延迟着色（Deferred Shading）**：
```
Pass 1: Render G-Buffer (geometry only)
Pass 2:
    for each light:
        render light volume
        compute lighting for covered pixels

成本：O(Pixels + Lights × AffectedPixels)
```

#### 与延迟着色的关系

**本章技术是Deferred Lighting的前身**：

```
2004年（本章）：
- Forward Rendering + Light Volumes
- 使用模板缓冲优化
- 每个光源仍需访问场景几何

2007年+（现代Deferred）：
- G-Buffer存储所有几何信息
- 光照Pass完全解耦
- 仅计算光照，无需几何数据
```

**核心相同点**：
- 将光照计算限制在影响范围内
- 使用包围体渲染
- 多Pass累加光照

#### 深度优化：Scissor Rect

```cpp
// 进一步优化：计算光源包围球的屏幕空间矩形
Rect ComputeScissorRect(Sphere lightVolume, Camera camera) {
    // 投影光源包围球到屏幕空间
    Point2D projCenter = ProjectToScreen(lightVolume.center, camera);
    float projRadius = ComputeProjectedRadius(lightVolume, camera);

    // 计算屏幕空间矩形
    return Rect(
        projCenter.x - projRadius,
        projCenter.y - projRadius,
        projCenter.x + projRadius,
        projCenter.y + projRadius
    );
}

// 渲染时应用裁剪
glEnable(GL_SCISSOR_TEST);
glScissor(rect.x, rect.y, rect.width, rect.height);
RenderSceneWithLight(scene, light);
glDisable(GL_SCISSOR_TEST);
```

**效果**：
```
无Scissor：光源包围球覆盖100×100像素
使用Scissor：仅处理80×80实际影响的像素
→ 节省36%像素着色器调用
```

#### 性能分析

**场景示例**：
```
分辨率：1920×1080 = 207万像素
光源数：50个点光源
平均影响：每个光源影响10%像素

无优化：
207万 × 50 = 1.035亿光照计算

Light Volumes优化：
207万 × 0.1 × 50 = 1035万光照计算
→ 减少90%计算量！
```

#### 现代应用

```
本章技术演变为：
1. Deferred Lighting（Light Pre-Pass）
   - Killzone 2 (2009)
   - 分离几何和光照

2. Deferred Shading
   - CryEngine 3+, Unreal Engine 4+
   - 完整G-Buffer
   - 现代游戏标配

3. Clustered Lighting
   - 将屏幕空间分割为3D格子
   - 每个格子记录影响的光源
   - Doom 2016, 现代引擎

核心思想不变：
"不要计算看不见或无影响的光照"
```

---

## Part III - Materials 材质

### Chapter 16: Real-Time Approximations to Subsurface Scattering
**作者**: Simon Green (NVIDIA)

#### 核心概念

半透明材质（皮肤、大理石）的实时次表面散射近似技术。

#### 物理原理

光线进入半透明材质后：
- 在内部散射和吸收
- 从不同位置射出

**视觉特征**：
- 整体光照柔和化
- 光线在相邻区域扩散
- 表面细节可见度降低
- 皮肤中出现红色色移（血液和组织吸收）

#### 实时近似方法

**1. Wrap Lighting（环绕光照）**

改进Lambert漫反射：
```
wrap_diffuse = max(0, (dot(L,N) + wrap) / (1 + wrap))
```
- 使光照在法线垂直于光向时继续贡献

**2. 深度图吸收模拟**

- 从光源视角渲染深度贴图
- 计算光线穿过材质的距离：`s = d_o - d_i`
- 估算衰减

**3. 纹理空间扩散**

- 将模型展开至UV空间进行光照计算
- 应用高斯模糊模拟光线扩散

#### Shader实现

**查表光照**：
- 将wrap lighting编码为1D纹理
- 包含颜色偏移

**投影纹理映射**：
- 深度贴图通过投影变换应用到表面

**多通道渲染**：
- 分离深度/法线/颜色通道存储入纹理

**分离滤波**：
- RGB通道应用不同宽度高斯核
- 红色扩散更广（血液效应）

#### 参数控制

- `wrap`值（0-1）：环绕光照范围
- `scatterWidth`：光影过渡的色移宽度
- `scatterColor`：通常偏红模拟血液
- `shininess`：镜面高光指数
- 通道权重：RGB独立模糊系数

#### 应用场景

- **皮肤渲染**：结合wrap lighting、纹理空间扩散及色移
- **半透明材质**：大理石、玉石（指数衰减）
- **实时角色**：面部和薄区域（耳朵、鼻孔）

#### 限制

- 仅适用凸形物体（凹陷处理需深度剥离）
- 需要良好UV参数化
- GeForce FX精度限制（需浮点纹理或打包）

---

### Chapter 17: Ambient Occlusion
**作者**: Matt Pharr (NVIDIA), Simon Green

#### 核心概念

环境光遮蔽（AO）- 智能环境光照项，根据表面各点能看到的外部环境比例变化。

> [!note] 作者注
> Matt Pharr后来成为PBRT的主要作者之一。

#### 技术原理

**核心洞察**：
- 预处理模型，计算表面各点能看到多少外部环境
- 计算有多少被其他几何体遮挡
- 本质是漫反射项，支持复杂光照分布

#### 预计算方法

**基础算法**：
1. 在三角形中心生成半球形光线集合
2. 追踪检测遮挡情况
3. 计算**可访问性**：未被遮挡的射线占比
4. 计算**平均方向**：未遮挡光线的加权方向（"弯曲法线"）

**采样技术**：
- **拒绝采样法**生成随机方向
- 在单位立方体中随机生成向量
- 拒绝超出单位球体或指向下方的方向
- 确保均匀分布

**硬件加速方案**：
- 围绕物体放置球形阴影贴图灯阵列（128-1024个灯）
- 多次渲染累积阴影贡献
- 模拟大面积光源

#### 实时着色器集成

**三步流程**：

1. **坐标转换**：3D方向→纬度-经度纹理坐标
2. **模糊计算**：基于可访问性确定过滤范围
3. **环境查询**：模糊采样后乘以可访问性值

**性能**：
- 仅需约10条GPU指令
- 支持实时性能

#### 效果对比

- **简单漫反射**：反差生硬，缺乏细节感
- **应用AO后**：裂缝暗化、暴露部分明亮、投影自然

#### 关键优势

✓ 不依赖特定光照环境（预计算与照明独立）
✓ 兼容旧硬件（仅需顶点颜色传递）
✓ 易于集成纹理和传统光源
✓ 支持动画（通过关键姿态插值）

---

### Chapter 18: Spatial BRDFs
**作者**: David McAllister

#### 核心概念

Spatial BRDF (SBRDF) - 将传统纹理映射与BRDF相结合，表面每个点存储不同反射特性。

#### 与传统BRDF的区别

- **传统BRDF**：描述单一点的光学属性
- **SBRDF**：表面各处拥有不同的反射参数
- 处理光线与表面的复杂空间变化交互

#### 纹理编码方法

**Lafortune表示法**：
- 漫反射系数 **d** 存储在一张贴图
- 每个镜面叶瓣的反照率 **s** 和形状系数 **C** 分别存储
- 八位纹理：应用缩放和偏移处理坐标范围

#### Shader实现

**两种渲染策略**：

**离散光源**：
- 直接计算点光源与表面交互

**环境贴图**：
- 预卷积环境贴图与不同指数的Phong函数
- 通过LOD采样

#### 应用优势

- 仅需10个系数
- 比RGB纹理更真实
- 性能开销主要为点积与指数运算
- 适合实时渲染

---

### Chapter 19: Image-Based Lighting
**作者**: Kevin Bjorke (NVIDIA)

#### 核心概念

基于图像的光照（IBL）技术，通过着色器数学将对象放置在特定大小和位置的反射环境中。

#### IBL原理

**突破性创新**：
- 传统立方体贴图：表现"无限远处"环境反射
- 本章技术：通过着色器将对象放置在特定位置的反射环境中
- 仅需少量额外着色器数学

#### 立方体贴图技术

**光照空间系统**：
- 半径1.0的单位立方体（范围-1.0到1.0）
- 世界坐标与光照空间的矩阵变换
- 传递顶点法线、切线、副法线数据
- 支持凹凸贴图增强真实感

#### 局部反射实现

**核心算法**：
- **球面相交计算**
- 从表面位置沿反射向量与半径1.0球体求交
- 解二次方程获得环境贴图采样位置
- 超出球体范围：红色安全色

#### 菲涅尔衰减

- 基于视角的菲涅尔衰减项
- 幂函数逼近
- 推荐指数5.0
- 较低值产生"漆面"效果

#### 扩展功能

**漫反射IBL**：
- 预卷积立方体贴图支持漫反射照明

**阴影处理**：
- 投影阴影简化
- 强调"接触阴影"连接角色与环境

**背景渲染**：
- 简化立方体几何
- 直接投影环保贴图作环境

---

### Chapter 20: Texture Bombing
**作者**: Steve Glanville

#### 核心概念

纹理轰炸通过Voronoi图和元胞技术减少大面积纹理重复感。

#### 核心思想

**原理**：
- 将UV空间划分为规则网格单元
- 在每个单元内随机位置放置小图像
- 从像素视角计算所在单元及邻近单元
- 合成最终结果

#### Voronoi图GPU实现

**距离场单元划分**：
- 以距离最近点的平方值作为优先级
- 而非随机权重
- 确定每个区域的所有权
- 增加每单元采样数减少网格规则感

**元胞技术扩展**：
- **2D→3D**：单元扩展为立方体，采样4→8个
- **多图像/单元**：循环采样增加变化性
- **随机选择**：纹理中水平排列多张图像，随机索引

#### 伪随机生成

**机制**：
- 使用低精度坐标（0.037、0.119等）
- 映射单元坐标到随机纹理
- 确保邻近单元产生不相关值

**纹理通道**：
- RGBA四通道分别存储：
  - xy: 位置偏移
  - w: 优先级
  - z: 颜色索引

#### 性能优化

- 将颜色采样移出循环（程序化形状）
- 使用定点/半精度变量（GeForce FX）
- 随机纹理用NEAREST滤波避免LOD跳变
- 图像纹理采用CLAMP寻址防止幽灵采样

> [!success] 应用价值
> 从基础实现到高级特效的完整GPU纹理技术演进路径。

---

## Part IV - Image Processing 图像处理

### Chapter 21: Real-Time Glow
**作者**: Greg James, John O'Rorke

#### 核心概念

实时辉光效果通过屏幕空间后处理，模拟强光在视觉系统中的散射。

#### 辉光原理

视觉系统对光强度敏感性有限，区分强光的唯一方式是通过周围的辉光和光晕。

#### 三阶段实现流程

**第一阶段 - 提取高亮源**：
- 使用纹理Alpha通道标记发光区域
- 场景渲染至离屏纹理
- 仅保留高亮部分

**第二阶段 - 可分离卷积模糊**：
- 采用二步高斯模糊而非2D卷积
- 复杂度从O(d²)降至O(2d)
- 关键优化：将2D卷积分解为两个1D卷积

**第三阶段 - 加法混合合成**：
- 加法透明混合将辉光叠加至原场景

#### 性能优化

**分辨率缩减**：
- 可用1/4分辨率渲染辉光纹理
- 无明显质量损失

**硬件适配**：
- DirectX 7-9多层级实现
- 2纹理采样到8纹理采样

**Render-to-Texture**：
- StretchRect函数快速拷贝和缩放

#### 参数动态控制

- 模糊权重按帧变化产生脉动效果
- 渲染风格映射表控制各对象发光行为
- 雾效参数调整缓解采样别名

#### 应用场景

- 景深效果（不同聚焦程度）
- 投影纹理阴影柔化
- 辐照度映射近似
- 非真实感渲染

> [!success] 实战案例
> 《Tron 2.0》中实现60fps+性能，证明工程可行性。

---

### Chapter 22: Color Controls
**作者**: Kevin Bjorke

#### 核心概念

技术与美术导向的色彩控制，将Photoshop级色彩调整引入实时渲染。

#### 核心技术

**两种基础方法**：
1. **Per-channel corrections**：独立修改RGB分量
2. **Color-mixing operations**：输出通道由组合RGB输入导出

#### Levels调整

**公式**（每通道）：
```
outPixel = (pow(((inPixel * 255.0) - inBlack) / (inWhite - inBlack), inGamma)
           * (outWhite - outBlack) + outBlack) / 255.0
```

**功能**：
- 独立调整对比度、gamma、动态范围
- 每通道分别控制

#### 查找表(LUT)方法

**核心思想**：
- 不复制Photoshop曲线数学
- 创建1×256像素渐变纹理
- 应用曲线后作为查找表

**Shader实现**：
```glsl
OutColor.r = tex1D(ColorCorrMap, InColor.r).r;
```

**优势**：
- 捕获任意曲线变换
- 简单纹理查找

#### 多通道转换

**灰度转换**：
- 点积使用ITU Rec 709权重
- `float3(0.222, 0.707, 0.071)`

**色彩空间转换**：
- 3×3矩阵乘法
- RGB → CIE/sRGB/Adobe RGB等

#### DCC工具集成

**工作流**：
1. 美术在Photoshop中定义调整
2. 保存为`.acv`曲线文件
3. 直接影响纹理生成
4. 桥接美术工具与实时着色器

---

### Chapter 23: Depth of Field
**作者**: Joe Demers

#### 核心概念

GPU实现景深（DOF）效果，模拟真实相机对焦特性。

#### 光学原理

**物理基础**：
- 焦点范围内的物体清晰
- 焦点外的物体模糊
- 模糊量化为**Circle of Confusion (CoC)**

**CoC计算**：
```
CoC = abs(aperture * (focallength * (objectdistance - planeinfocus))
      / (objectdistance * (planeinfocus - focallength)))
```

#### 五种实现技术

**1. 光线追踪**：
- 在透镜表面分布采样
- 物理精确但非实时

**2. 累积缓冲**：
- 从不同透镜位置渲染多次
- 混合结果
- 需50+遍才能产生微妙效果

**3. 分层方法**：
- 分割场景为深度层
- 每层应用uniform blur
- 快速但在物体跨层时产生人工边缘

**4. 正向映射Z-Buffer**：
- 基于sprite的splatting
- 离线效果好但实时昂贵

**5. 反向映射Z-Buffer**：
- 基于深度应用变化模糊
- 通过mipmap或纹理查找
- 最适合实时GPU实现

#### 关键伪影与解决

**深度不连续**：
- 读取多个深度值减少halo
- 偏置CoC添加额外模糊

**双线性插值**：
- 抖动采样或summed-area table替代

**像素渗色**：
- 分层渲染部分解决颜色泄漏

#### 性能权衡

没有单一算法平衡质量和速度。实时应用通常牺牲着色正确性换取速度，接受一些视觉伪影。

---

### Chapter 24: High-Quality Filtering
**作者**: 多位作者

#### 核心概念

GPU硬件虽快速但功能受限，自定义滤波方法提供更高质量和灵活性。

#### 滤波核设计

**卷积操作**：
- 通过定义的权重模式变换源像素
- 生成目标图像

**优化策略**：
- 预先计算权重
- 利用辅助纹理通道减少采样次数
- 针对灰度数据使用助手纹理（邻域偏移）

**双三次滤波**：
- 使用查找表实现高质量图像缩放
- 避免"生硬"方形像素伪影

#### 解析计算技术

**偏导数函数**：
- `ddx()`和`ddy()`获取像素间变化量
- 确定适当滤波范围

**条纹反锯齿**：
- 利用积分函数
- 计算像素跨度内条纹覆盖比例
- 平滑边界而非锯齿状伪影

#### 应用场景

- 图像处理
- 纹理重采样
- 非真实感渲染
- 视频格式转码（YCbCr解码）
- 边缘检测

---

### Chapter 25: Fast Filter-Width Estimates
**作者**: Matt Pharr

#### 核心概念

使用纹理操作快速估算滤波宽度，服务于程序纹理反走样。

#### 核心问题

程序纹理需要反走样处理：
- 计算像素周围区域的平均值
- 而非单点采样
- 避免锯齿状伪影

#### 纹理操作方法

**巧妙技术**：
- 利用mipmap各层级填充特定值
- 每层存储对应分辨率的log2值×16
- 硬件自动选择合适mipmap层级
- 反推出滤波宽度

#### 偏导数替代

**某些硬件不支持ddx()/ddy()**：
- 通过tex2D()查询特殊构建纹理
- 返回值告诉实际选择的mipmap层级
- 间接获得空间导数信息

#### 性能与限制

**优势**：
- 仅需3条指令
- 性能相当

**缺陷**：
- 极端情况可能高估或低估
- 超出mipmap范围时不准确

**改进**：
- 缩放纹理坐标重新查询提高精度

---

### Chapter 26: The OpenEXR Image File Format
**作者**: Florian Kainz, Rod Bogart, Drew Hess (ILM)

#### 核心概念

工业光魔开发的高动态范围（HDR）图像格式。

#### 核心特性

**数据精度**：
- 16位浮点"half"精度色彩值
- 支持多图像通道with不同数据类型
- 无损压缩选项（PIZ、ZIP、RLE）
- 完整C++ API with RGBA接口

#### HDR数据存储

**动态范围**：
- 保存超出典型显示限制（0.0-1.0）的亮度信息
- Half精度：5.96×10⁻⁸ 到 65,504.0
- 约一万亿比一的动态范围

**处理优势**：
- 压暗过曝图像时保持自然效果
- 传统格式压暗产生灰色伪影

#### 与传统格式区别

**JPEG/标准格式**：
- 裁剪亮值
- 丢失过曝数据

**OpenEXR**：
- 保留过曝数据
- 后期处理保持自然

#### 工业应用

- 视觉特效合成和图像处理
- 3D渲染环境映射
- 景深和运动模糊效果
- 色彩校正工作流
- 实时GPU渲染with正确线性色彩空间

---

### Chapter 27: A Framework for Image Processing
**作者**: Frank Jargstorff

#### 核心概念

集成GPU和CPU的图像处理框架，采用三层设计模式。

#### 核心架构

**三层设计**：
- **源操作符(SourceOperator)**：生成图像数据
- **滤波器(ImageFilter)**：继承源和汇，执行处理
- **汇操作符(SinkOperator)**：消费最终结果

**数据模型**：
- "拉取"数据模型
- 结果节点主动从输入获取数据

#### GPU/CPU协作

**分工**：
- GPU：像素级操作
- CPU：流程控制

**技术细节**：
- 屏幕对齐四边形渲染至不可见缓冲区
- 16位浮点（half）精度平衡性能与精度
- WGL扩展实现渲染到纹理
- 数据无需在内存间移动

#### 滤波链设计

**递归脏检查**：
- 追踪上游参数变化
- 图像使用引用计数管理
- Image代理Buffer对象

**Cg实现**：
- 单个滤波器通过片元着色器实现不同效果

#### 性能考虑

**加速效果**：
- 十倍加速已被测量（合理的图像处理问题）

**要求**：
- 需饱和CPU和GPU工作负荷
- 硬件限制（纹理尺寸、显存）需通过分块等工程方案克服

---

## Part V - Performance and Practicalities 性能与实践

### Chapter 28: Graphics Pipeline Performance
**作者**: Cem Cebenoyan (NVIDIA)

#### 核心概念

系统化GPU管道瓶颈识别与优化策略。

#### GPU瓶颈识别方法论

**核心识别循环**：
1. 变化每个管道阶段的工作负荷或计算能力
2. 测量性能变化定位瓶颈
3. 优化该特定阶段
4. 重复直到达到性能目标

**关键原则**：
- 管道速度取决于最慢阶段
- 多处理器系统中盲目优化适得其反

#### 性能分析技术

**按阶段测试方法**：

| 阶段 | 测试方法 | 时钟因素 |
|------|---------|---------|
| **ROP** | 调整颜色/深度位深度 | GPU内存时钟 |
| **纹理带宽** | 应用正mipmap LOD偏移 | GPU内存时钟 |
| **片段着色** | 修改分辨率；调整shader复杂度 | GPU核心时钟 |
| **顶点处理** | 改变顶点程序长度 | GPU核心时钟 |
| **顶点传输** | 修改顶点格式大小 | AGP/PCIe或内存时钟 |

**细粒度方法**：
- 按对象或材质逐个变化工作负荷
- 瓶颈通常在帧渲染过程中转移

#### 各阶段优化策略

**CPU级优化**：
- 最小化资源锁定操作（防止GPU管道停顿）
- 最大化批次大小（减少API调用开销）
- 使用shader分支和常量内存查找表

**顶点处理**：
- 优化后变换顶点缓存利用率（索引排序）
- 实现顶点级LOD（远距离几何）
- 移动每对象计算到CPU

**片段着色**：
- 先渲染depth-only pass（减少片段处理）
- 复杂数学函数存储为纹理查找表
- 移动每顶点计算到顶点着色器
- 使用最低必要精度
- 不必要时禁用三线性过滤

**内存带宽**：
- DXT格式压缩颜色纹理
- 缩小表面实现适当mipmapping
- 前到后渲染（最大化early-Z优化）
- 可接受时使用16位缓冲

#### 测试方法论

**诊断流程图**：
1. 从帧缓冲开始向后工作
2. 开始ROP评估
3. 进入纹理带宽评估
4. 测试片段和顶点处理阶段
5. 通过CPU降频验证CPU瓶颈

**关键洞察**：
- 修改多个管道阶段的工作负荷通常产生不同影响
- 需要细粒度测试方法

#### 实战建议

**批处理策略**：
- 使用退化三角形合并不相交strips
- 实现纹理图集（减少材质批次中断）
- 利用shader分支实现条件处理路径

**内存层次优化**：
- 按顺序访问顶点数据（最大化缓存局部性）
- 按空间参考局部性排序原语
- 优先使用索引原语（顶点缓存有效性）

**质量-性能平衡**：
- 使用各向异性过滤而非禁用mipmapping
- 仅必要时使用浮点帧缓冲
- 多遍渲染中关闭深度写入

> [!tip] 核心原则
> 系统化瓶颈识别必须先于优化工作，防止在非约束阶段浪费开发周期。

---

### Chapter 29: Efficient Occlusion Culling
**作者**: Dean Sekulic (Croteam)

#### 核心概念

通过硬件遮挡查询提升渲染性能，跳过视锥外或被遮挡的几何体。

#### 核心概念

**两种主要方法**：
- **遮挡查询**：几何级别拒绝（GeForce3+）
- **Early-Z拒绝**：光栅化阶段每片段剔除

**关键区别**：
- 遮挡查询在几何级别拒绝多边形
- Early-Z在光栅化级别工作

#### 硬件遮挡查询机制

**处理流程**：
1. 禁用颜色/深度缓冲写入
2. 开始查询并渲染对象的包围盒
3. 结束查询获取可见像素数
4. 如果数量 > 阈值，渲染完整对象

**关键洞察**：
GPU报告"经过所有管道测试后应该出现在屏幕上的像素数"。

#### 实现策略

**关键问题 - 管道停顿**：
- 朴素方法导致CPU-GPU同步瓶颈

**解决方案 - 跨帧延迟查询**：
- 当前帧查询可见性，下一帧检查结果
- 上帧可见对象完全渲染（作为遮挡物）
- 先前不可见对象仅测试包围盒

**优势**：
- 消除GPU停顿
- 1帧延迟可接受

#### 优化技术

**排序策略**：
- 分离不透明对象（前到后）和半透明对象（后到前）
- 不透明对象自动成为遮挡物
- 使后续剔除更有效

**包围盒细化**：
- **静态对象**：复杂几何使用多个子盒（金字塔示例）
- **动画模型**：存储每动画盒而非每帧盒

#### 常见陷阱

**填充率限制**：
- 高分辨率+简单shader时
- 包围盒可能需要比对象更多像素处理

**近距离对象**：
- 观察者接近包围盒内部时跳过测试
- 背面剔除导致误报

**简单几何无效**：
- ~300三角形以下对象改善最小

**CPU开销**：
- 简单对象（200三角形）查询成本可能超过直接渲染

**性能阈值**：
- 对象超过1000三角形时显示"超过两倍"加速

---

### Chapter 30-31: FX Composer
**作者**: Christopher Maughan (NVIDIA)

#### 核心概念

NVIDIA FX Composer着色器开发工具的设计理念与实际使用。

#### Chapter 30 - 设计目标

**核心目标**：
- 熟悉的IDE界面（类似Visual Studio .NET）
- 可扩展架构（支持未来Direct3D升级）
- 稳定创作环境（.fx文件编辑和可视化）
- 目标用户：编程开发者和技术美术

**核心功能**：
- 材质面板：显示多个.fx文件在3D对象上的效果
- 纹理面板：展示渲染目标和材质纹理
- 编辑器窗口：撤销/重做、书签、语法高亮
- 渲染窗口：显示应用特效的简单场景

**着色器开发工作流**：
- 基于COM的接口系统（即插即用架构）
- 支持参数动画和关键帧插值
- "几何管道"系统自动适配着色器输入语义
- 三种蒙皮策略支持不同模型

**DCC工具集成**：
- 混合型项目文件（XML + ZIP二进制）
- 支持.x和.nvb格式导入
- 对象支持XML流接口（灵活序列化）
- 插件系统（自定义导入器和几何处理器）

#### Chapter 31 - 实际使用

**项目加载**：
- 需DirectX 9 2003 Summer Update
- File...Load Project加载样本（如alien_gooch.fxcomposer）
- 导入模型后从材质面板选择效果

**主要界面功能**：

| 面板 | 功能 |
|------|------|
| **材质面板** | 快速预览效果无需应用到场景 |
| **编辑器** | 语法高亮和IntelliSense |
| **属性面板** | 调整颜色、数值、向量和矩阵 |
| **场景图** | 树形结构管理对象和灯光 |
| **着色器性能** | 查看汇编代码和芯片优化 |

**调试技巧**：
- Tasks面板中的错误直接链接到编辑器
- 红色线框：无效效果
- 蓝色线框：硬件不兼容
- Textures面板：实时显示渲染目标

---

### Chapter 32: Shader Interfaces
**作者**: Matt Pharr

#### 核心概念

着色器接口实现抽象编程，允许运行时绑定实现而无需重新编译。

#### 设计原则

- **模块化**：从可重用片段组合着色器
- **运行时灵活性**：运行时绑定实现无需重编译
- **零性能成本**：最终GPU代码仅在绑定解析后生成
- **类型安全**：编译时验证with运行时绑定

#### 参数绑定机制

**运行时流程**：
1. 禁用自动编译：`cgSetAutoCompile(context, CG_COMPILE_MANUAL)`
2. 创建接口实现：`cgCreateParameter()`
3. 连接实现到参数：`cgConnectParameter()`
4. 编译最终程序：`cgCompileProgram()`

#### 跨平台考虑

- 未定大小数组`[]`（运行时确定可变长度集合）
- 单个接口实例可跨同一上下文中的多个程序共享
- 支持层级组合（接口包含其他接口）
- 减少对预处理器指令和字符串代码生成的依赖

---

### Chapter 33: Converting Production RenderMan Shaders
**作者**: Stephen Marshall (Sony Pictures Imageworks)

#### 核心概念

将离线RenderMan着色器转换为实时GPU着色器的挑战与策略。

> [!info] 章节状态
> 本章URL在NVIDIA网站上404。核心内容涉及Sony Pictures Imageworks的生产经验。

**主要挑战**：
- RenderMan支持任意复杂度计算
- GPU实时限制
- 着色语言差异

**典型策略**：
- 预计算复杂项为纹理
- 简化算法保持视觉相似
- LOD策略平衡质量和性能

---

### Chapter 34-36: Shader Integration
**作者**: 多位作者

#### 核心概念

将GPU着色器集成到商业3D应用（Cinema 4D、RenderMan等）的工程实践。

**集成挑战**：
- 不同API和平台
- DCC工具现有工作流
- 美术师友好界面

**通用策略**：
- 插件架构
- 着色器参数自动UI生成
- 预览渲染集成
- 与现有材质系统桥接

---

## Part VI - Beyond Triangles 超越三角形

### Chapter 37: GPU Programming Toolkit
**作者**: Ian Buck, Tim Purcell

#### 核心概念

GPU通用计算工具包，将GPU作为通用并行处理器的早期探索。

#### GPU通用计算的理由

**性能对比（2004年）**：
- GeForce FX 5900 Ultra：20亿次乘法/秒
- Pentium 4：~60亿次/秒
- GPU内存带宽：25.3 GB/sec
- CPU内存带宽：5.96 GB/sec

**性能增速**：
- GPU：每年增长24 Gigaflops
- CPU：每年增长0.65 Gigaflops

#### 数据并行编程模型

**流处理架构**：
- 对数据流应用kernel函数并行处理
- 每个数据元素独立计算，无相互依赖
- "mandatory parallelism"约束决定可映射算法

**粒子系统示例**：
- 粒子位置存储为纹理
- 渲染四边形触发片段着色器
- 并行更新所有粒子

#### GPU排序/搜索算法

**Bitonic Merge Sort（双调排序）**：
- O(log² n)复杂度的并行排序
- 每个渲染通道执行比较-交换阶段
- 100万元素需210个渲染通道

**Binary Search（二分搜索）**：
- 单通道片段程序实现
- 支持并行搜索多个grid cells
- 搜索100万元素<1毫秒

#### 实现技巧

**Reduce操作**：
- 多通道缩小处理范围
- O(log n)复杂度规约（如求最大值）

**纹理坐标映射**：
- `convert1dto2d`函数
- 1D数组地址→2D纹理坐标

**Uniform Grid数据结构**：
- 通过排序+搜索构建空间加速结构
- 用于碰撞检测

#### 性能与限制

**优势**：
- 减少CPU-GPU数据传输
- 数据保持在GPU显存中

**限制**：
- 片段着色器输出受限（单/多个四分量向量）
- 回读性能瓶颈（AGP 1x上传 vs 8x下载）
- 并非所有CPU算法适合GPU

> [!note] 历史意义
> 2004年的GPGPU先驱工作，为后来的CUDA/OpenCL奠定基础。

---

### Chapter 38: Fast Fluid Dynamics on the GPU
**作者**: Mark J. Harris (UNC Chapel Hill)

#### 核心概念

GPU上的实时流体动力学模拟，求解不可压缩流的Navier-Stokes方程。

#### 物理基础

**Navier-Stokes方程**：
- 支配速度和压力场
- "流体的速度导致流体沿流动传输对象、密度和其他量"

**四个关键加速项**：
- **Advection（对流）**：速度的自传输
- **Pressure（压力）**：通过流体传播力
- **Diffusion（扩散）**：粘性效应
- **External forces（外力）**：用户输入和体力

#### 数学框架

**Helmholtz-Hodge分解定理**：
- 任何矢量场可分解为无散度分量和压力梯度
- 引出**Poisson-pressure方程**求解
- 在计算中间速度更新后保持不可压缩性

#### GPU实现策略

**纹理作为数据**：
- 纹理=数据数组
- 片段程序=并行计算kernel

**模拟管线**：
1. **Advection**：半拉格朗日积分回溯粒子路径（大时间步稳定）
2. **Diffusion**：通过隐式拉普拉斯算子求解粘性
3. **Force Application**：添加外部加速度
4. **Projection**：通过迭代Poisson求解强制零散度

#### 迭代求解器

**Jacobi迭代**：
- 在GPU上高效求解Poisson方程
- 收敛比multigrid方法慢
- 通常40-80次迭代平衡精度和性能

#### 性能收益

**加速效果**：
- NVIDIA GeForce FX硬件上
- 相比等效CPU模拟"最多6倍加速"
- 证明交互式应用的实时能力

---

### Chapter 39: Volume Rendering Techniques
**作者**: Milan Ikits, Joe Kniss, Aaron Lefohn, Charles Hansen

#### 核心概念

GPU加速的直接体积渲染技术，无需显式提取几何表面。

#### 核心方法

**直接体积渲染**：
- 不显式提取几何表面生成图像
- 使用"光学模型将数据值映射到光学属性（颜色和不透明度）"
- 沿视线累积光学属性形成图像

#### 光线投射技术

作为纹理方法的替代方案，光线投射是另一种GPU加速体积渲染算法（Roettger 2003, Krüger 2003）。

#### 2D vs. 3D纹理存储

**3D纹理方案**：
- 使用垂直于视向的视对齐切片平面
- 更节省内存（无数据复制）
- 采样距离随视点变化

**2D纹理切片**：
- 需要3倍内存（数据复制）
- 更快切片生成但产生采样伪影
- 切换视点时强度变化和图像跳跃

#### 传输函数

**核心功能**：
- "将颜色和不透明度分配给数据值"强调特征

**类型**：
- 1D查找表：标量值→颜色
- 2D传输函数：结合梯度幅值数据
- 不透明度校正：基于采样率变化（依赖纹理查找）

#### 性能优化

**关键考虑**：
- **光栅化瓶颈**：通过空白空间跳跃仅绘制必需片段
- **片段复杂度**：平衡shader操作与纹理内存访问
- **纹理效率**：将数据打包入RGBA元组减少带宽压力
- **质量-速度权衡**：调整切片数量和采样率

---

### Chapter 40: Real-Time 3D Ultrasound Visualization
**作者**: Thilaka Sumanaweera

#### 核心概念

医学超声数据的实时3D可视化，应用实时着色技术。

#### 特殊挑战

**非笛卡尔网格**：
- 超声数据采集于锥形网格
- "与CT和MRI相比，超声数据体积渲染更复杂"
- 数据从探头向体内发散
- 需要特殊坐标变换

#### 实时着色应用

**顶点和片段着色器**：
- 顶点程序：生成金字塔形坐标的纹理坐标
- 片段程序："3D投影纹理查询"并应用颜色映射
- 实现快速体积渲染

#### 体积数据处理

**切平面技术**：
- 逐层渲染
- "平行于屏幕的切平面"从远到近合成
- 配合alpha混合实现透明度

#### 医疗成像需求

**4D超声**：
- 三维空间 + 时间维度
- "特别适用心脏功能和胎儿异常（腭裂）诊断"
- 满足动态成像帧率要求

---

### Chapter 41: Real-Time Stereograms
**作者**: Fabio Policarpo

#### 核心概念

单图随机点立体图（SIRDS）的GPU实时生成。

#### 立体图原理

**定义**：
- "在2D图像中编码立体信息"
- "正确观看时揭示隐藏的3D场景"
- 基于两眼视差原理
- 眼睛位置差异产生深度感知

#### GPU生成算法

**分条带渲染**：
- 将深度图分为N条垂直条带
- 逐条处理
- 第一条带作参考
- 后续条带通过片段着色器根据深度值计算像素偏移
- 从前一条带采样颜色

#### 深度编码方法

**位移计算**：
```
displace = depthmap_value * factor * strip_width
```

**控制参数**：
- 深度值反转改变视觉效果
- 调整条带数量改变眼睛聚焦距离

#### 性能实现

**Z-Buffer集成**：
- "启用时，程序使用的深度图从z-buffer获取"
- 每帧更新深度图
- 实现交互式3D场景与立体图同步渲染

---

### Chapter 42: Deformers
**作者**: Eugene d'Eon

#### 核心概念

GPU变形器技术与顶点法线计算的数学方法。

#### 变形器定义

**数学形式**：
- "接收顶点集合并生成新坐标的操作"
- 向量函数：**f**(*x*, *y*, *z*) = (*fx*, *fy*, *fz*)

**核心特性**：
- 顶点数量保持不变
- 单个顶点变形独立（不受邻接顶点影响）
- 操作确定性（相同输入→相同输出）

**应用**：
- 平移
- 波形
- 弯曲
- 扭转

#### 顶点法线计算方法

**挑战**：
- 传统软件需重新遍历网格计算邻接关系
- GPU顶点着色器无法访问相邻顶点

**两种解决方案**：

**1. 数值近似法**：
- 对每个顶点变形三个点
- 沿切线和副法线轻微偏移
- 通过叉积估算变形后法线

**2. 雅可比矩阵法（推荐）**：
- 计算变形函数的一阶偏导数矩阵
- 两种等价方式变换法线：
  - 使用逆转置矩阵直接变换
  - 变换切线和副法线后计算叉积

#### GPU实现

**顶点程序流程**：
1. 将变形函数参数化
2. 通过uniform输入传递控制参数和时间
3. 计算雅可比矩阵
4. 变换切线/副法线
5. 叉积得新法线
6. 重新归一化

**性能优势**：
- 雅可比方法相比变形三个顶点更高效
- 可重复利用计算表达式

#### 应用限制

- 面片化网格可能产生不连续结果
- 要求雅可比矩阵可逆（行列式非零）
- 需要解析可微函数
- 顶点程序长度限制（复杂变形可能超出指令预算）

> [!tip] 数学洞察
> 雅可比矩阵方法是计算变形后法线的数学上正确和高效的方法。

---

## 💡 核心价值总结

### 与RTR4、PBRT4的关系

| 维度 | **GPU Gems 1** | **RTR4** | **PBRT4** |
|------|---------------|----------|-----------|
| **定位** | 实战技巧合集 | 理论教材 | 实现参考 |
| **深度** | 具体实现 | 全面理论 | 物理精确 |
| **代码** | Shader代码 | 伪代码 | 完整C++17 |
| **时代** | 2004（DX9/OGL2） | 2018（现代管线） | 2023（路径追踪） |
| **价值** | 实战经验 | 理论框架 | 精确实现 |

### 学习建议

**适合人群**：
- ✅ 有基础图形学知识
- ✅ 想学习具体shader实现
- ✅ 需要实战技巧和优化经验
- ✅ 研究GPU计算的早期探索

**与现代技术对比**：
- 🕐 硬件限制（2004年GPU）
- 🔄 很多技术已演进（如阴影技术）
- ⭐ 核心思想仍然有效
- 📚 补充RTR4的具体实现细节

---

## ⚠️ 版权声明

本笔记仅包含技术要点总结和概念提取，不含原书的完整内容。
完整内容请访问NVIDIA官方在线版本（免费）。

**原书版权**：© 2004 NVIDIA Corporation and Addison-Wesley

---

## 🤝 贡献

欢迎提出改进建议！

---

*笔记整理：Master + Claude*
*最后更新：2026-03-05*
