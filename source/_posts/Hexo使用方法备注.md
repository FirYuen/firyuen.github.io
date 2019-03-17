---
title: hexo使用方法备注
date: 2018-05-14 21:50:54
tags:
---
# 使用 Hexo + GitHub 可以轻松搞出一个好看的博客


1. 在 GitHub 上新建一个空 repo，repo 名称是「你的用户名.github.io」（注意个用户名是你的GitHub用户名，不是你的电脑用户名）
2. 'npm install -g hexo-cli'，安装 Hexo
3. 'hexo init myBlog'
4. 'cd myBlog'
5. 'npm i'
6. 'hexo new xxx'(博客新文章名)
7. start _config.yml，编辑网站配置
    1. 把第 6 行的 title 改成你想要的名字
    2. 把第 9 行的 author 改成你的大名
    3. 把最后一行的 type 改成 type: git
    4. 在最后一行后面新增一行，左边与 type 平齐，加上一行 repo: 仓库地址 （请将仓库地址改为「你的用户名.github.io」对应的仓库地址，仓库地址以 git@github.com: 开头你知道吧？不知道？不知道的话现在你知道了）,repo后要记得加空格
8. 'npm install hexo-deployer-git --save'，安装 git 部署插件
9. 'hexo deploy'
10. 进入「你的用户名.github.io」对应的 repo，打开 GitHub Pages 功能，如果已经打开了，就直接点击预览链接,你现在应该看到了你的博客！


# 第二篇博客


1. hexo new 第二篇博客
2. 复制显示的路径，使用 start 路径 来编辑它
3. 'hexo generate'
4. 'hexo deploy'
5. 去看你的博客，应该能看到第二篇博客了


#换主题

1. https://github.com/hexojs/hexo/wiki/Themes 上面有主题合集
2. 随便找一个主题，进入主题的 GitHub 首页，比如我找的是 https://github.com/iissnan/hexo-theme-next
3. 复制它的 SSH 地址或 HTTPS 地址，假设地址为 git@github.com:iissnan/hexo-theme-next.git
4. 'cd themes'
5. 'git clone git@github.com:iissnan/hexo-theme-next.git'
6. 'cd ..'
7. 将 _config.yml 的第 75 行改为 theme: hexo-theme-next，保存
8. 'hexo generate'
9. 'hexo deploy'
10. '等一分钟，然后刷新你的博客页面，你会看到一个新的外观。如果不喜欢这个主题，就回到第 1 步，重选一个主题。'
