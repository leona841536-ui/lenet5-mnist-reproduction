# LeNet-5 MNIST 手写数字识别

PyTorch 复现 LeNet-5，含 MLP 基线对照与完整评估脚本。

## 环境

- Python 3.8+
- 依赖见 `requirements.txt`（torch、torchvision 等）
- CPU 可运行，有 GPU 会自动使用

## 安装与运行

```bash
git clone https://github.com/你的用户名/lenet5-mnist-reproduction.git
cd lenet5-mnist-reproduction
pip install -r requirements.txt
python run_all.py
```

Windows 可直接双击 `run_all.bat`。

首次运行会自动下载 MNIST 到 `data/`。完整实验（可视化 + 对照训练 + 评估）约 8～10 分钟（CPU）。

## 分步执行

```bash
python visualize_data.py      # 数据分布图 → results/figures/data/
python compare_experiment.py  # MLP 与 LeNet-5 对照训练
python evaluate.py            # 测试集评估与混淆矩阵
```

只训练 LeNet-5：

```bash
python train.py
python evaluate.py
```

已有模型权重、跳过训练：

```bash
python run_all.py --skip-compare --skip-data-viz
```

## 目录说明

| 文件/目录 | 说明 |
|-----------|------|
| `config.py` | 超参数、路径配置 |
| `models/lenet5.py` | LeNet-5 网络 |
| `models/mlp.py` | MLP 基线 |
| `utils/dataset.py` | MNIST 加载与预处理 |
| `compare_experiment.py` | 对照实验主脚本 |
| `evaluate.py` | 测试集指标与图表 |
| `results/` | 运行后生成（指标、图表、权重） |

## 默认超参数

Batch Size 64，Epochs 10，Learning Rate 0.001，Adam 优化器，随机种子 42（见 `config.py`）。

## 本地参考结果

| 模型 | 测试准确率 | 参数量 |
|------|-----------|--------|
| MLP | 97.97% | 658,698 |
| LeNet-5 | 98.82% | 61,706 |

以实际运行输出为准。

## 常见问题

- **MNIST 下载失败**：先跑 `compare_experiment.py`，再跑 `visualize_data.py`
- **找不到模型权重**：先跑 `compare_experiment.py` 或 `train.py`
