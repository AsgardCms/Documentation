# Installing modules as subtrees

## Pulling


### Core module


```
git remote add core git@github.com:nWidart-Modules/Core.git
git subtree add --prefix=Modules/Core core master
```

### Dashboard module


```
git remote add dashboard git@github.com:nWidart-Modules/Dashboard.git
git subtree add --prefix=Modules/Dashboard dashboard master
```

### User module


```
git remote add user git@github.com:nWidart-Modules/User.git
git subtree add --prefix=Modules/User user master
```

### Workshop module


```
git remote add workshop git@github.com:nWidart-Modules/Workshop.git
git subtree add --prefix=Modules/Workshop workshop master
```


### Blog module


```
git remote add blog git@github.com:nWidart-Modules/Blog.git
git subtree add --prefix=Modules/Blog blog master
```

### Setting module


```
git remote add setting git@github.com:nWidart-Modules/Setting.git
git subtree add --prefix=Modules/Setting setting master
```

### Menu module


```
git remote add menu git@github.com:AsgardCms/Menu.git
git subtree add --prefix=Modules/Menu menu master
```

### Media module


```
git remote add media git@github.com:AsgardCms/Media.git
git subtree add --prefix=Modules/Media media master
```

## Pushing


## User module

Example:

```
git subtree push --prefix=Modules/User user fixing-user-seed-name
```

Abstract:

```
git subtree push --prefix=Modules/User [remote-name] [branch]
```

## Core module

Example:

```
git subtree push --prefix=Modules/Core core adding-install-command
```



## Pulling


## Core module

```
git subtree pull --prefix=Modules/Core --squash core master
```

## User module

```
git subtree pull --prefix=Modules/User --squash user master
```

## Dashboard module

```
git subtree pull --prefix=Modules/Dashboard --squash dashboard master
```

## Workshop module

```
git subtree pull --prefix=Modules/Workshop --squash workshop master
```

## Setting module

```
git subtree pull --prefix=Modules/Setting --squash setting master
```
## Menu module

```
git subtree pull --prefix=Modules/Menu --squash menu master
```

## Media module

```
git subtree pull --prefix=Modules/Media --squash media master
```

## References

* [git subtree tutorial on medium](https://medium.com/@v/git-subtrees-a-tutorial-6ff568381844)