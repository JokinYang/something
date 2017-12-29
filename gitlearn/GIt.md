# Git基础
Git中所有数据在存储之前会计算校验和(sha-1)

## 三种状态
> 已提交(committed)、已修改(modified)、已暂存(staged)

### Git仓库目录
是Git用于保存项目的元数据和对象数据库的地方

### 工作目录
是对项目中的某个版本独立提取出来的内容

### 暂存区域
是一个文件，保存了下次将提交的文件列表信息

### 跳过暂存
git commit -a -m "...."
跳过git add，直接提交所有已跟踪的文件

### 三方合并

# 文件周期

# 日常操作
- 初始化 git init
- 跟踪文件 git add （可以理解为 添加内容到下一次提交中）
- 提交：git commit
- 克隆：git clone [url]
- 文件状态：git status
- 查看修改：git diff [file 指定查看某个文件]
- 提交历史：git log [-p 显示每次提交的内容差异]
- 分支：git branch [-d 删除 -D 强制删除]
- 切换：git checkout [-b(新建并切换) feature]
- 合并：git merge [feature]
- 更新：git fetch origin 从origin抓取本地没有的数据，更新本地数据库，移动指针
- 同步：git pull [origin master]
- 推送：git push [origin master --force(覆盖远程仓库)]
- 删除远程分支：git push origin --delete [feature]从服务器上删除feature分支

# 骚操作
- 变基：git rebase master [feature]

> 工作目录下的文件只有两种状态：已跟踪、未跟踪
> 在“Changes to be committed”下，说明是已暂存状态
> 分支切换会改变工作目录里的文件
> 冲突：同一文件的同一部分有不同的修改