# Git Pull Requests Resource

Tracks the pull requests in a [git](http://git-scm.com/) repository and posts a status message on the pull requests with success/failure of a build.


## Source Configuration

* `uri`: *Required.* The location of the repository.

* `access_token`: *Required.* Used for accessing a release in a private-repo 
   during an `in` and pushing a release to a repo during an `out`.

* `repo`: *Required.* The repository name that contains the releases.

* `private_key`: *Optional.* Private key to use when pulling/pushing.
    Example:
    ```
    private_key: |
      -----BEGIN RSA PRIVATE KEY-----
      MIIEowIBAAKCAQEAtCS10/f7W7lkQaSgD/mVeaSOvSF9ql4hf/zfMwfVGgHWjj+W
      <Lots more text>
      DWiJL+OFeg9kawcUL6hQ8JeXPhlImG6RTUffma9+iGQyyBMCGd1l
      -----END RSA PRIVATE KEY-----
    ```

* `username`: *Required.* The GitHub username or organization name for the repository that the releases are in.

## Behavior

### `check`: Check for new commits.

The repository is cloned (or pulled if already present), and any commits
made after the given version are returned. If no version is given, the ref
for `HEAD` is returned.

### `in`: Clone the repository, at the given ref.

Clones the repository to the destination, and locks it down to a given ref.
Returns the resulting ref as the version.

Submodules are initialized and updated recursively.


#### Parameters

* `depth`: *Optional.* If a positive integer is given, *shallow* clone the
  repository using the `--depth` option.


* `fetch`: *Optional.* Additional branches to fetch so that they're available
  to the build.

* `submodules`: *Optional.* If `none`, submodules will not be
  fetched. If specified as a list of paths, only the given paths will be
  fetched. If not specified, or if `all` is explicitly specified, all
  submodules are fetched.


### `out`: Push to a repository.

Push a repository to the source's URI and branch. All tags are also pushed
to the source.

#### Parameters

* `repository`: *Required.* The path of the repository to push to the source.

* `state`: *Optional.* The state of the build status for the pullrequest. Default to `success`.

* `description`: *Optional.* The copy for the status message on the pull request.
