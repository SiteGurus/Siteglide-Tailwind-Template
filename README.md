---
layout: modules/sitegurus_documentation/templates/2
converter: markdown
metadata:
  name: Using the Tailwind CLI with Siteglide
---
## Before You Start

* Check [Choosing a Build Method](https://sitegurus.io/documentation/modules/sitebuilder/libraries_and_frameworks/libraries_using_tailwind_css_choosing_a_build_method) first to choose which option suits you best.
* Make sure you have already installed the Siteglide-CLI and are familiar with its use. This should give you the tools and the understanding you need to follow this guide. [Introducing Siteglide CLI](https://developers.siteglide.com/introducing-siteglide-cli "Introducing Siteglide CLI").

## Introduction

Using the Command Line Interface (CLI) to build a Tailwind CSS file allows you to use the latest versions of TailwindCSS and its various 1st and 3rd party plugins.

If you prefer using the Siteglide CLI to build sites already, the two CLIs work very well together.

This guide is both a quick-start guide to get you started and a set of tips for how to build Tailwind CLI into your Siteglide workflow.

## Quick Start

1. SiteBuilder Tailwind Settings

    Enter the Module Admin and Scroll past the libraries to the Tailwind Settings Card and click the gear icon.

    ![How to Switch to CLI Mode](https://res.cloudinary.com/sitegurus/image/upload/v1658411912/modules/module_86/documentation/Tailwind/select_just_in_time.jpg)

    Then select "CLI".

2. Create Directory Structure
    
    Open up a command-line terminal on your machine and change directory (`cd`) to your project folder. Use `siteglide-cli pull <env>` or `siteglide-cli init` to create your directory structure.

3. Copy Files

    Copy the files you need into your project folder, using whichever method you prefer.

    + Copy package.json and package-lock.json from the this repository root to your own. (See troubleshooting if your project already has a package.json file.)
    + Copy the tailwind.config.js and tailwind.css files from the this repository's folder:
    ```bash
    ├───marketplace_builder
    │   └───assets
    │       └───modules
    │           └───module_86
    │               └───src
    │                   tailwind.config.js
    │                   tailwind.css
    ```
    to an identical folder structure inside your own project. Using this custom location will allow it to be pushed and pulled to the site.

    (If you prefer, you can create a new repository using the template in Github and then pull your site into the new folder!)

4. Install NPM Dependencies

    In terminal, change directory to the root of your project folder

    ```bash
    cd <my_folder_path>
    ```

    and use the command 

    ```bash
    npm i
    ```

    This will install the required dependencies needed to run the Tailwind CLI with our default setup.

5. Run the command `siteglide-cli sync <env>` to watch your `marketplace_builder` folder for changes and push these to the site. 

6. Run the command: `npm run tailwind` to generate the CSS file for the first time. Since you started syncing in step 4, this will immediately be pushed to the site.

7. Set up your Page Template

    You can either create a new template using SiteBuilder (option a) or edit an existing one (option b).

    a. After you have synced your new `css/tailwind.min.css` file to the site, the SiteBuilder module will by default add this CSS file to any [new templates](./../../Libraries.md#creating-a-template) created through the Module. 

    b. Edit your Page Template in Siteglide to change the  `<link rel="stylesheet" href="modules/module_86/css/tailwind-default.min.css file">`, to your newly generated minified CSS file. If you've followed our example, this will be: `<link rel="stylesheet" href="css/tailwind.min.css file">`.

## An Example Workflow using Siteglide CLI and Tailwind CLI

Each time you start work:

1. Pull the latest files from the site using `siteglide-cli pull`. It's important to have the latest files, because Tailwind only adds classes that you're actually using, but it can only see which files you're using if the files are available locally.
   
2. Use `siteglide-cli sync` to watch your `marketplace_builder` folder.

3. In terminal, run the command: `npm run tailwind` to watch for Tailwind changes. 

4. Now you can begin work! Every time you make a change and save, your updated file will sync to Siteglide and so will a brand new version of the Tailwind CSS.

## Adding Custom CSS

You can use the src file `tailwind_src/tailwind.css` to write any custom CSS for your Tailwind build. Check the [Tailwind CSS documentation on Functions & Directives](https://tailwindcss.com/docs/functions-and-directives) for details.

## Troubleshooting

### NodeJS and NPM Versions

If you see an error relating to the version of NPM, you may want to check which version of NodeJS and NPM you have installed on your machine:

```bash
node -v
```
```bash
npm -v
```

Follow the instructions here to update depending on your operating system: [Installing NPM](https://docs.npmjs.com/cli/v8/configuring-npm/install "Installing NPM").

### Version Control and Conflicts on Siteglide

If you work with other developers (or on multiple devices) on the same Siteglide project, it is definately recommended to use a version-control (otherwise known as source-control) tool like GitHub to share your package.json file etc. with the other developer.

The risk of conflicts is somewhat mitigated if you follow our reccomendation in the Quick Start guide of storing the `tailwind.config.js` file in a custom location (inside `marketplace_builder/views/partials`). This means it will be accessible via Siteglide CLI pull and editable via sync, but not from the Siteglide Admin.

If you are using version-control, the node_modules folder can become very large and we recommend adding this to your `.gitignore` file or equivalent.

### I've got a `syntax error` when I run the `npm run tailwind` command

There might be an issue with your Tailwind Config File. Try temporarily reverting the file to the state it is in here and see if that fixes the problem. If not [contact Sitegurus](https://sitegurus.io). 

### I've got a different problem

Please [contact Sitegurus](https://sitegurus.io).

## Removing JIT Code from the Template

If you are certain that you won't be using the [Tailwind's JIT Compiler Via CDN](https://sitegurus.io/documentation/modules/sitebuilder/libraries_and_frameworks/tailwinds_jit_compiler_via_cdn) in the future, you can optionally remove the `<script type="module">` and `<script type="tailwind-config">` tags containing the JIT version of the Tailwind Config file from the Page Template. This may help avoid clutter and confusion.
## Alternative Configurations

### I already have a package JSON file.

In that case, use npm to add dev-dependencies to the existing file rather than copying across our file:

```bash
npm i -D tailwindcss@3.1.5
```
```bash
npm i -D flowbite@1.4.7
```
```bash
npm i -D @tailwindcss/typography@0.5.3
```

[Adding Dependencies to a package.json file](https://docs.npmjs.com/specifying-dependencies-and-devdependencies-in-a-package-json-file#adding-dependencies-to-a-packagejson-file "Adding Dependencies to a package.json file").

### I use an alternative package manager, instead of NPM.

This is fine! We don't cover this in our example, but there is plenty of documentation out there. You can use the information in the answer above to see which dependencies we use.

### Editing this configuration

This repository is a "quick-start" guide, not fixed instructions for how to use Tailwind with Siteglide. Feel free to read the relevant documentation from [Tailwind](https://tailwindcss.com/docs/installation "Tailwind"), [NPM](https://docs.npmjs.com/specifying-dependencies-and-devdependencies-in-a-package-json-file "NPM"), [Flowbite](https://flowbite.com/docs/getting-started/quickstart/ "Flowbite") and configure Tailwind however you wish. 

### I prefer to work in the Siteglide Admin

Have you tried our [JIT Compiler](https://sitegurus.io/documentation/modules/sitebuilder/libraries_and_frameworks/tailwinds_jit_compiler_via_cdn)? Based on the fantastic JIT Compiler from the folks at Beyond Code, we've added caching to allow better production speeds and integrated it with a Siteglide Template. This allows a developer to use Tailwind entirely from the Siteglide Admin without using any CLI tools.

