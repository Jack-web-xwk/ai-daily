# AI推理加速日报 - 2026年3月28日

## 🔥 本周要闻

**1. vLLM v0.18.0 正式发布：445个提交，多项推理突破**
本周最大亮点。新增gRPC服务、GPU-less多模态预处理、NGram GPU推测解码、KV Cache智能CPU卸载（FlexKV后端）、MoE弹性专家并行（NIXL-EP），还移除了Ray作为默认依赖。
来源：https://github.com/vllm-project/vllm/releases/tag/v0.18.0

**2. TensorRT-LLM 发布预览版：DeepSeek-V3.2 NVFP4优化 + Qwen3.5 FP8支持**
新增Qwen3.5文本模型的PyTorch后端BF16/FP8支持，DeepSeek-V3.2的NVFP4索引器GEMM和路由内核优化，Trtllm-Gen注意力后端新增KV Cache和推测解码支持。
来源：https://github.com/NVIDIA/TensorRT-LLM/releases

**3. vLLM 推测解码大升级：Eagle3 支持 Qwen3.5 / Kimi K2.5 MLA**
Eagle3推测解码扩展到更多主流模型，包括Qwen3.5、Kimi K2.5的MLA架构和Mistral Large 3的dense层。
来源：https://github.com/vllm-project/vllm/releases/tag/v0.18.0

**4. DeepSpeed v0.18.8：修复华为昇腾NPU兼容性 + EXAONE 4.0推理支持**
修复华为昇腾NPU上async_io构建错误，新增EXAONE 4.0模型的Inference V2支持，修复ROCm BF16转换问题。
来源：https://github.com/deepspeedai/DeepSpeed/releases

**5. SGLang v0.4.6 发布 — FlashAttention3 成为默认注意力后端**
DeepSeek/Qwen/Llama等主流模型默认启用FA3；引入PD分离+ Mooncake/NIXL传输后端；初步支持NVIDIA Blackwell架构。
来源：https://github.com/sgl-project/sglang/releases/tag/v0.4.6

## 📋 技术进展

### 推理框架
- **vLLM v0.18.0**：gRPC高性能RPC服务；GPU-less渲染（多模态预处理与GPU推理解耦）；NGram推测解码迁移至GPU执行；Ray不再作为默认依赖
- **SGLang v0.4.6**：FA3默认后端大幅提升attention性能；PD分离架构实现Prefill和Decode的计算-显存解耦
- **TensorRT-LLM**：Trtllm-Gen后端支持KV Cache + 推测解码；新增Qwen3.5/GLM5模型

### 推测解码
- vLLM的NGram推测解码迁移至GPU执行，兼容async scheduler
- Eagle3新增Qwen3.5、Kimi K2.5 MLA、Mistral Large 3支持
- TensorRT-LLM Trtllm-Gen后端原生支持MTP推测解码

### KV Cache 优化
- vLLM：智能CPU卸载仅保留高频复用KV block在GPU，FlexKV新后端
- TensorRT-LLM KVCacheManagerV2新增约束内存分区 + Python调度器

### 量化技术
- torchao v0.16.0：MXFP8 MoE训练级量化，DeepSeekV3 16B训练加速10%-25%
- vLLM：FP8 LoRA dense kernel

### 硬件适配
- **NVIDIA Blackwell**：SGLang初步支持
- **华为昇腾NPU**：DeepSpeed修复async_io编译错误
- **AMD ROCm**：DeepSpeed修复BF16转换

## 📊 趋势洞察

**KV Cache精细化管理和推测解码普惠化** 是本周两大关键词。vLLM的FlexKV + 智能CPU卸载标志着KV Cache走向按热度分层的精细化调度。推测解码对Qwen3.5、Kimi K2.5等热门国产模型的覆盖意味着这项技术正在加速进入生产环境。

**推理框架的"去重"和"解耦"** 也在加速：vLLM移除Ray默认依赖、引入gRPC独立于REST，GPU-less render serving将多模态预处理从GPU推理中解耦，让CPU和GPU各司其职。
