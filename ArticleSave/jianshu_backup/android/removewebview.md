# 去除app内置内核，让页面加载飞起来

前段时间在酷安发布了一条动态教各位去除支付宝的内置uc内核，但是有人反映说会死灰复燃，经过琴梨梨多次分析，发现问题都是出现在重启后，系统重新把含有内核的so文件释放了出来，所以今天琴梨梨就来教各位以支付宝为例怎么彻底去除app内置浏览器内核

首先我们可以判定支付宝的uc内核在本地无需热加载，就是安装包lib文件夹里最大的那个文件(震惊！支付宝里体积最大的竟然是...浏览器内核)﻿

![](http://upload-images.jianshu.io/upload_images/5660880-e0800485db71607a.png)

是它，是它，就是它！

看文件名里含有7z，咱们以压缩格式打开试试﻿

![](http://upload-images.jianshu.io/upload_images/5660880-1f59b70b4417aa72.png)

使用rarlab打开

果真是7z，还固实了，解压后约28m

既然找到了目标，那么我们现在就要开始对症下药移除这个文件

安卓在安装app时会把lib文件夹内所有文件从安装包里释放出来加速启动，以支付宝的app文件夹为例﻿

![](http://upload-images.jianshu.io/upload_images/5660880-0c23c7b8d6bf1a6d.png)

图片发自简书App

lib文件夹存放的就是apk文件里释放的so文件，so文件是linux的一种可执行文件格式，玩linux的应该都懂，毕竟安卓基于linux嘛

oat文件夹是5.0＋引入的，存放odex文件，odex文件就是把含有源代码的dex文件提前编译出来，避免每次启动时从apk内提取，加快启动速度

base.apk就是安装包，原封不动的复制过来

上次在酷安的教程是仅仅干掉了lib文件夹内的内核so﻿

![](http://upload-images.jianshu.io/upload_images/5660880-09860df695bef008.png)

图片发自简书App

但是这个方法有局限性，就和黑域一样，打死不能重启，可是谁又能避免不重启呢？昨天在手机上解码4kx265还重启了好几次。所以现在琴梨梨要做的就是彻底移除这个so文件

除了lib文件夹，这个文件也就只有安装包里有了，我们先提取安装包到外部存储，因为data分区内更改是权限不足的

![](http://upload-images.jianshu.io/upload_images/5660880-750e8b2c0c97f2cf.png)

现在我们已经有了对安装包更改的权限，因为外置存储是公共读写目录。

打开安装包，找到这个lib，果断删掉它！﻿

![](http://upload-images.jianshu.io/upload_images/5660880-2cf8480719aecb83.png)

图片发自简书App

安装试试﻿

![](http://upload-images.jianshu.io/upload_images/5660880-45674c7cde3cda25.png)

图片发自简书App

可以看到，这样是不能正常安装的

有人问是不是核心破解就行了？答案是否 ﻿

![](http://upload-images.jianshu.io/upload_images/5660880-69e7144601f59d8d.png)

图片发自简书App

纵然已经核心破解，但是还是不行，这里就有必要详细科普一下什么是核心破解

安装包安装时有几个阶段，第一阶段会检查完整性，对照签名检查是否具备所有应该有的文件。第二阶段计算文件校验数值与签名比较以及检查版本号顺序。第三阶段才是释放文件和odex。

很明显核心破解只能攻克第二阶段，对于删文件导致卡在第一阶段，核心破解是然并卵的。

那么怎么办呢？很简单，既然文件列表在签名文件里，那我干掉删掉文件的记录不就行了吗？琴梨梨就要采用这种方法。

记录签名文件的文件夹是meta-inf，里面有三个文件

![](http://upload-images.jianshu.io/upload_images/5660880-d4f3e928061b8ddf.png)

图片发自简书App

rsa文件记录了开发者信息和校验算法，简单说就是开发者告诉系统我是谁和怎么确认是真的我。

mf文件存储apk内几乎所有文件校验数值，而sf文件会基于rsa把mf文件内校验数值加密，同时保存mf文件的校验数值

所以文件清单的来源就是mf和sf文件

打开mf文件找到被删so的记录﻿

![](http://upload-images.jianshu.io/upload_images/5660880-f68f3db1e1784b7d.png)

图片发自简书App

选中后退格键猛敲，记录就去除了

同理对付sf文件﻿

![](http://upload-images.jianshu.io/upload_images/5660880-f735583a71472248.png)

图片发自简书App

现在再安装就能正常安装了﻿

![](http://upload-images.jianshu.io/upload_images/5660880-0208c7738381b2c1.png)

图片发自简书App

可是你以为这就完成了嘛？不！﻿

![](http://upload-images.jianshu.io/upload_images/5660880-1778f3f71952c06b.png)

还是uc内核

内核文件已经被释放，源文件删除还能照样加载！

那么现在该做的就是把释放的文件删掉﻿

打开支付宝data目录

删除下图中含有uc字样，h5container字样的文件夹

![](http://upload-images.jianshu.io/upload_images/5660880-afcabbd74936eb46.png)

图片发自简书App

现在我们再打开支付宝﻿

可以看到uc内核已经消失了

![](http://upload-images.jianshu.io/upload_images/5660880-2a49cef247c106c2.png)

图片发自简书App

经过这样的深度处理，即使是重启，uc内核也不会死灰复燃。因为支付宝的uc内核只在本地存储。不过蚂蚁财富/咸鱼就不行了，它们的内核是联网热加载的。这种方法具备一定局限性，只支持在本地存放内核文件的app。

另外值得一提的是因为更新时系统会更新lib文件夹里的so文件，所以每次支付宝更新前你需要对更新安装包进行同样的手术。好在支付宝更新还不算频繁。