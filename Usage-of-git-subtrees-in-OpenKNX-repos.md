**this information is maybe deprecated. Git Subtrees are not the preferd solution in the OpenKNX project at the time of writing this.**

# example usage

## setup

using master / main branch in the subtree command will select the latest commit in that branch. This subtree is exactly this commit until a `git subtree pull` is performed.

```
git remote add -f subtree-knx https://github.com/thelsing/knx.git
git subtree add --prefix lib/knx subtree-knx master --squash

git remote add -f subtree-OGM-Common https://github.com/OpenKNX/OGM-Common.git
git subtree add --prefix lib/OGM-Common subtree-OGM-Common main --squash

git remote add -f subtree-OAM-LogicModule https://github.com/OpenKNX/OAM-LogicModule.git
git subtree add --prefix lib/OAM-LogicModule subtree-OAM-LogicModule main --squash
```

use specific releases:
```
git subtree add --prefix lib/OAM-LogicModule subtree-OAM-LogicModule 0.12.1-Beta --squash
```


## update the subtree

pull the latest commit from master branch into the subtree
```
git subtree pull --prefix lib/knx subtree-knx master --squash
```

change the subtree from any branch / tag / commit to another one ("V1.2.3")
```
git rm lib/knx
git commit
git remote add -f subtree-knx https://github.com/thelsing/knx.git
git subtree add --prefix lib/knx subtree-knx V1.2.3 --squash
git push
```


## commit / push changes in the subtree to its repo
```
git commit
git subtree push --prefix lib/OGM-Common subtree-OGM-Common main
```


# Links
https://gist.github.com/SKempin/b7857a6ff6bddb05717cc17a44091202
