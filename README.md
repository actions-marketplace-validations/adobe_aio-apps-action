[![Build Status](https://travis-ci.com/adobe/aio-apps-action.svg?branch=master)](https://travis-ci.com/adobe/aio-apps-action)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

# aio-apps-action
[Adobe Developer App Builder](https://github.com/AdobeDocs/project-firefly) support for GitHub actions. This action leverages [AIO CLI](https://github.com/adobe/aio-cli) to build, test and deploy App Builder applications.

# Getting Started
This Github action supports following commands
1) `build` - Builds Adobe Firefly App. This is similar to using `aio app build` command using AIO CLI
2) `test` - Test Adobe Firefly App. This is similar to using `aio app test` command using AIO CLI
3) `deploy` - Deploys Adobe Firefly App. This is similar to running `aio app deploy  --skip-build` command using AIO CLI. Deploy Command also supports `--no-publish` flag for `aio app deploy` command to control publishing of Extensions. See usage section for more details.
4) `auth` - Generates IMS Token and adds that to Github Action Enviornment for AIO CLI to use. The token is required to build and deploy Adobe Firefly Extensions.


Command Usage and required params
You can include the action in your workflow as adobe/aio-apps-action@1.0.0. Example :


```
    on: [push]
    jobs:
      build:
        runs-on: ubuntu-latest
        steps:
          - name: Checkout
            uses: actions/checkout@v2
          - name: Setup CLI
            uses: adobe/aio-cli-setup-action@1.0.0
            with:
              os: ubuntu-latest
          - name: Build
            uses: adobe/aio-apps-action@1.0.0
            with:
              os: ubuntu-latest
              command: build
              AIO_RUNTIME_NAMESPACE: ${{ secrets.AIO_RUNTIME_NAMESPACE }}
          - name: Test
            uses: adobe/aio-apps-action@1.0.0
            with:
              command: test
          - name: Deploy
            uses: adobe/aio-apps-action@1.0.0
            with:
              command: deploy
              AIO_RUNTIME_AUTH: ${{ secrets.AIO_RUNTIME_AUTH }}
              AIO_RUNTIME_NAMESPACE: ${{ secrets.AIO_RUNTIME_NAMESPACE }}
```

 ## Contributing

Contributions are welcomed! Read the [Contributing Guide](./.github/CONTRIBUTING.md) for more information.

## Licensing

This project is licensed under the Apache V2 License. See [LICENSE](LICENSE) for more information.
