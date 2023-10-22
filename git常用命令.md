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