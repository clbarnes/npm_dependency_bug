# npm dependency resolution bug

Probably this https://github.com/npm/npm/issues/12184

## Issue

I want to `npm install --only=dev` in order to install only my dev dependencies.
Doing this installs all of my dev dependencies except `minimatch`, `mkdirp`, and `optimist`.
This are installed if I do `npm install --only=prod`, or `npm install`, or `npm install --dev`.

## Severity

It seems like it would be really common for dev and prod dependencies to share some upstream dependencies.
If so, and if `npm install --only=dev` is, in theory, a useful tool, then this is a severe bug.

## Probable cause

As those problem dependencies are also dependencies of the production packages,
they are probably marked as production packages themselves during deduplication.

## To reproduce

```bash
git clone <this_repo>
cd <the_new_directory>
npm install --only=dev
npm list minimatch mkdirp optimist
```

My NVM, node and NPM versions are shown in `versions.txt`.

The state of my package-lock with `--only=dev`, `--only=prod`, and bare `npm install`s are also here.

