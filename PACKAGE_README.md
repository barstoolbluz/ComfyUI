# ComfyUI Flox Package

This is a Flox package builder for ComfyUI - a powerful and modular visual AI engine with a node-based interface.

## Building the Package

```bash
# Enter the Flox environment
flox activate

# Build the ComfyUI package
flox build comfyui

# Test the built package
./result-comfyui/bin/comfyui --help
```

## Publishing to Flox Catalog

To publish your ComfyUI package to the Flox catalog:

1. **Login to Flox Hub**:
```bash
flox auth login
```

2. **Ensure Git is configured**:
```bash
git add .
git commit -m "Add ComfyUI Flox package"
git push origin main
```

3. **Publish the package**:
```bash
# Publish to your personal catalog
flox publish comfyui

# Or publish to an organization
flox publish -o myorg comfyui
```

## Using the Published Package

Once published, users can install your ComfyUI package:

```bash
# Install from your catalog
flox install barstoolbluz/comfyui

# The package provides these commands:
comfyui                    # Main ComfyUI launcher
comfyui-server              # Pre-configured server (listens on 0.0.0.0:8188)
comfyui-download-models     # Model downloader utility
```

## Important Notes

### Python Dependencies
This package provides the ComfyUI source code and launcher scripts. Users need to install Python dependencies separately:

```bash
# In their environment, users should install:
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu124
pip install -r requirements.txt
```

### Model Storage
Models are stored in `~/.comfyui/models/` by default. Users can override this with:
```bash
export COMFYUI_MODELS_DIR=/custom/path/to/models
```

## Package Structure

The built package includes:
- `/bin/comfyui` - Main launcher script
- `/bin/comfyui-server` - Server wrapper (0.0.0.0:8188)
- `/bin/comfyui-download-models` - Model download utility
- `/share/comfyui/` - Complete ComfyUI source code

## Development

To modify the package:

1. Edit `.flox/env/manifest.toml`
2. Rebuild with `flox build comfyui`
3. Test locally before publishing

## Build Variants

The manifest includes several build targets:

- `comfyui` - Main package (requires separate Python deps)
- `comfyui-standalone` - Package with vendored Python dependencies (larger but self-contained)
- `comfyui-docs` - Documentation package

Build specific variant:
```bash
flox build comfyui-standalone
```