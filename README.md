# 🧬 Protein Structure Visualizer

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/happyprotein/protein-visualizer/blob/main/protein_visualizer.ipynb)
![Python](https://img.shields.io/badge/Python-3.10+-blue?logo=python)
![License](https://img.shields.io/badge/License-MIT-green)
![Platform](https://img.shields.io/badge/Platform-Google%20Colab-orange?logo=google-colab)

An interactive, zero-install protein structure viewer and animation exporter that runs entirely in Google Colab. Upload any PDB or mmCIF file, or fetch structures directly from the RCSB Protein Data Bank — no local setup required.

---

## ✨ Features

| Feature | Details |
|---|---|
| 🔍 **Interactive 3D viewer** | Powered by py3Dmol — rotate, zoom, pan in the browser |
| 📂 **Flexible loading** | Upload `.pdb` / `.mmcif` files or fetch by 4-letter RCSB accession code |
| 🎨 **10 colour modes** | Rainbow, Neon, Pastel, Ocean, Fire, Sunset, Secondary structure, Spectrum, B-factor, CPK |
| 🧱 **5 representations** | Cartoon, Stick, Sphere, Line, Surface |
| 💊 **Ligand display** | Toggle HETATM ligands and water molecules independently |
| 🎬 **Animation export** | Export a full 360° rotation as **GIF** or **MP4** — server-side, no browser driver needed |
| 📊 **Structure stats** | Chain count, residue count, atom count, heteroatom count displayed on render |

---

## 🚀 Quick Start

### Option 1 — Open directly in Colab (recommended)

Click the badge at the top of this README, then:

```
Runtime → Run all
```

That's it. All dependencies install automatically in the first cell.

### Option 2 — Clone and run locally (Jupyter)

```bash
git clone https://github.com/YOUR_USERNAME/protein-visualizer.git
cd protein-visualizer
pip install -r requirements.txt
jupyter notebook protein_visualizer.ipynb
```

> ⚠️ The **Export Animation** feature uses `google.colab.files.download()` and will only trigger a browser download when running in Colab. In a local Jupyter environment the file is still saved to `/tmp/protein_rotation.gif` or `/tmp/protein_rotation.mp4`.

---

## 📸 Usage

### Visualizing a structure

1. **Load** — upload a file or type a PDB ID (e.g. `6LU7`) and click **Fetch from RCSB**
2. **Style** — choose a representation and colour mode from the dropdowns
3. **Render** — click **Render / Update**

### Exporting a rotation animation

After rendering:

1. Choose **Format** (GIF or MP4), **Duration**, and **FPS**
2. Click **Export Animation**
3. Watch the progress bar — frames are rendered server-side in Python
4. The file downloads automatically when complete

---

## 🎨 Colour Modes

| Mode | Description |
|---|---|
| Rainbow / Neon / Pastel / Ocean / Fire / Sunset | Vivid explicit hex colours, one per chain |
| Secondary structure | Helix = red, Sheet = yellow, Loop = green |
| Spectrum (N to C) | Blue at N-terminus fading to red at C-terminus |
| B-factor | Blue (rigid/low) → red (flexible/high) |
| Element (CPK) | Standard atom-type colouring |

---

## 🧬 Test Structures

| PDB ID | Description | Good for |
|---|---|---|
| `1CRN` | Crambin | Quick test — tiny and fast |
| `6LU7` | SARS-CoV-2 Mpro + N3 inhibitor | Ligand display |
| `1HHO` | Oxyhaemoglobin | Multi-chain colour palettes |
| `4HHB` | Deoxyhaemoglobin | Quaternary structure |
| `1BNA` | B-DNA dodecamer | Nucleic acid structure |

---

## 🛠️ Dependencies

All installed automatically by Cell 1:

```
py3Dmol        — WebGL-based molecular viewer
biopython      — PDB/mmCIF parsing and structure analysis
ipywidgets     — Interactive UI widgets
imageio        — GIF and MP4 encoding
imageio-ffmpeg — MP4 codec support
Pillow         — Frame compositing for GIF export
matplotlib     — Server-side 3D ribbon renderer for export
```

---

## 📁 Repository Structure

```
protein-visualizer/
├── protein_visualizer.ipynb   # Main notebook
├── requirements.txt           # Python dependencies
├── README.md                  # This file
└── LICENSE                    # MIT License
```

---

## 🔬 How the Export Works

The export pipeline is entirely server-side — it does **not** try to capture the py3Dmol browser canvas (which is sandboxed inside a Colab iframe and inaccessible to JavaScript).

Instead:

1. **BioPython** parses the structure and extracts Cα backbone coordinates
2. **Matplotlib 3D** renders each frame — drawing a ribbon-style backbone coloured by secondary structure, with CPK ligand spheres and bond sticks
3. **imageio** encodes the frames into GIF (Pillow) or MP4 (libx264)
4. **`google.colab.files.download()`** triggers the browser download

This approach works reliably on every Colab runtime without any browser driver dependencies.

---

## 📄 License

MIT License — see [LICENSE](LICENSE) for details.

---

## 🤝 Contributing

Contributions are welcome! Ideas for future features:

- [ ] Residue-level selection and highlighting
- [ ] Distance measurement tool
- [ ] DSSP secondary structure assignment integration
- [ ] Multi-structure overlay / alignment
- [ ] PNG snapshot export

Please open an issue or submit a pull request.

---

## 📬 Contact

Made with ❤️ for structural biology and bioinformatics.  
Questions or suggestions? Open an [issue](https://github.com/YOUR_USERNAME/protein-visualizer/issues).
