## Linux命令

### 基础命令

- **cd**：change direcroty 切换目录

  **e.g.**：(注意不是反斜杠)
  
  ```shell
  $ cd e:ImportantFile/LearningFiles/2_2/OOP/PreviewFiles/GitLearningNotes
  
- **ls**：list files 列出非隐藏文件

  **dir**：directory 列出非隐藏文件

  （两者略有不同，ls的```GitLearningNotes```为蓝色）

  ```shell
  $ dir
  GitLeaningNotes  OO工具链教程.pdf  推送.jpg
  ```

  ```shell
  $ ls
  GitLeaningNotes/  OO工具链教程.pdf  推送.jpg```

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

### VI相关命令

- **vi**：在VI中打开已存在文件或创建新文件
  
- **i**：进入插入模式

- **Esc**：退出插入模式

- **u**：撤销上次更改

- **shift + zz**：保存文件并退出

## Git Bash快捷键

- 复制：ctrl + insert
- 粘贴：shift + insert

## Git 使用

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

- 查看仓库状态（是否有文件被修改未add，add后未commit）：

  ```shell
  $ git status
  ```

- 查看**工作区**与**暂存区**的区别：

  ```shell
  $ git diff
  ```

  查看

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
    >```shell
    $ git reset --hard 1094a
    > ```
  
  - 撤销工作区修改——从工作区回退到最近一次commit（版本库）或add（暂存区）的状态:
    >即直接丢弃工作区：（checkout还有其他用法：见下面*从版本库删除某个文件*）
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







## 相关资料

- [廖雪峰Git教程](https://www.liaoxuefeng.com/wiki/896043488029600)
- [廖雪峰Git命令整理](https://liaoxuefeng.gitee.io/resource.liaoxuefeng.com/git/git-cheat-sheet.html#)
- [Linux常用命令整理](https://www.cnblogs.com/hi3254014978/p/12643601.html)
- 更多见收藏夹
