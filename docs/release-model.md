# Public release model

This repository contains public product material and release assets. The application source remains in a separate private repository.

## Tags and GitHub Releases

Create public release tags on commits in this documentation/distribution repository only. **Do not push a tag that points to a commit in the private source repository.** A Git tag identifies a commit and its tree; publishing a source tag here could expose the full source snapshot through the tag archive.

A public release can use the same product version as the private build while pointing to a documentation-only commit in this repository. Attach the prebuilt artifacts to that release:

- the versioned deployment bundle and SHA-256 checksum;
- the standalone sandbox-worker archive and checksum;
- release notes with supported runtime/provider versions;
- exact GHCR image names and tags;
- applicable `LICENSE`, `NOTICE`, and third-party notices.

Build and verify the images and archives in the private source repository. To upload a release asset to this separate public repository, its publishing workflow needs narrowly scoped write permission for this repository; the private repository's default `GITHUB_TOKEN` does not automatically grant cross-repository write access. Store any cross-repository credential only as an Actions secret, never in the bundle or public repository.

## Container images

Publish versioned images under the intended public namespace, for example `ghcr.io/bladexxx/oma-main-node:<version>` and `ghcr.io/bladexxx/oma-vault:<version>`. Set each GHCR package's visibility to public before announcing the release. Keep the image references in the deployment bundle pinned to the same release version; avoid using `latest` as the deployment default.

## Release checklist

- Confirm the bundle contains deployment configuration and binaries only, with no source checkout, private `.env`, logs, database, or runtime artifacts.
- Confirm the server, Vault, and sandbox-worker artifacts were built from the intended version and are compatible with one another.
- Verify checksums and health-check steps on a clean Linux x86_64 host.
- Confirm package visibility, release links, installation docs, and image tags before announcing the release.
- Keep a rollback bundle and document any migration that cannot be reversed automatically.
