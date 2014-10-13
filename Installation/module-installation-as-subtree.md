# Installing modules as subtrees

## Pulling


### Core module


```
git remote add core git@github.com:nWidart-Modules/Core.git
git subtree add --prefix=Modules/Core core develop
```

### Dashboard module


```
git remote add dashboard git@github.com:nWidart-Modules/Dashboard.git
git subtree add --prefix=Modules/Dashboard dashboard develop
```

### User module


```
git remote add user git@github.com:nWidart-Modules/User.git
git subtree add --prefix=Modules/User user develop
```

### Workshop module


```
git remote add workshop git@github.com:nWidart-Modules/Workshop.git
git subtree add --prefix=Modules/Workshop workshop develop
```


### Blog module


```
git remote add blog git@github.com:nWidart-Modules/Blog.git
git subtree add --prefix=Modules/Blog blog develop
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

