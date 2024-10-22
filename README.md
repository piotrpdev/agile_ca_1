# Agile Software Practice - Assignment 1

- Transplanted `compose.yaml` from previous `docker-profile-app` lab repo.
- Added `cache` service that uses `redis:alpine` image.
- Tried `REDIS_URI=redis://localhost` but that didn't work
  - Did some research and used `REDIS_URI=redis://host.docker.internal` as a workaround
  - Later on switched to `REDIS_URI=redis://cache`