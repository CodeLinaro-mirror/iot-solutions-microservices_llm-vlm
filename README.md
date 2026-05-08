# GitLab CI Overview

This project is used to build and push GenAI LLM/VLM services Docker containers from CLO.
Its `.gitlab-ci.yml` builds and validates an ARM64 Docker image for the GenAI LLM/VLM service.

- Uses `docker:25.0.3-dind` on an `arm64-runner` and starts Docker-in-Docker in `before_script`.
- Defines image coordinates (`artifacts.codelinaro.org/.../genai-llm-vlm-service`) with both versioned (`1.0.0`) and `latest` tags.
- Clones `solutions-microservices` from CodeLinaro, checks out a pinned commit, and builds from `genai/src/Dockerfile.chatcompletion` targeting `genai-llm-vlm-service`.
- Pushes both tags to the JFrog registry.
- Runs smoke tests in a `test` stage by launching containers from both `latest` and versioned images and verifying runtime artifacts (Python, site-packages, native libs, and interface header).

To build images from the latest CLO source, update `SOLUTIONS_MICROSERVICES_COMMIT` to the latest commit from `SOLUTIONS_MICROSERVICES_REPO_URL`. This change triggers the CI pipeline, which then builds and pushes updated images.
