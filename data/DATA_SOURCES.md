# Open Data Sources for a Dental Simulator & Learning App

Legal, open (or request-access) data to replace what commercial apps such as
Handpiece build in-house. **Check each licence before use**: several datasets
are research-only and must be cited.

Last checked: 2026-10-24

---

## 1. 3D tooth geometry (what you cut / view)

| Dataset | What it gives you | Size | Access / licence | Use in app |
|---|---|---|---|---|
| **Teeth3DS+** (3DTeethSeg / 3DTeethLand, MICCAI) | Intra-oral surface scans, each tooth segmented + FDI-labelled, plus landmarks | 1,800 scans, 900 patients, ~24k teeth | Free on request, see [project page](https://crns-smartvision.github.io/teeth3ds), [paper](https://arxiv.org/abs/2210.06094v3) | Crown surfaces, arch layout, landmark training |
| **ToothFairy2** (CVPR 2025) | CBCT volumes, 42 labelled classes: teeth, inferior alveolar canals, maxillary sinuses, pharynx, crowns, implants | 480 public volumes | Free account, cite papers, [page](https://ditto.ing.unimore.it/toothfairy2) | **OMFS module**: IAN canal, third molars, sinus, implants |
| **STS-Tooth** (Scientific Data 2025) | Panoramic X-rays + CBCT, tooth masks | 4,000 OPGs, ~31.8 GB | [Zenodo](https://zenodo.org/records/10597292) | Radiology module, AI tooth detection |
| **CTooth+** | CBCT, 22 fully annotated + 146 unlabelled volumes | small | [paper](https://astro.paperswithcode.com/paper/ctooth-a-large-scale-dental-cone-beam) | Root/whole-tooth volumes |
| **Micro-CT teeth (Zenodo, 2025)** | Enamel / dentin / pulp labels per tooth | n/a | Files restricted, request access: [Zenodo](https://zenodo.org/records/15038971) | **Most important for cutting sim** (layered tooth) |
| **Edinburgh micro-CT teeth** | Raw micro-CT, 22–26 µm voxels, unlabelled | n/a | [DataShare](https://datashare.ed.ac.uk/handle/10283/9165) | Segment enamel/dentin/pulp yourself in 3D Slicer |
| **Avizo molar sample** | One micro-CT molar with enamel/dentin/pulp/crack labels | 1 tooth | [Thermo Fisher](https://www.thermofisher.com/software-em-3d-vis/xtra-library/xtras/molar-segmentation-using-watershed-and-top-hat-and-surface-generation), licence unstated | Prototype tooth #1 |
| **NIH 3D upper teeth** | Printable upper arch model | 1 model | Public domain, [NIH 3D](https://3d.nih.gov/entries/3dpx-003002) | Quick placeholder |
| **Sketchfab human teeth** (A. Antipov) | Textured full set | 1 set | CC-BY, [Sketchfab](https://sketchfab.com/3d-models/human-teeth-c4c569f0e08948e2a572007a7a5726f2) | Visual mouth / gingiva |

**Best route to a Handpiece-quality layered tooth:** scan extracted teeth at your
own faculty (micro-CT or a lab CBCT), then segment enamel/dentin/pulp in
**3D Slicer** (free). You own that data, and the scan protocol is a publishable
methods paper.

---

## 2. Grading criteria (what "correct" means)

These come from textbooks, not app data: *Sturdevant's Art & Science of
Operative Dentistry*, *Wheeler's Dental Anatomy*. **Verify every value against
your faculty's preclinical manual before you encode it.**

### Class I amalgam
| Criterion | Target |
|---|---|
| Pulpal depth (from central groove) | 1.5–2.0 mm, ~0.2 mm into dentin |
| Isthmus width | As narrow as possible, ≤ ¼ intercuspal distance |
| Facial/lingual walls | Slightly convergent occlusally |
| Cavosurface angle | ~90° (no bevel for amalgam) |
| Remaining marginal ridge | ≥ 1.6 mm premolars, ≥ 2.0 mm molars |

### Class II amalgam, proximal box
| Criterion | Target |
|---|---|
| Axial wall depth | 0.2–0.5 mm into dentin |
| Proximal clearance from adjacent tooth (F, L, gingival) | ~0.2–0.5 mm (contact broken) |
| Gingival floor width (mesiodistal) | ~0.8 mm (≈ one #245 bur width) |
| Axiopulpal line angle | Rounded/beveled |
| Retention grooves (if used) | 0.2–0.3 mm deep, in dentin |

### Bur library
| Bur | Shape | Head dimensions |
|---|---|---|
| #245 | Inverted pear, carbide | 3.0 mm long, 0.8 mm tip diameter |
| #330 | Pear, carbide | ~1.5 mm long, 0.8 mm diameter |
| #169L | Tapered fissure, long | Verify with manufacturer catalogue |
| Round #2 / #4 | Round | ~1.0 / ~1.4 mm diameter (ISO 010 / 014) |
| Flame | Finishing diamond | Verify with manufacturer catalogue |

Exact bur geometry: manufacturer catalogues (Komet, SS White, Dentsply)
publish ISO head length and diameter for each bur.

---

## 3. Tooth anatomy reference values (Wheeler's, permanent teeth, mm)

Sample rows only. **Fill and verify the rest from Wheeler's Table of measurements.**

| Tooth | Crown length | Root length | MD crown | MD cervix | BL crown | BL cervix |
|---|---|---|---|---|---|---|
| Maxillary central incisor | 10.5 | 13.0 | 8.5 | 7.0 | 7.0 | 6.0 |
| Maxillary first molar | 7.5 | B 12 / L 13 | 10.0 | 8.0 | 11.0 | 10.0 |
| Mandibular first molar | 7.5 | 14.0 | 11.0 | 9.0 | 10.5 | 9.0 |

Numbering: support Universal, FDI, and Palmer (Handpiece shows all three);
FDI is standard in Germany.

---

## 4. Free tools to process the data

- **3D Slicer**: CBCT / micro-CT segmentation → STL
- **MeshLab / Blender**: clean, decimate, texture meshes
- **nnU-Net**: auto-segmentation (ToothFairy2 is already in nnU-Net format)
- **OpenVDB** or a custom voxel grid: material removal for cutting simulation

---

## 5. Data the app must collect itself (your research data)

- Student preparation scores per criterion, attempt number, and time taken
- With consent and ethics approval, this becomes the dataset for validation papers
  (simulator scores vs. phantom-head scores).
