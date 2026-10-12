# Deep CORAL 复现（GPU 版）使用指南

## 1. 下载代码和数据

```bash
git clone https://github.com/Cheng-quan-Z/DeepCORAL-GPU.git
```
```bash
cd DeepCORAL-GPU
```

## 2. 创建 Python 环境

```bash
conda create -n deepcoral python=3.11 -y
```
```bash
conda activate deepcoral
```

## 3. 安装依赖

先安装 CUDA 版 PyTorch。CUDA 版本要不高于 `nvidia-smi` 显示的版本，具体命令以 https://pytorch.org/get-started/locally/ 为准。下面以 CUDA 12.8 为例：
```bash
pip install torch torchvision --index-url https://download.pytorch.org/whl/cu128
```
再安装其余依赖：
```bash
pip install -r requirements.txt
```

## 4. 检查环境

```bash
python check_env.py
```
输出里应该有 `CUDA 可用: True`。

## 5. 训练（以 Amazon → Webcam 为例）

Deep CORAL：
```bash
python train.py --source A --target W
```
无适配基线：
```bash
python train.py --source A --target W --lambda_coral 0
```
`A` / `D` / `W` 分别代表 amazon / dslr / webcam。日志和结果保存在 `results/` 目录。

## 6. 画图并汇总结果

```bash
python plot.py --shift A2W --lambda_coral 1 --seed 0
```
```bash
python plot.py --table
```

## 7. 跑全部实验（6 个迁移方向 × 5 个随机种子）

Linux：
```bash
bash run_all.sh
```
Windows PowerShell：
```bash
powershell -ExecutionPolicy Bypass -File run_all.ps1
```
