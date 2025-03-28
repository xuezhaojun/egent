# Task: Bump up Dependencies

## Parameters

- package name
- target version
- repo list

## Description

The goal is to bump the dependencies of the specified package to the target version.

The process is as follows, for each repo:

- Checkout to the `main` branch, if there are any uncommitted changes, stash them.
- Sync the branch with latest upstream `main` branch.
- Create a new branch, named "bump-{{package-name}}-to-{{target-version}}", target version miss then use `@latest`
- Run `go get {{package-name}}@{{target-version}}` to bump the dependency.
- If there is vendor in the project, run `go mod tidy && go mod vendor` and if there is not, only run `go mod tidy`
- Review the Makefile, find the make command that related to `go build` and run it. If there is no such command, run `go build` under the `cmd` directory in that repo.
- Review the Makefile, find the make command that related to `go test` and run it. If there is no such command, run `make test` under the `test` directory in that repo.
- If error is hard to fix, notify the user with the error message, and stop the task waiting for user's next instruction.
- If no error occurs, deliver the code changes to github.
  - The branch name should be like `bump-up-dependencies-<package-name>-to-<target-version>`, the target version miss then use `@latest`.
