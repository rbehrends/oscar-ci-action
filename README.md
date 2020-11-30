# GitHub actions for Oscar CI

This repository defines three different GitHub actions, `configure`,
`install`, and `test` that can be used from workflows.

It is recommended to use the `@master` version, because that is kept
in sync with the CI scripts in the https://github.com/oscar-system/oscar-ci
repository.

## The `configure` action.

This action takes the following parameters, most of them optional.


    - uses: oscar-system/oscar-ci-action/configure@master
    - with:
        # Julia version, defaults to a recent stable version.
        julia: "1.5.3"

        # The following parameters specify the package name (without
        # a trailing ".jl"), the package repository, and the Git ref.
        # The package name is mandatory, the other parameters default
        # to github.repository and github.ref, respectively.
        #
        # This results in this package version being used to override
        # the default version in an Oscar installation. It can be
        # a branch or the internal ref used in a pull requeest.
        package: ""
        repository: ${{ github.repository }}
        ref: ${{ github.ref }}

        # buildtype specifies whether one wants to test against the
        # current master branch versions or the released versions.
        # The value can be one of "master", "develop", or "stable".
        buildtype: "master"

        # The config parameter specifies the configuration data.
        # In most cases, this can be left alone. It defaults to
        # ci/config/standalone.yaml, which is the local version of
        # config/standalone.yaml in https://oscar-system/oscar-ci.
        config: "ci/config/standalone.yaml"

        # The final parameter denotes which tests are to be run. It
        # can be one of "load", "packages", or "all". The "load"
        # tests is the fastest and merely tests if all Oscar packages
        # can be loaded. The "packages" test also runs all Oscar
        # package tests. The "all" test runs all tests in the CI
        # suite, but can take a long time to finish.
        test: "load"

## The `install` action

This action installs the actual Oscar packages in a local environment.

The only parameter is the configuration file, same as for the `configure`
action. It is generally unnecessary to specify that parameter.

    - uses: oscar-system/oscar-ci-action/install@master
    - with:
        # The config parameter specifies the configuration data.
        # In most cases, this can be left alone. It defaults to
        # ci/config/standalone.yaml, which is the local version of
        # config/standalone.yaml in https://oscar-system/oscar-ci.
        config: "ci/config/standalone.yaml"

## The `test` action

This action runs the CI tests.

The only parameter is the configuration file, same as for the `configure`
action. It is generally unnecessary to specify that parameter.

    - uses: oscar-system/oscar-ci-action/install@master
    - with:
        # The config parameter specifies the configuration data.
        # In most cases, this can be left alone. It defaults to
        # ci/config/standalone.yaml, which is the local version of
        # config/standalone.yaml in https://oscar-system/oscar-ci.
        config: "ci/config/standalone.yaml"
