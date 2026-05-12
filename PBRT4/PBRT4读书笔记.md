# 《Physically Based Rendering: From Theory To Implementation》第4版 读书笔记

> 作者：Matt Pharr, Wenzel Jakob, Greg Humphreys
> 出版社：MIT Press
> 在线版本：https://pbr-book.org/4ed/
> GitHub源码：https://github.com/mmp/pbrt-v4

---

## 📚 阅读进度

- [x] Preface 序言
- [x] Chapter 1: Introduction
- [x] Chapter 2: Monte Carlo Integration
- [x] Chapter 3: Geometry and Transformations
- [x] Chapter 4: Radiometry, Spectra, and Color
- [x] Chapter 5: Cameras and Film
- [x] Chapter 6: Shapes
- [x] Chapter 7: Primitives and Intersection Acceleration
- [x] Chapter 8: Sampling and Reconstruction
- [x] Chapter 9: Reflection Models
- [x] Chapter 10: Textures and Materials
- [x] Chapter 11: Volume Scattering
- [x] Chapter 12: Light Sources
- [x] Chapter 13: Light Transport I: Surface Reflection
- [x] Chapter 14: Light Transport II: Volume Rendering
- [x] Chapter 15: Wavefront Rendering on GPUs
- [x] Chapter 16: Retrospective and the Future
- [x] Appendix A: Sampling Algorithms
- [x] Appendix B: Utilities
- [x] Appendix C: Processing the Scene Description

**当前进度**：✅ 16/16 章节 + 3/3 附录 —— 全书完成！

---

## 📖 目录

