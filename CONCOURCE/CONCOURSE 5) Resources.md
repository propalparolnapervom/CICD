# CONCOURSE 5) RESOURCES


# RESOURCES TYPES

## docker-image

[docker-image repository](https://github.com/concourse/docker-image-resource)



### `in`

Pulls down the repository image by the requested digest.



### `out`

Push a Docker image to the source's repository and tag. The resulting version is the image's digest.

**Parameters**

  - `build`: Optional. The path of a directory containing a `Dockerfile` to build.
  - `tag`: DEPRECATED - Use `tag_file` instead
  - `tag_file`: Optional. The value should be a path to a file containing the name of the tag.
  - `tag_as_latest`: Optional. Default `false`. If `true`, the pushed image will be tagged as latest in addition to whatever other tag was specified.
  - `load_base`: Optional. A path to a directory containing an image to `docker load` before running `docker build`. The directory must have `image`, `image-id`, `repository`, and `tag` present, i.e. the tree produced by /in.



## git-resource

[git-resource](https://github.com/concourse/git-resource)

### Source Configuration

  - `paths`: Optional. If specified (as a list of glob patterns), only changes to the specified files will yield new versions from `check`.
  - `ignore_paths`: Optional. The inverse of paths; changes to the specified files are ignored.
 
> Note: if you want to push commits that change these files via a put, the commit will still be "detected", as check and put both introduce versions. To avoid this you should define a second resource that you use for commits that change files that you don't want to feed back into your pipeline - think of one as read-only (with ignore_paths) and one as write-only (which shouldn't need it).


### `check`: Check for new commits.

The repository is cloned (or pulled if already present), and any commits from the given version on are returned. 

If no version is given, the ref for `HEAD` is returned.

Any commits that contain the string `[ci skip]` will be ignored. 

This allows you to commit to your repository without triggering a new version.


### `in`: Clone the repository, at the given ref.

Parameters:
  
  - `submodules`: Optional. If none, submodules will not be fetched. If specified as a list of paths, only the given paths will be fetched. If not specified, or if all is explicitly specified, all submodules are fetched.









