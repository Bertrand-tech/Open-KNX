# example usage

```
git remote add -f subtree-knx https://github.com/thelsing/knx.git
git subtree add --prefix lib/knx subtree-knx master --squash

git remote add -f subtree-OAM-LogicModule https://github.com/OpenKNX/OAM-LogicModule.git
git subtree add --prefix lib/OAM-LogicModule subtree-OAM-LogicModule main --squash

git remote add -f subtree-OGM-Common https://github.com/OpenKNX/OGM-Common.git
git subtree add --prefix lib/OGM-Common subtree-OGM-Common main --squash
```