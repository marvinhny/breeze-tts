# voice：个人文本转语音工具

fork 自 breezeblue-ai/breeze-tts（Breeze TTS 2 官方 PyTorch 推理），作为动画口播 / 配音工具，后续在此改进。

- 远端：`origin` = marvinhny/breeze-tts（个人改动推这里），`upstream` = breezeblue-ai/breeze-tts（`git fetch upstream && git merge upstream/main` 同步）。
- 下游使用方：`~/MyProjects/animation`（fy-code-animation 技能）按本工具生成的实际音轨卡点。

## 本机注意

- 官方要求 Linux + NVIDIA CUDA（eager 约 7.7 GiB 显存）。本机是 Apple M4 / 32 GB，无 CUDA：
  - `breeze_infer/runtime.py` 的 `resolve_device` 在无 CUDA 时回落到 `cpu`，eager 路径（不加 `--fast-*`）理论上可在 CPU 跑，速度和兼容性尚未验证；`--fast-*` 依赖 CUDA Graph，本机不可用。
  - MPS（Apple GPU）支持尚未加入，是第一项可做的改进。
  - 也可以把本仓库部署到有 NVIDIA GPU 的云主机，用 `python -m breeze_infer.api` 起服务，本机通过 HTTP 调用。
- 模型权重在 Hugging Face `BreezeBlue/breeze-tts-2`，首次运行会下载到 HF 缓存。
- 依赖固定版本（torch 2.9.1 等），本机请用独立虚拟环境（Python ≥ 3.10，例如 `/opt/homebrew/bin/python3.13 -m venv .venv`）。

## 许可

代码 Apache 2.0；模型权重与自托管生成的音频仅限研究与非商业用途（BreezeBlue Research and Non-Commercial License）。商用口播需走其付费托管 API 或换其他 TTS。克隆他人声音须取得授权。
