## Linux/Shell命令

### 基础命令

- **cd**：change direcroty 切换目录

  **e.g.**：
  
  ```shell
  $ cd e:ImportantFile/LearningFiles/2_2/OOP/PreviewFiles/GitLearningNotes # 注意不是反斜杠
  
- **ls**：list files 列出非隐藏文件

  **dir**：directory 列出非隐藏文件

  （两者略有不同，ls的```GitLearningNotes```为蓝色）

  ```shell
  $ dir
  GitLeaningNotes  OO工具链教程.pdf  推送.jpg
  ```

  ```shell
  $ ls
  GitLeaningNotes/  OO工具链教程.pdf  推送.jpg
  ```

- **ls -a**：list files -all 列出所有文件

- **ls -l**：显示文件时间记录

- **touch**：更改文件时间属性，若不存在则创建一个新文件

- **mkdir**：make directory 创建目录

  **e.g.**：

  ```shell
  $ mkdir GitLearningNotes

- **pwd**：print working directory 显示当前路径

- **clear**：清除bash屏幕（实质相当于翻页）

- **reset**：清除历史输入

- **cat**：concatenate 显示内容

- **rm**：remove file 删除文件

- **reboot**：重启

- **echo**：打印字符串

### 具体指令(Ubuntu)

#### 软件相关

- 显示apt/snap已安装软件：

  ```shell
  $ sudo apt list --installed
  $ sudo snap list
  # 注：apt为advanced packaging tool
  #    sudo为super user do
  ```

  显示apt可升级软件、apt/snap更新：

  ```shell
  $ sudo apt list --upgradeable
  $ sudo apt upgrade xxx
  $ sudo snap refresh <xxx>  # 若不加文件名则更新全部
  ```
  
- 卸载软件：

  ```shell
  $ sudo apt remove xxx
  ```

  删除软件（包括所有文件）:

  ```shell
  $ sudo apt purge xxx
  ```

- apt/snap安装软件包：

  ```shell
  $ sudo apt install xxx
  $ sudo snap install xxx
  ```

#### 系统资源

- 查看磁盘空间：

  ```shell
  $ df -hl
  ```

- 查看内存空间：

  ```shell
  $ free [-b  -k  -m]  # B / KB / MB
  ```


### VI相关命令

- **vi**：在VI中打开已存在文件或创建新文件
  
- **i**：进入插入模式

- **Esc**：退出插入模式

- **u**：撤销上次更改

- **shift + zz**：保存文件并退出

## Git Bash/Ubuntu Terminal快捷键

- 复制：```ctrl + insert``` / ```shift + ctrl + c```
- 粘贴：```shift + insert``` / ```shift + ctrl + v```

## Git 命令

### Git初始化与帮助

- 查看git相关命令说明

  ```shell
  $ git
  ```

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

### 创建repository

- 将当前目录初始化为仓库：

  ```shell
  $ git init
  ```

- 添加文件：

  ```shell
  $ git add xxx.xx

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

- 查看所有commit历史：

  ```shell
  $ git log
  ```

  简洁版：
  
  ```shell
  $ git log --pretty=oneline
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

     一路回车后在/.ssh中有```id_rsa```(私钥)和```id_rsa.pub```(公钥)。

  3. 在Github设置SSH Key：填上任意Title，在Key文本框里粘贴`id_rsa.pub`文件的内容。
  

#### 本地库→远程仓库

- **首次**将本地库push到远程库上：（在github中新建了```GitLearningNotes```这一repository）
  
  在本地对应仓库运行命令：
  
  ```shell
  $ git remote add origin git@github.com:<github name>/<repository name>.git
  ```
  
  e.g.:
  
  ```shell
  $ git remote add origin git@github.com:NormalLLer/GitLearningNotes.git
  ```
  
  然后：（回车后会提示输入密钥-同qq密码）
  
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

#### 远程仓库→本地库

- 从远程库克隆（**首次**）：

  ```shell
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

- 创建并切换分支

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

## 相关资料

- [廖雪峰Git教程](https://www.liaoxuefeng.com/wiki/896043488029600)
- [廖雪峰Git命令整理](https://liaoxuefeng.gitee.io/resource.liaoxuefeng.com/git/git-cheat-sheet.html#)
- [Linux常用命令整理](https://www.cnblogs.com/hi3254014978/p/12643601.html)
- [git log参数](https://www.cnblogs.com/bellkosmos/p/5923439.html)
- [git stash](https://www.cnblogs.com/tocy/p/git-stash-reference.html)
- [github官方git教程](https://docs.github.com/cn/get-started/using-git/about-git)
- 更多见浏览器收藏夹

# test rebase

