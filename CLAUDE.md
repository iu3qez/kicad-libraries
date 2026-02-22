# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a custom KiCad component library repository. Components are imported from EasyEDA/LCSC using [`easyeda2kicad.py`](https://github.com/uPesy/easyeda2kicad.py) and stored here for use in KiCad PCB design projects.

## Library Structure

KiCad libraries use a three-part convention, all sharing the same base name (`kicad-libraries`):

- **`kicad-libraries.kicad_sym`** — Schematic symbol library (single file, all symbols concatenated in KiCad S-expression format)
- **`kicad-libraries.pretty/`** — PCB footprint library (one `.kicad_mod` file per component)
- **`kicad-libraries.3dshapes/`** — 3D model assets (`.step` and `.wrl` pairs per component, referenced by footprints)

## Adding Components

Components are imported from EasyEDA using the LCSC part number:

```bash
# Install the tool if needed
pip install easyeda2kicad

# Import a component (e.g., LCSC part C5366877)
easyeda2kicad --full --lcsc_id C5366877 --output kicad-libraries
```

The `--full` flag imports symbol, footprint, and 3D model together. The `--output` flag must match the base library name so files land in the correct locations.

## KiCad Integration

In KiCad, add this repository as a library:
- **Symbols**: `Preferences > Manage Symbol Libraries` → add `kicad-libraries.kicad_sym`
- **Footprints**: `Preferences > Manage Footprint Libraries` → add `kicad-libraries.pretty/`
- **3D Models**: Referenced automatically via relative paths in footprint files

## Git Commits

When committing, do **not** add a `Co-Authored-By: Claude` trailer. Commit messages should be plain, without any AI co-author attribution.

## File Formats

- `.kicad_sym` — KiCad S-expression symbol library (text-based, version 20211014+)
- `.kicad_mod` — KiCad S-expression footprint (text-based)
- `.step` / `.wrl` — Standard 3D model formats (STEP for mechanical, WRL for KiCad rendering)
