---
title: Testing changes locally
parent: Contributing
has_children: false
nav_order: 4
---

# Inner loop, testing your changes

## Using Github Codespaces (preferred)

This repo has a github codespace dev container defined, this container is based on Debian Bookworm and contains all the libraries and components to run github pages locally in Github Codespaces (Ruby 3.2, Jekyll, gems, VS Code tasks). To test your changes locally do the following:

- Enable [Github codespaces](https://github.com/features/codespaces) for your account
- Fork this repo
- Open the repo in github codespaces

![](https://docs.github.com/assets/images/help/codespaces/new-codespace-button.png)

- Wait for the container to build and connect to it
- Understand the folder structure of the Repo:
    - "apim-lab" folder , contains all the mark down documentation files for all the challenges
    - "assets" folder, contains all the images, slides, and files used in the lab
- Understand the index, title, and child metadata used by [just-the-docs theme](https://pmarsceill.github.io/just-the-docs/docs/navigation-structure/#ordering-pages) 
- Run the website in github codespaces using the built-in task:
    - the ".vscode" folder contains a tasks.json file with all the tasks necessary 
    - For example, Pressing  ⇧⌘B on a mac, or running Run Build Task from the global Terminal menu will run the website locally in github codespace. [See Vscode docs for other OS key bindings](https://code.visualstudio.com/docs/editor/tasks).


![Enabling Codespace](../../assets/gifs/codespace.gif)

## Local Development

You can also run the site locally on your own machine without Github Codespaces. This requires Ruby and Bundler to be installed.

### Prerequisites

- [Ruby](https://www.ruby-lang.org/en/documentation/installation/) (the version compatible with Jekyll 3.9.5)
- [Bundler](https://bundler.io/) (`gem install bundler`)
- Git

### Setup

1. Fork and clone the repo:

    ```bash
    git clone https://github.com/<your-username>/apim-lab.git
    cd apim-lab
    ```

2. Install dependencies:

    ```bash
    bundle install
    ```

## Running the site with live reload

There are several VS Code tasks defined in `.vscode/tasks.json` you can use, or run the commands directly in a terminal:

- **Build and serve with live reload** (recommended for local development):

    ```bash
    bundle exec jekyll serve --livereload --force_polling
    ```

    This starts a local server at `http://localhost:4000` and automatically rebuilds the site when files change.

- **Build only** (no server):

    ```bash
    bundle exec jekyll build
    ```

    The generated site will be in the `_site/` directory.

### Folder structure

- `apim-lab/` — Contains all the Markdown documentation files for each lab section
- `assets/` — Contains all images, slides, and supporting files used in the lab
- `_config.yml` — Jekyll site configuration
- `Gemfile` — Ruby dependency definitions