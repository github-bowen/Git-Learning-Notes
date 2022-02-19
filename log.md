## Linux命令

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

## Git Bash快捷键

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

- 注：笔记中使用```SSH```协议，github还支持```HTTP```协议。

- 准备工作步骤

  1. 进入用户主目录(c:Users/BH LU)：

     ```shell
     $ cd ~
     ```

  2. 创建SSH Key：

     ```shell
     $ ssh-keygen -t rsa -C "youremail@example.com"
     ```

     一路回车后在/.ssh中有```id_rsa```(私钥)和```id_rsa.pub```(公钥)。

  3. 在Github设置SSH Key：填上任意Title，在Key文本框里粘贴`id_rsa.pub`文件的内容。
  
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

- 将本地库push到远程库：

  ```shell
  $ git push origin master
  ```

- 查看远程库信息：

  ```shell
  $ git remote -v
  ```

- 删除远程库：（指解除本地库与远程库的绑定）

  ```shell
  $ git remote rm name
  # e.g:
  $ git remote rm origin
  ```

- 从远程库克隆

  ```shell
  $ git clone git@github.com:<Github name>/<repository name>.git
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

- 查看分支：

  ```shell
  $ git branch  # 输出带星号的为当前分支
  ```

- 与name分支合并：

  ```shell
  $ git merge <name>
  ```

- 删除分支：

  ```shell
  $ git branch -d <name>
  ```

- 



## 相关资料

- [廖雪峰Git教程](https://www.liaoxuefeng.com/wiki/896043488029600)
- [廖雪峰Git命令整理](https://liaoxuefeng.gitee.io/resource.liaoxuefeng.com/git/git-cheat-sheet.html#)
- [Linux常用命令整理](https://www.cnblogs.com/hi3254014978/p/12643601.html)
- 更多见收藏夹
