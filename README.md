# GWplotter

**Gravitational Wave Sensitivity Curve Plotter**

## 项目背景

引力波天文学自 2015 年 LIGO 首次直接探测到引力波信号（GW150914）以来，已迅速发展为一门崭新的观测天文学分支。不同类型的引力波探测器——地面激光干涉仪（如 LIGO、Virgo、KAGRA）、空间干涉仪（如 LISA、Taiji、TianQin）以及脉冲星计时阵列（如 IPTA、EPTA、SKA）——各自覆盖不同的频段，探测不同质量尺度的引力波源。

**灵敏度曲线（sensitivity curve）** 是描述探测器在不同频率下对引力波信号的敏感程度的函数，通常以特征应变 $h_c(f)$ 或无量纲能量密度 $\Omega_{\text{GW}}(f)$ 表示。绘制同一张图上，可以直观地对比不同探测器的探测能力，以及各类引力波源（致密双星并合、超大质量黑洞并合、银河系内致密双星、随机引力波背景等）的信号强度。

本项目最初由 **Christopher Moore**、**Robert Cole** 和 **Christopher Berry**（剑桥大学天文研究所引力波组）创建，并托管于 [gwplotter.com](http://gwplotter.com) 网站。该工作基于其 2015 年发表于 *Classical and Quantum Gravity* 的论文：

> Moore, C. J., Cole, R. H. & Berry, C. P. L. *Gravitational-wave sensitivity curves*. Class. Quantum Grav. **32**, 015014 (2015). [arXiv:1408.0740](https://arxiv.org/abs/1408.0740)

## 项目现状

原始网页版 [gwplotter.com](http://gwplotter.com) 现已恢复访问。同时，项目在原始代码基础上做了以下扩展：

- 添加了基于 **Jupyter Notebook** 的离线绘制方案（`graph.ipynb` 等），方便在本地运行
- 补充了 **Taiji（太极计划）** 和 **Gaia（盖亚卫星）** 的灵敏度数据，覆盖多个运行时长版本
- 保留了原始网页版可视化（`index.html`），基于 jQuery Flot 构建交互式绘图界面

## 支持的探测器

涵盖地面、空间和脉冲星计时阵列三大类，共计 **29 个探测器/配置**：

### 地面干涉仪（~10 – 10⁴ Hz）
| 探测器 | 说明 |
|--------|------|
| LIGO | 初始 LIGO |
| aLIGO-O1 | 先进 LIGO 首次观测运行（O1）灵敏度 |
| aLIGODesign | 先进 LIGO 设计灵敏度 |
| A+ | LIGO A+ 升级 |
| VIRGO / aVIRGO | Virgo / 先进 Virgo |
| KAGRA | 日本神冈引力波探测器 |
| GEO | 德国 GEO600 |
| TAMA | 日本 TAMA300 |
| ET | Einstein Telescope（第三代地面探测器概念） |
| CosmicExplorer | Cosmic Explorer（第三代地面探测器概念） |

### 空间干涉仪（~10⁻⁵ – 1 Hz）
| 探测器 | 说明 |
|--------|------|
| LISA | Laser Interferometer Space Antenna（欧空局/NASA） |
| eLISA | 早期 eLISA 概念 |
| Taiji | 太极计划（中国空间引力波探测） |
| TianQin | 天琴计划（中国空间引力波探测，中山大学） |
| Gaia | 盖亚卫星天体测量引力波探测（含 3年/5年/10年等版本） |
| ALIA | 先进激光干涉仪天线（概念） |
| DECIGO | 日本 DECi-hertz Interferometer Gravitational Wave Observatory |
| BBO | Big Bang Observer（概念） |

### 脉冲星计时阵列（~10⁻⁹ – 10⁻⁶ Hz）
| 探测器 | 说明 |
|--------|------|
| IPTA | 国际脉冲星计时阵列 |
| EPTA | 欧洲脉冲星计时阵列 |
| SKA | 平方公里阵列 |

## 引力波源模型

项目内置了多类引力波源的预期信号强度数据：

| 源类型 | 说明 |
|--------|------|
| 随机引力波背景（Stochastic background） | 宇宙早期引力波辐射遗迹 |
| 致密双星并合（CBCs / compact binary inspirals） | 中子星/黑洞双星旋近与并合 |
| 超大质量黑洞并合（Supermassive binaries） | 星系并合过程中的超大质量黑洞对 |
| 大质量黑洞并合（Massive binaries / mergers） | 中等质量黑洞并合事件 |
| 极端质量比旋近（EMRIs） | 小质量致密天体绕大质量黑洞的旋近 |
| 银河系致密双星（Galactic binaries） | 可分辨/不可分辨的银河系内双星 |
| 脉冲星（Pulsars） | 由脉冲星自身引力波辐射 |
| 超新星（Core-collapse / Type Ia supernovae） | 超新星爆发产生的引力波信号 |
| GW150914 | LIGO 首次直接探测到的双黑洞并合事件 |

## 技术实现

### 网页版
- 基于 **jQuery Flot** 的交互式图表
- 支持选择/取消探测器与源，自定义显示
- 依赖 `data/files.json` 配置绘图参数

### Jupyter Notebook 版
- **`graph.ipynb`** — 主力绘图脚本，对比各类探测器灵敏度曲线
- **`graph-Gaia.ipynb`** / **`graph-Gaia0.ipynb`** — 聚焦 Gaia、Taiji、LISA、TianQin 等空间探测器的对比
- **`Energy_density.ipynb`** — 能量密度 $\Omega_{\text{GW}}$ 的相关计算与转换
- **`Taiji.ipynb`** — 太极任务轨道数据加载与分析
- **`Gaia.ipynb`** — 盖亚任务引力波灵敏度理论计算

### 数据格式
探测器与源的灵敏度数据均以 JSON 格式存储：
- `data/detectors/` — 探测器灵敏度曲线，`{ "data": [[f1, h1], [f2, h2], ...] }`
- `data/sources/` — 引力波源强度曲线
- `data/files.json` — 元数据配置（类别、颜色、标签位置、默认显示等）

## 运行环境

Jupyter Notebook 版依赖以下 Python 库：
- `numpy`
- `scipy`
- `matplotlib`
- `astropy`

## 引用

如使用本代码进行学术研究，请引用原论文：

```
@article{Moore:2014we,
    author         = "Moore, Christopher J. and Cole, Robert H. and Berry, Christopher P. L.",
    title          = "{Gravitational-wave sensitivity curves}",
    journal        = "Class. Quant. Grav.",
    volume         = "32",
    year           = "2015",
    number         = "1",
    pages          = "015014",
    doi            = "10.1088/0264-9381/32/1/015014",
    eprint         = "1408.0740",
    archivePrefix  = "arXiv",
    primaryClass   = "gr-qc"
}
```

---

*2024-08-26 更新：新增 IPv6 Notebook 离线绘制方案，补充 Taiji 与 Gaia 探测器数据。*

*原始网页版：[gwplotter.com](http://gwplotter.com)*
