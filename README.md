# :rocket: YOPO: You Only Prune Once for Your MLLMs


This repository contains the core code to implement the idea of  our paper:

[Treat Visual Tokens as Text? But Your MLLM Only Needs Fewer Efforts to See](https://arxiv.org/abs/2410.06169v2)

![Alt text](images/method_fig.png "Overview of our method.")

### :bangbang: While many studies focus on pruning visual tokens to reduce the computational overhead caused by visual redundancy, the process of identifying these tokens for each conversation is itself resource-intensive. Now the question comes, ###  

### **Can we prune our MLLM just once instead?**:interrobang: ###


## Abstract
By treating visual tokens from visual encoders as text tokens, Multimodal Large Language Models (MLLMs) have achieved remarkable progress across diverse visual understanding tasks, leveraging the robust architectures of Large Language Models (LLMs). However, as token counts grow, the quadratic scaling of computation in LLMs introduces a significant efficiency bottleneck, impeding further scalability. Although recent approaches have explored pruning visual tokens or employing lighter LLM architectures, the computational overhead from an increasing number of visual tokens remains a substantial challenge.

In this study, we investigate the redundancy in visual computation at both the parameter and computational pattern levels within LLaVA, a representative MLLM, and introduce a suite of streamlined strategies to enhance efficiency. These include **neighbor-aware visual token attention**, **pruning of inactive visual attention heads**, and **selective layer dropping** for visual computations. By implementing these strategies in LLaVA, we achieve a reduction in computational demands of 88% while maintaining model performance across key benchmarks. Additionally, we validate the existence of visual computational redundancy in other MLLMs, such as Qwen2-VL-7B and InternVL-2.0-4B/8B/26B. These results present a novel pathway for MLLMs to handle dense visual tokens with minimal computational costs. Code and model checkpoints will be released to support further research.




## How to use our code?
1. set up LLavA  
```Shell
cd LLaVA
conda create -n llava python=3.10 -y
conda activate llava
pip install --upgrade pip  
pip install -e .
```

2. Update the modeling file to ours for acceleration
```Shell
cd ~
cp modeling_llama_prune.py {YOUR ENV PATH}/lib/python3.10/site-packages/transformers//models/llama/modeling_llama.py
```

3. Download the checkpoints of pruned LLaVA

1. [LLaVA-1.5-7B (12% FLOPs)](https://huggingface.co/zwt123home123/llava-1.5-7b-prune-zp12)
2. [LLaVA-1.5-7B (25% FLOPs)](https://huggingface.co/zwt123home123/llava-1.5-13b-prune-zp25)
3. [LLaVA-1.5-13B (12% FLOPs)](https://huggingface.co/zwt123home123/llava-1.5-7b-prune-zp12)
4. [LLaVA-1.5-13B (25% FLOPs)](https://huggingface.co/zwt123home123/llava-1.5-13b-prune-zp25)

:warning: for sanity check, please refer to the [infer.sh](infer.sh).

:triangular_flag_on_post:  We will release the code for pruning the visual computation in Qwen, InternVL without the fine-tuning process very soon.  
:triangular_flag_on_post:  The code for training pruned LLava will also be released soon.  


## Main result
![Results on prunining the LLaVa](images/main_result.png "Results on prunining the LLaVa")
![Results on pruning the Qwen and InternVL](images/many_models.png "Results on pruning the Qwen and InternVL")


## Citation

If you find the idea or code useful for your research, please consider citing our [paper](https://arxiv.org/abs/2403.12777):

```
@article{zhang2024treat,
  title={Treat Visual Tokens as Text? But Your MLLM Only Needs Fewer Efforts to See},
  author={Zhang, Zeliang and Pham, Phu and Zhao, Wentian and Wan, Kun and Li, Yu-Jhe and Zhou, Jianing and Miranda, Daniel and Kale, Ajinkya and Xu, Chenliang},
  journal={arXiv preprint arXiv:2410.06169},
  year={2024}
}
```

## Contact
Questions and suggestions can be sent to hust0426@gmail.com and {wezhao, kuwan}@adobe.com.
