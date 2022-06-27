# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Changed

- Update pods resource quotas after production testing and fine-tuning to improve efficiency
- Updated to [ArgoCD v2.4.2](https://github.com/argoproj/argo-cd/releases/tag/v2.4.2)
  - Tightened some security context params
  - Added support for OpenTelemetry by pushing traces to [Tempo](https://github.com/karavel-io/platform-component-tempo)

## [1.0.2] - 2022-04-21

### Changed

- Changed Redis image from `quay.io/bitnami/redis` to `public.ecr.aws/bitnami/redis` after Bitnami removed their images from Quay
- Update redis to 6.2.6
- Update ArgoCD to 2.3.3

## [1.0.1] - 2022-03-31

### Fixed

- Added missing RBAC permissions for leader election to argocd-applicationset

## [1.0.0] - 2022-03-03

Initial release

[unreleased]: https://github.com/karavel-io/platform-component-argocd/compare/1.0.2...HEAD
[1.0.2]: https://github.com/karavel-io/platform-component-argocd/compare/1.0.1...1.0.2
[1.0.1]: https://github.com/karavel-io/platform-component-argocd/compare/1.0.0...1.0.1
[1.0.0]: https://github.com/karavel-io/platform-component-argocd/releases/tag/1.0.0
