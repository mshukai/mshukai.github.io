## 仓库操作

## 分支操作
---
### 关联分支
```shell
# 直接关联
git branch --set-upstream-to=origin/<branch> <local_branch>

# 执行 git push 时关联
git push -u origin <remote_branch>

# 当项目跟踪的 git 远程仓库地址被改动（前提必须是同一个 Git 仓库，比如由 http 地址改为 ssh 地址），这时候再执行 git pull 会提示 refusing to merge unrelated histories
git pull --allow-unrelated-histories
```

### 删除分支
```shell
# 删除本地分支
git branch -d <branch>
# 删除远程分支
git push origin -d <remote_branch>

```

