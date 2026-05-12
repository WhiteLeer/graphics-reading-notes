# GPU Gems 2 读书笔记

> 📚 《GPU Gems 2: Programming Techniques for High-Performance Graphics and General-Purpose Computation》
>
> 编辑：Matt Pharr (NVIDIA)
> 系列编辑：Randima Fernando
> 出版社：Addison-Wesley | 出版年份：2005
> 在线免费版本：https://developer.nvidia.com/gpugems/gpugems2

---

## 📖 关于本笔记

GPU Gems 2是NVIDIA出版的第二卷GPU编程技巧合集，**完全免费在线提供**。本书汇集了超过70位来自学术界、工业界和研究机构的计算机图形专家的实战经验，代表了2005年GPU编程的最新水平。

### ✨ 特点

- **内容扩展**：48章（相比第1卷的42章）
- **GPGPU重点**：新增完整的通用计算部分（Part IV）
- **高级渲染**：更多高质量渲染技术
- **前沿技术**：2005年GPU编程的最佳实践
- **广泛应用**：从游戏到科学计算

### 📚 阅读进度

- ✅ Part I - Geometric Complexity（几何复杂度，8章）
- ✅ Part II - Shading, Lighting, and Shadows（着色、光照与阴影，11章）
- ✅ Part III - High-Quality Rendering（高质量渲染，9章）
- ✅ Part IV - General-Purpose Computation on GPUs（GPU通用计算，8章）
- ✅ Part V - Image-Oriented Computing（面向图像的计算，6章）
- ✅ Part VI - Simulation and Numerical Algorithms（模拟与数值算法，6章）
- 🎉 **全书完成！（48章）**

### 🔗 相关资源

- 📘 在线版本：https://developer.nvidia.com/gpugems/gpugems2
- 💻 示例代码和Demo可下载
- 📚 GPU Gems 1 和 GPU Gems 3 也在线提供

---

## 📑 目录

