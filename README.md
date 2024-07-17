<div align="center">
<h1>T-GATE: Temporally Gating Attention to Accelerate Diffusion Model for Free! 🥳</h1>  
    <a href="https://github.com/HaozheLiu-ST/T-GATE/blob/main/LICENSE">
    <img alt="GitHub" src="https://img.shields.io/github/license/HaozheLiu-ST/T-GATE.svg?color=blue"> 
</a>
<a href="https://arxiv.org/abs/2404.02747">
  <img alt="arxiv" src="https://img.shields.io/badge/arXiv-<2404.02747>-<COLOR>.svg">
</a>
<a href="https://github.com/HaozheLiu-ST/T-GATE/releases">
    <img alt="GitHub release" src="https://img.shields.io/github/release/HaozheLiu-ST/T-GATE.svg">
</a>
</div>

> **TGATE-V1: Cross-Attention Makes Inference Cumbersome in Text-to-Image Diffusion Models**  
> [Wentian Zhang](https://wentianzhang-ml.github.io/)<sup>&#42;</sup>&nbsp; [Haozhe Liu](https://haozheliu-st.github.io/)<sup>1&#42;</sup>&nbsp; [Jinheng Xie](https://sierkinhane.github.io/)<sup>2&#42;</sup>&nbsp; [Francesco Faccio](https://scholar.google.com/citations?user=0z3DkrkAAAAJ&hl=en)<sup>1,3</sup>&nbsp; [Mike Zheng Shou](https://scholar.google.com/citations?hl=zh-CN&user=h1-3lSoAAAAJ&view_op=list_works&sortby=pubdate)<sup>2</sup>&nbsp; [Jürgen Schmidhuber](https://scholar.google.com/citations?user=gLnCTgIAAAAJ&hl=en)<sup>1,3</sup>&nbsp;
> 
> <sup>1</sup> AI Initiative, King Abdullah University of Science And Technology &nbsp;
> 
> <sup>2</sup> Show Lab, National University of Singapore &nbsp; <sup>3</sup> The Swiss AI Lab, IDSIA
>


> **TGATE-V2: Faster Diffusion Through Temporal Attention Decomposition**  
> [Haozhe Liu](https://haozheliu-st.github.io/)<sup>1,4&#42;</sup>&nbsp; [Wentian Zhang](https://wentianzhang-ml.github.io/)<sup>&#42;</sup>&nbsp; [Jinheng Xie](https://sierkinhane.github.io/)<sup>2&#42;</sup>&nbsp; [Francesco Faccio](https://scholar.google.com/citations?user=0z3DkrkAAAAJ&hl=en)<sup>1,3</sup>&nbsp; [Mengmeng Xu](https://scholar.google.com/citations?user=be_ox9QAAAAJ&hl=en)<sup>4</sup>&nbsp; [Tao Xiang](https://scholar.google.com/citations?user=MeS5d4gAAAAJ&hl=en)<sup>4</sup>&nbsp; [Mike Zheng Shou](https://scholar.google.com/citations?hl=zh-CN&user=h1-3lSoAAAAJ&view_op=list_works&sortby=pubdate)<sup>2</sup>&nbsp; [Juan-Manuel Pérez-Rúa](https://scholar.google.com/citations?user=Vbvimu4AAAAJ&hl=en)<sup>4</sup>&nbsp; [Jürgen Schmidhuber](https://scholar.google.com/citations?user=gLnCTgIAAAAJ&hl=en)<sup>1,3</sup>&nbsp;
> 
> <sup>1</sup> AI Initiative, King Abdullah University of Science And Technology &nbsp;
> 
> <sup>2</sup> Show Lab, National University of Singapore &nbsp; <sup>3</sup> The Swiss AI Lab, IDSIA &nbsp; <sup>4</sup> Meta
>

![](./assets/teaser.png)

## Quick Introduction

> We explore the role of attention mechanism during inference in text-conditional diffusion models. Empirical observations suggest that cross-attention outputs converge to a fixed point after several inference steps. The convergence time naturally divides the entire inference process into two phases: an initial phase for planning text-oriented visual semantics, which are then translated into images in a subsequent fidelity-improving phase. Cross-attention is essential in the initial phase but almost irrelevant thereafter. However, self-attention initially plays a minor role but becomes crucial in the second phase. These findings yield a simple and training-free method known as temporally gating the attention (TGATE), which efficiently generates images by caching and reusing attention outputs at scheduled time steps. Experimental results show when widely applied to various existing text-conditional diffusion models, TGATE accelerates these models by 10%–50%.

![](./assets/visualization.png)
>  The images generated by the diffusion model with or without TGATE. Our method can accelerate the diffusion model without generation performance drops. It is training-free and can be widely complementary to the existing studies.


## 🚀 Major Features

* Training-Free.
* Easily Integrate into Existing Frameworks.
* Only a few lines of code are required.
* Friendly support CNN-based U-Net, Transformer, and Consistency Model
* 10%-50% speed up for different diffusion models. 

  
## 📄 Updates

<!-- * 2024/07/18: We release TGATE [v1.0.0](https://github.com/HaozheLiu-ST/T-GATE/tree/0.1.1) to support the `PixArt-Sigma` and `StableVideoDiffusion` models. -->

* 2024/05/22: We have successfully extended TGATE to self-attention modules for greater acceleration!

* 2024/04/17: TGATE [v0.1.1](https://github.com/HaozheLiu-ST/T-GATE/tree/0.1.1) is officially added to [diffusers](https://huggingface.co/docs/diffusers/main/en/optimization/tgate).

* 2024/04/14: We release TGATE [v0.1.1](https://github.com/HaozheLiu-ST/T-GATE/tree/0.1.1) to support the [`playground-v2.5-1024`](https://huggingface.co/playgroundai/playground-v2.5-1024px-aesthetic) model.

* 2024/04/10: We release our package to [PyPI](https://pypi.org/project/tgate/). Check [here](https://github.com/HaozheLiu-ST/T-GATE/tree/releases) for the usage.

* 2024/04/04: Technical Report is available on [arxiv](https://arxiv.org/abs/2404.02747). 

* 2024/04/04: TGATE for DeepCache (SD-XL) is released.

* 2024/03/30: TGATE for SD-1.5/2.1/XL is released.

* 2024/03/29: TGATE for LCM (SD-XL), PixArt-Alpha is released.
  
* 2024/03/28: TGATE is open source.


## 📖 Key Observation

![](./assets/observation.png)

>  Impact of cross-attention on the inference steps in a pre-trained diffusion model (SD-2.1). The images generated by the diffusion model at different denoising steps. The first row feeds the text embedding to the cross-attention modules for all steps. The second row only uses the text embedding from the first step to the 10th step, and the third row inputs the text embedding from the 11th to the 25th step.

We summarize our observations as follows:

* Cross-attention converges early during inference, which can be characterized by a semantics-planning and a fidelity-improving phases. The impact of cross-attention is not uniform in these two phases.

* Cross-attention in the semantics-planning phase is significant for generating semantics aligned with the text conditions

* The fidelity-improving phase mainly improves the image quality without requiring cross-attention. FID scores can be slightly improved via null-text embedding in this phase.

## 🖊️ Method

* Step 1: TGATE caches the attention outcomes from the semantics-planning phase.
```
if gate_step == cur_step:
    hidden_uncond, hidden_pred_text = hidden_states.chunk(2)
    cache = (hidden_uncond + hidden_pred_text ) / 2
```

* Step 2: TGATE reuses the self attention throughout the semantics-planning phase.

```
if self_attn and (gate_step>cur_step):
    hidden_states = cache
```

* Step 3: TGATE reuses the cross attention throughout the fidelity-improving phase.

```
if cross_attn and (gate_step<cur_step):
    hidden_states = cache
```

## 📄 Results
| Model                 | MACs     | Latency | Zero-shot 10K-FID on MS-COCO |
|-----------------------|----------|---------|---------------------------|
| SD-XL                 | 149.438T | 53.187s | 24.164                    |
| SD-XL w/ TGATE        | 95.988T  | 31.643s | 22.917                    |
| Pixart-Alpha          | 107.031T | 61.502s | 37.983                    |
| Pixart-Alpha w/ TGATE | 73.971T  | 36.650s | 36.390                    |
| Pixart-Sigma          | 107.766T | 60.467s | 34.278                    |
| Pixart-Sigma w/ TGATE | 74.420T  | 36.449s | 32.927                    |
| DeepCache (SD-XL)     | 57.888T  | 19.931s | 25.678                    |
| DeepCache w/ TGATE    | 43.868T  | 14.666s | 24.511                    |
| LCM (SD-XL)           | 11.955T  | 3.805s  | 26.357                    |
| LCM w/ TGATE          | 11.171T  | 3.533s  | 26.902                    |
| LCM (Pixart-Alpha)    | 8.563T   | 4.733s  | 35.989                    |
| LCM w/ TGATE          | 7.623T   | 4.543s  | 35.843                    |

The FID is computed on [idx_caption.txt](https://github.com/HaozheLiu-ST/T-GATE/files/15369063/idx_caption.txt).

The latency is tested on a 1080ti commercial card and diffusers v0.28.2. 

The MACs are calculated by [calflops](https://github.com/MrYxJ/calculate-flops.pytorch). 

The FID is calculated by [PytorchFID](https://github.com/mseitzer/pytorch-fid).

## 🛠️ Requirements

* pytorch>=2.0.0
* diffusers>=0.29.2
* transformers==4.37.2
* DeepCache==0.1.1
* accelerate


## 🌟 Usage

### Examples

To use TGATE for accelerating the denoising process, you can simply use `main.py`. For example,


* SD-XL w/ TGATE: generate an image with the caption: "Astronaut in a jungle, cold color palette, muted colors, detailed, 8k" 

```bash
python main.py \
--prompt 'Astronaut in a jungle, cold color palette, muted colors, detailed, 8k' \
--model 'sdxl' \
--gate_step 10 \
--sa_interval 5 \
--ca_interval 1 \
--warm_up 2 \
--saved_path './sd_xl/' \
--inference_step 25 \
```


* Pixart-Alpha w/ TGATE: generate an image with the caption: "An alpaca made of colorful building blocks, cyberpunk." 

```bash
python main.py \
--prompt 'An alpaca made of colorful building blocks, cyberpunk.' \
--model 'pixart_alpha' \
--gate_step 15 \
--sa_interval 3 \
--ca_interval 1 \
--warm_up 2 \
--saved_path './pixart_alpha/' \
--inference_step 25 \
```

* Pixart-Sigma w/ TGATE: generate an image with the caption: "an astronaut sitting in a diner, eating fries, cinematic, analog film." 

```bash
python main.py \
--prompt 'an astronaut sitting in a diner, eating fries, cinematic, analog film.' \
--model 'pixart_sigma' \
--gate_step 15 \
--sa_interval 3 \
--ca_interval 1 \
--warm_up 2 \
--saved_path './pixart_sigma/' \
--inference_step 25 \
```

* LCM-SDXL w/ TGATE: generate an image with the caption: "Self-portrait oil painting, a beautiful cyborg with golden hair, 8k" 

```bash
python main.py \
--prompt 'Self-portrait oil painting, a beautiful cyborg with golden hair, 8k' \
--model 'lcm_sdxl' \
--gate_step 1 \
--sa_interval 1 \
--ca_interval 1 \
--warm_up 0 \
--saved_path './lcm_sdxl/' \
--inference_step 4 \
```


* SDXL-DeepCache w/ TGATE: generate an image with the caption: "A haunted Victorian mansion under a full moon." 

```bash
python main.py \
--prompt 'A haunted Victorian mansion under a full moon.' \
--model 'sd_xl' \
--gate_step 10 \
--sa_interval 1 \
--ca_interval 1 \
--warm_up 0 \
--saved_path './sd_xl_deepcache/' \
--inference_step 25 \
--deepcache \
```
1. For LCMs, `gate_step` is set as 1 or 2, and `inference step` is set as 4.

2. To use DeepCache, `deepcache` is set as True. 

### Third-party Usage
- T-GATE in ComfyUI [ComfyUI_TGate](https://github.com/JettHu/ComfyUI_TGate)

## Acknowledgment

* We thank [prompt to prompt](https://github.com/google/prompt-to-prompt)  and [diffusers](https://huggingface.co/docs/diffusers/index) for the great code.

## Citation
If you find our work inspiring or use our codebase in your research, please consider giving a star ⭐ and a citation.
```
@article{tgate,
  title={Cross-Attention Makes Inference Cumbersome in Text-to-Image Diffusion Models},
  author={Zhang, Wentian and Liu, Haozhe and Xie, Jinheng and Faccio, Francesco and Shou, Mike Zheng and Schmidhuber, J{\"u}rgen},
  journal={arXiv preprint arXiv:2404.02747},
  year={2024}
}
```
