# [⇦][] 无需root无需7.0＋，扫一扫快捷方式自己做主  
你是不是早就很想实现下图的效果，点击扫一扫就能进入，再也不用先点开主页  
![](53.png)  
但是目前只有两条路可以走，第一条是7.0＋的shortcut，如下图  
![](54.png)  
第二条是第三方工具，却需要root  
![](55.png)  
很明显这些方式固然方便，却也有弊端，喜欢通过魔改安装包解决问题的琴梨梨当然更愿意选择通过修改安装包实现  
今天我们以微信为例，给微信添加独立的扫一扫快捷方式。  
首先我们要进行一些准备工作  
pre1:挖出扫一扫图标的arsc编号  
方法很简单，翻res文件夹找扫一扫图标，不过微信做了资源混淆，如果要方便找最好要用电脑反编译再正常回编译一次  
![](56.png)  
然后去arsc里搜索对应路径和文件名，找到文件后长按复制  
![](57.png)  
琴梨梨的a屏黑版微信，扫一扫的编号是7F0205D6  
这个先留着，一会要用  
pre2:保存下面的代码到剪贴板，一会要用  
>             <intent-filter>  
>                 <action  
>                     android:name="android.intent.action.MAIN" />  
>                 <category  
>                     android:name="android.intent.category.LAUNCHER" />  
>             </intent-filter> 
>             <intent-filter>  
>                 <action  
>                     android:name="android.intent.action.MAIN" />  
>                 <category  
>                     android:name="android.intent.category.LEANBACK_LAUNCHER" />  
>             </intent-filter>  
>         </activity>  

pre3:(可选)找到扫一扫的strings编号  
arec里直接搜索然后复制编号就行，琴梨梨发现的编号是7F080967，不同版本可能不同  
![](58.png)  
pre4:获取扫一扫的活动名  
打开扫一扫，然后用开发者助手复制活动名即可  
6.5.16版本的活动名是com.tencent.mm.plugin.scanner.ui.BaseScanUI  
![](59.png)  
接下来开始动手操作吧！  
step1打开manifest文件，搜索扫一扫活动  
它很容易被找到  
![](60.png)  
step2去除括号前的斜杠和空格，在括号后把pre2里的代码插进去  
![](61.png)  
step3在android:theme下面键入以下内容  
>             android:label="@7F080967"  
>             android:icon="@7F0205D6"  

label后面的编号就是扫一扫strings的编号，当然你也可以直接引号里打扫一扫，不过从规范的角度来看不推荐这么做  
icon后面的编号是扫一扫图标的编号  
注意输编号时要加个@  
![](62.png)  
step4保存，安装(如果没有核心破解那就别忘了签名)  
![](63.png)  
安装完返回桌面看看是不是多了一个扫一扫图标  
![](64.png)  
点开它，稍等让微信载入完，就能直接进入扫一扫而不进入主界面，载入也更快一些，如果微信允许后台，那么还能实现秒进，是不是很好用？  
最后放上微信和支付宝快捷方式的合影  
![](65.png)  
不过值得注意的是，某些定制rom的默认启动器并不允许单个app创建多个图标，对于那些rom，解决办法很简单，那就是刷tnd，不要怂尽管刷  
![](66.png)  












[⇦]: ../../list.md