# release-actions

## env in workflow yaml
<dl>
<dt><code>GITHUB_TOKEN</code></dt>
<dd>secrets.GITHUB_TOKEN</dd>
<dt><code>PACKAGE_JSONS_TO_REWRITE</code>: json array</dt>
<dd>package.jsons to rewrite version</dd>
</dl>

### 

```yaml
env:
  GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
  PACKAGE_JSONS: |
    ["package.json", "packages/misskey-js/package.json"]
```

## Variables

<dl>
<dt><code>RULESET_ID_WITHIN_RELEASE</code> <i>(optional)</i></dt>
<dd>Id of ruleset to be activated within release period</dd>
<dt><code>RULESET_ID_OUT_OF_RELEASE</code> <i>(optional)</i></dt>
<dd>Id of ruleset to be activated out of release period</dd>
</dl>