### 主要章节
- [Chapter 1: Introduction](#chapter-1-introduction)
- [Chapter 2: Monte Carlo Integration](#chapter-2-monte-carlo-integration)
- [Chapter 3: Geometry and Transformations](#chapter-3-geometry-and-transformations)
- [Chapter 4: Radiometry, Spectra, and Color](#chapter-4-radiometry-spectra-and-color)
- [Chapter 5: Cameras and Film](#chapter-5-cameras-and-film)
- [Chapter 6: Shapes](#chapter-6-shapes)
- [Chapter 7: Primitives and Intersection Acceleration](#chapter-7-primitives-and-intersection-acceleration)
- [Chapter 8: Sampling and Reconstruction](#chapter-8-sampling-and-reconstruction)
- [Chapter 9: Reflection Models](#chapter-9-reflection-models)
- [Chapter 10: Textures and Materials](#chapter-10-textures-and-materials)
- [Chapter 11: Volume Scattering](#chapter-11-volume-scattering)
- [Chapter 12: Light Sources](#chapter-12-light-sources)
- [Chapter 13: Light Transport I: Surface Reflection](#chapter-13-light-transport-i-surface-reflection)
- [Chapter 14: Light Transport II: Volume Rendering](#chapter-14-light-transport-ii-volume-rendering)
- [Chapter 15: Wavefront Rendering on GPUs](#chapter-15-wavefront-rendering-on-gpus)
- [Chapter 16: Retrospective and the Future](#chapter-16-retrospective-and-the-future)

### 附录
- [Appendix A: Sampling Algorithms](#appendix-a-sampling-algorithms)
- [Appendix B: Utilities](#appendix-b-utilities)
- [Appendix C: Processing the Scene Description](#appendix-c-processing-the-scene-description)

---

## 🎯 本书特色

### 与RTR4的区别

| 维度 | **PBRT4（本书）** | **RTR4** |
|------|------------------|----------|
| **核心主题** | 离线光线追踪 | 实时渲染 |
| **目标帧率** | 秒级到小时级 | 60-144fps |
| **渲染方式** | 路径追踪（Path Tracing） | 光栅化 + 混合光追 |
| **代码** | 完整C++17实现（15000+行） | 理论+伪代码 |
| **应用场景** | 电影渲染、建筑可视化 | 游戏、VR、交互 |

### 学习价值

- ✅ **完整的生产级代码**：可编译运行的渲染器
- ✅ **数学推导详尽**：从理论到实现的完整路径
- ✅ **工程实践并重**：性能优化、边界处理
- ✅ **补充RTR4深度**：蒙特卡洛、BRDF推导、路径追踪

---

## Preface 序言

### 核心观点

本书第4版的主要特点：
- **完整的C++17实现**：pbrt-v4渲染器包含约15,000行生产级代码
- **理论与实践结合**：每个算法都有数学推导和实际代码
- **开源免费**：在线版本和源码完全开放
- **物理精确**：基于物理的光传输模拟

### 第4版更新

相比第3版的主要改进：
- 新增GPU波前渲染（Chapter 15）
- 采用C++17现代特性
- 改进的采样算法
- 更完整的体积渲染
- 优化的BVH构建

---

## Chapter 1: Introduction

### 1.1 Literate Programming 文学化编程

**核心思想**（Donald Knuth）：
> 将程序从"指示计算机做什么"转变为"向人类解释我们想让计算机做什么"

**pbrt的实践**：
- 整本书本身就是一个文学化程序
- 使用"代码片段"（Fragment）机制组织代码
- 每个片段控制在10行以内，独立可理解
- 片段的呈现顺序≠编译顺序，符合人类思维

**优势**：
```cpp
// 传统方式：代码分散在多个文件
// 文学化编程：相关代码集中展示

<<Light Transport Equation>>
  <<Generate camera ray>>
  <<Find ray-surface intersection>>
  <<Evaluate BSDF>>
  <<Sample light sources>>
```

### 1.2 光线追踪算法基础

**核心流程（6步）**：

1. **光线生成（Ray Generation）**
   - 相机生成射线：`r(t) = o + t·d`
   - 针孔相机：从眼睛位置指向成像平面

2. **相交测试（Intersection）**
   - 将射线参数方程代入物体隐函数
   - 求解最小正根获取交点
   - 计算表面法线等几何信息

3. **光照计算（Lighting）**
   - 点光源辐照度公式：`dE = Φ·cosθ / (4πr²)`
   - 距离平方反比律 + 余弦衰减

4. **阴影测试（Shadow）**
   - 构造阴影射线（从表面指向光源）
   - 检测是否被遮挡

5. **表面散射（BRDF）**
   - 双向反射分布函数：`f_r(p, ω_o, ω_i)`
   - 描述材质如何散射入射光

6. **递归追踪（Recursion）**
   - 反射/折射光线的递归计算
   - 通过光传输方程（渲染方程）求解间接光照

**加速结构**：
- 使用BVH等加速结构
- 复杂度从O(mn)降至O(m log n)

### 1.3 pbrt系统架构

**14个核心接口类型**：

| 类别 | 类型 | 职责 |
|------|------|------|
| **渲染基础** | Spectrum | 光谱分布表示 |
| | Camera | 视角和透镜参数 |
| | Film | 图像存储和输出 |
| **几何** | Shape | 场景几何表示 |
| | Primitive | 几何+材质组合 |
| | 加速结构 | 快速相交测试 |
| **材质** | Material | 表面外观 |
| | BxDF | 反射/透射模型 |
| | Texture | 纹理定义 |
| **采样** | Sampler | 采样点生成 |
| | Filter | 图像重建滤波 |
| **光源** | Light | 光源定义 |
| | LightSampler | 光源采样策略 |
| **体积** | Medium | 参与介质 |
| | Integrator | 光传输求解器 |

**渲染管线（3阶段）**：

```markdown
阶段1：解析场景描述 → BasicScene对象
阶段2：创建具体实例 → 可渲染表示（如PerspectiveCamera）
阶段3：主渲染循环 → Integrator求解光传输方程
```

**工作流**：
```
ImageTileIntegrator（图像分块）
  ↓
RayIntegrator（生成相机射线）
  ↓
Sampler（提供采样位置）
  ↓
Scene Aggregate（加速结构相交测试）
  ↓
Material/BxDF（计算表面反射）
  ↓
Light（评估光照贡献）
  ↓
Film（输出最终图像）
```

**设计特点**：
- 标签分派（Tagged Dispatch）多态机制
- CPU和GPU统一接口
- 所有几何收集到单一聚合体（统一加速结构）

### 1.4 学习路径建议

**必读章节（所有读者）**：

| 章节 | 内容 | 原因 |
|------|------|------|
| Ch2-4 | 蒙特卡洛、几何、辐射度学 | 理论基础 |
| Ch5-8 | 相机、形状、加速、采样 | 图像形成 |

**学习策略**：
- 默认从前到后顺序阅读
- 星号标记的高级主题可第二遍再读
- 不必深究每个实现细节（如只需知道`Camera::GenerateRayDifferential()`的功能）

**不同背景的路径**：

```markdown
初学者：
├─ 按顺序读Ch1-8
└─ 掌握基础后再看光传输算法

有图形学基础：
├─ 快速浏览基础章节
└─ 重点Ch9-14（光传输）

GPU优化兴趣：
└─ 优先Ch15（GPU波前渲染）
```

### 1.5 代码使用说明

**文学化编程的阅读方式**：
- 代码片段可点击展开
- 理解概念即可，无需记忆细节
- 在线版支持交互式探索

**补充资源**：
- pbr-book.org/4ed/fig - 所有渲染图像
- 在线版包含额外章节（如双向光传输）

### 1.6 物理渲染简史

**关键里程碑**：
- Literate Programming（Knuth，TEX系统）
- 基于物理的光传输理论发展
- pbrt系统的四代演进（v1→v4）
- 从纯CPU到CPU+GPU统一架构

**第4版创新**：
- 首次支持GPU加速路径追踪
- 采用现代C++17特性重写
- 保持教学清晰性的同时提升性能

---


## Chapter 2: Monte Carlo Integration

### 2.1 Monte Carlo基础

**核心思想**：
通过随机采样评估积分，收敛速度与被积函数维度无关

**蒙特卡洛估计量**：
$$F_n = \frac{1}{n} \sum_{i=1}^{n} \frac{f(X_i)}{p(X_i)}$$

其中：
- $X_i$ 从概率密度函数 $p(x)$ 采样
- $p(x) > 0$ 当 $|f(x)| > 0$（必须满足）

**期望值**：
$$E[f(x)] = \int_D f(x)p(x)dx$$

**方差**：
$$V[F] = E[F^2] - E[F]^2$$

**收敛速度**：
- 误差以 $O(n^{-1/2})$ 速率下降
- 与维度无关！（优于数值求积）
- 维度无关性是处理渲染高维积分的关键

**估计量特性**：
- 无偏性：$E[F_n]$ = 真实积分值
- Las Vegas算法：结果确定
- Monte Carlo算法：平均意义上正确

### 2.2 提升效率的方法

#### 重要性采样（Importance Sampling）

**核心原理**：
- 选择与被积函数形状相似的采样分布
- 在函数值较大的区域集中采样

**理想情况**：
- 如果 $p(x) \propto f(x)$，方差趋于零
- 实践中使用近似分布仍能显著降低方差

**风险**：
- 糟糕的分布选择会大幅增加方差（可达36倍）
- 必须确保 $p(x)$ 非零区域覆盖 $f(x)$ 非零区域

#### 分层采样（Stratified Sampling）

**方法**：
1. 将积分域划分为不重叠的区域（strata）
2. 从每个区域独立采样
3. 防止样本聚集

**特性**：
- 永远不会增加方差（当函数均值各不相同时）
- 确保重要特征被采样到
- 维度诅咒：D维空间需要 $S^D$ 个样本

**使用建议**：
- 函数行为未知时，使用紧凑的分层
- 低维情况效果最好

#### 多重要性采样（MIS）

**应用场景**：
被积函数是多个函数乘积时

**平衡启发式权重**：
$$w_i(x) = \frac{n_i \cdot p_i(x)}{\sum_j n_j \cdot p_j(x)}$$

**关键思想**：
- 同时从多个分布采样
- 每个样本的权重考虑所有可能生成它的分布
- 降权来自不匹配技术的样本

**幂启发式**：
- 使用指数 $\beta=2$ 的增强版本
- 进一步抑制低概率贡献
- 通常性能更好

#### 俄罗斯轮盘赌（Russian Roulette）

**原理**：
- 以概率 $q$ 跳过昂贵的计算
- 未跳过的样本权重为 $\frac{1}{1-q}$ 补偿

**特性**：
- 保持无偏性
- 不降低方差，但提升效率
- 避免计算可能不重要的贡献

#### 分裂（Splitting）

**方法**：
- 对嵌套积分增加采样维度
- 外层每个样本对应内层多个样本
- 分摊昂贵的部分计算成本

### 2.3 反演法采样

**核心步骤**：
1. 对PDF积分得到CDF：$P(x) = \int_{-\infty}^{x} p(t)dt$
2. 生成均匀随机数：$\xi \sim U[0,1)$
3. 求逆得到样本：$X = P^{-1}(\xi)$

**数学原理**：
- 均匀样本映射到CDF上
- 结果遵循原始PDF分布
- 利用CDF的单调性

**CDF的作用**：
```markdown
离散情况：概率累积和（堆叠条形图）
连续情况：PDF的积分，其逆函数是采样公式
几何解释：从CDF纵轴的均匀值水平投影到曲线
```

**应用**：
- BSDF采样
- 光源采样
- 参与介质采样
- 与高质量采样器结合效果显著

### 2.4 分布变换

**一维变换**：
$$p_f(y) = \left|\frac{df}{dx}\right|^{-1} \cdot p(x)$$

其中 $Y = f(X)$

**多维变换（雅可比行列式）**：
$$p_T(y) = \frac{p(x)}{|J_T(x)|}$$

**雅可比行列式的作用**：
- 量化变换如何缩放微小体积元素
- 在坐标系转换时必须考虑
- 确保概率密度的正确性

**球面坐标采样**：
- 雅可比行列式：$r^2 \sin\theta$
- 转换公式：
$$p(r, \theta, \phi) = r^2 \sin\theta \cdot p(x, y, z)$$

**多维采样策略**：
1. 积分消除某些维度得到边缘分布
2. 先从边缘分布采样
3. 使用条件分布依次采样其余维度
4. 实现对非可分离联合分布的有效采样

**实践要点**：
- 导数/雅可比绝对值决定概率密度如何拉伸或压缩
- 单位球面上的方向采样需要正确的概率加权
- 边缘和条件分布的顺序采样处理复杂分布

---

## Chapter 3: Geometry and Transformations

### 我的理解

**几何基础设施**：渲染器的数学基础，所有几何操作的构建块。

### 3.1 坐标系统

**我的理解**：
- **左手系 vs 右手系**：pbrt使用左手系（z轴指向屏幕内）
- **重要性**：影响叉积方向、法线朝向

### 3.2-3.3 向量和点

**我的实现理解**：

```cpp
// Vector3: 表示方向和位移
template <typename T>
class Vector3 {
    T x, y, z;

    // 关键操作
    Vector3 operator+(Vector3 v);  // 向量加法
    Vector3 operator*(T s);        // 标量乘法
    T Dot(Vector3 v);              // 点积
    Vector3 Cross(Vector3 v);      // 叉积
    T Length();                    // 长度
    Vector3 Normalize();           // 归一化
};

// Point3: 表示3D空间位置
template <typename T>
class Point3 {
    T x, y, z;

    // 关键性质
    Point3 - Point3 = Vector3  // 两点相减得向量
    Point3 + Vector3 = Point3  // 点加向量得点
    Point3 + Point3 = ❌      // 点加点无意义
};
```

**设计哲学**（我的理解）：
- 类型安全：编译期防止错误操作（如两点相加）
- 明确语义：Point表位置，Vector表方向

### 3.4 法线

**我的理解**：

```cpp
// Normal3: 表面法向量
class Normal3 {
    Float x, y, z;
};

// 为什么需要单独的Normal类型？
// 答案：变换行为不同！

// 变换规则
Vector3 变换：v' = M × v
Normal3 变换：n' = (M^-1)^T × n  // 逆转置矩阵！
```

**为什么法线要用逆转置？**（我的推导）：

```
条件：法线垂直于切线
即：n · t = 0

变换后仍需满足：
n' · t' = 0

推导：
t' = M × t（切线正常变换）
n' · t' = n' · (M × t) = 0
=> (n'^T) × M × t = 0
=> 要使对所有t成立
=> n'^T = n^T × M^-1
=> n' = (M^-1)^T × n  ✓
```

### 3.5 光线

**我的实现思路**：

```cpp
class Ray {
    Point3 o;      // 起点（Origin）
    Vector3 d;     // 方向（Direction，已归一化）
    Float tMax;    // 最大参数（避免无限延伸）
    Float time;    // 时间（用于运动模糊）
    Medium medium; // 传播介质

    // 参数方程
    Point3 operator()(Float t) {
        return o + d * t;  // r(t) = o + t·d
    }
};

// 光线-物体求交
struct RayIntersection {
    Float t;              // 交点参数
    SurfaceInteraction si; // 交点信息
};
```

### 3.6 包围盒

**我的AABB实现**：

```cpp
// Axis-Aligned Bounding Box
class Bounds3 {
    Point3 pMin, pMax;  // 对角顶点

    // 关键操作
    Point3 Corner(int i);        // 获取8个角点
    Vector3 Diagonal();          // 对角线向量
    Float SurfaceArea();         // 表面积（用于SAH）
    Float Volume();              // 体积
    int MaxExtent();             // 最长轴

    // 扩展操作
    Bounds3 Union(Bounds3 b2);   // 包含两个盒子的最小盒
    Bounds3 Union(Point3 p);     // 包含点的扩展盒

    // 相交测试
    bool Intersect(Ray r, Float* t0, Float* t1);  // 光线相交
    bool IntersectP(Ray r);      // 快速测试（不返回t）
};

// 我的光线-AABB相交算法（Slab方法）
bool Bounds3::Intersect(Ray r, Float* t0, Float* t1) {
    Float tMin = 0, tMax = r.tMax;

    // 对每个轴（x,y,z）
    for (int i = 0; i < 3; i++) {
        // 计算该轴两个slab的交点
        Float invDir = 1 / r.d[i];
        Float tNear = (pMin[i] - r.o[i]) * invDir;
        Float tFar = (pMax[i] - r.o[i]) * invDir;

        // 处理方向为负的情况
        if (tNear > tFar) std::swap(tNear, tFar);

        // 更新总区间
        tMin = max(tMin, tNear);
        tMax = min(tMax, tFar);

        // 无交集
        if (tMin > tMax) return false;
    }

    *t0 = tMin;
    *t1 = tMax;
    return true;
}
```

### 3.7 变换

**我的变换系统理解**：

```cpp
// Transform类：封装4×4矩阵及其逆
class Transform {
    SquareMatrix<4> m;      // 变换矩阵
    SquareMatrix<4> mInv;   // 逆矩阵（提前计算，加速）

    // 构造基本变换
    static Transform Translate(Vector3 delta);
    static Transform Scale(Float x, Float y, Float z);
    static Transform RotateX/Y/Z(Float angle);
    static Transform LookAt(Point3 eye, Point3 look, Vector3 up);

    // 应用变换（重载operator()）
    Point3 operator()(Point3 p);
    Vector3 operator()(Vector3 v);
    Normal3 operator()(Normal3 n);  // 使用逆转置
    Ray operator()(Ray r);
    Bounds3 operator()(Bounds3 b);

    // 组合变换
    Transform operator*(Transform t2);  // 矩阵乘法
};

// 我的使用示例
Transform worldToCamera = LookAt(
    Point3(0, 5, 10),  // 相机位置
    Point3(0, 0, 0),   // 看向原点
    Vector3(0, 1, 0)   // 上方向
);

Transform scale = Scale(2, 2, 2);
Transform combined = scale * worldToCamera;  // 先scale再transform

// 变换光线
Ray cameraRay = combined(worldRay);
```

### 3.8 交点信息

**我的SurfaceInteraction结构**：

```cpp
struct SurfaceInteraction {
    // 几何信息
    Point3 p;          // 交点位置
    Float time;        // 交点时间
    Vector3 wo;        // 出射方向（指向相机）
    Normal3 n;         // 几何法线
    Point2 uv;         // 纹理坐标

    // 切线空间
    Vector3 dpdu, dpdv;  // 偏导数（切线）
    Normal3 dndu, dndv;  // 法线偏导（用于bump mapping）

    // 着色法线（可与几何法线不同）
    Normal3 shading.n;
    Vector3 shading.dpdu, shading.dpdv;

    // 关联对象
    const Shape* shape;
    const Primitive* primitive;

    // 散射函数
    BSDF* bsdf;  // 由Material生成

    // 计算散射方程
    void ComputeScatteringFunctions(RayDifferential ray);
};
```

### 3.9 球面几何

**我的球面坐标理解**：

```cpp
// 直角坐标 ↔ 球面坐标
// (x,y,z) ↔ (r,θ,φ)

// 转换公式
Vector3 SphericalDirection(Float sinTheta, Float cosTheta, Float phi) {
    return Vector3(
        sinTheta * cos(phi),
        sinTheta * sin(phi),
        cosTheta
    );
}

Float SphericalTheta(Vector3 v) {
    return acos(Clamp(v.z, -1, 1));  // θ ∈ [0,π]
}

Float SphericalPhi(Vector3 v) {
    Float p = atan2(v.y, v.x);
    return (p < 0) ? (p + 2*Pi) : p;  // φ ∈ [0,2π]
}

// 立体角
Float SolidAngle(Point3 p, Triangle tri) {
    // 投影到单位球
    Vector3 a = Normalize(tri.v0 - p);
    Vector3 b = Normalize(tri.v1 - p);
    Vector3 c = Normalize(tri.v2 - p);

    // 球面三角形面积（Girard定理）
    Float alpha = AngleBetween(b, c);
    Float beta = AngleBetween(c, a);
    Float gamma = AngleBetween(a, b);

    return alpha + beta + gamma - Pi;
}
```

---

## Chapter 4: Radiometry, Spectra, and Color

### 我的理解

**辐射度学**：光传输的物理基础，定量描述光的能量分布。

### 4.1 辐射度学基础

**我的物理量理解**：

```
能量层级（从大到小）：

1. 辐射能量 Q (Joule)
   - 光子携带的总能量

2. 辐射通量 Φ (Watt = J/s)
   - 单位时间的能量
   - Φ = dQ/dt

3. 辐照度 E (W/m²)
   - 单位面积接收的通量
   - E = dΦ/dA
   - 用于：Lambert定律、光照计算

4. 辐射强度 I (W/sr)
   - 单位立体角的通量（点光源）
   - I = dΦ/dω

5. 辐射亮度 L (W/(m²·sr))  ⭐⭐⭐ 最重要！
   - 单位面积、单位立体角的通量
   - L = d²Φ / (dA·dω·cosθ)
   - 关键性质：沿光线不变（在真空中）
```

**为什么Radiance最重要？**（我的理解）：

```
1. 传播不变性：
   L(p→direction) 沿直线传播时保持不变
   → 使光线追踪算法可行

2. 传感器测量：
   相机、眼睛测量的就是radiance

3. 渲染方程基础：
   L_o = ∫ f_r(ω_o, ω_i) L_i(ω_i) cosθ_i dω_i
```

### 4.2 光谱分布

**我的光谱表示**：

```cpp
// Spectrum类型：描述光的波长分布
class SampledSpectrum {
    static constexpr int nSamples = 4;  // 或更多
    Float values[nSamples];             // 各波长的能量

    // 运算
    SampledSpectrum operator+(SampledSpectrum s);  // 光叠加
    SampledSpectrum operator*(SampledSpectrum s);  // 滤波（材质吸收）
    Float y();  // 亮度（CIE Y值）

    // 从波长函数采样
    static SampledSpectrum FromSampled(
        const Float* lambda,  // 波长数组
        const Float* values,  // 对应能量
        int n
    );
};

// 黑体辐射（理想发光体）
Float BlackBody(Float lambda, Float T) {
    // Planck定律
    const Float c = 299792458;       // 光速
    const Float h = 6.62606957e-34;  // 普朗克常数
    const Float kb = 1.3806488e-23;  // 玻尔兹曼常数

    Float l5 = (lambda * 1e-9) * (lambda * 1e-9) *
               (lambda * 1e-9) * (lambda * 1e-9) *
               (lambda * 1e-9);
    return (2 * h * c * c) /
           (l5 * (exp((h * c) / (lambda * 1e-9 * kb * T)) - 1));
}
```

### 4.3 BRDF和BTDF

**我的散射函数理解**：

```
BRDF (Bidirectional Reflectance Distribution Function)
双向反射分布函数

定义：
f_r(p, ω_o, ω_i) = dL_o(p, ω_o) / dE_i(p, ω_i)
                 = dL_o(p, ω_o) / [L_i(p, ω_i) cosθ_i dω_i]

物理意义：
- 入射方向ω_i的微分辐照度 → 出射方向ω_o的微分辐亮度

性质：
1. Helmholtz互易性：
   f_r(p, ω_o, ω_i) = f_r(p, ω_i, ω_o)

2. 能量守恒：
   ∫_{hemisphere} f_r(p, ω_o, ω_i) cosθ_i dω_i ≤ 1

3. 非负性：
   f_r ≥ 0
```

**常见BRDF**（我的总结）：

```cpp
// 1. Lambert漫反射（完美漫反射）
Float LambertBRDF(Color albedo) {
    return albedo / Pi;  // 归一化使半球积分=albedo
}

// 2. 镜面反射（完美镜面）
Vector3 PerfectSpecular(Vector3 wo, Normal3 n) {
    return -wo + 2 * Dot(wo, n) * n;  // wi = reflect(wo, n)
    // BRDF = Dirac delta函数
}

// 3. Microfacet模型（真实材质）
Float MicrofacetBRDF(Vector3 wo, Vector3 wi, Normal3 n, Float roughness) {
    Vector3 wh = Normalize(wo + wi);  // 半角向量

    Float D = GGX_Distribution(wh, n, roughness);  // 法线分布
    Float G = Smith_Geometry(wo, wi, n, roughness); // 几何遮挡
    Float F = Fresnel_Schlick(Dot(wo, wh));        // 菲涅尔

    return (D * G * F) / (4 * Dot(wo, n) * Dot(wi, n));
}
```

### 4.4 渲染方程

**我的完整推导**：

```
目标：计算点p沿方向ω_o的出射辐亮度

1. 直接光照（自发光）：
   L_e(p, ω_o)

2. 反射光照：
   来自半球所有方向的入射光，经BRDF散射到ω_o

   L_r(p, ω_o) = ∫_Ω f_r(p, ω_o, ω_i) L_i(p, ω_i) |cosθ_i| dω_i

3. 完整渲染方程：
   L_o(p, ω_o) = L_e(p, ω_o) + ∫_Ω f_r(p, ω_o, ω_i) L_i(p, ω_i) |cosθ_i| dω_i

递归性质：
L_i(p, ω_i) 本身又是另一点的L_o
→ 需要递归求解或迭代求解
→ 路径追踪算法的基础
```

**我的路径追踪理解**：

```cpp
Spectrum PathTrace(Ray ray, int depth) {
    // 递归终止
    if (depth > maxDepth) return 0;

    // 相交测试
    SurfaceInteraction si;
    if (!scene.Intersect(ray, &si))
        return L_environment(ray.d);

    // 自发光
    Spectrum L_o = si.Le(-ray.d);

    // 采样入射方向
    Vector3 wi;
    Float pdf;
    Spectrum f = si.bsdf->Sample_f(-ray.d, &wi, &pdf);

    // 递归追踪
    Ray scattered(si.p, wi);
    Spectrum L_i = PathTrace(scattered, depth + 1);

    // 渲染方程估计
    L_o += f * L_i * AbsDot(wi, si.n) / pdf;

    return L_o;
}
```

### 4.5 颜色和光谱

**我的颜色空间理解**：

```
CIE XYZ（人眼响应）：
- X, Y, Z：三刺激值，对应人眼锥细胞
- Y：亮度
- x = X/(X+Y+Z), y = Y/(X+Y+Z)：色度坐标

RGB（设备相关）：
- sRGB：标准显示器色域
- Adobe RGB：更大色域
- 线性 vs Gamma校正（见GPU Gems 3 Ch24）

转换矩阵（XYZ → sRGB）：
[ R ]   [  3.2406 -1.5372 -0.4986 ]   [ X ]
[ G ] = [ -0.9689  1.8758  0.0415 ] × [ Y ]
[ B ]   [  0.0557 -0.2040  1.0570 ]   [ Z ]

Gamma校正：
sRGB_out = Linear^(1/2.2)  // 近似
```

---

## Chapter 5: Cameras and Film

### 我的理解

**相机模型**：将3D场景投影到2D图像的过程。

### 5.1 相机模型

**我的针孔相机实现**：

```cpp
class PerspectiveCamera {
    Transform CameraToWorld;  // 相机变换
    Float fov;                // 视场角
    Film* film;               // 胶片

    Ray GenerateRay(CameraSample sample) {
        // 1. 图像坐标[0,1]² → 屏幕坐标[-1,1]²
        Point2 pScreen(
            2 * sample.pFilm.x / film->resolution.x - 1,
            1 - 2 * sample.pFilm.y / film->resolution.y  // y翻转
        );

        // 2. 屏幕坐标 → 相机空间
        Point3 pCamera(
            pScreen.x * tan(fov/2) * aspectRatio,
            pScreen.y * tan(fov/2),
            1.0  // z=1平面
        );

        // 3. 生成光线（相机空间）
        Ray ray(Point3(0,0,0), Normalize(Vector3(pCamera)));

        // 4. 变换到世界空间
        return CameraToWorld(ray);
    }
};
```

**景深（Depth of Field）**（我的理解）：

```cpp
class ThinLensCamera {
    Float lensRadius;      // 透镜半径
    Float focalDistance;   // 对焦距离

    Ray GenerateRay(CameraSample sample) {
        // 1. 生成针孔光线
        Ray ray = GeneratePinholeRay(sample.pFilm);

        // 2. 计算对焦平面交点
        Float ft = focalDistance / ray.d.z;
        Point3 pFocus = ray(ft);

        // 3. 在透镜上采样起点
        Point2 pLens = lensRadius * ConcentricSampleDisk(sample.pLens);

        // 4. 从透镜点指向对焦点
        ray.o = Point3(pLens.x, pLens.y, 0);
        ray.d = Normalize(pFocus - ray.o);

        return CameraToWorld(ray);
    }
};
```

### 5.2 Film和像素采样

**我的Film实现**：

```cpp
class Film {
    Point2i resolution;        // 分辨率
    Bounds2f cropWindow;       // 裁剪窗口
    Filter* filter;            // 重建滤波器
    Float diagonal;            // 对角线长度（mm）

    struct Pixel {
        Float rgb[3];          // 累积颜色
        Float weightSum;       // 权重和
    };
    std::vector<Pixel> pixels;

    void AddSample(Point2 pFilm, Spectrum L, Float weight) {
        // 1. 找到影响的像素
        Bounds2 sampleBounds = filter->GetSampleBounds(pFilm);

        // 2. 对每个像素
        for (int y = sampleBounds.pMin.y; y < sampleBounds.pMax.y; y++) {
            for (int x = sampleBounds.pMin.x; x < sampleBounds.pMax.x; x++) {
                // 计算滤波器权重
                Float w = filter->Evaluate(pFilm - Point2(x, y));

                // 累积
                Pixel& pixel = pixels[y * resolution.x + x];
                for (int c = 0; c < 3; c++)
                    pixel.rgb[c] += L[c] * w * weight;
                pixel.weightSum += w * weight;
            }
        }
    }

    void WriteImage() {
        // 归一化并输出
        for (Pixel& p : pixels) {
            for (int c = 0; c < 3; c++)
                p.rgb[c] /= p.weightSum;
        }
        // Tone mapping, Gamma校正, 写入文件...
    }
};
```

**重建滤波器**（我的对比）：

```cpp
// Box滤波：最快但质量差
Float BoxFilter(Vector2 p, Float radius) {
    return 1.0;  // 常数权重
}

// Gaussian：平滑但可能过度模糊
Float GaussianFilter(Vector2 p, Float alpha) {
    return exp(-alpha * p.x * p.x) * exp(-alpha * p.y * p.y);
}

// Mitchell-Netravali：平衡锐度和平滑
Float MitchellFilter(Vector2 p, Float B, Float C) {
    // B=1/3, C=1/3是推荐值
    // 分段三次函数，兼顾锐利和平滑
}
```

---

## Chapter 6: Shapes

### 我的理解

**Shape是光线追踪中的几何基元**：定义表面在世界空间的位置和相交算法。

### 6.1 Shape接口

**我的核心接口设计**：

```cpp
class Shape {
public:
    // 1. 包围盒（加速结构必需）
    virtual Bounds3f Bounds() const = 0;

    // 2. 光线相交测试（核心）
    virtual bool Intersect(const Ray& ray,
                          Float* tHit,
                          SurfaceInteraction* si) const = 0;

    // 3. 快速相交测试（阴影光线）
    virtual bool IntersectP(const Ray& ray) const = 0;

    // 4. 表面积（面光源需要）
    virtual Float Area() const = 0;

    // 5. 表面采样（直接光照）
    virtual Interaction Sample(const Point2f& u, Float* pdf) const = 0;

    // 6. 从点采样（用于重要性采样）
    virtual Interaction Sample(const Interaction& ref,
                              const Point2f& u,
                              Float* pdf) const = 0;

    // 变换
    const Transform* ObjectToWorld;
    const Transform* WorldToObject;
};
```

### 6.2 球体（Sphere）

**我的完整实现**（最经典的Shape）：

```cpp
class Sphere : public Shape {
    Float radius;
    Float zMin, zMax;      // 部分球体
    Float thetaMin, thetaMax, phiMax;

    bool Intersect(const Ray& r, Float* tHit, SurfaceInteraction* si) const {
        // 1. 变换光线到物体空间
        Ray ray = (*WorldToObject)(r);

        // 2. 求解二次方程 |o + td|² = r²
        Float a = ray.d.x * ray.d.x + ray.d.y * ray.d.y + ray.d.z * ray.d.z;
        Float b = 2 * (ray.d.x * ray.o.x + ray.d.y * ray.o.y + ray.d.z * ray.o.z);
        Float c = ray.o.x * ray.o.x + ray.o.y * ray.o.y + ray.o.z * ray.o.z
                  - radius * radius;

        Float t0, t1;
        if (!Quadratic(a, b, c, &t0, &t1))
            return false;

        // 3. 检查t范围
        if (t0 > ray.tMax || t1 <= 0)
            return false;

        Float tShapeHit = t0;
        if (tShapeHit <= 0) {
            tShapeHit = t1;
            if (tShapeHit > ray.tMax)
                return false;
        }

        // 4. 计算交点
        Point3f pHit = ray(tShapeHit);

        // 5. 处理浮点误差（避免pHit正好在球面上）
        pHit *= radius / Distance(pHit, Point3f(0, 0, 0));

        // 6. 计算参数化坐标(u,v)
        Float phi = std::atan2(pHit.y, pHit.x);
        if (phi < 0) phi += 2 * Pi;
        Float theta = std::acos(Clamp(pHit.z / radius, -1, 1));

        // 7. 计算偏导数 dp/du, dp/dv（用于法线和切线）
        Float zRadius = std::sqrt(pHit.x * pHit.x + pHit.y * pHit.y);
        Float invZRadius = 1 / zRadius;
        Float cosPhi = pHit.x * invZRadius;
        Float sinPhi = pHit.y * invZRadius;

        Vector3f dpdu(-phiMax * pHit.y, phiMax * pHit.x, 0);
        Vector3f dpdv = (thetaMax - thetaMin) *
                        Vector3f(pHit.z * cosPhi, pHit.z * sinPhi,
                                -radius * std::sin(theta));

        // 8. 填充SurfaceInteraction
        *si = (*ObjectToWorld)(SurfaceInteraction(
            pHit, Vector3f(0,0,0), Point2f(phi/phiMax, theta/thetaMax),
            -ray.d, dpdu, dpdv, Normal3f(0,0,0), Normal3f(0,0,0),
            ray.time, this));

        *tHit = tShapeHit;
        return true;
    }

    Float Area() const {
        // 部分球体表面积
        return phiMax * radius * (zMax - zMin);
    }

    Interaction Sample(const Point2f& u, Float* pdf) const {
        // 均匀采样球面
        Point3f pObj = Point3f(0, 0, 0) + radius * UniformSampleSphere(u);
        Interaction it;
        it.n = Normalize((*ObjectToWorld)(Normal3f(pObj.x, pObj.y, pObj.z)));
        pObj *= radius / Distance(pObj, Point3f(0, 0, 0));  // 误差修正
        it.p = (*ObjectToWorld)(pObj, Vector3f(0,0,0), &it.pError);
        *pdf = 1 / Area();
        return it;
    }
};
```

**我的球体相交推导**：

```
光线：r(t) = o + td
球面：|p|² = R²

代入：|o + td|² = R²
展开：(o + td)·(o + td) = R²
     o·o + 2t(o·d) + t²(d·d) = R²

整理成标准二次方程：
at² + bt + c = 0

其中：
a = d·d
b = 2(o·d)
c = o·o - R²

判别式：Δ = b² - 4ac
t = (-b ± √Δ) / 2a

取较小的正根作为交点
```

### 6.3 三角网格（Triangle Mesh）

**我的Möller-Trumbore算法实现**（最高效的三角形相交算法）：

```cpp
class Triangle : public Shape {
    const TriangleMesh* mesh;  // 共享顶点数据
    int v[3];                   // 顶点索引

    bool Intersect(const Ray& ray, Float* tHit, SurfaceInteraction* si) const {
        // 获取三角形顶点
        const Point3f& p0 = mesh->p[v[0]];
        const Point3f& p1 = mesh->p[v[1]];
        const Point3f& p2 = mesh->p[v[2]];

        // Möller-Trumbore算法（无需预计算）
        Vector3f e1 = p1 - p0;
        Vector3f e2 = p2 - p0;
        Vector3f s = ray.o - p0;

        Vector3f s1 = Cross(ray.d, e2);
        Vector3f s2 = Cross(s, e1);

        Float invDivisor = 1.0f / Dot(s1, e1);
        Float t = Dot(s2, e2) * invDivisor;
        Float b1 = Dot(s1, s) * invDivisor;   // 重心坐标u
        Float b2 = Dot(s2, ray.d) * invDivisor; // 重心坐标v

        // 检查相交条件
        if (t < 0 || t > ray.tMax)
            return false;
        if (b1 < 0 || b1 > 1)
            return false;
        if (b2 < 0 || b1 + b2 > 1)
            return false;

        // 计算重心坐标
        Float b0 = 1 - b1 - b2;

        // 插值UV坐标
        Point2f uv = b0 * mesh->uv[v[0]]
                   + b1 * mesh->uv[v[1]]
                   + b2 * mesh->uv[v[2]];

        // 插值或计算法线
        Normal3f n;
        if (mesh->n) {
            n = Normalize(b0 * mesh->n[v[0]]
                        + b1 * mesh->n[v[1]]
                        + b2 * mesh->n[v[2]]);
        } else {
            n = Normalize(Normal3f(Cross(e1, e2)));
        }

        // 计算偏导数（用于纹理映射）
        Vector3f dpdu, dpdv;
        ComputeTrianglePartials(p0, p1, p2, mesh->uv[v[0]],
                               mesh->uv[v[1]], mesh->uv[v[2]],
                               &dpdu, &dpdv);

        *si = SurfaceInteraction(p0 + b1*e1 + b2*e2, Vector3f(0,0,0),
                                uv, -ray.d, dpdu, dpdv,
                                Normal3f(0,0,0), Normal3f(0,0,0),
                                ray.time, this);
        si->n = si->shading.n = n;

        *tHit = t;
        return true;
    }
};
```

**Möller-Trumbore推导**（我的理解）：

```
三角形顶点：p0, p1, p2
重心坐标：p = p0 + u(p1-p0) + v(p2-p0), u≥0, v≥0, u+v≤1
光线：r = o + td

联立：
o + td = p0 + u·e1 + v·e2  (e1=p1-p0, e2=p2-p0)

整理成矩阵形式：
[-d, e1, e2] [t]   [o - p0]
             [u] =
             [v]

使用Cramer法则求解，避免矩阵求逆：
t = det(s, e1, e2) / det(-d, e1, e2)
u = det(-d, s, e2) / det(-d, e1, e2)
v = det(-d, e1, s) / det(-d, e1, e2)

利用混合积性质：det(a,b,c) = a·(b×c)
→ 最终得到高效的向量叉乘形式
```

### 6.4 浮点误差处理

**我的误差处理策略**（PBRT4的关键创新）：

```cpp
// 1. 保守误差估计
Vector3f pError = gamma(5) * Abs(pHit);

// 2. 偏移起点避免自相交
Point3f OffsetRayOrigin(const Point3f& p, const Vector3f& pError,
                        const Normal3f& n, const Vector3f& w) {
    Float d = Dot(Abs(n), pError);
    Vector3f offset = d * Vector3f(n);
    if (Dot(w, n) < 0)
        offset = -offset;
    Point3f po = p + offset;

    // 确保偏移量足够（针对极端情况）
    for (int i = 0; i < 3; ++i) {
        if (offset[i] > 0)      po[i] = NextFloatUp(po[i]);
        else if (offset[i] < 0) po[i] = NextFloatDown(po[i]);
    }
    return po;
}
```

**误差来源**（我的总结）：

```
1. 光线-表面相交计算误差
   → pHit可能略微偏离真实表面
   → 可能在表面上方或下方

2. 后续光线从pHit出发
   → 如果在表面下方：错误地与自身相交
   → 产生阴影粉刺（shadow acne）

3. 解决方案：
   - 计算误差界：γ(n) = nε / (1 - nε)，ε为机器精度
   - 沿法线偏移起点：确保在表面正确一侧
   - 使用NextFloatUp/Down确保数值上越过边界
```

### 6.5 其他形状

**圆柱体相交**（我的理解）：

```cpp
bool Cylinder::Intersect(const Ray& ray, Float* tHit, SurfaceInteraction* si) {
    // 1. 忽略z分量，在xy平面求交
    //    圆柱方程：x² + y² = r²
    Float a = ray.d.x * ray.d.x + ray.d.y * ray.d.y;
    Float b = 2 * (ray.d.x * ray.o.x + ray.d.y * ray.o.y);
    Float c = ray.o.x * ray.o.x + ray.o.y * ray.o.y - radius * radius;

    Float t0, t1;
    if (!Quadratic(a, b, c, &t0, &t1))
        return false;

    // 2. 检查z范围 [zMin, zMax]
    Float z0 = ray.o.z + t0 * ray.d.z;
    Float z1 = ray.o.z + t1 * ray.d.z;
    if (z0 < zMin || z0 > zMax) t0 = t1;
    if (z1 < zMin || z1 > zMax) return false;

    // 3. 计算参数化坐标和偏导数
    // φ = atan2(y, x), u = φ/φ_max, v = (z-zMin)/(zMax-zMin)
    // ...
}
```

**曲线（Curve）**（毛发渲染）：

```
- 使用Bézier曲线段
- 光线与曲线段相交
- 用于头发、草、电缆等细长物体
- 采用特殊的散射模型（见Ch9毛发BSDF）
```

---

## Chapter 7: Primitives and Intersection Acceleration

### 我的理解

**Primitive = Shape + Material + Light + Medium**，是渲染器的完整几何对象。
**加速结构**：将O(N)场景遍历优化到O(logN)，是光线追踪性能的关键。

### 7.1 Primitive系统

**我的接口设计**：

```cpp
class Primitive {
public:
    // 光线相交（完整信息）
    virtual bool Intersect(const Ray& r, SurfaceInteraction* si) const = 0;

    // 快速相交测试（阴影光线，只需bool）
    virtual bool IntersectP(const Ray& r) const = 0;

    // 包围盒
    virtual Bounds3f WorldBound() const = 0;

    // 面光源（如果是发光物体）
    virtual const AreaLight* GetAreaLight() const = 0;

    // 材质
    virtual const Material* GetMaterial() const = 0;

    // 介质（体积渲染）
    virtual const Medium* GetMedium() const = 0;
};
```

**GeometricPrimitive实现**（我的完整代码）：

```cpp
class GeometricPrimitive : public Primitive {
    std::shared_ptr<Shape> shape;
    std::shared_ptr<Material> material;
    std::shared_ptr<AreaLight> areaLight;
    MediumInterface mediumInterface;

    bool Intersect(const Ray& r, SurfaceInteraction* si) const override {
        Float tHit;
        if (!shape->Intersect(r, &tHit, si))
            return false;

        r.tMax = tHit;
        si->primitive = this;

        // 初始化材质和介质接口
        if (mediumInterface.IsMediumTransition())
            si->mediumInterface = mediumInterface;
        else
            si->mediumInterface = MediumInterface(r.medium);

        return true;
    }

    bool IntersectP(const Ray& r) const override {
        return shape->IntersectP(r);
    }

    Bounds3f WorldBound() const override {
        return shape->Bounds();
    }

    const AreaLight* GetAreaLight() const override {
        return areaLight.get();
    }

    const Material* GetMaterial() const override {
        return material.get();
    }
};
```

### 7.2 BVH加速结构（Bounding Volume Hierarchy）

**我的BVH原理理解**：

```
核心思想：
1. 将场景物体递归分组到包围盒层次结构中
2. 光线先测试父节点，如果不相交则跳过所有子节点
3. 大量剔除不必要的相交测试

示例场景（8个物体）：
                [Root: Bounds(all)]
                /                  \
        [Left: Bounds(0-3)]    [Right: Bounds(4-7)]
         /           \             /            \
    [Obj0,1]    [Obj2,3]      [Obj4,5]     [Obj6,7]
      /  \        /  \          /  \         /  \
   Obj0 Obj1  Obj2 Obj3     Obj4 Obj5    Obj6 Obj7

遍历复杂度：
- 无加速：O(N) = 8次相交测试
- 有BVH：O(logN) = 平均2-3个节点测试 + 1-2个物体测试
```

**我的BVH节点实现**：

```cpp
struct BVHBuildNode {
    Bounds3f bounds;
    BVHBuildNode* children[2];
    int splitAxis;        // 分割轴（0=x, 1=y, 2=z）
    int firstPrimOffset;  // 叶节点：第一个图元索引
    int nPrimitives;      // 叶节点：图元数量

    void InitLeaf(int first, int n, const Bounds3f& b) {
        firstPrimOffset = first;
        nPrimitives = n;
        bounds = b;
        children[0] = children[1] = nullptr;
    }

    void InitInterior(int axis, BVHBuildNode* c0, BVHBuildNode* c1) {
        children[0] = c0;
        children[1] = c1;
        bounds = Union(c0->bounds, c1->bounds);
        splitAxis = axis;
        nPrimitives = 0;  // 内部节点标记
    }
};
```

### 7.3 SAH构建算法（Surface Area Heuristic）

**我的SAH推导**（PBRT4核心算法）：

```
成本模型：
C(A, B) = t_traverse + p_A * C(A) + p_B * C(B)

其中：
- t_traverse：遍历节点成本（常数）
- p_A = SA(A) / SA(parent)：光线击中A的概率
- SA(A)：A的表面积
- C(A)：遍历A的成本

叶节点成本：
C_leaf = n * t_intersect

分割决策：
找到最优分割位置，使得总成本最小
→ 遍历所有可能的分割点，计算成本，选择最小值
```

**我的SAH实现**：

```cpp
struct BucketInfo {
    int count = 0;          // 该区间的图元数量
    Bounds3f bounds;        // 该区间的包围盒
};

BVHBuildNode* BVHAccel::BuildRecursive(
    std::vector<BVHPrimitiveInfo>& primitiveInfo,
    int start, int end,
    int* totalNodes,
    std::vector<std::shared_ptr<Primitive>>& orderedPrims) {

    BVHBuildNode* node = new BVHBuildNode;
    (*totalNodes)++;

    // 1. 计算所有图元的包围盒
    Bounds3f bounds;
    for (int i = start; i < end; i++)
        bounds = Union(bounds, primitiveInfo[i].bounds);

    int nPrimitives = end - start;

    // 2. 叶节点条件
    if (nPrimitives <= maxPrimsInNode) {
        // 创建叶节点
        int firstPrimOffset = orderedPrims.size();
        for (int i = start; i < end; i++) {
            int primNum = primitiveInfo[i].primitiveNumber;
            orderedPrims.push_back(primitives[primNum]);
        }
        node->InitLeaf(firstPrimOffset, nPrimitives, bounds);
        return node;
    }

    // 3. 内部节点：选择分割轴和位置
    Bounds3f centroidBounds;
    for (int i = start; i < end; i++)
        centroidBounds = Union(centroidBounds, primitiveInfo[i].centroid);

    int dim = centroidBounds.MaximumExtent();  // 最长轴

    // 4. 退化情况：所有质心重合
    if (centroidBounds.pMax[dim] == centroidBounds.pMin[dim]) {
        // 无法分割，创建叶节点
        // ...（同上）
    }

    // 5. SAH分割
    const int nBuckets = 12;
    BucketInfo buckets[nBuckets];

    // 将图元分配到桶中
    for (int i = start; i < end; i++) {
        int b = nBuckets * centroidBounds.Offset(
            primitiveInfo[i].centroid)[dim];
        if (b == nBuckets) b = nBuckets - 1;
        buckets[b].count++;
        buckets[b].bounds = Union(buckets[b].bounds,
                                 primitiveInfo[i].bounds);
    }

    // 计算每个分割位置的成本
    Float cost[nBuckets - 1];
    for (int i = 0; i < nBuckets - 1; i++) {
        Bounds3f b0, b1;
        int count0 = 0, count1 = 0;

        // 左侧：[0, i]
        for (int j = 0; j <= i; j++) {
            b0 = Union(b0, buckets[j].bounds);
            count0 += buckets[j].count;
        }

        // 右侧：[i+1, nBuckets-1]
        for (int j = i + 1; j < nBuckets; j++) {
            b1 = Union(b1, buckets[j].bounds);
            count1 += buckets[j].count;
        }

        // SAH成本
        cost[i] = 1 + // 遍历成本
                  (count0 * b0.SurfaceArea() +
                   count1 * b1.SurfaceArea()) /
                  bounds.SurfaceArea();
    }

    // 找到最小成本
    Float minCost = cost[0];
    int minCostSplitBucket = 0;
    for (int i = 1; i < nBuckets - 1; i++) {
        if (cost[i] < minCost) {
            minCost = cost[i];
            minCostSplitBucket = i;
        }
    }

    // 6. 决定是否创建叶节点
    Float leafCost = nPrimitives;
    if (nPrimitives > maxPrimsInNode || minCost < leafCost) {
        // 创建内部节点，按选定的桶分割
        BVHPrimitiveInfo* pmid = std::partition(
            &primitiveInfo[start], &primitiveInfo[end - 1] + 1,
            [=](const BVHPrimitiveInfo& pi) {
                int b = nBuckets * centroidBounds.Offset(pi.centroid)[dim];
                if (b == nBuckets) b = nBuckets - 1;
                return b <= minCostSplitBucket;
            });
        int mid = pmid - &primitiveInfo[0];

        // 递归构建子树
        node->InitInterior(dim,
            BuildRecursive(primitiveInfo, start, mid, totalNodes, orderedPrims),
            BuildRecursive(primitiveInfo, mid, end, totalNodes, orderedPrims));
    } else {
        // 创建叶节点
        // ...
    }

    return node;
}
```

### 7.4 BVH遍历

**我的遍历实现**（深度优先）：

```cpp
bool BVHAccel::Intersect(const Ray& ray, SurfaceInteraction* si) const {
    if (!nodes) return false;

    bool hit = false;
    Vector3f invDir(1 / ray.d.x, 1 / ray.d.y, 1 / ray.d.z);
    int dirIsNeg[3] = {invDir.x < 0, invDir.y < 0, invDir.z < 0};

    // 遍历栈（避免递归）
    int toVisitOffset = 0, currentNodeIndex = 0;
    int nodesToVisit[64];

    while (true) {
        const LinearBVHNode* node = &nodes[currentNodeIndex];

        // 1. 检查与节点包围盒相交
        if (node->bounds.IntersectP(ray, invDir, dirIsNeg)) {
            if (node->nPrimitives > 0) {
                // 2. 叶节点：测试所有图元
                for (int i = 0; i < node->nPrimitives; i++) {
                    if (primitives[node->primitivesOffset + i]->Intersect(ray, si))
                        hit = true;
                }

                // 栈回退
                if (toVisitOffset == 0) break;
                currentNodeIndex = nodesToVisit[--toVisitOffset];
            } else {
                // 3. 内部节点：选择遍历顺序
                if (dirIsNeg[node->axis]) {
                    nodesToVisit[toVisitOffset++] = currentNodeIndex + 1;
                    currentNodeIndex = node->secondChildOffset;
                } else {
                    nodesToVisit[toVisitOffset++] = node->secondChildOffset;
                    currentNodeIndex = currentNodeIndex + 1;
                }
            }
        } else {
            // 不相交，栈回退
            if (toVisitOffset == 0) break;
            currentNodeIndex = nodesToVisit[--toVisitOffset];
        }
    }

    return hit;
}
```

**优化技巧**（我的总结）：

```
1. 紧凑内存布局：
   - LinearBVHNode：32字节（缓存友好）
   - 左子节点紧跟父节点（currentNodeIndex + 1）
   - 右子节点存储偏移

2. 遍历顺序优化：
   - 先访问光线方向的近端子节点
   - 提高提前退出的概率

3. SIMD包围盒测试：
   - 并行测试多个轴的区间
   - 使用SSE/AVX指令

4. 光线相交统计：
   - 平均相交测试次数：15-30（无BVH为N）
   - 百万三角形场景：~20次测试
```

### 7.5 其他加速结构

**KD-Tree vs BVH**（我的对比）：

| 特性 | **BVH** | **KD-Tree** |
|------|---------|-------------|
| **构建复杂度** | O(N logN) | O(N logN) |
| **内存** | 更大（重叠包围盒） | 更小（严格分割） |
| **动态场景** | ✅ 易于更新 | ❌ 需重建 |
| **构建速度** | ✅ 更快 | ❌ 更慢 |
| **遍历效率** | ⚠️ 可能遍历重叠区域 | ✅ 无重叠 |
| **现代趋势** | ✅ 主流选择 | ⚠️ 较少使用 |

**GPU光线追踪**（我的理解）：

```
现代GPU API（DXR/Vulkan RT）：
- BLAS（Bottom-Level Acceleration Structure）：
  → 单个模型的BVH
  → GPU硬件加速构建和遍历

- TLAS（Top-Level Acceleration Structure）：
  → 场景实例的BVH
  → 支持变换和动画

优势：
- 硬件RT核心（Tensor Cores）
- 每秒数十亿条光线
- 比CPU软件BVH快100-1000倍
```

---

## Chapter 8: Sampling and Reconstruction

### 我的理解

**采样是蒙特卡洛渲染的基础**：如何在高维积分空间高效采样，决定渲染质量和速度。

### 8.1 采样理论

**我的奈奎斯特定理理解**：

```
采样定理（Shannon-Nyquist）：
要完美重建信号，采样率必须≥2倍最高频率

f_sample ≥ 2 * f_max

否则产生走样（Aliasing）：
- 高频信号被误认为低频信号
- 无法从采样值恢复原始信号

示例：
信号频率：10Hz
采样率：15Hz（< 2×10）❌ 走样
采样率：25Hz（≥ 2×10）✅ 可重建
```

**走样类型**（我的总结）：

```
1. 几何走样（Geometric Aliasing）：
   - 现象：边缘锯齿（jaggies）
   - 原因：三角形边缘是无限高频
   - 解决：超采样或预滤波

2. 着色走样（Shading Aliasing）：
   - 现象：高频纹理或高光闪烁
   - 原因：纹理频率高于采样率
   - 解决：Mipmap、各向异性过滤

3. 时间走样（Temporal Aliasing）：
   - 现象：旋转轮子反向、闪烁
   - 原因：运动快于帧率
   - 解决：运动模糊（时间采样）
```

### 8.2 采样器（Sampler）

**我的采样器接口**：

```cpp
class Sampler {
public:
    // 当前样本的维度值
    virtual Float Get1D() = 0;
    virtual Point2f Get2D() = 0;

    // 相机样本
    virtual CameraSample GetCameraSample(const Point2i& pRaster) {
        CameraSample cs;
        cs.pFilm = (Point2f)pRaster + Get2D();
        cs.time = Get1D();
        cs.pLens = Get2D();
        return cs;
    }

    // 开始新像素
    virtual void StartPixel(const Point2i& p) = 0;

    // 生成下一个样本
    virtual bool StartNextSample() = 0;

    // 每像素样本数
    virtual int SamplesPerPixel() const = 0;

    // 克隆（线程安全）
    virtual std::unique_ptr<Sampler> Clone(int seed) = 0;
};
```

### 8.3 采样器类型对比

**1. 独立采样器（Independent Sampler）**

```cpp
class IndependentSampler : public Sampler {
    std::mt19937 rng;

    Float Get1D() override {
        std::uniform_real_distribution<Float> dist(0, 1);
        return dist(rng);
    }

    Point2f Get2D() override {
        return Point2f(Get1D(), Get1D());
    }
};
```

**优缺点**：
```
✅ 简单、快速
✅ 无结构化伪影
❌ 高方差（噪声重）
❌ 收敛慢（需要更多样本）
❌ 可能产生样本聚集
```

**2. 分层采样器（Stratified Sampler）**

```cpp
class StratifiedSampler : public Sampler {
    int xSamples, ySamples;  // 分层数
    bool jitter;

    void StartPixel(const Point2i& p) override {
        // 为像素生成分层样本
        for (int y = 0; y < ySamples; y++) {
            for (int x = 0; x < xSamples; x++) {
                Float dx = jitter ? rng.UniformFloat() : 0.5f;
                Float dy = jitter ? rng.UniformFloat() : 0.5f;

                samples2D.push_back(Point2f(
                    (x + dx) / xSamples,
                    (y + dy) / ySamples
                ));
            }
        }

        // 打乱顺序（Latin Hypercube）
        Shuffle(samples2D.begin(), samples2D.end(), rng);
    }
};
```

**分层原理**（我的理解）：

```
将采样域分成N×M个格子，每个格子采一个样本

示例：4×4分层 = 16样本
[0]  [1]  [2]  [3]
[4]  [5]  [6]  [7]
[8]  [9]  [10] [11]
[12] [13] [14] [15]

优势：
- 保证均匀覆盖
- 降低聚集风险
- 比独立采样方差更低

限制：
- 高维空间难以分层（维度诅咒）
- 样本数必须是N²
```

**3. 低差异序列（Low-Discrepancy Sequence）**

**Halton序列实现**（我的代码）：

```cpp
Float RadicalInverse(int n, int base) {
    Float invBase = (Float)1 / base;
    Float invBi = invBase;
    Float result = 0;

    while (n > 0) {
        int digit = n % base;
        result += digit * invBi;
        n /= base;
        invBi *= invBase;
    }

    return result;
}

Point2f HaltonSample(int index) {
    return Point2f(
        RadicalInverse(index, 2),   // base 2
        RadicalInverse(index, 3)    // base 3
    );
}

class HaltonSampler : public Sampler {
    int sampleIndex;

    void StartPixel(const Point2i& p) override {
        // 计算全局样本索引
        sampleIndex = p.x + p.y * imageWidth;
    }

    Point2f Get2D() override {
        Point2f sample = HaltonSample(sampleIndex);
        sampleIndex++;
        return sample;
    }
};
```

**Halton序列推导**（我的理解）：

```
Van der Corput序列（1维）：
将索引n的二进制反转，作为小数

n=0: 0   → 0.0
n=1: 1   → 0.1   = 0.5
n=2: 10  → 0.01  = 0.25
n=3: 11  → 0.11  = 0.75
n=4: 100 → 0.001 = 0.125
...

Halton序列（2维）：
x = VanDerCorput(n, base=2)
y = VanDerCorput(n, base=3)

前16个样本的可视化：
（完美均匀分布，无聚集）
```

**Sobol序列**（我的理解）：

```cpp
// Sobol序列使用Gray码和方向数
// 更高效的生成算法，更好的高维性质

class SobolSampler : public Sampler {
    uint32_t sobolIndex;
    uint32_t dimension;

    Float SobolSample(uint32_t index, uint32_t dim) {
        uint32_t result = 0;
        uint32_t i = index;
        for (int bit = 0; i; i >>= 1, bit++) {
            if (i & 1)
                result ^= SobolDirectionNumbers[dim][bit];
        }
        return result * 2.3283064365386963e-10f;  // / 2^32
    }

    Float Get1D() override {
        Float sample = SobolSample(sobolIndex, dimension);
        dimension++;
        return sample;
    }
};
```

**低差异序列优势**（我的总结）：

```
差异度（Discrepancy）：
衡量样本分布的均匀程度

D_N = max_B |实际样本数/N - 体积(B)|

随机采样：D_N = O(√(loglogN / N))
低差异序列：D_N = O((logN)^d / N)  ⭐ 更快收敛

视觉效果：
- 独立采样：明显噪声，需4096 spp
- Halton/Sobol：平滑噪声，256 spp即可
- 收敛速度提升10-20倍
```

### 8.4 图像重建

**我的重建滤波器实现**：

```cpp
// 1. Box滤波（最简单）
class BoxFilter : public Filter {
    Float radius;

    Float Evaluate(const Point2f& p) const override {
        return 1.0f;  // 常数权重
    }
};

// 2. Triangle滤波（帐篷滤波）
class TriangleFilter : public Filter {
    Float Evaluate(const Point2f& p) const override {
        return std::max(0.f, radius - std::abs(p.x)) *
               std::max(0.f, radius - std::abs(p.y));
    }
};

// 3. Gaussian滤波
class GaussianFilter : public Filter {
    Float alpha;  // 控制宽度
    Float expX, expY;  // 预计算的指数

    Float Evaluate(const Point2f& p) const override {
        return Gaussian(p.x, expX) * Gaussian(p.y, expY);
    }

    Float Gaussian(Float d, Float expv) const {
        return std::max(0.f, std::exp(-alpha * d * d) - expv);
    }
};

// 4. Mitchell-Netravali滤波（推荐）⭐
class MitchellFilter : public Filter {
    Float B, C;  // B=C=1/3是推荐值

    Float Evaluate(const Point2f& p) const override {
        return Mitchell1D(p.x * invRadius.x) *
               Mitchell1D(p.y * invRadius.y);
    }

    Float Mitchell1D(Float x) const {
        x = std::abs(2 * x);
        if (x > 1)
            return ((-B - 6*C) * x*x*x + (6*B + 30*C) * x*x +
                    (-12*B - 48*C) * x + (8*B + 24*C)) * (1.f/6.f);
        else
            return ((12 - 9*B - 6*C) * x*x*x +
                    (-18 + 12*B + 6*C) * x*x +
                    (6 - 2*B)) * (1.f/6.f);
    }
};
```

**滤波器对比**（我的实验总结）：

| 滤波器 | 半径 | 锐度 | 振铃 | 性能 | 适用场景 |
|--------|------|------|------|------|----------|
| **Box** | 0.5 | 低 | 无 | 最快 | 预览 |
| **Triangle** | 1.0 | 中 | 无 | 快 | 通用 |
| **Gaussian** | 2.0 | 低 | 无 | 中 | 平滑画面 |
| **Mitchell** | 2.0 | 高 | 轻微 | 中 | 最终渲染⭐ |
| **Lanczos** | 3.0 | 最高 | 明显 | 慢 | 锐利细节 |

**重建过程**（我的完整代码）：

```cpp
void Film::AddSample(Point2f pFilm, Spectrum L, Float sampleWeight) {
    // 1. 计算影响的像素范围
    Point2f pFilmDiscrete = pFilm - Vector2f(0.5f, 0.5f);
    Point2i p0 = (Point2i)Ceil(pFilmDiscrete - filter->radius);
    Point2i p1 = (Point2i)Floor(pFilmDiscrete + filter->radius) + Point2i(1, 1);
    p0 = Max(p0, Point2i(0, 0));
    p1 = Min(p1, Point2i(resolution.x, resolution.y));

    // 2. 预计算滤波器表查找
    int* ifx = new int[p1.x - p0.x];
    for (int x = p0.x; x < p1.x; x++) {
        Float fx = std::abs((x - pFilmDiscrete.x) * filterTable->invFilterWidth);
        ifx[x - p0.x] = std::min((int)std::floor(fx), filterTable->width - 1);
    }

    int* ify = new int[p1.y - p0.y];
    for (int y = p0.y; y < p1.y; y++) {
        Float fy = std::abs((y - pFilmDiscrete.y) * filterTable->invFilterWidth);
        ify[y - p0.y] = std::min((int)std::floor(fy), filterTable->width - 1);
    }

    // 3. 对每个受影响的像素
    for (int y = p0.y; y < p1.y; y++) {
        for (int x = p0.x; x < p1.x; x++) {
            // 查表获取滤波器权重
            int offset = ify[y - p0.y] * filterTable->width + ifx[x - p0.x];
            Float filterWeight = filterTable->table[offset];

            // 累积加权样本
            Pixel& pixel = pixels[(y * resolution.x + x)];
            for (int c = 0; c < 3; c++)
                pixel.rgbSum[c] += L[c] * sampleWeight * filterWeight;
            pixel.weightSum += sampleWeight * filterWeight;
        }
    }

    delete[] ifx;
    delete[] ify;
}

void Film::WriteImage() {
    // 归一化并应用Tone Mapping
    for (int y = 0; y < resolution.y; y++) {
        for (int x = 0; x < resolution.x; x++) {
            Pixel& pixel = pixels[y * resolution.x + x];

            // 归一化
            Float invWeight = 1.0f / pixel.weightSum;
            Float rgb[3];
            for (int c = 0; c < 3; c++)
                rgb[c] = pixel.rgbSum[c] * invWeight;

            // Tone Mapping（可选）
            // rgb = ToneMap(rgb);

            // Gamma校正
            for (int c = 0; c < 3; c++)
                rgb[c] = std::pow(rgb[c], 1.0f / 2.2f);

            // 写入图像
            // ...
        }
    }
}
```

### 8.5 采样模式（Sampling Patterns）

**我的重要性采样理解**（见Ch13-14详细内容）：

```
核心思想：
根据被积函数的分布采样，而非均匀采样

∫ f(x) dx ≈ (1/N) Σ f(x_i) / p(x_i)

其中p(x)是采样PDF

如果p(x) ∝ f(x)：
→ 方差最小
→ 收敛最快

示例：余弦加权半球采样
p(ω) = cosθ / π  （匹配Lambert BRDF）
```

**采样技巧**（我的总结）：

```
1. 反演法（Inversion Method）：
   CDF^(-1)(ξ) → sample

2. 拒绝采样（Rejection Sampling）：
   生成样本，检查是否接受

3. 多重重要性采样（MIS）：
   组合多个采样策略
   w_i = (n_i * p_i)^β / Σ(n_j * p_j)^β
   β=2（balance heuristic）或β=1（power heuristic）
```

---

## Chapter 9: Reflection Models

### 核心抽象

**三大散射函数**：
- BRDF：双向反射分布函数（反射）
- BTDF：双向透射分布函数（透射）
- BSDF：双向散射分布函数（反射+透射）

### 反射模型来源

五种生成方式：
1. 实验室测量数据
2. 现象学模型（粗糙度等参数）
3. 微结构行为模拟
4. 物理波动光学
5. 几何光学推导

### 反射类型

| 类型 | 特征 |
|------|------|
| **漫反射** | 各方向均匀散射 |
| **光泽镜面** | 模糊反射，有主方向 |
| **完美镜面** | 单一出射方向（镜子、玻璃） |
| **回射反射** | 主要后向散射 |

### 材质属性

- 各向同性：反射与表面旋转无关
- 各向异性：方向依赖（毛发、布料、拉丝金属）

### 主要模型

**微表面理论**：
- 表面由微小平面组成
- 粗糙度控制微平面分布
- 用于光泽和粗糙表面

**导体BRDF**：
- 金属材质
- 菲涅尔反射
- 能量全部反射

**电介质BSDF**：
- 玻璃、水等透明材质
- 同时反射和折射
- 菲涅尔方程决定反射/折射比例

**毛发散射**：
- 专门的圆柱形散射模型
- 考虑多次内部反射

---

## Chapter 10: Textures and Materials

### 核心概念

**Texture（纹理）**：
- 将域点（UV或XYZ）映射到输出值
- 可以是常量、2D图像、程序化函数

**Material（材质）**：
- 在表面点评估纹理
- 确定BSDF参数
- 分离图案生成和反射模型

### 关键问题：纹理走样

**原因**：
- 高频纹理变化
- 采样率不匹配纹理频率

**解决方案**：
- 纹理函数根据采样率调整频率内容
- 预滤波移除高频细节
- 而非增加图像采样数

**抗锯齿方法**：
- Mipmap层级选择
- 各向异性过滤
- 基于采样率的自适应滤波

### 纹理系统

**纹理接口**：
- FloatTexture：实数纹理
- SpectrumTexture：光谱纹理

**图像纹理**：
- 支持多种格式
- Mipmap金字塔
- 纹理坐标生成

**材质实现**：
- 组合纹理和反射模型
- 灵活的表面外观

---

## Chapter 11: Volume Scattering

### 核心概念

**参与介质**：
- 雾、烟、云、浑浊水
- 固体内部的次表面散射

### 体积散射过程

**物理过程**：
- 吸收：能量转化为热
- 外散射：光线偏离原方向
- 内散射：其他方向光线散射到当前方向
- 发射：介质自身发光

### 关键量

**透射率（Transmittance）**：
- 光在介质中的衰减
- 指数衰减规律

**相位函数（Phase Function）**：
- 体积散射的"BRDF"
- 描述散射方向分布
- 常用：各向同性、Henyey-Greenstein

### Medium接口

**职责**：
- 提供散射特性
- 支持零散射（Null Scattering）
- 处理非均质介质

**应用**：
- 大气效果
- 光束（god rays）
- 次表面散射

---

## Chapter 12: Light Sources

### 核心设计

**Light接口**：
- 统一的光源抽象
- 支持多种光源类型
- 保持接口一致性

**物理基础原则**：
- 能量守恒：表面接收能量≤光源发射能量
- 排除非物理模型（如无阴影光源）

### 光源类型

**点光源**：
- 从单点向所有方向发射
- 与距离平方成反比衰减

**方向光**：
- 模拟太阳等远距离光源
- 平行光线

**区域光**：
- 有形状的发光表面
- 产生柔和阴影

**无限区域光**：
- 环境贴图
- 360度照明

### LightSampler接口

**作用**：
- 多光源场景的高效采样
- 通过权重因子选择光源
- 保持无偏估计

**优化**：
- 重要性采样光源
- 减少不重要光源的计算

---

## Chapter 13: Light Transport I: Surface Reflection

### 光传输方程

**渲染方程**：
积分形式描述表面点的辐射亮度，考虑：
- 自发光
- 半球上所有方向的入射光
- BRDF散射

### 路径追踪算法

**核心思想**：
- 从相机发射光线
- 递归追踪反弹
- 蒙特卡洛积分求解

**关键技术**：
- 重要性采样BRDF
- 重要性采样光源
- 多重重要性采样（MIS）
- 俄罗斯轮盘赌终止

### 两种实现

**SimplePathIntegrator**：
- 精简实现
- 教学和调试用途
- 清晰展示算法结构

**PathIntegrator**：
- 完整优化实现
- 性能优化
- 生产级质量

**性能提升**：
- 相比早期方法降低数百倍误差
- 适用于复杂场景

---

## Chapter 14: Light Transport II: Volume Rendering

### 传输方程

**推广**：
- 将光传输方程扩展到参与介质
- 描述体积中辐射亮度平衡

**零散射**：
- 支持非均质介质
- 无偏采样积分
- 处理变化的散射属性

### 体积散射积分器

**两种求解器**：
- 基于蒙特卡洛积分
- 处理直接光照和多重散射
- 实现复杂体积效果

**渲染效果**：
- 体积雾
- 云层光照
- 烟雾模拟

### LayeredBxDF

**分层材质**：
- 一维传输方程特化
- 模拟分层表面
- 统一表面和体积散射

**应用**：
- 清漆涂层
- 多层材质
- 次表面散射简化

---

## Chapter 15: Wavefront Rendering on GPUs

### 波前架构

**核心设计**：
- 多光线同时处理
- 任务队列组织
- 收集相关任务批处理

**GPU友好**：
- 并行计算模式
- 避免线程分歧
- 最大化GPU利用率

### 硬件要求

**三大需求**：
1. 统一地址空间（CPU-GPU共享内存）
2. C++17兼容（代码复用）
3. 光线追踪支持（硬件或软件加速）

### 性能数据

**基准测试**（1500×1500，2048样本）：
- 高端GPU：318.6秒
- 8核CPU：11,983秒
- 32核CPU：2,669秒
- **GPU加速：37倍**（vs 8核CPU）

### 实现细节

**平台支持**：
- 当前仅NVIDIA CUDA
- 约2000行平台特定代码
- 处理内存管理和GPU启动

**渲染算法**：
- 统一的体积路径追踪
- 不支持所有CPU积分器特性

---

## Chapter 16: Retrospective and the Future

### pbrt演进历程

**四代发展**：
- v1-v3：纯CPU实现
- v4：首次支持GPU加速
- C++11 → C++17现代化
- 保持教学清晰性

### 设计选择

**架构原则**：
- 物理正确性优先
- 代码可读性
- 模块化设计
- 扩展性考虑

### 新兴话题

**前沿技术**：
- 神经渲染（Neural Rendering）
- AI去噪（AI Denoising）
- 实时光线追踪
- 混合渲染管线

**研究方向**：
- 更高效的采样算法
- 自适应渲染
- 机器学习加速
- 可微分渲染

### 未来展望

**技术趋势**：
- GPU算力持续增长
- 硬件光追普及
- 实时与离线融合
- AI辅助渲染

**pbrt的使命**：
- 继续作为教学工具
- 探索新算法
- 保持开源免费
- 推动技术进步

---

## Appendix A: Sampling Algorithms

### 核心采样方法

本附录补充第2章的蒙特卡洛积分，介绍额外的采样技术。

**三种方法**：
1. **别名方法（Alias Method）**：
   - 离散分布的高效采样
   - O(1)时间复杂度
   - 预处理构建别名表

2. **水塘采样（Reservoir Sampling）**：
   - 从流数据中随机采样
   - 内存效率高
   - 适用于未知总数的情况

3. **拒绝采样（Rejection Method）**：
   - 从复杂分布采样
   - 使用简单分布作为提议分布
   - 接受/拒绝策略

### 函数采样

**一维函数采样**：
- 扩展反演法
- 数值积分生成CDF
- 逆函数查找

**多维函数采样**：
- 边缘和条件分布
- 降维采样
- 保持采样效率

---

## Appendix B: Utilities

### 系统基础设施

**核心模块**：
- 数学基础：向量、矩阵运算
- 错误报告机制
- 内存管理工具
- 并行执行支持

**数学工具**：
- 浮点运算辅助
- 数值稳定性处理
- 常用数学函数

**并行化**：
- 多核CPU支持
- 线程池管理
- 任务调度

**内存管理**：
- 自定义分配器
- 内存池优化
- 智能指针

**统计系统**：
- 性能计数器
- 渲染统计
- 调试信息

---

## Appendix C: Processing the Scene Description

### 场景描述系统

**解析器**：
- 场景文件格式
- 词法和语法分析
- 对象实例化

**场景管理**：
- 场景图构建
- 对象组织
- 依赖关系处理

**扩展机制**：
- 添加新对象类型
- 插件系统
- 自定义命令

---

## 📝 阅读完成总结

**全书概览**：
- **16章主要内容**：从基础几何到GPU渲染的完整路径追踪系统
- **3个附录**：补充采样算法、工具库和场景处理
- **核心价值**：理论推导+完整C++实现，物理精确的离线渲染

**关键收获**：
1. 蒙特卡洛积分的深度理论（Ch2）
2. 完整的光传输方程推导（Ch13-14）
3. GPU波前渲染架构（Ch15）
4. 微表面理论的详细实现（Ch9）
5. 体积散射的物理模拟（Ch11）

**与RTR4的互补**：
- RTR4：实时渲染，光栅化管线，游戏应用
- PBRT4：离线渲染，路径追踪，电影级质量

**后续学习建议**：
- 编译运行pbrt-v4源码
- 实现Ch13的SimplePathIntegrator
- 对比CPU和GPU性能
- 结合RTR4实现混合渲染管线

---

*笔记完成日期：2026-03-05*
*参考资料：https://pbr-book.org/4ed/*
*GitHub源码：https://github.com/mmp/pbrt-v4*

