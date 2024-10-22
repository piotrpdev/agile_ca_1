# Agile Software Practice - Assignment 1

- Transplanted `compose.yaml` from previous `docker-profile-app` lab repo.
- Added `cache` service that uses `redis:alpine` image.
- Tried `REDIS_URI=redis://localhost` but that didn't work
  - Did some research and used `REDIS_URI=redis://host.docker.internal` as a workaround
  - Later on switched to `REDIS_URI=redis://cache`
- Created `mongo-express-database-network` network so the Express web app can only reach the MongoDB database.
- Created `database-movies-network` network so the Movies API can reach the MongoDB database.
- Created `cache-movies-network` network so the Movies API can reach the Redis cache.
- Changed Express web app to use `ME_CONFIG_MONGODB_URL` env var instead of [outdated `ME_CONFIG_MONGODB_SERVER` env var](https://github.com/mongo-express/mongo-express-docker/issues/120).
  - [Setting `ME_CONFIG_MONGODB_SERVER` doesn't actually do anything, it always uses the default value](https://github.com/mongo-express/mongo-express-docker/issues/126).
- Researched ways to have certain docker compose services only start in development.
  - Found and implemented [compose profiles](https://docs.docker.com/compose/how-tos/profiles/).
  - By default, `docker compose up` starts production stack. `docker compose --profile development up` starts development stack.
