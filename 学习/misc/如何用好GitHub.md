# 如何用好GitHub

## Introduction

GitHub 是一个面向开源及私有软件项目的托管平台，因为只支持 Git 作为唯一的版本库格式进行托管，故名 GitHub。

为一个项目贡献代码非常简单：首先点击项目站点的Fork的按钮，然后将代码检出并将修改加入到刚才分出的代码库中，最后通过内建的pull request机制向项目负责人申请代码合并。

在 GitHub 里面有众多的业界大神、有丰富的学习资料、有著名的开源项目代码，我们也可以在 GitHub 中增长自己的技术能力、渲染自己的简历，甚至搭建自己的个人博客或者网站。

## GitHub 术语解释

**Repository**：简称Repo，可以理解为“仓库”，我们的项目就存放在仓库之中。也就是说，如果我们想要建立项目，就得先建立仓库；有多个项目，就建立多个仓库。

**Issues**：可以理解为“问题”，举一个简单的例子，如果我们开源一个项目，如果别人看了我们的项目，并且发现了bug，或者感觉那个地方有待改进，他就可以给我们提出Issue，等我们把Issues解决之后，就可以把这些Issues关闭；反之，我们也可以给他人提出Issue。

**Star**：可以理解为“点赞”，当我们感觉某一个项目做的比较好之后，就可以为这个项目点赞，而且我们点赞过的项目，都会保存到我们的Star之中，方便我们随时查看。在 GitHub 之中，如果一个项目的点星数能够超百，那么说明这个项目已经很不错了。

**Fork**：可以理解为“拉分支”，如果我们对某一个项目比较感兴趣，并且想在此基础之上开发新的功能，这时我们就可以Fork这个项目，这表示复制一个完成相同的项目到我们的 GitHub 账号之中，而且独立于原项目。之后，我们就可以在自己复制的项目中进行开发了。

**Pull Request**：可以理解为“提交请求”，此功能是建立在Fork之上的，如果我们Fork了一个项目，对其进行了修改，而且感觉修改的还不错，我们就可以对原项目的拥有者提出一个Pull请求，等其对我们的请求审核，并且通过审核之后，就可以把我们修改过的内容合并到原项目之中，这时我们就成了该项目的贡献者。

**Merge：**可以理解为“合并”，如果别人Fork了我们的项目，对其进行了修改，并且提出了Pull请求，这时我们就可以对这个Pull请求进行审核。如果这个Pull请求的内容满足我们的要求，并且跟我们原有的项目没有冲突的话，就可以将其合并到我们的项目之中。当然，是否进行合并，由我们决定。

**Watch：**可以理解为“观察”，如果我们Watch了一个项目，之后，如果这个项目有了任何更新，我们都会在第一时候收到该项目的更新通知。

一般情况下，我们在push操作之前都会先进行pull操作，这样不容易造成冲突。

对于向远处仓库（GitHub）提交代码，我们可以细分为两种情况：

第一种：本地没有 Git 仓库，这时我们就可以直接将远程仓库clone到本地。通过clone命令创建的本地仓库，其本身就是一个 Git 仓库了，不用我们再进行init初始化操作啦，而且自动关联远程仓库。我们只需要在这个仓库进行修改或者添加等操作，然后commit即可。

第二种：本地有 Git 仓库，并且我们已经进行了多次commit操作。

作者：程序员吴师兄
链接：https://www.zhihu.com/question/30119197/answer/1877067450
来源：知乎
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。



首先，建立一个本地仓库，命名为springmvc-tutorial：

![img](https://picx.zhimg.com/80/v2-db781e9d147fbad141a3e25124e7572a_720w.webp?source=1940ef5c)

如上图所示，进入该仓库，进入init初始化操作：

![img](https://picx.zhimg.com/80/v2-93a1b4932f996da643621d66407c6514_720w.webp?source=1940ef5c)

然后，输入

```text
git remote add origin https://github.com/guobinhit/springmvc-tutorial.git
```

命令，关联远程仓库（在此，默认大家都知道如何获取远程仓库的地址），其中origin为远程仓库的名字：

![img](https://pic1.zhimg.com/80/v2-ea435870e321c2befd427ea6bc9b1a9b_720w.webp?source=1940ef5c)

输入git pull origin master命令，同步远程仓库和本地仓库：

![img](https://pica.zhimg.com/80/v2-5a0caecda20f89df85f250580686fb57_720w.webp?source=1940ef5c)

再回到本地springmvc-tutorial仓库，看看我们是否已经把远程仓库的内容同步到了本地：

![img](https://pica.zhimg.com/80/v2-bc4c9c8c62be0d85355f39e4727391ec_720w.webp?source=1940ef5c)

如上图所示，显然我们已经把远程springmvc-tutorial仓库里面仅有的README.md文件同步到了本地仓库。接下来，在本地仓库新建一个名为test.txt的测试文件：

![img](https://picx.zhimg.com/80/v2-b4ae6a7adbd1eae904003b4f7c0d5b36_720w.webp?source=1940ef5c)

输入git add和git commit命令，将文件test.txt添加并提交到springmvc-tutorial仓库：

![img](data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' width='573' height='160'></svg>)

再输入git push origin master命令，将本地仓库修改（或者添加）的内容提交到远程仓库：

![img](https://picx.zhimg.com/80/v2-6acb455e9035ac8d73ea8e9f9d1783bf_720w.webp?source=1940ef5c)

如上图所示，我们已经将本地仓库的内容同步到了远程仓库。下面，我们进入远程springmvc-tutorial仓库的页面，看看我们的提交结果：

![img](https://picx.zhimg.com/80/v2-4c192aa5e2a5f118f0c5191f46d43c0c_720w.webp?source=1940ef5c)

一般来说，我们习惯性将远程仓库命名为origin。

## 参考文章

|              标题              |                           来源                            |
| :----------------------------: | :-------------------------------------------------------: |
| 如何开始在 github 上学习东西？ | https://www.zhihu.com/question/30119197/answer/1877067450 |
|                                |                                                           |
|                                |                                                           |
|                                |                                                           |

