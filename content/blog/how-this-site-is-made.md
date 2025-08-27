---
title: "How This Site Is Made - Hugo, GitHub Pages, and GitHub Actions"
date: 2023-04-10T13:00:13+01:00
description:
toc: false
draft: false
tags: [hugo, guide, github, github-actions]
---
## What exactly is a Static Site Generator (SSG)?
A Static Site Generator takes content you give it (text, images and so on) and builds this all as standard HTML. What this means is that the content does not change and is shown to the user exactly the same way every single time.

For websites that are primarily text based (such as blogs), this can be useful. It means that the site is quick to load for visitors, quick to develop/build, and very easy to maintain. All you need to really do is provide the text after you've done the initial setup.

## Getting started with Hugo

To get started with Hugo, head over to the [Quick Start](https://gohugo.io/getting-started/quick-start/) guide which will walk you through getting up and running in about 10 minutes. 

The main things to do are:

- Install Hugo (depending on the OS you're using, this may vary somewhat)
- Make sure Git is installed (if you're new to Git/need to set up an SSH key, you can find a good guide here: [Generating a new SSH Key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent))
- Log into your GitHub account. If you don't have one, head over to [GitHub](https://github.com) and sign up for one.
- Pick your Hugo theme that you want to use for your site (visit [Hugo Themes](https://themes.gohugo.io/) to see all themes available and for instructions on how to add it to your site)

## But where will my Hugo site live?

If you've followed all the steps up until now, you have a Hugo site created (and hopefully, some basic content). But, for now, it only lives in the Git repository that you're storing it in and it isn't hosted anywhere. For hosting, you've got plenty of options:

- GitHub Pages (probably the easiest)
- Netlify
- An AWS Amplify instance
- An Azure Static Web App instance

Personally, unless there's a specific reason for hosting it elsewhere, I'd recommend GitHub Pages. Mainly because you'll already have a GitHub account created as part of the earlier steps (you can't add an SSH Key to a non-existant GitHub account), and also because it won't cost anything at all unless you want to set it up with your own domain so you can have yourname.com as the URL.

## Getting Hugo set up with GitHub Pages

Since you already have a Git repository where you have your site stored, all you have to do to get it hosted on GitHub is turn on the GitHub pages option and select "GitHub Actions" as the source. Once that's done, head back to your code editor for the next section...

## Pulling it all together with GitHub Actions

Why don't we we make our lives a little easier and automate the entire process? Instead of having to remove our "public" folder before uploading new content or manually building our site to be deployed, what if all we had to do was write the content we wanted to add and have our site automatically build itself and publish as soon as we ```git push``` our changes? Let's do that now...

In your code editor, create a new folder called ```.github``` (the . in front of the folder name denotes that it's a hiden folder) and then a subfolder called ```workflows```. In the ```workflows``` folder, create a new file called ```pages.yaml```

Once you've got your yaml file created, paste in the following:

```yaml 
name: Deploy Hugo SSG to GH Pages

# When the action should run. Here we specify it should run on push to main branch.
# We also allow for manually running the action with the empty "workflow_dispatch".
on:
  push:
    branches:
      - master

  workflow_dispatch:

# Set the needed permissions.
permissions:
  contents: read
  pages: write
  id-token: write

# Cancel running deployments if a new one is issued - avoids any conflicts or overwriting content.
concurrency:
  group: pages
  cancel-in-progress: true

jobs:
  build:
    runs-on: ubuntu-latest # Always pulls latest version of Ubuntu runner.
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          submodules: true # Ensures that our theme is always the latest stable version.

      - name: Setting up Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: "latest" # Always pulls latest version of Hugo.
          extended: true

      - name: Remove public dir
        run: rm -rf public # Delete the public directory (our published output folder - ./public) before build so stale content is not kept.

      - name: Setting up Pages
        id: pages
        uses: actions/configure-pages@v4

      - name: Build
        run: hugo --baseURL "${{ steps.pages.outputs.base_url }}/"

      - name: Upload artifact # Here we are able to view the contents of our site at the time of deploy - it will be kept for a short while before deletion.
        uses: actions/upload-pages-artifact@v4
        with:
          path: ./public

  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy build to GH Pages
        id: deployment
        uses: actions/deploy-pages@v4
```
The above script tells GitHub that we have created an action called "Deploy Hugo SSG to GH Pages" and does the following in order:

- The action will automatically run any time a ```git push``` happens once we've updated some content on our site.
- We set the necessary read/write permissions we need in our site repository.
- With concurency we make sure that if multiple people are working on the site and both push changes at the same time one does not overwrite the other or that there is some kind of conflict.
- We build our site using the latest version of Ubuntu and pull down the latest version of Hugo.
- We delete the ```./public directory``` before we build our site for deployment so that the latest content is published. If we have existing files in the public folder without removing it, our content might not show up depending on how it's named/what it is.
- We set up GitHub Pages and buld our site.
- The site gets deployed onto GitHub Pages as a fresh copy.

That's it! Now all you have to focus on is the writing itself, and when you want to publish new content, just push your changes to GitHub and let the GitHub Action we set up handle the rest. A few minutes later and your site will be live with your new content.

