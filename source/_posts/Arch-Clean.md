---
title: 如何高效优雅地为Arch Linux瘦身?
categories: Linux
---



​		虽然Linux本身的体积比Windows 10小很多，但是使用Manjaro的这段时间里，感觉产生的日常垃圾也不少。由于喜欢大空间带来的自由的感觉，必然就要进行瘦身啦！

<!-- more -->

- #### 清理安装包缓存

  删除未安装 & 已安装 & 旧版本的包文件缓存


```shell
sudo pacman -Scc
```

- #### 清除孤立软件包(无用依赖)

```shell
sudo pacman -Rns $(pacman -Qtdq)
```

- #### 清理日志文件(限制日志文件大小)

```shell
sudo journalctl --vacuum-size=30M
```

