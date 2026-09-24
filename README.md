<h1 align="center">Guillaume Cassez</h1>
<p align="center">
  <em>AI Engineer · Independent research · Medical imaging &amp; Autonomous driving</em>
</p>

<p align="center">
  <a href="https://guillaume-cassez.fr">guillaume-cassez.fr</a> ·
  <a href="https://orcid.org/0009-0007-0987-3931">ORCID</a> ·
  <a href="https://zenodo.org/search?q=metadata.creators.name%3A%22Cassez%2C%20Guillaume%22">Zenodo (5 papers)</a> ·
  <a href="https://openalex.org/A5134353579">OpenAlex</a> ·
  <a href="https://huggingface.co/GuillaumeCassez">🤗 Weights</a> ·
  <a href="https://www.linkedin.com/in/guillaume-cassez/">LinkedIn</a>
</p>

---

### About

AI Engineer based in **Amiens, France**, with a domain-aware and application-driven approach to deep learning. I focus on **practical performance over headline benchmarks**, and on **clinically meaningful metrics** over aggregate scores.

My research habit is the hard one: **evaluate under the official challenge metrics** (BraTS-2023 lesion-wise Dice/HD95, Cityscapes official mIoU), on **full 5-fold cross-validation**, with a **pre-specified primary endpoint**, Holm correction, effect sizes and bootstrap CIs — and **publish the null results in full**. Two of the five papers below report a loss that does *not* beat its baseline alone; what they establish is where it sits and what it is worth in combination.

- **Medical imaging** — 3D brain tumour segmentation (BraTS 2023 GLI, MedNeXt-B / nnU-Net v2, 1 196 patients): auxiliary losses (signed-distance transform, Kervadec boundary, blob), expert-initialised mixture-of-experts, parameter-free connected-component consensus.
- **Autonomous driving** — full-resolution Cityscapes segmentation (ConvNeXt-V2 + UPerNet): controlled 2×2 loss ablations, 4 configurations × 3 seeds, 160 epochs.
- **Production ML** — customer call transcription pipeline with `faster-whisper` (local GPU inference).
- **Founder of ImmoIA**, a PropTech AI product.

### Publications — 5 papers, all open access with a DOI

