# Contributing

## How to bump the TruffleRuby version

1. Update `update-dockerfiles` with the new version number.
2. Run `update-dockerfiles` which will generate new Dockerfiles.
3. Update the README with the new version number.
4. Commit and tag the release with `stable-<TRUFFLEVERSION>` (e.g., `stable-21.1.0`)
5. Push the commit and the tags
6. Copy the README to the [DockerHub project](https://hub.docker.com/repository/docker/flavorjones/truffleruby).
