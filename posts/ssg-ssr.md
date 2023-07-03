---
title: 'Git'
date: '2020-01-02'
---

# Git

## 1.什么是 Git?

- 版本控制软件

- 分布式版本控制软件

## 2. 命令

- git add：将本地文件增加到暂存区
- git commit：将暂存区的内容提交到本地仓库（本地分支，默认==master==分支）
- git push：将本地仓库的内容推送到远程仓库（远程分支）
- git pull：将远程仓库的内容拉取到本地仓库

## 3. 安装 Git

- 安装时：Use git from git bash only..,其他默认下一步
- 配置 path：E:\programs\Git\bin
- 配置 Git：右键 Git Bash

  - 配置用户名和邮箱

  - ```shell
    git config --global user.name "codehuan"
      git config --global user.email "codehuan@163.com"
    ```

  - 查看 C:\Users\ZhangHuan\.gitconfig

### 3.1 搭建 Git 仓库（远程仓库）：

0. 统一的托管网站（https://github.com）
1. 为了在本地和远程仓库之间进行免密钥登录，可以配置 ssh
2. 配置 ssh：先生成本地的 ssh

```shell
#一直回车
ssh-keygen -t rsa -C codehuan@163.com -f  ~/.ssh/gitee_id_rsa
```

```shell

5. 将本地生成的id_sra_pub内容复制到远程的key中

   1. 首先登录Github账号

   2. 点击头像的Settings

   3. 然后点击SSH

   4. 点击New SSH title任意，在key中将生成的ssh复制到文本框中

   5. 测试连通性

```

```shell
 ssh -T git@github.com
```

```tex
  - 如果本地和远程成功通信，则可以在/.ssh目录中发现know_hosts文件
```

- 如果失败：多尝试几次、检查回车符
  ```shell
  #本地项目-远程项目关联
  git remote add origin git@gitee.com:zhanghuan08/Notes.git
  ```

## 4. 发布项目

#### 4.1 第一次发布项目

```shell
# 添加需要push的文件
git add  文件名称
git add .  添加所有文件
# 将需要push 的文件添加到本地仓库
git commit -m "注释内容"
# 将本地仓库更新到远程仓库
git push -u origin master
```

#### 4.2 第一次下载项目

```shell
 git clone git@github.com:zh1730272469/Notes.git
```

#### 4.3 提交（本地-远程）

```java
git add .
git commit -m "注释内容"
git push -u origin master （第一次提交需要 -u之后就不再需要）
```

#### 4.4 更新（远程-本地）

```shell
git pull
```

## 5. 多人开发（分支）

### 5.1 克隆项目到本地

```shell
git clone [仓库路径]
```

### 5.2 创建分支

```shell
git branch [分支名称]
```

### 5.3 查看本地分支

```shell
git branch -a
```

### 5.4 切换分支

```shell
git checkout [分支名称]
```

### 5.5 将新分支推送到 GitHub/Gitee

```shell
git push origin [branch name]
```

### 5.6 更新远程分支列表

```shell
git remote update origin --prune
```

### 5.7 删除分支

```shell
# 删除
git branch -d [分支名称]
# 删除远程分支
git push origin --deleye [分支名称]
```

## 6. 配置 Gitee 和 GitHub

### 1. 清除已有的 git 设置

```bash
git config --global --unset user.name "YourName"
git config --global --unset user.email "YourEmail"
```

### 2. 设置本地用户名和邮箱

```bash
git config --global user.name "ZhangHuan"
git config --global user.email "codehuan@163.com"
```

### 3. 生成新的 SSH Keys

#### 3.1 Github 密钥

```bash
ssh-keygen -t rsa -C "codehuan@163.com" -f  ~/.ssh/github_id_rsa

ssh-keygen -t ED25519 -C "codehuan@163.com" -f  ~/.ssh/github_id_ED25519
```

复制公钥`github_id_rsa.pub`公钥的内容，并添加到 github 的 SSH Keys 中保存．

#### 3.2 Gitee 密钥

```bash
ssh-keygen -t rsa -C "codehuan@163.com" -f  ~/.ssh/gitee_id_rsa

ssh-keygen -t ED25519 -C "codehuan@163.com" -f  ~/.ssh/gitee_id_ED25519

```

复制公钥`gitee_id_rsa.pub`公钥的内容，并添加到 gitee 的 SSH Keys 中保存．

#### 3.3 Gitlab 密钥

```bash
ssh-keygen -t ed25519 -C "codehuan@163.com" -f  ~/.ssh/gitlab_id_ed25519
```

复制公钥`gitee_id_rsa.pub`公钥的内容，并添加到 gitee 的 SSH Keys 中保存．

### 4. 创建 config 文件防止冲突

在`~/.ssh`文件夹下新建`config`文件，添加以下内容

```bash
# gitee
Host gitee.com
    HostName gitee.com
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/gitee_id_rsa

# github
Host github.com
    HostName github.com
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/github_id_rsa

# gitlab
Host 106.52.176.43
	HostName 106.52.176.43
	PreferredAuthentications publickey
	IdentityFile ~/.ssh/gitlab_id_ed25519
```

### 5. 测试

```bash
#执行
ssh -T git@github.com
#如果返回successfully则github配置成功．

#执行
ssh -T git@gitee.com
#如果返回successfully则gitee配置成功．
```
