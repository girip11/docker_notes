# Docker best practices for production

## Broken status quo

- Always choose very specific base image(with version and OS) rather than generic base image for reproducible builds. Ex: `python:3` is bad, while `python:3.8.5-stretch` is good.

- Always pin the versions of the packages that our software depends on using package management tools. Otherwise it affects the reproducibility.

- Order the steps in the Dockerfile that respects the docker caching model.

- By default Docker containers run as root. It’s much better to run as a non-root user.

- Regularly rebuild docker images from scratch to get security updates of the base image.

- Multi stage builds can reduce image size but at the same time break caching which can lead to increase in the image build time.

- Opening ports `<1024` requires root privileges. So don’t bind to ports `<1024`, and do run as a non-privileged user.

- For python debian based images are better compared to alpine based (increased build time) if your are building one. If you are consuming from other built images, go for alpine as its size is less.

- Once in a while, **security updates should be run while building the docker image using `apt-get -y upgrade`**. This command requires to be run as root. Also not all the base images will be rolled out frequently with all the latest security updates.

- [Hadolint](https://github.com/hadolint/hadolint/) is a Dockerfile linter. Use this to lint Dockerfiles. VSCode also has extension for hadolint.

## Base image and dependencies

- Choose images that are supported long term, well maintained with security updates. Also look up what's the best image for a particular programming language. For instance, [debian based slim images are recommended compared to alpine images for python till PEP 656 is complete](https://pythonspeed.com/articles/alpine-docker-python/).

- Whether you’re setting up a development environment or writing your `Dockerfile`, make sure you upgrade pip. Otherwise you’ll have a much harder time installing packages.
- Always pin the dependency versions. Update the dependencies once in a while, while setup things like **github dependabot** that can notify updates with security bug fixes.

---

## References

- [Docker best practices for production](https://pythonspeed.com/docker/#articles-best-practices-for-production)
