# remote-falcon-image-builder

This is a template repository provides two GitHub Actions workflows that can be utilized to build [Remote Falcon](https://remotefalcon.com/) images([packages](https://docs.github.com/en/packages/quickstart)) on GitHub and push them to the [GitHub Container Registry](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-container-registry).

[Remote Falcon](https://remotefalcon.com/) is an awesome project and I thought I would give back by creating a simplified way to run Remote Falcon for those who would like to self host beyond just these [ways](https://docs.remotefalcon.com/docs/developer-docs/running-it/methods).

[cloudflared-remotefalcon](https://github.com/Ne0n09/cloudflared-remotefalcon/tree/main) helps you self host [Remote Falcon](https://remotefalcon.com/) with guided setup and configuration using [Cloudflare Tunnels](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/) and your own server capable of running [Docker](https://www.docker.com/) through the use of various helper scripts.

For full details check the [documentation](https://ne0n09.github.io/cloudflared-remotefalcon/)!

## Create Repository from Template

[See instructions here](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template)

## Build args:

The build arguments used in the workflow are below. 

These can be manually configured from the Repository settings -> Secrets and variables -> Actions -> Secrets. 

These should be set before building new images.

- HOST_ENV

- VERSION

- CONTROL_PANEL_API

- VIEWER_API

- VIEWER_JWT_KEY

- GOOGLE_MAPS_KEY

- PUBLIC_POSTHOG_KEY

- PUBLIC_POSTHOG_HOST

- GA_TRACKING_ID

- MIXPANEL_KEY

- HOSTNAME_PARTS

- SOCIAL_META

- SWAP_CP

- VIEWER_PAGE_SUBDOMAIN

- OTEL_OPTS

- OTEL_URI

- MONGO_URI

- CLARITY_PROJECT_ID

## GitHub Actions Workflows

Click Actions on the top bar. There are two workflows provided

1. Build All Remote-Falcon Images

2. Build Single Remote-Falcon Image

Both workflows can be invoked on demand selecting the workflow and clicking 'Run workflow'.

The Build All workflow also runs automatically every day at 11:00 PM CST. It fetches the latest commit hash from the [Remote Falcon repositories](https://github.com/Remote-Falcon) and compares the short hash image tag for any existing images in the GHCR.

- If the hashes match the workflow stops.

- If the hashes do not match, then the workflow will build a new image with the currently configured secrets to allow for faster updates.

## Pulling the images

The images may be pulled after they are built via 'sudo docker pull' after running 'sudo docker login ghcr.io'

The ${REPO} variable is your repository that contains these workflows and images.

- ghcr.io/${REPO}/plugins-api:latest

- ghcr.io/${REPO}/control-panel:latest

- ghcr.io/${REPO}/viewer:latest

- ghcr.io/${REPO}/ui:latest

- ghcr.io/${REPO}/external-api:latest
