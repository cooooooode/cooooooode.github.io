### 部署命令

`hexo clean && hexo deploy`

### 遇到问题的参考解决方案

删除git提交内容文件夹 `rm -rf .deploy_git/`

### 提交文章后没有发布到首页的问题

`hexo clean && hexo generate`

`hexo deploy`