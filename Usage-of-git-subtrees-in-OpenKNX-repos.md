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

## update the subtree

pull the latest commit from master branch into the subtree
```
git subtree pull --prefix lib/knx subtree-knx master --squash
```