# version-for-publishing

This action generates a new dev version number for a git branch, e.g. `1-0-0` for all projects where the version is part of a json file, e.g. `package.json`.

It accepts a json file path and a branch name as input.
No release magic or analyzing changelogs is happening.
The main part of the version, e.g. `1.0.0` will not be touched. 

## What is happening

1.   reads a json file - in general a package.json
2.   check the **version** field in the json file
3.   defaults to 1-0-0
6.   provides the new version string as output of the action
7.   Now you can do what you want, e.g. commit & push the changes, use it for a build step or anything else :)

## Examples

### Simple branch

1.   there is a branch named `develop` and its base branch is `main`
2.   the `package.json` version is `1.0.0`
3.   Using this action results in version `1-0-0-develop`

### Nested branches

1.   there is a branch named `parent` and its base branch is `main`
2.   now another branch `child` is based on `parent`
3.   there is already a version in `parent` - `1.0.0-parent.1`
4.   Using this action for `child` results in version `1-0-0-child.1`
5.   The **nesting** is not represented in the version!

### Branch names with `/`

1.   there is a branch named `feat/next-big-thing`
2.   Using this action for `feat/next-big-thing` results in version `1-0-0-next-big-thing.1`

### Main branch

1.   there is a branch named `main`
2.   the `package.json` version is `1.0.0`
3.   Using this action results in version `1-0-0`

## Inputs

- **branch**: The name of the branch to check if the current branch is main or a dev-branch. Default `main`.
- **filePath**: The json file path or file name where the `version` field is present. Default `package.json`.

## Outputs

- **version**: The generated version number.

## Example usage

```
uses: trendoid/version-for-publishing@0.1.7
with:
  branch: feat/version-for-publishing
  filePath: ./package.json
```
