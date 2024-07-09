CHANGELOG
=======================================
## 2.0.2
- Fixed release-edit-with-push.yml failing when there is no release PR

## 2.0.1
- Removed unnecessary secrets (RULESET_...)

## 2.0.0
Release Manager Actions v2 is a release support workflow based on the develop-stable branches system.
It is incompatible with v1.

### Migration
Migration is deprecated because it is so different from v1, but if it is necessary, do the following:

1. Create a stable branch and register its name as a `STABLE_BRANCH` variable.
2. Since ruleset management is no longer needed, remove `RULESET_EDIT_APP_PRIVATE_KEY`, `RULESET_ID_WITHIN_RELEASE`, and `RULESET_ID_OUT_OF_RELEASE`. Also, the rulesets used in v1 should be deleted.
3. Grant `Repository - Pull request - Read and Write` permission to the GitHub App for `on: release`. If you don't have it, please create it.   
   In the `Install App` tab, select org or user right ⚙️ and go to the App installation management screen, where you will see `(app) is requesting an update to its permissions. [Review Request]`. Select `Review Request` and on the next screen select `Accept new permissions`.
4. Create a ruleset to protect the stable branch according to README.md.
5. Override the three release manager workflows.  
   Set line 6 of `release-edit-with-push.yml` to the name of the develop branch (the default branch in your repository).

## 1.2.1
The copied actions need to be replaced like following:

* release-edit-with-push.yml  
  https://github.com/misskey-dev/release-manager-actions/commit/c9287a3b002a6b6a765bdfcbe4597f88f581bafc#diff-e203de9569f7e3142efd374c0dca7e88b6d3fa704c51dd02d55b0a2d3810f6de
* release-with-ready.yml
  https://github.com/misskey-dev/release-manager-actions/commit/c9287a3b002a6b6a765bdfcbe4597f88f581bafc#diff-72b079e73412ba22b09f29c84b4205de9370875dc1aa56f9b27a7797941e578e

- Eliminated the possibility of code execution and token theft via external input

## 1.2.0
The copied actions need to be replaced by the rewritten actions like this: https://github.com/misskey-dev/misskey/commit/f5d57c02c7edbf71c4f2eaff789dfd093513027d .

- The `INDENT` variable allows selection of the indentation format of `package.json`.

## 1.1.2
- Fix: Creating Pre-release always creates rc

## 1.1.1
- Fix: release-with-ready not creating releases in external apps

## 1.1.0
- Make it possible to specify the app when creating a release, so that the `on: release` workflow can be triggered.

## 1.0.0
- The first release