| Paper | Task · scale | Headline result (official metrics) | Artefacts |
|---|---|---|---|
| **1 · Two Models That Agree Beat the Best of Them Alone** (v10, 2026-09-22) | BraTS 2023 GLI · 5-fold CV, n = 1 196 | A parameter-free connected-component consensus is the only configuration that beats the baseline on both official ranking metrics: lesion-wise Dice **+0.024** (Holm p = 4.5×10⁻¹⁶), lesion-wise HD95 **−9.49 mm** (Holm p = 5.7×10⁻²⁶), ~41 % fewer spurious lesions at negligible recall cost | [DOI](https://doi.org/10.5281/zenodo.19695263) · [code](https://github.com/guillaume-cassez/brats-moe-distmap-fusion-1) · [page](https://guillaume-cassez.fr/imagerie-medicale/brats/2023-distance-map/) · weights [baseline](https://huggingface.co/GuillaumeCassez/mednext-baseline-brats2023gli) / [distmap](https://huggingface.co/GuillaumeCassez/mednext-distmap-brats2023gli) |
| **2 · Precision Pays** (v2.6, 2026-09-22) | BraTS 2023 GLI · 5-fold CV, n = 1 196 + 3 seeds | Fixed-weight boundary loss (λ = 0.05) is **null alone** (lesion-wise Dice +0.000, Holm p = 0.34) but is the precision mirror of the SDT head — and wins as a consensus veto: lesion-wise HD95 **−9.95 mm** (p = 2.3×10⁻²⁰) vetoing the SDT model, lesion-wise Dice WT **+3.89 pp** (p = 0.005) as primary model with a baseline veto | [DOI](https://doi.org/10.5281/zenodo.22906446) · [page](https://guillaume-cassez.fr/imagerie-medicale/brats/boundary-loss-kervadec/) · [PDF](https://guillaume-cassez.fr/imagerie-medicale/brats/boundary-loss-kervadec/paper.pdf) · [weights](https://huggingface.co/GuillaumeCassez/mednext-kervadec-brats2023gli) |
| **3 · The Gate Does Not Choose** (v0.13, 2026-09-22) | BraTS 2023 GLI · 29 arms × 5 folds, 239 patients/fold | An expert-initialised patch-wise MoE is the best arm of the study: **+0.0057** lesion-wise Dice over its own baseline averaged over 5 folds, positive on **5/5**, above the pre-declared smallest effect of interest (0.003) on **4/5**; the best of 24 training-free consensus operators reaches only +0.0013 (gate margin **+0.0044** = 1.5× SESOI) — yet routing stays near-uniform, so the gate does not choose | [DOI](https://doi.org/10.5281/zenodo.22776410) · [page](https://guillaume-cassez.fr/imagerie-medicale/brats/consensus-vs-moe/) · [PDF](https://guillaume-cassez.fr/imagerie-medicale/brats/consensus-vs-moe/paper.pdf) · [weights](https://huggingface.co/GuillaumeCassez/mednext-moe-v3-brats2023gli) |
| **4 · Boundary Loss Ablation for Full-Resolution Cityscapes** (v0.2.2, 2026-06-28) | Cityscapes 1024×2048 · 4 configs × 3 seeds, 160 ep | CE+Boundary reaches the best mean mIoU **81.69 ± 0.25** (Boundary F1 77.32 ± 0.13) and beats the field-standard CE+Dice under Holm (p = 0.032) on a paired image-bootstrap over the 500 val images | [DOI](https://doi.org/10.5281/zenodo.20528680) · [code](https://github.com/guillaume-cassez/city-scape) · [page](https://guillaume-cassez.fr/voiture-autonome/cityscapes/boundary-loss-kervadec/) · [weights](https://huggingface.co/GuillaumeCassez/cityscape-boundary-loss-kervadec) |
| **5 · Distance-Map Auxiliary Regression for Full-Resolution Cityscapes** (v0.1.0, 2026-06-28) | Cityscapes 1024×2048 · 4 configs × 3 seeds, 160 ep | CE+DistMap (SDT auxiliary head, dropped at inference → zero test-time cost) reaches the best mean mIoU **81.64 ± 0.27**, beating CE+Dice (Holm p = 0.046) and the joint variant (p = 0.001) | [DOI](https://doi.org/10.5281/zenodo.21006235) · [code](https://github.com/guillaume-cassez/cityscape-distmap-aux-regression) · [page](https://guillaume-cassez.fr/voiture-autonome/cityscapes/distmap-aux-regression/) · [weights](https://huggingface.co/GuillaumeCassez/cityscape-distmap-aux-regression) |

Concept DOIs are cited above: they always resolve to the latest version of each deposit. Co-author on the three BraTS papers: Stanislas Larnier (methodological guidance and reviews).

### Interactive artefacts

- 🧠 **[3D BraTS viewer](https://guillaume-cassez.fr/imagerie-medicale/brats/2023-distance-map/viewer/)** — 1 196 patients, 4 experts, 12 consensus operators and the patch-wise MoE, side by side with ground truth (webgl, no install).
- 📊 **[Per-patient ranking](https://guillaume-cassez.fr/imagerie-medicale/brats/2023-distance-map/ranking/)** — Dice and HD95 for every one of the 1 196 validation cases, sortable and filterable.
- 🚗 **[Cityscapes viewer](https://guillaume-cassez.fr/voiture-autonome/cityscapes/viewer/)** — full-resolution predictions explorer.
- 🤗 **[Model weights on Hugging Face](https://huggingface.co/GuillaumeCassez)** — 5-fold MedNeXt-B checkpoints (BraTS: baseline, DistMap, Kervadec boundary-loss, MoE-V3) and 3-seed ConvNeXt-V2+UPerNet checkpoints (Cityscapes), `safetensors`, MIT.

### Tech I work with

`PyTorch` · `nnU-Net v2` · `MedNeXt` · `mmsegmentation` · `faster-whisper` · `Three.js` · `Next.js` · `TypeScript` · `Docker` · `Docker Swarm` · `FastAPI` · `AWS S3/CloudFront`

### Hardware

Workstation Ryzen 9950X3D + **RTX PRO 6000 Blackwell 96 GB** + RTX 3090. Local-first ML training and inference.

### Available for

MedTech R&D positions in France (AZmed, Gleamer, Pixyl, Owkin, Therapixel, Hera-MI, Milvue, Incepto, Raidium, etc.).

📫 [cassez.guillaume@gmail.com](mailto:cassez.guillaume@gmail.com)
