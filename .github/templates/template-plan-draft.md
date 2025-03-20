### PR files:
<details><summary>Click to expand</summary>

```sh
${{ steps.git-diff.outputs.all_changed_files }}
```

</details>

### PR files eligible for plan:
<details><summary>Click to expand</summary>

```sh
${{ steps.filter-files.outputs.all_filtered_files || 'Files eligible for plan not found' }}
```

</details>

### PR plan output:
<details><summary>Click to expand</summary>

```hcl
${{ steps.terragrunt-plan.outputs.plan || 'No available plan output' }}
```

</details>
