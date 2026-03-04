# 📊 Differentiable XAJ Training Outputs / 可微分新安江模型训练输出

[English](#english) | [中文](#chinese)

---

<a id="english"></a>

## 🌍 English Documentation

This directory acts as the repository for all artifacts, optimized model weights, and visualization graphics generated during the autonomous training phase of the **Differentiable Xin'anjiang (XAJ) Model V4**.

### 📁 Artifact Descriptions

| File Name | Description | Functional Significance |
|:---|:---|:---|
| **`differentiable_xaj_model_improved.pth`** | **PyTorch Model Weights** | The serialized `.pth` dictionary of the fully trained model. Contains the exact physical parameters ($WM$, $B$, $MuskK$, $MuskX$, etc.) successfully learned via gradient descent. Load this directly via `torch.load()` to run fast hydrological inference without retraining. |
| **`training_results_improved.png`** | **Comprehensive Hydrograph & State Analysis** | Provides a dynamic snapshot of the entire simulation vs. reality:<br>1. **Hydrograph Fit:** Simulated discharge curve vs. Observed streamflow.<br>2. **Residuals:** Time-series error tracking.<br>3. **Source Flow Partition:** The internal split of flow paths (Surface, Interflow, Groundwater).<br>4. **Storage Variables:** Tracks the hidden internal constraints (Soil Moisture $W$, Free Water $S$) to verify strict physical realism dynamically. |
| **`training_history_improved.png`** | **Loss & Efficiency Convergence Curve** | Plots the overall PDE-Loss function decay across epochs alongside the Nash-Sutcliffe Efficiency (NSE) score. Crucial for verifying that the neural gradient descent is effectively minimizing error without running into severe local minima or oscillatory divergence. |
| **`parameter_evolution.png`** | **Trajectory of Physical Parameters** | A powerful visual diagnostic showing how individual conceptual parameters converge over time. Watch parameters move from random initialization bounds to their optimal, hydrologically sound constraints. |

---

<a id="chinese"></a>

## 🇨🇳 中文文档

本文件夹是**可微分新安江模型 V4** 自动训练阶段生成的所有产物、优化后的模型权重以及可视化图表的统一存放位置。

这些输出结果旨在提供一个全面、透明的视角，不仅展示神经网络纯数据驱动的拟合能力，更用于验证通过反向传播学习到的参数在物理层面上的合理性。

### 📁 文件功能说明

| 文件名 | 功能描述 | 科研意义与用途 |
|:---|:---|:---|
| **`differentiable_xaj_model_improved.pth`** | **PyTorch 模型权重文件** | 完全训练好的模型序列化 `.pth` 字典文件。包含通过梯度下降成功学习到的精确物理参数（如 $WM$, $B$, $MuskK$, $MuskX$ 等）。可通过 `torch.load()` 直接加载，实现快速水文预测推理而无需重新训练。 |
| **`training_results_improved.png`** | **综合水文过程线与状态分析图** | 提供模拟与现实对比的动态全局视图：<br>1. **流量拟合:** 模拟流量曲线对比观测径流。<br>2. **残差分析:** 时间序列误差追踪。<br>3. **水源划分:** 内部径流分量的变化（地表、壤中、地下径流）。<br>4. **蓄水变量:** 追踪内部隐藏的物理约束（如土壤水分 $W$、自由水 $S$），以动态验证其绝对的物理真实性。 |
| **`training_history_improved.png`** | **损失与效率收敛曲线图** | 绘制整体偏微分方程（PDE）损失函数的下降过程，以及纳什效率（NSE）的得分演变。这对于验证神经网络梯度下降是否真正在有效降低误差，且未陷入严重的局部最优或震荡发散现象具有关键作用。 |
| **`parameter_evolution.png`** | **物理参数演变轨迹图** | 一个极其强大的可视化诊断工具，展示各个概念性参数在训练过程中是如何随着时间推移逐渐收敛的。可以直观观察参数是如何从随机初始化边界，最终探索并锁定在其物理范围内最优值的。 |

### ⚙️ 验证与评价模型 (Evaluation Guide)

无论看中文还是英文，评价模型好坏需注意： / When evaluating a model, check for:

1. **高纳什效率 (NSE > 0.85)** / **High NSE (> 0.85)**: 收敛平稳表明 Muskingum 汇流发挥了重要作用。 / Stable convergence is a sign of effective routing.
2. **合理的储水状态** / **Stable Storage States**: 土壤水分 ($W$) 不应剧烈突破最大物理容量 ($WM$)。 / Soil Moisture ($W$) must not violently breach its bounds ($WM$).
3. **参数平稳收敛** / **Smooth Parameter Convergence**: 参数演变图 (`parameter_evolution.png`) 末期曲线应平滑。 / Parameters should stabilize into flat lines.
