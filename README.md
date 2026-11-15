# php81

[![Build Images](https://github.com/specsnl/php81/actions/workflows/main.yml/badge.svg)](https://github.com/specsnl/php81/actions/workflows/main.yml)

A PHP 8.1 (FPM and Apache) based Docker base image.

## Pulling the images

```
# FPM
docker pull ghcr.io/specsnl/php81:latest
docker pull ghcr.io/specsnl/php81/builder:latest

# Apache
docker pull ghcr.io/specsnl/php81/apache:latest
docker pull ghcr.io/specsnl/php81/apache/builder:latest
```

The image name scheme: `ghcr.io/specsnl/php81[/{VARIANT}][/{TARGET}]:{VERSION}`

- **{VARIANT}**: omitted for FPM, otherwise `apache`
- **{TARGET}**: omitted for `runtime`, otherwise `builder`
- **{VERSION}**: `latest`, a release tag (i.e. `1.0.1`), `main` or `pr-<number>`

The `builder` image is also published under its old names, `builder_nodejs` and `node`, from the time Node.js had its own
target. These names are deprecated and will be removed ([specsnl/github-actions#76](https://github.com/specsnl/github-actions/issues/76));
use `builder` instead.

## Building the docker image(s)

There are multiple targets:

  - **runtime**: this is for *production*. It does not contain any development tools like Composer and Xdebug.
  - **builder**: this is for *development*. This is based on the runtime-target and it adds Composer, Xdebug, Node.js etc.

Building `runtime`-target:

```
docker build --tag ghcr.io/specsnl/php81:latest --file fpm/Dockerfile --target runtime .
```

Building `builder`-target:

```
docker build --tag ghcr.io/specsnl/php81/builder:latest --file fpm/Dockerfile --target builder .
```

## Task commands

Available [Task](https://taskfile.dev/#/) commands:

```
* build:              Build all PHP Docker image targets of the FPM and Apache variants
* generate:           Generate all Dockerfiles from Dockerfile.tmpl
* lint:               Apply a Dockerfile linter to all Dockerfiles
* build:apache:       Build all PHP Docker image targets of the Apache variant
* build:fpm:          Build all PHP Docker image targets of the FPM variant
* install:hooks:      Install git hooks (pre-commit regenerates and stages Dockerfiles from template)
* lint:apache:        Apply a Dockerfile linter (https://github.com/hadolint/hadolint)
* lint:fpm:           Apply a Dockerfile linter (https://github.com/hadolint/hadolint)
* remove:hooks:       Remove installed git hooks
* shell:apache:       Interactive shell
* shell:fpm:          Interactive shell
```
