# Shrubwise Data Challenge Submission

Main Repository https://github.com/ICharmU/shrub

Flowchart:

- Online access - [Lucid Chart](https://lucid.app/lucidchart/32a2e4fe-7cf1-4b10-921b-789723bfd876/edit?viewport_loc=-3172%2C-604%2C9084%2C4564%2C0_0&invitationId=inv_f4a3a702-681c-4030-95ef-ffcd3ce97884)

- PDF access under `/materials/flowchart.pdf`

## Executing the Notebooks

We provide two primary entry points:

1. **`submission_runner.ipynb`**: This is a streamlined, reproducible environment designed specifically for this submission.
   - **Setup**: First, create the required environment using: `conda create --name reproduce_env python=3.14.4`. Activate it, then install dependencies via `pip install -r requirements.txt`.
   - **Usage**: Run this notebook end-to-end to view our final model's performance metrics, predictions, and summary visualizations.
   - **Cloning main repo**: The notebook attempts to automatically clone the main repo (named shrub) into its own directory within this repo. If cloning doesn't work you will need to clone the [shrub repo](https://github.com/ICharmU/shrub) into this repository locally or download the shrub repo as a zip and extract into this repo.

2. **`main.ipynb` (Full Development Pipeline)**: This notebook lives in the main repository and acts as our central orchestration pipeline. It manages everything from data fetching and feature extraction to training and evaluation.

## Artifact Management & Storage Approach

Because the provided server environment was constrained to 5GB of storage, we could not store all point clouds, imagery, and intermediate features locally. To solve this, we implemented a custom artifact management system backed by Google Drive.

- **Google Drive Integration**: Our pipeline uses `pydrive2` to dynamically pull required data into memory and push intermediate artifacts (e.g., extracted features, labels) back to Google Drive to free up local disk space.
- **The Local `artifacts` Directory**:
  When running the pipeline, files are temporarily cached in the local artifact directories (e.g., `artifact_store_local/` and `shared_artifacts/`). The directory structure generally follows:
  ```text
  artifact_store_local/
  ├── features/          # Cached intermediate features (e.g., point cloud aggregations, chunks)
  ├── labeling/          # Generated masks and rasterized labels
  └── manifests/         # JSON tracking files that map data signatures to cache states
  ```

You may inspect this link as well for inspection into said Google Drive directory:
https://drive.google.com/drive/folders/1F9AtiUfx_z48tQIkNbDpzZUpH6R5uoCN?usp=drive_link
