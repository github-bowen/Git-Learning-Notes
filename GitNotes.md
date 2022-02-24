## Git Bash/Ubuntu Terminal快捷键

- 复制：```ctrl + insert``` / ```shift + ctrl + c```
- 粘贴：```shift + insert``` / ```shift + ctrl + v```

## Git 命令

### Git初始化与帮助


- 设置名字和邮箱

  ```shell
  $ git config --global user.name "Your Name"
  $ git config --global user.email "email@example.com"
  ```

- 查看当前编辑者姓名和邮箱

  ```shell
  $ git config user.name
  $ git config user.email
  ```

- 查看git工具版本

  ```shell
  $ git version
  # or
  $ git --version
  ```

### 创建repository

- 创建空的Git仓库

  - 缺省，初始分支名为master：

    ```shell
    $ git init
    ```

  - 指定初始分支名：

    ```shell
    $ git init --initial-branch=<branch name>
    # e.g.
    $ git init --initial-branch=main
    ```

- 添加文件(夹)：

  ```shell
  $ git add <fils>/<directory>
  ```

  特殊：add所有文件

  ```shell
  $ git add .
  ```

- 提交文件：（带说明）

  ```shell
  $ git commit -m "commit instructions"
  ```

  提交文件的说明可以同时针对多个文件：

  ```shell
  $ git add file1.txt
  $ git add file2.txt file3.txt
  $ git commit -m "add 3 files."
  ```

### 增删改查

- 查看仓库状态（是否有文件被修改未add，add后未commit；即工作区、暂存区、版本库间区别）：

  ```shell
  $ git status
  ```

- 查看**工作区**与**暂存区**的区别：

  ```shell
  $ git diff
  ```

  查看**工作区**和**版本库**的区别：

  ```shell
  $ git diff HEAD -- file
  ```

- ```git log```（查看commit历史信息）相关：

  - 基本命令（不带参数）：

    ```shell
    $ git log
    ```

  - commit在一行内显示：

    ```shell
    $ git log --pretty=oneline
    # or
    $ git log --oneline
    ```

  - 用图线展示branch历史：

    ```shell
    $ git log --branch --pretty=oneline
    ```

  - 缩短commit id：

    ```shell
    $ git log --abbrev-commit
    ```

  - 展示最新n次commit：

    ```shell
    $ git log -n
    ```

- 查看输入的命令历史：（来确定要回到未来的哪个版本）

  ```shell
  $ git reflog
  ```

- **回退与撤销**

  - 回退（版本库）版本——在committed(版本库)中切换： 

    > - HEAD：当前版本
    >
    > - HEAD^：上一个版本
    >
    > - HEAD^^：上上个版本
    >
    > - HEAD~100：上100个版本
    >
    > 回退上一个版本： 
    > ```shell
    > $ git reset --hard HEAD^
    > ```
    > 根据版本号回退到制定版本（包括"未来"的版本，下面1094a为版本号前5位）：
    > ```shell
    > $ git reset --hard 1094a
    > ```
  
  - 撤销工作区修改——从工作区回退到最近一次commit（版本库）或add（暂存区）的状态:
    >即直接丢弃工作区：（checkout还有其他用法：见下面*恢复从版本库删除的某个文件*）
    >```shell
    >$ git checkout -- file
    >```
    >或
    >```shell
    >$ git restore file
    >```
    
  - 撤销暂存区修改——将暂存区修改撤销，放回工作区：
  
    > 即丢弃暂存区，放回工作区（工作区可以进一步丢弃）：
    >
    > ```shell
    > $ git reset HEAD file
    > ```
    > 或
    > ```shell
    > $ git restore --staged file
    > ```
  
- 从版本库删除某个文件（本地，即工作区也会一起被删除）：

  ```shell
  $ git rm file
  $ git commit -m "message"
  ```

  若在工作区误删某个文件，可以通过如下命令从版本库恢复到工作区：

  ```shell
  $ git checkout -- file
  ```

  或：

  ```shell
  $ git restore file
  ```

  *删除与修改命令相同的原因：*删除也是一种改变

### 远程仓库

#### 预备工作

- 注：笔记中使用```SSH```协议，github还支持```HTTP```协议。

