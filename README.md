# hancher's blog

[个人博客](https://www.hancher.top/), 欢迎光临!
![blogHome](/images/blog_home.png)


## 常用操作
### 本地启动
首次: 初始化+运行
```bash
安装ruby: ruby -v
安装bundler : bundle -v
安装jekyll : gem install jekyll
根据Gemfile初始化配置: bundle install
  - 如果比较慢,可以换成国内源,参考配置文件
固化gem配置(可选): git add Gemfile Gemfile.lock
运行: bundle exec jekyll serve
```
非首次: 直接运行
```bash
bundle exec jekyll serve
```

## 包结构
- _post : 文章
    - 年月日+标题

## jekyll 常用命令
```bash
bundle exec jekyll build : 打包,默认打包到_site路径
bundle exec jekyll serve : 本地启动
bundle exec jekyll clean : 清理
bundle exec jekyll help build: 帮助
```

## 扩展
jekyll 支持通过插件的方式扩展. 一切扩展依托于_config.yml 实现.

## 目前支持的功能
- 不辣子统计
- 网站访问分析
  - 谷歌分析
  - 百度统计
- 文章搜索能力
- 评论功能

## 参考
1. [参考主题](https://github.com/mzlogin/mzlogin.github.io)  
2. [Jekyll与github建站](https://docs.github.com/cn/pages/setting-up-a-github-pages-site-with-jekyll/about-github-pages-and-jekyll)
3. [如何本地预览](https://docs.github.com/cn/pages/setting-up-a-github-pages-site-with-jekyll/testing-your-github-pages-site-locally-with-jekyll)
4. [bundler](https://bundler.io/)
5. [jekyll](https://jekyllrb.com/)
6. [beaudar评论模块](https://beaudar.lipk.org/)