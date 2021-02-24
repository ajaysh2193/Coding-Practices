## Creating a new release consists of the following steps:

* Prepare release branch
* Final updates and checks
* Merge
* Dependent repositories and announcements

## Preparing the release branch
### Deciding the type of release
We use [semantic versioning](https://semver.org/), i.e. version labels have the form v<major>.<minor>.<patch>

Patch release: `v0.0.1` to `v0.0.2`, only bug fixes
Minor release: `v0.0.1` to `v0.1.0`, bug fixes and new features that maintain backwards compatibility
Major release: `v0.9.0` to `v1.0.0`, bug fixes and new features that break backwards compatibility

### Creating the release branch
We use the [gitflow](https://nvie.com/posts/a-successful-git-branching-model/) branching model. In short: since the last release, new features and bug fixes will have been merged into the `dev` branch through pull requests.

**Patch release**
Branch off the new release branch from the latest release tag.

`git checkout tags/v0.0.1 -b release_v0.0.2`

**Note:** Usually, this branch will already exist and you can skip this step!

## Creating tags 
[Create a release tag for your branch using Git UI](https://git-scm.com/book/en/v2/Git-Basics-Tagging)


## Managing and merging tags
Follow the below commands:
```
  git checkout -b release/<release_number>
  git tag <tag_number>
  git checkout dev
  git merge <tag_number>
  git push --tags origin dev

  git checkout master
  git merge --ff-only <release_number>

  git checkout release/<release_number>
  git branch -d release/<release_number>
```

