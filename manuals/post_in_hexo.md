## 在Hexo博客系统中Post文章

在source/_posts/blog中增加DIR和文章。

修改soruce/_posts/menu.md，为文章添加目录。

```shell
git add #增加的文章
hexo s -g # 本地生成web页面以便预览
hexo d -g # 本地生成web页面并不熟到username.github.io的master分支
```

参考：https://zhuanlan.zhihu.com/p/63434340