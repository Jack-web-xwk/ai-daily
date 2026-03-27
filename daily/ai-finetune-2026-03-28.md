# AI微调技术日报 - 2026年3月28日

## 🔥 今日要闻

**1. HIVE：基于历史奖励轨迹的高效RL训练prompt选择框架**
提出双阶段prompt筛选框架，利用历史奖励轨迹进行粗筛选，并用prompt熵作为实时指标裁剪低效用样本，在多个数学推理基准上显著提升GRPO等RL算法的rollout效率，同时不损失性能。
来源：https://arxiv.org/abs/2603.25184

**2. Balanced DPO：通过均衡DPO提升LLM安全对齐**
提出平衡DPO方法改进标准DPO在安全对齐中的偏差问题，在RLHF框架下增强LLM的安全性表现，减少有害输出。
来源：https://arxiv.org/abs/2603.25538

**3. TuneShift-KD：面向微调模型的知识蒸馏与迁移**
提出新方法实现从微调后模型到新模型的知识蒸馏与迁移，解决领域微调后知识难以高效传递的痛点。
来源：https://arxiv.org/abs/2603.24916

**4. Axolotl v0.15.0 发布 — MoE训练大幅升级**
新增ScatterMoE LoRA支持、SonicMoE快速内核、MoE专家量化（GLM-4.7-Flash QLoRA显存从~127GiB降至~23GiB），同时支持Qwen3.5、SageAttention、MXFP4量化等。
来源：https://github.com/axolotl-ai-cloud/axolotl/releases

**5. FedPDPO：联邦学习下的个性化DPO对齐**
针对联邦场景中分散、隐私敏感且非IID的偏好数据，提出联邦个性化DPO方法，在保护隐私的同时实现LLM与人类偏好的对齐。
来源：https://arxiv.org/abs/2603.24828

## 📋 技术进展

### 训练方法与参数高效微调

- **Zipper-LoRA**：针对Speech-LLM多语言ASR，提出动态参数解耦LoRA，在共享与语言特定参数之间取得平衡。
  来源：https://arxiv.org/abs/2603.25029

- **PEFT vs 全量微调对比研究**：在医学文本摘要任务上系统比较LoRA、Prompt Tuning与全量微调的效果。
  来源：https://arxiv.org/abs/2603.25157

- **HypoTermInstruct**：通过专门构建的SFT数据集引导LLM认识自身知识边界，减少幻觉，从"总是回答"转向"认知谦逊"。
  来源：https://arxiv.org/abs/2603.24844

### 对齐技术

- **wDPO (Winsorized DPO)**：对DPO中的极端偏好样本进行Winsorized处理，提升LLM对齐的鲁棒性。
  来源：https://arxiv.org/abs/2603.22979

- **DARC (Disagreement-Aware Risk-Constrained Decoding)**：在解码阶段引入风险约束，基于偏好分歧进行对齐。
  来源：https://arxiv.org/abs/2603.21109

### 工具框架更新

- **Axolotl v0.15.0**：ScatterMoE LoRA + SonicMoE MoE训练加速内核；MoE专家量化显存降低80%+；SageAttention集成；Qwen3.5支持
  来源：https://github.com/axolotl-ai-cloud/axolotl/releases

- **LLaMA-Factory**：支持LD-DPO、PyTorch-elastic容错训练、Muon优化器、Qwen3/Llama 4/Gemma 3/MiniCPM4等新模型
  来源：https://github.com/hiyouga/LlamaFactory/releases

## 📊 趋势洞察

**1. DPO变体持续涌现，对齐方法走向精细化。** 本周可观察到DPO及其变体（Balanced DPO、wDPO、FedPDPO）仍是偏好对齐研究的主力方向。研究焦点正从"能不能用DPO替代RLHF"转向"如何让DPO在安全对齐、联邦场景等复杂条件下更鲁棒"。

**2. MoE微调基础设施快速成熟。** Axolotl v0.15.0中MoE专家量化将GLM-4.7-Flash QLoRA的显存从~127GiB暴降至~23GiB，标志着MoE模型的微调门槛正在急剧降低。

**3. RL训练效率优化成为新热点。** HIVE框架和多步工具编排的分级奖励设计，显示社区正从单纯扩大rollout规模转向更智能的训练数据管理和奖励设计。
