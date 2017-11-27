# Git

## Tags

Deleting a tag locally and on remote:
```sh
git tag -d my-tag                   // delete locally
git push orign :refs/tags/my-tag    // update remote to remove tag
```

## Refs/Diffing

`master^` is equivalent to `master~1`
`master^^` is equivalent to `master~2`

These git diff commands are all equivalent:

```sh
git diff master~1 master
git diff master~1..master
git diff master~1..
git diff master^ master
git diff master~1 HEAD
```

Another useful tool for refs is `git rev-parse` it can be used to get the SHA-1
of a named reference (like master, a branch, or HEAD):

For example:
```sh
git rev-parse master
// => 6blksfio23hskfh3h324 (some sha)
```

[A great blog post with some neat git tricks](https://csswizardry.com/2017/05/little-things-i-like-to-do-with-git/#generate-a-changelog)