- 准备工作步骤

  1. 进入用户主目录(c:Users/UserName)：

     ```shell
     $ cd ~
     ```

  2. 创建SSH Key：

     ```shell
     $ ssh-keygen -t rsa -C "youremail@example.com"
     ```

     一路回车后（一开始会问要不要设置密码，回车即不需要）在/.ssh中有```id_rsa```(私钥)和```id_rsa.pub```(公钥)。

  3. 在Github设置SSH Key：填上任意Title，在Key文本框里粘贴`id_rsa.pub`文件的内容。
  
  4. 补：**设置新SSH**
  
     进入```.ssh```文件夹后，输入命令：
  
     ```shell
     ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
     ```
  
     按一次回车后会问：```Overwrite (y/n)? ```，输入```y```后步骤同上。
  

#### 本地库→远程仓库

- **首次**将本地库push到远程库上：（在github中新建了```GitLearningNotes```这一repository）
  
  在本地对应仓库运行命令：
  
  ```shell
  $ git remote add origin git@github.com:<github name>/<repository name>.git
  ```
  
  e.g.:
  
  ```shell
  $ git remote add origin git@github.com:NormalLLer/GitLearningNotes.git
  $ git remote add origin git@gitlab.oo.buaa.edu.cn:oo_2022/pre_2022_2_20231198_pre2_task2.git
  ```
  
  然后：
  
  ```shell
  $ git push -u origin master
  ```
  
- 将本地库push到远程库origin：

  - 格式一：（默认远程库分支名与本地分支名相同）

    ```shell
    $ git push <remote name> <local branch name>
    $ git push origin master  # 将本地当前分支push到origin库的master分支上
    ```

  - 格式二：（重命名远程库分支名）

    ```shell
    $ git push <remote name> <local branch name>:<remote branch name>
    # 将local-branch推送到remote并改名为remote-branch-name
    ```
  

  - 注：可用```--force```参数强行push，但有风险！
  
    ```shell
    # e.g.
    $ git push --force javarepo main
    ```

#### 远程仓库→本地库

- 从远程库克隆（**首次**）：

  ```shell
  # git clone <repo:local/SSH/HTTP>
  $ git clone git@github.com:<Github name>/<repository name>.git
  ```

- 获取远程仓库更新（但不与本地库合并）：

  ```shell
  $ git fetch <remote name>
  ```

- (在fetch后)将其的某个分支与本地当前分支合并：

  ```shell
  $ git merge <remote name>/<remote branch name>
  ```

- 以上两个命令的合并：

  ```shell
  $ git pull <remote name> <remote branch name>:<local branch name>
  # or
  $ git pull <remote name> <remote branch name>
  # or
  $ git pull
  ```
  
- 退出合并：(恢复合并前状态)

  ```shell
  $ git merge --abort
  ```


#### 其它

- 查看远程库信息：

  ```shell
  $ git remote
  # or
  $ git remote -v
  ```

- 删除远程库：（指解除本地库与远程库的绑定）

  ```shell
  $ git remote rm name
  # e.g:
  $ git remote rm origin
  ```

- 删除远程库某个分支：

  ```shell
  $ git push <remote name> --delete <remote branch name>>
  # e.g.
  $ git push origin --delete testbranch2	
  ```

- 当远程仓库（别人修改）和本地仓库（自己修改）冲突时：
  - 方法一：先pull（fetch + merge）下来后修改再push（根据git bash的输出反馈进行操作）
  - 方法二：采用rebase（略）

### 分支管理

- 创建分支：

  ```shell
  $ git branch <name>
  ```

- 切换分支：

  ```shell
  $ git checkout <name>
  # or
  $ git switch <name>
  ```

- 修改本地分支名：

  ```shell
  $ git branch -m <old> <new>
  # e.g.
  $ git branch -m master main  # 将master修改为main
  ```

- 创建并切换分支：

  ```shell
  $ git checkout -b <name>
  # or
  $ git switch -c <name>
  ```

- 创建并将指定远程分支clone到本地：

  ```shell
  $ git switch -c <local branch name> <remote name>/<remote branch name>
  # e.g.
  $ git switch -c localtest origin/testbranch
  ```

- 查看分支：

  - 查看本地库分支：

    ```shell
    $ git branch
    ```

  - 查看远程库分支：

    ```shell
    $ git branch -r
    ```

  - 查看所有分支：

    ```shell
    $ git branch -a
    ```

