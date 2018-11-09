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




















