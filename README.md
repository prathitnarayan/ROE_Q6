# Matrix Build Workflow Demo

**Email:** 25ds2000019@ds.study.iitm.ac.in

## Overview

This repository demonstrates a GitHub Actions workflow with:
- **Matrix Build Strategy**: 6 parallel build jobs (3 OS × 2 Node versions)
- **Artifact Management**: Each build generates and uploads unique artifacts
- **Cross-Platform Testing**: Ubuntu, macOS, and Windows builds

## Workflow Features

### Matrix Configuration
- **Operating Systems**: Ubuntu, macOS, Windows
- **Node.js Versions**: 18 (LTS), 20 (Current)
- **Total Combinations**: 6 parallel jobs

### Generated Artifacts
Each matrix job creates artifacts with the prefix `build-4a5eacb-` followed by:
- `linux-lts` - Ubuntu with Node 18
- `linux-current` - Ubuntu with Node 20
- `macos-lts` - macOS with Node 18
- `macos-current` - macOS with Node 20
- `windows-lts` - Windows with Node 18
- `windows-current` - Windows with Node 20

### Artifact Contents
Each artifact contains:
1. `build-info.txt` - Build metadata and system information
2. `metadata.json` - Structured build data in JSON format
3. `config.js` - JavaScript configuration export
4. `build.log` - Build process log

## Setup Instructions

1. **Create Repository**
   ```bash
   mkdir matrix-workflow-demo
   cd matrix-workflow-demo
   git init
   ```

2. **Create Workflow Directory**
   ```bash
   mkdir -p .github/workflows
   ```

3. **Add Workflow File**
   - Copy the workflow YAML content
   - Save as `.github/workflows/matrix-build.yml`

4. **Add README**
   - Copy this README content
   - Update the email address at the top
   - Save as `README.md`

5. **Commit and Push**
   ```bash
   git add .
   git commit -m "Add matrix build workflow"
   git branch -M main
   git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO.git
   git push -u origin main
   ```

## Triggering the Workflow

The workflow runs automatically on:
- Push to `main` or `master` branch
- Pull requests to `main` or `master` branch
- Manual trigger via GitHub Actions UI (workflow_dispatch)

### Manual Trigger
1. Go to your repository on GitHub
2. Click **Actions** tab
3. Select **Matrix Build with Artifact Management**
4. Click **Run workflow** button
5. Select branch and click **Run workflow**

## Verification

After the workflow completes, verify:

✅ **6 successful matrix jobs** (3 OS × 2 Node versions)  
✅ **6 artifacts uploaded** with `build-4a5eacb-` prefix  
✅ **All artifacts contain content** (4 files each)  
✅ **Step identifier** `matrix-4a5eacb` present in logs  
✅ **README.md** contains email address  

### Viewing Artifacts
1. Go to the **Actions** tab
2. Click on the completed workflow run
3. Scroll to the **Artifacts** section at the bottom
4. Download and inspect each artifact

## Workflow Details

### Matrix Strategy
```yaml
strategy:
  matrix:
    os: [ubuntu-latest, macos-latest, windows-latest]
    node-version: [18, 20]
```

### Required Step
```yaml
- name: matrix-4a5eacb
  run: |
    echo "🚀 Building for OS: ${{ matrix.os }}"
    echo "📦 Node version: ${{ matrix.node-version }}"
```

### Artifact Upload
```yaml
- name: Upload build artifact
  uses: actions/upload-artifact@v4
  with:
    name: build-4a5eacb-${{ matrix.artifact-suffix }}
    path: build-output/
```

## Additional Features

### Verification Job
The workflow includes a `verify-artifacts` job that:
- Downloads all generated artifacts
- Lists and verifies their contents
- Generates a summary report in the GitHub Actions UI

### Build Summary
Each workflow run generates a summary showing:
- All artifacts created
- Total artifact count
- Build status for each matrix combination

## Customization

You can modify the matrix to test different combinations:
- Add more OS versions
- Include different Node.js versions
- Add build configurations or feature flags
- Test multiple programming languages

Example:
```yaml
strategy:
  matrix:
    os: [ubuntu-latest, macos-latest, windows-latest]
    node-version: [16, 18, 20, 21]
    build-type: [debug, release]
```

## License

MIT License - feel free to use and modify as needed.

## Support

For issues or questions about this workflow, please open an issue in this repository.
