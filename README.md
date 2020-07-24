# Helm Basics Training

In this guided hands-on training, we show participants the Helm's basics.

For more see [Helm Basics Training online](https://helm-basics.k8s.puzzle.ch/).


## Content Sections

The Techlab content resides within the [content](content) directory.

The main part are the labs, which can be found at [content/en/docs](content/en/docs).


## Hugo

Helm Techlab is built using the static page generator [Hugo](https://gohugo.io/) and is published at [helm-basics.k8s.puzzle.ch](https://helm-basics.k8s.puzzle.ch/).

The page uses the [docsy theme](https://github.com/google/docsy) which is included as a Git Submodule.

After cloning the main repo, you need to initialize the submodule like this: 

```bash
git submodule update --init --recursive
``` 


## How to test locally
### Using Docker

Build the image:

```bash
docker build -t acend/helm-basics-training:latest .
```

Run it locally:

```bash
docker run --rm --interactive --publish 8080:8080 acend/helm-basics-training
```


### Using Buildah and Podman

Build the image:

```bash
buildah build-using-dockerfile -t acend/helm-basics-training:latest .
```

Run it locally with the following command. Beware that `--rmi` automatically removes the built image when the container stops, so you either have to rebuild it or remove the parameter from the command.

```bash
podman run --rm --rmi --interactive --publish 8080:8080 localhost/acend/helm-basics-training
```


## How to develop locally

To develop locally we don't want to rebuild the entire container image every time something changed, and it is also important to use the same hugo versions like in production.
We simply mount the working directory into a running container, where hugo is started in the server mode.

```bash
$ docker run --rm --interactive --publish 8080:8080 -v $(pwd):/opt/app/src -w /opt/app/src acend/hugo:0.68.3 hugo server -p 8080 --bind 0.0.0.0
```

## Contributions

If you find errors, bugs or missing information please help us improve our training and have a look at the [Contribution Guide](CONTRIBUTING.md).
