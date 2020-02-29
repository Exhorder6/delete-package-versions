# Delete Package Versions

This action deletes versions of a package from [GitHub Packages](https://github.com/features/packages). 

### What It Can Do

* Delete a single version
* Delete multiple versions
* Delete specific version(s) 
* Delete oldest version(s)
* Delete version(s) from a package that is hosted in the same repo that is executing the workflow
* Delete version(s) from a package that is hosted in a different repo than the one executing the workflow

# Usage

```yaml
- uses: actions/delete-package-versions@v1
  with:
  # Can be a single package version id, or a comma separated list of package version ids.
  # Defaults to an empty string.
  package-version-ids:
  
  # Owner of the repo hosting the package.
  # Defaults to the owner of the repo executing the workflow.
  # Required if deleting a version from a package hosted in a different repo than the one executing the workflow.
  owner:

  # Repo hosting the package.
  # Defaults to the repo executing the workflow.
  # Required if deleting a version from a package hosted in a different repo than the one executing the workflow.
  repo:

  # Name of the package.
  # Defaults to an empty string.
  # Required if `package-version-ids` input is not given.
  package-name:

  # The number of old versions to delete starting from the oldest version.
  # Defaults to 1.
  num-old-versions-to-delete:

  # The token used to authenticate with GitHub Packages.
  # Defaults to github.token.
  # Required if deleting a version from a package hosted in a different repo than the one executing the workflow.
  #   If `package-version-ids` is given the token only needs the delete packages scope.
  #   If `package-version-ids` is not given the token needs the delete packages scope and the read packages scope
  token:
```

# Scenarios

* [Delete a specific version from a package hosted in the same repo as the workflow](#delete-a-specific-version-from-a-package-hosted-in-the-same-repo-as-the-workflow)
* [Delete a specific version from a package hosted in a different repo than the workflow](#delete-a-specific-version-from-a-package-hosted-in-a-different-repo-than-the-workflow)
* [Delete multiple specific versions from a package hosted in the same repo as the workflow](delete-multiple-specific-versions-from-a-package-hosted-in-the-same-repo-as-the-workflow)
* [Delete multiple specific versions from a package hosted in a different repo than the workflow](delete-multiple-specific-versions-from-a-package-hosted-in-a-different-repo-than-the-workflow)



### Delete a specific version from a package hosted in the same repo as the workflow

Package version ids can be retrieved via the [GitHub GraphQL API][api].

```yaml
- uses: actions/delete-package-versions@v1
  with:
    package-version-ids: 'MDE0OlBhY2thZ2VWZXJzaW9uOTcyMDY3'
```



### Delete a specific version from a package hosted in a different repo than the workflow

Package version ids can be retrieved via the [GitHub GraphQL API][api]. The token input is required to delete a version of a package hosted in a different repo than the workflow. The [token][token] only needs the delete packages scope. It is recommended [to store the token as a secret][secret]. In this example the [token][token] was stored as a secret named __GITHUB_PAT__.

```yaml
- uses: actions/delete-package-versions@v1
  with:
    package-version-ids: 'MDE0OlBhY2thZ2VWZXJzaW9uOTcyMDY3'
    token: ${{ secrets.GITHUB_PAT }}
```



### Delete multiple specific versions from a package hosted in the same repo as the workflow

To delete multiple specifc versions of a package set __package-version-ids__ to a comma separated string of package version ids. Package version ids can be retrieved via the [GitHub GraphQL API][api].

```yaml
- uses: actions/delete-package-versions@v1
  with:
    package-version-ids: 'MDE0OlBhY2thZ2VWZXJzaW9uOTcyMDY3, MDE0OlBhY2thZ2VWZXJzaW9uOTcyMzQ5, MDE0OlBhY2thZ2VWZXJzaW9uOTcyMzUw'
```

<br>

### Delete multiple specific versions from a package hosted in a different repo than the workflow

To delete multiple specifc versions of a package set __package-version-ids__ to a comma separated string of package version ids. Package version ids can be retrieved via the [GitHub GraphQL API][api]. The token input is required to delete a version of a package hosted in a different repo than the workflow. The [token][token] only needs the delete packages scope. It is recommended [to store the token as a secret][secret]. In this example the [token][token] was stored as a secret named __GITHUB_PAT__.

```yaml
- uses: actions/delete-package-versions@v1
  with:
    package-version-ids: 'MDE0OlBhY2thZ2VWZXJzaW9uOTcyMDY3, MDE0OlBhY2thZ2VWZXJzaW9uOTcyMzQ5, MDE0OlBhY2thZ2VWZXJzaW9uOTcyMzUw'
    token: ${{ secrets.GITHUB_PAT }}
```



# License

The scripts and documentation in this project are released under the [MIT License](https://github.com/actions/delete-package-versions/blob/master/LICENSE)

[api]: https://developer.github.com/v4/previews/#github-packages
[token]: https://help.github.com/en/packages/publishing-and-managing-packages/about-github-packages#about-tokens
[secret]: https://help.github.com/en/actions/configuring-and-managing-workflows/creating-and-storing-encrypted-secrets

