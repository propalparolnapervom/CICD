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
  - `tag_file`: Optional. The value should be a path to a file containing the name of the tag.
  - `tag_as_latest`: Optional. Default `false`. If `true`, the pushed image will be tagged as latest in addition to whatever other tag was specified.




















