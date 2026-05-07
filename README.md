# Tree Re-Identification Across Visits Challenge

## Background

[FloCard](https://flocard.app) is a sustainability-focused digital platform that combines digital identity, community engagement, climate action, and nature-based project tools. The platform supports businesses, communities, and sustainability initiatives through features such as digital business cards, sustainability profiles, carbon offsetting, project development, and tools aligned with climate and SDG goals.

FloCard also has a Tree Planters App used by communities, planters, and farms working on afforestation projects.

The app helps users digitally tag and trace trees using:

- geo-tagged single tree images
- Google Map based boundary tagging for clusters of trees or forest areas
- mobile app or mobile browser based field capture
- offline capture support for areas with low or no internet connectivity

Tree tagging usually happens in remote or low-connectivity areas. Users capture the tree image and location first. Later, when internet connectivity is available, the captured assets are synced and edited with details such as species, age, date of plantation, and related information. After review and approval, the tree record becomes a blockchain-based tree asset.

## Current Tree Tagging Flow

The tree asset creation process broadly follows three steps:

1. A user captures a tree image and geo-tag in the mobile app or mobile browser, often in offline mode.
2. The asset is synced later and edited with details such as species, age, plantation date, and other metadata.
3. The asset goes through an approval step before becoming a blockchain-based asset.

This process works, but long-term monitoring needs a way to understand whether images captured at different times refer to the same physical tree.

## Problem Statement

In afforestation and tree-tracking projects, the same tree may be revisited and photographed multiple times over months or years.

Images may differ because of:

- season
- lighting
- camera angle
- tree growth
- health changes
- partial occlusion
- background changes
- image quality

Without re-identification, duplicate tree assets may be created, or follow-up images may not be linked to the correct tree. This can affect monitoring, survival tracking, growth history, and carbon or GHG offset reporting.

FloCard is exploring an AI-assisted workflow where tree images captured across visits can be compared to estimate whether they likely represent the same physical tree.

## Challenge Objective

Build a solution that can compare tree images captured across different visits and suggest whether they likely refer to the same physical tree.

The solution should support human review rather than treating matches as final truth.

## Expected Outcome

A useful solution should be able to:

- accept image pairs or collections of tree images
- generate embeddings or comparable visual signatures
- rank possible same-tree matches
- provide similarity scores or confidence indicators
- support review of suggested matches
- export reviewed match decisions
- document the approach, assumptions, limitations, and failure cases

## Suggested Approach

Contributors are free to propose their own approach.

Possible approaches may include:

- visual embedding models
- image similarity search
- metric learning
- Siamese network style matching
- CLIP or DINO-style embeddings
- nearest-neighbor indexing
- optional use of non-sensitive metadata such as coarse site ID or visit date

The solution should explain why the selected approach is suitable and what kinds of image changes may reduce matching quality.

## Suggested Stack

Preferred languages:

- Python
- C#

Possible libraries and tools:

- OpenCV
- Pillow
- PyTorch
- TensorFlow
- Hugging Face
- OpenCLIP
- DINOv2
- FAISS
- scikit-learn
- ONNX Runtime
- ML.NET where applicable

Contributors may use other tools if they explain the reasoning.

## Data Access

Images are not included publicly in this repository unless they are open, synthetic, or approved for public use.

Contributors may use:

- open-license tree images
- contributor-created tree images
- approved sample image pairs or visit collections provided by the maintainers

Contributors who need access to image samples can contact the maintainers by email. Contact [abhijeet@366pitech.com]

Do not commit private geo-tagged images, precise location data, private farm or project data, credentials, or restricted-license imagery to the repository.

## Contribution Guidelines

- Fork the repository.
- Create a feature branch.
- Submit your Contribution through a pull request.
- Keep the implementation focused on this challenge.
- Do not commit private images, precise location data, credentials, or large generated datasets.
- Do not adapt this challenge for identifying or tracking people, faces, vehicles, license plates, or other sensitive subjects.
- Include setup and running instructions.
- Include sample output using safe, open, synthetic, or approved images.
- Explain your assumptions and known limitations.
- Mention any additional data you needed or data gaps you found.
- Document how the solution can be customized and scaled.

