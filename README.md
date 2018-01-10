# git-madge

> Git-aware madge wrapper

[Madge] Madge is a developer tool for generating a visual graph of your module
dependencies, finding circular dependencies, and give you other useful info.

[Madge]: https://github.com/pahen/madge

`git-madge` is a simple wrapper that makes it git-aware.


## Install

### Dependencies

Requires that `madge` and `jq` are on your path:

```
npm install -g madge
brew install jq
```

### Installation

Copy the `git-madge` file to your path. Alternatively, on Homebrew:

```
brew install jez/formulae/git-madge
```


## Usage

If you're on master, it lists all JavaScript files, sorted by their
dependencies.

```
~/demo (master)
❯ git madge .
components/Element.js
components/Element.test.js
components/Elements.js
components/PaymentRequestButtonElement.js
components/PaymentRequestButtonElement.test.js
components/Provider.js
components/Provider.test.js
components/inject.js
components/inject.test.js
decls/Stripe.js
index.js
index.test.js
utils/shallowEqual.js
utils/shallowEqual.test.js
```

If you're on a branch, it'll filter the list to only files that have changed
since master. This is especially useful for code review; reviewing the files in
sorted order makes it so that you read the leaves first, then move up the tree.

```
~/demo (my-branch)
❯ git madge .
components/Element.js
components/Element.test.js
components/Elements.js
components/PaymentRequestButtonElement.js
components/PaymentRequestButtonElement.test.js
```

If you want to filter with respect to a different revision, set `REVIEW_BASE`:

``` bash
# only files changed by last commit:
❯ REVIEW_BASE=HEAD^ git madge .
```

You can pass [any arguments that `madge` supports][flags], like webpack config,
or paths:

```bash
# Custom webpack config
❯ git madge --webpack-config webpack.config.js

# Limit to src/components/ folder
❯ git madge src/components/
```

[flags]: https://github.com/pahen/madge#cli


## License

[![MIT License](https://img.shields.io/badge/license-MIT-blue.svg)](https://jez.io/MIT-LICENSE.txt)
