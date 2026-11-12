# Marketscan models

Pinned copies of the on-device models the Marketscan app downloads, so the app never depends on a
third-party page staying up. Files live in this repo's **Releases**; the app checks every file by SHA-256.

| In the app | File(s) | Based on | License |
| --- | --- | --- | --- |
| Scan TSFModal | `scan-tsfmodal-c512-h128-w16.onnx` | Google Research TimesFM 2.5 200M, exported to ONNX with fp16 weights | Apache-2.0 |
| Scan AI | `scan-ai-e4b.litertlm.part1` + `.part2` (joined in order) | Google Gemma 4 E4B-it, LiteRT-LM build | Apache-2.0 |

Scan AI is split in two because GitHub caps a release asset at 2 GB. Join with
`cat scan-ai-e4b.litertlm.part1 scan-ai-e4b.litertlm.part2 > scan-ai-e4b.litertlm`.

## Updating a model

Publish a new release (never replace files in an old one), then bump the release tag, file names and SHA-256
values in `engine/src/main/kotlin/app/marketscan/engine/OnDevice.kt`. A phone or Mac that already has a model keeps
it; the new file reaches people who download it after the app update (or who tap Remove, then Download, in
Settings).
