# Awesome Image to Layer

A curated list of tools, models, papers, datasets and libraries for turning a flat image into editable layers, a task also called image to layer, image layer decomposition or image to layered PSD. Most pipelines combine three steps: cutting out each element (segmentation and matting), filling in what was hidden behind it (inpainting or amodal completion), and packaging the result as layers (usually a PSD). Newer end-to-end models do all three in one pass.

## Contents

- [Online tools](#online-tools)
- [Image to PSD converters](#image-to-psd-converters)
- [Design software features](#design-software-features)
- [Open-source models and code](#open-source-models-and-code)
- [Research papers](#research-papers)
  - [Layer decomposition](#layer-decomposition)
  - [Layered image generation](#layered-image-generation)
  - [Amodal completion and de-occlusion](#amodal-completion-and-de-occlusion)
- [Building blocks](#building-blocks)
  - [Segmentation](#segmentation)
  - [Matting and background removal](#matting-and-background-removal)
  - [Inpainting](#inpainting)
  - [Depth](#depth)
- [PSD libraries](#psd-libraries)
- [Datasets](#datasets)
- [Tutorials](#tutorials)
- [Browser extensions](#browser-extensions)

## Online tools

- [Image to Layer](https://image2layers.org/) - AI splits a flat JPG, PNG or WebP into editable transparent layers with the background filled in, and exports a layered PSD. Free in-browser PSD converter; layer splitting is paid (credits).
- [Qwen-Image-Layered on fal](https://fal.ai/models/fal-ai/qwen-image-layered) - Hosted API for the Qwen-Image-Layered model, which decomposes an image into multiple RGBA layers.
- [Qwen-Image-Layered on Hugging Face](https://huggingface.co/spaces/Qwen/Qwen-Image-Layered) - Official demo Space that separates an uploaded image into several RGBA layers you can download together.
- [remove.bg](https://www.remove.bg/) - Automatic background removal; produces a transparent cut-out of the subject, not a filled-in background layer.
- [RunDiffusion Image-to-Layers](https://www.rundiffusion.com/introducing-image-to-layers-a-rundiffusion-exclusive-workflow-with-psd-export) - Workflow on the RunDiffusion platform that auto-segments a flat image into layers and exports a layered PSD.
- [See-through demo](https://huggingface.co/spaces/24yearsold/see-through-demo) - Official Hugging Face Space for See-through; turns an anime character illustration into a layered PSD, with a few free runs per day.

## Image to PSD converters

- [CloudConvert PNG to PSD](https://cloudconvert.com/png-to-psd) - General-purpose online file converter; changes the file format without separating the image into object layers.
- [Image to Layer — AI-generated image to PSD](https://image2layers.org/ai-generated-image-to-psd) - Turns ChatGPT, Midjourney or Gemini images into a PSD for free, or into a layered PSD with subject, text and background on separate layers.
- [Image to Layer — JPG to PSD](https://image2layers.org/jpg-to-psd) - Free in-browser JPG to PSD conversion, with optional AI layering that puts the product and the background on separate layers.
- [Image to Layer — PNG to PSD](https://image2layers.org/png-to-psd) - Free in-browser PNG to PSD conversion, with optional AI layering that separates subject, graphics and background.
- [ImageMagick](https://imagemagick.org/) - Command-line image toolkit that reads and writes PSD; useful for batch format conversion in scripts.
- [Photopea](https://www.photopea.com/) - Free browser-based image editor with full PSD support; open a JPG or PNG, build layers by hand and save as PSD.

## Design software features

- [Adobe Photoshop — Content-Aware Fill](https://helpx.adobe.com/photoshop/desktop/repair-retouch/remove-objects-fill-space/remove-objects-with-content-aware-fill.html) - Removes a selected object and fills the area from surrounding pixels; one way to rebuild the background behind a subject moved to its own layer.
- [Adobe Photoshop — Generative Fill](https://helpx.adobe.com/photoshop/desktop/create-open-import-images/create-images/edit-images-with-generative-fill.html) - Adds, removes or modifies content inside a selection from a text prompt, or fills it from surrounding pixels when the prompt is left empty.
- [Adobe Photoshop — Select Subject](https://helpx.adobe.com/photoshop/desktop/make-selections/automatic-color-based-selections/detect-subject-using-select-subject.html) - Automatically detects and selects the main subjects in an image, a common first step before copying a subject to a new layer.
- [Canva Magic Layers](https://www.canva.com/magic-layers/) - Canva feature that breaks a flat PNG or JPG into separate, movable elements and editable text inside the Canva editor.

## Open-source models and code

- [CLD](https://github.com/monkek123King/CLD) - Code and checkpoints for Controllable Layer Decomposition, a FLUX-based model for controllable multi-layer separation of raster images.
- [ComfyUI-See-through](https://github.com/jtydhr88/ComfyUI-See-through) - ComfyUI nodes that wrap See-through for anime layer decomposition with depth ordering, aimed at Live2D workflows.
- [LayerD](https://github.com/CyberAgentAILab/LayerD) - Official code for decomposing raster graphic designs into layers, with SVG and PSD export; installable with pip (ICCV 2025).
- [layerdivider](https://github.com/mattyamonaca/layerdivider) - Splits an illustration into color-based layers by pixel clustering and writes a PSD; local Gradio GUI or Colab.
- [OmniPSD](https://github.com/showlab/OmniPSD) - Code for text-to-PSD generation and image-to-PSD decomposition of flat posters, built on FLUX with an RGBA-VAE.
- [Qwen-Image-Layered](https://github.com/QwenLM/Qwen-Image-Layered) - Apache-2.0 model that decomposes an image into a variable number of RGBA layers; includes a Gradio app that exports PPTX, ZIP and PSD.
- [RevealLayer](https://github.com/360CVGroup/RevealLayer) - Inference code and checkpoint for occlusion-aware decomposition of natural images into RGBA layers, including hidden content (ICML 2026).
- [sd-forge-layerdiffuse](https://github.com/lllyasviel/sd-forge-layerdiffuse) - LayerDiffuse for Stable Diffusion WebUI Forge; generates transparent layers and includes models that produce a foreground from a background plus the blended image.
- [See-through](https://github.com/shitagaki-lab/see-through) - Official code that splits one anime character illustration into up to 23 inpainted, semantically distinct layers with drawing order and exports a PSD (SIGGRAPH 2026).

## Research papers

### Layer decomposition

- [Controllable Layer Decomposition for Reversible Multi-Layer Image Generation](https://arxiv.org/abs/2511.16249) - Splits raster images into RGBA layers with fine-grained control; the layers can be edited directly in tools such as PowerPoint (2025).
- [Decomposing Digital Paintings into Layers via RGB-space Geometry](https://arxiv.org/abs/1509.03335) - Non-learning method that derives paint colors from the convex hull of pixels in RGB space and solves for translucent layer opacities (2015).
- [Fast Soft Color Segmentation](https://arxiv.org/abs/2004.08096) - Neural network that decomposes an image into color-homogeneous RGBA layers in a single forward pass (2020).
- [Generative Image Layer Decomposition with Visual Effects](https://arxiv.org/abs/2411.17864) - LayerDecomp: outputs a clean background and a transparent foreground that keeps shadows and reflections (2024).
- [LayerD: Decomposing Raster Graphic Designs into Layers](https://arxiv.org/abs/2509.25134) - Iteratively extracts unoccluded foreground layers from graphic designs and proposes a quality metric for decomposition (ICCV 2025).
- [OmniPSD: Layered PSD Generation with Diffusion Transformer](https://arxiv.org/abs/2512.09247) - One diffusion framework for text-to-PSD generation and image-to-PSD decomposition by iterative extract-and-erase (2025).
- [Qwen-Image-Layered: Towards Inherent Editability via Layer Decomposition](https://arxiv.org/abs/2512.15603) - End-to-end diffusion model for variable-length RGBA layer decomposition, trained on layers extracted from real PSD files (2025).
- [RevealLayer: Disentangling Hidden and Visible Layers via Occlusion-Aware Image Decomposition](https://arxiv.org/abs/2605.11818) - Decomposes natural images into RGBA layers and recovers occluded content; introduces the RevealLayer-100K dataset (ICML 2026).
- [See-through: Single-image Layer Decomposition for Anime Characters](https://arxiv.org/abs/2602.03749) - Decomposes an anime illustration into fully inpainted semantic layers with inferred drawing order for 2.5D animation (SIGGRAPH 2026).

### Layered image generation

- [ART: Anonymous Region Transformer for Variable Multi-Layer Transparent Image Generation](https://arxiv.org/abs/2502.18364) - Generates 50+ transparent layers from a global prompt and an anonymous region layout (CVPR 2025).
- [PrismLayers: Open Data for High-Quality Multi-Layer Transparent Image Generative Models](https://arxiv.org/abs/2505.22523) - Releases a 200K multi-layer transparent image dataset and the ART+ generation model (2025).
- [Text2Layer: Layered Image Generation using Latent Diffusion Model](https://arxiv.org/abs/2307.09781) - Generates background, foreground, layer mask and composite image together (2023).
- [Transparent Image Layer Diffusion using Latent Transparency](https://arxiv.org/abs/2402.17113) - LayerDiffuse: encodes alpha into the latent space so pretrained diffusion models can generate transparent images and layers (2024).

### Amodal completion and de-occlusion

- [Amodal Completion via Progressive Mixed Context Diffusion](https://arxiv.org/abs/2312.15540) - Training-free method that guides a pretrained inpainting model with context outside the object box to complete occluded objects (2023).
- [pix2gestalt: Amodal Segmentation by Synthesizing Wholes](https://arxiv.org/abs/2401.14398) - Diffusion model that reconstructs the whole shape and appearance of partially hidden objects (CVPR 2024).
- [Self-Supervised Scene De-occlusion](https://arxiv.org/abs/2004.02788) - Recovers occlusion order and completes the invisible parts of objects without ordering or amodal annotations (CVPR 2020).

## Building blocks

### Segmentation

- [SAM 3](https://github.com/facebookresearch/sam3) - Segment Anything with Concepts: detects, segments and tracks objects from text or visual prompts such as points, boxes and masks.
- [Segment Anything](https://github.com/facebookresearch/segment-anything) - The original promptable segmentation model (SAM), with inference code, checkpoints and example notebooks.

### Matting and background removal

- [BiRefNet](https://github.com/ZhengPeng7/BiRefNet) - High-resolution dichotomous image segmentation with matting variants; used by LayerD and available as a model in rembg.
- [rembg](https://github.com/danielgatis/rembg) - Background removal library and CLI with a choice of models, including U2-Net, IS-Net, BiRefNet and BRIA RMBG.
- [RMBG-2.0](https://huggingface.co/briaai/RMBG-2.0) - BRIA background removal model; gated weights, free for non-commercial use.

### Inpainting

- [FLUX.1 Fill \[dev\]](https://huggingface.co/black-forest-labs/FLUX.1-Fill-dev) - Rectified flow transformer (12B parameters) that fills masked areas from a text description; non-commercial license.
- [LaMa](https://github.com/advimman/lama) - Large-mask inpainting with Fourier convolutions that generalizes to resolutions around 2K; useful for filling the background after an object is cut out (WACV 2022).

### Depth

- [Depth Anything V2](https://github.com/DepthAnything/Depth-Anything-V2) - Monocular depth estimation; a depth map can help order extracted layers from front to back (NeurIPS 2024).

## PSD libraries

- [Adobe Photoshop File Formats Specification](https://www.adobe.com/devnet-apps/photoshop/fileformatashtml/) - Official description of the PSD and PSB file structure, including the layer and mask section.
- [ag-psd](https://github.com/Agamnentzar/ag-psd) - JavaScript library for reading and writing PSD files, including layers; RGB and 8 bits per channel only.
- [PhotoshopAPI](https://github.com/EmilDohne/PhotoshopAPI) - C++20 library with Python bindings on PyPI for reading and writing PSD and PSB files.
- [psd-tools](https://github.com/psd-tools/psd-tools) - Python package for reading PSD and PSB files and exporting layers to PIL or NumPy, with basic support for adding and removing pixel layers.
- [psd.js](https://github.com/meltingice/psd.js) - PSD parser for Node.js and browsers.
- [webtoon/psd](https://github.com/webtoon/psd) - Fast, zero-dependency TypeScript parser for PSD and PSB files in browsers and Node.js.

## Datasets

- [Crello](https://huggingface.co/datasets/cyberagent/crello) - Graphic design templates with document metadata and pre-rendered elements; a common benchmark for design layer decomposition (CDLA-Permissive-2.0).
- [MuLAn](https://huggingface.co/datasets/mulan-dataset/v1.0) - Over 44K instance-wise RGBA layer decompositions of COCO and LAION images (CC BY-NC-SA 4.0).
- [OmniPSD Layered Poster](https://huggingface.co/datasets/lc03lc/OmniPSD_Layered_Poster) - Subset of the layered poster dataset released with OmniPSD (Apache-2.0).
- [PrismLayersPro](https://huggingface.co/datasets/artplus/PrismLayersPro) - Curated set of 20K multi-layer transparent images with captions, taken from the 200K PrismLayers set (Apache-2.0).
- [RevealLayer-100K](https://huggingface.co/datasets/qihoo360/RevealLayer-100K) - Multi-layer natural images for occlusion-aware layer decomposition, together with the RevealLayerBench benchmark (Apache-2.0).

## Tutorials

- [How to separate an image into layers](https://image2layers.org/guides/how-to-separate-an-image-into-layers) - Compares three ways to split a flat JPG or PNG into layers: by hand in Photoshop, free in GIMP or Photopea, or with AI.
- [How to turn a flat image into an editable design with Magic Layers](https://www.canva.com/design-school/resources/how-to-edit-flat-images-with-magic-layers/) - Canva Design School walkthrough of Magic Layers.
- [psd-tools usage guide](https://psd-tools.readthedocs.io/en/latest/usage.html) - Opening a PSD in Python, modifying the layer structure and exporting layers to PIL or NumPy.
- [Qwen-Image-Layered ComfyUI workflow](https://docs.comfy.org/tutorials/image/qwen/qwen-image-layered) - Official ComfyUI example workflow for running Qwen-Image-Layered.

## Browser extensions

- [Image to Layer — example library (Chrome)](https://github.com/s07811005141-lang/image-to-layer-extension) - Browse layer-split examples offline; search by image type.

## Contributing

Contributions are welcome. Read the [contribution guidelines](CONTRIBUTING.md) first.

## License

[CC0 1.0](LICENSE). To the extent possible under law, the contributors have waived all copyright and related or neighboring rights to this work.
