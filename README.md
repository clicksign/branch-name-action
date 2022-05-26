<p align="center">
  <a href="https://github.com/actions/typescript-action/actions"><img alt="typescript-action status" src="https://github.com/actions/typescript-action/workflows/build-test/badge.svg"></a>
</p>

# About

Action created by clicksign's devops team

# Create a JavaScript Action using TypeScript

Use this template to bootstrap the creation of a TypeScript action.:rocket:

This template includes compilation support, tests, a validation workflow, publishing, and versioning guidance.  

If you are new, there's also a simpler introduction.  See the [Hello World JavaScript Action](https://github.com/actions/hello-world-javascript-action)

## Code in Main

> First, you'll need to have a reasonably modern version of `node` handy. This won't work with versions older than 9, for instance.

Install the dependencies  
```bash
$ yarn
```

Build the typescript and package it for distribution
```bash
$ yarn build && yarn package
```

## Change action.yml

The action.yml defines news inputs and output for action.

| Inputs                       |    required   |                     default                        |                  description                  |
|------------------------------|:-------------:|---------------------------------------------------:|:---------------------------------------------:|
| allowed_branch_list          | false         | main,release,feature,devops,hotfix,fix,dependabot  | Add list branch validate, separeted with ,    |
| payload                      | false         | null                                               | Create payload to slack message               |
| channel_id                   | false         | null                                               | Add chanel id slack                           |



## Example

```javascript
name: 'build-test'

on:
  create

jobs:
  test: # make sure the action works on a clean machine without building
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: clicksign/branch-name-action
        env:
          GITHUB_TOKEN: ${{ secrets.TOKEN }}
          SLACK_TOKEN: ${{ secrets.SLACK_TOKEN }}
        with:
          allowed_branch_list: ${{ secrets.ALLOWED_BRANCH_LIST }}
          channel_id: ${{ secrets.CHANNEL_ID }}
```
