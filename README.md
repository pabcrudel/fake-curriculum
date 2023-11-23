# Fake Curriculum

Here you can see a fake curriculum forked from
[Jorge Lopez](https://github.com/jorloque), who was my teacher of
`Developing Environment` and `Web Applications Deployment`.

## Dual Deployment

This fake curriculum is deployed on GitHub Pages, Azure MV using Apache, Nginx
and Docker and on AWS S3 with Static Site Hosting enabled.

### GitHub Pages

When I made a change on `main` branch, a deployment workflow is called using my
own
[Minify Composite Action](https://github.com/pabcrudel/static-site-optimizer).

```yml
# .github/workflows/gh-pages-deployment.yml

name: GitHub Pages Deployment

on:
  push:
    branches:
      - main

jobs:
  ci-cd:
    runs-on: ubuntu-latest
    name: Minify & Deploy
    permissions:
      contents: write
    steps:
      - name: Checkout files
        uses: actions/checkout@v3

      - name: Minify html, css and js files
        uses: pabcrudel/static-site-optimizer@main
        with:
          project_path: .

      - name: Deploy to GitHub Pages
        uses: JamesIves/github-pages-deploy-action@v4.4.3
        with:
          folder: dist
```

### Azure MV

This feature has 4 versions:

1. Apache
1. Nginx
1. Docker with httpd (Apache) image
1. Docker with nginx image

In order to perform these tasks I've created bash [scripts to install Docker and
Apache-Nginx containers](docker). Then, using [Rsync Composite Action by
up9cloud](https://github.com/marketplace/actions/action-rsync) and my own
workflow, the website folder is deployed on Azure MV. There are 3 types of
workflows depending on it's target:

1. Base workflow: common for Apache and Nginx. It's target is the same
(`/var/www/html/`).
1. Docker workflow: It's target is the folder linked whit the container:
    - Apache: (`/home/$USER/apache-docker/`)
    - Nginx: (`/home/$USER/nginx-docker/`)

### AWS S3 Hosting Bucket

This feature is being performed by the AWS Console of an AWS Academy Lab, so is
offline.

## Take a look

You can see this site on GH Pages here:
<https://pabcrudel.github.io/fake-curriculum>
