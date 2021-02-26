### 常用命令：
    git --version   查看版本

#### 用户配置
    git config --global user.name "user name" 设置个人用户名称
    git config --global user.email "email" 设置个人邮箱
    git config --list  查看已有的配置信息
    git config --global core.autocrlf false 关闭自动转换。

#### 底层命令
    ·基础的linux命令
    cd：进入目录
    clear:清除屏幕
    echo 'test content':往控制台输出信息
    echo 'test content' > test.txt:将信息输出到test.txt文件中，如没有该文件则会创建该文件。
    ll:将当前目录下的子文件和子孙目录平铺在控制台
    ls:将当前目录下的子文件平铺在控制台
    find 目录名:将对应目录下的子孙文件和子孙目录平铺在控制台
    find 目录名 -type f:将对应目录下的文件平铺在控制台
    rm 文件名:删除文件
    mv 源文件 重命名文件:重命名
    cat 文件的url :查看对应文件的内容
    vim 文件的url:
        按i进入插入模式 进行文件的编辑。
        按esc键然后按:键 进行命令的执行
        q! 强制退出（不保存）
        wq 保存退出
        set nu 设置行号

    ·初始化仓库
        git init 要对现有的某个项目开始用git管理，只需到次项目所在的目录，执行：git init
        初始化后，在当前目录下会出现一个名为.git的目录，所有git需要的数据和资源都存放在这个目录中。
    
        ··git内容下目录：
            hooks：目录包含客户端或服务端的钩子脚本。
            info：包含一个全局性排除文件。
            logs：保存日志信息。
            objects：目录存储所有数据内容。
            refs：目录存储指向数据（分支）的提交对象的指针
            config：文件包含项目特有的配置选项
            description：用来显示对仓库的描述
            HEAD：文件指示目前被检出的分支
            index：文件保存暂存区信息




### 高层命令
    git init：初始化新仓库。
    git add ./:将修改添加到暂存区。工作目录先到版本库，再从版本库到暂存区。
        git add 文件名：跟踪一个新文件，使其处于暂存状态。
                只要在“Changes to be committed”这行下面的，就说明是已暂存状态。
    git commit -m "注释内容"：将更新内容从暂存区提交到版本库。
    git commint -a -m "注释内容":将更新内容跳过暂存区直接提交到版本库。
    git status：查看文件当前状态
    git diff：查看哪些修改还没有暂存
    git diff-cached 或者 git diff-staged：有哪些更新已经暂存但还未提交
    git log：查看提交历史记录
        git log --pretty=oneline
        git log --oneline：以每次提交显示为一行的格式查看提交的历史记录。
    git reflog：查看完整操作
    git rm 文件名：从工作目录删除该文件并将其提交到暂存区。
    git mv 源文件名 新文件名：将工作目录中的文件进行重命名并将其提交到暂存区。


### 分支操作
    ·创建分支
    git branch：显示分支列表
    git branch 分支名：创建一个新的分支
    
    ·切换分支
        ··注意：分支切换会改变工作目录中的文件。如果切换到一个较旧的分支，工作目录会恢复到该分支最后一次提交时的样子。如果不能恢复，将禁止切换分支。
               所以在切换分支前，应该提交一下当前分支。
    git checkout 分支名：切换分支
    git checkout -b 分支名：创建一个新分支并指向该分支
    git branch -d name：删除分支
    git branch -D name：强制删除分支
    git branch -v：查看每一个分支的最后一次提交
    git branch name commitHash：创建一个名为name的分支并指向commitHash对象（回滚）
    git log --oneline --decorate --graph --all

### git存储
    ·git stash：将未完成的修改保存到一个栈上，保存到该栈后工作目录里原有修改消失。
    git stash list：查看存储
    git stash apply stash@｛2｝：应用2号栈存取，不指定的话默认未最近储藏
    git stash pop：应用储藏后立即从栈上扔掉它
    git stash drop stash@｛2｝：移除指定的储藏
    git stash

### 撤销和重置
    撤回工作区和暂存区：
        ·通过git status查看当前修改的状态，然后可以根据提示进行撤销工作区修改或者暂存区修改
    撤回版本库提交（提交注释出错）：
        ·git commit --amend：修改上次提交的注释

    重置：
        git log --pretty=oneline:查看提交日志及其完整哈希值
        git reset --hard 哈希值：将分支硬重置到该哈希值对应的提交

    恢复：
        git reflog:显示分支完整操作日志
        git branch recover-branch 哈希值

### 打tag
    ·轻量标签
    git tag v1.0：将当前提交对象设置v1.0的标签。
    git show tagname:查看特定标签
    git push origin [tagname]:将标签推送到远程仓库
    git push origin --tags:将所有不在远程仓库服务器的标签推送到服务器仓库
    git tag -d tagname:删除标签
    git checkout tagname:指针会跳转到该标签所在提交，但是没有分支
    
    ·附注标签
    git tag l 'v1.8.5*':将v1.8.5及之后标签都列出

### 远程协作
    ·推送现有仓库到远程仓库：
        git remote add origin url:将url所在远程仓库关联
        git push -u origin master:将master分支内容推送到origin仓库

    ·创建一个新仓库
        echo '注释' >> READE.md
        git init
        git add READE.md
        git commint -m "first commit"
        git remote add origin url
        git push -u origin master

    `其他命令：
        git remote -v:显示远程git别名与其对应的url
        git push origin branchname:将分支推送到远程origin仓库
        git clone url

    
    

        