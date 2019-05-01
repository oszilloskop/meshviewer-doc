# Build/Install

## Build utilities

* yarn [https://yarnpkg.com/](https://yarnpkg.com/)
* optional: gulp-cli (or use `yarn run gulp [command]` instead of `gulp`)

### Installing dependencies

Install yarn package-manager:

```
Choose your OS and install yarn https://yarnpkg.com/en/docs/install
```

Execute these commands on your server as a normal user to prepare the dependencies:

```bash
git clone https://github.com/ffrgb/meshviewer.git
cd meshviewer
yarn
# Only needed if no global gulp is installed / OS like arch provides a package
yarn global add gulp-cli
```

## Adjust config and style

1. [Change configuration to your community](/config_js.md)
2. \(optional\) Edit files in `scss/custom/`. Additional information under [development](/development.md).
3. \(optional\) Change `logo.svg` and generate new icons or adjust the images yourself.

## Building

Just run the following command from the meshviewer directory:

```bash
gulp
```

This will generate the folder `build/` that will contain all required files.

## Upgrade

1. Update the git repository but keep your local changes:

       git update-index --assume-unchanged config.js
      
2. Check your config for possible changes that were added since your last checkout
      
3. Run the build step again
