# Standard Version

Having problems? want to contribute?

Automate versioning and CHANGELOG generation, with semver and conventional commit messages.

## Installation

### As `npm run` script

Install and add to `devDependencies`:

```
npm i --save-dev standard-version
```

Add an [`npm run` script](https://docs.npmjs.com/cli/run-script) to your _package.json_:

```json
{
  "scripts": {
    "release": "standard-version"
  }
}
```

Now you can use `npm run release` in place of `npm version`.

This has the benefit of making your repo/package more portable, so that other developers can cut releases without having to globally install `standard-version` on their machine.

### As global bin

Install globally (add to your `PATH`):

```
npm i -g standard-version
```

Now you can use `standard-version` in place of `npm version`.

This has the benefit of allowing you to use `standard-version` on any repo/package without adding a dev dependency to each one.

## CLI Usage

### First Release

To generate your changelog for your first release, simply do:

```sh
# npm run script
npm run release -- --first-release
# or global bin
standard-version --first-release
```

This will tag a release **without bumping the version in package.json (_et al._)**.

When ready, push the git tag and `npm publish` your first release. \o/

### Cut a Release

If you typically use `npm version` to cut a new release, do this instead:

```sh
# npm run script
npm run release
# or global bin
standard-version
```

As long as your git commit messages are conventional and accurate, you no longer need to specify the semver type - and you get CHANGELOG generation for free! \o/

After you cut a release, you can push the new git tag and `npm publish` (or `npm publish --tag next`) when you're ready.

### Release as a pre-release

Use the flag `--prerelease` to generate pre-releases:

Suppose the last version of your code is `1.0.0`, and your code to be committed has patched changes. Run:

```bash
# npm run script
npm run release -- --prerelease
```
you will get version `1.0.1-0`.

If you want to name the pre-release, you specify the name via `--prerelease <name>`.

For example, suppose your pre-release should contain the `alpha` prefix:

```bash
# npm run script
npm run release -- --prerelease alpha
```

this will tag the version `1.0.1-alpha.0`

### Release as a target type imperatively like `npm version`

To forgo the automated version bump use `--release-as` with the argument `major`, `minor` or `patch`:

Suppose the last version of your code is `1.0.0`, you've only landed `fix:` commits, but
you would like your next release to be a `minor`. Simply do:

```bash
# npm run script
npm run release -- --release-as minor
# Or
npm run release -- --release-as 1.1.0
```

you will get version `1.1.0` rather than the auto generated version `1.0.1`.

> **NOTE:** you can combine `--release-as` and `--prerelease` to generate a release. This is useful when publishing experimental feature(s).