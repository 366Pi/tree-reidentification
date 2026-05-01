# Tree Re-Identification Across Visits Scenario

## Overview

Build a self-contained tree re-identification prototype that estimates whether tree images captured at different times likely refer to the same physical tree.

This scenario should support repeat monitoring and longitudinal tree inventory workflows using open, synthetic, or contributor-created imagery and optional non-sensitive metadata. It should not depend on a separate detection or identification project, internal Canopy tracking logic, private imagery, or private location data.

## What Problem It Solves

Tree monitoring often needs to compare observations across visits: the same tree may be photographed from different angles, in different seasons, or under different lighting. Re-identification helps determine whether two observations likely refer to the same physical tree so changes in condition can be tracked over time.

The goal is not to build a production identity graph or guaranteed tree matching system. The goal is to create a limited-scope reference implementation for tree image embeddings, candidate matching, review, and evaluation.

## Scope

The implementation should include:

- local upload or folder-based ingestion of tree image sets
- support for image pairs or multi-visit image collections
- optional non-sensitive metadata such as approximate site ID, visit ID, timestamp, or coarse location bucket
- embedding generation for tree images or tree crops
- similarity search or ranked candidate matching
- same-tree / different-tree prediction output
- lightweight review UI, static gallery, or notebook for accepting or rejecting matches
- reviewed match export
- evaluation script using labeled same/different pairs where available
- documentation for setup, usage, assumptions, and limitations

## Non-Goals

This work packet is not intended to cover:

- private field imagery or customer datasets
- precise private GPS tracking
- person, vehicle, face, or surveillance re-identification
- production identity graph management
- guaranteed tree identity resolution
- internal Canopy tracking logic
- tree detection, segmentation, or species classification as required dependencies
- carbon estimation or ESG reporting

## Expected Deliverables

A complete contribution should include:

- working local re-identification prototype
- sample open/synthetic/contributor-created image pairs or collection setup instructions
- embedding generation workflow
- similarity search or matching workflow
- match output schema
- visual review UI, gallery, or notebook
- reviewed match export format
- evaluation script and sample evaluation output where labels exist
- setup and running documentation
- notes on assumptions, failure cases, and limitations

## Success Criteria

A submission will be considered successful if:

- it runs locally without private internal APIs
- it uses open, synthetic, or contributor-created imagery only
- it generates embeddings for tree images or crops
- it produces ranked candidate matches with similarity scores
- reviewers can accept, reject, or mark candidate matches as uncertain
- reviewed match decisions can be exported
- top-k accuracy or a similar retrieval metric is reported when labeled pairs are available
- failure cases such as season change, occlusion, similar neighboring trees, camera angle, and poor image quality are documented

## Suggested Stack

Preferred stack:

- Python
- PyTorch / Hugging Face
- OpenCLIP, DINOv2, ResNet/ViT embeddings, or similar open tooling
- FAISS or scikit-learn nearest neighbors
- Streamlit, Gradio, static HTML, or notebook-based review where useful
- JSON, JSONL, or CSV for match and review outputs

## Output Contract

The implementation should export re-identification results in a documented format. A useful minimal shape is:

```json
{
  "query_image_id": "string",
  "query_source_file": "string",
  "method": "tree_reidentification",
  "candidate_matches": [
    {
      "candidate_image_id": "string",
      "candidate_source_file": "string",
      "similarity_score": 0.0,
      "rank": 1,
      "metadata_used": {
        "site_id": "string",
        "visit_id": "string",
        "timestamp": "string"
      },
      "review": {
        "status": "pending | same_tree | different_tree | uncertain",
        "reviewer_notes": "string"
      }
    }
  ],
  "run_metadata": {
    "embedding_model": "string",
    "model_version": "string",
    "index_type": "string",
    "runtime": "local | hosted",
    "latency_ms": 0
  }
}
```

## Design Notes

This packet should remain independent. It may optionally use tree crops if supplied, but it must also support ordinary image-folder input or image-pair input.

The intended flow is:

```text
Tree image collection
-> local ingestion
-> embedding generation
-> similarity search
-> ranked candidate matches
-> human review
-> reviewed match export
```

Optional metadata should only be used to improve candidate ranking or filtering. The visual matching workflow should still be understandable without private location data.

## Safety and Data Notes

Do not include private field imagery, precise private GPS data, customer imagery, restricted-license datasets, or internal Canopy data.

This scenario is only for tree re-identification. It must not be adapted to identify or track people, faces, vehicles, license plates, or other sensitive subjects.

## Submission Guidelines

- Fork the repository and create a feature branch for your contribution.
- Submit your work through a pull request against the main repository. Do not submit code, imagery, annotations, location files, or datasets through email, chat, or shared drives.
- Open an issue first if your proposed approach changes the scope materially, introduces a major dependency, requires a hosted service by default, or needs a different runtime than the one described in this README.
- Include a short solution approach in the pull request that explains the embedding model, matching strategy, metadata use, review workflow, design tradeoffs, and known limitations.
- Include architecture documentation that shows the main components, data flow, configuration files, local storage, embedding/index files, and output artifacts. A simple diagram is preferred where useful.
- Include setup and running instructions that allow a reviewer to run the project from a clean checkout.
- Include deployment notes, even if the project only runs locally. State the expected runtime, environment variables, model setup, index storage, and optional services.
- Include scaling notes that explain what would need to change for larger image collections, approximate nearest neighbor indexing, batch embedding generation, GPU execution, cloud storage, queues, or managed compute.
- Include integration notes describing how match outputs could later feed longitudinal tree monitoring, review workbenches, or inventory analytics without depending on hidden internal APIs.
- Include code documentation for public functions, configuration options, CLI commands, model inputs, metadata fields, data formats, review states, and export formats.
- Include sample inputs and outputs using open, synthetic, or contributor-created imagery only.
- Include tests or validation checks for core behavior, such as image loading, embedding export, candidate ranking, output schema validation, review state handling, and error handling.
- Include a short quality report or evidence section showing sample runs, known failure cases, and how reviewers should inspect outputs.
- Keep secrets, credentials, API keys, generated caches, local model files, large generated outputs, location files, and local environment files out of the repository.
- Add or update `.gitignore` where needed to prevent accidental submission of local data, model artifacts, generated files, location files, or credentials.
- Use clear commit messages and keep unrelated refactors out of the pull request.
- The pull request should be reviewable as a standalone contribution: reviewers should not need access to internal roadmaps, private datasets, or proprietary platform details to understand or run it.