- fast forward模式与name分支合并（合并后log中无分支名字）：

  ```shell
  $ git merge <name>
  ```

- 删除本地分支：

  ```shell
  $ git branch -d <name>
  ```

- 在个```git log```后添加参数：

  ```shell
  $ git log --graph --pretty=oneline --abbrev-commit -n
  # --graph: 用ascii图表示分支合并历史
  # --abbrev-commit: 缩写前面序号SHA （abbreviation n.缩写）
  # -n: 显示最新n条
  ```


- 普通模式合并分支（合并后log有分支名记录）：

  ```shell
  $ git merge --no-ff -m "annotation" <branch name>
  ```

- 将本地```lb```分支与远程```rb```分支建立链接：

  ```shell
  $ git branch --set-upstream-to=<remote name>/<remote branch name> <local branch name>
  # e.g.
  $ git branch --set-upstream-to=origin/rb lb
  ```

### Stash 相关

注：stash v.  藏

- [参考链接](https://www.cnblogs.com/tocy/p/git-stash-reference.html)

- 储藏当前修改（包括工作区和暂存区）：

  ```shell
  $ git stash
  # or add annotations by "save"
  $ git stash save "annotations"
  ```

- 恢复stash：

  ```shell
  # 将缓存堆栈中的第一个stash弹出并删除
  $ git stash pop
  ```

  ```shell
  # 将缓存堆栈中的第一个stash输出但不删除
  $ git stash apply
  # 输出制定stash
  $ git stash apply stash@{0}  # e.g. 输出最新
  ```

  ```shell
  # 删除stash
  $ git stash drop
  $ git stash drop stash@{0}
  ```

- 查看现有stash：

  ```shell
  $ git stash list
  ```

### 标签相关

- 创建标签

  ```shell
  $ git tag -a <tag name> -m "annotations" <commit id>
  ```

  - 形式一：在最新commit创建tag

    ```shell
    $ git tag <name>
    # e.g.
    $ git tag v1.0
    ```

  - 形式二：在指定```commit id```创建tag

    ```shell
    $ git tag <name> <id>
    # e.g.
    $ git tag v1.1 f52c633
    ```

  - 形式三：在指定```commit id```创建带有说明文字的tag

    ```shell
    $ git tag -a <tag name> -m "annotations" <commit id>
    # e.g.
    $ git tag -a v1.2 -m "create tag v1.2 in id:1094ab" 1094ab
    ```

- 查看标签列表：

  ```shell
  $ git tag
  ```

- 查看tag具体说明：(tag说明文字、commit说明文字等)

  ```shell
  $ git show <tag name>
  ```

- 本地仓库删除标签：

  ```shell
  $ git tag -d <tag name>
  ```

- 本地与远程仓库的相关信息交互

  - 推送指定标签到远程：

    ```shell
    $ git push <remote name> <tag name>
    # e.g.
    $ git push origin v1.0
    ```

  - 推送所有标签到远程：

    ```shell
    $ git push <remote name> --tags
    ```

  - 从远程仓库删除指定tag：

    - 先从本地删除（设删除v0.9)

      ```shell
      $ git tag -d v0.9 
      ```

    - 再删除远程tag：

      ```shell
      $ git push <remote name> :refs/tags/<tag>
      # e.g.
      $ git push origin :refs/tags/v0.9
      ```

      

## 相关资料

- [廖雪峰Git教程](https://www.liaoxuefeng.com/wiki/896043488029600)
- [廖雪峰Git命令整理](https://liaoxuefeng.gitee.io/resource.liaoxuefeng.com/git/git-cheat-sheet.html#)
- [Linux常用命令整理](https://www.cnblogs.com/hi3254014978/p/12643601.html)
- [git log参数](https://www.cnblogs.com/bellkosmos/p/5923439.html)
- [git stash](https://www.cnblogs.com/tocy/p/git-stash-reference.html)
- [github官方git教程](https://docs.github.com/cn/get-started/using-git/about-git)
- [--decorate参数与git版本的关系](https://stackoverflow.com/questions/51009808/whats-the-difference-between-git-log-and-git-log-decorate)
- 更多见浏览器收藏夹

