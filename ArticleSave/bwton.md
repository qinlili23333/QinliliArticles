# 实锤某毒瘤公司所开发的APP的流氓行为
# 

某公司说我恶意抹黑拿不出证据，还投诉掉我一个知乎回答,为了防止本文又被投诉掉,我在b站也同步发一份

# 

明天就考试，但我就不复习！就是要和毒瘤对抗到底！

# 

本文一切内容真实可复现！如果你复现不出来请告诉我你的设备环境，我会尽可能协助你复现结果

由于我是苏州人，我就取这家毒瘤公司为苏州地铁开发的app做例子吧

我们从苏e行-小米应用商店下载安装包，并截图小米商店网页的版本号和更新时间

![](//i0.hdslb.com/bfs/article/bc5cf29a93edca0bf6f0ddb1bfed23fe6ffaefab.png@1320w_2860h.webp)

  

得到58.42M安装包一个

![](//i0.hdslb.com/bfs/article/3893a995674f7c00b11a37073c088cb85db3e886.png@1320w_930h.webp)

记录文件校验，以确保这是一个完整的文件，

![](//i0.hdslb.com/bfs/article/4b754801ecd9a30b146de9b2cd95bd719d9d0b0d.png@1320w_1396h.webp)

为了确保没有任何其他APP干扰，我准备了一个全新的炼妖壶环境，可以看到炼妖壶里除了系统必须的谷歌套件外只有一个mt管理器，而且存储空间内啥也没有非常干净

![](//i0.hdslb.com/bfs/article/454687a0e2e7369cdc638a55226b9e1117cd38d2.png@1320w_2860h.webp)

![](//i0.hdslb.com/bfs/article/1769d52bda40266df049e89a7b95e0faf3f8e9cb.png@1320w_2860h.webp)

我们把安装包安装到炼妖壶

![](//i0.hdslb.com/bfs/article/c51cfe5d59ac74284952a421e00e5bebaf128c8b.png@1320w_2860h.webp)

  

# 

证明环节1：滥用权限

直接打开app，同意用户协议，但拒绝电话和文件权限请求（这个app用来刷地铁，显然这两个权限和该app必须功能没有任何关联）

![](//i0.hdslb.com/bfs/article/5c072cb894176013d1bb4f79ce89b5b8ad5e8cfc.png@1320w_2860h.webp)

ps：非常有意思的是，进入主界面后的位置权限拒绝了没什么后果

可明明位置权限倒是比电话权限有用114514倍啊

# 

证明环节2：滥用后台

我们同意权限（反正壶中界，非常安全），进入app，过掉开屏后直接按下桌面按钮

可以看到弹出了该app在后台运行的toast

![](//i0.hdslb.com/bfs/article/19ce175bf1ced430be9003cd36f0c0e8b3efc8c6.png@1320w_2860h.webp)

当然，可能有人要问了，我就弹个toast不能充分证明我在后台运行啊

所以在进入后台后，我打开终端

![](//i0.hdslb.com/bfs/article/7fbafbe0589ba36489167a0638f3ce19e6fb8279.png@1320w_356h.webp)

用top命令查看cpu占用，发现占用了2.3%（top只显示单核cpu占用，即占用一个核心的2.3%，和windows端任务管理器显示的全核占用有所区别请特别留意）

可能还有人会问，刚切入后台当然有占用，那么我们过几分钟去设置里看看

正常返回桌面5分钟左右之后我们打开该app设置页面的电池页面

![](//i0.hdslb.com/bfs/article/bcdd148692dc9f30853c0d448f69e3f3039c4657.png@1320w_2860h.webp)

足足运行了两分钟才被系统休眠（我系统设置全部禁止自启动禁止后台活动），显然是做了保活的

你一个刷地铁的app，有什么后台存活需求么？进出站刷一下不就够了？

# 

证明环节3：全包加固

![](//i0.hdslb.com/bfs/article/fbb1c508b91911f5774820347f3eb0febf97d36b.png@1320w_1700h.webp)

![](//i0.hdslb.com/bfs/article/19b0686fc7aa4c3090870d39cfdf34b2ff489180.png@1320w_384h.webp)

之前写那个回答的时候还是360加固，现在改用网易了

nesec.so，非常典型的网易加固，没法洗

# 

证明环节4：32位

![](//i0.hdslb.com/bfs/article/e6f539bce8d22669704f692c3772aa7e9146759e.png@1320w_2860h.webp)

armeabi，铁32位，还tm是没neon的v5时代，山顶洞人么？

我检查过所有so文件了，都有对应64位sdk可以接入，没屎坑问题，那就是单纯的坏了

当然你硬要举例哪里上64位有屎坑难度尽管告诉我，我能解决的屎坑实在不行你交给我解决

# 

证明环节5：X5 Webview

公共存储data目录，圈红均为实锤X5证据

![](//i0.hdslb.com/bfs/article/d2008589c2cf7138a2603fb21bd53955625f0097.png@1320w_1514h.webp)

还有这个service，洗不了

![](//i0.hdslb.com/bfs/article/c42f4f71b2ed55cf4f016733f71357d423c1ec3a.png@1320w_2860h.webp)

# 

证明环节6：存储脱粪+证明环节7：使用个推推送

原本干净的壶中界，多了好多东西呢！

![](//i0.hdslb.com/bfs/article/4d6162d8e2787ec19dd74cbeb7169408e245aa75.png@986w_2418h.webp)

.tbs，QQBrowser，tencent都是接入X5带来的

turingdebug似乎也是X5的锅

bwtCashierSDK和bwton是这个app自己脱粪的，理应放在私有data目录

libs是个推SDK，个推老毒瘤SDK了这个libs文件斩草不除根春风吹又生，知乎也有，所以我现在禁止知乎写入存储

![](//i0.hdslb.com/bfs/article/4fd80097d9c189eb93fc444280eabadb813f2acf.png@1294w_854h.webp)

加起来体积不大，但是污染公共存储确实是毒瘤行为

所有不需要共享的数据，请务必存储于data目录，为了存储整洁，也为了数据安全

# 

表扬时间

一个一年前发现但当前已被修补的问题是SDK版本过低，当时不同的app分别为22或26，目前已被提升到28，该表扬的我也绝对不会少表扬，但是目前最新的应该是30咯！

![](//i0.hdslb.com/bfs/article/10ae1fbb355e5e930609370a13d5a01ef5fb016b.png@1166w_446h.webp)

# 

总结

一年前写的回答到此已全部给出充分证据实锤

如果该公司仍然认为我是在恶意抹黑请拿出充分证据，如果该公司坚持我是同行，那也请拿出充分证据

# 

本文全部证据均使用合法的工具软件取得，没有通过任何反编译手段进行

# 

我的证据列完了，请反击或认输，我愿意奉陪到底

# 

我不是该行业从事人员，我只不过是个学制药的大二学生，我对科技和程序只不过是兴趣爱好罢了，但我仍然坚持为更美好的软件生态贡献自己的力量

  

# 

小彩蛋

经典打包事故，把网易加固的SDK jar文件也给打包进去了，还有那个aapt文件夹也不用打包

![](//i0.hdslb.com/bfs/article/5d1807bc634e52ee23cb807440329fd6950afd89.png@1320w_2860h.webp)
