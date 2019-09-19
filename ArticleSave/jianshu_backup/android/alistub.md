# 一次对签名验证＋阿里加固的逆向实录

前几天bzy找到琴梨梨，问我可否攻克其签名验证﻿

![](http://upload-images.jianshu.io/upload_images/5660880-5475110809cd6ebf.png)

图片发自简书App

我想了想就答应了试试，毕竟任何的加密和保护措施都只不过是加了一把好锁罢了，而好锁也是能开的只不过可能难度大一点而已。

下载安装包，先发挥琴梨梨的特长:拆包。﻿

![](http://upload-images.jianshu.io/upload_images/5660880-efff4c5f3a09e846.png)

assets文件夹

一看assets，确定是阿里加固，琴梨梨就知道难度不小，阿里加固是目前最难攻克的加固，采用类抽取的策略，传统脱壳的dumpdex方法对其毫无任何作用。﻿

![](http://upload-images.jianshu.io/upload_images/5660880-db977964b525168c.png)

drizzleDumper跑了半天什么也没有

对于目前最新的阿里壳，由于没有合适的解密算法，暂时还不能脱壳，所以琴梨梨就考虑从破解签名入手。

前段时间mt管理器更新了移除签名验证功能，于是琴梨梨果断试了一下，然后...emmmm......﻿

![](http://upload-images.jianshu.io/upload_images/5660880-bd4b012ed96b4b51.png)

一键移除失败

看样子dex做过特殊处理，我们不更改直接保存一次试试﻿，然后...

![](http://upload-images.jianshu.io/upload_images/5660880-d551ba2082a57e01.png)

保存出错

好在总算找到了问题根源，是z/z/z/z0，是个加固后多出来的class，于是琴梨梨打算去打开这个class看看，然后...﻿

![](http://upload-images.jianshu.io/upload_images/5660880-fa112ddb69e93368.png)

并不能打开

这个class看样子被处理过不能正常被反编译，那么我们先考虑修复一下。﻿

修复成功之后总算看到了这个class，看样子是壳的调用。

![](http://upload-images.jianshu.io/upload_images/5660880-6e7fd1cf0d757750.png)

修复后反编译

正当琴梨梨高高兴兴的塞回dex安装时，IT CRASHED!!!﻿

![](http://upload-images.jianshu.io/upload_images/5660880-f49b37ab8a453022.png)

崩溃了...

看来阿里加固有对付反编译和修复dex的部分，我们要绕道走。

前几天拆的小猿搜题给了我启发﻿

![](http://upload-images.jianshu.io/upload_images/5660880-b6b1d1a44b46944d.png)

小猿搜题的multidex

小猿搜题是梆梆加固企业版，梆梆加固为了效率，只加固第一个dex，所以很明显第一个dex只有16k是个壳dex，而后面的dex并没有加固，可以任意改动。

安卓的art虚拟机是完美支持multidex的，不需要使用multidex库，在dex2oat过程就会自动把所有dex优化为单个oat文件。而mt管理器的移除签名验证原理是重定向启动位置到hook签名的操作然后再正常启动，所以既然我们没法改现在的dex，如果用multidex的办法，用第二个dex做hook，这样就可以不动原dex了。

经过修复的dex可以正常移除签名验证。﻿

![](http://upload-images.jianshu.io/upload_images/5660880-c9bd492af82deb47.png)

成功移除签名验证

我们打开处理过的dex，删掉hook之外的所有classes并保存。

﻿还别说这样真挺像壳dex的。

![](http://upload-images.jianshu.io/upload_images/5660880-44250f6ff6051235.png)

清空其他classes

原dex改名classes2.dex丢进来。﻿

![](http://upload-images.jianshu.io/upload_images/5660880-7866360be99feb21.png)

丢入dex2

签个名，安装打开一切正常！！

![](http://upload-images.jianshu.io/upload_images/5660880-1c5c44404123e6a3.png)

图片发自简书App

最后，还是那句老话，这世上没有绝对的安全。

那就让我们一起期待bzy日空调吧(滑稽)﻿

![](http://upload-images.jianshu.io/upload_images/5660880-12c5fde01f223741.png)