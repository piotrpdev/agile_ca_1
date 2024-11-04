# Docker Assignment - Agile Software Practice

__Name:__ Piotr Placzek (20097618)

__Demo:__ <https://www.youtube.com/watch?v=k9bOmDjkF6Q>

This repository contains the containerization of the multi-container application illustrated below.

![arch](./images/arch.png)

## Database Seeding

- Researched ways to seed database.
  - Found and copied [this StackOverflow answer](https://stackoverflow.com/a/55819683/19020549) that involves creating an image for seeding.
  - Created `database-mongo-seed-network` network so the seed image can reach the MongoDB database.
  - Had to pass `--authenticationDatabase=admin` flag to avoid `mongoimport` error. Found that solution on [StackOverflow](https://stackoverflow.com/a/68937584/19020549).
  - Switched to using `command` property and bind mount instead of building a whole new image.

## Multi-Stack

- Researched ways to have certain docker compose services only start in development.
  - Found and implemented [compose profiles](https://docs.docker.com/compose/how-tos/profiles/).
  - By default, `docker compose up` starts production stack. `docker compose --profile development up` starts development stack.

## Steps taken

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
- Researched ways to seed database.
  - Found and copied [this StackOverflow answer](https://stackoverflow.com/a/55819683/19020549) that involves creating an image for seeding.
  - Created `database-mongo-seed-network` network so the seed image can reach the MongoDB database.
  - Had to pass `--authenticationDatabase=admin` flag to avoid `mongoimport` error. Found that solution on [StackOverflow](https://stackoverflow.com/a/68937584/19020549).
  - Switched to using `command` property and bind mount instead of building a whole new image.
- Learned that docker compose reads `.env` files and switched to using interpolation for MongoDB username and password.
  - Changed `MONGODB_PASSWORD` in `.env` file to `secret` instead of the default `password` because it was causing issues.

## Resources used

- <https://stackoverflow.com/questions/45255066/create-networks-automatically-in-docker-compose>
- <https://stackoverflow.com/questions/43308319/how-can-i-run-bash-in-a-docker-container>
- <https://www.dragonflydb.io/error-solutions/redis-connection-error-111>
- <https://stackoverflow.com/questions/24319662/from-inside-of-a-docker-container-how-do-i-connect-to-the-localhost-of-the-mach>
- <https://medium.com/@akilblanchard09/creating-isolated-network-in-docker-ff55941e3665>
- <https://github.com/mongo-express/mongo-express-docker/issues/126>
- <https://github.com/mongo-express/mongo-express-docker/issues/120>
- <https://www.reddit.com/r/docker/comments/13kxfjf/how_to_handle_dockercompose_for_production_and/>
- <https://docs.docker.com/compose/how-tos/profiles/>
- <https://stackoverflow.com/questions/31210973/how-do-i-seed-a-mongo-database-using-docker-compose>
- <https://stackoverflow.com/a/55819683/19020549>
- <https://www.mongodb.com/docs/database-tools/mongoimport/>
- <https://stackoverflow.com/a/68937584/19020549>
- <https://stackoverflow.com/a/59554543/19020549>
- <https://stackoverflow.com/questions/29377853/how-can-i-use-environment-variables-in-docker-compose>
