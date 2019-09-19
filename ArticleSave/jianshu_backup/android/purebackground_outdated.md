# 让更多APP开启后台纯净

自从绿色守护加入后台纯净功能，相信各位也都已经体会到了后台纯净的加速效果，尤其对于加固后的APP能够更快的启动

但是实际上支持后台纯净的毕竟只是少数APP，所以我们可以考虑为其他APP做手术开启后台纯净

本期教程需要以下工具:MT管理器，my android tools

那么现在就让我们开始吧

STEP1 找到需要处理APP的安装包

本次我们以游戏pancake为例﻿，本身不支持后台纯净﻿

![](http://upload-images.jianshu.io/upload_images/5660880-b91e1e6cf64d8d01.png)

![](http://upload-images.jianshu.io/upload_images/5660880-a16540bb0a5a45cf.png)

一定要复制！

然后把它复制到外部存储，因为在data分区内是不能直接修改的

STEP2 打开安装包，找到androidmanifest.xml﻿

![](http://upload-images.jianshu.io/upload_images/5660880-07a15a1618013f62.png)

是它是它就是它

STEP3 打开，选择反编译﻿

![](http://upload-images.jianshu.io/upload_images/5660880-092bac16ea801031.png)

需要mt会员

STEP4 修改targetsdkversion到24或更高，这里琴梨梨设置为25，minsdkversion可以往高改，个人习惯改23

![](http://upload-images.jianshu.io/upload_images/5660880-325b89586c62d50a.png)

修改前

![](http://upload-images.jianshu.io/upload_images/5660880-74a6593cd764c39b.png)

修改后

STEP5 保存安装﻿

![](http://upload-images.jianshu.io/upload_images/5660880-f0b105ca0ce6613e.png)

需要核心破解

如果提示安装包损坏那么你需要进行核心破解，核心破解是什么下一期琴梨梨会讲解

STEP6 关闭后台服务，使用mat﻿

![](http://upload-images.jianshu.io/upload_images/5660880-888589831cbef5e6.png)

把后台常驻的服务关了

现在回到绿守看看，是不是成功激活后台纯净了？﻿

![](http://upload-images.jianshu.io/upload_images/5660880-c67e5d54f5070963.png)

大部分APP都可以这么操作，所以琴梨梨甚至让一部分老APP都后台纯净了

![](http://upload-images.jianshu.io/upload_images/5660880-70755bd432273624.png)

原targetsdkversion只有9，修改后也可以后台纯净

如果修改后闪退则APP不支持修改，恢复原版即可