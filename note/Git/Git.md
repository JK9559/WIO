### 时光穿梭
1. ```git add .```
    + 把要提交的修改放到暂存区 ```Stage```
2. ```git commit -m 'commit files'```
    + 一次性把 ```Stage``` 的所有修改提交到分支
3. ```git push```
4. ```git log```
    + 作用是查看提交历史
    + ```--pretty=oneline``` 选项，作用是只展示 ```commit id``` 和提交注释信息。
5. ```git``` 版本：
    + ```HEAD``` 表示当前版本
    + ```HEAD^``` 表示上一个版本
    + ```HEAD^^``` 表示上上一个版本
    + ```HEAD~100``` 表示上 100 个版本
6. ```git reset```：
    + 将内容重置为上个版本：```git reset --hard HEAD^```
    + 将回滚的内容再还原到当前的版本：需要找到某个版本的 ```commit id``` ，然后：```git reset --hard commit_id```
    + 如果使用了 ```git add``` 添加了文件到 ```Stage```, 可以使用 ```git reset HEAD file_name``` 将存到暂存区的文件拿出来到工作区
7. ```git reflog```
    + 作用是查看命令历史，可以找到历史的 ```commit id``` 方便进行回滚
8. ```git diff HEAD -- file_name```
    + 比较变化：```git diff HEAD -- file_name```
9. ```git checkout -- file_name```
    + 可以丢弃工作区的修改，回滚工作区到上一次 ```git commit``` 或者 ```git add```
    + 当修改后没有 ```git add``` 就是回滚到上次的 ```git commit```
    + 当修改后 ```git add``` 了，就是回滚到上次的 ```git add```

### 分支管理
1. ```git checkout -b dev```：
    + 表示创建并切换到 ```dev``` 分支
    + 相当于以下两条命令：
        + ```git branch dev``` 创建分支 ```dev```
        + ```git checkout dev``` 切换分支到 ```dev```
    + 通过命令 ```git branch``` 查看当前分支
2. ```git merge branch_name```
    + 作用是将 ```branch_name``` 分支 合并到当前分支
3. ```git branch -d branch_name```
    + 删除分支
4. ```git switch -c branch_name```：
    + 创建并切换到 ```branch_name``` 分支
5. ```git switch branch_name```：
    + 切换到 ```branch_name``` 分支
#### 解决冲突
6. ```git log --graph```：
    + 查看分支合并图
7. ```git merge --no-ff -m 'merge branch' branch_name```：
    + 使用 ```--no-ff``` 之后 采用普通模式合并，合并后的历史有分支，能看出做过合并
    + 不使用参数，默认用 ```fast forward``` 合并，无法看出曾经做过合并
#### BUG分支
8. ```git stash```
    + 将工作现场存储起来，后续再用。
9. 改完其他的文件。
10. 查看 ```stash``` 的工作现场：```git stash list```
11. 复原现场：```git stash pop```
12. 丢弃一个没有合并的分支，使用 ```git branch -D <branch_name>``` 强制删除分支
13. 