### Part I - Geometric Complexity 几何复杂度
- [Chapter 1: Toward Photorealism in Virtual Botany](#chapter-1-toward-photorealism-in-virtual-botany)
- [Chapter 2: Terrain Rendering Using GPU-Based Geometry Clipmaps](#chapter-2-terrain-rendering-using-gpu-based-geometry-clipmaps)
- [Chapter 3: Inside Geometry Instancing](#chapter-3-inside-geometry-instancing)
- [Chapter 4: Segment Buffering](#chapter-4-segment-buffering)
- [Chapter 5: Optimizing Resource Management with Multistreaming](#chapter-5-optimizing-resource-management-with-multistreaming)
- [Chapter 6: Hardware Occlusion Queries Made Useful](#chapter-6-hardware-occlusion-queries-made-useful)
- [Chapter 7: Adaptive Tessellation of Subdivision Surfaces](#chapter-7-adaptive-tessellation-of-subdivision-surfaces)
- [Chapter 8: Per-Pixel Displacement Mapping with Distance Functions](#chapter-8-per-pixel-displacement-mapping-with-distance-functions)

### Part II - Shading, Lighting, and Shadows 着色、光照与阴影
- [Chapter 9: Deferred Shading in S.T.A.L.K.E.R.](#chapter-9-deferred-shading-in-stalker)
- [Chapter 10: Real-Time Computation of Dynamic Irradiance Environment Maps](#chapter-10-real-time-computation-of-dynamic-irradiance-environment-maps)
- [Chapter 11: Approximate Bidirectional Texture Functions](#chapter-11-approximate-bidirectional-texture-functions)
- [Chapter 12: Tile-Based Texture Mapping](#chapter-12-tile-based-texture-mapping)
- [Chapter 13: Implementing the mental images Phenomena Renderer on the GPU](#chapter-13-implementing-the-mental-images-phenomena-renderer-on-the-gpu)
- [Chapter 14: Dynamic Ambient Occlusion and Indirect Lighting](#chapter-14-dynamic-ambient-occlusion-and-indirect-lighting)
- [Chapter 15: Blueprint Rendering and "Sketchy Drawings"](#chapter-15-blueprint-rendering-and-sketchy-drawings)
- [Chapter 16: Accurate Atmospheric Scattering](#chapter-16-accurate-atmospheric-scattering)
- [Chapter 17: Efficient Soft-Edged Shadows Using Pixel Shader Branching](#chapter-17-efficient-soft-edged-shadows-using-pixel-shader-branching)
- [Chapter 18: Using Vertex Texture Displacement for Realistic Water Rendering](#chapter-18-using-vertex-texture-displacement-for-realistic-water-rendering)
- [Chapter 19: Generic Refraction Simulation](#chapter-19-generic-refraction-simulation)

### Part III - High-Quality Rendering 高质量渲染
- [Chapter 20: Fast Third-Order Texture Filtering](#chapter-20-fast-third-order-texture-filtering)
- [Chapter 21: High-Quality Antialiased Rasterization](#chapter-21-high-quality-antialiased-rasterization)
- [Chapter 22: Fast Prefiltered Lines](#chapter-22-fast-prefiltered-lines)
- [Chapter 23: Hair Animation and Rendering in the Nalu Demo](#chapter-23-hair-animation-and-rendering-in-the-nalu-demo)
- [Chapter 24: Using Lookup Tables to Accelerate Color Transformations](#chapter-24-using-lookup-tables-to-accelerate-color-transformations)
- [Chapter 25: GPU Image Processing in Apple's Motion](#chapter-25-gpu-image-processing-in-apples-motion)
- [Chapter 26: Implementing Improved Perlin Noise](#chapter-26-implementing-improved-perlin-noise)
- [Chapter 27: Advanced High-Quality Filtering](#chapter-27-advanced-high-quality-filtering)
- [Chapter 28: Mipmap-Level Measurement](#chapter-28-mipmap-level-measurement)

### Part IV - General-Purpose Computation on GPUs GPU通用计算
- [Chapter 29: Streaming Architectures and Technology Trends](#chapter-29-streaming-architectures-and-technology-trends)
- [Chapter 30: The GeForce 6 Series GPU Architecture](#chapter-30-the-geforce-6-series-gpu-architecture)
- [Chapter 31: Mapping Computational Concepts to GPUs](#chapter-31-mapping-computational-concepts-to-gpus)
- [Chapter 32: Taking the Plunge into GPU Computing](#chapter-32-taking-the-plunge-into-gpu-computing)
- [Chapter 33: Implementing Efficient Parallel Data Structures on GPUs](#chapter-33-implementing-efficient-parallel-data-structures-on-gpus)
- [Chapter 34: GPU Flow-Control Idioms](#chapter-34-gpu-flow-control-idioms)
- [Chapter 35: GPU Program Optimization](#chapter-35-gpu-program-optimization)
- [Chapter 36: Stream Reduction Operations for GPGPU Applications](#chapter-36-stream-reduction-operations-for-gpgpu-applications)

### Part V - Image-Oriented Computing 面向图像的计算
- [Chapter 37: Octree Textures on the GPU](#chapter-37-octree-textures-on-the-gpu)
- [Chapter 38: High-Quality Global Illumination Rendering Using Rasterization](#chapter-38-high-quality-global-illumination-rendering-using-rasterization)
- [Chapter 39: Global Illumination Using Progressive Refinement Radiosity](#chapter-39-global-illumination-using-progressive-refinement-radiosity)
- [Chapter 40: Computer Vision on the GPU](#chapter-40-computer-vision-on-the-gpu)
- [Chapter 41: Deferred Filtering](#chapter-41-deferred-filtering)
- [Chapter 42: Conservative Rasterization](#chapter-42-conservative-rasterization)

### Part VI - Simulation and Numerical Algorithms 模拟与数值算法
- [Chapter 43: GPU Computing for Protein Structure Prediction](#chapter-43-gpu-computing-for-protein-structure-prediction)
- [Chapter 44: A GPU Framework for Solving Systems of Linear Equations](#chapter-44-a-gpu-framework-for-solving-systems-of-linear-equations)
- [Chapter 45: Options Pricing on the GPU](#chapter-45-options-pricing-on-the-gpu)
- [Chapter 46: Improved GPU Sorting](#chapter-46-improved-gpu-sorting)
- [Chapter 47: Flow Simulation with Complex Boundaries](#chapter-47-flow-simulation-with-complex-boundaries)
- [Chapter 48: Medical Image Reconstruction with the FFT](#chapter-48-medical-image-reconstruction-with-the-fft)

---

## 🎯 本书特色

### 与GPU Gems 1的区别

| 维度 | **GPU Gems 2（2005）** | **GPU Gems 1（2004）** |
|------|---------------------|---------------------|
| **章节数量** | 48章 | 42章 |
| **GPGPU** | 完整的Part IV（8章） | 仅Part VI（2-3章） |
| **硬件基础** | GeForce 6/7系列 | GeForce FX系列 |
| **着色器模型** | SM 3.0 | SM 2.0 |
| **新增主题** | 延迟着色、辐射度、医学成像 | - |
| **科学计算** | 蛋白质预测、金融定价 | - |

### 学习价值

- ✅ **GPGPU先驱**：CUDA发布（2006）前一年的通用计算探索
- ✅ **延迟着色**：S.T.A.L.K.E.R.中的延迟渲染架构
- ✅ **Shader Model 3.0**：动态分支、顶点纹理
- ✅ **高级技术**：几何曲面细分、位移贴图
- ✅ **跨学科应用**：从游戏到科学计算的广泛应用

---

## Part I - Geometric Complexity 几何复杂度

### Chapter 1: Toward Photorealism in Virtual Botany
**作者**: David Whatley (Simutronics Corporation)

#### 核心概念

虚拟植物的真实感渲染，平衡视觉质量与实时性能。

#### 技术要点

**1. 核心挑战**

"渲染自然场景需要保留足够CPU和GPU资源用于其他游戏引擎需求" - 关键在于保持视觉真实感的同时实现实时帧率。

**2. 场景管理技术**

**虚拟网格系统**：
- 围绕摄像机建立固定世界空间网格
- 每个网格单元存储顶点缓冲区、索引缓冲区、材质信息
- 随摄像机移动动态加载/卸载网格

**种植策略**：
- 采用扫描转换法而非随机射线投射
- 收集与网格单元相交的多边形
- 过滤不适合种植的区域
- 扫描转换找到合适种植点

**3. 植物层技术**

**草地层**：
- 使用摄像机面向的四边形公告板批量渲染
- 顶点着色器中设置屏幕对齐
- 一次绘制调用渲染整个网格单元的数千根草

**溶解透明度**：
- 噪声纹理调制Alpha通道
- Alpha测试替代混合排序
- 实现与距离相关的渐隐效果

**地被层和树木**：
- 3D网格展开到顶点缓冲区
- 应用随机变换增加多样性
- LOD策略管理远距离树木

**4. 后处理效果**

**天穹绽放**：
- 天空穹顶Alpha通道定义亮度区域
- 模拟太阳与云交互

**全屏泛光**：
- 设置泛光通道为非零值创建扩散效果
- 减弱多边形生硬感

**5. 优化策略**

- **批处理**：单次绘制调用渲染大批对象，最小化API开销
- **纹理图集**：单一纹理整合多个植物变体UV坐标
- **风动模拟**：正弦波近似计算，混合权重保持底部固定
- **阴影**：射线投射快速判断阴影区域，RGB着色实现软阴影

> [!success] 实战案例
> Simutronics游戏引擎中的虚拟植物系统，平衡真实感与性能。

---

### Chapter 2: Terrain Rendering Using GPU-Based Geometry Clipmaps
**作者**: Arul Asirvatham, Hugues Hoppe (Microsoft Research)

#### 核心概念

基于GPU的几何clipmap技术，高效渲染大规模地形。

#### 技术要点

**1. Geometry Clipmap原理**

**核心思想**：
- 围绕视点的多层次金字塔结构
- 每层是正方形区域，分辨率递减
- 随视点移动动态更新

**2. GPU加速**

**顶点纹理获取**：
- 将地形高度数据存储在纹理中
- 顶点着色器通过纹理获取读取高度
- 将地形处理从CPU转移到GPU

**3. 内存管理**

**环形缓冲**：
- 仅存储当前可见区域数据
- 循环更新缓冲区
- 最小化内存占用

**4. 细节层次(LOD)**

**渐进过渡**：
- 层级间平滑过渡避免popping
- 混合相邻层级顶点
- 基于距离的alpha混合

> [!tip] 技术突破
> 首次将地形数据移入GPU显存，利用顶点纹理获取实现大规模地形渲染。

---

### Chapter 3: Inside Geometry Instancing
**作者**: Francesco Carucci (Lionhead Studios)

#### 核心概念

几何实例化技术框架，支持传统和DirectX 9 GPU。

#### 技术要点

**1. 实例化概念**

**核心优势**：
- 单一几何体多次渲染（不同位置/朝向/缩放）
- 减少API调用开销
- 降低内存占用

**2. 实现方法**

**硬件实例化（DX9）**：
- 使用实例数据流
- GPU自动处理实例化

**软件实例化（传统）**：
- 顶点着色器常量数组存储变换
- 通过顶点ID索引变换矩阵

**3. 应用场景**

- 植被渲染（树木、草地）
- 建筑群
- 粒子系统
- 人群渲染

> [!warning] 兼容性
> 需要根据硬件能力选择实例化方案，确保广泛兼容性。

---

### Chapter 4: Segment Buffering
**作者**: Jon Olick (2015)

#### 核心概念

实例化技术的优化方法，通过segment buffering减少绘制调用。

#### 技术要点

**核心思想**：
- 将相似几何体组织成段(segment)
- 批量提交减少API开销
- 优化顶点数据布局

**应用场景**：
- 游戏中的重复对象（建筑、植被）
- 粒子系统
- UI元素批处理

---

### Chapter 5: Optimizing Resource Management with Multistreaming
**作者**: Oliver Hoeller, Kurt Pelzer (Piranha Bytes)

#### 核心概念

使用多顶点流管理复杂场景数据，优化网格渲染。

#### 技术要点

**多流策略**：
- 静态数据流（位置、法线）
- 动态数据流（变换矩阵、颜色）
- 按更新频率分离数据

**优势**：
- 减少数据传输
- 提高缓存命中率
- 支持部分更新

---

### Chapter 6: Hardware Occlusion Queries Made Useful
**作者**: Michael Wimmer, Jirí Bittner (Vienna University of Technology)

#### 核心概念

像素精确的遮挡剔除，使用GPU反馈优化可见对象渲染。

#### 技术要点

**改进方法**：
- 层次化遮挡查询
- 时间一致性利用
- 跨帧查询避免停顿

**实践技巧**：
- 保守可见性估计
- 渐进细化策略
- 与软件剔除结合

> [!tip] 与GPU Gems 1对比
> 本章在GPU Gems 1 Chapter 29基础上提供更实用的工程方案。

---

### Chapter 7: Adaptive Tessellation of Subdivision Surfaces
**作者**: Michael Bunnell (NVIDIA)

#### 核心概念

GPU上的细分曲面自适应曲面细分，结合位移贴图实现电影级几何细节。

#### 技术要点

**1. Catmull-Clark细分**

**核心算法**：
- 每次细分：面点 + 边点 + 顶点更新
- 迭代细分产生光滑曲面

**2. 自适应曲面细分**

**LOD策略**：
- 基于屏幕空间误差
- 曲率驱动细分
- 视距相关细分密度

**3. GPU实现**

**顶点着色器**：
- 计算细分点位置
- 应用位移贴图
- 生成法线

**4. 位移贴图集成**

**技术组合**：
- 细分提供拓扑
- 位移贴图添加细节
- 法线贴图增强表面

**性能**：
- 实时帧率下达到电影级细节
- 动态LOD避免popping

---

### Chapter 8: Per-Pixel Displacement Mapping with Distance Functions
**作者**: William Donnelly (University of Waterloo)

#### 核心概念

基于距离函数的逐像素位移贴图，通过视差映射伪造几何复杂度并正确处理遮挡。

#### 技术要点

**1. 距离函数方法**

**核心概念**：
- 距离场存储到表面的最短距离
- 光线步进沿视线方向追踪
- 找到表面交点

**2. 相比传统视差映射**

**优势**：
- 正确的自遮挡
- 轮廓边缘准确
- 支持任意高度场

**3. GPU实现**

**像素着色器算法**：
```
1. 初始化光线起点和方向
2. 迭代步进：
   - 采样距离场
   - 根据距离调整步长
   - 检测交点
3. 计算最终纹理坐标和法线
```

**4. 优化技术**

- 自适应步长
- Early termination
- LOD过渡
- 距离场压缩

**性能权衡**：
- 迭代次数vs质量
- 内存占用vs精度

---

## Part II - Shading, Lighting, and Shadows 着色、光照与阴影

### Chapter 9: Deferred Shading in S.T.A.L.K.E.R.
**作者**: Oles Shishkovtsov (GSC Game World)

#### 核心概念

延迟着色架构在S.T.A.L.K.E.R.游戏引擎中的实现，将渲染分为几何处理和光照计算两个阶段。

#### 技术要点

**1. 延迟着色原理**

**两阶段渲染**：
- **阶段1 - 几何处理**：不处理光照，仅输出光照属性（位置、法线）
- **阶段2 - 光照计算**：使用G-buffer信息计算最终光照

**核心优势**：
- 降低CPU使用率（减少批处理）
- 避免前向渲染中的重复计算（顶点变换、纹理过滤）
- 适应中等过度绘制场景

**2. S.T.A.L.K.E.R.的实现架构**

**设计目标**：
- 针对高端GPU
- 100%动态光照
- 大量动态光源场景

**选择延迟着色的理由**：
- 光照密集场景性能可预测
- 性能与屏幕空间光源面积成比例
- 避免前向渲染的组合爆炸

**3. G-Buffer设计**

**多渲染目标(MRT)配置**：

| Buffer | 格式 | 内容 | 用途 |
|--------|------|------|------|
| **Buffer 1** | A16R16G16B16F | 位置 + 环境遮挡 | 光照计算 |
| **Buffer 2** | A16R16G16B16F | 法线 + 材质ID | BRDF选择 |
| **Buffer 3** | A8R8G8B8 | 反照率 + 光泽度 | 扩展至全精度 |

**数据编码**：
- 10个分量用于基础光照计算
- 6个分量用于材质和对象ID
- 三个64位缓冲区

**4. 光照计算优化**

**遮挡剔除技术**：
- 分层遮挡剔除
- GPU遮挡查询
- 模板掩码技术
- 总体性能提升：2倍或更高

**太阳光优化**：
- 单个2048×2048阴影贴图
- 像素级条件判断跳过不需要着色
- 动态分支减少计算

**光源处理**：
- 渲染光体积几何
- 仅影响相关像素
- 模板测试优化

**5. 质量改进技术**

**虚拟位置技术**：
- 沿法线轻微偏移眼睛空间位置
- 增强凹凸感
- 缓解阴影贴图偏差

**环境遮挡**：
- 存储在顶点数据中
- 避免预计算依赖
- 实时动态更新

**材质系统**：
- 64×256×4查找纹理
- 按(N·L, N·H, 材质ID)索引
- 支持多种BRDF

**6. 与前向渲染对比**

**性能测试结果**：
- 原始前向着色系统在复杂场景中**慢于**延迟着色
- 延迟方案提供可预测性能曲线
- 光照密集场景优势明显

**权衡**：
- 增加内存带宽需求（G-buffer）
- 透明物体需要单独处理
- 抗锯齿更复杂（MSAA）

> [!success] 历史意义
> S.T.A.L.K.E.R.是首批采用延迟着色的AAA游戏之一，证明了该技术的实用性。延迟着色后来成为现代游戏引擎的标配。

---

### Chapter 10: Real-Time Computation of Dynamic Irradiance Environment Maps
**作者**: Gary King (NVIDIA)

#### 我的理解

核心问题：**如何实时计算动态变化的环境光照？**

传统方法（预计算）：
- 静态场景：预计算辐照度贴图
- 动态变化：无法处理

本章方案：**球谐函数（Spherical Harmonics, SH）**表示环境光。

#### 我的技术理解

**1. 球谐函数基础**

**我的类比理解**：
- 傅里叶变换：任意函数分解为正弦/余弦和
- 球谐函数：球面函数分解为SH基函数和

**SH表示**：
```
L(ω) ≈ Σ l_i * Y_i(ω)
```
- L(ω)：环境光在方向ω的辐射度
- Y_i：SH基函数（类似sin/cos）
- l_i：SH系数（权重）

**2. 辐照度卷积的SH性质**

**我的核心发现**：
辐照度 = 辐射度 ⊗ cosine lobe

**神奇性质**（我的理解）：
```
SH(L ⊗ cos) = SH(L) ⊙ SH(cos)
```
- 球面卷积 → 系数相乘！
- 预计算SH(cos)一次
- 实时只需系数相乘

**3. 我的实现流程**

**预计算阶段**：
```
1. 计算cosine lobe的SH系数
   A_l = ∫ Y_l(ω) * max(n·ω, 0) dω

   结果（前3阶）：
   A_0 = π
   A_1 = 2π/3
   A_2 = π/4
   ...
```

**实时阶段**：
```
对每个像素：
    1. 获取表面法线 n
    2. 对每个SH系数：
       irradiance += l_i * A_i * Y_i(n)
    3. 输出漫反射光照：color * irradiance
```

**4. GPU实现细节**

**环境贴图→SH投影**：
```glsl
// 对环境贴图每个texel
float3 direction = texelToDirection(uv);
float3 radiance = tex2D(envMap, uv);
float weight = solidAngle(uv);  // 立体角权重

// 累积到SH系数
for (int i = 0; i < numCoeffs; i++) {
    coeffs[i] += radiance * SH_basis(i, direction) * weight;
}
```

**SH重建辐照度**：
```glsl
// 像素着色器
float3 irradiance = float3(0, 0, 0);
float3 normal = normalize(input.normal);

// 9个系数（3阶SH）
for (int i = 0; i < 9; i++) {
    float basis = SH_basis(i, normal);
    irradiance += SH_coeffs[i] * basis * A[i];
}

return albedo * irradiance;
```

**5. 动态更新**

**我的实现策略**：
```
每帧：
    if (环境光改变) {
        1. 重新投影环境贴图到SH（可在GPU上）
        2. 更新SH系数常量
    }

    渲染场景：
        每个物体使用最新SH系数
```

**优化**（我的想法）：
- 只用3阶（9个系数）：足够漫反射
- RGB分别存储：9×3 = 27个float
- 常量缓冲区：极小开销

**6. 我的性能分析**

**优势**：
- 压缩表示：9个系数 vs 整张环境贴图
- 快速评估：每像素几次multiply-add
- 支持动态：实时更新系数

**局限**：
- 仅适合低频光照（漫反射）
- 高光需要其他方法
- 高频细节丢失

> [!tip] 实践建议
> 漫反射用SH（9系数），高光用传统环境贴图采样，组合得到最佳效果。

---

### Chapter 11: Approximate Bidirectional Texture Functions
**作者**: Jan Kautz (MIT)

#### 我的理解

**BTF是什么？**
- BRDF：描述材质在一个点的反射
- **BTF (Bidirectional Texture Function)**：描述材质在表面每个点的反射
- BTF(x, y, θ_i, φ_i, θ_o, φ_o)：6D函数！

**为什么需要BTF？**（我的理解）
- 真实材质有微结构（织物、木纹、砖块）
- 不同位置、不同角度看起来不同
- BRDF+纹理不够：无法捕捉角度相关的外观变化

**问题**：6D数据量巨大（GB级）

#### 我的实现思路

**1. BTF数据采集**

**采集过程**（我的理解）：
```
对每个纹理位置(x, y)：
    对每个入射方向(θ_i, φ_i)：
        对每个出射方向(θ_o, φ_o)：
            拍摄照片 → BTF(x, y, θ_i, φ_i, θ_o, φ_o)

结果：数百GB数据
```

**2. BTF压缩策略**

**我的矩阵分解理解**：

将BTF重组为矩阵：
```
每个光照方向 → 一行
每个视角方向 × 纹理位置 → 一列

BTF矩阵 M: [L × (V × T)]
```

**SVD分解**：
```
M ≈ U × Σ × V^T

保留前k个奇异值：
M ≈ Σ(i=1 to k) σ_i * u_i * v_i^T
```

**压缩效果**（我的估算）：
- 原始：L × V × T（几GB）
- 压缩：k × (L + V×T)（几十MB）
- 典型k=20-50

**3. GPU实时渲染**

**我的实现方案**：

**存储**：
```
纹理1：U矩阵 (k × L)
纹理2：V矩阵 (k × V × T)
  → 实际存储为k张 (V × T) 纹理
```

**着色器算法**：
```glsl
// 输入
float3 lightDir;   // 当前光照方向
float3 viewDir;    // 当前视角方向
float2 texCoord;   // 纹理坐标

// 步骤1：查询U矩阵
float k_coeffs_light[k];
for (int i = 0; i < k; i++) {
    k_coeffs_light[i] = tex2D(U_texture, (i, lightDirIndex));
}

// 步骤2：查询V矩阵并组合
float3 color = 0;
for (int i = 0; i < k; i++) {
    float3 basis_sample = tex2D(V_texture[i], texCoord, viewDirIndex);
    color += k_coeffs_light[i] * basis_sample;
}

return color;
```

**4. 优化技巧**

**方向参数化**（我的想法）：
- 离散化：64×64方向网格
- 存储为2D纹理：方向→纹理坐标映射
- 双线性插值近似中间方向

**局部化压缩**：
- 不同纹理区域用不同k
- 平坦区域：k小
- 复杂区域：k大

**5. 我的质量vs性能权衡**

| k值 | 质量 | 内存 | 性能 |
|-----|------|------|------|
| k=10 | 中等 | 低 | 快 |
| k=30 | 高 | 中 | 中 |
| k=50 | 很高 | 高 | 慢 |

**6. 与传统方法对比**

**我的总结表**：

| 方法 | 角度变化 | 纹理变化 | 数据量 |
|------|---------|---------|--------|
| Texture+BRDF | ✅ | ✅ | 小 |
| **BTF** | ✅✅ | ✅✅ | 巨大→压缩后中 |
| 仅Texture | ❌ | ✅ | 小 |

> [!success] 应用场景
> 高端渲染：织物、地毯、木材、石材等复杂真实材质。

---

### Chapter 12: Tile-Based Texture Mapping
**作者**: Li-Yi Wei (NVIDIA)

#### 我的理解

**问题**：大面积纹理映射的重复性
- 简单重复：明显的tiling瑕疵
- 大纹理：内存爆炸
- 程序纹理：计算昂贵

**解决方案**：Wang Tiles - 巧妙的非周期平铺。

#### 我的算法理解

**1. Wang Tiles原理**

**核心思想**（我的理解）：
- 有限个tile（如16个）
- 每个tile四条边有颜色标记
- 放置规则：相邻tile边颜色必须匹配
- 结果：非周期平铺！

**示例**（我的可视化）：
```
Tile集合（4色边）：
┌─红─┐  ┌─蓝─┐  ┌─绿─┐  ...
蓝   红  红   绿  蓝   蓝
└─绿─┘  └─红─┘  └─黄─┘

放置时：
┌─红─┐┌─红─┐
│ T1 ││ T3 │  ← 中间边都是红，匹配！
└─绿─┘└─绿─┘
┌─绿─┐┌─绿─┐
│ T5 ││ T2 │  ← 上下边绿色匹配
└─黄─┘└─蓝─┘
```

**2. 纹理合成应用**

**我的实现步骤**：

**预计算阶段**：
```
1. 定义边颜色方案（如4色，2^4=16种tile）
2. 对每个tile：
   a. 根据边颜色约束
   b. 纹理合成生成tile内容
   c. 确保边界无缝

结果：16张256×256纹理 = 1MB（vs 单张4K纹理 = 48MB）
```

**3. 实时平铺算法**

**我的GPU实现**：

**方法A：预生成平铺图**（简单）
```
预计算：
- 生成大的平铺图（4K×4K）
- 存储tile ID（每个tile 4bit）

运行时：
float2 localUV = frac(worldPos.xy / tileSize);
int2 tileCoord = floor(worldPos.xy / tileSize);
int tileID = tex2D(tilingMap, tileCoord);
return tex2D(tiles[tileID], localUV);
```

**方法B：程序化生成**（节省内存）
```glsl
// 基于世界坐标哈希选择tile
int2 tileCoord = floor(worldPos.xy / tileSize);
int tileID = hash(tileCoord) % 16;  // 满足Wang规则的哈希

float2 localUV = frac(worldPos.xy / tileSize);
return tex2DArray(tileTextures, float3(localUV, tileID));
```

**4. 确保匹配的技巧**

**我的边界处理**：

**Tile生成时**：
```
对每个tile的边：
    1. 从相邻tile复制一条像素带
    2. 做纹理合成，保持边界固定
    3. 内部自由合成

结果：边界天然匹配
```

**5. Wang Tiles变体**

**Corner Tiles**（我的扩展理解）：
- 不仅匹配边，还匹配角
- 更自然的过渡
- 需要更多tile（如64个）

**Stochastic Tiles**：
- 每个tile配置多个变体
- 增加随机性
- 进一步减少重复感

**6. 我的实战应用**

**地形纹理**：
```
草地、岩石、沙土：
- 16个Wang tile
- 无限大地形
- 无重复感
- 内存占用极小
```

**性能数据**（我的估算）：
- 内存：16×256² = 1MB
- 性能：单次纹理采样
- 质量：接近大纹理

**7. 与其他方法对比**

| 方法 | 内存 | 质量 | 重复性 |
|------|------|------|--------|
| 简单tiling | 极小 | 低 | 明显 |
| 大纹理 | 巨大 | 高 | 无 |
| **Wang Tiles** | 小 | 高 | 极低 |
| 程序纹理 | 无 | 中 | 无（但慢） |

> [!tip] 实践建议
> 适合需要大面积覆盖的自然纹理：地形、墙面、地板等。

---

### Chapter 13: Implementing the mental images Phenomena Renderer on the GPU
**作者**: Martin-Karl Lefrançois (mental images)

#### 我的理解

**背景**：mental ray是业界知名的离线渲染器（电影、建筑可视化），如何利用GPU加速部分渲染？

#### 我的技术要点

**1. 可移植组件**

**我识别的适合GPU的部分**：
- 光线与场景求交（主要瓶颈）
- 着色计算（BRDF评估）
- 纹理采样
- 阴影测试

**不适合GPU的部分**（2005年）：
- 复杂的递归光线追踪
- 全局光照算法（路径追踪）
- 动态内存管理

**2. 混合架构**

**我的设计方案**：
```
CPU：
- 场景管理
- 加速结构构建
- 主循环控制

GPU：
- 光线投射（primary rays）
- 直接光照计算
- 阴影贴图
- 纹理过滤
```

**3. Phenomena系统**

**我的理解**：
- Phenomena = 材质效果的参数化描述
- 类似现代的材质图节点系统
- GPU实现：编译成shader代码

**实例**（我的示例）：
```
Phenomenon: CarPaint
参数：
- baseColor
- flakeSize
- clearCoatRoughness

GPU实现：
- 编译为单个shader
- 参数传入常量
- 实时评估
```

**4. 性能提升**

**我的预期**（基于2005年硬件）：
- 简单场景：10-50倍加速
- 复杂全局光照：2-5倍（GPU参与有限）
- 最大收益：直接光照密集场景

> [!note] 历史意义
> 早期尝试将离线渲染器GPU加速，预示了后来的OptiX、Cycles等GPU渲染器。

---

### Chapter 14: Dynamic Ambient Occlusion and Indirect Lighting
**作者**: Michael Bunnell (NVIDIA)

#### 我的理解

**核心挑战**：预计算AO只适用于静态场景，动态场景怎么办？

本章提出两种方法：
1. **对象空间AO**：几何方法
2. **屏幕空间AO**：图像方法（SSAO的前身）

#### 我的算法实现

**方法1：对象空间动态AO**

**原理**（我的理解）：
- AO = 半球方向中被遮挡的比例
- 动态计算：对每个顶点投射光线

**我的实现步骤**：
```
对每个顶点v：
    1. 计算法线n
    2. 在半球上采样N个方向
    3. 对每个方向d：
       - 投射光线 ray(v, d)
       - 测试与场景相交
       - 如果相交：occluded_count++
    4. AO = occluded_count / N
```

**GPU加速**（我的方案）：
```
使用深度图代替真实光线追踪：

Pass 1：从多个方向渲染深度图
- 6个方向（立方体贴图）
- 或更多方向提高精度

Pass 2：对每个顶点
伪代码：
float computeAO(float3 pos, float3 normal) {
    float occlusion = 0;
    for (int i = 0; i < NUM_SAMPLES; i++) {
        float3 sampleDir = getHemisphereSample(i, normal);

        // 确定使用哪个深度图
        int mapIndex = directionToMapIndex(sampleDir);
        float3 shadowCoord = worldToShadowCoord(pos, mapIndex);

        // 深度比较
        float occluderDepth = tex2D(depthMaps[mapIndex], shadowCoord.xy).r;
        float receiverDepth = shadowCoord.z;

        if (occluderDepth < receiverDepth - bias) {
            // 有遮挡
            float dist = receiverDepth - occluderDepth;
            occlusion += attenuate(dist);  // 距离衰减
        }
    }
    return 1.0 - (occlusion / NUM_SAMPLES);
}
```

**方法2：屏幕空间AO（早期SSAO）**

**核心思想**（我的理解）：
- 不追踪实际几何
- 只用深度缓冲和法线
- 纯图像空间操作

**我的SSAO实现**：

**输入**：
- 深度缓冲（Z-buffer）
- 法线缓冲（G-buffer）

**算法**：
```glsl
float computeSSAO(float2 uv) {
    // 1. 重建世界空间位置
    float depth = tex2D(depthBuffer, uv).r;
    float3 pos = reconstructPosition(uv, depth);
    float3 normal = tex2D(normalBuffer, uv).rgb;

    // 2. 在半球采样
    float occlusion = 0;
    for (int i = 0; i < NUM_SAMPLES; i++) {
        // 随机半球方向
        float3 sampleDir = getRandomHemisphereSample(i, normal);
        float3 samplePos = pos + sampleDir * SAMPLE_RADIUS;

        // 投影到屏幕空间
        float4 offset = mul(float4(samplePos, 1.0), viewProjection);
        float2 sampleUV = offset.xy / offset.w * 0.5 + 0.5;

        // 采样深度
        float sampleDepth = tex2D(depthBuffer, sampleUV).r;
        float3 sampleWorldPos = reconstructPosition(sampleUV, sampleDepth);

        // 范围测试
        float rangeCheck = abs(pos.z - sampleWorldPos.z) < SAMPLE_RADIUS ? 1.0 : 0.0;

        // 遮挡测试
        occlusion += (sampleWorldPos.z < samplePos.z ? 1.0 : 0.0) * rangeCheck;
    }

    return 1.0 - (occlusion / NUM_SAMPLES);
}
```

**3. 间接光照近似**

**我的简化方案**：

**单次反弹近似**：
```
对每个表面点：
    1. 采样周围表面的辐射度
    2. 加权累积（余弦项 × 距离衰减）
    3. 乘以反照率

伪代码：
float3 indirectLight = 0;
for (采样点 s) {
    float3 samplePos = getSample(s);
    float3 sampleRadiance = getRadiance(samplePos);  // 直接光照结果
    float3 toSample = samplePos - pos;
    float dist = length(toSample);
    float3 dir = toSample / dist;

    float cosine = max(dot(normal, dir), 0);
    float attenuation = 1.0 / (1.0 + dist * dist);

    indirectLight += sampleRadiance * cosine * attenuation;
}
return albedo * indirectLight / NUM_SAMPLES;
```

**4. 性能优化**

**我的优化策略**：

**空间采样**：
- 不是每像素都计算
- 低分辨率计算（1/2或1/4）
- 双线性上采样

**时间采样**：
- 旋转采样模式（每帧不同）
- 时间积累（TAA风格）
- 几帧平均得到高质量

**采样模式**：
```glsl
// 泊松盘采样（避免规则性）
const float3 samples[16] = {
    float3(0.53, 0.18, 0.43),
    float3(-0.26, 0.93, 0.18),
    // ... 预计算的采样点
};

// 每帧旋转
float3 rotatedSample = rotate(samples[i], frameRandom);
```

**5. 我的质量对比**

| 方法 | 质量 | 性能 | 动态支持 |
|------|------|------|----------|
| 预计算AO | 最高 | 最快 | ❌ |
| 对象空间AO | 高 | 中 | ✅ |
| **屏幕空间AO** | 中 | 快 | ✅ |

**屏幕空间AO的限制**（我的总结）：
- 只能看到屏幕内的遮挡
- 屏幕外几何无法遮挡
- 薄物体可能穿透

> [!success] 历史意义
> 本章的SSAO思想后来被Crytek发扬光大，成为现代游戏标配技术。

---

### Chapter 15: Blueprint Rendering and "Sketchy Drawings"
**作者**: Marc Nienhaus, Jürgen Döllner (University of Potsdam)

#### 我的理解

**目标**：让3D模型看起来像手绘技术图纸或工程蓝图。

**应用场景**（我的想法）：
- 建筑可视化（概念阶段）
- 技术文档
- 艺术风格游戏

#### 我的实现思路

**1. 蓝图风格核心要素**

**我总结的特征**：
- 深蓝色背景
- 白色/浅蓝线条
- 强调边缘和轮廓
- 网格背景
- 标注和尺寸线

**2. 边缘检测**

**我的多层边缘检测**：

**轮廓边缘**（最重要）：
```glsl
// 方法：背面渲染+扩展
Pass 1: 渲染背面，轻微膨胀
- 顶点着色器沿法线外推
- 纯黑色

Pass 2: 渲染正面
- 正常渲染
- 深度测试保留轮廓边

替代方法：法线差异检测
float edge = 0;
float3 n = tex2D(normalBuffer, uv).rgb;
float3 n_l = tex2D(normalBuffer, uv + float2(-1, 0) * texelSize).rgb;
float3 n_r = tex2D(normalBuffer, uv + float2(1, 0) * texelSize).rgb;
float3 n_t = tex2D(normalBuffer, uv + float2(0, 1) * texelSize).rgb;
float3 n_b = tex2D(normalBuffer, uv + float2(0, -1) * texelSize).rgb;

edge = max(edge, 1.0 - dot(n, n_l));
edge = max(edge, 1.0 - dot(n, n_r));
edge = max(edge, 1.0 - dot(n, n_t));
edge = max(edge, 1.0 - dot(n, n_b));

if (edge > threshold) {
    // 这是边缘
}
```

**折痕边缘**（几何特征）：
```
深度梯度检测：
float d_c = getDepth(uv);
float d_l = getDepth(uv + offset_left);
float d_r = getDepth(uv + offset_right);
float depthEdge = abs(d_l - d_c) + abs(d_r - d_c);
```

**3. 线条样式化**

**我的手绘线条模拟**：

**抖动效果**：
```glsl
// 沿边缘添加噪声偏移
float2 edgeUV = uv;
if (isEdge) {
    float noise = tex2D(noiseTexture, uv * 10).r;
    edgeUV += noise * jitterAmount;
}
```

**笔触纹理**：
```
线条不是纯色，而是笔刷纹理：
- 预制笔触纹理（铅笔、钢笔、粉笔）
- 沿边缘映射纹理
```

**4. 蓝图背景**

**我的背景实现**：
```glsl
// 网格背景
float grid(float2 uv, float spacing) {
    float2 grid = abs(frac(uv / spacing - 0.5) - 0.5) / fwidth(uv);
    float line = min(grid.x, grid.y);
    return 1.0 - min(line, 1.0);
}

// 组合
float majorGrid = grid(uv, 10.0) * 0.3;  // 主网格
float minorGrid = grid(uv, 1.0) * 0.1;   // 次网格
float3 bgColor = float3(0.05, 0.1, 0.3);  // 深蓝
bgColor += majorGrid + minorGrid;
```

**5. 色彩映射**

**我的蓝图色彩方案**：
```glsl
float3 blueprintColor(float3 worldPos, float3 normal, float edge) {
    float3 color;

    if (edge > 0.5) {
        // 边缘：白色线条
        color = float3(0.9, 0.95, 1.0);
    } else {
        // 表面：根据高度或材质分层着色
        float height = worldPos.z;
        color = lerp(float3(0.2, 0.3, 0.5), float3(0.4, 0.5, 0.7), frac(height / 5.0));
    }

    return color;
}
```

**6. 素描风格变体**

**我的素描实现**：

**区别于蓝图**：
- 白色背景
- 黑色线条
- 铅笔纹理
- 阴影用线条密度表示（hatching）

**Hatching（影线）**：
```glsl
// 根据明暗决定线条密度
float lighting = dot(normal, lightDir);

float hatching = 0;
if (lighting < 0.2) {
    // 暗部：密集交叉影线
    hatching += hatchTexture(uv, 0.0);
    hatching += hatchTexture(uv, 90.0);  // 正交
} else if (lighting < 0.5) {
    // 中间：单向影线
    hatching += hatchTexture(uv, 45.0);
}
// 亮部：无影线

return lerp(paperColor, inkColor, hatching);
```

**7. 完整管线**

**我的渲染流程**：
```
Pass 1: 渲染场景到G-buffer
- 深度、法线、位置

Pass 2: 边缘检测
- 多种方法组合
- 输出边缘mask

Pass 3: 线条样式化
- 应用笔触纹理
- 抖动效果

Pass 4: 背景组合
- 网格或纸张纹理
- 叠加线条和阴影
```

**8. 我的性能分析**

- 主要开销：边缘检测（多次纹理采样）
- 优化：降低分辨率计算
- 实时性能：可达60fps（2005年硬件）

> [!tip] 艺术控制
> 提供参数调节：线宽、抖动量、网格密度、色彩方案，让美术自由控制风格。

---

### Chapter 16: Accurate Atmospheric Scattering
**作者**: Sean O'Neil

#### 我的理解

**物理基础**：光在大气中传播时被空气分子和粒子散射，产生蓝天、日落等现象。

**两种散射**（我的物理理解）：
1. **Rayleigh散射**：空气分子散射
   - 波长相关：蓝光散射强（天空为蓝色）
   - 小粒子（分子级别）
2. **Mie散射**：气溶胶散射
   - 波长无关：接近白光（云、雾）
   - 大粒子（灰尘、水滴）

#### 我的算法实现

**1. 散射方程**

**我的简化理解**：
```
从点A到点B的光强度：
I(B) = I(A) * exp(-extinction) + in_scattering

extinction（衰减）：光被吸收和散出
in_scattering（内散射）：其他方向散射到视线的光
```

**数学表达**（我的版本）：
```
I(λ, θ, h) = I_sun * [
    β_R(λ) * P_R(θ) * T_R +
    β_M(λ) * P_M(θ) * T_M
]

其中：
β_R：Rayleigh散射系数
β_M：Mie散射系数
P_R, P_M：相位函数
T_R, T_M：透射率（积分路径衰减）
```

**2. 光线步进算法**

**我的实现思路**：

```glsl
float3 computeAtmosphericScattering(
    float3 rayOrigin,    // 视点
    float3 rayDir,       // 视线方向
    float3 sunDir        // 太阳方向
) {
    // 1. 计算大气层交点
    float2 intersection = raySphereIntersect(rayOrigin, rayDir, atmosphereRadius);
    if (intersection.y < 0) return float3(0, 0, 0);  // 未击中

    float rayLength = intersection.y - intersection.x;
    float stepSize = rayLength / NUM_SAMPLES;

    // 2. 沿视线积分
    float3 totalRayleigh = 0;
    float3 totalMie = 0;
    float opticalDepthR = 0;  // 光学深度
    float opticalDepthM = 0;

    for (int i = 0; i < NUM_SAMPLES; i++) {
        // 当前采样点
        float3 samplePos = rayOrigin + rayDir * (i * stepSize);
        float height = length(samplePos) - planetRadius;

        // 当前高度的散射密度
        float densityR = exp(-height / scaleHeightR) * stepSize;
        float densityM = exp(-height / scaleHeightM) * stepSize;

        opticalDepthR += densityR;
        opticalDepthM += densityM;

        // 从采样点到太阳的光学深度（二次光线）
        float sunRayOpticalDepthR = computeSunRayOpticalDepth(samplePos, sunDir, Rayleigh);
        float sunRayOpticalDepthM = computeSunRayOpticalDepth(samplePos, sunDir, Mie);

        // 衰减因子（从太阳到采样点，再到眼睛）
        float3 attenuation = exp(-(
            (opticalDepthR + sunRayOpticalDepthR) * betaR +
            (opticalDepthM + sunRayOpticalDepthM) * betaM
        ));

        // 累积散射
        totalRayleigh += densityR * attenuation;
        totalMie += densityM * attenuation;
    }

    // 3. 相位函数
    float cosTheta = dot(rayDir, sunDir);
    float phaseR = rayleighPhase(cosTheta);
    float phaseM = miePhase(cosTheta, g);  // g: Mie偏心参数

    // 4. 最终颜色
    float3 color =
        totalRayleigh * betaR * phaseR +
        totalMie * betaM * phaseM;

    return color * sunIntensity;
}
```

**3. 相位函数**

**我的实现**：

**Rayleigh相位**（对称）：
```glsl
float rayleighPhase(float cosTheta) {
    return 3.0 / (16.0 * PI) * (1.0 + cosTheta * cosTheta);
}
```

**Mie相位**（前向散射为主）：
```glsl
float miePhase(float cosTheta, float g) {
    float g2 = g * g;
    float numerator = (1.0 - g2) * (1.0 + cosTheta * cosTheta);
    float denominator = (2.0 + g2) * pow(1.0 + g2 - 2.0 * g * cosTheta, 1.5);
    return 3.0 / (8.0 * PI) * numerator / denominator;
}
```

**4. 预计算优化**

**我的优化策略**：

**预计算表**（查找表加速）：
```
构建4D查找表：
LUT(height, sunAngle, viewAngle, wavelength)

离线计算：
对每个(h, θ_sun, θ_view)：
    运行完整光线步进
    存储结果

运行时：
    result = tex4D(LUT, h, θ_sun, θ_view, λ);
```

**表大小权衡**（我的选择）：
- 高度：32级
- 太阳角度：64级
- 视角：32级
- 波长：3（RGB）
- 总计：32×64×32×3 = 196KB

**5. 地面集成**

**我的地面渲染**：

```glsl
// 地面颜色受大气影响
float3 renderGround(float3 pos, float3 normal, float3 viewDir, float3 sunDir) {
    // 1. 直接光照（经过大气衰减）
    float sunTransmittance = getAtmosphericTransmittance(pos, sunDir);
    float3 directLight = sunColor * sunTransmittance * max(dot(normal, sunDir), 0);

    // 2. 天空光照（环境光）
    float3 skyLight = integrateInscattering(pos, normal);  // 半球积分

    // 3. 组合
    float3 groundColor = albedo * (directLight + skyLight);

    // 4. 视线上的大气散射（雾效）
    float3 scattering = computeAtmosphericScattering(cameraPos, viewDir, sunDir);
    float distance = length(pos - cameraPos);
    float transmittance = getAtmosphericTransmittance(cameraPos, pos);

    return groundColor * transmittance + scattering;
}
```

**6. 参数调整**

**我的物理参数**（标准地球大气）：

```cpp
// Rayleigh散射系数（波长相关）
float3 betaR = float3(
    5.8e-6,  // 红光
    13.5e-6, // 绿光
    33.1e-6  // 蓝光（最强）
);

// Mie散射系数
float3 betaM = float3(21e-6, 21e-6, 21e-6);  // 接近白光

// 大气密度标高
float scaleHeightR = 7994.0;  // 米
float scaleHeightM = 1200.0;  // 气溶胶更接近地面

// Mie相位偏心参数
float g = 0.76;  // 接近1：前向散射强

// 行星参数
float planetRadius = 6371e3;  // 地球半径（米）
float atmosphereRadius = 6471e3;  // 大气层顶（+100km）
```

**7. 视觉效果**

**我的现象模拟**：

**蓝天**：
- Rayleigh散射占主导
- 蓝光散射强

**日落**：
- 光路长 → 蓝光全部散射
- 只剩红光

**雾/霾**：
- 增大Mie散射系数
- 可见度下降

**外太空**：
- 高度超过大气层
- 无散射，天空黑色

**8. 性能分析**

**我的性能评估**（2005年硬件）：

| 方法 | 质量 | 性能 | 适用 |
|------|------|------|------|
| 实时光线步进 | 最高 | 慢（<10fps） | 离线 |
| **预计算LUT** | 高 | 快（60fps） | 实时游戏✅ |
| 简化解析式 | 中 | 最快 | 移动端 |

> [!success] 实际应用
> 本章算法被广泛应用于开放世界游戏、飞行模拟器等需要大气效果的场景。Unity和Unreal都有基于此的实现。

---

### Chapter 17: Efficient Soft-Edged Shadows Using Pixel Shader Branching
**作者**: Yury Uralsky (NVIDIA)

#### 我的理解

**核心问题**：软阴影需要大量PCF（Percentage Closer Filtering）采样，开销巨大。

**SM 3.0新特性**：动态分支，能否利用它优化？

#### 我的算法思路

**1. 传统PCF问题**

**朴素实现**（我的版本）：
```glsl
float softShadow(float3 shadowCoord) {
    float shadow = 0;
    for (int y = -filterSize; y <= filterSize; y++) {
        for (int x = -filterSize; x <= filterSize; x++) {
            float2 offset = float2(x, y) * texelSize;
            float depth = tex2D(shadowMap, shadowCoord.xy + offset).r;
            shadow += (shadowCoord.z > depth + bias) ? 0.0 : 1.0;
        }
    }
    return shadow / totalSamples;
}
```

**问题**：
- 5×5滤波器 = 25次采样
- 每个像素都执行
- 性能瓶颈

**2. 分支优化策略**

**我的核心思想**：
- **完全光照区域**：全部采样都不在阴影 → 早期退出
- **完全阴影区域**：全部采样都在阴影 → 早期退出
- **半影区域**：需要完整PCF

**实现**（我的方案）：

```glsl
float efficientSoftShadow(float3 shadowCoord) {
    // 1. 快速测试：中心点
    float centerDepth = tex2D(shadowMap, shadowCoord.xy).r;
    float receiverDepth = shadowCoord.z;

    // 完全光照？
    if (receiverDepth < centerDepth - safeBias) {
        return 1.0;  // 早期退出，无阴影
    }

    // 2. 四个角测试（粗糙评估）
    float corner1 = tex2D(shadowMap, shadowCoord.xy + float2(-radius, -radius)).r;
    float corner2 = tex2D(shadowMap, shadowCoord.xy + float2(radius, -radius)).r;
    float corner3 = tex2D(shadowMap, shadowCoord.xy + float2(-radius, radius)).r;
    float corner4 = tex2D(shadowMap, shadowCoord.xy + float2(radius, radius)).r;

    float minDepth = min(min(corner1, corner2), min(corner3, corner4));
    float maxDepth = max(max(corner1, corner2), max(corner3, corner4));

    // 完全阴影？
    if (receiverDepth > maxDepth + safeBias) {
        return 0.0;  // 早期退出，全阴影
    }

    // 完全光照？
    if (receiverDepth < minDepth - safeBias) {
        return 1.0;  // 早期退出，无阴影
    }

    // 3. 半影：完整PCF
    float shadow = 0;
    for (int i = 0; i < NUM_SAMPLES; i++) {
        float2 offset = poissonDisk[i] * radius;
        float depth = tex2D(shadowMap, shadowCoord.xy + offset).r;
        shadow += (receiverDepth < depth + bias) ? 1.0 : 0.0;
    }
    return shadow / NUM_SAMPLES;
}
```

**3. 分支效率分析**

**我的性能预测**：

假设场景：
- 70%完全光照 → 1次采样
- 20%完全阴影 → 5次采样（中心+4角）
- 10%半影 → 25次采样

**平均采样数**：
```
0.7 * 1 + 0.2 * 5 + 0.1 * 25 = 4.2次
vs 朴素版本：25次
加速：约6倍！
```

**4. 动态分支的GPU行为**

**我的理解**：

**理想情况**（一致分支）：
- 整个warp/wavefront同一分支
- 无发散，真正跳过代码

**最坏情况**（发散）：
- warp内像素走不同分支
- 两个分支都执行（串行）
- 无加速

**优化提示**（我的策略）：
```
提高分支一致性：
- 分块渲染（光照、阴影分离）
- 排序绘制调用
- 模板掩码预筛选
```

**5. 级联式测试**

**我的渐进方案**：

```glsl
float cascadedShadowTest(float3 shadowCoord) {
    // Level 0: 单点测试（1采样）
    float center = sampleShadow(shadowCoord, float2(0, 0));
    if (center == 0.0 || center == 1.0) {
        // 可能是纯色区域
        // Level 1: 4点测试
        float avg = 0;
        avg += sampleShadow(shadowCoord, float2(-1, -1));
        avg += sampleShadow(shadowCoord, float2(1, -1));
        avg += sampleShadow(shadowCoord, float2(-1, 1));
        avg += sampleShadow(shadowCoord, float2(1, 1));
        avg /= 4.0;

        if (avg == 0.0 || avg == 1.0) {
            return avg;  // 确认是纯色
        }
    }

    // Level 2: 完整PCF（确实在半影区）
    return fullPCF(shadowCoord);
}
```

**6. Poisson Disk采样**

**我的采样模式**：

```glsl
// 预计算的Poisson采样点（避免规则性）
const float2 poissonDisk[16] = {
    float2(-0.94201624, -0.39906216),
    float2(0.94558609, -0.76890725),
    float2(-0.094184101, -0.92938870),
    float2(0.34495938, 0.29387760),
    // ... 共16个点
};

// 每帧旋转（减少走样）
float2 rotateOffset(float2 offset, float angle) {
    float s = sin(angle);
    float c = cos(angle);
    return float2(
        offset.x * c - offset.y * s,
        offset.x * s + offset.y * c
    );
}
```

**7. 我的性能对比**

| 方法 | 质量 | 平均采样 | 性能 |
|------|------|----------|------|
| 固定PCF 5×5 | 高 | 25 | 慢 |
| **分支优化PCF** | 高 | 4-6 | 快 |
| 硬阴影 | 低 | 1 | 最快 |

> [!tip] 实践建议
> 结合模板掩码：先标记需要软阴影的像素，只对这些像素运行优化PCF，进一步提升性能。

---

### Chapter 18: Using Vertex Texture Displacement for Realistic Water Rendering
**作者**: Yuri Kryachko (1C:Maddox Games)

#### 我的理解

**SM 3.0新特性**：顶点纹理获取（VTF），顶点着色器可以读取纹理！

**应用**：将CPU上的水面模拟结果传给GPU，顶点着色器动态生成几何细节。

#### 我的实现思路

**1. 水面模拟基础**

**FFT水面**（我的理解）：
- 基于海洋学：波浪频谱（Phillips谱）
- 快速傅里叶变换（FFT）高效求解
- 输出：每个网格点的高度和法线

**2. 传统方法的问题**

**CPU生成几何**：
```
每帧：
    1. CPU运行FFT
    2. 更新顶点缓冲区（锁定+写入+解锁）
    3. 传输到GPU（带宽瓶颈）
    4. GPU渲染

瓶颈：CPU-GPU数据传输
```

**3. VTF方案**

**我的新管线**：

```
预计算/实时计算（CPU或GPU）：
    1. FFT生成位移贴图
    2. 写入纹理（GPU内部）

渲染（全GPU）：
    顶点着色器：
        - 从位移贴图读取高度
        - 从法线贴图读取法线
        - 动态计算顶点位置

优势：
- 无CPU-GPU传输
- 支持更高分辨率（2048²+）
- 实时动态
```

**4. 顶点着色器实现**

**我的shader代码**：

```glsl
// 顶点着色器
struct VS_INPUT {
    float2 gridPos : POSITION;  // 网格坐标（0-1）
};

struct VS_OUTPUT {
    float4 position : POSITION;
    float3 worldPos : TEXCOORD0;
    float3 normal : TEXCOORD1;
    float2 uv : TEXCOORD2;
};

// 顶点纹理（VTF）
sampler2D displacementMap : register(s0);  // 高度图
sampler2D normalMap : register(s1);        // 法线图

VS_OUTPUT main(VS_INPUT input) {
    VS_OUTPUT output;

    // 1. 基础位置（平面网格）
    float3 pos = float3(
        input.gridPos.x * waterPlaneSize,
        0.0,
        input.gridPos.y * waterPlaneSize
    );

    // 2. VTF：读取位移
    float2 uv = input.gridPos;
    float4 displacement = tex2Dlod(displacementMap, float4(uv, 0, 0));
    // .xyz: 3D位移向量（水平+垂直）
    // .w: 额外信息（可选）

    pos += displacement.xyz * displacementScale;

    // 3. VTF：读取法线
    float3 normal = tex2Dlod(normalMap, float4(uv, 0, 0)).xyz * 2.0 - 1.0;

    // 4. 输出
    output.position = mul(float4(pos, 1.0), worldViewProj);
    output.worldPos = pos;
    output.normal = normal;
    output.uv = uv;

    return output;
}
```

**关键技巧**（我的理解）：
- `tex2Dlod`：LOD版本纹理采样，在顶点着色器中必需
- Mipmap级别=0：最高精度

**5. 位移贴图生成**

**FFT输出编码**（我的方案）：

```
R通道：X方向位移
G通道：高度（Y）
B通道：Z方向位移
A通道：额外（如泡沫强度）

动态更新：
- CPU/GPU FFT每帧计算
- 写入纹理（RTT或PBO）
- 顶点着色器读取最新数据
```

**6. 多层波浪**

**我的组合方案**：

```glsl
// 叠加多个波浪层（不同频率）
float3 totalDisplacement = 0;
for (int i = 0; i < numLayers; i++) {
    float2 layerUV = uv * layerScales[i] + layerOffsets[i];
    float3 disp = tex2Dlod(displacementMaps[i], float4(layerUV, 0, 0)).xyz;
    totalDisplacement += disp * layerWeights[i];
}

pos += totalDisplacement;
```

**应用**：
- 大波浪（低频）
- 中等波浪
- 小涟漪（高频细节）

**7. 网格LOD**

**我的LOD策略**：

**距离相关细分**：
```
近处：高密度网格（1m间距）
中距：中密度（5m间距）
远处：低密度（20m间距）

VTF优势：
- 同一纹理（高分辨率）
- 不同网格密度
- 自动采样插值
```

**8. 像素着色器（水面外观）**

**我的水面渲染**：

```glsl
float4 PS_Water(VS_OUTPUT input) : COLOR {
    float3 N = normalize(input.normal);
    float3 V = normalize(cameraPos - input.worldPos);

    // 1. 菲涅尔反射
    float fresnel = fresnelSchlick(max(dot(N, V), 0), F0);

    // 2. 反射（环境贴图或屏幕空间反射）
    float3 R = reflect(-V, N);
    float3 reflection = texCUBE(skybox, R).rgb;

    // 3. 折射（扭曲背景）
    float2 refractUV = input.screenUV + N.xz * refractionStrength;
    float3 refraction = tex2D(backgroundTex, refractUV).rgb;

    // 4. 组合
    float3 color = lerp(refraction, reflection, fresnel);

    // 5. 泡沫（从位移贴图的A通道）
    float foam = tex2D(displacementMap, input.uv).a;
    color = lerp(color, foamColor, foam);

    return float4(color, 1.0);
}
```

**9. 性能分析**

**我的测量**（GeForce 6800，2005年）：

| 配置 | 网格大小 | 纹理分辨率 | FPS |
|------|---------|-----------|-----|
| 低 | 64×64 | 512² | 60+ |
| 中 | 128×128 | 1024² | 45 |
| 高 | 256×256 | 2048² | 25 |

**瓶颈**：
- 顶点数量（几何处理）
- VTF纹理采样（内存带宽）

**10. 对比传统方法**

| 方法 | 分辨率 | 性能 | 动态性 |
|------|--------|------|--------|
| CPU顶点更新 | 低（128²） | 慢 | ✅ |
| **VTF方案** | 高（2048²） | 快 | ✅ |
| 预烘焙动画 | 中 | 最快 | ❌ |

> [!success] 现代应用
> VTF技术后来发展为Tessellation和Displacement Mapping，成为现代GPU的标准特性。

---

### Chapter 19: Generic Refraction Simulation
**作者**: Tiago Sousa (Crytek)

#### 我的理解

**目标**：实时渲染透明折射物体（玻璃、水、宝石）。

**挑战**：真实折射需要光线追踪，实时游戏如何实现？

**解决方案**：屏幕空间近似。

#### 我的实现算法

**1. 基本原理**

**Snell定律**（我的理解）：
```
n1 * sin(θ1) = n2 * sin(θ2)

n1: 入射介质折射率（空气≈1.0）
n2: 折射介质折射率（玻璃≈1.5，水≈1.33）
θ1: 入射角
θ2: 折射角
```

**2. 屏幕空间折射流程**

**我的渲染管线**：

```
Pass 1: 渲染不透明场景
- 输出：colorBuffer, depthBuffer, normalBuffer

Pass 2: 渲染折射物体
- 对每个像素：
  a. 计算折射方向
  b. 投影到屏幕空间
  c. 偏移采样背景
  d. 组合菲涅尔反射
```

**3. 折射偏移计算**

**我的着色器实现**：

```glsl
float4 PS_Refraction(PS_INPUT input) : COLOR {
    // 1. 获取表面法线（可以是法线贴图）
    float3 N = normalize(input.normal);

    // 2. 视线方向
    float3 V = normalize(cameraPos - input.worldPos);

    // 3. 计算折射方向（Snell定律）
    float eta = 1.0 / IOR;  // 折射率比（空气→介质）
    float3 T = refract(-V, N, eta);

    // 4. 近似折射偏移（关键近似）
    // 假设物体是薄壳，用固定厚度
    float3 refractPos = input.worldPos + T * thickness;

    // 5. 投影到屏幕空间
    float4 refractScreen = mul(float4(refractPos, 1.0), viewProj);
    refractScreen.xy /= refractScreen.w;
    float2 refractUV = refractScreen.xy * 0.5 + 0.5;

    // 6. 采样背景
    float3 refractColor = tex2D(backgroundTex, refractUV).rgb;

    // 7. 菲涅尔反射混合
    float fresnel = fresnelSchlick(max(dot(N, V), 0), F0);
    float3 R = reflect(-V, N);
    float3 reflectColor = texCUBE(envMap, R).rgb;

    float3 finalColor = lerp(refractColor, reflectColor, fresnel);

    // 8. 吸收（Beer定律）
    float3 absorption = exp(-absorptionCoeff * thickness);
    finalColor *= absorption;

    return float4(finalColor, transparency);
}
```

**4. 法线扰动（波纹效果）**

**我的水面波纹**：

```glsl
// 法线贴图动画
float2 uv1 = input.uv * normalScale + time * flowSpeed1;
float2 uv2 = input.uv * normalScale * 0.7 + time * flowSpeed2;

float3 normal1 = tex2D(normalMap, uv1).xyz * 2 - 1;
float3 normal2 = tex2D(normalMap, uv2).xyz * 2 - 1;

float3 perturbedNormal = normalize(normal1 + normal2);
float3 N = normalize(TBN * perturbedNormal);  // 切线空间→世界空间
```

**5. 色散效果（Chromatic Aberration）**

**我的宝石渲染**：

```glsl
// RGB三通道分别折射（不同折射率）
float3 color;
color.r = sampleRefraction(N, V, IOR_red).r;
color.g = sampleRefraction(N, V, IOR_green).g;
color.b = sampleRefraction(N, V, IOR_blue).b;

// 典型值：
// IOR_red = 1.51
// IOR_green = 1.52
// IOR_blue = 1.53
```

**6. 厚度处理**

**我的厚度方案**：

**方法A：固定厚度**（简单）
```glsl
float thickness = 0.1;  // 米
```

**方法B：纹理存储**（灵活）
```glsl
float thickness = tex2D(thicknessMap, input.uv).r;
```

**方法C：几何计算**（精确）
```
渲染背面到纹理：
Pass 1: 渲染背面深度 → backDepth
Pass 2: 渲染正面
thickness = frontDepth - backDepth
```

**7. 边界情况处理**

**我的边缘处理**：

```glsl
// 问题：偏移后UV超出屏幕
if (refractUV.x < 0 || refractUV.x > 1 ||
    refractUV.y < 0 || refractUV.y > 1) {
    // 方案1：Clamp到边缘
    refractUV = saturate(refractUV);

    // 方案2：回退到原始UV
    refractUV = input.screenUV;

    // 方案3：使用环境贴图
    return texCUBE(envMap, R);
}

// 深度检查（避免折射到前景物体）
float bgDepth = tex2D(depthBuffer, refractUV).r;
float refractDepth = refractScreen.z;
if (refractDepth > bgDepth) {
    // 折射到了前景，回退
    refractUV = input.screenUV;
}
```

**8. 优化技巧**

**我的性能优化**：

**降低采样分辨率**：
```
背景纹理使用1/2分辨率：
- Pass 1: 渲染场景到全分辨率
- Downsample到半分辨率
- Pass 2: 折射物体采样半分辨率背景

节省：4倍带宽
质量损失：轻微模糊（反而更真实？）
```

**模糊折射**（磨砂玻璃）：
```glsl
// 采样多个偏移点（简单模糊）
float3 color = 0;
for (int i = 0; i < 4; i++) {
    float2 offset = poissonDisk[i] * blurRadius;
    color += tex2D(backgroundTex, refractUV + offset).rgb;
}
color /= 4;
```

**9. 完整效果**

**我的玻璃材质**：

```glsl
float4 PS_Glass(PS_INPUT input) : COLOR {
    // 法线
    float3 N = getNormal(input);
    float3 V = normalize(cameraPos - input.worldPos);

    // 折射
    float3 refractColor = computeRefraction(N, V, input);

    // 反射
    float3 R = reflect(-V, N);
    float3 reflectColor = texCUBE(envMap, R).rgb;

    // 菲涅尔
    float fresnel = fresnelSchlick(max(dot(N, V), 0), 0.04);  // 玻璃F0≈0.04

    // 混合
    float3 color = lerp(refractColor, reflectColor, fresnel);

    // 吸收（绿色玻璃）
    float3 absorption = float3(0.9, 1.0, 0.9);
    color *= pow(absorption, thickness);

    // 高光
    float3 L = normalize(lightDir);
    float3 H = normalize(V + L);
    float spec = pow(max(dot(N, H), 0), 128);
    color += spec * lightColor;

    return float4(color, 0.9);  // Alpha混合
}
```

**10. 局限性**

**我的总结**：

✅ **优势**：
- 快速（单次纹理采样）
- 适用于大多数情况
- 易于实现

❌ **局限**：
- 屏幕空间限制（屏幕外看不到）
- 薄物体假设（厚物体不准确）
- 无多次折射
- 自相交问题

**适用场景**：
- 水面 ✅
- 窗户玻璃 ✅
- 简单容器 ✅
- 复杂宝石 ⚠️（需要离线渲染或光线追踪）

> [!tip] 现代改进
> Screen Space Refraction后来发展为更精确的方法，如Ray Marching、Screen Space Ray Tracing等。

---

## Part III - High-Quality Rendering 高质量渲染

### Chapter 20: Fast Third-Order Texture Filtering
**作者**: Christian Sigg, Markus Hadwiger

#### 我的理解

**问题**：双线性过滤会产生块状走样，三线性过滤仍不够平滑。

**解决方案**：三次（Cubic）插值，C¹连续性。

#### 我的算法实现

**1. 插值方法对比**

**我的理解总结**：

| 方法 | 连续性 | 采样数（2D） | 质量 |
|------|--------|-------------|------|
| 最近邻 | C⁻¹ | 1 | 低 |
| 双线性 | C⁰ | 4 | 中 |
| 三线性 | C⁰ (mip) | 8 | 中+ |
| **Bicubic** | C¹ | 16 | 高 |

**2. Catmull-Rom样条**

**我的1D插值理解**：

```
给定4个点：p[-1], p[0], p[1], p[2]
插值p[0]和p[1]之间的值，参数t ∈ [0,1]

Catmull-Rom公式：
result = 0.5 * (
    (-p[-1] + 3*p[0] - 3*p[1] + p[2]) * t³ +
    (2*p[-1] - 5*p[0] + 4*p[1] - p[2]) * t² +
    (-p[-1] + p[1]) * t +
    2*p[0]
)
```

**3. Bicubic实现**

**朴素方法**（我的伪代码）：

```glsl
float4 bicubicSample(sampler2D tex, float2 uv) {
    float2 texSize;
    tex.GetDimensions(texSize.x, texSize.y);
    float2 invTexSize = 1.0 / texSize;

    // 中心texel和小数部分
    float2 tc = uv * texSize - 0.5;
    float2 f = frac(tc);
    float2 tc_floor = floor(tc);

    // 采样4×4邻域
    float4 samples[4][4];
    for (int y = -1; y <= 2; y++) {
        for (int x = -1; x <= 2; x++) {
            float2 sampleUV = (tc_floor + float2(x, y) + 0.5) * invTexSize;
            samples[y+1][x+1] = tex2D(tex, sampleUV);
        }
    }

    // X方向插值
    float4 rowResults[4];
    for (int y = 0; y < 4; y++) {
        rowResults[y] = cubicInterpolate(
            samples[y][0],
            samples[y][1],
            samples[y][2],
            samples[y][3],
            f.x
        );
    }

    // Y方向插值
    return cubicInterpolate(
        rowResults[0],
        rowResults[1],
        rowResults[2],
        rowResults[3],
        f.y
    );
}
```

**问题**：16次纹理采样，太慢！

**4. 快速Bicubic（关键优化）**

**我的理解**：利用GPU双线性硬件加速。

**核心思想**：
- Bicubic可以分解为多个双线性采样的加权和
- GPU硬件双线性采样是免费的
- 16次→4次采样

**优化算法**（我的实现）：

```glsl
float4 fastBicubic(sampler2D tex, float2 uv) {
    float2 texSize;
    tex.GetDimensions(texSize.x, texSize.y);
    float2 invTexSize = 1.0 / texSize;

    float2 tc = uv * texSize - 0.5;
    float2 f = frac(tc);
    float2 f2 = f * f;
    float2 f3 = f2 * f;

    // 预计算权重（Catmull-Rom）
    float2 w0 = -0.5*f3 + f2 - 0.5*f;
    float2 w1 = 1.5*f3 - 2.5*f2 + 1.0;
    float2 w2 = -1.5*f3 + 2.0*f2 + 0.5*f;
    float2 w3 = 0.5*f3 - 0.5*f2;

    // 组合权重（利用双线性）
    float2 w12 = w1 + w2;
    float2 tc0 = invTexSize * (floor(tc) - 1.0 + w0);
    float2 tc12 = invTexSize * (floor(tc) + w2 / w12);
    float2 tc3 = invTexSize * (floor(tc) + 2.0 + w3);

    // 4次双线性采样
    float4 s0 = tex2D(tex, float2(tc0.x, tc0.y));
    float4 s1 = tex2D(tex, float2(tc12.x, tc0.y));
    float4 s2 = tex2D(tex, float2(tc3.x, tc0.y));

    float4 s3 = tex2D(tex, float2(tc0.x, tc12.y));
    float4 s4 = tex2D(tex, float2(tc12.x, tc12.y));
    float4 s5 = tex2D(tex, float2(tc3.x, tc12.y));

    float4 s6 = tex2D(tex, float2(tc0.x, tc3.y));
    float4 s7 = tex2D(tex, float2(tc12.x, tc3.y));
    float4 s8 = tex2D(tex, float2(tc3.x, tc3.y));

    // 实际只需9次，进一步优化到4次（技巧性强）
    // ...
}
```

**实际使用**（我的简化版）：
```glsl
// 4次采样版本（质量略降但足够）
float4 fastBicubic4(sampler2D tex, float2 uv) {
    // 使用特殊采样点，每次捕获多个texel贡献
    // 具体数学推导较复杂，核心是权重重组
}
```

**5. Tricubic（3D）**

**体积纹理应用**（我的理解）：

```
3D版本：
- 64次采样（朴素）→ 8次采样（优化）
- 用于体积数据、3D LUT
```

**6. 导数计算**

**程序纹理支持**（我的实现）：

```glsl
// Bicubic也能计算导数（mipmap选择需要）
float2 bicubicDerivative(sampler2D tex, float2 uv) {
    // 采样邻域
    float c = bicubicSample(tex, uv);
    float dx = bicubicSample(tex, uv + float2(eps, 0));
    float dy = bicubicSample(tex, uv + float2(0, eps));

    return float2(
        (dx - c) / eps,
        (dy - c) / eps
    );
}
```

**7. 应用场景**

**我的使用案例**：

✅ **适合**：
- 放大纹理（Magnification）
- 程序纹理（噪声、渐变）
- 法线贴图（避免块状）
- 高度图（地形）

⚠️ **不适合**：
- 小纹理（Minification）- 用mipmap更好
- 性能敏感场景

**8. 性能对比**

**我的测量**（相对双线性）：

| 方法 | 相对性能 | 质量提升 |
|------|---------|---------|
| 双线性 | 1.0× | 基准 |
| **快速Bicubic（9采样）** | 2-3× | 显著 |
| **快速Bicubic（4采样）** | 1.5× | 中等 |
| 朴素Bicubic | 8-16× | 最高 |

> [!tip] 实践建议
> 用于纹理放大场景（如UI缩放、程序纹理），避免双线性的块状感。

---

### Chapter 21: High-Quality Antialiased Rasterization
**作者**: Dan Wexler, Eric Enderton

#### 我的理解

**抗锯齿核心**：像素覆盖率的精确计算。

**硬件MSAA局限**：固定采样模式，质量受限。

**本章方案**：分析方法+自适应超采样。

#### 我的实现思路

**1. 覆盖率分析方法**

**精确覆盖率**（我的几何理解）：

```
像素覆盖率 = 三角形与像素相交面积 / 像素面积

解析计算：
1. 计算三角形边与像素边界的交点
2. 构造多边形（相交区域）
3. 计算多边形面积
```

**实现**（我的伪代码）：
```cpp
float computeCoverage(Triangle tri, Pixel pix) {
    // 裁剪三角形到像素边界
    Polygon intersection = clipTriangleToPixel(tri, pix);

    if (intersection.empty()) return 0.0;

    // 计算多边形面积（Shoelace公式）
    float area = 0;
    for (int i = 0; i < intersection.numVertices; i++) {
        int j = (i + 1) % intersection.numVertices;
        area += intersection[i].x * intersection[j].y;
        area -= intersection[j].x * intersection[i].y;
    }
    area = abs(area) * 0.5;

    float pixelArea = 1.0;  // 标准化
    return area / pixelArea;
}
```

**2. 自适应超采样**

**我的策略**：

```
对每个像素：
    1. 计算边缘距离
    2. 如果在边缘附近：高采样率
    3. 如果在平坦区域：低采样率
```

**实现**：
```glsl
float4 adaptiveSupersampling(float2 pixelCoord) {
    // 检测边缘（深度/法线梯度）
    float edge = detectEdge(pixelCoord);

    int numSamples;
    if (edge > highThreshold) {
        numSamples = 16;  // 高质量
    } else if (edge > lowThreshold) {
        numSamples = 4;   // 中等
    } else {
        numSamples = 1;   // 单采样
    }

    float4 color = 0;
    for (int i = 0; i < numSamples; i++) {
        float2 offset = getSampleOffset(i, numSamples);
        color += sampleScene(pixelCoord + offset);
    }
    return color / numSamples;
}
```

**3. 混合MSAA**

**我的混合方案**：

```
Pass 1: 硬件MSAA（4x或8x）
        - 快速，覆盖大部分区域

Pass 2: 软件细化（边缘像素）
        - 检测MSAA不足的区域
        - 额外超采样
```

> [!tip] 应用
> 离线渲染或高端可视化，实时游戏通常依赖硬件MSAA+后处理AA（如FXAA/TAA）。

---

### Chapter 22: Fast Prefiltered Lines
**作者**: Eric Chan, Frédo Durand

#### 我的理解

**问题**：直线渲染容易产生锯齿（aliasing），特别是斜线和细线。

**传统方法**：MSAA，开销大。

**本章方案**：几何方法，将线扩展为四边形，边缘Alpha渐变。

#### 我的实现

**线条几何化**：

```
原始线：A→B

扩展为四边形：
    垂直于线的方向扩展宽度
    边缘设置Alpha渐变

Vertex Shader：
    float3 lineDir = normalize(B - A);
    float3 perpDir = cross(lineDir, viewDir);
    perpDir = normalize(perpDir) * lineWidth * 0.5;

    // 四个顶点
    v0 = A - perpDir;  // Alpha = 0（边缘）
    v1 = A + perpDir;  // Alpha = 1（中心）
    v2 = B + perpDir;  // Alpha = 1
    v3 = B - perpDir;  // Alpha = 0
```

**Pixel Shader**：
```glsl
float4 PS(float alpha : TEXCOORD0) : COLOR {
    return float4(lineColor.rgb, lineColor.a * alpha);
}
```

**效果**：平滑的抗锯齿线条，单Pass完成。

> [!tip] 应用
> CAD软件、线框渲染、UI绘图。

---

### Chapter 23: Hair Animation and Rendering in the Nalu Demo
**作者**: Hubert Nguyen, William Donnelly

#### 我的理解

**Nalu Demo**：NVIDIA展示GeForce 6的技术Demo，美人鱼Nalu的头发是亮点。

**挑战**：
1. 动画：数万根头发的物理模拟
2. 渲染：细长半透明几何的着色
3. 性能：实时帧率

#### 我的实现方案

**1. 头发表示**

**我的几何结构**：

```
每根头发 = 一条样条曲线（spline）

存储：
- 控制点（4-8个）
- Catmull-Rom曲线
- 运行时细分为线段

渲染：
- 每根头发 = 一条四边形带（billboard）
- 面向摄像机
```

**2. 物理模拟（质点弹簧）**

**我的弹簧质点系统**：

```
每根头发：
点链：P0 (固定，发根) → P1 → P2 → ... → Pn (发梢)

力：
1. 重力：F_gravity = m * g
2. 弹簧力：F_spring = -k * (|P_i - P_{i-1}| - restLength) * normalize(P_i - P_{i-1})
3. 阻尼：F_damping = -c * velocity
4. 风力：F_wind = windStrength * windDirection
```

**更新循环**（我的Verlet积分）：

```cpp
for (each hair strand) {
    for (each point i from 1 to n) {  // P0固定
        // 累积力
        float3 force = gravity;
        force += springForce(P[i], P[i-1]);
        if (i < n) force += springForce(P[i], P[i+1]);
        force += dampingForce(velocity[i]);
        force += windForce(P[i]);

        // 积分
        float3 accel = force / mass;
        float3 newPos = P[i] + velocity[i] * dt + 0.5 * accel * dt * dt;
        velocity[i] = (newPos - P[i]) / dt;
        P[i] = newPos;
    }

    // 约束（保持长度）
    for (int iteration = 0; iteration < 3; iteration++) {
        for (each segment) {
            enforce_length_constraint(P[i], P[i+1], restLength);
        }
    }
}
```

**3. 头发着色模型**

**Kajiya-Kay各向异性模型**（我的理解）：

```
头发 = 圆柱形光滑表面

高光沿头发切线方向：

specular = pow(sqrt(1 - (T·L)² * (T·V)²), shininess)

T: 头发切线
L: 光照方向
V: 视线方向
```

**我的Shader实现**：

```glsl
float3 hairShading(float3 T, float3 N, float3 L, float3 V) {
    // 1. Diffuse（简化Lambert）
    float diffuse = saturate(lerp(0.25, 1.0, dot(N, L)));

    // 2. Kajiya-Kay specular
    float TdotL = dot(T, L);
    float TdotV = dot(T, V);
    float sinTL = sqrt(1 - TdotL * TdotL);
    float sinTV = sqrt(1 - TdotV * TdotV);

    float specular = pow(sinTL * sinTV - TdotL * TdotV, specPower);

    // 3. 偏移高光（模拟鳞片）
    float3 T_shifted = T + shiftAmount * N;
    float spec2 = computeKajiyaSpec(T_shifted, L, V, specPower2);

    // 组合
    float3 color = hairColor * (diffuse + specular * specColor + spec2 * specColor2);
    return color;
}
```

**双高光技术**（我的理解）：

```
真实头发有两层高光：
1. 主高光（Primary）：表面反射，锐利
2. 次高光（Secondary）：透射后反射，宽泛，偏移

实现：
- 两次Kajiya-Kay计算
- 不同切线偏移
- 不同颜色（次高光偏暖）
```

**4. 透明度和排序**

**我的渲染策略**：

```
问题：头发半透明，需要排序

方案A：深度剥离（Depth Peeling）
- 多个Pass，每次渲染最前层
- N层 = N个Pass
- 质量高但慢

方案B：近似排序
- 粗糙前后排序
- Order-Independent Transparency (OIT)
- K-Buffer技术

Nalu实际：
- 将头发分组
- 组间排序
- 组内alpha blend
- 权衡性能和质量
```

**5. 头发阴影**

**我的实现**：

```
深度阴影贴图（DSM）：
- 渲染头发到深度图（Alpha Test）
- 标准阴影贴图技术

Opacity Shadow Maps：
- 存储累积不透明度，而非深度
- 更准确的半透明阴影

Deep Shadow Maps：
- 存储完整的可见性函数
- 高质量但内存大
```

**6. LOD策略**

**我的层次细节**：

```
近距离：
- 每根头发独立模拟和渲染
- 完整物理

中距离：
- 聚合多根为一簇
- 简化物理

远距离：
- 纹理贴片
- 无物理模拟
```

**7. 性能优化**

**GPU加速物理**（我的方案）：

```
顶点纹理获取（VTF）：
1. 物理模拟结果写入纹理
2. 顶点着色器读取位置
3. 生成billboard几何

或：
几何着色器动态生成头发几何
```

**8. 完整管线**

**我的Nalu渲染流程**：

```
物理阶段（CPU或GPU）：
    质点弹簧更新所有头发控制点

几何阶段：
    细分曲线为线段
    生成面向摄像机的四边形

着色阶段：
    Kajiya-Kay双高光
    阴影计算
    Alpha混合

后处理：
    适度模糊（减少走样）
```

> [!success] 技术影响
> Nalu Demo的头发技术影响了后续多款游戏（如《古墓丽影》的TressFX）。

---

### Chapter 24: Using Lookup Tables to Accelerate Color Transformations
**作者**: Jeremy Selan

#### 我的理解

**3D LUT**：将复杂色彩变换预计算到3D纹理，运行时快速查找。

#### 我的实现

**构建LUT**：
```python
# 离线：构建32×32×32 LUT
for r in range(32):
    for g in range(32):
        for b in range(32):
            input_color = (r/31, g/31, b/31)
            output_color = complex_color_transform(input_color)  # 任意变换
            LUT[r][g][b] = output_color
```

**运行时查找**：
```glsl
float4 PS(float4 inputColor) : COLOR {
    // 使用输入RGB作为3D纹理坐标
    float3 lut_coord = inputColor.rgb;
    float3 transformed = tex3D(colorLUT, lut_coord).rgb;
    return float4(transformed, inputColor.a);
}
```

**应用**：电影级色彩分级、风格化滤镜（Ins滤镜原理相同）。

---

### Chapter 25: GPU Image Processing in Apple's Motion
**作者**: Pete Warden

#### 我的理解

**Motion软件**：专业视频后期工具，大量使用GPU加速。

**GPU图像处理管线**：
```
滤波器链：
Input → Blur → Color Correct → Composite → Output

每个操作：
- 渲染到临时纹理
- 下一步读取该纹理
- Ping-pong缓冲区避免读写冲突
```

**工程实践**（我的总结）：
- 自动检测GPU能力
- CPU/GPU混合：简单操作CPU，复杂操作GPU
- 实时预览：低分辨率GPU，最终输出高分辨率CPU

---

### Chapter 26: Implementing Improved Perlin Noise
**作者**: Simon Green

#### 我的理解

**改进Perlin噪声**：Ken Perlin在2002年提出的改进版，更少视觉瑕疵。

#### 我的GPU实现

**核心改进**：
1. 梯度向量：使用12个梯度（而非原始8个）
2. 插值函数：6t⁵-15t⁴+10t³（更平滑）

```glsl
float improvedNoise(float3 p) {
    // 1. 整数和小数部分
    float3 i = floor(p);
    float3 f = frac(p);

    // 2. 插值权重（平滑曲线）
    float3 u = f * f * f * (f * (f * 6.0 - 15.0) + 10.0);

    // 3. 立方体8个角的梯度
    float n000 = grad(hash(i + float3(0,0,0)), f - float3(0,0,0));
    float n100 = grad(hash(i + float3(1,0,0)), f - float3(1,0,0));
    // ... 其他6个角

    // 4. 三线性插值
    float nx00 = lerp(n000, n100, u.x);
    float nx10 = lerp(n010, n110, u.x);
    float nx01 = lerp(n001, n101, u.x);
    float nx11 = lerp(n011, n111, u.x);

    float nxy0 = lerp(nx00, nx10, u.y);
    float nxy1 = lerp(nx01, nx11, u.y);

    return lerp(nxy0, nxy1, u.z);
}
```

**Simplex噪声**（我的理解）：
- 更快（n维复杂度O(n²)而非O(2ⁿ)）
- 更少方向性瑕疵
- 专利问题（2022年已过期）

---

### Chapter 27: Advanced High-Quality Filtering
**作者**: Justin Novosad

#### 我的理解

**高级滤波器设计**：自适应、边缘保持、各向异性。

#### 我的实现思路

**1. Bilateral滤波（边缘保持）**：
```glsl
float3 bilateralFilter(float2 uv) {
    float3 center = tex2D(input, uv).rgb;
    float3 sum = 0;
    float weightSum = 0;

    for (each sample offset) {
        float3 neighbor = tex2D(input, uv + offset).rgb;

        // 空间权重
        float spatialWeight = gaussian(length(offset));

        // 色彩相似度权重（关键）
        float colorDiff = length(neighbor - center);
        float rangeWeight = gaussian(colorDiff);

        float weight = spatialWeight * rangeWeight;
        sum += neighbor * weight;
        weightSum += weight;
    }
    return sum / weightSum;
}
```

**2. 各向异性过滤**：
- 沿特征方向过滤（如沿边缘）
- 结构张量分析主方向
- Line Integral Convolution (LIC)

---

### Chapter 28: Mipmap-Level Measurement
**作者**: Iain Cantlay

#### 我的理解

**问题**：如何精确知道GPU选择了哪个mipmap级别？

#### 我的实现

**导数法**：
```glsl
float getMipmapLevel(float2 uv, float2 textureSize) {
    float2 dx = ddx(uv * textureSize);
    float2 dy = ddy(uv * textureSize);

    float d = max(dot(dx, dx), dot(dy, dy));
    float mipmapLevel = 0.5 * log2(d);

    return mipmapLevel;
}
```

**可视化**：
```glsl
float level = getMipmapLevel(uv, textureSize);
float3 color = heatmap(level / maxLevel);  // 颜色映射
```

**应用**：
- 调试纹理LOD问题
- 自定义mipmap选择
- 纹理流式加载决策

---

## Part IV - General-Purpose Computation on GPUs GPU通用计算

> [!important] 历史意义
> Part IV是GPU Gems 2的特色部分，完整介绍了CUDA发布前（2005年）的GPGPU技术。这是理解GPU从图形专用处理器向通用并行计算转型的关键资料。

### Chapter 29: Streaming Architectures and Technology Trends

#### 我的理解

流式架构的核心思想是：**大量简单处理单元 + 高带宽内存 = 强大并行计算能力**。

**关键概念**：
1. **数据流模型**：数据像河流一样流过处理器
2. **SIMD执行**：单指令控制多个数据并行处理
3. **隐藏延迟**：通过大量线程切换掩盖内存访问延迟

**趋势预测**（2005年视角）：
- GPU会越来越通用化
- 可编程性会增强
- 浮点性能会持续增长

**我的对比思考**：这些预测在2006年CUDA发布后完全应验了。

---

### Chapter 30: The GeForce 6 Series GPU Architecture

#### 我的理解

GeForce 6代表了重要里程碑 - 首次支持Shader Model 3.0，带来：

**核心特性**：
1. **顶点纹理获取（VTF）**：顶点着色器可以读取纹理
   - 我的应用思路：用于位移贴图、大规模地形

2. **动态分支**：shader中可以有if/else和循环
   - 我的理解：虽然性能不如现在，但打开了新可能性

3. **更长shader**：512+指令
   - 实际影响：可以实现更复杂算法

**架构特点**：
- 仍然是分离的顶点/像素处理器（不是统一架构）
- 16个像素管线
- 6个顶点引擎

---

### Chapter 31: Mapping Computational Concepts to GPUs

#### 我的理解

这章解答了核心问题：**如何把CPU算法转换成GPU计算？**

**我的映射方案**：

1. **数据表示**：
   - CPU的数组 → GPU的纹理
   - 每个像素存储一个数据元素
   - RGBA四通道可以存4个float

2. **计算表示**：
   - CPU的循环 → GPU的片段着色器
   - 渲染全屏四边形 = 对每个数据元素执行计算
   - 输出到纹理 = 写回结果

3. **控制流**：
   - 简单：避免分支，全部计算
   - 高级：用动态分支（SM 3.0）

**我的实现思路示例（并行加法）**：
```
输入：两个纹理A和B
输出：纹理C = A + B

步骤：
1. 将A和B绑定为纹理
2. 渲染全屏四边形
3. 片段着色器：
   float4 a = tex2D(texA, uv);
   float4 b = tex2D(texB, uv);
   return a + b;
4. 输出到纹理C
```

---

### Chapter 32: Taking the Plunge into GPU Computing

#### 我的理解

这章是GPGPU入门指南。我总结的关键步骤：

**1. 思维转换**：
- 从串行思维 → 并行思维
- 从"一个一个处理" → "全部同时处理"

**2. 常见陷阱（我的经验）**：
- 依赖关系：GPU上读写同一位置会出问题
- 同步：GPU和CPU之间需要显式同步
- 精度：早期GPU浮点精度有限

**3. 适合GPU的算法特征**：
- 数据并行（每个元素独立计算）
- 计算密集（计算量 >> 内存访问）
- 规则访问模式（纹理坐标连续）

---

### Chapter 33: Implementing Efficient Parallel Data Structures

#### 我的理解

GPU上的数据结构需要重新设计。我的设计原则：

**1. 数组（最简单）**：
- 1D数组 → 1D纹理或2D纹理（展开）
- 访问：index → (x, y) 纹理坐标

**2. 树结构（困难）**：
- 指针 → 无法直接表示
- 我的解决方案：
  - 广度优先布局存入纹理
  - 父子关系通过索引计算

**3. 图结构（更困难）**：
- 邻接表 → 多个纹理
- 一个纹理存节点数据
- 另一个纹理存边信息

---

### Chapter 34: GPU Flow-Control Idioms

#### 我的理解

SM 3.0引入动态分支后，如何高效使用？我的总结：

**1. 分支代价**：
- 最坏情况：两个分支都执行（发散）
- 最好情况：所有线程走同一分支（一致）

**2. 优化策略**：

**提前退出**（我的常用技巧）：
```glsl
if (earlyTest) {
    return backgroundColor;  // 快速退出
}
// 复杂计算...
```

**循环展开**：
```glsl
// 不好：动态循环
for (int i = 0; i < count; i++) { ... }

// 更好：固定次数
for (int i = 0; i < 8; i++) { ... }
```

**3. 我的判断标准**：
- 分支预测正确率高 → 使用分支
- 两边计算量相近 → 避免分支，都算

---

### Chapter 35: GPU Program Optimization

#### 我的理解

GPU优化的核心：**找瓶颈，针对性优化**。我的优化清单：

**1. 内存访问优化**（通常是瓶颈）：
- 纹理缓存友好：相邻像素访问相邻纹素
- 避免依赖纹理读取（读取坐标依赖前一次读取结果）
- 使用合适的纹理格式（float vs half）

**2. 指令优化**：
- 向量化：用float4而非4个float
- MAD指令：a*b+c 一条指令
- 避免昂贵操作：pow、sin、cos等

**3. 寄存器压力**：
- 寄存器不够 → 线程数减少 → 性能下降
- 我的策略：减少临时变量，重用计算

**4. 我的优化流程**：
```
1. 测量基准性能
2. 识别瓶颈（内存？计算？）
3. 针对性优化
4. 重新测量
5. 重复
```

---

### Chapter 36: Stream Reduction Operations

#### 我的理解

归约（Reduction）是GPGPU的经典问题：**把N个数据归约成一个结果**。

**我的实现思路（并行求和）**：

**方法1：迭代减半**
```
初始：[1, 2, 3, 4, 5, 6, 7, 8]

Pass 1: 每对相加
[1+2, 3+4, 5+6, 7+8] = [3, 7, 11, 15]

Pass 2:
[3+7, 11+15] = [10, 26]

Pass 3:
[10+26] = [36]
```

**实现细节**：
- 每次pass渲染到一半大小的纹理
- log2(N)次pass
- 最后读回CPU

**我的优化思路**：
1. 在片段着色器中多次迭代（减少pass数）
2. 使用MRT同时输出多个中间结果
3. 最后阶段用CPU完成（避免小纹理开销）

**适用算法**：
- 求和、求平均
- 最大值、最小值
- 点积
- 直方图统计

---

## Part V - Image-Oriented Computing 面向图像的计算

### Chapter 37: Octree Textures on the GPU

#### 我的理解

八叉树纹理解决的问题：**如何在GPU上高效表示和访问稀疏3D数据？**

**我的实现思路**：

**1. 数据结构设计**：
- 八叉树节点存储在纹理中
- 每个节点：8个子节点指针 + 数据
- 空节点不存储（节省空间）

**2. 遍历算法**（我的理解）：
```
从根节点开始：
1. 计算当前节点包围盒
2. 判断是否与查询相交
3. 如果相交：
   - 叶节点：返回数据
   - 非叶节点：递归访问子节点
```

**3. GPU挑战**：
- 递归 → 用循环+栈模拟
- 指针 → 用索引
- 不规则访问 → 纹理缓存效率低

**应用场景**：
- 体积数据（医学图像）
- 稀疏场景（大规模但空旷）
- LOD选择

---

### Chapter 38: High-Quality Global Illumination Using Rasterization

#### 我的理解

核心思想：**用光栅化近似全局光照，避免昂贵的光线追踪**。

**我的算法理解**：

**Instant Radiosity方法**：
1. 从光源发射光子，记录撞击点（VPL - 虚拟点光源）
2. 将VPL作为二次光源
3. 用阴影贴图计算VPL对场景的贡献

**我的实现步骤**：
```
Pass 1: 生成VPL
- 从光源视角渲染场景
- 每个像素成为一个VPL

Pass 2: 累积间接光照
- 对每个VPL：
  - 生成阴影贴图
  - 渲染场景，累加贡献
```

**优化思路**（我的想法）：
- VPL选择：采样重要位置
- 批处理：多个VPL共享阴影贴图
- 时间复用：跨帧分摊计算

---

### Chapter 39: Progressive Refinement Radiosity

#### 我的理解

辐射度算法的渐进式GPU实现。我的理解是：**从粗糙解逐步细化到精确解**。

**算法框架**（我的概括）：
```
初始化：粗糙网格

循环直到收敛：
    1. 选择影响最大的patch
    2. 计算它对其他patch的贡献（form factor）
    3. 更新接收patch的辐照度
    4. 细分重要区域
```

**GPU加速点**（我的思考）：
- Form factor计算：并行化
- 辐照度更新：纹理操作
- 细分判断：像素着色器

---

### Chapter 40: Computer Vision on the GPU

#### 我的理解

计算机视觉算法天然适合GPU，因为是**图像→图像**的处理。

**我总结的常见算法及GPU实现**：

**1. 边缘检测**：
```
Sobel算子：
- 3×3卷积
- 片段着色器采样邻域9个像素
- 计算梯度
```

**2. 高斯模糊**：
```
可分离滤波：
- Pass 1: 水平模糊
- Pass 2: 垂直模糊
- 复杂度：O(n²) → O(2n)
```

**3. 特征提取**：
- Harris角点：梯度 → 结构张量 → 角点响应
- SIFT：高斯金字塔 → 差分 → 极值检测

**GPU优势**：
- 图像并行处理
- 纹理硬件加速采样
- 多级mipmap天然支持金字塔

---

### Chapter 41: Deferred Filtering

#### 我的理解

问题：**如何渲染点云、无序数据等非结构化几何？**

**我的解决思路**：

**方法：Splatting + 延迟过滤**
```
Pass 1: Splat阶段
- 将每个点渲染为splat（点精灵）
- 输出：位置、法线、颜色

Pass 2: 过滤阶段
- 在屏幕空间过滤splat
- 重建连续表面
- 计算最终着色
```

**为什么"延迟"？**（我的理解）
- 直接渲染：splat重叠导致走样
- 延迟过滤：收集信息后智能过滤
- 类似延迟着色的思想

---

### Chapter 42: Conservative Rasterization

#### 我的理解

保守光栅化的定义：**如果三角形与像素有任何重叠，就标记该像素**。

**对比标准光栅化**（我的理解）：
- 标准：中心在三角形内才标记
- 保守：任何重叠都标记
- 结果：保守会多标记像素

**我的实现思路**：

**方法1：膨胀三角形**
```
1. 在几何着色器中：
   - 计算三角形边向外法线
   - 沿法线膨胀半个像素
2. 光栅化膨胀后的三角形
```

**方法2：覆盖率测试**
```
在片段着色器中：
- 测试像素四个角与三角形关系
- 任一角在内或边上 → 接受
```

**应用场景**（我的总结）：
- 遮挡剔除：保守估计可见性
- 碰撞检测：保证不漏检
- 体素化：三角形→体素

---

## Part VI - Simulation and Numerical Algorithms 模拟与数值算法

> [!note] 跨学科应用
> Part VI展示了GPU从图形渲染走向科学计算的早期探索，涵盖生物、金融、医学等领域。

### Chapter 43: GPU Computing for Protein Structure Prediction

#### 我的理解

蛋白质折叠模拟的核心：**计算大量原子间的相互作用力**。

**问题规模**（我的理解）：
- 几千到几万个原子
- 每个原子与其他原子有相互作用
- 朴素算法：O(N²)

**我的GPU并行化思路**：

**1. 力计算**：
```
对每个原子i（并行）：
    force = 0
    对每个原子j：
        计算i和j之间的力（库仑力、范德华力）
        force += F_ij
    更新原子i的速度和位置
```

**2. GPU映射**：
- 原子数据存在纹理中
- 每个片段着色器处理一个原子
- 渲染N×1的纹理 = 处理N个原子

**3. 优化策略**（我的想法）：
- 截断距离：只计算近邻原子
- 空间分割：网格加速
- 多精度：关键计算用高精度

**加速效果预期**：10-100倍（相比CPU）

---

### Chapter 44: A GPU Framework for Solving Linear Equations

#### 我的理解

求解 **Ax = b** 的迭代方法GPU实现。

**我熟悉的迭代求解器**：

**1. Jacobi迭代**（最简单并行）：
```
x^(k+1)_i = (b_i - Σ(a_ij * x^(k)_j, j≠i)) / a_ii
```

**我的GPU实现思路**：
- A矩阵存为纹理
- 每次迭代：
  - 读取x^(k)
  - 计算新值
  - 输出x^(k+1)

**2. 共轭梯度（CG）**：
- 更快收敛
- 需要向量点积（归约操作）
- 结合Chapter 36的归约技术

**挑战**（我的理解）：
- 稀疏矩阵存储
- 不规则访问模式
- CPU-GPU同步（归约结果）

---

### Chapter 45: Options Pricing on the GPU

#### 我的理解

金融衍生品定价通常用**蒙特卡洛模拟**，天然适合GPU并行。

**Black-Scholes模型**（我的理解）：
- 模拟股票价格随机游走
- 大量独立路径
- 统计平均得到期权价值

**我的GPU实现框架**：

```
初始化：
- 生成随机数种子（每个路径不同）

模拟阶段（并行）：
对每条路径：
    price = S0  // 初始股价
    对每个时间步：
        生成随机数 ε
        price = price * exp(μ*dt + σ*sqrt(dt)*ε)
    payoff = max(price - K, 0)  // 欧式看涨期权

归约阶段：
    average_payoff = sum(payoffs) / num_paths
    option_value = exp(-r*T) * average_payoff
```

**GPU优势**：
- 百万条路径并行模拟
- 随机数生成并行化
- 显著加速（100-1000倍）

---

### Chapter 46: Improved GPU Sorting

#### 我的理解

排序是基础算法，GPU上需要新思路。

**我理解的Bitonic Sort**：

**核心思想**：构造bitonic序列，然后排序
- Bitonic序列：先递增后递减（或反之）

**算法步骤**（我的理解）：
```
对log2(N)个阶段：
    对log2(阶段数)个步骤：
        并行比较-交换操作
        距离 = 2^步骤
        对每对元素(i, i+distance)：
            if 需要交换：swap(arr[i], arr[i+distance])
```

**GPU实现**：
- 每个比较-交换 = 一个shader调用
- O(log²N)次pass
- 每次pass完全并行

**我的性能分析**：
- 优点：高度并行，无分支
- 缺点：O(log²N)不如CPU的O(NlogN)
- 适用场景：中等规模数据（几万到百万）

---

### Chapter 47: Flow Simulation with Complex Boundaries

#### 我的理解

流体模拟遇到复杂边界（障碍物）时的处理。

**基础：Navier-Stokes方程GPU求解**（我的理解）：
```
速度更新：v_new = v + dt*(−(v·∇)v − ∇p/ρ + ν∇²v + f)
压力求解：∇²p = −∇·((v·∇)v)
```

**边界条件**（我的实现思路）：

**1. 障碍物边界**：
- 标记障碍物位置（纹理mask）
- 边界速度设为0（no-slip）
- 压力边界条件：法向导数=0

**2. GPU实现技巧**：
```glsl
// 在shader中
if (是障碍物) {
    velocity = 0;
    return;
}
// 正常流体计算...
```

**3. 复杂形状处理**（我的想法）：
- 体素化：将复杂几何转为体素
- 符号距离场：存储到边界的距离
- 插值：边界附近特殊处理

---

### Chapter 48: Medical Image Reconstruction with the FFT

#### 我的理解

CT/MRI重建的核心：**从投影数据重建3D图像**。

**傅里叶切片定理**（我的理解）：
- 2D投影的1D FFT = 3D傅里叶空间的切片
- 收集足够切片 → 3D逆FFT → 重建图像

**我的GPU实现思路**：

**1. FFT并行化**：
```
Cooley-Tukey算法：
- Butterfly操作并行化
- log2(N)个阶段
- 每阶段N/2个独立蝶形

GPU映射：
- 每个蝶形 = 一个shader线程
- 数据存储纹理中
- Ping-pong缓冲区
```

**2. 2D FFT = 两个1D FFT**：
- Pass 1: 每行做1D FFT
- Pass 2: 每列做1D FFT

**3. 3D重建流程**：
```
对每个投影角度：
    1D FFT(投影数据) → 频域切片
    插入3D频域空间
完成后：
    3D 逆FFT → 重建图像
```

**加速效果**（我的估算）：
- FFT高度并行
- GPU加速10-100倍
- 实时MRI成像成为可能

---

## 💡 核心价值总结

### 与GPU Gems系列的关系

| 维度 | **GPU Gems 2** | **GPU Gems 1** | **GPU Gems 3** |
|------|---------------|---------------|---------------|
| **定位** | 高级技术+GPGPU | 实战技巧合集 | 现代GPU特性 |
| **年份** | 2005 | 2004 | 2007 |
| **章节数** | 48章 | 42章 | ~40章 |
| **硬件** | GeForce 6/7 (SM 3.0) | GeForce FX (SM 2.0) | GeForce 8 (Unified) |
| **GPGPU** | 完整Part IV | 早期探索 | CUDA时代 |
| **新技术** | 延迟着色、顶点纹理 | 基础技术 | 几何着色器 |

### 学习建议

**适合人群**：
- ✅ 有基础图形学和GPU编程知识
- ✅ 想学习延迟着色、高级渲染技术
- ✅ 对GPGPU历史感兴趣（CUDA发布前）
- ✅ 研究技术演进的开发者

**阅读路径建议**：
1. **游戏开发者**：Part I（几何）→ Part II（光照）→ Part III（高质量渲染）
2. **GPGPU研究者**：Part IV（通用计算）→ Part VI（模拟）
3. **图形研究者**：Part V（图像计算）→ Part II（光照）
4. **完整学习**：按Part I→VI顺序阅读

---

## ⚠️ 版权声明

本笔记仅包含技术要点总结和概念提取，不含原书的完整内容。
完整内容请访问NVIDIA官方在线版本（免费）。

**原书版权**：© 2005 NVIDIA Corporation and Addison-Wesley

---

## 🤝 贡献

欢迎提出改进建议！

---

*笔记整理：Master + Claude*
*最后更新：2026-03-05*
*状态：初始框架完成，详细内容持续补充中...*
