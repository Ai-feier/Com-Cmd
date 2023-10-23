配置(在./git 下的 config )
```bash
git config --global --list
    作用域：--local, --global, --system
```

git add
```bash
git add -u # 更新工作区内容
git add . # 可直接加文件或目录 git add dir a.txt
```

清空暂存区的内容
```bash
git reset --hard
```

git log 
```bash
git log --oneline --all --n3 --graph
```

查看 git 文件信息
```bash
git cat-file -t 前缀哈希值  # 类型
git cat-file -p 前缀哈希值  # 详细信息
```

git checkout
```bash
git checkout <前缀哈希>   # 分离头指针, 注意保存, 绑定分支
git checkout -b <new-branch>
```

git diff 
- 比较 commit 间的差异
- 比较暂存区与 HEAD 的差异
- 比较工作区与暂存区的差异
```bash
git diff <前缀哈希> <前缀哈希>
git diff HEAD HEAD^(HEAD^1/HEAD^1^1/HEAD~1/HEAD~2:commit的父节点)

git diff --cached  # 比较暂存区与 HEAD 的差异
git diff  # 比较工作区与暂存区的差异
git diff -- <file-name> <file-name>  # 指定文件

git diff <branch1> <branch2> -- <file>...  # 比较分支
git diff <哈希前缀> <哈希前缀> -- <file>...  # 比较 commit
```

删除分支
```bash
git branch -d/D <branch-name>
```

对最近一次的commit进行变更
```bash
git commit --amend 
```

变基（选择要更改commit的父commit）
- 修改以前 commit 消息 (r)
- 合并多个连续或不连续的 commit (s)
```bash
git rebase -i <前缀哈希>
    # -i 交互式
```

git reset 
```bash
git reset HEAD  # 清空暂存区
git reset HEAD -- <file-name>...  # 指定恢复文件
```

> 变更暂存区：reset
> 变更工作区：checkout

将工作区文件变更为暂存区版本
```bash
git checkout -- <file-name>
```


git rm 
```bash
git rm <file>...
```

git stash
- 把当前工作区暂存起来，后清空
```bash
git stash  # 暂存当前工作区
git stash list
git stash apply  # 把 stash 栈中数据恢复到工作区
git stash pop  # 把 stash 栈中数据恢复到工作区病弹出stash 栈中数据
```

git remote
```bash
git remote -v  # 显示
git remote add <name> <远程 git 地址> 
```

git push
```bash
git push <remote-name>  # 把当前分支推送到 reomte 地址
git push --set-upstream <remote-name> <now-branch>  # 设置上游
```

git pull = git fetch + merge
要 push 到远端，要当前版本节点是远端版本的父节点，fetch远端分支后 切换到当前要push的分支，后merge远端分支





### 远程
查看远程仓库地址
```bash
git remote show origin
git remote -v
```

设置新的仓库地址
```bash
设置新的仓库地址
git remote set-url origin <remote-url>
```


删除命令
```bash
git rm -r --cached 文件/文件夹名字
```

### 分支
创建独立分支
```bash
git checkout --orphan 分支名
```

关联
```bash
$git branch --set-upstream-to=origin/newBranch
```

删除分支
```bash
git branch –delete dev
```