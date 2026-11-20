# PostFace

**Flow-Guided Adversarial Face Editing for Postable Social Photo Privacy**

![PostFace](./FLUX_Guard/src/image.PNG)

## Authors

Jie Wang (Beijing University of Posts and Telecommunications, WangJie2023@bupt.edu.cn), Tao Wang (Nanjing University of Aeronautics and Astronautics, wangtao21@nuaa.edu.cn), Ru Zhang (Beijing University of Posts and Telecommunications, zhangru@bupt.edu.cn).

## Abstract

Social photo sharing has become a major form of online self-presentation, while users increasingly seek to curate their facial appearance. However, faces posted on public platforms remain exposed to face recognition (FR) systems, leading to unauthorized identity linkage and associated privacy risks. Existing adversarial facial privacy methods are often constrained by fixed visual styles or source-preserving objectives, limiting their applicability to social photo sharing, where users seek personalized appearance curation. We therefore consider postable social photo privacy to require visual shareability, personalized appearance expression, and protection against unauthorized FR systems. To address these limitations, we introduce PostFace, a flow-guided adversarial face editing scheme for postable social photo privacy. It employs flow-trajectory control to align semantic manipulation with the generation process, enabling personalized facial editing, and performs perceptual-adaptive latent optimization to achieve identity protection through appearance-compatible edits. Experiments on public datasets and commercial FR APIs demonstrate competitive performance in identity protection and black-box transferability. Furthermore, PostFace remains highly effective after actual social-media processing and exhibits advanced postability in social-sharing scenarios.

## Prepare Model Checkpoints

### 1. Victim Face Recognition Models

Download the pretrained weights for the victim models from [here](https://drive.google.com/file/d/19_Y0jR789BGciogjjoGtWNEv-5QBiCB7/view) and extract them into `./models`.

### 2. FLUX.1-dev

Download the FLUX.1-dev model from [Hugging Face](https://huggingface.co/black-forest-labs/FLUX.1-dev).

### 3. BiSeNet (Face Parsing)

Download the pretrained BiSeNet checkpoint (`79999_iter.pth`) from the [official face-parsing repository](https://github.com/zllrunning/face-parsing.PyTorch).

- [Google Drive Download](https://drive.google.com/open?id=154JgKpzCPW82qINcVieuPH3fZ2e0P812)
- [Hugging Face Mirror](https://huggingface.co/vivym/face-parsing-bisenet/blob/main/79999_iter.pth)

Save the downloaded checkpoint as `./models/bisenet/79999_iter.pth` and update the checkpoint path in the configuration accordingly.

### 4. VGG-19 (Perceptual Feature Extraction)

Download the pretrained VGG-19 weights (ImageNet-1K):

- [VGG-19 Pretrained Weights](https://download.pytorch.org/models/vgg19-dcbb9e9d.pth)
- [Torchvision Model Documentation](https://docs.pytorch.org/vision/stable/models/generated/torchvision.models.vgg19.html)

The checkpoint corresponds to `VGG19_Weights.IMAGENET1K_V1`.

When using the corresponding Torchvision pretrained-weight interface, the weights can also be downloaded automatically.

### 5. SBERT (Prompt-to-Region Semantic Matching)

Download the pretrained `all-mpnet-base-v2` model:

- [Hugging Face Model Repository](https://huggingface.co/sentence-transformers/all-mpnet-base-v2)

Alternatively, download it locally using:

```bash
pip install -U huggingface_hub

hf download sentence-transformers/all-mpnet-base-v2 \
    --local-dir ./models/all-mpnet-base-v2
```

Update `LOCAL_SBERT_PATH` in `auto_mask.py` to point to the downloaded model directory.

## Run the Code

```bash
python FLUX_Guard/src/runfluxguard.py
```
