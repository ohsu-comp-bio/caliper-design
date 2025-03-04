# `g3t`

`g3t` (gen3-tracker) is a command-line utility that facilitates data sharing on the CALIPER platform.

## Guides

- [Install `g3t`](./install)
- [Upload Files](./upload.md)
- [Download Files](./download.md)

# Comparisons

| Operation         | g3t                       | git        | git-lfs | dvc  |
| ----------------- | ------------------------- | ---------- | ------- | ---- |
| Adding Files      | `g3t add`                 | `git add`  | TODO    | TODO |
| Uploading Files   | `g3t push`                | `git push` | TODO    | TODO |
|                   | `g3t push --step upload`  |            |         |      |
|                   | `g3t push --step publish` |            |         |      |
| Downloading Files | `g3t pull`                | `git pull` | TODO    | TODO |
