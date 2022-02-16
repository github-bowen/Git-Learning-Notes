## Linux命令

- **cd**：change direcroty 切换目录

  **e.g.**：(注意不是反斜杠)
  
  ```shell
  $ cd e:ImportantFile/LearningFiles/2_2/OOP/PreviewFiles/GitLeaningNotes
  
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

## Git Bash快捷键

- 复制：ctrl + insert
- 粘贴：shift + insert

## Git 使用

查看git相关命令说明

```shell
$ git
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

- 查看最新一次未commit修改与最新一次已commit修改的区别：

  ```shell
  $ git diff
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

- 回退版本：

  - HEAD：当前版本

  - HEAD^：上一个版本

  - HEAD^^：上上个版本

  - HEAD~100：上100个版本

  回退上一个版本：

  ```shell
  $ git reset --hard HEAD^
  ```

  根据版本号回退到制定版本（包括"未来"的版本，下面1094a为版本号前5位）：
  
  ```shell
  $ git reset --hard 1094a
  ```

- 
