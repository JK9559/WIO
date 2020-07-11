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
7. ```git reflog```
    + 作用是查看命令历史，可以找到历史的 ```commit id``` 方便进行回滚