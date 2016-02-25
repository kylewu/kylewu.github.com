---
layout: post
title: Mac 下 packer build 卡死
date: 2015-09-01 13:52:08.000000000 +02:00
published: true
categories:
- 编程技术
tags:
- docker
- packer
---
> Packer is a tool for creating machine and container images for multiple platforms from a single source configuration.

通过一个配置文件，Packer可以生成Amazon EC2，Docker，DigitalOcean的image，非常实用。工作中很多项目都是用Packer生成ec2 ami，确实很方便。但是最近在生成Docker时出现一个问题。

<script src="https://gist.github.com/kylewu/c9f93df5f3cc1d55b51e.js"></script>

这里的上传操作是在packer.json的inline脚本中配置的。这条命令就卡死在这里，不能继续了。

如果你也有同样的问题，说明你也是在使用Mac OSX。原因非常简单，mac下的docker是运行在虚拟机里的。也就是说如果要上传文件，需要从mac，传到虚拟机，再到docker。

上面的命令行输出中可以看到我们要上传的文件在`/var/folders/`目录下，但是这个目录并没有在虚拟机的设置中同步。默认情况下，只有 `/Users`目录设置了同步，所以解决方案就是设置一个`TMPDIR`变量，并且指向`/Users`目录下的一个文件夹。

`$ TMPDIR=~/tmp packer build packer.json`
