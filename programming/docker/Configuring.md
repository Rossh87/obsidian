## ARG
- ARG is a Dockerfile command that expects to be passed a value on `build` invocation
- Optionally a default value can be provided:
```
# No default. If this value is not provided by 'docker build' command, build will fail
ARG my_arg

# Default value. If this value is provided at build time, the passed-in value will be used. Otherwise, the default will be used, and the build proceeds as normal.
ARG my_arg=foo
```
- Set `ARG` values with docker CLI: `docker build --build-arg my_arg=foo`
- Set `ARG` values with docker compose:
```
services:
	example:
		build: 
			context: .
			dockerfile: Dockerfile
			args:
				my_arg: foo
```
- ARG variables are available during the build, but not inside any containers, either in build layers or in final image at runtime

## ENV
- Used to set values that should be available in running containers based on built images
- Cannot be set directly from CLI or other external means
- To use dynamic `ENV` values, set `ENV` in Dockerfile from dynamic `ARG`:
```
# Expect a build-time variable and set a default:
ARG dynamic_value=foo

# Assign the value of dynamic value to an ENV. 'my_env' will be available inside of any running containers.
ENV my_env=$dynamic_value
```
- `ENV` values from build time can be [overridden](https://docs.docker.com/engine/reference/commandline/run/#env) in containers at run time: `docker run --env my_env=bar <image>`.
- environment variables that are not defined in a Dockerfile can still be passed to images at runtime.
- docker compose will automagically look for a `.env` file and interpolate any values from the `.env` that match dollar-annotated values in the compose file:
```console
$ cat .env
TAG=v1.5

$ cat compose.yml
services:
  web:
    image: "webapp:${TAG}"
```
This is done in a compilation step before anything actually runs.
- There is an additional, seemingly undocumented(?) behavior that will automagically assign the value of an unassigned `environment` value to its mate in a `.env` file, if one exists:
```console
$ cat .env
TAG=v1.5

$ cat compose.yml
services:
  web:
    environment:
		- TAG # resolves to 'v1.5' in containers
```