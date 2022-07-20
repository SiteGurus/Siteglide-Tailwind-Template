# tailwind-template-flowbite
A quick-start Tailwind CSS setup for Siteglide CLI, using the Flowbite plugin.

Requirements:
- Make sure you have already installed the Siteglide-CLI and are familiar with its use. This should give you the tools and the understanding you need to follow this guide. [Introducing Siteglide CLI](https://developers.siteglide.com/introducing-siteglide-cli "Introducing Siteglide CLI").

Key points:
- Siteglide-CLI will only be able to pull and sync files that are inside the marketplace_builder folder. This means if you wish to be able to sync or pull configuration files to and from the site, you will need to configure these files to work in a different location.

## Step 1

Use Siteglide CLI pull or init to create your directory structure in your project folder.

## Step 2

- Copy package.json, package-lock.json and the tailwind_src folder from this repository root to your own. (See troubleshooting if your project already has a package.json file.)
- Copy the tailwind.config.js file from "marketplace_builder/views/partials/tailwind/tailwind.config.js" to the identical path in your own project folder. Using this custom location will allow it to be pushed and pulled to the site.

## Step 3

In terminal, change directory to your project folder `cd <my_folder_path>` and use the command `npm i`. This will install the required dependencies.
## Step 4 - Making Changes to the Site

Each time you start work:

1. Pull the latest files from the site using siteglide-cli. It's important to have the latest files, because Tailwind only adds classes that you're actually using, but it can only see which files you're using if the files are available locally.
2. In terminal, run the command: `npm run watch_tw`. This will watch your files for any changes and keep the tailwind CSS up to date.
3. Use Siteglide-CLI sync or deploy to push the latest Tailwind to the site.

### Troubleshooting

#### NodeJS and NPM Versions

If you see an error relating to the version of NPM, you may want to check which version of NodeJS and NPM you have installed on your machine:

`node -v
npm -v`

Follow the instructions here to update depending on your operating system: [Installing NPM](https://docs.npmjs.com/cli/v8/configuring-npm/install "Installing NPM").

#### Version Control and Conflicts on Siteglide

If you work with other developers (or on multiple devices) on the same Siteglide project, it is definately recommended to use a version-control (otherwise known as source-control) tool like GitHub to share your Tailwind config file etc. with the other developer.

The risk of conflicts is somewhat mitigated through storing the tailwind.config.js file in a custom location (inside marketplace_builder/views/partials). This means it will be accessible via Siteglide CLI pull and editable via sync, but not from the Siteglide Admin.

However, the package.json and package-lock.json files will not be accessible via pull or sync in their root location, so if you intend to edit these, working with a version-control tool becomes an advantage to prevent conflicts.

If you are using version-control, the node_modules folder can become very large and you may want to add this to gitignore.

#### I already have a package JSON file.

In that case, use npm to add dev-dependencies to the existing file rather than copying across our file:

`npm i -D tailwindcss@3.1.5`
`npm i -D flowbite@1.4.7`
`npm i -D @tailwindcss/typography@0.5.3`

[Adding Dependencies to a package.json file](https://docs.npmjs.com/specifying-dependencies-and-devdependencies-in-a-package-json-file#adding-dependencies-to-a-packagejson-file "Adding Dependencies to a package.json file").

#### I use an alternative package manager, instead of NPM.

This is fine! We don't cover this in our example, but there is plenty of documentation out there. You can use the information in the answer above to see which dependencies we use.

#### Editing this configuration

This repository is a "quick-start" guide, not fixed instructions for how to use Tailwind with Siteglide. Feel free to read the relevant documentation from [Tailwind](https://tailwindcss.com/docs/installation "Tailwind"), [NPM](https://docs.npmjs.com/specifying-dependencies-and-devdependencies-in-a-package-json-file "NPM"), [Flowbite](https://flowbite.com/docs/getting-started/quickstart/ "Flowbite") and configure Tailwind however you wish. 