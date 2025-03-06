# Identified Gaps in g3t Functionality

## Associating a single file metadata entry with multiple links

In the PDAC-HTAN user journey, there will be a point where a file will need to be transferred across the OHSU firewall into the Fortera bucket.

We want to be able to support referencing to multiple files?

(counterargument: if we are transferring from external to internal, why don't we just have a different project name for that?)

## [Untested to my Knowledge] Associating existing files with metadata

The Cambridge user journey is the reverse of the PDAC-HTAN use case: Given that external files have already been uploaded to OHSU buckets, can we attach self-supplied metadata to the existing file manifest / file metadata? This might work in g3t but to my knowledge (QW) it is untested and there is no go-to workflow for this situation.

## Creating a git-like source of truth data project

In the SMMART and PDAC-HTAN user journey for example, [multiple] users will want to iteratively upload data to a single project. This is a two-pronged request, where...

1. In order to resolve conflicts and ensure that all of their data is accurately maintained, we need a system to pull and push.
2. Given that system to pull and push, we also need to enforce guardrails to ensure that a user is not overwriting another users set of data