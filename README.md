# Release Manager
GitHub Actions workflows for release management of the repository. 

## Flow
![](flow.png)

## Installation
### 1. Variable(s) to set
- If you want to rewrite package.json(s), set `PACKAGE_JSONS_TO_REWRITE` and `INDENT` according to [the Variables clause](#variables).

### 2. workflows you should copy
Copy and use these workflows.

#### ⅰ. release-with-dispatch.yml (Release Manager [Dispatch])
The core workflow that is manually triggered. It has three functions:

1. Prepare release - create release branch, beta.0 tag, and PR
2. Issue a pre-release version during the release process
3. Issue a stable release when you check `MERGE RELEASE BRANCH TO MAIN`

#### ⅱ. release-edit-with-push.yml
This workflow changes the description of the PR when CHANGELOG.md is changed.

#### ⅲ. release-with-ready.yml
Release rc when PR becomes ready for review.

## If you have `on: release` workflows...
If you have workflow(s) with `on: release`, you must create a GitHub App with following settings and set `RELEASE_APP_ID` and `RELEASE_APP_PRIVATE_KEY` as secrets.

Please execute following installation: https://github.com/actions/create-github-app-token/tree/v1/?tab=readme-ov-file#usage

|App Settings||
|:--|:--|
|Webhook||
|Active|disabled|
|Repository permission||
|Contents|Read and Write|

Open `Install App` tab and install to the repository or whole the user/organization.

Then set `USE_RELEASE_APP` as `true` [as a repository variable](https://docs.github.com/en/actions/learn-github-actions/variables#creating-configuration-variables-for-a-repository).

The reason is that `on: release` workflows are not triggered for releases created with the default `GITHUB_TOKEN`.

You can share the application and the private key with ruleset management.

## Ruleset management
You can enable/disable ruleset for release working and non-working periods.

To enable ruleset management, you must create an GitHub App with following settings and set `RULESET_EDIT_APP_ID` and `RULESET_EDIT_APP_PRIVATE_KEY` as secrets.  
Reference: https://github.com/actions/create-github-app-token/tree/v1/

|App Settings||
|:--|:--|
|Webhook||
|Active|disabled|
|Repository permission||
|Administration|Read and Write|

Open `Install App` tab and install to the repository or whole the user/organization.

Then create the ruleset(s) you want to use and set its (their) ID to `RULESET_ID_WITHIN_RELEASE` or `RULESET_ID_OUT_OF_RELEASE` as variable(s).  
For example, create a ruleset with enabling `Restrict updates` (to lock the main branch) during the release work period and set it to `RULESET_ID_WITHIN_RELEASE`.

## Repository secrets and variables
### Secrets
<dl>
<dt><code>RELEASE_APP_ID</code></dt>
<dd>See "If you have `on: release` workflows..."</dd>
<dt><code>RELEASE_APP_PRIVATE_KEY</code></dt>
<dd>See "If you have `on: release` workflows..."</dd>
<dt><code>RULESET_EDIT_APP_ID</code> <i>(optional)</i></dt>
<dd>See Ruleset management</dd>
<dt><code>RULESET_EDIT_APP_PRIVATE_KEY</code> <i>(optional)</i></dt>
<dd>See Ruleset management</dd>
</dl>

### Variables

<dl>
<dt><code>PACKAGE_JSONS_TO_REWRITE</code> <i>(optional)</i></dt>
<dd>package.jsons to rewrite version<br>e.g. <code>"package.json" "packages/misskey-js/package.json"</code></dd>
<dt><code>INDENT</code> <i>(required when PACKAGE_JSONS_TO_REWRITE be set)</i></dt>
<dd>Indent type of package.json.<br><code>tab</code> or number of spaces</dd>
<dt><code>USE_RELEASE_APP</code></dt>
<dd>See "If you have `on: release` workflows..."</dd>
<dt><code>RULESET_ID_WITHIN_RELEASE</code> <i>(optional)</i></dt>
<dd>See Ruleset management</dd>
<dt><code>RULESET_ID_OUT_OF_RELEASE</code> <i>(optional)</i></dt>
<dd>See Ruleset management</dd>
</dl>
