# Prompt-Guided Superalloy Microstructure Segmentation

This repository provides a small demonstration set and a ComfyUI workflow for prompt-guided segmentation of Ni-based single-crystal superalloy SEM micrographs. The workflow uses a multimodal image editing model to generate color-coded label images from structured text prompts, followed by color-based mask extraction for quantitative microstructure analysis.

The example task focuses on $\gamma/\gamma'$ microstructures after thermal exposure at $1070\,^{\circ}\mathrm{C}$. The included examples cover four exposure times: 10 h, 150 h, 300 h, and 500 h.

## Repository Structure

```text
.
|-- README.md
|-- data
|   |-- manifest.csv
|   `-- examples
|       |-- 1070-10H
|       |-- 1070-150H
|       |-- 1070-300H
|       `-- 1070-500H
|
`-- workflows
    `-- prompt-guided-superalloy-segmentation.comfyui.json
```




## Model and Workflow

The ComfyUI workflow is provided at:

```text
workflows/prompt-guided-superalloy-segmentation.comfyui.json
````

The workflow was configured with the following model files:

| Component | File name used in the workflow | Hugging Face source | ModelScope source |
|---|---|---|---|
| Diffusion model / UNet | `qwen_image_edit_2511_fp8mixed.safetensors` | [Comfy-Org/Qwen-Image-Edit_ComfyUI](https://huggingface.co/Comfy-Org/Qwen-Image-Edit_ComfyUI/blob/main/split_files/diffusion_models/qwen_image_edit_2511_fp8mixed.safetensors) | [Qwen/Qwen-Image-Edit-2511](https://modelscope.cn/models/Qwen/Qwen-Image-Edit-2511) |
| Lightning LoRA / acceleration adapter | `Qwen-Image-Edit-2511-Lightning-4steps-V1.0-bf16.safetensors` | [lightx2v/Qwen-Image-Edit-2511-Lightning](https://huggingface.co/lightx2v/Qwen-Image-Edit-2511-Lightning/blob/main/Qwen-Image-Edit-2511-Lightning-4steps-V1.0-bf16.safetensors) | [lightx2v/Qwen-Image-Edit-2511-Lightning](https://modelscope.cn/models/lightx2v/Qwen-Image-Edit-2511-Lightning) |
| Text encoder / CLIP | `qwen_2.5_vl_7b_fp8_scaled.safetensors` | [Comfy-Org/Qwen-Image_ComfyUI](https://huggingface.co/Comfy-Org/Qwen-Image_ComfyUI/blob/main/split_files/text_encoders/qwen_2.5_vl_7b_fp8_scaled.safetensors) | [Qwen/Qwen-Image-Edit-2511](https://modelscope.cn/models/Qwen/Qwen-Image-Edit-2511) |
| VAE | `qwen_image_vae.safetensors` | [Comfy-Org/Qwen-Image_ComfyUI](https://huggingface.co/Comfy-Org/Qwen-Image_ComfyUI/blob/main/split_files/vae/qwen_image_vae.safetensors) | [Qwen/Qwen-Image-Edit-2511](https://modelscope.cn/models/Qwen/Qwen-Image-Edit-2511) |




Model weights are not included in this repository. Please download the corresponding files from the links above and place them in the model directories expected by your ComfyUI installation for `diffusion_models`, `text_encoders`, `vae`, and `loras`.





## Prompt Design

The structured prompt describes:

- target microstructural morphology, such as strip-like, band-like, blocky, or connected regions;
- spatial relationships between $\gamma'$ precipitates and the $\gamma$ matrix;
- fixed color rules for each microstructural class;
- output constraints, including solid-color filling, no transparency, no gradients, and preservation of the original morphology and phase boundaries.




## Notes

- This repository is intended as a compact demonstration package rather than a full training dataset.
- No model weights are included.
- Before public release, add a license file that matches the intended data and code sharing policy.
- If these data are used in a publication, cite the associated paper or manuscript once available.
