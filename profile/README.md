# VeriTrace: Blockchain-Backed Content Provenance

VeriTrace is a decentralized content provenance protocol that establishes an immutable chain of custody for digital media to combat deepfakes, plagiarism, and metadata tampering.

## The Architecture
The ecosystem is built using a hybrid Layer-2 ledger and off-chain inference pipeline:
- **Smart Contract Registry** (Arbitrum Sepolia L2 via Rust Stylus SDK): Stores immutable anchors containing cryptographic SHA-256 and visual pHash signatures at near-zero gas costs.
- **Hashing & AI Services Engine**: Computes visual pHash, structural Simhash, semantic embeddings (CLIP), face geometric coordinates (InsightFace), and speaker patterns (Wav2Vec2).
- **Core Backend Orchestrator**: Manages off-chain metadata, Qdrant vector indexing, caching, and evaluation flow (deepfake checks, temporal integrity, and heatmaps).

## Active Repositories
- [**veritrace-backend**](https://github.com/VetiTrace-Lampros-Dao/veritrace-backend): Core API router, Redis cache, and Qdrant indexer.
- [**veritrace-hashing-ai**](https://github.com/VetiTrace-Lampros-Dao/veritrace-hashing-ai): Processing engine executing FFmpeg splitting, LibreOffice doc parsing, and PyTorch models.
- [**contract**](https://github.com/VetiTrace-Lampros-Dao/contract): WASM smart contract registry managing L2 content verification and dataset escrow-licensing.
- [**Veritrace-Frontend**](https://github.com/VetiTrace-Lampros-Dao/Veritrace-Frontend): Creators' dashboard to register assets, view provenance reports, and purchase access.
- [**veritrace-extension**](https://github.com/VetiTrace-Lampros-Dao/veritrace-extension): Chrome extension providing instant in-page verification badges for web images.

## Verification Flow
1. **Anchor**: Creator uploads file via Dashboard -> registers on Arbitrum Sepolia.
2. **Verify**: Verifier scans image (using Dashboard or Chrome Extension) -> Core Backend queries Qdrant & EVM.
3. **Auditing**: Match metrics are evaluated: pHash (Visual >= 65.6%), CLIP (Semantic >= 85.0%), InsightFace (Face >= 60.0%), and Wav2Vec2 (Audio >= 99.9%).
4. **Alerts**: System outputs similarity scores, alteration heatmaps, and flags AI deepfakes (e.g. audio-visual speech mismatch).
